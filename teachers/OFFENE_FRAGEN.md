# Offene Fragen zum Prompt Generator für Lehrkräfte

Stand: 9. Oktober 2026. Dieses Dokument hält Entscheidungen und noch offene
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
