# FHEM PID20 - Fehlerkorrigierte Version (V1.0.0.14)

Dieses Repository enthält eine aktiv gepflegte und korrigierte Community-Version des originalen FHEM-Moduls `98_PID20.pm`.

### Behobene Fehler & neue Features:
* **D-Anteil Vorzeichen-Fehler (Fix in V1.0.0.13):** Bei Aktivierung von `pidReverseAction = 1` (z. B. Kühlbetrieb) rechnete der D-Anteil mit dem falschen Vorzeichen und wirkte als Mitkopplung, was die Regelung destabilisierte. Der D-Anteil dämpft nun in beiden Modi mathematisch korrekt (Gegenkopplung).
* **Mittelwert-Filter für D-Anteil (Neu in V1.0.0.14):** Über das neue, optionale Attribut `pidDPortionFilter` kann ein gleitender Mittelwert über die letzten X Gradienten berechnet werden. Dies beruhigt den zappeligen D-Anteil bei schnellen Temperaturänderungen oder Messwertrauschen an trägen Systemen (z. B. Fußbodenheizungsmischern) und verhindert das Aufschwingen des Reglers.

### Installation in FHEM:

Um dieses Modul live von GitHub auf deinem FHEM-Server zu installieren und die alte Version dauerhaft zu überschreiben, gib einfach folgenden Befehl in die FHEM-Kommandozeile (FHEM-Cmd) ein:

{ GetFileFromURL("https://githubusercontent.com", undef, undef, 1, undef, "/opt/fhem/FHEM/98_PID20.pm") }

Aktivierte danach das Modul ohne FHEM-Neustart im laufenden Betrieb:

reload 98_PID20

### Neues Attribut nutzen (optional):
Um den D-Anteil-Mittelwert-Filter für ein Device zu aktivieren (z. B. Glättung über die letzten 10 Messwerte), setze einfach das neue Attribut:

attr <dein_mischer_device> pidDPortionFilter 10
