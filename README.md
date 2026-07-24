# Prompt Generator

Ein didaktisches Web-Tool zur Erstellung von Sprachlern-Prompts für KI-Sprachmodelle, orientiert am Gemeinsamen Europäischen Referenzrahmen für Sprachen (GER/CEFR).

**Live:** [promptgenerator.site](https://promptgenerator.site)

## Struktur

```
index.html                    Hauptversion (14 Sprachen)
gi-telaviv/index.html         White-Label-Fork für Goethe-Institut Tel Aviv (10 Sprachen)
wifi/index.html                White-Label-Fork für WIFI Vorarlberg (14 Sprachen)
impressum.html                 Rechtliche Pflichtangaben
datenschutz.html               Datenschutzerklärung (DSGVO)
nutzungsbedingungen.html       Nutzungsbedingungen
logo.jpg / wifi-logo.jpg       Logos für Social-Media-Vorschau (Meta-Tags)
```

## Technik

- Reines Vanilla JavaScript, keine Build-Pipeline, keine Dependencies
- Alle Inhalte (Übersetzungen, Themenpakete, Vokabeln) liegen in einem zentralen `DATA`-Objekt pro Sprache im `<script>`-Block
- Analytics: [Plausible](https://plausible.io) (cookiefrei, DSGVO-konform ohne Consent-Banner)
- Hosting: [Netlify](https://netlify.com)

## Sprachen

Deutsch, Englisch, Französisch, Italienisch, Portugiesisch, Spanisch, Russisch, Türkisch, Arabisch, Hebräisch, Chinesisch, Koreanisch, Ungarisch, Japanisch

Die Themenpakete (61 Kategorien, 183 Sprechsituationen) sind aktuell nur für Deutsch und Englisch vollständig übersetzt; die übrigen Sprachen nutzen deutsche Themen als Platzhalter.

## Deploy

Manuelles Deploy via Netlify (Drag & Drop des Repo-Root-Ordners oder Netlify CLI). Automatisches CI/CD via Git-Push ist noch nicht eingerichtet.

## Lizenz / Rechtliches

© Ingo Schönleber. Alle Rechte vorbehalten. Details siehe `impressum.html`, `datenschutz.html`, `nutzungsbedingungen.html`.
