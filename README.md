# FHEM PID20 - Fehlerkorrigierte Version

Dieses Repository enthält eine korrigierte Version des originalen FHEM-Moduls `98_PID20.pm`.

### Behobene Fehler:
* **D-Anteil Vorzeichen-Fehler:** Bei Aktivierung von `pidReverseAction = 1` (z. B. Kühlbetrieb) rechnete der D-Anteil mit dem falschen Vorzeichen und destabilisierte die Regelung. Dies wurde behoben.

### Installation in FHEM:
Füge einfach folgende Zeile in deine FHEM-Befehlszeile (FHEM-Cmd) ein, um dieses Repository hinzuzufügen:

update add https://githubusercontent.com

Danach kannst du das Modul ganz normal über den FHEM-Befehl updaten:

update
