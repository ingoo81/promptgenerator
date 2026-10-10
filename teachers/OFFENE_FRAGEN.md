# Offene Fragen zum Prompt Generator für Lehrkräfte

Stand: 10. Oktober 2026. Dieses Dokument hält Entscheidungen und noch offene
Folgefragen fest; es ist keine Liste bereits beschlossener Änderungen.

## Feedback für alle Lernenden auf einmal

**Entscheidung:** Der Feedback-Prompt soll alle im Transkript enthaltenen
Lernenden in einer Antwort bearbeiten. Die frühere Aufteilung in Runden zu je
fünf Personen wurde am 9. Oktober 2026 entfernt. Fünf war nie eine Grenze für
die Anzahl der Lernenden, sondern nur die Größe einer Ausgabe-Runde.

**Hintergrund der Diskussion:** Die Runden sollten lange KI-Antworten und
abgeschnittene Ausgaben vermeiden. Sie verlangten aber wiederholte
„weiter“-Eingaben. Die Lehrkraft lässt die individuellen Übungen automatisch
erstellen und verteilt sie anschließend als HTML oder Link; sie muss nicht jede
Feedback-Runde als eigenen Arbeitsschritt sehen. Daher ist eine vollständige
Antwort der gewünschte Standard. Der Prompt nennt am Ende Anzahl und Codes
oder Namen, damit die Lehrkraft die Vollständigkeit prüfen kann.

**Noch zu klären:** Wie verhalten sich die verwendeten KI-Modelle bei sehr
großen Gruppen, langen Transkripten und vielen individuellen Übungen? Falls
Antworten abgeschnitten werden, brauchen wir eine erkennbare Warnung und eine
praktische Fortsetzung, ohne wieder eine feste Fünfer-Aufteilung für alle
einzuführen. Auch die anschließende Erstellung einer einzigen interaktiven
HTML-Seite kann an Ausgabelimits stoßen.

## Dynamische Anzahl individueller Übungen

Bei längeren Transkripten könnten mehr belegte Fehlerbereiche und damit mehr
persönliche Übungen sinnvoll sein. Noch offen sind die Regel für die Anzahl
pro Person, eine Obergrenze und der Umgang mit kurzen oder fehlerarmen
Transkripten. Die Übungen sollen automatisch erstellt und per Link oder HTML
verteilt werden; ihre Anzahl ist daher keine Frage der manuellen Korrekturzeit
der Lehrkraft. Eine feste Begrenzung auf fünf Lernende ist dafür nicht
vorgesehen.

## Verhältnis von Grammatik und Wortschatz in Gruppenübungen

**Entscheidung:** In Schritt 4 kann die Lehrkraft zwischen einer automatischen
Verteilung und festen Richtwerten von 100/0, 75/25, 50/50, 25/75 oder 0/100
für Grammatik/Wortschatz wählen. Die Anteile beziehen sich auf einzelne
Aufgaben, nicht auf ganze Übungsblöcke. Ohne genügend belegte Fehler soll die
KI weniger Aufgaben erstellen und die Abweichung nennen.

**Noch zu prüfen:** Ergeben die festen Verhältnisse bei echten Transkripten
eine sinnvolle Aufgabenverteilung, besonders bei wenigen Aufgaben und bei
Mischfällen wie falschen Artikeln? Hält die KI dabei die Belegpflicht ein,
statt fehlende Fehler zu erfinden oder stillschweigend durch Aufgaben des
anderen Bereichs zu ersetzen? Die Ausgaben für alle gewählten Übungsformate
an kurzen und längeren Transkripten vergleichen.

## Fehlerdichte und Flüssigkeitsindex

**Entscheidung:** Für jede Person werden Grammatik- und Wortschatzfehler pro
100 Wörter getrennt und als Gesamtfehlerdichte ausgewiesen, unabhängig von
der Transkriptart. Es gibt keine Korrektheitspunktzahl. Bei Dateien des
Transkriptionsskripts kommt ein vorläufiger Flüssigkeitsindex von 0 bis 100
hinzu, der im Skript aus Tempo, Pausen und Unterbrechungen berechnet wird.
Formeln, Pilotgrenzen und Einschränkungen stehen in `KENNZAHLEN.md`.

**Noch zu prüfen:** Die Pilotgrenzen und Gewichte mit ausreichend echten,
unterschiedlichen Aufnahmen und menschlichen Einschätzungen kalibrieren.
Insbesondere prüfen, ob der Index sinnvolle Sprechpausen zu stark bestraft,
ob Whisper Zögerungslaute und Wiederholungen zuverlässig erfasst und wie
stabil die Werte bei verschiedenen Aufgaben, Längen und Spracherkennungsmodellen
sind. Die Fehlerzählung der KI anhand manuell markierter Transkripte prüfen:
Wortzahl bei App-Transkripten, Grenzfälle zwischen Grammatik und Wortschatz,
fehlende Wörter und mögliche Erkennungsfehler. Eine niedrige Fehlerdichte oder
ein hoher Index darf nicht als Nachweis für ein bestimmtes Sprachniveau gelten.
