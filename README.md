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

### Hinweiß solage die neue Version nicht offiziel teil von FHEM ist :
Aber Vorsicht bei zukünftigen FHEM-Updates!Es gibt einen wichtigen Unterschied für die Zukunft. Wenn ein User (oder du selbst) später wieder ein ganz normales, allgemeines update in FHEM ausführt, passiert folgendes:Ohne das globale Attribut: FHEM gleicht alle Dateien mit dem offiziellen FHEM-Server ab. Da dort für das originale Modul immer noch das Jahr 2025 hinterlegt ist, denkt FHEM, deine Version auf der Festplatte sei fehlerhaft oder verändert worden. FHEM wird deine mühsam installierte Version 1.0.0.14 beim nächsten großen Update einfach wieder mit dem alten Original (1.0.0.12) überschreiben.Meine Empfehlung für die README / Forum:Damit die Version 1.0.0.14 dauerhaft auf dem System geschützt bleibt, solltest du den Usern (und dir selbst) empfehlen, das Modul vom offiziellen FHEM-Update auszuschließen.Füge diesen kurzen Befehl am besten gedanklich nach dem reload-Befehl hinzu:

attr global exclude_from_update 98_PID20.pm
