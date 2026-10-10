# Fehlerdichte und Flüssigkeitsindex

Stand: 10. Oktober 2026. Dies sind vorläufige Regeln für die Auswertung von
Gesprächstranskripten, keine Prüfungsnoten oder GER-Einstufungen.

## Fehlerdichte für alle Transkriptarten

Die auswertende KI zählt je Person belegte Grammatik- und Wortschatzfehler
getrennt. Grammatik umfasst Formen, Artikel, Kasus, Endungen, Zeiten und
Satzbau; Wortschatz umfasst falsche oder fehlende Inhaltswörter und unpassende
Wendungen. Eine Fehlerstelle zählt nur einmal, auch wenn beide Kategorien
denkbar wären. Wiederholte Vorkommen zählen erneut; vermutete
Spracherkennungsfehler und bloße Stilpräferenzen nicht.

Nur Wörter der lernenden Person zählen. Bei Skriptdateien ist die ausgewiesene
Wortzahl ohne Zögerungslaute der Nenner; maskierte, tatsächlich gesprochene
Wörter sind darin enthalten, aber Platzhalter gelten nicht als Fehler. Bei
KI-App-Transkripten zählt die auswertende KI die Wörter ohne Fülllaute,
Platzhalter und Zeitmarken selbst.

```
Grammatik pro 100 Wörter = 100 * Grammatikfehler / Wörter
Wortschatz pro 100 Wörter = 100 * Wortschatzfehler / Wörter
Gesamtfehlerdichte = 100 * (Grammatikfehler + Wortschatzfehler) / Wörter
```

Erst die Endwerte werden auf eine Dezimalstelle gerundet. Die Gesamtfehlerdichte
ist eine Fehlerzahl, keine umgekehrte Korrektheitspunktzahl. Bei weniger als
50 Wörtern steht ein Warnhinweis, bei null auswertbaren Wörtern kein Wert.
Automatische Transkription kann Fehler glätten; niedrige Fehlerdichte beweist
deshalb nicht fehlerfreies Sprechen.

## Flüssigkeitsindex nur für Skriptdateien

Die beiden Python-Varianten des Transkriptionsskripts berechnen einen
vorläufigen Index von 0 bis 100 aus ungerundeten Rohwerten (ab Skriptversion
2.5). Der Lehrer-Prompt
übernimmt den Wert nur aus der Datei; ältere Dateien ohne Index werden nicht
nachträglich aus gerundeten Tabellenwerten berechnet.

Für jeden Messwert gilt eine festgehaltene Pilotgrenze `a..b`:
`N_auf(x) = 100 * clamp((x-a)/(b-a), 0, 1)` und
`N_ab(x) = 100 - N_auf(x)`. Höhere Teilwerte bedeuten den im Pilotmodell
günstigeren Bereich; jenseits der Grenzen gibt es keine Extrapunkte oder
weiteren Abzüge.

| Teilwert | Berechnung mit Pilotgrenzen |
| --- | --- |
| Tempo `T` | `N_auf(Artikulationsrate; 60..160 Wörter/Minute)` |
| Pausen/Fluss `P` | `0,50 * N_ab(Pausen/Minute; 2..12) + 0,20 * N_ab(lange Pausen/Minute; 0..4) + 0,30 * N_auf(Wörter zwischen Pausen; 2..10)` |
| Unterbrechungen `U` | `0,50 * N_ab(Zögerungslaute/100 Wörter; 0..20) + 0,50 * N_ab(direkte Wortwiederholungen/100 Wörter; 0..6)` |

`Flüssigkeitsindex = runden(0,40 * T + 0,45 * P + 0,15 * U)`.
Lange Pausen pro Minute werden aus der Zahl langer Pausen und der Sprechzeit
der lernenden Person berechnet. Sprechrate wird separat gezeigt, aber nicht
zusätzlich gewichtet, da sie Tempo und Pausen bereits vermischt. Reaktionszeit,
Wortschatzvielfalt und Gesprächspartikeln gehen nicht in den Index ein.

Bei weniger als 50 Wörtern, nicht messbarer Sprechzeit, ausgeschalteter
Stimmtrennung oder unsicherer Stimmzuordnung wird kein Index ausgewiesen.
Für Zeitvergleiche sollen Aufgabe,
Skriptversion, Whisper-Modell und Aufnahmebedingungen möglichst gleich bleiben.
Die Pilotgrenzen und Gewichte sind **nicht empirisch kalibriert**. Der Index
ersetzt kein Nachhören und keine Beurteilung durch die Lehrkraft.

Die Auswahl von Artikulationsrate, Pausen und Reparaturmerkmalen folgt der
[Forschung zu mehreren Dimensionen der Sprechflüssigkeit](https://www.cambridge.org/core/journals/studies-in-second-language-acquisition/article/multidimensionality-of-second-language-oral-fluency-interfacing-cognitive-fluency-and-utterance-fluency/517AD8890EBDEA32B3557891B6D589E8).
Die konkreten Gewichte und Pilotgrenzen sind dagegen eigene, noch zu prüfende
Produktentscheidungen.
