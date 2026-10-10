# Projektanweisungen

## Befehle `cmsd` und `cmsd+p`

Wenn der Nutzer `cmsd` schreibt, ist das ein ausdrücklicher Auftrag, die
Änderungen der aktuellen Aufgabe lokal zu committen. `cmsd` bedeutet
"Commit mit Summary und Description". Ein Push gehört nicht dazu.

Wenn der Nutzer `cmsd+p` schreibt, gilt derselbe Commit-Ablauf. Anschließend
die aktuelle Branch mit einem normalen `git push` zum eingerichteten Upstream
auf GitHub pushen. Niemals einen Force-Push verwenden. Ist kein Upstream
eingerichtet oder schlägt der Push fehl, den Commit bestehen lassen und das
Problem klar melden; keinen Push-Zielort erraten.

Vor dem Commit `git status` und den Diff prüfen. Nur Änderungen stagen, die
zur aktuellen Aufgabe gehören; fremde oder unklare Änderungen nicht
einbeziehen. Für den Commit eine kurze, passende deutsche Summary und eine
deutsche Description mit den wesentlichen Änderungen verwenden.

Nach dem Commit den Hash und den Status nennen; bei `cmsd+p` auch das
Push-Ergebnis. Summary und Description zusätzlich in zwei getrennten, leicht
kopierbaren Blöcken ausgeben. Ohne ausdrücklichen Commitauftrag keinen Commit
erstellen und ohne `cmsd+p` oder andere ausdrückliche Aufforderung nicht
pushen.
