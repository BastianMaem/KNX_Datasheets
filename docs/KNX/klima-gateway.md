---
title: Intesis ME-AC-KNX-1-V2 (KNX-Klimaanlagen-Gateway)
device_type: KNX-Klimaanlagen-Gateway
manufacturer: Intesis
article_number: [ME-AC-KNX-1-V2]
bus: KNX TP
source_pdf:
  - originals/KNX/Intesis_INKNXMIT001I000.pdf
  - originals/Klimaanlage/MSZ-LN18VG2W._Innengeraet.pdf
  - originals/Klimaanlage/SLZ-M35FA2_Innengeraet.pdf
  - originals/Klimaanlage/MXZ-3F54VF4_Aussengeraet.pdf
last_updated: 2026-07-24
synonyms: [AC-Gateway, Klimaanlagen-Interface, Mitsubishi-KNX-Schnittstelle,
  KNX-Klimasteuerung]
tags: [knx, gateway, klimaanlage, intesis, mitsubishi]
---

## Übersicht

Das INKNXMIT001I000 (Handelsbezeichnung ME-AC-KNX-1-V2) ist ein Gateway, das
Mitsubishi-Electric-Klimageräte der Linien Domestic, Mr. Slim und City Multi
in eine KNX-TP-1(EIB)-Anlage einbindet. Auf der einen Seite stellt es
KNX-Kommunikationsobjekte (Bit-, Byte- und Text-Objekte mit KNX-Standard-DPTs)
bereit, auf der anderen Seite spricht es intern das Steuerungsprotokoll des
angeschlossenen Mitsubishi-Innengeräts an. Für jedes Control_-Objekt existiert
in der Regel ein passendes Status_-Objekt, sodass jeder Steuerbefehl auch
rückgelesen werden kann.

Wesentliche Eigenschaften laut Datenblatt:
- Ansteuerung von Ein/Aus, Betriebsart, Lüfterstufe, Lamellenposition und
  Solltemperatur, jeweils mit Status-Rückmeldung.
- Die Klimaanlage kann gleichzeitig über die Infrarot-Fernbedienung des
  Geräts und über KNX bedient werden.
- Die Regelung kann wahlweise auf der geräteinternen Ansaugtemperatur oder
  auf einer von einem beliebigen KNX-Thermostat bereitgestellten
  Ambient-Temperatur basieren.
- Überwachung von Betriebsstunden (für Filterwartung) sowie Fehlerstatus und
  numerischem Fehlercode.
- Bis zu 5 Szenen, die eine Kombination aus Betriebsart, Solltemperatur,
  Lüfterstufe, Lamellenposition und Fernbedienungssperre speichern und per
  einfachem Schaltbefehl abrufen.
- Konfiguration ausschließlich über das ETS-Parameterblatt; die Auswahl des
  korrekten angeschlossenen Innengeräte-Typs erfolgt dort und ist laut
  Hersteller zwingend erforderlich.

## Technische Daten

| Eigenschaft | Wert |
|---|---|
| Gehäuse | ABS (UL 94 HB), 2,5 mm Wandstärke |
| Abmessungen (B×H×T) | 59 × 36 × 21 mm |
| Gewicht | 42 g |
| Betriebstemperatur | -25 °C bis 60 °C |
| Lagertemperatur | -40 °C bis 85 °C |
| Betriebs-/Lagerfeuchte | < 90 % rF, nicht kondensierend |
| Spannungsversorgung | 29 V DC, 5 mA, über KNX-Bus versorgt |
| KNX-Anschluss | 1 × KNX TP1 (EIB), optoisoliert, steckbare Klemme (2-polig) |
| Anschluss Klimagerät | 1 × spezifischer Steckverbinder, Anschlusskabel (1,9 m) im Lieferumfang |
| Isolationsspannung | 4000 V |
| Schutzart | IP20 (IEC 60529) |
| Konfiguration | ausschließlich über ETS |
| Bedienelemente | 1 × Programmiertaste |
| Anzeige | 1 × Programmier-LED |
| Kompatible Klimageräte | Mitsubishi Electric Domestic, Mr. Slim, City Multi (Anschluss an Buchse CN92 bei Mr.-Slim-Modellen bzw. CN105 bei übrigen Modellen) |
| Zertifizierungen | RoHS (2002/95/CE); CE nach EMV-Richtlinie (2004/108/EC) und Niederspannungsrichtlinie (2006/95/EC); EN 61000-6-3, EN 61000-6-1, EN 60950-1, EN 50491-3 |

Eine vollständige Kompatibilitätsliste der unterstützten Mitsubishi-Innengeräte
und ihrer jeweils verfügbaren Funktionen wird vom Hersteller separat online
gepflegt (siehe Abschnitt "Quelle").

## Kommunikationsobjekte

Alle Objektnummern und Datenpunkttypen (DPT) stammen aus der
Kommunikationsobjekt-Tabelle (Appendix A) des Gateway-Handbuchs. Flags: R =
Read, W = Write, T = Transmit, U = Update.

### Ein/Aus

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 0 | Control_ On/Off | Schaltet das Klimagerät ein/aus | DPT_Switch (1.001) | W, T |
| 43 | Status_ On/Off | Rückmeldung des Schaltzustands | DPT_Switch (1.001) | R, T |

Dies ist eines der vier Basisobjekte, die im Gateway ab Werk aktiviert sind.

### Betriebsart (Mode)

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 1 | Control_ Mode | Byte-Objekt zur direkten Anwahl der Betriebsart | DPT_HVACContrMode (20.105) | W, T |
| 2 | Control_ Mode Cool/Heat | Umschaltung Kühlen/Heizen als 1-Bit-Objekt | DPT_Heat/Cool (1.100) | W, T |
| 3–7 | Control_ Mode Auto / Heat / Cool / Fan / Dry | je ein 1-Bit-Objekt pro Modus zur direkten Aktivierung | DPT_Bool (1.002) | W, T |
| 8 | Control_ Mode -/+ bzw. +/- | zyklischer Moduswechsel über Stufenobjekt | DPT_Step / DPT_UpDown (1.007 / 1.008) | W |
| 44 | Status_ Mode | Rückmeldung der aktuellen Betriebsart | DPT_HVACContrMode (20.105) | R, T |
| 45 | Status_ Mode Cool/Heat | Rückmeldung Kühlen/Heizen | DPT_Heat/Cool (1.100) | R, T |
| 46–50 | Status_ Mode Auto / Heat / Cool / Fan / Dry | Rückmeldung je Modus als 1-Bit-Objekt | DPT_Bool (1.002) | R, T |
| 51 | Status_ Mode Text | Textrückmeldung der Betriebsart (frei konfigurierbare Strings) | DPT_String_8859_1 (16.001) | R, T |
| 76 | Legacy_ Mode | Kompatibilitätsobjekt zu älteren Gateway-Versionen, andere Kodierung (0-Auto;1-Heat;2-Dry;3-Fan;4-Cool) | 1 Byte, Enumerated | R, T |

Das Byte-Objekt für den Modus arbeitet mit DPT 20.105: Auto = 0, Heat = 1,
Cool = 3, Fan = 9, Dry = 14. Ob der Fan-Modus überhaupt zur Verfügung steht,
hängt vom angeschlossenen Innengerät ab und wird über den ETS-Parameter
"Indoor unit has FAN mode" festgelegt. Die einzelnen Bit-Objekte (3–7)
erlauben die direkte Aktivierung eines Modus mit einer "1"; die
+/‑-Variante (Objekt 8) wandert stattdessen zyklisch durch die Reihenfolge
Auto → Heat → Cool → Fan → Dry.

### Lüfterstufe (Fan Speed)

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 9 | Control_ Fan Speed / 2(3)(4) Speeds | Byte-Objekt zur direkten Anwahl der Lüfterstufe | DPT_Enumerated (5.010) | W, T |
| 10 | Control_ Fan Speed Manual/Auto | Umschaltung Hand-/Automatikbetrieb der Lüfterstufe | DPT_Bool (1.002) | W, T |
| 11–14 | Control_ Fan Speed 1–4 | 1-Bit-Objekte zur direkten Anwahl je Stufe | DPT_Bool (1.002) | W, T |
| 15 | Control_ Fan Speed -/+ bzw. +/- | stufenweises Erhöhen/Verringern der Lüfterstufe | DPT_Step / DPT_UpDown (1.007 / 1.008) | W |
| 52 | Status_ Fan Speed | Rückmeldung der aktuellen Lüfterstufe | DPT_Enumerated (5.010) | R, T |
| 53–57 | Status_ Fan Speed Manual/Auto, Speed 1–4 | Rückmeldung je Betriebsart/Stufe | DPT_Bool (1.002) | R, T |
| 58 | Status_ Fan Speed Text | Textrückmeldung (frei konfigurierbare Strings je Stufe) | DPT_String_8859_1 (16.001) | R, T |
| 77 | Legacy_ Fan Speed | Kompatibilitätsobjekt zu älteren Gateway-Versionen | 1 Byte, Enumerated | R, T |

Wie viele Lüfterstufen (1 bis 4) tatsächlich zur Verfügung stehen und ob eine
Auto-Stufe existiert, wird über die ETS-Parameter "Available fanspeeds in
Indoor Unit" bzw. "Indoor unit has AUTO fan speed" passend zum realen
Innengerät eingestellt; nur die dadurch freigeschalteten Objekte sind am
Gerät auch wirksam.

### Lamellen Auf/Ab (Vanes Up-Down)

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 16 | Control_ Vanes U-D / 5 pos | Byte-Objekt zur direkten Anwahl der Lamellenposition | DPT_Enumerated (5.010) | W, T |
| 17 | Control_ Vanes U-D Man/Auto | Umschaltung Hand-/Automatikbetrieb der Lamellenposition | DPT_Bool (1.002) | W, T |
| 18–22 | Control_ Vanes U-D Pos1–Pos5 | 1-Bit-Objekte zur direkten Anwahl je Position | DPT_Bool (1.002) | W, T |
| 23 | Control_ Vanes U-D Swing | aktiviert/deaktiviert Swing-Betrieb | DPT_Bool (1.002) | W, T |
| 24 | Control_ Vanes U-D -/+ bzw. +/- | stufenweises Verstellen der Lamellenposition | DPT_Step / DPT_UpDown (1.007 / 1.008) | W, T |
| 59 | Status_ Vanes U-D / 4(5) pos | Rückmeldung der aktuellen Position | DPT_Enumerated (5.010) | R, T |
| 60–66 | Status_ Vanes U-D Man/Auto, Pos1–Pos5, Swing | Rückmeldung je Betriebsart/Position | DPT_Bool (1.002) | R, T |
| 67 | Status_ Vanes U-D Text | Textrückmeldung (frei konfigurierbare Strings) | DPT_String_8859_1 (16.001) | R, T |
| 78 | Legacy_ Vanes | Kompatibilitätsobjekt zu älteren Gateway-Versionen | 1 Byte, Enumerated | R, T |

Wird über Swing (Objekt 23) oder das kombinierte Man/Auto-Objekt (17) eine
"1" gesendet, fahren die Lamellen in den Auto-/Swing-Betrieb; eine "0"
aktiviert den manuellen Betrieb und stellt die erste Position ein. Im
Auto-Modus wählt das Innengerät selbständig die passende Lamellenposition;
diese wird jedoch weder in KNX noch an der Fernbedienung angezeigt.

### Solltemperatur und Ambient-Temperatur

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 25 | Control_ Setpoint Temperature | Vorgabe der Solltemperatur in °C | DPT_Value_Temp (9.001) | W, T |
| 26 | Control_ Setpoint Temp -/+ bzw. +/- | stufenweise Sollwertänderung zwischen 19 °C und 28 °C | DPT_Step / DPT_UpDown (1.007 / 1.008) | W |
| 27 | Control_ Ambient Temperature | externe Ist-Temperatur, z. B. von einem KNX-Raumsensor | DPT_Value_Temp (9.001) | W, T |
| 68 | Status_ AC Setpoint Temp | Rückmeldung der am Innengerät wirksamen Solltemperatur | DPT_Value_Temp (9.001) | R, T |
| 69 | Status_ AC Return Temperature | Rückmeldung der vom Innengerät gemessenen Ansaug-/Rücklauftemperatur | DPT_Value_Temp (9.001) | R, T |

Das +/‑-Objekt für die Solltemperatur arbeitet innerhalb der festen
Gerätegrenzen von 19 °C (unteres Limit) bis 28 °C (oberes Limit). Wird
zusätzlich Objekt 27 genutzt, verschiebt das Gateway die tatsächlich an das
Innengerät gesendete Solltemperatur nach der Formel:

`AC-Solltemp. = AC-Rücklauftemp. − (KNX-Ist-Temp. − KNX-Solltemp.)`

Damit lässt sich die Regelung auf die Temperatur eines externen KNX-Sensors
statt auf die geräteeigene Ansaugtemperatur stützen; die Formel wirkt in
beide Richtungen (Heizen/Kühlen/Auto) korrekt und wird erst aktiv, sobald
sowohl Objekt 25 als auch Objekt 27 mindestens einmal von der
KNX-Anlage beschrieben wurden.

### Betriebsstundenzähler

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 28 | Control_/Status_ Operation Hour Counter | zählt die Betriebsstunden des Gateways; kann zum Rücksetzen/Aktualisieren auch beschrieben werden | DPT_Value_2_Ucount (7.001) | W, T |
| 72 | Status_ Operation Hour Counter | reine Statusrückmeldung des Zählerstands | DPT_Value_2_Ucount (7.001) | R, T |

Der Zähler wird auch nach einem Busausfall/-reset im Gateway gehalten. Eine
Statusmeldung wird nur gesendet, wenn sich der Wert ändert; steht der
Zähler auf 0 Stunden, wird kein Status auf den Bus gesendet. Zum
Zurücksetzen muss eine "0" auf das Objekt geschrieben werden; dafür muss am
Objekt zusätzlich das Schreib-Flag (W) aktiviert werden, da es
werksseitig nicht gesetzt ist.

### Fensterkontakt

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 29 | Control_ Window Contact Status | startet/stoppt eine Abschaltverzögerung für das Innengerät | DPT_OpenClose (1.009) | W, T |

Eine "1" (Fenster geschlossen) auf dieses Objekt startet – sofern das
Innengerät bereits eingeschaltet ist – die parametrierte
Abschaltverzögerung; eine "0" (Fenster geöffnet) stoppt sie wieder.

### Sperrfunktionen (Locking)

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 30 | Control_ Lock Remote Control | sperrt/entsperrt die Infrarot-Fernbedienung des Klimageräts | DPT_Bool (1.002) | W, T |
| 31 | Control_ Lock Control Objects | sperrt/entsperrt alle Control_-Objekte außer sich selbst | DPT_Bool (1.002) | W, T |
| 73 | Status_ Lock Remote Control | Rückmeldung Fernbedienungssperre | DPT_Bool (1.002) | R, T |
| 74 | Status_ Lock Control Objects | Rückmeldung Objektsperre | DPT_Bool (1.002) | R, T |

Beide Sperr-Objekte merken sich ihren letzten Wert auch über einen
Busausfall hinweg. Wichtig: Ist eine Startszene (Initial Scene) aktiv und
enthält sie für die Fernbedienungssperre den Wert "unverändert" oder
"entsperrt", hebt sie die Sperre auf, da die Startszene Vorrang vor dem
Control_-Lock-Objekt hat.

### Szenen

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 32 | Control_ Store/Exec Scene | Byte-Objekt: Werte 0–4 führen Szene 1–5 aus, Werte 128–132 speichern Szene 1–5 | DPT_SceneControl (18.001) | W, T |
| 33–37 | Control_ Store Scene 1–5 | 1-Bit-Objekte zum Speichern der aktuellen Werte als jeweilige Szene | DPT_Bool (1.002) | W |
| 38–42 | Control_ Execute Scene 1–5 | 1-Bit-Objekte zum Ausführen der jeweiligen Szene | DPT_Bool (1.002) | W, T |
| 75 | Status_ Current Scene | Rückmeldung der aktuell aktiven Szene (0–4 = Szene 1–5; 63 = keine Szene aktiv) | DPT_SceneNumber (17.001) | R, T |

Eine Szene speichert die Kombination aus Ein/Aus, Betriebsart, Lüfterstufe,
Lamellenposition, Solltemperatur und Fernbedienungssperre. Zum Ausführen von
Szene 4 über die Bit-Objekte wird z. B. eine "1" auf Objekt 41 (Control_
Execute Scene4) gesendet; zum Speichern von Szene 4 entsprechend eine "1"
auf Objekt 36 (Control_ Store Scene4).

### Fehlerstatus

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 70 | Status_ Error/Alarm | Sammelalarm: 0 = kein Alarm, 1 = Alarm aktiv | DPT_Alarm (1.005) | R, T |
| 71 | Status_ Error Code | numerischer Fehlercode des Innengeräts, 2 Byte; 0 = kein Fehler | 2 Byte, Enumerated | R, T |

Die vom Innengerät gemeldeten Fehlercodes (Objekt 71) sind laut Handbuch
wie folgt kodiert:

| Fehlercode | Bedeutung |
|---|---|
| -1 | Kommunikationsfehler zwischen Gateway und Klimagerät |
| 0 | kein aktiver Fehler |
| 0001 | Kommunikationsfehler mit dem Klimagerät |
| 1102 | Auslasstemperatur zu hoch |
| 1108 | interner Thermostatfühler aktiv (49C) |
| 1110 | Außengerätestörung |
| 1300 | Druck zu niedrig |
| 1302 | Druck zu hoch (Hochdruckfühler 63H) |
| 1503 | Frostschutz bzw. Batterie-Übertemperatur |
| 1504 | Frostschutz/Übertemperatur bzw. Überhitzungsschutz |
| 1509 | Hochdruckfehler (Kugelventil geschlossen) |
| 1520 | Überhitzungsanomalie durch zu niedrige Auslasstemperatur (TH4) |
| 2500 / 2502 | Fehlfunktion der Kondensatpumpe |
| 2503 | Kondensatfühler-Anomalie (DS) |
| 4030 | serieller Übertragungsfehler |
| 4100 / 4101 | Verdichterpause wegen Überstrom (Anlauf/Überlast) |
| 4102 | Phasenerkennung unterbrochen |
| 4103 | Anti-Phasen-Erkennung ausgelöst |
| 4108 | Phase L2 bzw. Steckverbinder 51CM unterbrochen |
| 4118 | Fehler im Anti-Phasen-Detektor (Elektronikplatine) |
| 4124 | Steckverbinder 49L unterbrochen |
| 4210 | Abschaltung wegen Verdichter-Überstrom |
| 4220 | Spannungsanomalie |
| 4230 | Temperaturanomalie Kühlkörper (TH8) |
| 5101 | Anomalie Raumtemperaturfühler Innengerät (TH1) |
| 5102 | Anomalie Flüssigkeitsfühler (TH2) |
| 5103 | Anomalie Kondensator-/Verdampferfühler (TH5) |
| 5104 | Fehler bei Erkennung der Auslasstemperatur |
| 5105–5110 | diverse Außenfühlerfehler (TH3, TH7, TH6, TH8) |
| 5202 | Steckverbinder 63L unterbrochen |
| 5300 | Fehler Stromfühler |
| 6600 | doppelte MNET-Adressvergabe |
| 6602–6608 | diverse MNET-Bus-/Übertragungsfehler (Hardware, Bus busy, ohne ACK/Antwort) |
| 6831/6832 | Übertragungsfehler der Infrarot-Fernbedienung (Empfang/Sendung) |
| 6840/6841 | Übertragungsfehler zwischen Innen-/Außengerät (Empfang/Sendung) |
| 6844 | Fehler im Verbindungskabel Innen-/Außengerät, Innengerätenummer deaktiviert (≥ 5 Min.) |
| 6845 | Fehler im Verbindungskabel Innen-/Außengerät (Verkabelung/Unterbrechung) |
| 6846 | Anfangstimer deaktiviert |

Nicht gelistete Fehlercodes sollen laut Hersteller über den
Mitsubishi-Electric-Support abgeklärt werden.

## ETS-Parameter

Die Parameter sind in ETS auf sieben Dialogseiten gegliedert. Sofern nicht
anders vermerkt, entsprechen die "Standard"-Werte der jeweils im Handbuch
als Werksauslieferung/Erstimport dargestellten Konfiguration.

### General dialog

| Parameter | Werte | Standard |
|---|---|---|
| Send READs for Control_ objects on bus recovery (T & U Flags erforderlich) | Yes / No | No |
| › Delay before sending READs (sec) | 0–30 | 10 |
| Enable comm obj "Ctrl_ Remote Lock" | Yes / No | No |
| Enable func "Control_ Lock Control Obj" | Yes / No | No |
| Enable func "Operating Hours Counter" | Yes / No | No |
| Enable object "Error Code [2byte]" | Yes / No | No |

Wird "Send READs…" aktiviert, sendet das Gateway bei Busrückkehr bzw.
Neustart für alle Control_-Objekte mit gesetzten T- und U-Flags ein
READ-Telegramm und übernimmt die Antwort als neuen Wert; die Verzögerung
gibt anderen Busteilnehmern Zeit zum Hochfahren. Die drei "Enable…"-Schalter
blenden die zugehörigen Objekte (Fernbedienungssperre, Sperre aller
Control_-Objekte, Betriebsstundenzähler, numerischer Fehlercode) ein oder
aus; ohne Aktivierung sind diese Objekte in der ETS-Projektierung nicht
sichtbar.

### Mode Configuration dialog

| Parameter | Werte | Standard |
|---|---|---|
| Indoor unit has FAN mode | Yes / No | Yes |
| Enable "Mode Cool/Heat" objects (für Control und Status) | Yes / No | No |
| Enable use of +/- object for Mode | Yes / No | No |
| › DPT type for +/- Mode Object | 0-Up/1-Down [1.008] / 0-Decrease/1-Increase [1.007] | 0-Up/1-Down [1.008] |
| Enable use of bit-type Mode objects (für Control) | Yes / No | No |
| Enable use of bit-type Mode objects (für Status) | Yes / No | No |
| Enable use of Text object for Mode | Yes / No | No |
| › Strings je Modus (AUTO/HEAT/COOL/FAN/DRY) | freier Text | "AUTO"/"HEAT"/"COOL"/"FAN"/"DRY" |
| Enable use of Legacy_ object for Mode (kompatibel zu alten XXACKNX1-Versionen) | Yes / No | No |

"Indoor unit has FAN mode" muss anhand der Innengerät-Dokumentation gesetzt
werden, da nicht jedes Modell einen reinen Lüfter-Modus unterstützt. Das
+/‑-Objekt durchläuft je nach gewähltem DPT die Reihenfolge
Auto→Heat→Cool→Fan→Dry vorwärts (Increase/Up) oder rückwärts
(Decrease/Down). Die Bit-Objekte für Control und Status sind unabhängig
voneinander zu- oder abschaltbar. Das Legacy-Objekt dient ausschließlich der
Rückwärtskompatibilität zu älteren Gateway-Programmversionen und nutzt eine
andere Werte-Kodierung als das reguläre Byte-Objekt.

### Fan Speed Configuration dialog

| Parameter | Werte | Standard |
|---|---|---|
| Fan is accessible in Indoor unit | Yes / No | Yes |
| Available fanspeeds in Indoor Unit | 1–4 | 3 |
| Indoor unit has AUTO fan speed | Yes / No | No |
| › Enable "Fan Speed Manual/Auto" objects (für Control und Status) | Yes / No | No |
| Enable use of +/- object for Fan Speed | Yes / No | No |
| › DPT type for +/- Fan Speed object | 0-Decrease/1-Increase [1.007] / 0-Up/1-Down [1.008] | 0-Decrease/1-Increase [1.007] |
| Enable use of bit-type Fan Speed objects (für Control) | Yes / No | No |
| Enable use of bit-type Fan Speed objects (für Status) | Yes / No | No |
| Enable use of Text object for Fan Speed | Yes / No | No |
| › Strings je Stufe (AUTO/1/2/3/4) | freier Text | "AUTO"/"SPEED 1"…"SPEED 4" |
| Enable use of Legacy_ object for Fan (kompatibel zu alten XXACKNX1-Versionen) | Yes / No | No |

Ob überhaupt eine Lüftersteuerung sowie eine Auto-Stufe existiert und wie
viele feste Stufen (bis zu 4) verfügbar sind, richtet sich strikt nach dem
angeschlossenen Innengerät und muss laut Hersteller anhand von dessen
Dokumentation gewählt werden – nicht passend gewählte Werte führen zu nicht
funktionierenden oder nicht vorhandenen Objekten.

### Vanes Up-Down Configuration dialog

| Parameter | Werte | Standard |
|---|---|---|
| Indoor unit has U-D Vanes | Yes / No | Yes |
| Available positions in Indoor Unit | 1–5 | 5 |
| Indoor unit has AUTO Vanes U-D | Yes / No | No |
| › Enable "Vanes U-D Man/Auto" objects (für Control und Status) | Yes / No | No |
| Enable "Vanes U-D Swing" objects (für Control und Status) | Yes / No | No |
| Enable use of +/- object for Vanes U-D | Yes / No | No |
| › DPT type for +/- Vane Up-Down Objekt | 0-Decrease/1-Increase [1.007] / 0-Up/1-Down [1.008] | 0-Decrease/1-Increase [1.007] |
| Enable use of bit-type Vane U-D objects (für Control) | Yes / No | No |
| Enable use of bit-type Vane U-D objects (für Status) | Yes / No | No |
| Enable use of Text object for Vane U-D | Yes / No | No |
| › Strings je Position (AUTO/POS1–5/SWING) | freier Text | "U-D AUTO"/"U-D POS 1"…"U-D POS 5"/"U-D SWING" |
| Enable use of Legacy_ object for Vanes (kompatibel zu alten XXACKNX1-Versionen) | Yes / No | No |

Die Man/Auto- und die Swing-Objekte verhalten sich identisch: eine "1"
schaltet in den Automatikbetrieb, eine "0" in den manuellen Betrieb mit
Position 1. Auch hier gilt: Positionsanzahl und Verfügbarkeit von
Auto/Swing müssen anhand der Innengerätedokumentation korrekt gesetzt
werden.

### Temperature Configuration dialog

| Parameter | Werte | Standard |
|---|---|---|
| Enable use of +/- obj for Setpoint Temp | Yes / No | No |
| › DPT type for +/- Setp Temp object | 0-Decrease/1-Increase [1.007] / 0-Up/1-Down [1.008] | 0-Decrease/1-Increase [1.007] |
| Ambient temp. ref. is provided from KNX | Yes / No | No |

Wird die Ambient-Temperatur-Referenz aktiviert (Control_ Ambient
Temperature, Objekt 27), gilt die in Abschnitt "Solltemperatur und
Ambient-Temperatur" beschriebene Verrechnungsformel; ohne Aktivierung regelt
das Innengerät weiterhin auf Basis seiner eigenen Ansaugtemperatur.

### Scene Configuration dialog

| Parameter | Werte | Standard |
|---|---|---|
| Enable use of scenes | Yes / No | Yes |
| Enable use of bit objects for scene execution | Yes / No | No |
| Enable use of bit objects for storing scenes | Yes / No | No |

Ist die Szenenfunktion aktiviert, genügt zur Ausführung über das Byte-Objekt
(32) ein Wert von "0" bis "4" (entspricht Szene 1 bis 5). Die zusätzlichen
Bit-Objekte zum Ausführen bzw. Speichern einzelner Szenen sind optional und
unabhängig voneinander zuschaltbar.

### Window Contact Configuration dialog

| Parameter | Werte | Standard/Beispiel |
|---|---|---|
| Enable use of Open Window function | Yes / No | No |
| › AC switch-off timeout (min) | frei wählbar | 10 (Beispielwert lt. Abbildung) |
| › Reload last On/Off val once window is closed | Yes / No | Yes (Beispielwert lt. Abbildung) |

Ist die Funktion aktiviert, startet eine "1" auf Objekt 29 (Control_ Window
Contact Status, sofern das Innengerät bereits läuft) die parametrierte
Abschaltverzögerung; eine "0" stoppt sie. Ist "Reload last On/Off val…"
aktiviert, wird nach Ablauf der Verzögerung der zuletzt gesendete Ein/Aus-
Wert wiederhergestellt: eine nach Timeout-Ende gesendete "1" schaltet das
Gerät wieder ein, eine "0" bewirkt keine Aktion. Ist die Option
deaktiviert, wird nach Timeout-Ende kein Wert wiederhergestellt.

## Angeschlossene Klimageräte – Funktionsumfang

Die folgenden Angaben stammen aus den Bedien- bzw. Installationsanleitungen
der drei Mitsubishi-Electric-Geräte. Diese Geräte besitzen selbst keine
KNX-Schnittstelle; angesteuert werden sie ausschließlich über das
Intesis-Gateway und die oben beschriebenen KNX-Objekte/ETS-Parameter.

### MSZ-LN18VG2W (Innengerät)

| Betriebsmodi | Lüfterstufen | Temperaturbereich | Besonderheiten |
|---|---|---|---|
| Auto, Kühlen (COOL), Trocknen (DRY), Heizen (HEAT), Ventilator (FAN) | Auto sowie 5 feste Stufen: Lautlos, Niedrig, Mittel, Hoch, Sehr Hoch | Sollwert in 1-°C-Schritten einstellbar; exakter Min./Max.-Sollwertbereich im Datenblatt nicht beziffert. Referenzwerte für den garantierten Betriebsbereich (mit MUZ-Außengerät): Kühlen 21–32 °C, Heizen 20–27 °C Raumtemperatur | Wandgerät der LN-Serie. Verfügt zusätzlich über i-see-Präsenzsensor (Airflow-Control-Modus, Absence Detection/Energiesparen bzw. Auto-Aus bei Abwesenheit), i-save-Speicherfunktion, ECONO COOL, Night Mode, Air-Purifying-Funktion (Plasma), Powerful-Betrieb, eigene Wochenschaltuhr sowie eine werkseitige Wi-Fi-Schnittstelle (MAC-597IFB-E) für MELCloud. Horizontale Lamellen (WIDE VANE, Links-Rechts-Schwenk) sind zusätzlich zur vertikalen Lamellenverstellung vorhanden. Laut Hersteller wird der Auto-Modus nicht empfohlen, wenn das Gerät an ein Multi-Split-Außengerät der MXZ-Reihe angeschlossen ist. |

**Bezug zu den Gateway-Objekten:** "Indoor unit has FAN mode" ist auf **Yes** zu setzen. Für "Available fanspeeds in Indoor Unit" stehen nur 4 feste Bit-/Byte-Stufen im Gateway zur Verfügung; die fünfte Gerätestufe ("Sehr Hoch") lässt sich über die separaten Fan-Speed-Bit-Objekte des Gateways nicht direkt adressieren, ist aber über die AUTO-Funktion und/oder die IR-Fernbedienung weiterhin erreichbar. "Available positions in Indoor Unit" = 5, "Indoor unit has AUTO Vanes U-D" = Yes. Die horizontale (Links-Rechts-) Lamellenverstellung des Geräts wird vom Gateway nicht abgebildet, da dessen Vanes-U-D-Objekte nur die vertikale Achse steuern.

### SLZ-M35FA2 (Innengerät)

| Betriebsmodi | Lüfterstufen | Temperaturbereich | Besonderheiten |
|---|---|---|---|
| Cool, Dry, Fan, Auto, Heat | Auto sowie 3 feste Stufen (Niedrig/Mittel/Hoch) | Kühlen/Trocknen: 19–30 °C; Heizen: 17–28 °C; Auto: 19–28 °C; im Fan-Betrieb nicht einstellbar | 4-Wege-Deckenkassette. Lamellen: Auto mit Schwingen sowie 5 feste Stufen (Step 1–5) plus Zugluftreduzierung und Einzelauslasssteuerung (4 Auslässe individuell einstellbar); horizontale Lamellenverstellung nicht verfügbar. Optional mit 3D-i-see-Sensor (Luftverteilung, Energiesparoption, Jahreszeitluftstrom) ausstattbar, sofern das Außengerät dies unterstützt. Filter ist langlebig ausgelegt, Reinigungsempfehlung alle 2.500 Betriebsstunden. |

**Bezug zu den Gateway-Objekten:** "Available fanspeeds in Indoor Unit" = 3, "Indoor unit has AUTO fan speed" = Yes. "Available positions in Indoor Unit" = 5, "Indoor unit has AUTO Vanes U-D" = Yes, Swing-Objekt nutzbar. Zu beachten: Das Gerät akzeptiert im Kühlen/Trocknen-Betrieb Sollwerte bis 30 °C, während das Gateway-Objekt "Control_ Setpoint Temperature" bzw. dessen +/‑-Variante werkseitig nur den Bereich 19–28 °C abdeckt (siehe Abschnitt "ETS-Parameter → Temperature Configuration dialog") – der obere Gerätebereich (29–30 °C im Kühlbetrieb) ist über KNX damit nicht erreichbar.

### MXZ-3F54VF4 (Außengerät)

| Betriebsmodi | Lüfterstufen | Temperaturbereich | Besonderheiten |
|---|---|---|---|
| Kühlen und Heizen (Multi-Split, kein eigenständiger Modusschalter – wird durch die angeschlossenen Innengeräte vorgegeben) | nicht separat einstellbar (außengeräteseitig automatisch geregelt) | Betriebsgrenzen laut Typenschild: HP 4,15 MPa, LP 2,30 MPa; Kältemittel R32, Füllmenge 2,4 kg (GWP 675 / 1,62 t CO₂-Äquivalent, werkseitig vorgefüllt) | Multi-Split-Außengerät mit 3 Kältemittel-Anschlüssen (Ports A–C) für bis zu 3 Innengeräte gleichzeitig (die größeren Varianten MXZ-4F72VF4/-4F80VF4 der gleichen Baureihe besitzen einen vierten Port D). Nennleistung MXZ-3F54VF4: Kühlen 5,4 kW / Heizen 7,0 kW (bei 230 V); Geräuschpegel 46 dB(A) Kühlen / 50 dB(A) Heizen; Nettogewicht 58 kg; Schutzart IP24. Per DIP-Schalter am Außengerät lassen sich zusätzlich eine Betriebsart-Verriegelung (nur Kühlen/Trocknen oder nur Heizen), ein Niedrigenergie-Standbymodus sowie eine Geräuschabsenkung konfigurieren – diese Einstellungen erfolgen ausschließlich am Außengerät selbst und sind über das KNX-Gateway nicht zugänglich. |

**Bezug zu den Gateway-Objekten:** Das Außengerät selbst hat keine direkte Entsprechung unter den KNX-Objekten des Intesis-Gateways; es begrenzt jedoch, welche Betriebsarten gleichzeitig an den angeschlossenen Innengeräten möglich sind (im Multi-Split-Verbund kann z. B. nicht ein Innengerät kühlen, während ein anderes heizt – siehe Hinweis "Multibetrieb" in der MSZ-LN-Bedienungsanleitung). Für jedes an das Außengerät angeschlossene Innengerät wird ein eigenes Intesis-Gateway (INKNXMIT001I000) benötigt, da jedes Gateway genau ein Innengerät ansteuert.

## Inbetriebnahme / Hinweise

- **Zwingende Geräteauswahl in ETS:** In den Parametern muss das exakt
  angeschlossene Innengerät bzw. dessen Eigenschaften (FAN-Modus,
  Lüfterstufenanzahl, AUTO-Lüfterstufe, Lamellenanzahl, AUTO-Lamellen)
  korrekt hinterlegt werden; andernfalls können nicht am Gerät verfügbare
  Funktionen als KNX-Objekte erscheinen bzw. real vorhandene Funktionen
  fehlen.
- **Anschluss:** Das Gateway wird über das mitgelieferte 1,9 m lange Kabel
  an die Innengeräte-Platine (Buchse CN92 bei Mr.-Slim-Modellen, CN105 bei
  übrigen Modellen) angeschlossen; die Kabellänge darf laut Hersteller
  nicht verändert werden, da dies die Funktion beeinträchtigen kann.
- **Szenen vs. Sperrobjekte:** Eine aktive Startszene (Initial Scene) hat
  Vorrang vor dem Control_-Lock-Remote-Control-Objekt; enthält sie den Wert
  "entsperrt" oder "unverändert" für die Fernbedienungssperre, wird die
  Sperre dadurch aufgehoben, auch wenn zuvor über KNX gesperrt wurde.
  
- **Ambient-Temperatur-Mapping:** Bei Nutzung von Objekt 27 (Control_
  Ambient Temperature) verschiebt sich die tatsächlich an das Innengerät
  gesendete Solltemperatur um die Differenz zwischen KNX-Ist- und
  KNX-Solltemperatur, bezogen auf die eigene Rücklauftemperatur des
  Innengeräts (Formel siehe Abschnitt "Solltemperatur und
  Ambient-Temperatur"). Die Verrechnung wird erst aktiv, nachdem beide
  beteiligten Objekte (25 und 27) mindestens einmal von der KNX-Anlage
  beschrieben wurden.
- **ETS-Datenbank:** Die aktuelle ETS-Produktdatenbank sowie das
  Benutzerhandbuch werden vom Hersteller online zum Download bereitgestellt
  (README.txt in der ZIP-Datei beachten).
- **Multi-Split-Betrieb (MXZ-3F54VF4):** Sind mehrere Innengeräte (hier
  MSZ-LN18VG2W und SLZ-M35FA2) an dasselbe MXZ-Außengerät angeschlossen,
  können diese nicht gleichzeitig gegensätzliche Betriebsarten fahren
  (nicht gleichzeitig kühlen und heizen); das zuletzt umgeschaltete
  Innengerät geht in diesem Fall in Bereitschaft. Dies betrifft auch
  KNX-seitig ausgelöste Modus-Wechsel über das jeweilige Intesis-Gateway.
- **Nicht per KNX steuerbare Funktionen:** Einige Funktionen der
  Innengeräte (z. B. i-see-Präsenzsteuerung, Airflow-Control, ECONO COOL,
  Night Mode, Air Purifying, Wi-Fi/MELCloud-Anbindung bei MSZ-LN18VG2W;
  3D-i-see-Optionen und Einzelauslass-Lamellensteuerung bei SLZ-M35FA2)
  sowie sämtliche außengeräteseitigen DIP-Schalter-Einstellungen des
  MXZ-3F54VF4 (Betriebsart-Verriegelung, Niedrigenergie-Standby,
  Geräuschabsenkung) besitzen keine Entsprechung unter den
  KNX-Kommunikationsobjekten des Intesis-Gateways und lassen sich nur über
  die Original-Fernbedienung bzw. am Außengerät selbst einstellen.

## Quelle

Gateway: `originals/KNX/Intesis_INKNXMIT001I000.pdf`

Klimageräte:
- `originals/Klimaanlage/MSZ-LN18VG2W._Innengeraet.pdf` (Bedienungsanleitung)
- `originals/Klimaanlage/SLZ-M35FA2_Innengeraet.pdf` (Bedienungshandbuch)
- `originals/Klimaanlage/MXZ-3F54VF4_Aussengeraet.pdf` (Installationsanleitung)
