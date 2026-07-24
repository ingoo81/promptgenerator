---
description: Strukturelle Konsistenzprüfung der drei Forks (main, gi-telaviv, wifi)
---

# Strukturelle Konsistenzprüfung der drei Forks

Prüfe `index.html`, `gi-telaviv/index.html` und `wifi/index.html` auf strukturelle
Konsistenz. Dies ist eine **reine Analyseaufgabe – niemals eine Datei verändern**,
nur lesen und vergleichen.

Geprüft wird pro vorhandener Sprache:
1. **Themenkategorien** – Anzahl pro Niveau (A1–C2) und gesamt
2. **Akkordeon-Optionen** – Anzahl der Akkordeon-Items und Optionen pro Schlüssel (fok, ro, di, gd, kf, ko)
3. **Nachbereitungs-Optionen** (nb) und **Nächste-Schritte-Optionen** (ha)
4. **Sprachnamen-Übersetzungen** (`LANG_NAME_TRANS`)

Zusätzlich: **UI-angebotene Sprachen (`LANG_OPTIONS`) vs. vorhandene `DATA`** –
verwaiste Sprachdaten aufdecken.

## Ausführung

Führe vom Projekt-Root aus exakt dieses Skript aus (Git Bash / Bash-Tool):

```bash
python - <<'PY'
import json, re, os, sys
try:
    sys.stdout.reconfigure(encoding='utf-8')  # Windows-Konsole: CJK/Umlaute nicht crashen
except Exception:
    pass

FILES = {"main": "index.html", "gi-telaviv": "gi-telaviv/index.html", "wifi": "wifi/index.html"}

def extract_literal(text, varname):
    m = re.search(r'var\s+' + re.escape(varname) + r'\s*=\s*', text)
    if not m:
        return None
    i = m.end()
    while i < len(text) and text[i] in ' \t\r\n':
        i += 1
    start = i; depth = 0; ins = False; esc = False; q = ''
    while i < len(text):
        c = text[i]
        if ins:
            if esc: esc = False
            elif c == chr(92): esc = True
            elif c == q: ins = False
        else:
            if c == '"' or c == "'":
                ins = True; q = c
            elif c in '{[': depth += 1
            elif c in '}]':
                depth -= 1
                if depth == 0:
                    return text[start:i+1]
        i += 1
    return None

def lang_options(text):
    lit = extract_literal(text, 'LANG_OPTIONS') or ''
    return re.findall(r'code:\s*"([a-z]{2})"', lit)

def analyze(path):
    text = open(path, encoding='utf-8').read()
    out = {"errs": []}
    dl = extract_literal(text, 'DATA')
    ll = extract_literal(text, 'LANG_NAME_TRANS')
    try:
        DATA = json.loads(dl)
    except Exception as e:
        out["errs"].append("DATA parse FAIL: %s" % e); return out
    try:
        LNT = json.loads(ll)
    except Exception as e:
        out["errs"].append("LANG_NAME_TRANS parse FAIL: %s" % e); return out
    out["ui_langs"] = lang_options(text)
    out["data_langs"] = sorted(DATA.keys())
    out["lnt_langs"] = sorted(LNT.keys())
    langs = {}
    for lang, d in DATA.items():
        themes = d.get('themes', {}) or {}
        acc = nb = ha = None
        for st in (d.get('steps', []) or []):
            if isinstance(st, dict):
                if 'accordion' in st: acc = st['accordion']
                if 'nb' in st: nb = st['nb']
                if 'ha' in st: ha = st['ha']
        langs[lang] = {
            "steps": len(d.get('steps', []) or []),
            "cat_per_niv": {n: len(themes[n]) for n in sorted(themes)},
            "cat_total": sum(len(themes[n]) for n in themes),
            "cat_names": {n: [c.get('cat') for c in themes[n]] for n in sorted(themes)},
            "acc_count": len(acc) if acc is not None else None,
            "acc_opts": [(it.get('key'), len(it.get('opts', []))) for it in acc] if acc else None,
            "nb": nb, "nb_count": len(nb) if nb is not None else None,
            "ha": ha, "ha_count": len(ha) if ha is not None else None,
            "niv_count": len(d.get('niv', []) or []),
            "lnt_count": len(LNT.get(lang, {})) if lang in LNT else None,
        }
    out["langs"] = langs
    return out

report = {f: analyze(p) for f, p in FILES.items()}

# Print machine-readable-ish structured findings
DEV = []  # deviations

for fork, r in report.items():
    if r["errs"]:
        print("### %s: FEHLER: %s" % (fork, r["errs"]))
        DEV.append((fork, "-", "; ".join(r["errs"])))
        continue
    print("[%s] DATA=%d %s | UI=%d %s | LNT=%d" % (
        fork, len(r["data_langs"]), ",".join(r["data_langs"]),
        len(r["ui_langs"]), ",".join(r["ui_langs"]), len(r["lnt_langs"])))
    langs = r["langs"]
    base = langs.get("de")
    # within-fork per-language vs de
    for lang in sorted(langs):
        if lang == "de":
            continue
        # NUR strukturelle Zähler pro Sprache vergleichen – NICHT übersetzte
        # Inhalte wie cat_names/nb/ha (die unterscheiden sich sprachbedingt).
        i = langs[lang]
        for field in ["steps", "cat_total", "cat_per_niv",
                      "acc_count", "acc_opts", "nb_count", "ha_count",
                      "niv_count", "lnt_count"]:
            if i[field] != base[field]:
                DEV.append((fork, lang, "%s: %r != de %r" % (field, i[field], base[field])))
    # LNT langs must equal DATA langs
    if r["lnt_langs"] != r["data_langs"]:
        DEV.append((fork, "*", "LNT-Sprachen != DATA-Sprachen: LNT=%s DATA=%s" % (r["lnt_langs"], r["data_langs"])))
    # UI vs DATA orphans
    orphans = sorted(set(r["data_langs"]) - set(r["ui_langs"]))
    missing = sorted(set(r["ui_langs"]) - set(r["data_langs"]))
    if orphans:
        print("    HINWEIS %s: DATA ohne UI-Karte (verwaist): %s" % (fork, ",".join(orphans)))
    if missing:
        DEV.append((fork, "*", "UI-Sprache OHNE DATA (defekt!): %s" % ",".join(missing)))

# cross-fork de baseline comparison
print("-" * 60)
ref = None
for fork, r in report.items():
    if r["errs"]:
        continue
    b = r["langs"]["de"]
    sig = (b["cat_per_niv"], b["cat_names"], b["acc_opts"], b["nb"], b["ha"])
    if ref is None:
        ref = (fork, sig)
    elif sig != ref[1]:
        DEV.append((fork, "de", "Cross-Fork: de-Baseline weicht von %s ab" % ref[0]))

print("=" * 60)
if DEV:
    print("ABWEICHUNGEN (%d):" % len(DEV))
    for fork, lang, msg in DEV:
        print("  [%s / %s] %s" % (fork, lang, msg))
else:
    print("KEINE ABWEICHUNGEN – alle drei Forks strukturell konsistent.")
    print("(Sprach-Umfang je Fork ist by design unterschiedlich; verwaiste DATA-Sprachen siehe HINWEIS oben.)")
PY
```

## Ausgabe

Lies die Skript-Ausgabe und präsentiere dem Nutzer:

- **Falls `KEINE ABWEICHUNGEN`:** Sag klar, dass alle drei Forks in den vier Dimensionen
  vollständig konsistent sind. Zeige eine kompakte Übersichtstabelle (Fork · Sprachanzahl ·
  Themenkategorien gesamt · Akkordeon-Items · nb · ha). Erwähne verwaiste DATA-Sprachen
  (HINWEIS-Zeilen) nur als Info, nicht als Fehler.
- **Falls Abweichungen:** Gib eine kompakte Markdown-Tabelle **sortiert nach Fork und Sprache**
  mit Spalten: Fork · Sprache · betroffene Dimension · Abweichung.
- **Falls ein FEHLER** beim Parsen auftritt (z. B. eine Datei lässt sich nicht als JSON lesen):
  melde das prominent zuerst und brich die Bewertung für den betroffenen Fork ab.

Verändere unter keinen Umständen eine der geprüften Dateien.
