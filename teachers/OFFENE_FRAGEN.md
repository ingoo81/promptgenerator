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

**Entscheidung zur Fortsetzung:** Bricht das Feedback ab, bietet der Generator
einen optionalen Folgeauftrag im selben Chat an. Die KI soll nur die fehlenden
Personen bearbeiten und ein zuletzt angefangenes, unvollständiges Feedback
vollständig neu ausgeben. Eine feste Fünfer-Aufteilung wird nicht eingeführt.

**Noch zu klären:** Wie verhalten sich die verwendeten KI-Modelle bei sehr
großen Gruppen, langen Transkripten und vielen individuellen Übungen? Die
Vollständigkeitsangaben und der Folgeauftrag müssen mit echten Ausgaben
getestet werden. Auch die anschließende Erstellung interaktiver HTML-Seiten
kann an Ausgabelimits stoßen. Für die Übungsseiten gilt deshalb
vorläufig: bis zu 20 einzeln zu beantwortende Aufgaben in einer Datei; darüber
werden ganze Personen auf möglichst wenige eigenständige Dateien verteilt.
Eine Person wird nie aufgeteilt, auch wenn sie allein mehr als 20 Aufgaben hat.
Das ist eine Grenze für die Ausgabe, keine Fünfer-Grenze für die Auswertung.
Jede Datei bekommt eine nur für die Lehrkraft sichtbare Übersicht mit Anzahl
der Aufgaben und enthaltenen Codes. Wenn die Ausgabe nicht vollständig in eine
KI-Antwort passt, werden weitere komplette Dateien nach „weiter“ ausgegeben.
Die Grenze von 20 Aufgaben und die Vollständigkeit der erzeugten Dateien sind
mit echten Gruppen noch zu prüfen.

## Dynamische Anzahl individueller Übungen

**Entscheidung:** Bei individuellen Übungen zählt jede kurze,
einzeln zu beantwortende Aufgabe als eine Übung, nicht ein Block mit mehreren
Teilaufgaben. Auch die vorläufige Grenze von 20 Aufgaben pro HTML-Datei zählt
in dieser Einheit. Die Gruppenübungen dürfen weiterhin aus Blöcken mit
mehreren Aufgaben bestehen.

**Vorläufige Regel:** In Schritt 4 wählt die Lehrkraft die Bearbeitungszeit
pro Person statt einer festen Zahl von 2 oder 4 Übungen. Der Prompt rechnet
konservativ mit etwa 45 Sekunden pro kurzer Einzelaufgabe. Die Anzahl wird
zusätzlich auf die eigenständigen, im Transkript belegten Fehlerstellen dieser
Person begrenzt: eine Aufgabe je Fehlerstelle; wiederholte Fehler zählen nur
bei mehreren tatsächlichen Stellen. Bei kurzen oder fehlerarmen Transkripten
entstehen entsprechend weniger Aufgaben. Die Lehrkraft verteilt diese per Link
oder HTML, sie korrigiert nicht jede Aufgabe selbst. Eine feste Begrenzung auf
fünf Lernende ist nicht vorgesehen.

**Noch zu prüfen:** Passt der Richtwert von 45 Sekunden bei authentischen
Aufgaben und Lernenden? Führen längere Transkripte zu einer sinnvollen Zahl
verschiedener Aufgaben, ohne dass die Feedback-Ausgabe oder HTML-Dateien zu
lang werden? Gegebenenfalls Zeitoptionen und Zählregel nach den Praxistests
anpassen.

## Verhältnis von Grammatik und Wortschatz in Gruppenübungen

**Entscheidung:** In Schritt 4 kann die Lehrkraft zwischen einer automatischen
Verteilung und festen Richtwerten von 100/0, 75/25, 50/50, 25/75 oder 0/100
für Grammatik/Wortschatz wählen. Die Anteile beziehen sich auf einzelne
Aufgaben, nicht auf ganze Übungsblöcke. Ohne genügend belegte Fehler soll die
KI weniger Aufgaben erstellen und die Abweichung nennen. Mischfälle zählen
genau einmal nach dem hauptsächlichen Lernziel der Aufgabe: Das Üben von
Artikelformen oder Kongruenz ist Grammatik, ein neues Nomen mit seinem festen
Artikel zu lernen ist Wortschatz, sofern die Unterscheidung in der Zielsprache
relevant ist.

**Noch zu prüfen:** Ergeben die festen Verhältnisse bei echten Transkripten
eine sinnvolle Aufgabenverteilung, besonders bei wenigen Aufgaben und bei
Mischfällen wie falschen Artikeln? Hält die KI die Zuordnungsregel und die
Belegpflicht ein,
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
