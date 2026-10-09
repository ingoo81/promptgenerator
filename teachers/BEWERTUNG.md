# Orientierungspunktzahl aus Gesprächstranskripten

Stand: 9. Oktober 2026. Die Regeln werden in `teachers/index.html` unter
`BEWERTUNGSRUBRIKEN` und `bewertungsRegeln` als Teil des Auswertungs-Prompts
erzeugt. Die Punktzahl ist relativ zum eingestellten Zielniveau. Sie ist **kein
Goethe-Prüfungsergebnis** und keine automatisch festgestellte GER-Stufe.

## Offizielle Ausgangspunkte

Die Goethe-Prüfungen bewerten mehrere vorgegebene Aufgaben und Kriterien mit
festgelegten Punktwerten; zwei Prüfende bewerten unabhängig. Aussprache ist
ein eigenes Kriterium. Grundlage sind die offiziellen Erwachsenen-Modellsätze
und Durchführungsbestimmungen:

| Niveau | Offizielle mündliche Wertung | Quelle |
| --- | --- | --- |
| A1: Start Deutsch 1 | Drei Teile mit 3 + 6 + 6 = 15 Rohpunkten. Je Sprachhandlung volle, halbe oder keine Punkte nach Aufgabenerfüllung und Verständlichkeit; die Gesamtprüfung gewichtet den mündlichen Teil mit Faktor 1,66 auf ungefähr 25 Punkte. | [Durchführungsbestimmungen](https://www.goethe.de/pro/relaunch/prf/bg/Durchfuehrungsbestimmungen_A1_Start_Deutsch_1.pdf), [Prüfungsziele und Testbeschreibung](https://www.goethe.de/pro/relaunch/prf/en/Pruefungsziele_Testbeschreibung_A2_SD2.pdf) |
| A2 | Aufgabenerfüllung und Sprache je 2 + 4 + 4 = 10 Punkte, Aussprache 5; insgesamt 25. | [Modellsatz](https://www.goethe.de/pro/relaunch/prf/materialien/A2/A2_Modellsatz_Erwachsene.pdf) |
| B1 | Aufgabenerfüllung 36, Interaktion/Kohärenz 8, Wortschatz/Register 20, Strukturen 20, Aussprache 16; insgesamt 100. | [Modellsatz](https://bfu.goethe.de/b1_mod/sprechen.php) |
| B2 | Aufgabenerfüllung 18, Kohärenz 8, Wortschatz 18, Strukturen 22, Fragen/Antworten 8, Interaktion 10, Aussprache 16; insgesamt 100. | [Modellsatz](https://www.goethe.de/pro/relaunch/prf/materialien/B2/b2_modellsatz_erwachsene.pdf) |
| C1 | Aufgabenerfüllung 14, Kohärenz 10, Wortschatz 20, Strukturen 22, Fragen/Antworten 8, Interaktion 10, Aussprache 16; insgesamt 100. | [Modellsatz](https://www.goethe.de/pro/relaunch/prf/materialien/C1_modular/c1-modular_modellsatz.pdf) |
| C2 | Zwei Teile mit je fünf Kriterien zu je 4 Punkten; vier sprachlich-inhaltliche Kriterien und Aussprache. Das amtliche Ergebnis multipliziert 40 Rohpunkte mit 2,5. | [Modellsatz](https://www.goethe.de/pro/relaunch/prf/materialien/C2/c2_modellsatz.pdf) |

Für A1 ist besonders wichtig: Die Verständlichkeit entscheidet, nicht die
bloße Fehlerzahl. Auch grammatisch unvollkommene, aber verständliche und
aufgabengerechte Äußerungen können volle Punkte bekommen. Die Stufen A–E bei
A2–C1 sind **Kriteriumsstufen**, keine fertigen Gesamtnoten.

## Übertragung auf ein Transkript

- Ein KI-Gespräch ist keine Goethe-Prüfung: Die amtlichen Aufgabenteile fehlen.
  Deshalb beziehen sich Aufgabenerfüllung, Antwortverhalten und Interaktion
  ausschließlich auf die von der Lehrkraft angegebene Gesprächsaufgabe.
- Aussprache und Intonation entfallen vollständig. Auch Pausen, Tempo und
  Sprechflüssigkeit gehen nicht in diese Punktzahl ein, selbst wenn ein
  Transkript Zeitmarken enthält. Spracherkennung kann Merkmale glätten.
- A1: Jede eigenständige, aufgabenbezogene Sprachhandlung erhält 1, 0,5 oder
  0. Die Punktzahl ist `runden(100 * Summe / Anzahl Sprachhandlungen)`.
- A2–C1: Die oben genannten Gewichte ohne Aussprache werden beibehalten. Jedes
  Kriterium erhält einen der Anteile A=100 %, B=75 %, C=50 %, D=25 %, E=0 %
  seines Gewichts. Die Punktzahl ist `runden(100 * gewichtete Summe / 20)`
  für A2 bzw. `runden(100 * gewichtete Summe / 84)` für B1–C1. Erst das
  Endergebnis wird auf ganze Punkte gerundet. Beispiel B1: A/B/C/B für die
  vier Kriterien ergibt `(36 + 6 + 10 + 15) / 84 * 100 = 80` Punkte gerundet.
  Ist die Aufgabenerfüllung belegbar auf Stufe E, erhält die gesamte
  Gesprächsaufgabe 0 Punkte. Fehlende Daten sind dagegen nicht bewertbar.
- C2 bleibt als Zielniveau im Generator verfügbar. Analog zum offiziellen
  C2-Bogen werden Aufgabenerfüllung, Kohärenz, Wortschatz und Strukturen mit
  gleichem Gewicht bewertet; Aussprache entfällt. Der Nenner ist 32.
- Für andere Zielsprachen als Deutsch ist das eine **übertragene didaktische
  Rubrik**, keine Goethe-Bewertung dieser Sprache.

Die KI gibt je Person **nur eine Zahl von 0 bis 100** und einen kurzen Beleg
aus. Die Kriteriumsstufen und Rohpunkte sind Rechenschritte, keine zusätzlichen
Noten in der Ausgabe. Sie soll nicht bewertbar ausgeben, wenn ein substantieller
eigener Gesprächsanteil oder verlässliche Zuordnung/Transkription fehlt. Null
Punkte stehen für belegtes Scheitern, nicht für fehlende Daten.
Direkt unter der Ergebnistabelle steht einmalig ein kurzer Hinweis auf die
Orientierung an den Kriterien der mündlichen Goethe-Prüfungen, den Ausschluss
der Aussprache und den Unterschied zu einem offiziellen Prüfungsergebnis.

## Grenzen und Vergleich über die Zeit

Die Punktzahl ist eine grobe Lehrkraft-Orientierung, keine kalibrierte Messung.
Die KI ersetzt weder zwei geschulte Prüfende noch eine Hörprobe. Sie soll nur
belegte Merkmale bewerten und keine Strukturen oberhalb des Zielniveaus
verlangen oder belohnen. Bei Spracherkennung können gerade Endungen fehlen oder
geglättet sein. Ergebnisse verschiedener Zielniveaus sind nicht direkt
vergleichbar: 80/100 auf A2 und 80/100 auf B2 bezeichnen unterschiedliche
Ansprüche. Auch bei gleichem Zielniveau beeinflussen Aufgabenart,
Schwierigkeit, Gesprächslänge, verwendete KI und Transkriptionsmodell den
Vergleich. Für eine Zeitreihe sollten diese Bedingungen möglichst konstant
bleiben und auffällige Veränderungen an der Aufnahme gegengeprüft werden.
