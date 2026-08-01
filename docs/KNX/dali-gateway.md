---
title: MDT DaliControl IP64 Gateway
device_type: DALI-Gateway
manufacturer: MDT
article_number: [SCN-DALI64.03]
bus: KNX TP / DALI
source_pdf: originals/KNX/MDT_THB_DaliControl_IP64_Gateway_03.pdf
last_updated: 2026-07-25
synonyms: [DALI-Steuerung, DALI-KNX-Gateway, Lichtsteuerung DALI]
tags: [knx, dali-gateway, mdt]
---

## Übersicht

Das MDT DaliControl IP Gateway (SCN-DALI64.03) koppelt den KNX-Bus mit einem DALI-Segment. Es setzt Schalt- und Dimmbefehle aus dem KNX-System in DALI-Telegramme um und meldet umgekehrt Status- und Fehlerinformationen der DALI-Teilnehmer zurück auf den KNX-Bus. Das Gerät ist ein DALI-Gerät der sogenannten Kategorie 1 (gemäß EN 62386-103): Es darf nur an einem DALI-Segment betrieben werden, in dem keine weiteren DALI-Steuergeräte aktiv sind (kein Multi-Master-Betrieb).

Wesentliche Eigenschaften:
- Ansteuerung von bis zu **64 einzelnen EVGs**, organisiert in bis zu **16 DALI-Gruppen**
- Unterstützung von DALI-Vorschaltgeräten nach DT6 (Leuchtstofflampen/LED) und DT8 (Farbsteuerung: Tunable White, RGB, RGBW, XY, HSV)
- Integriertes Szenenmodul (16 Szenen mit individuellen Andimmzeiten), Effektmodul und Zeitsteuerungsmodul für zeit- bzw. farbabhängige Abläufe
- Betriebsarten Normalbetrieb, Dauerbetrieb, Nachtbetrieb, Treppenhausbetrieb und Panikbetrieb
- Unterstützung von Notleuchten (Einzelbatterie- und Zentralbatterie-Notbeleuchtung) inkl. Fehlererkennung und automatischen Testfunktionen
- Stromversorgung für bis zu 64 angeschlossene EVGs erfolgt direkt aus dem Gateway; eine zusätzliche DALI-Spannungsversorgung ist nicht zulässig
- Inbetriebnahme wahlweise über die ETS-App (DCA – Device Control App), über einen integrierten Webserver oder direkt über Tasten/Display am Gerät, jeweils auch ohne aktive KNX-Verbindung möglich
- Gehäuse: 4 TE breites Hutschienengehäuse zum Einbau in einen Elektroverteiler

Typische Einsatzszenarien sind Bürogebäude, Schulen oder Gewerbeobjekte, in denen große Mengen an DALI-Leuchten (z. B. LED-Panels, Tunable-White- oder RGB(W)-Leuchten) zentral über KNX geschaltet, gedimmt, in Szenen gesteuert und auf Fehler/Betriebsstunden überwacht werden sollen, inklusive der Ansteuerung von Notbeleuchtung.

## Technische Daten

| Merkmal | Wert |
|---|---|
| Artikelnummer | SCN-DALI64.03 |
| Max. Anzahl EVGs | 64 (Einzelansteuerung) |
| Max. Anzahl DALI-Gruppen | 16 |
| Max. Anzahl Szenen | 16 (mit individuellen Andimmzeiten) |
| Unterstützte DALI-Gerätetypen | DT6 (Standard-Vorschaltgeräte), DT8 (Farbsteuerung: Tunable White, RGB, RGBW, XY, HSV) |
| DALI-Kategorie | Kategorie 1 gemäß EN 62386-103 (kein Multi-Master-Betrieb) |
| DALI-Spannungsversorgung | Wird vom Gateway selbst bereitgestellt; externe DALI-Spannungsversorgung nicht zulässig/nicht erforderlich |
| Anzahl Kommunikationsobjekte | 1343 |
| KNX-Kommunikationsstack | System B |
| Bauform | 4 TE breites Hutschienengehäuse |
| Netzwerk/IP | Integrierter Webserver (HTTP, Standardport 80), IP-Adresse fest oder per DHCP |
| Inbetriebnahmewege | ETS5-App (DCA), Webserver, Tasten/Display am Gerät |

Hinweis: Die im PDF enthaltene Datenblatt-Seite (Kapitel 18.4) liegt als reine Grafik-/Layoutseite ohne extrahierbaren Text vor; genaue Angaben zu Abmessungen, Gewicht, Betriebsspannung (230 V/KNX-Busspannung), Schutzart (IP-Klasse), Betriebstemperaturbereich und Leistungsaufnahme sind **nicht im Datenblatt spezifiziert** (bzw. in dieser Textextraktion nicht auslesbar) und sollten bei Bedarf im separaten Produktdatenblatt bzw. der Montageanleitung nachgeschlagen werden.

## Kommunikationsobjekte

Das Gerät stellt insgesamt 1343 Kommunikationsobjekte bereit, gegliedert nach Funktionsblöcken. Viele Blöcke wiederholen sich pro Gruppe (1–16) bzw. pro EVG (1–64) mit fortlaufender Objektnummerierung; im Folgenden wird das jeweilige Muster anhand von Beispielobjekten (Gruppe 1 / EVG 1) beschrieben.

### Allgemeine Objekte

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 1 | Broadcast, Schalten | Ein/Aus | 1 Bit / 1.001 | K, S |
| 2 | Broadcast, Wertsetzen | Wert | 1 Byte / 5.001 | K, S |
| 3–6 | Broadcast, Farbsteuerung (RGB Rot/Grün/Blau/Weiß) | Wert | 1 Byte / 5.001 | K, S |
| 7 | Broadcast, Farbtemperatur | Wert | 2 Byte / 7.600 | K, S |
| 8 | Aktiviere Panikbetrieb | Aktivieren/Stoppen | 1 Bit / 1.010 | K, S |
| 9 | Aktiviere Testmodus | Aktivieren/Stoppen | 1 Bit / 1.010 | K, S |
| 10 | Aktiviere Nachtbetrieb | Aktivieren/Stoppen | 1 Bit / 1.010 | K, S |
| 11 | Starten/Programmieren Szenen | Szenen Nr. | 1 Byte / 18.001 | K, S |
| 12 | Starten/Stoppen Effekt | Effekt Nr. | 1 Byte | K, S |
| 13 | Generelle Fehler | Ja/Nein | 1 Byte / 5.010 | K, L, Ü |
| 14 | DALI Fehler | Ja/Nein | 1 Byte / 5.010 | K, L, Ü |
| 15–22a | Fehlerschwellen und Fehlersummen (generell, Lampe, EVG, Konverter, je als Bit-Meldung, Summenwert und %-Wert) | Ja/Nein bzw. Wert | 1 Bit (1.005) bzw. 1 Byte (5.010/5.001) | K, L, Ü |
| 23 | Status An/Aus Gruppe 1–16 | Status | 4 Byte / 27.001 | K, L, Ü |
| 24–27 | Status An/Aus EVG 1–16 / 17–32 / 33–48 / 49–64 | Status | 4 Byte / 27.001 | K, L, Ü |
| 29 | Status Fehler Lampe/EVG | Status | 1 Byte / 238.600 | K, S, Ü |
| 30 | Zeit | Zeit | 3 Byte / 10.001 | K, S, Ü, A |
| 31 | Datum | Datum | 3 Byte / 11.001 | K, S, Ü, A |

Objekt 1 (Broadcast Schalten) und Objekt 2 (Broadcast Wertsetzen) schalten bzw. setzen alle angeschlossenen Leuchten gleichzeitig. Befinden sich EVGs in einem Sonderzustand (Test- oder Panikbetrieb), werden sie beim Broadcast ausgenommen und stattdessen sequenziell angesprochen, wodurch sichtbare Verzögerungen zwischen den Leuchten entstehen können. Beide Objekte werden nur eingeblendet, wenn die Broadcast-Funktion in den Parametern "Allgemein → Spezielle Funktionen" aktiviert wurde; die Broadcast-Farbobjekte (3–7) erscheinen zusätzlich nur, wenn Broadcast auch für die Farbansteuerung freigegeben wurde.

Objekt 11 startet oder programmiert eine der 16 Szenen: Der reine Aufruf einer Szene erfolgt mit dem Wert der Szenennummer (0–15), das Programmieren (Überschreiben) der aktuell eingestellten Werte in eine Szene erfolgt durch Setzen des höchstwertigen Bits (Werte 128–143). Objekt 12 funktioniert analog für die 16 Effekte.

Die Fehlerobjekte (13–22a) unterscheiden zwischen genereller Fehlermeldung, reinem DALI-Kurzschluss sowie separaten Auswertungen für Lampen-, EVG- und Konverterfehler. Für jede dieser Kategorien existiert ein Grenzwert-Meldeobjekt (Ja/Nein, sobald ein parametrierter Schwellwert überschritten wird) sowie ein Summen- bzw. Prozentwert-Objekt. Wichtig: Ein EVG- oder Konverterfehler unterdrückt die gleichzeitige Zählung eines Lampenfehlers am selben Gerät, sodass jedes Gerät nur einmal in die Fehlersumme eingeht.

Die Statusobjekte 23–27 fassen den Schaltzustand aller 16 Gruppen bzw. jeweils 16 EVGs in einem 4-Byte-Objekt zusammen (jedes Bit steht für einen Teilnehmer; jeder Wert > 0 % gilt als "Ein"). Objekt 29 überträgt bei Änderung oder auf Anfrage einen kombinierten Fehlerstatus für ein einzelnes EVG (Bit 6 = Lampenfehler, Bit 7 = EVG-Fehler) und kann auch als Statusabfrage für ein bestimmtes EVG genutzt werden.

Die Objekte 30 (Zeit) und 31 (Datum) versorgen das interne Zeitsteuerungsmodul mit der aktuellen Uhrzeit/dem Datum; sie müssen von einer zentralen Zeitquelle im Bus mindestens zweimal täglich aktualisiert werden, da das Gerät weder Schaltjahre noch die Sommer-/Winterzeitumstellung selbstständig berücksichtigt.

### Objekte der EVGs (je EVG, Beispiel EVG 1)

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 480 | EVG1, Schalten | An/Aus | 1 Bit / 1.001 | K, S |
| 481 | EVG1, Dimmen | Heller/Dunkler | 4 Bit / 3.007 | K, S |
| 482 | EVG1, Wert setzen | Wert | 1 Byte / 5.001 | K, S |
| 483a | EVG1, Freigeben | Ja/Nein | 1 Bit / 1.003 | K, S |
| 483b | EVG1, Sperren | Ja/Nein | 1 Bit / 1.003 | K, S |
| 484 | EVG1, Status | An/Aus | 1 Bit / 1.001 | K, L, Ü |
| 485 | EVG1, Status | Wert | 1 Byte / 5.001 | K, L, Ü |
| 486 | EVG1, Fehlerstatus | Status | 1 Bit / 1.005 | K, L, Ü |
| 486a | EVG1, Fehlerstatus | Status | 1 Byte / 5.010 | K, L, Ü |
| 487 | EVG1, Betriebsstunden zurücksetzen | Ja/Nein | 1 Bit / 1.015 | K, S |
| 488 | EVG1, Betriebsstunden | Wert | 4 Byte / 13.100 | K, L, Ü |
| 489 | EVG1, Lebensdauer überschritten | Ja/Nein | 1 Bit / 1.002 | K, L, Ü |

Jedes der bis zu 64 EVGs erhält einen eigenen Satz dieser Objekte (Nummerierung fortlaufend ab 480). Schalten, Dimmen und Wertsetzen wirken nur, solange sich das EVG nicht in einem Sonderbetrieb (Testbetrieb Notleuchte, Panik-/Notbetrieb) befindet. Die Freigeben-/Sperren-Objekte (483a/483b) blenden sich nur ein, wenn der zugehörige Parameter "Funktion des zusätzlichen Objektes" entsprechend konfiguriert ist, und erlauben eine externe Bediensperre pro EVG. Der Betriebsstundenzähler (Objekt 488) kann über den Bus sowohl zurückgesetzt als auch auf einen beliebigen Wert vorbelegt werden; das Schreiben-Flag ist hier werkseitig deaktiviert. Überschreitet der Zähler die parametrierte Lebensdauer, wird dies über Objekt 489 gemeldet.

### Objekte für Notleuchten

Für Notleuchten (Konverter) bietet das Gerät zwei alternative Objektsätze an, die per Parameter ausgewählt werden:

**Variante "neuer KNX-Standard"** (Beispiel Konverter 1):

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 490 | Konverter 1, Test Start | Start | 1 Byte / 20.611 (DPT_Converter_Test_Control) | K, S |
| 491 | Konverter 1, Test Ergebnis | Test | 6 Byte / 245.600 | K, L, Ü |
| 492 | Konverter 1, Status | Status | 2 Byte / 244.600 | K, L, Ü |

Über Objekt 490 lassen sich Funktionstest (FT), Dauerbetriebstest (DT), Teil-Dauerbetriebstest (PDT) sowie das Stoppen laufender Tests und das Zurücksetzen der Testergebnis-Merker gemäß DALI-Kommandos steuern. Objekt 491 liefert strukturierte Testergebnisse (u. a. letztes Ergebnis von Funktions-, Dauer- und Teildauertest, Startart, verbleibende Batterieladung), Objekt 492 den aktuellen Betriebsmodus des Konverters (z. B. Normalbetrieb, Inhibit-Modus, Notbetrieb, laufender Test) sowie Hardware- und Testausstehend-Status.

**Variante "frühere Version"**: Hier werden Testauslösung (Objekt 490) und Testergebnis inkl. Batteriezustand (Objekt 491, 3 Byte) bitkodiert in kompakterer Form übertragen (z. B. einzelne Bits für "Funktionstest läuft", "Dauertest läuft", "Batterie defekt" usw.). Beide Varianten stehen nicht gleichzeitig zur Verfügung; die Auswahl erfolgt über den Parameter "Objekttyp für den Notleuchtenbetrieb".

### Objekte der Gruppen (je Gruppe, Beispiel Gruppe 1)

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 32 | G1, Schalten | Ein/Aus | 1 Bit / 1.001 | K, S |
| 33 | G1, Dimmen | Heller/Dunkler | 4 Bit / 3.007 | K, S |
| 34 | G1, Wert setzen | Wert | 1 Byte / 5.001 | K, S |
| 35 | G1, Wert setzen | Wert/Zeit | 3 Byte / 225.001 | K, S |
| 36 | G1, Freigeben | Ja/Nein | 1 Bit / 1.003 | K, S |
| 36a | G1, Sperren | Ja/Nein | 1 Bit / 1.003 | K, S |
| 36c | G1, Treppenhausfunktion sperren | Ja/Nein | 1 Bit / 1.003 | K, S |
| 37 | G1, Status | Ein/Aus | 1 Bit / 1.001 | K, L, Ü |
| 38 | G1, Status | Wert | 8 Bit / 5.001 | K, L, Ü |
| 39 | G1, Fehlerstatus | Ein/Aus | 1 Bit / 1.001 | K, L, Ü |
| 39a | G1, Fehlerstatus | Status | 1 Byte / 5.x | K, L, Ü |
| 40 | G1, Fehlerstatus | Status (Geräteanzahl + Fehlertypen) | 4 Byte | K, L, Ü |
| 41 / 41a / 41b / 41c | G1, Fehlerstatus/-rate | Ja/Nein bzw. Wert | 1 Bit (1.005) bzw. 1 Byte (5.010/5.000) | K, L, Ü |
| 56 | G1, Betriebsstunden zurücksetzen | Ja/Nein | 1 Bit / 1.015 | K, S |
| 57 | G1, Betriebsstunden | Wert | 4 Byte / 13.100 | K, S |
| 58 | G1, Lebensdauer überschritten | Ja/Nein | 1 Bit / 1.005 | K, S |
| 59 | G1, EVG Spannungsversorgung über Objekt schalten | Ein/Aus | 1 Bit / 1.001 | K, S |

Jede der bis zu 16 Gruppen erhält diesen Objektsatz. Grundfunktionen sind Schalten (32), relatives Dimmen (33) und Wertsetzen (34); Objekt 35 kombiniert Wert und Andimmzeit in einem 3-Byte-Objekt und wird nur eingeblendet, wenn der entsprechende Parameter aktiviert ist – dabei wird die separat parametrierte Dimmzeit ignoriert. Freigeben/Sperren (36/36a) sperrt die Bedienung der ganzen Gruppe, während 36c spezifisch nur die Treppenhausfunktion sperrt (z. B. für Reinigungszwecke). Die Fehlerobjekte 39–41c liefern gestaffelte Informationen von einer einfachen Ja/Nein-Meldung bis zu einer detaillierten 4-Byte-Aufschlüsselung nach Geräteanzahl und Fehlertyp (normale/Notleuchten-EVGs, Lampen, Konverter). Objekt 59 ermöglicht in Verbindung mit einem externen Schaltaktor eine echte Abschaltung der EVG-Spannungsversorgung zur Energieeinsparung: Beim Ausschalten aller EVGs der Gruppe wird das Objekt verzögert auf 0 gesetzt, beim Einschalten sofort auf 1, gefolgt von einer 300-ms-Wartezeit vor dem ersten DALI-Telegramm.

### Objekte zur Farbansteuerung

Je nach in der Gruppe gewähltem Farbtyp (Farbtemperatur, RGB, HSV, RGBW, XY) werden unterschiedliche Objektsätze eingeblendet; pro Gruppe ist jeweils nur ein Farbtyp aktiv, und nur EVGs, die diesen Typ unterstützen, reagieren darauf.

| Farbtyp | Wesentliche Objekte (Beispiel G1) | DPT |
|---|---|---|
| Farbtemperatur | 42 Wert (Kelvin), 43 Wert relativ (%), 47 Farbwechsel (4 Bit), 51 Status | 7.600 / 5.001 / 3.007 / 7.600 |
| RGB (kombiniert) | 42 Wert RGB, 51 Status RGB | 232.600 |
| RGB (getrennt) | 43–45 Wert R/G/B, 47–49 Farbwechsel R/G/B, 52–54 Status R/G/B | 5.001 / 3.007 / 5.001 |
| HSV | 43 Farbton, 44 Sättigung (Wert V über separates Objekt Nr. 41), 47–48 Farbwechsel, 52–53 Status | 5.003 / 5.001 / 3.007 |
| RGBW (kombiniert) | 42 Wert RGBW, 51 Status RGBW | 251.600 |
| RGBW (getrennt) | 43–46 Wert R/G/B/W, 47–50 Farbwechsel, 52–54(+) Status | 5.001 / 3.007 |
| XY (kombiniert) | 42 Wert XY (inkl. Helligkeit), 51 Status | 242.600 |
| XY (getrennt) | 42 Wert X, 43 Wert Y, 51 Status X, 52 Status Y | 7.001 |

Bei der Farbtemperatur wird der Wert in Kelvin (unter 3000 K "Warmweiß", über 5000 K "Kaltweiß") oder relativ in Prozent übertragen. Beim HSV-Modell wird die Farbe über Farbton (0–360°, Auflösung durch DPT 5.003 auf ca. 1,4° begrenzt), Sättigung und Intensität definiert, wobei der Helligkeitswert über das separate Wertobjekt (Nr. 41 der Gruppen-Grundobjekte) gesteuert wird. Beim kombinierten RGBW-Objekt (DPT 251.600) sind zusätzlich 4 Gültigkeits-Bits enthalten, die angeben, welche der übertragenen Farbkanäle tatsächlich gültig sind. Bei XY-Koordinaten wird der Bereich 0–1 auf den KNX-Ganzzahlbereich 0–65535 abgebildet; X = Y = 0,33 entspricht dem Weißpunkt.

### Objekte der Szenen und des Zeitsteuerungsmoduls

Die Szenenobjekte 11 (Starten/Programmieren, siehe oben) und 12 (Effekt Starten/Stoppen) sind im Kanal "Szenen" zusammengefasst. Zusätzlich existiert je Szene ein Dimm-Objekt (ab Nr. 1312, 4 Bit), über das die aktuell aktive Szene relativ gedimmt werden kann – dabei bleiben die für die jeweiligen Gruppen in der ETS definierten Min-/Max-Grenzwerte wirksam.

Für das Zeitsteuerungsmodul (Farbsteuerungs-Vorlagen/Templates) steht je Vorlage (bis zu 16) ein Aktivierungsobjekt zur Verfügung (ab Objekt 1328, 1 Bit, DPT 1.010): Bei Wert 1 ist die Vorlage aktiv und wird gemäß dem im DCA hinterlegten Zeitplan ausgeführt; bei 0 ist sie gesperrt. Die Freigabe der Vorlagen für die Bus-Steuerung muss zusätzlich im DCA unter "Zeitsteuerung" erfolgen.

## ETS-Parameter

### Parameterblock "Allgemein"

**Verhalten** (u. a. Reaktion auf Busereignisse):

| Parameter | Werte | Standard |
|---|---|---|
| Verhalten bei KNX Fehler | keine Aktion / Schalten auf Einschaltwert / Ausschaltwert / Panikwert | nicht im Datenblatt spezifiziert |
| Verhalten bei KNX Spannungswiederkehr | keine Aktion / Schalten auf letzten Wert / Einschaltwert / Ausschaltwert | nicht im Datenblatt spezifiziert |
| Sendeverzögerung bei KNX Wiederkehr | Sofort … 60 Sekunden (Stufen) | nicht im Datenblatt spezifiziert |
| Sendebedingung Lichtstatus | auf Anfrage / bei Änderung / bei Änderung und Busreset | nicht im Datenblatt spezifiziert |
| Senden des Wertstatus während des Dimmens | ab >2/5/10/20 % Änderung / inaktiv | nicht im Datenblatt spezifiziert |
| Sendeverzögerung zwischen Statusobjekten | keine … 5 Sekunden | nicht im Datenblatt spezifiziert |
| Verhalten nach Panikbetrieb | Ausschaltwert / Einschaltwert / letzter Wert | nicht im Datenblatt spezifiziert |

Diese Parameter steuern das globale Verhalten aller angeschlossenen EVGs/Gruppen bei Busausfall bzw. -wiederkehr sowie das Timing des Statusversands. Die Sendeverzögerung bei KNX-Wiederkehr ist besonders in Anlagen mit mehreren Gateways relevant: Durch unterschiedliche Einstellung je Gerät wird verhindert, dass alle Gateways gleichzeitig mit dem Senden der Statusobjekte beginnen und den Bus belasten.

**Analyse und Wartung**:

| Parameter | Werte | Standard |
|---|---|---|
| Sendebedingung der Fehlerobjekte | auf Anfrage / bei Änderung / bei Änderung und Busreset | nicht im Datenblatt spezifiziert |
| Sendeverzögerung zwischen den Fehlerobjekten | keine … 5 Sekunden | nicht im Datenblatt spezifiziert |
| Zykluszeit für Fehlerabfragen | keine Abfragen / 0,5 … 10 Sekunden | nicht im Datenblatt spezifiziert |
| Typ des zentralen EVG-Fehlerobjektes | kein Objekt / DALI Diagnose (1 Byte) | nicht im Datenblatt spezifiziert |
| Funktion des zusätzlichen Fehlerobjektes | Anzahl der Fehler insgesamt / Fehlerrate 0–100 % | nicht im Datenblatt spezifiziert |
| Fehlergrenzwert (generell / Lampe / EVG / Konverter) | 1–100 % | nicht im Datenblatt spezifiziert |

Die zyklische Fehlerabfrage ist notwendig, um Lampen- und EVG-Fehler überhaupt zu erkennen, da diese aktiv über DALI-Telegramme abgefragt werden müssen. Bei der Einstellung "Keine Abfragen" werden keine EVG- und Lampenfehler mehr erkannt; laut Handbuch sollte diese Einstellung nur für Service-/Spezialfälle verwendet werden. Die Fehlergrenzwerte definieren jeweils die Schwelle (bezogen auf die Gesamtzahl der betroffenen Geräte im Segment), ab der das zugehörige Alarmobjekt sendet.

**Spezielle Funktionen**:

| Parameter | Werte | Standard |
|---|---|---|
| Broadcast freigeben | Nein / Ja | nicht im Datenblatt spezifiziert |
| Objekt für Broadcast Farbtemperatur | Nein / Ja | nicht im Datenblatt spezifiziert |
| Broadcast für Farb-EVGs (DT8) | keine / RGB / RGBW / XY Farbe | nicht im Datenblatt spezifiziert |
| Auswahl des Objekttyps (RGB/RGBW) | kombiniertes Objekt / getrennte Objekte / HSV(W) getrennt | nicht im Datenblatt spezifiziert |
| Bedienung am Gerät sperren | Nein / Ja | nicht im Datenblatt spezifiziert |
| Objekttyp für den Notleuchtenbetrieb | Neu / Alt | nicht im Datenblatt spezifiziert |

Die Aktivierung von "Broadcast freigeben" schaltet die zentralen Broadcast-Kommunikationsobjekte (Nr. 1–7) frei, mit denen alle EVGs gleichzeitig unabhängig von der Gruppenzuordnung geschaltet, gedimmt bzw. farblich angesteuert werden können. Statusinformationen der Broadcast-Farbansteuerung werden dabei nur aktualisiert, wenn der gewählte Broadcast-Farbtyp mit dem in der jeweiligen Gruppe konfigurierten Farbtyp übereinstimmt.

**IP-Einstellungen**:

| Parameter | Werte | Standard |
|---|---|---|
| Zugriff über Webseiten erlaubt | Nein / Ja | nicht im Datenblatt spezifiziert |
| Vergabe der IP-Adresse | Feste IP-Adresse / DHCP | nicht im Datenblatt spezifiziert |
| IP-Adresse, Subnetz, Gateway | IPv4-Eingabe | – |
| HTTP-Port | Zahlenwert | 80 |
| Passwort Visualisierung | max. 8 Zeichen | Benutzer "user" |
| Passwort Administration | max. 8 Zeichen | Benutzer "admin" |

Der Webserver dient sowohl zur Visualisierung/Bedienung als auch zur DALI-Inbetriebnahme und für Firmware-Updates. Wird der Webzugriff über die ETS deaktiviert, ist auch kein Firmware-Update mehr über die IP-Verbindung möglich; der Zugriff muss dann zuerst wieder über die ETS erlaubt werden. Ein leeres Administrations-Passwort ist nicht zulässig, ein leeres Visualisierungs-Passwort führt zu einem direkten, passwortlosen Zugriff auf die Visualisierungsseite.

### Parameterblock "Gruppe" (je Gruppe konfigurierbar)

**Allgemein**:

| Parameter | Werte | Standard |
|---|---|---|
| Gruppenbeschreibung | Freitext | – |
| Betriebsart | Normalbetrieb / Dauerbetrieb / Nachtbetrieb / Treppenhausfunktion | nicht im Datenblatt spezifiziert |
| Wert bei Dauerbetrieb | 0–100 % | 50 % |
| Verhalten im Nachtbetrieb | verzögertes Ausschalten (ggf. 2-stufig) / verzögertes Abdimmen / Dauerbetrieb + Telegramme ignorieren | nicht im Datenblatt spezifiziert |
| Automatisches Ausschalten nach (Nachtbetrieb) | 1–90 Minuten | nicht im Datenblatt spezifiziert |
| Verhalten im Treppenhausbetrieb | wie Nachtbetrieb | nicht im Datenblatt spezifiziert |
| Automatisches Ausschalten nach (Treppenhausbetrieb) | 1–90 Minuten | nicht im Datenblatt spezifiziert |
| Funktion des zusätzlichen Objektes | kein Objekt / Sperrobjekt / Freigabeobjekt / Treppenhausfunktion Sperrobjekt | nicht im Datenblatt spezifiziert |
| Verhalten beim Freigeben | keine Änderung / Einschaltwert / Ausschaltwert | nicht im Datenblatt spezifiziert |
| Freigegeben für Panikbetrieb | Nein / Ja | nicht im Datenblatt spezifiziert |
| Wert im Panikbetrieb | 1–100 % | nicht im Datenblatt spezifiziert |
| Wert bei DALI-Spannungsausfall (System Failure Level) | 0–100 % / letzter Wert | 100 % |
| Wert bei EVG-Spannungswiederkehr (Power On Level) | 0–100 % / letzter Wert | 100 % |
| EVG-Spannungsversorgung über Objekt schalten | Nein / Ja | nicht im Datenblatt spezifiziert |
| Verzögerung bis zum Ausschalten der EVG-Spannungsversorgung | 10 s – 10 Minuten | nicht im Datenblatt spezifiziert |
| Art der Berechnung der Dimmwerte | logarithmisch / halblogarithmisch | nicht im Datenblatt spezifiziert |

"Dauerbetrieb" hält die Gruppe fest auf einem parametrierten Wert; Schalt- oder Dimmtelegramme haben in diesem Modus keine Wirkung. "Nachtbetrieb" und "Treppenhausfunktion" definieren jeweils ein zeitgesteuertes automatisches Abschaltverhalten (direkt, zweistufig mit Zwischenstufe auf 50 %, oder sanftes Abdimmen), das über das zentrale Nachtobjekt (Nr. 10) bzw. objektseitig ausgelöst wird. Der "System Failure Level" wird bei Ausfall der DALI-Spannung im EVG selbst gespeichert und automatisch angefahren, sobald die Spannung wieder anliegt – unabhängig vom KNX-Bus. Die Option "EVG-Spannungsversorgung über Objekt schalten" blendet Kommunikationsobjekt 59 ein und ermöglicht per externem KNX-Schaltaktor eine echte Netzabschaltung der EVGs zur Energieeinsparung.

**Verhalten**:

| Parameter | Werte | Standard |
|---|---|---|
| Einschaltwert | 1–100 % / letzter Wert | nicht im Datenblatt spezifiziert |
| Einschaltverhalten | sofort / Dimmen auf Wert in 3 s – 10 min | nicht im Datenblatt spezifiziert |
| Ausschaltwert | 0–99 % | nicht im Datenblatt spezifiziert |
| Ausschaltverhalten | sofort / Dimmen auf Wert in 3 s – 10 min | nicht im Datenblatt spezifiziert |
| Verhalten beim Wertsetzen | sofort / Dimmen auf Wert in 3 s – 10 min | nicht im Datenblatt spezifiziert |
| Zeit zum Dimmen (relatives Dimmen) | 3–60 Sekunden | nicht im Datenblatt spezifiziert |
| Max./Min. Wert zum Dimmen | 0–100 % bzw. 0–50 % | nicht im Datenblatt spezifiziert |
| Min/Max Werte gültig für | Dimmobjekt / Wertobjekt / beide | nicht im Datenblatt spezifiziert |
| Einschalten via Dimmen | Nein / mit Dimmobjekt / Wertobjekt / beidem | nicht im Datenblatt spezifiziert |
| Zusätzliches Wertsetzen-Objekt mit Andimmzeit | Nein / Ja | nicht im Datenblatt spezifiziert |

Die Dimm-/Einschalt-/Ausschaltzeiten beziehen sich jeweils auf den vollen Wertebereich (0–100 %): Eine parametrierte Zeit von 30 s für eine Wertänderung über 100 % bedeutet z. B., dass eine Änderung um nur 50 % (etwa beim Szenenaufruf) in 15 s erfolgt. Min-/Max-Werte begrenzen den über relatives Dimmen erreichbaren Bereich und können wahlweise nur für das 4-Bit-Dimmobjekt, nur für das Wertsetzen-Objekt oder für beide gemeinsam gelten – dadurch lässt sich z. B. ein Dimm-Maximum von 60 % definieren, während über Wertsetzen weiterhin 100 % erreichbar bleiben.

**Analyse und Wartung**:

| Parameter | Werte | Standard |
|---|---|---|
| Typ des Fehlerstatusobjektes | 1 Bit / 1 Byte | nicht im Datenblatt spezifiziert |
| Zusätzliche Fehlerobjekte | Nein / Ja | nicht im Datenblatt spezifiziert |
| Zusätzliches Fehlerobjekt für | Fehlergrenzwert überschritten / Fehleranzahl/-rate | nicht im Datenblatt spezifiziert |
| Fehlergrenzwert für Fehleralarmobjekt | 1–100 % | 1 % |
| Betriebsstunden Berechnung | Ja / Nein | nicht im Datenblatt spezifiziert |
| Betriebsstunden Grenzwert | 1–200.000 h | 4000 h |

Diese Parameter steuern, in welcher Granularität Fehler- und Betriebsstunden-Informationen je Gruppe über den Bus gemeldet werden (einfache 1-Bit-Meldung vs. differenziertes 1-Byte-Objekt) sowie den Schwellwert, ab dem der Betriebsstundenzähler eine Lebensdauer-Warnung auslöst.

**Farbsteuerung** (nur bei aktivierter Farbansteuerung der Gruppe):

| Parameter | Werte | Standard |
|---|---|---|
| Typ der Farbsteuerung | keine / Farbtemperatur / RGB / RGBW / XY | nicht im Datenblatt spezifiziert |
| Farbtemperatur beim Einschalten | 1000–10000 K | 3000 K |
| Farbwert / X-/Y-Wert beim Einschalten | Farbauswahl bzw. 0–1 | X=Y=0,33 (Weißpunkt) |
| Zusätzlicher Weißwert (RGBW) | 0–100 % | nicht im Datenblatt spezifiziert |
| Verhalten beim Einschalten | letzten Objektwert behalten / ETS-Parameter nutzen | nicht im Datenblatt spezifiziert |
| Zeit beim Farbwechsel | sofort / 1–90 Sekunden | nicht im Datenblatt spezifiziert |
| Zeit beim Farbwechsel via Dimmen | schnell (10 s) / Standard (20 s) / langsam (40 s) | nicht im Datenblatt spezifiziert |
| Auswahl des Objekttyps (RGB/RGBW/XY) | kombiniertes Objekt / getrennte Objekte / HSV(W) | nicht im Datenblatt spezifiziert |

Wichtig ist, dass innerhalb einer Gruppe stets nur ein Farbansteuerungstyp aktiv ist; es muss sichergestellt werden, dass alle EVGs einer Gruppe denselben Farbtyp unterstützen, da andersartige Geräte auf die entsprechenden Farbtelegramme nicht reagieren. Bei "letzten Objektwert behalten" wird nach einem Ausfall der bisherige Farbwert wiederhergestellt, sofern dieser gültig ist – andernfalls greift automatisch der in der ETS parametrierte Startwert.

### Parameterblock "EVG" (nur relevant für nicht gruppierte Einzel-EVGs)

**Allgemein**:

| Parameter | Werte | Standard |
|---|---|---|
| EVG-Beschreibung | Freitext | – |
| EVG-Typ | Leuchtstofflampe / Einzelbatterienotleuchte / Entladungslampe / Niedervoltlampe / Glühlampe / 0–10V-Konverter / LED-Modul / Relaismodul / EVG mit Farbsteuerung | nicht im Datenblatt spezifiziert |
| Betriebsart | Normalbetrieb / Dauerbetrieb / Normal-/Nachtbetrieb | nicht im Datenblatt spezifiziert |
| Wert bei Dauerbetrieb | 1–100 % | 50 % |
| Verhalten im Nachtbetrieb | wie bei Gruppe | nicht im Datenblatt spezifiziert |
| EVG freigeben für Not-/Panikbetrieb | Ja / Nein | nicht im Datenblatt spezifiziert |
| Wert bei DALI-Spannungsausfall / EVG-Spannungswiederkehr | 0–100 % / letzter Wert | 100 % |
| Art der Berechnung der Dimmwerte | logarithmisch / linear | nicht im Datenblatt spezifiziert |
| Betriebsstunden Berechnung / Grenzwert | Ja/Nein bzw. 1–200.000 h | 4000 h |
| Typ des Fehlerobjektes | 1 Bit / 1 Byte | nicht im Datenblatt spezifiziert |
| Notbeleuchtung mit Zentralbatterie | Keine Notbeleuchtung / Notbeleuchtung mit Zentralbatterie | nicht im Datenblatt spezifiziert |
| Wert / Zeitdauer im Testbetrieb | 1–100 % bzw. 5 Min–4 Std | nicht im Datenblatt spezifiziert |

Diese Seite ist nur sichtbar, wenn das EVG nicht Teil einer Gruppe, sondern als Einzelgerät konfiguriert ist. Die Parameter entsprechen inhaltlich weitgehend denen auf Gruppenebene, gelten hier aber individuell für das einzelne EVG. Die Kennzeichnung als "Notbeleuchtung mit Zentralbatterie" sorgt dafür, dass das Gerät bei Statusmeldungen gesondert markiert wird und der objektgesteuerte Testbetrieb (Objekt 9) einen fest definierten Testwert für eine parametrierbare Dauer anfährt.

**Einstellung Notbetrieb** (nur bei EVG-Typ "Einzelbatterienotleuchte"):

| Parameter | Werte | Standard |
|---|---|---|
| Wert im Notbetrieb | 1–100 % | 50 % |
| Verzögerung bei Spannungswiederkehr | keine … 10 Minuten | nicht im Datenblatt spezifiziert |
| Intervall des Dauerbetriebstests | kein automatischer Test / 1–52 Wochen | nicht im Datenblatt spezifiziert |
| Intervall des Funktionstests | kein automatischer Test / 1–28 Tage | nicht im Datenblatt spezifiziert |
| Zeitüberschreitung nach Teststart | 0–255 Tage | 10 Tage (0 = 15 Minuten) |

Diese Parameter steuern das automatische, konverterinterne Testregime für Einzelbatterie-Notleuchten gemäß EN 62386-202: Kann ein Test (z. B. wegen unzureichend geladener Batterie) nicht sofort starten, versucht der Konverter es innerhalb des parametrierten Zeitfensters erneut, bevor ein Zeitüberschreitungsfehler gemeldet wird.

## Inbetriebnahme / Hinweise

- **Zweistufiger Ablauf:** Vor der eigentlichen DALI-Installation können Planung, Benennung der EVGs und Gruppenzuordnung bereits offline (ohne Verbindung zum Gateway) im DCA vorbereitet werden. Die eigentliche DALI-Inbetriebnahme (Suchen und Zuordnen der realen Geräte) erfordert dagegen zwingend eine Online-Verbindung zum Gerät.
- **DALI-Neuinstallation:** Der erste Schritt jeder Installation ist die Neuinstallation, bei der alle angeschlossenen EVGs zurückgesetzt und neu eingelernt werden. Da die DALI-Kurzadressen (0–63) dabei zufällig auf Basis einer zufällig generierten Langadresse vergeben werden, ist die Zuordnung nach der Neuinstallation zunächst ungeordnet. **Achtung:** Jede erneute Neuinstallation setzt alle EVGs erneut zurück und überschreibt bereits vorgenommene Konfigurationen.
- **Identifikation der EVGs:** Nach der Neuinstallation müssen die gefundenen EVGs den geplanten Leuchten zugeordnet werden, typischerweise durch Blinken oder Ein-/Ausschalten der jeweiligen Leuchte. Für Einzelbatterie-Notleuchten nach DT-1, die kein normales Schalten unterstützen, gibt es gemäß EN 62386-202 einen speziellen Identifikationszustand (meist Blinken der Kontroll-LED am Konverter).
- **EVG-Schnellaustausch:** Bei Defekt eines einzelnen EVGs kann das Gateway die gespeicherte Konfiguration (Kurzadresse, Gruppenzugehörigkeit etc.) automatisch auf ein neu eingesetztes Ersatzgerät gleichen Typs übertragen. Funktioniert nur, wenn genau ein Gerät defekt und durch genau ein neues Gerät desselben Typs ersetzt wurde; andernfalls liefert das Gateway einen spezifischen Fehlercode (z. B. "kein EVG defekt", "mehr als ein EVG defekt", "falscher Gerätetyp").
- **DALI-Nachinstallation:** Für die Erweiterung eines bereits laufenden Segments um neue EVGs oder den Austausch mehrerer defekter Geräte gleichzeitig ist die Nachinstallation zu verwenden (verfügbar am Gerät, im Webserver als Administrator oder in der ETS im Extended Mode). Nicht mehr auffindbare EVGs werden dabei aus der Konfiguration gelöscht – daher ist sicherzustellen, dass zum Zeitpunkt der Nachinstallation alle EVGs spannungsversorgt sind, um ein versehentliches Löschen zu vermeiden. Die maximale Grenze von 64 EVGs pro Segment ist zu beachten.
- **Mehrere Gateways im selben Projekt:** Über die parametrierbare Sendeverzögerung bei KNX-Spannungswiederkehr kann verhindert werden, dass mehrere Gateways nach einem Busreset gleichzeitig ihre Statusobjekte senden und den Bus kurzzeitig überlasten.
- **Broadcast vs. Gruppenparameter:** Die Broadcast-Schaltfunktion schaltet grundsätzlich hart auf 0 % oder 100 % und ignoriert dabei die für Gruppen/EVGs parametrierten Ein-/Ausschaltwerte.
- **Kategorie-1-Gerät:** Da es sich um ein DALI-Gerät der Kategorie 1 handelt, dürfen im selben DALI-Segment keine weiteren DALI-Steuergeräte (Multi-Master) betrieben werden.

## Quelle

MDT technologies GmbH, Technisches Handbuch – DaliControl IP Gateway SCN-DALI64.03 (Stand 2/2019).
Datei: `originals/KNX/MDT_THB_DaliControl_IP64_Gateway_03.pdf`
