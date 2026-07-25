---
title: MDT Busspannungsversorgung STC-0960.01
device_type: Busspannungsversorgung
manufacturer: MDT
article_number: [STC-0960.01]
bus: KNX TP
source_pdf: originals/KNX/MDT_TM_STC-xxx0-01_V11_DE.pdf
last_updated: 2026-07-25
synonyms: [Netzteil, Spannungsversorgung, Bus-Netzteil, KNX-Spannungsversorgung]
tags: [knx, busspannungsversorgung, mdt]
---

## Übersicht

Die STC-0960.01 ist eine überlast- und kurzschlussfeste KNX-Busspannungsversorgung, die eine Linie mit stabilisierter 30 V Gleichspannung versorgt. Zusätzlich zum eigentlichen Busausgang besitzt das Gerät einen unverdrosselten 30 V Hilfsspannungsausgang für Komponenten, die keine gedrosselte Spannung benötigen.

Kernstück ist die integrierte Diagnosefunktion: Das Gerät überwacht laufend Gerätetemperatur, Ausgangsspannung, Stromaufnahme und die Busauslastung (Telegrammverkehr). Erkannte Grenzwertüberschreitungen können per LED signalisiert, als Kommunikationsobjekt gemeldet und mit Zeitstempel in einem internen Ringspeicher für die letzten 9 Ereignisse abgelegt werden. Über Statusobjekte lässt sich dieser Ereignisspeicher auslesen bzw. für eine Visualisierung als Klartext aufbereiten.

Zusätzlich enthält das Gerät eine Geräteüberwachung, die bis zu 100 KNX-Teilnehmer aktiv (Abfrage über physikalische oder Gruppenadresse) oder passiv (Mithören zyklischer Telegramme) auf Erreichbarkeit prüft. Fehlt ein Gerät, wird dies per LED, Alarmobjekt und Klartextmeldung im Ringspeicher dokumentiert. Die überwachten Geräte lassen sich in bis zu 5 Gruppen einteilen, die zusätzlich zur Sammelmeldung und zum gezielten Ab-/Zuschalten (z. B. über einen nachgeschalteten Schaltaktor) genutzt werden können.

Ein Parallelbetrieb mehrerer STC-Busspannungsversorgungen an derselben Linie ist nicht zulässig.

## Technische Daten

| Eigenschaft | Wert |
|---|---|
| Artikelnummer | STC-0960.01 |
| Bauform | 6 TE REG (Reiheneinbaugerät) |
| Nennstrom / Dauerstrom | 960 mA |
| Schwellenwert Überstromerkennung (I > Imax) | 1300 mA |
| Schwellenwert Temperaturalarm | 60 °C |
| Schwellenwert Unterspannung | < 28 V |
| Schwellenwert Busauslastung (Traffic) | > 60 % |
| Busspannung (Ausgang) | 30 V DC, stabilisiert |
| Zusatzausgang | 30 V DC, unverdrosselt (U2) |
| Netzspannung | 230 V AC, 50 Hz (lt. Anschlussschema) |
| Zul. Umgebungstemperatur | -5 °C ... +45 °C (lt. Frontaufdruck) |
| Ringspeicher (Ereignisse) | 9 Ereignisse mit Zeitstempel |
| Geräteüberwachung | bis zu 100 Geräte, in bis zu 5 Gruppen |

Hinweis: Weitere mechanische Maße (Gewicht, exakte Gehäuseabmessungen) sind im Datenblatt nicht spezifiziert; hierzu wird auf das separate Datenblatt verwiesen.

## Kommunikationsobjekte

### Allgemein

| Nr. | Name | Funktion | Länge/DPT | Flags |
|---|---|---|---|---|
| 0 | In Betrieb | Status senden | 1 Bit | K, Ü |
| 1 | Bus Reset | Reset aktivieren | 1 Bit | K, S |
| 2 | Tageszeit | Wert empfangen | 3 Byte | K, S |
| 3 | Datum | Wert empfangen | 3 Byte | K, S |
| 4 | Datum und Uhrzeit | Wert empfangen | 8 Byte | K, S |
| 20 | Alle Messwerte | Anfrage starten | 1 Bit | K, S |
| 21 | Alle min/max Werte | Reset | 1 Bit | K, S |
| 240 | Betriebsstundenzähler | Betriebsstunden | 2 Byte | K, L, Ü |
| 241 | Betriebsstundenzähler | Betriebsstunden seit letztem Neustart | 2 Byte | K, L, Ü |
| 242 | Betriebsstundenzähler | Betriebsstunden Reset | 1 Bit | K, S |
| 243 | Betriebsstundenzähler | Betriebsstunden 4 Byte | 4 Byte | K, L, Ü |
| 244 | Betriebsstundenzähler | Betriebsstunden seit letztem Neustart 4 Byte | 4 Byte | K, L, Ü |

Das Objekt „In Betrieb" sendet zyklisch (falls aktiviert) ein Ein-Telegramm, damit andere Teilnehmer erkennen können, dass das Gerät aktiv ist ("Lebenszeichen"). Über „Bus Reset" lässt sich die Busspannung für ca. 20 Sekunden gezielt abschalten, wodurch alle angeschlossenen Busteilnehmer neu starten. Die Objekte für Tageszeit/Datum dienen dazu, den Ereignissen im Ringspeicher einen realen Zeitstempel zuzuordnen. „Alle Messwerte" stößt die gesammelte Übertragung aller aktuellen Mess- und Grenzwerte an, „Alle min/max Werte" setzt alle bisher erfassten Minimal-/Maximalwerte zurück. Der Betriebsstundenzähler zählt optional (2 oder 4 Byte, wählbar) die Gesamtlaufzeit sowie die Laufzeit seit dem letzten Neustart und kann zyklisch gemeldet oder zurückgesetzt werden.

### Stromüberwachung

| Nr. | Name | Funktion | Länge/DPT | Flags |
|---|---|---|---|---|
| 5 | Strommesswert | Messwert ausgeben | 2 Byte / 4 Byte | K, L, Ü |
| 8 | Stromüberschreitung | Alarmmeldung | 1 Bit | K, L, Ü |
| 14 | Stromüberwachung | Maximaler Stromwert | 2 Byte / 4 Byte | K, L, Ü |
| 15 | Stromüberwachung | Minimaler Stromwert | 2 Byte / 4 Byte | K, L, Ü |

Der Strommesswert kann wahlweise als 2-Byte-Wert (unsigned oder Gleitkomma in mA) oder 4-Byte-Gleitkommawert in A übertragen werden. Das Alarmobjekt „Stromüberschreitung" meldet, ob der für das jeweilige Gerät geltende Maximalstrom (bei der STC-0960.01: 1300 mA) über- oder unterschritten wird. Die Min-/Max-Objekte liefern den bisher niedrigsten bzw. höchsten gemessenen Stromwert.

### Spannungsüberwachung

| Nr. | Name | Funktion | Länge/DPT | Flags |
|---|---|---|---|---|
| 6 | Spannungsmesswert | Messwert ausgeben | 2 Byte / 4 Byte | K, L, Ü |
| 10 | Spannungsunterschreitung | Alarmmeldung | 1 Bit | K, L, Ü |
| 16 | Spannungsüberwachung | Maximaler Spannungswert | 2 Byte / 4 Byte | K, L, Ü |
| 17 | Spannungsüberwachung | Minimaler Spannungswert | 2 Byte / 4 Byte | K, L, Ü |

Analog zur Stromüberwachung liefert das Spannungsmessobjekt den aktuellen Ausgangsspannungswert. Unterschreitet die gemessene Busspannung 28 V, meldet das Alarmobjekt dies als Unterspannung. Auch hier stehen optionale Min-/Max-Objekte zur Verfügung.

### Busverkehrsüberwachung

| Nr. | Name | Funktion | Länge/DPT | Flags |
|---|---|---|---|---|
| 7 | Busverkehr | Überwachung | 1 Byte | K, L, Ü |
| 13 | Busverkehrüberschreitung | Alarmmeldung | 1 Bit | K, L, Ü |
| 18 | Busverkehr Überwachung | Maximaler Busverkehr | 1 Byte | K, L, Ü |
| 19 | Busverkehr Überwachung | Minimaler Busverkehr | 1 Byte | K, L, Ü |

Das Objekt „Busverkehr" gibt die aktuell gemessene Busauslastung in Prozent aus. Überschreitet diese 60 %, wird über das Alarmobjekt eine Meldung ausgelöst. Wichtig: Die gemessene Auslastung berücksichtigt jedes Telegramm auf dem Bus (inkl. Wiederholungen), daher ist der Wert nicht direkt mit der Anzeige im ETS-Busmonitor vergleichbar, der wiederholte/unbestätigte Telegramme anders behandelt.

### Temperaturüberwachung

| Nr. | Name | Funktion | Länge/DPT | Flags |
|---|---|---|---|---|
| 11 | Temperaturüberwachung | Alarm bei Überschreiten | 1 Bit | K, L, Ü |

Der Temperaturalarm wird ausgelöst, sobald die intern (nicht einstellbar) definierte Temperaturschwelle überschritten wird. Für die STC-0960.01 liegt dieser Grenzwert bei 60 °C.

### Geräteüberwachung

| Nr. | Name | Funktion | Länge/DPT | Flags |
|---|---|---|---|---|
| 22 (+1 je Gerät) | Gerät 1 ... 100 | Überwachung über Gruppenadresse | 1 Bit / 1 Byte / 2 Byte / 4 Byte | je nach Modus |
| 122 (+1 je Gerät) | Gerät 1 ... 100 | Überwachung Ergebnis | 1 Bit | K, L, Ü |
| 222 (+1 je Gruppe) | Gerätegruppe 1 ... 5 | Überwachung Ergebnis | 1 Bit | K, L, Ü |
| 227 (+1 je Gruppe) | Gerätegruppe 1 ... 5 | Schalten | 1 Bit | K, Ü |
| 232 | Alle Gerätegruppen | Überwachung Ergebnis | 1 Bit | K, L, Ü |
| 233 | Geräteüberwachung | Sperren | 1 Bit | K, S |
| 234 | Geräteüberwachung | Status | 1 Bit | K, Ü |

Jedem der bis zu 100 überwachten Geräte ist ein „Ergebnis"-Objekt zugeordnet, das meldet, wenn das jeweilige Gerät nicht erreichbar ist. Werden Geräte einer Gruppe (1–5) zugeordnet, meldet das jeweilige Gruppen-Ergebnisobjekt eine Sammelstörung, sobald mindestens ein Gerät der Gruppe ausgefallen ist; „Alle Gerätegruppen" fasst dies gruppenübergreifend zusammen. Das Schalt-Objekt einer Gruppe kann genutzt werden, um im Fehlerfall über einen externen Schaltaktor die betroffenen Busteilnehmer kurz vom Bus zu trennen und neu zu starten (siehe Abschnitt Inbetriebnahme/Hinweise). Über „Geräteüberwachung – Sperren" lässt sich die gesamte Überwachung temporär deaktivieren, z. B. während Wartungsarbeiten; der Status-Objekt zeigt den aktuellen Sperr-/Freigabezustand.

### Statusausgabe

| Nr. | Name | Funktion | Länge/DPT | Flags |
|---|---|---|---|---|
| 235 | Statusausgabe | Status des letzten Events | 14 Byte | K, Ü |
| 236 | Statusausgabe für Visualisierung | Statustext | 14 Byte | K, Ü |
| 237 | Menünavigation für Visualisierung | Textnachrichten blättern | 1 Bit | K, S |
| 238 | Menünavigation für Visualisierung | Menüauswahl bestätigen | 1 Bit | K, S |
| 239 | Ereignisspeicher für Statusausgabe | Reset | 1 Bit | K, S |

Das Objekt „Statusausgabe" (Nr. 235) sendet unmittelbar bei Eintritt eines neuen Ereignisses (z. B. Temperaturalarm, Überstrom, Geräteausfall) einen 14-Byte-Klartextstring. Je nach Parametrierung wird entweder ein einzelner zusammenfassender String gesendet, oder es werden nacheinander bis zu drei Telegramme mit Art des Alarms, betroffenem Gerät und Zeitstempel übertragen – Letzteres eignet sich z. B. für eine Weiterverarbeitung als E-Mail-Benachrichtigung über ein IP-Interface/IP-Router.

Das Objekt „Statusausgabe für Visualisierung" (Nr. 236) liest den Ringspeicher (letzte 9 Ereignisse) aus. Mit dem Blätter-Objekt (237) navigiert man im Speicher vorwärts/rückwärts, wobei jeweils die laufende Nummer und Alarmart als Kurztext gesendet wird. Mit dem Bestätigen-Objekt (238) werden für das aktuell ausgewählte Ereignis nacheinander drei Detail-Telegramme (Alarmart, betroffenes Gerät, Zeitstempel) übertragen, die z. B. in einer Visualisierung als Klartext dargestellt werden können. Über das Reset-Objekt (239) wird der komplette Ereignisspeicher gelöscht.

Folgende Klartext-Kürzel werden dabei verwendet: T>Tmax (Temperaturalarm), I>Imax (Stromalarm), U<Umin (Unterspannung), Busl. max (Busverkehr über 60 %), Busreset (durchgeführter Busspannungsreset), Dev.Lost (Geräteüberwachung hat ein fehlendes Gerät erkannt).

## ETS-Parameter

### Allgemeine Einstellungen

| Parameter | Wertebereich | Standard |
|---|---|---|
| Geräteanlaufzeit | 2 ... 200 s | 10 s |
| In Betrieb Zykluszeit | 0 min (inaktiv) – 4 h | 10 min |
| Sprachauswahl für Statusausgabe | Deutsch / Englisch | – |
| Betriebsstundenzähler | nicht aktiv / aktiv | – |
| Objekte Auswahl (wenn aktiv) | 2 Byte / 4 Byte | – |
| Zyklisch melden alle (wenn aktiv) | 0 ... 255 h (0 = nicht aktiv) | 0 h |

Die Geräteanlaufzeit verzögert den funktionalen Start nach einem Neustart (z. B. nach Busspannungsreset oder Neuprogrammierung). Sinn dieser Verzögerung: Wenn viele Geräte gleichzeitig auf einer Linie starten würden, entstünde eine kurzzeitig hohe Buslast; durch unterschiedliche Anlaufzeiten je Gerät wird dies entzerrt. Die „In Betrieb"-Zykluszeit legt fest, ob und wie oft ein Lebenszeichen-Telegramm gesendet wird.

### Diagnosefunktionen – Temperaturüberwachung

| Parameter | Wertebereich | Standard |
|---|---|---|
| Temperaturalarm | nicht aktiv / aktiv | – |
| Aktion bei Temperaturalarm | nichts senden / Wert=1 senden / Wert=0 senden | – |
| Aktion bei Rücknahme des Alarms | nichts senden / Wert=1 senden / Wert=0 senden | – |
| Zyklisches Senden | nicht senden, 1 min – 24 h | – |

Die beiden Aktions-Parameter legen fest, welcher Objektwert im Alarmfall bzw. im Normalbetrieb gesendet wird – so kann z. B. wahlweise eine reine Alarmmeldung (Wert=1 bei Alarm) oder eine "Alles ok"-Rückmeldung (Wert=1 bei Normalbetrieb) realisiert werden; der jeweils andere Fall sendet automatisch den Gegenwert 0.

### Diagnosefunktionen – Stromüberwachung

| Parameter | Wertebereich | Standard |
|---|---|---|
| Objekt für Busstrommessung | 2 Byte unsigned mA (DPT 7.012) / 2 Byte Gleitkomma mA (DPT 9.021) / 4 Byte Gleitkomma A (DPT 14.019) | – |
| Messwert senden nach Änderung von | nicht senden, 5 % – 50 % | – |
| Stromwert zyklisch senden | nicht senden, 1 min – 24 h | – |
| Überstrom aktivieren | nicht aktiv / aktiv | – |
| Aktion bei Überschreitung | nichts senden / Wert=1 senden / Wert=0 senden | – |
| Aktion bei nicht Überschreitung | nichts senden / Wert=1 senden / Wert=0 senden | – |
| Zyklisches Senden | nicht senden, 1 min – 24 h | – |
| Reaktionsgeschwindigkeit | hoch / mittel / gering | mittel |
| Min-/Maxwerte senden | nicht aktiv / aktiv | – |

Die Reaktionsgeschwindigkeit filtert kurzzeitige Stromspitzen, damit diese nicht sofort einen Alarm auslösen: Bei „hoch" wird jede noch so kurze Überschreitung des Maximalstroms sofort gemeldet; bei „mittel" muss der Grenzwert mindestens 5 Sekunden anhaltend überschritten sein; bei „gering" ist eine mindestens 10-sekündige Überschreitung nötig, bevor der Alarm auslöst. Damit lässt sich das Gerät gegen kurzzeitige Einschaltstromspitzen unempfindlicher einstellen.

### Diagnosefunktionen – Spannungsüberwachung

| Parameter | Wertebereich | Standard |
|---|---|---|
| Objekt für Buspannungsmessung | 4 Byte Gleitkomma V (DPT 14.027) / 2 Byte Gleitkomma mV (DPT 9.020) | – |
| Messwert senden nach Änderung von | nicht senden, 5 % – 50 % | – |
| Spannungswert zyklisch senden | nicht senden, 1 min – 24 h | – |
| Unterspannung (U < 28 V) aktivieren | nicht aktiv / aktiv | – |
| Aktion bei Unterschreitung | nichts senden / Wert=1 senden / Wert=0 senden | – |
| Aktion bei nicht Unterschreitung | nichts senden / Wert=1 senden / Wert=0 senden | – |
| Zyklisches Senden | nicht senden, 1 min – 24 h | – |
| Reaktionsgeschwindigkeit | hoch / mittel / gering | mittel |
| Grenzwerte senden | nicht aktiv / aktiv | – |

Die Reaktionsgeschwindigkeit wirkt analog zur Stromüberwachung: „hoch" meldet jede kurzzeitige Unterschreitung der 28-V-Schwelle sofort, „mittel" erst nach mindestens 5 Sekunden anhaltender Unterschreitung, „gering" erst nach mindestens 10 Sekunden. So werden kurzzeitige Spannungseinbrüche (z. B. durch Lastspitzen anderer Geräte) gefiltert, bevor ein Alarm ausgelöst wird.

### Diagnosefunktionen – Busverkehrsüberwachung

| Parameter | Wertebereich | Standard |
|---|---|---|
| Messwert senden nach Änderung von | nicht senden, 5 % – 50 % | – |
| Messwert Busverkehr zyklisch senden | nicht senden, 1 min – 24 h | – |
| Schwellenwerte für max. Busverkehr aktivieren | nicht aktiv / aktiv | – |
| Aktion bei Überschreitung | nichts senden / Wert=1 senden / Wert=0 senden | – |
| Aktion bei nicht Überschreitung | nichts senden / Wert=1 senden / Wert=0 senden | – |
| Zyklisches Senden | nicht senden, 1 min – 24 h | – |
| Reaktionsgeschwindigkeit | hoch / mittel / gering | mittel |
| Grenzwerte senden | nicht aktiv / aktiv | – |

Auch hier filtert die Reaktionsgeschwindigkeit kurzzeitige Lastspitzen: „hoch" meldet sofort jede Überschreitung von 60 % Buslast, „mittel" erst nach mindestens 5 Sekunden, „gering" erst nach mindestens 10 Sekunden anhaltender Überlastung.

### Diagnosefunktionen – Statusausgabe

| Parameter | Wertebereich | Standard |
|---|---|---|
| Ausgabemodus Statusausgabe letztes Event (Obj. 235) | einmaliges Senden des Events / einmaliges Senden einer Stringfolge | – |
| Zyklische Ausgabe (Obj. 236) | nicht senden, 1 min – 24 h | – |
| Umschaltzeit der verschiedenen Seiten | 1 ... 255 | 2 |
| Anzahl der Wiederholungen | 0 – 5 | 2 |
| Übertemperatur über Ausgabetexte versenden | nein / ja | – |
| Überstrom über Ausgabetexte versenden | nein / ja | – |
| Busverkehrsüberschreitungen über Ausgabetexte versenden | nein / ja | – |
| Geräteüberwachung Gruppe 1 (... 5) über Ausgabetexte versenden | nein / ja | – |
| Status "Busreset" über Ausgabetext versenden (ab HW-Rev. R2.2) | keine Meldung / Meldung bei Reset-Taste / Meldung bei Reset-Taste + Neustart | – |

Über die Parameter „... über Ausgabetexte versenden" wird festgelegt, ob der jeweilige Alarm nur als Kommunikationsobjekt gemeldet oder zusätzlich mit Zeitstempel im Ringspeicher (und damit in der Klartext-Statusausgabe) hinterlegt wird. Die „Umschaltzeit" und „Anzahl der Wiederholungen" steuern das Timing der Stringfolgen-Übertragung für Visualisierungen.

### Geräteüberwachung – Allgemeine Einstellungen

| Parameter | Wertebereich | Standard |
|---|---|---|
| Geräteüberwachung | nicht aktiv / aktiv | – |
| Polarität des Status | als Alarm (erreichbar = "Aus") / als "In Betrieb"-Objekt (erreichbar = "Ein") | – |
| Dauer der Sperrung bei Busspannungswiederkehr | 10 s – 8 h | 10 min |
| Dauer der Sperrung über Sperrobjekt | unbegrenzt, 1 min – 8 h | 10 min |
| Zyklisches Senden Sammelmeldung "Alle Geräte" | nicht senden, 1 min – 24 h | – |
| Zyklisches Senden Sammelmeldung "Gruppe 1 (... 5)" | nicht senden, 1 min – 24 h | – |
| Objekte für Trennung von KNX-Teilnehmern (alle Gruppen) | nicht aktiv / aktiv | – |
| Zeit des "Aus"-Signals | 5 s – 4 min | 5 s |

Die „Dauer der Sperrung bei Busspannungswiederkehr" verhindert Fehlalarme direkt nach einem Neustart der Anlage, da überwachte Geräte selbst erst hochfahren müssen, bevor sie antworten können. Die „Dauer der Sperrung über Sperrobjekt" definiert, wie lange die Überwachung nach einer externen Sperrung (Objekt 233) inaktiv bleibt, bevor sie automatisch wieder anläuft (oder unbegrenzt gesperrt bleibt, bis explizit wieder freigegeben wird).

Die Funktion „Objekte für Trennung von KNX-Teilnehmern" erlaubt es, im Fehlerfall automatisch einen Schaltaktor anzusteuern, der den Bus-Kontakt zur betroffenen Gerätegruppe kurzzeitig auftrennt und danach wieder verbindet – nützlich bei älteren/fehlerhaften Geräten, die sich nur durch einen Busspannungsreset zurücksetzen lassen. Dazu ist zwingend ein externer Schaltaktor im Busleitungspfad der jeweiligen Gruppe erforderlich; die STC selbst schaltet nicht den gesamten Bus, sondern nur über das zugeordnete Gruppen-Schaltobjekt den vorgeschalteten Aktor. Bleibt der Fehler nach dem Trennvorgang bestehen, wird der Schaltvorgang nicht automatisch wiederholt.

### Geräteüberwachung – Gerät 1 (... 100)

| Parameter | Wertebereich | Standard |
|---|---|---|
| Gerät 1 (... 100) überwachen | nicht aktiv / über physikalische Adresse (aktive Abfrage) / über Gruppenadresse (aktive Abfrage) / über Gruppenadresse (passives Empfangen) | nicht aktiv |

Es stehen drei Überwachungsarten zur Wahl, die sich in Buslast und Anwendungsfall unterscheiden:

**Über physikalische Adresse (aktive Abfrage):** Das zu überwachende Gerät wird per Bereich/Linie/Geräteadresse referenziert (individuell oder identisch zur Linie der STC) und in einem einstellbaren Intervall (20 s – 24 h) aktiv per Telegramm angefragt.

**Über Gruppenadresse (aktive Abfrage):** Ein Kommunikationsobjekt wird eingeblendet und mit einem Objekt des Zielgeräts verknüpft (dieses muss ein L-Flag besitzen); das Objekt wird im eingestellten Intervall aktiv abgefragt. Bei 1-Bit-Objekten kann zusätzlich gefiltert werden, welcher Wert (AUS/EIN/jeder Wert) als "Gerät gültig" gilt.

**Über Gruppenadresse (passives Empfangen):** Es findet keine aktive Abfrage statt; stattdessen wird innerhalb des Überwachungsintervalls auf ein eingehendes Telegramm eines zyklisch sendenden Objekts gewartet. Dieser Modus erzeugt die geringste zusätzliche Buslast und eignet sich besonders für Geräte, die ohnehin bereits zyklisch senden (z. B. "In Betrieb"-Objekte oder Temperaturwerte).

Alle drei Modi erlauben zusätzlich die Zuordnung des Geräts zu einer der 5 Gerätegruppen für die Sammelmeldung.

## Inbetriebnahme / Hinweise

- Reihenfolge der Inbetriebnahme: Verdrahtung nach Anschlussschema → Busschnittstelle anschließen → Netzspannung zuschalten → Programmiertaste ≥ 1 s drücken (rote Programmier-LED leuchtet dauerhaft) → physikalische Adresse in der ETS programmieren (LED erlischt) → Applikationsparameter programmieren.
- Ein Parallelschalten mehrerer STC-Busspannungsversorgungen an derselben Linie ist nicht zulässig.
- Die Grenzwerte für Überstrom- und Temperaturalarm sind geräteabhängig (bei STC-0960.01: 1300 mA bzw. 60 °C) und in der ETS nicht editierbar.
- Für die Funktion „Objekte für Trennung von KNX-Teilnehmern" wird zwingend ein zusätzlicher, extern angeschlossener Schaltaktor pro Gerätegruppe benötigt, über dessen Kontakt der Bus zur jeweiligen Gruppe geführt wird – die STC trennt nicht selbst den kompletten Busausgang.
- Bei der Geräteüberwachung sollte, wo funktional möglich, die passive Abfrage über Gruppenadresse bevorzugt werden, um die Buslast gering zu halten.
- Die per Reaktionsgeschwindigkeit (Strom/Spannung/Busverkehr) einstellbare Filterung dient dazu, Fehlalarme durch kurzzeitige Spitzen zu vermeiden; bei sicherheitskritischen Anwendungen sollte "hoch" gewählt werden, für tolerantere Überwachung "mittel" oder "gering".
- Funktion „Status Busreset über Ausgabetext versenden" steht erst ab Hardware-Revision R2.2 zur Verfügung.

## Quelle

MDT Technisches Handbuch „KNX Busspannungsversorgung mit Diagnosefunktion [STC-xxx0.01]", Stand 04/2025, Version 1.1.
Datei: `originals/KNX/MDT_TM_STC-xxx0-01_V11_DE.pdf`