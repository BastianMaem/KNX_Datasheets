---
title: Theben Meteodata 140 S GPS
device_type: Wetterstation
manufacturer: Theben AG
article_number: [1409208]
bus: KNX TP
source_pdf: originals/KNX/Theben_Meteodata_140_S_Handbuch.pdf
last_updated: 2026-07-25
synonyms: [Wettersensor, Windsensor, Helligkeitssensor, Wetterstation mit GPS]
tags: [knx, wetterstation, theben]
---

## Übersicht

Die Meteodata 140 S GPS ist eine KNX-Wetterstation, die Temperatur, Helligkeit aus drei Blickrichtungen (vorne, links, rechts), Windgeschwindigkeit und Niederschlag (nur binär: Regen / kein Regen) erfasst und diese Werte auf den Bus sendet. Die GPS-Variante ermittelt Datum, Uhrzeit sowie Standortkoordinaten (Breiten-/Längengrad) selbstständig per Satellitenempfang und benötigt dadurch keine externe Zeitquelle über den Bus.

Aus den Messwerten sowie – bei der GPS-Variante – aus dem berechneten Sonnenstand (Azimut/Elevation) lassen sich im Applikationsprogramm mehrere Funktionsblöcke parametrieren:

- **Universalkanäle (C1–C10):** frei konfigurierbare Bedingungen auf Basis von Helligkeit, Temperatur, Wind und Regen (UND/ODER-verknüpfbar), z. B. für Wind- oder Frostalarme, die als Sicherheitsmeldung an Antriebsaktoren weitergegeben werden.
- **Sonnenschutzkanäle (C11–C13, C24–C28):** Ansteuerung von Rollläden, Jalousien oder Markisen, wahlweise rein helligkeitsgesteuert oder mit echter Sonnenstandnachführung (Lamellen-/Behangposition folgt dem tatsächlichen Sonnenverlauf).
- **Schwellwertkanäle (C14–C17):** vom Bus empfangene Zahlen-/Prozent-/Gleitkommawerte werden mit einer Schwelle verglichen und lösen bei Über-/Unterschreitung ein Schaltverhalten aus.
- **Logikkanäle (C18–C23):** UND-/ODER-/XOR-Verknüpfung von bis zu vier 1-Bit-Eingängen, wobei auch die Zustände der Universal- und Schwellwertkanäle als Eingang genutzt werden können.

Typischer Einsatzzweck ist die automatische, wettergeführte Beschattungssteuerung mit integrierter Sicherheitsfunktion (Wind-, Regen-, Frostschutz), bei der die Wetterstation die Sensorik bereitstellt und die eigentliche Antriebsansteuerung in einem separaten Jalousie-/Rollladenaktor erfolgt.

## Technische Daten

Angaben gelten für die Netzspannungs-Variante Meteodata 140 S / 140 S GPS (110–230 V AC). Für die 24-V-Varianten (1409201 / 1409204) gelten abweichende Versorgungsdaten, die hier nicht relevant sind.

| Kenngröße | Wert |
|---|---|
| Betriebsspannung | 110–230 V AC |
| Betriebsspannung KNX | 21–32 V DC / ≤ 3 mA |
| Eigenverbrauch | typ. 0,7 W (max. 5,5 W) |
| Montageart | Wand- bzw. Mastbefestigung |
| Abmessungen (H x B x T) | 84 x 121 x 227 mm |
| Anschlussart | Federsteckklemme & KNX-Busklemme |
| Max. Leitungsquerschnitt | 1,5 mm² |
| Umgebungstemperatur | -20 °C … +55 °C |
| Schutzart | IP44 nach EN 60529 |
| Schutzklasse | II bei bestimmungsgemäßer Montage |

**Messbereiche:**

| Messgröße | Bereich |
|---|---|
| Helligkeit | 1 … 100.000 Lux |
| Temperatur | -30 … 60 °C |
| Wind | 2 – 30 m/s |
| Niederschlag | Regen / kein Regen (binär, kein Regenmengensensor) |

Sensorik: 3 fest eingebaute Helligkeitssensoren im 90°-Versatz (vorne, links, rechts) sowie ein Regenfühler mit optionaler Tauunterdrückung/Beheizung. Zusätzlich stehen zwei Objekte zur Verfügung, um Helligkeitswerte externer Sensoren (z. B. Theben Luna 133 KNX) für weitere Fassaden einzubinden.

Applikationsprogramm: „Meteodata 140 S V1.2" (Hersteller: THEBEN AG, Produktfamilie: Phys. Sensoren, Produkttyp: Wetterstationen). Umfang: 186 Kommunikationsobjekte, 254 Gruppenadressen, 255 Zuordnungen.

## Kommunikationsobjekte

### Physikalische Werte (Obj. 0–19)

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 0 | Helligkeitswert vorne | Physikalischer Wert | 2 Byte 9.004 | K L - Ü |
| 1 | Helligkeitswert links | Physikalischer Wert | 2 Byte 9.004 | K L - Ü |
| 2 | Helligkeitswert rechts | Physikalischer Wert | 2 Byte 9.004 | K L - Ü |
| 3 | Maximaler Helligkeitswert | Physikalischer Wert | 2 Byte 9.004 | K L - Ü |
| 4 | Temperaturwert | Physikalischer Wert | 2 Byte 9.001 | K L - Ü |
| 5 | Windgeschwindigkeit (m/s) | Physikalischer Wert | 2 Byte 9.005 | K L - Ü |
| 5 | Windgeschwindigkeit (km/h) | Physikalischer Wert | 2 Byte 9.028 | K L - Ü |
| 5 | Windgeschwindigkeit (Bft) | Physikalischer Wert | 1 Byte 20.014 | K L - Ü |
| 6 | Regenmelder | Regen / kein Regen | 1 Bit 1.001 | K L - Ü |
| 7 | n.b. | – | – | – |
| 8 | Lokale Zeit (senden) | senden | 3 Byte 10.001 | K - - Ü |
| 8 | Lokale Zeit (empfangen) | empfangen | 3 Byte 10.001 | K - S - |
| 9 | Datum (senden) | senden | 3 Byte 11.001 | K - - Ü |
| 9 | Datum (empfangen) | empfangen | 3 Byte 11.001 | K - S - |
| 10 | Zeitanfrage (senden) | senden | 1 Bit 1.001 | K L - Ü |
| 10 | Zeitanfrage (empfangen) | empfangen | 1 Bit 1.001 | K - S - |
| 11 | Status Zeit | 1 = Zeit gültig | 1 Bit 1.001 | K - - Ü |
| 12 | Elevation | 0° = Horizont | 4 Byte 14.007 | K L - Ü |
| 13 | Azimut | N=0°, E=90°, S=180°, W=270° | 4 Byte 14.007 | K L - Ü |
| 14 | n.b. | – | – | – |
| 15 | Temperatursensor Status | 0 = OK, 1 = defekt | 1 Bit 1.001 | K L - Ü |
| 16–17 | n.b. | – | – | – |
| 18 | Externer Luxwert 1 | empfangen | 2 Byte 9.004 | K L S - |
| 19 | Externer Luxwert 2 | empfangen | 2 Byte 9.004 | K L S - |

**Erläuterung:** Die Objekte 0–3 geben die drei eingebauten Helligkeitssensoren sowie deren Maximalwert aus; extern empfangene Helligkeitswerte (Obj. 18/19) fließen dort nicht mit ein, sondern stehen separat für andere Kanäle zur Verfügung. Objekt 5 stellt die Windgeschwindigkeit parallel in drei Formaten bereit, die passende Einheit wird über einen Parameter gewählt.

Bei der GPS-Variante liefert das Gerät selbst Uhrzeit/Datum (Obj. 8/9 als Sender, mit Empfangsmöglichkeit zum externen Stellen) sowie eine Zeitanfrage-Antwortfunktion: Andere Busteilnehmer können bei der Wetterstation die aktuelle Zeit anfragen (Obj. 10 wird dann empfangen statt gesendet). Objekt 11 zeigt an, ob innerhalb der letzten 24 h ein gültiges GPS-Zeitsignal empfangen wurde – ohne gültige Zeit ist keine Sonnenstandnachführung möglich. Die Objekte 12/13 geben den aktuell berechneten Sonnenstand (Elevation = Höhe über Horizont, Azimut = Himmelsrichtung) aus und werden je nach Parametrierung nur auf Anfrage oder zyklisch gesendet.

### Universalkanäle C1–C10 (Obj. 20–59)

Jeder Universalkanal belegt vier Objekte nach folgendem Muster (dargestellt am Beispiel C1, Obj. 20–23; die Struktur wiederholt sich identisch für C2–C10 in 4er-Schritten bis Obj. 56–59):

| Nr. (C1) | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 20 | C1.1 Universalkanal | schalten / Wertgeber / Priorität | 1 Bit 1.001 / 1 Byte 5.010 / 2 Bit 2.001 | K L - Ü |
| 21 | C1.2 Universalkanal | schalten / Wertgeber / Priorität | 1 Bit 1.001 / 1 Byte 5.010 / 2 Bit 2.001 | K L - Ü |
| 22 | C1 sperren | Sperren = 1 / Sperren = 0 | 1 Bit 1.001 | K L S - |
| 23 | C1 Helligkeitsschwelle | vorgeben/abfragen bzw. nur abfragen | 2 Byte 9.004 | K L S Ü / K L - Ü |

Kanalzuordnung: C2 = Obj. 24–27, C3 = Obj. 28–31, C4 = Obj. 32–35, C5 = Obj. 36–39, C6 = Obj. 40–43, C7 = Obj. 44–47, C8 = Obj. 48–51, C9 = Obj. 52–55, C10 = Obj. 56–59.

**Erläuterung:** Jeder Universalkanal besitzt zwei unabhängig parametrierbare Ausgangsobjekte (x.1 und x.2), über die je nach Telegrammart ein Schaltbefehl, ein 2-Bit-Prioritätstelegramm oder ein 1-Byte-Wert gesendet wird, sobald die im Kanal definierte Wetterbedingung erfüllt bzw. nicht erfüllt ist. Das Sperrobjekt unterdrückt kanalweise das Senden, unabhängig vom Bedingungszustand. Das Helligkeitsschwellen-Objekt existiert nur, wenn der Kanal (auch) auf Helligkeit reagiert, und erlaubt das nachträgliche Ändern der parametrierten Schwelle per Bustelegramm.

### Sonnenschutzkanäle C11–C13 und C24–C28 (Obj. 60–83, 146–185)

Struktur je Sonnenschutzkanal (dargestellt am Beispiel C11, Obj. 60–67):

| Nr. (C11) | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 60 | C11 auf/ab | Antriebe auf/ab (0 = hoch, 1 = runter) | 1 Bit 1.008 | K - - Ü |
| 61 | C11 Rollladen/Jalousie Höhe bzw. Szene | Höhentelegramm % oder Szenennummer, je nach Betriebsart | 1 Byte 5.001 bzw. 18.001 | K L - Ü |
| 62 | C11 Lamellen | Lamellenposition 0–100 % | 1 Byte 5.001 | K L - Ü |
| 63 | C11 Sonnenautomatik | Morgen = 1 / Abend = 0 (nur bei Aktivierung „über Objekt") | 1 Bit 1.001 | K L S - |
| 64 | C11 Beschattung unterbrechen | empfangen | 1 Bit 1.001 | K L S - |
| 65 | C11 Sicherheit | Eingang | 1 Bit 1.001 | K L S - |
| 66 | C11 Dämmerungsschwelle | senden/empfangen | 2 Byte 9.004 | K L S Ü |
| 67 | C11 Helligkeitsschwelle | senden/empfangen | 2 Byte 9.004 | K L S Ü |

Kanalzuordnung: C12 = Obj. 68–75, C13 = Obj. 76–83, C24 = Obj. 146–153, C25 = Obj. 154–161, C26 = Obj. 162–169, C27 = Obj. 170–177, C28 = Obj. 178–185.

**Erläuterung:** Über „auf/ab" wird der Behang komplett gefahren, während „Höhe"/„Lamellen" bzw. das Szenenobjekt die feine Positionierung übernehmen (abhängig vom Parameter „Kanal steuert": Rollladen, Jalousie oder Szenensteuerung). Das Sonnenautomatik-Objekt aktiviert/deaktiviert die automatische Beschattung, sofern diese nicht stattdessen automatisch über die Dämmerungsschwelle gesteuert wird. „Beschattung unterbrechen" fährt den Behang temporär in eine parametrierte Pausenposition, ohne die Automatik grundsätzlich zu deaktivieren – dies wirkt nur, solange sich die Sonne im definierten Sonnenschutzbereich befindet. Das Sicherheitsobjekt hat Vorrang vor allen anderen Steuerbefehlen: Solange Sicherheit aktiv ist, sendet der Kanal keine Höhen-/Lamellentelegramme mehr; die eigentliche Schutzreaktion (z. B. Hochfahren) übernimmt üblicherweise der Antriebsaktor. Dämmerungs- und Helligkeitsschwelle können jeweils per Objekt nachträglich verändert werden.

### Schwellwertschalter C14–C17 (Obj. 84–99)

Struktur je Schwellwertkanal (dargestellt am Beispiel C14, Obj. 84–87):

| Nr. (C14) | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 84 | C14 Eingang Schwellwertschalter | je nach Objekttyp: 0..65535 / EIS5 (Gleitkomma) / Prozent / 0..255 | 2 Byte 7.001 / 2 Byte 9.x / 1 Byte 5.001 / 1 Byte 5.010 | K L S - |
| 85 | C14 sperren | Sperren = 1 / 0 | 1 Bit 1.001 | K L S - |
| 86 | C14.1 Schwellwertschalter | schalten / Wertgeber / Priorität | 1 Bit 1.001 / 1 Byte 5.010 / 2 Bit 2.001 | K L - Ü |
| 87 | C14.2 Schwellwertschalter | schalten / Wertgeber / Priorität | 1 Bit 1.001 / 1 Byte 5.010 / 2 Bit 2.001 | K L - Ü |

Kanalzuordnung: C15 = Obj. 88–91, C16 = Obj. 92–95, C17 = Obj. 96–99.

**Erläuterung:** Die Schwellwertkanäle sind funktional unabhängig von der Wettersensorik der Station und können beliebige, per Bus empfangene Werte auswerten (z. B. CO₂, externe Helligkeit, Prozentwerte anderer Geräte). Der empfangene Wert wird mit einer parametrierten Schwelle verglichen; liegt er darüber, gilt die Bedingung als erfüllt, darunter als nicht erfüllt. Das Sendeverhalten der beiden Ausgangsobjekte bei Über-/Unterschreiten wird auf der zugehörigen Objekte-Parameterseite festgelegt (siehe Abschnitt ETS-Parameter). Der Erfüllungszustand jedes Schwellwertkanals kann zusätzlich als Eingangsgröße eines Logikkanals oder als Auslöser der Sicherheitsfunktion eines Sonnenschutzkanals dienen.

### Logikmodule C18–C23 (Obj. 100–141)

Struktur je Logikkanal (dargestellt am Beispiel C18, Obj. 100–106):

| Nr. (C18) | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 100 | C18 Logikeingang 1 | Eingang für UND/ODER/XOR-Gatter | 1 Bit 1.001 | K L S - |
| 101 | C18 Logikeingang 2 | Eingang für UND/ODER/XOR-Gatter | 1 Bit 1.001 | K L S - |
| 102 | C18 Logikeingang 3 | Eingang für UND/ODER-Gatter (nicht bei XOR) | 1 Bit 1.001 | K L S - |
| 103 | C18 Logikeingang 4 | Eingang für UND/ODER-Gatter (nicht bei XOR) | 1 Bit 1.001 | K L S - |
| 104 | C18 sperren | Sperren = 1 / 0 | 1 Bit 1.001 | K L S - |
| 105 | C18.1 Logikmodul | schalten / Wertgeber / Priorität | 1 Bit 1.001 / 1 Byte 5.010 / 2 Bit 2.001 | K L - Ü |
| 106 | C18.2 Logikmodul | schalten / Wertgeber / Priorität | 1 Bit 1.001 / 1 Byte 5.010 / 2 Bit 2.001 | K L - Ü |

Kanalzuordnung: C19 = Obj. 107–113, C20 = Obj. 114–120, C21 = Obj. 121–127, C22 = Obj. 128–134, C23 = Obj. 135–141.

**Erläuterung:** Jeder Logikkanal verknüpft bis zu vier 1-Bit-Eingänge über UND, ODER oder XOR (XOR nur mit zwei Eingängen). Als Eingang kann sowohl ein echtes Busobjekt als auch der interne Zustand eines Universal-, Schwellwert- oder eines anderen Logikkanals dienen (ein Logikkanal kann sich dabei nicht selbst referenzieren). Damit lassen sich z. B. mehrere Alarmbedingungen unterschiedlicher Kanäle zu einer gemeinsamen Sicherheitsmeldung zusammenfassen.

### Erweiterungsmodul – GPS (Obj. 142–145)

| Nr. | Name | Funktion | DPT | Flags |
|---|---|---|---|---|
| 142 | GPS Breitengrad | senden | 4 Byte 14.007 | K L - Ü |
| 143 | GPS Längengrad | senden | 4 Byte 14.007 | K L - Ü |
| 144 | UTC Zeit | senden (nur senden, kein Empfang) | 3 Byte 10.001 | K - - Ü |
| 145 | UTC Datum | senden (nur senden, kein Empfang) | 3 Byte 10.001 | K - - Ü |

**Erläuterung:** Diese vier Objekte sind ausschließlich bei der GPS-Geräteausführung vorhanden. Sie stellen die vom GPS-Empfänger ermittelten Standortkoordinaten sowie die Weltzeit (UTC, Bezugszeit am Nullmeridian) zur Verfügung, aus der andere Geräte lokale Zeitzonen ableiten können (MEZ = UTC + 1 h, MESZ = UTC + 2 h).

## ETS-Parameter

### Parameterseite „Allgemein"

| Parameter | Werte | Standard |
|---|---|---|
| Universalkanal C1–C10 aktivieren | Nein / Ja | Nein |
| Sonnenschutzkanal C11–C13, C24–C28 aktivieren | Nein / Ja | Nein |
| Schwellwertkanal C14–C17 aktivieren | Nein / Ja | Nein |
| Logikkanal C18–C23 aktivieren | Nein / Ja | Nein |
| Geräteausführung | ohne GPS-Modul / mit GPS-Modul | – |
| Manuelle Positionseingabe | ja (nur bei GPS-Ausführung sichtbar) | ja |
| Breitengrad des Standorts (°) | 0..63 | 48 |
| Position (Breite) | Nord / Süd | Nord |
| Längengrad des Standorts (°) | 0..180 | 9 |
| Position (Länge) | Ost / West | Ost |

**Erläuterung:** Auf dieser Seite werden zunächst die benötigten Kanäle freigeschaltet – nur aktivierte Kanäle erscheinen als eigene Parameterseiten und Kommunikationsobjekte. Für eine funktionierende Sonnenstandnachführung muss entweder die GPS-Ausführung Zeit und Standort selbst liefern, oder bei der Nicht-GPS-Ausführung müssen Uhrzeit/Datum über den Bus empfangen sowie Breiten- und Längengrad manuell eingetragen werden. Auch bei GPS-Geräten kann der Standort weiterhin manuell fixiert werden, statt ihn laufend automatisch zu aktualisieren.

### Parameterseite „Messwerte"

| Parameter | Werte | Standard |
|---|---|---|
| Helligkeitswert senden bei Änderung | nein / ab 10 %, 20 %, 30 %, 50 % (mind. 1 lx) | ab 30 %, mind. 1 lx |
| Helligkeitswert zyklisch senden | nicht zyklisch … alle 60 min | nicht zyklisch |
| Helligkeitsabgleich Sensor vorne/links/rechts | -30 % .. 30 % | 0 |
| Temperatur senden bei Änderung | nein / ab 0,5 °C .. 2,5 °C | ab 1,0 °C |
| Temperatur zyklisch senden | nicht zyklisch … alle 60 min | nicht zyklisch |
| Temperaturabgleich | -64 .. 63 (x 0,1 °C) | 0 |
| Windgeschwindigkeit senden in | m/s / km/h / Beaufort | – |
| Windgeschw. senden bei Änderung | nein / ab 10 %, 20 %, 30 %, 50 % | ab 10 %, mind. 0,5 m/s |
| Windgeschwindigkeit zyklisch senden | nicht zyklisch … alle 60 min (zzgl. 10 s für Testzwecke) | nicht zyklisch |
| Regen senden bei Änderung | ja / nein | ja |
| Regen zyklisch senden | nein … alle 60 min | nein |
| Abfallverzögerung (Regen) | keine, 1–15 min | 10 min |
| Tauunterdrückung aktivieren | Ja / nein | Ja |
| Elevation und Azimut der Sonne senden | nur auf Anfrage / alle 5, 15, 30 min | nur auf Anfrage |

**Erläuterung:** Die Sende-Trigger (bei Änderung/zyklisch) bestimmen die Buslast: „bei Änderung" reduziert unnötigen Traffic, ein zyklisches Senden dient als Watchdog/Redundanz. Die Abgleichparameter korrigieren systematische Messabweichungen (z. B. durch Sonneneinstrahlung auf das Gehäuse gegenüber der tatsächlichen Umgebungstemperatur). Die Tauunterdrückung beheizt den Regensensor konstant auf ca. 30 °C, damit Tau nicht als Regen erkannt wird; sie funktioniert nur oberhalb +5 °C, darunter greift ohnehin ein Frostschutz-Heizbetrieb. Die Abfallverzögerung verhindert, dass der Regenstatus bei schwachem, unterbrochenem Niederschlag ständig zwischen „Regen"/„kein Regen" wechselt.

### Parameterseite „Datum und Uhrzeit"

| Parameter | Werte | Standard |
|---|---|---|
| Zeit und Datum senden (nur GPS-Ausführung) | nicht senden / jede Stunde … alle 12 Stunden | jede Stunde |
| Zeitanfrage zyklisch senden (nur ohne GPS) | nur auf Anfrage … alle 12 Stunden | alle 2 Stunden |
| Zeitzone des Standortes | -12 h … +13 h (in Teilstufen) | 1 h (MEZ) |
| Sommer-/Winterzeit-Umschaltung | keine / wie Mitteleuropa / wie Großbritannien / Griechenland, Finnland, Türkei / wie Nordamerika / benutzerdefiniert | wie Mitteleuropa |
| Sommerzeitanfang / Winterzeitanfang (bei benutzerdefiniert) | 1.–4./letzter Sonntag im gewählten Monat, Uhrzeit 0–6 Uhr | letzter Sonntag im März 2:00 Uhr / letzter Sonntag im Oktober |

**Erläuterung:** Bei der GPS-Ausführung liefert das Gerät die Weltzeit selbst und rechnet sie über Zeitzone und Sommerzeitregel in Lokalzeit um; ohne GPS-Modul fragt die Station die Zeit periodisch über den Bus bei einem Zeitgeber an. Die vordefinierten Umschaltregeln decken die gängigen Regionen ab, alternativ lässt sich eine eigene Regel (Wochentag/Monat/Uhrzeit) definieren.

### Parameterseiten „Universalkanal C1..C10: Funktion" (je Kanal eigene Seite)

| Parameter | Werte | Standard |
|---|---|---|
| Funktion des Kanals | Helligkeitssensor 1..100.000 lx / Temperatursensor / Windsensor / Regensensor / Verknüpfung folgender Sensoren | – |
| Helligkeit (bei Funktion Helligkeitssensor) | unter 3 lx .. unter 90.000 lx / über 3 lx .. über 90.000 lx | über 10.000 lx |
| Quelle (Helligkeit) | Sensor vorne / links / rechts / maximaler Wert der 3 Sensoren | Sensor vorne |
| Hysterese Licht | 20 %, 30 %, 50 % (mind. 1 lx) | 20 % |
| Verzög. bei zu-/abnehmender Helligkeit | keine, 5 s .. 20 min | 3 min (zunehmend) / 10 min (abnehmend) |
| Temperatur (bei Funktion Temperatursensor) | unter -30 °C .. unter 40 °C / über -30 °C .. über 40 °C | über 18 °C |
| Hysterese Temperatur | 1,0 / 1,5 / 2,0 / 2,5 K | 1,0 K |
| Windgeschwindigkeit (bei Funktion Windsensor) | unter/über 4 m/s .. 30 m/s | über 4 m/s |
| Abfallverzögerung Wind | keine, 5 s .. 20 min | 3 min |
| Regenbedingung (bei Funktion Regensensor) | Es regnet / es regnet nicht | Es regnet |
| Bei „Verknüpfung folgender Sensoren": Helligkeit/Temperatur/Wind/Regen einzeln | Ja / Nein je Größe | Nein |
| Art der Verknüpfung | UND / ODER | UND |
| Wert über Objekt überschreibbar | Ja / nein | Ja |
| Wert bei Download überschreiben | Ja / nein | Ja |

**Erläuterung:** Jeder Universalkanal kann entweder auf genau eine Wettergröße reagieren oder mehrere Größen UND-/ODER-verknüpfen. Eine UND-Verknüpfung eignet sich für „scharfe" Bedingungen (z. B. Temperatur UND Helligkeit), eine ODER-Verknüpfung typischerweise für Sicherheitsfunktionen (z. B. Wind ODER Regen löst gemeinsam einen Schutzzustand aus). Die Hysterese verhindert häufiges Umschalten bei Werten nahe der Schwelle; die Verzögerungszeiten dämpfen kurzzeitige Spitzen (z. B. Windböen), bevor der Kanalzustand tatsächlich wechselt. „Wert bei Download überschreiben" bestimmt, ob ein ETS-Download eine zwischenzeitlich per Objekt geänderte Schwelle wieder auf den Planungswert zurücksetzt (Ausnahme: bei leerem Gerätespeicher, also Erstinbetriebnahme, werden immer alle ETS-Werte geladen).

### Parameterseiten „Objekte" (gemeinsam für Universal-, Schwellwert- und Logikkanäle)

| Parameter | Werte | Standard |
|---|---|---|
| Telegrammart CX.1 / CX.2 | Schaltbefehl / Priorität / Wert | Schaltbefehl |
| Wenn Bedingung erfüllt/nicht erfüllt | kein Telegramm / einmalig senden / zyklisch senden | einmalig senden |
| Telegramm bei erfüllter/unerfüllter Bedingung | EIN/AUS bzw. Priorität EIN/AUS bzw. 0–255 | je nach Objekt |
| Soll ein zweites Telegramm gesendet werden? | Ja / nein | nein |
| Sperrfunktion aktivieren | Ja / nein | nein |
| Verhalten bei Setzen/Aufheben der Sperre | nicht senden / wie erfüllt/nicht erfüllt / Kanal aktualisieren | nicht senden (Setzen) / Kanal aktualisieren (Aufheben) |
| Zykluszeit (falls zyklisch verwendet) | nicht zyklisch … alle 60 min | alle 60 min |
| Telegramm bei erkanntem Sensorfehler (nur Temperatur/Regen) | nicht mehr senden / wie unerfüllt / wie erfüllt | nicht mehr senden |
| Telegramm nach Reset/Download | nicht mehr senden / wie unerfüllt / wie erfüllt | nicht mehr senden |

**Erläuterung:** Diese Seite legt für jeden Kanal fest, welches Telegramm (Schalten, 2-Bit-Priorität oder 1-Byte-Wert) beim Erfüllen bzw. Nicht-Erfüllen der Kanalbedingung gesendet wird, optional zusätzlich über ein zweites, unabhängig parametrierbares Ausgangsobjekt. Priorität-Telegramme eignen sich, um Aktoren zwangsweise in einen Zustand zu versetzen (z. B. „Priorität AUS" zum Sperren einer manuellen Bedienung während eines Windalarms). Die Sperrfunktion blendet ein zusätzliches Sperrobjekt ein; ihr Verhalten kann wahlweise wie eine erfüllte oder unerfüllte Bedingung wirken oder komplett stumm bleiben.

### Parameterseiten „Sonnenschutzkanal C11..C13 und C24..C28"

| Parameter | Werte | Standard |
|---|---|---|
| Kanal steuert | Rollladen / über Szenen / Jalousie | – |
| Sonnenstandnachführung | Ja / Nein | – |
| Quelle für Helligkeitsmessung | Sensor vorne/links/rechts / max. Wert der 3 Sensoren / externer Luxwert 1/2 | Sensor vorne |
| Dämmerungsschwelle | 2–500 lx | 10 lx |
| Helligkeitsschwelle für Beschattung | 2.000–90.000 lx | 20.000 lx |
| Verzögerung bei zu-/abnehmender Helligkeit | keine, 5 s .. 20 min | 30 s (zunehmend) / 5 min (abnehmend) |
| Antriebshöhe bei Überschreiten der Helligkeitsschwelle | 0–100 % | 10 % |
| Szenennummer bei Überschreiten der Helligkeitsschwelle | 1–64 | Szene 1 |
| Lamelle bei Überschreiten der Helligkeitsschwelle | 0–100 % | 50 % |
| Schwellen über Objekt überschreibbar / bei Download überschreiben | Ja / nein | Ja |

**Erläuterung:** Ohne Sonnenstandnachführung fährt der Kanal bei Überschreiten der Helligkeitsschwelle einmalig auf eine feste Höhe/Lamellenposition (bzw. ruft eine feste Szene ab) und bei Unterschreiten der Dämmerungsschwelle wieder hoch. Mit aktivierter Sonnenstandnachführung übernimmt stattdessen die Parameterseite „Sonnenstandnachführung" die laufende, elevationsabhängige Positionierung. Die Quelle für die Helligkeitsmessung kann pro Kanal individuell gewählt werden, z. B. um bei Ecklagen den jeweils passenden Sensor (oder einen externen Sensor an einer anderen Fassade) zu verwenden.

### Parameterseite „Sonnenstandnachführung" (nur bei aktivierter Nachführung)

| Parameter | Werte | Standard |
|---|---|---|
| Fassadenrichtung | 0–360° (32 Schritte) | – |
| Sonnenschutzbereich „vor der Fassade" | -90° .. 90° | – |
| Sonnenschutzbereich „nach der Fassade" | -90° .. 90° | – |
| Min. Elevation | 0–90° | 10° |
| Max. Elevation | 0–90° | 80° |
| Verhalten bei Verlassen des Sonnenschutzbereichs | Keine Reaktion / Hochfahren / Lamelle anpassen | Keine Reaktion |
| Lamellenposition bei Verlassen des Bereichs | 0–100 % | 20 % |
| Szenennummer bei Verlassen des Bereichs | 1–64 | Szene 1 |
| Erneut positionieren alle | 10° / 15° / 22,5° / 30° | 22,5° |
| Neue Szene abrufen alle | 10° / 15° / 22,5° / 30° | 22,5° |
| Berechnung der Lamellenposition | Automatisch über Lamellenmaße / Eigene Werte zuweisen | Automatisch über Lamellenmaße |
| Abstand der Lamellen in mm | 0–255 | 20 |
| Breite der Lamellen in mm | 0–255 | 50 |
| Reserve für sicheres Beschatten | 0–25 % | 0 |
| Werte für Beschattung / Beschattungspause je Elevationsstufe | 0–100 % Höhe bzw. Lamelle, je Stufe | siehe Tabellenwerte im Handbuch |

**Erläuterung:** Die Fassadenrichtung gibt die Blickrichtung eines Beobachters an, der geradeaus aus dem Fenster schaut (z. B. per Kompass ermittelt). Der Sonnenlauf vor der Fassade deckt maximal 180° ab und wird in eine linke Zone „vor der Fassade" (dort erscheint die Sonne für den Beobachter zuerst) und eine rechte Zone „nach der Fassade" unterteilt; nördlich des nördlichen Wendekreises ist „vor der Fassade" stets die linke, „nach der Fassade" stets die rechte Fensterseite (südlich davon kehrt sich die Zuordnung um: „vor der Fassade" wird positiv/rechts, „nach der Fassade" negativ/links). Über negative bzw. positive Winkelwerte lässt sich der Sonnenschutzbereich unsymmetrisch, einseitig oder auf den vollen 180°-Bereich (-90°/90°) einstellen; der Wert 0° blendet eine Zone komplett aus. Zusätzlich wird die Beschattung auf einen Elevationsbereich (Sonnenhöhe über Horizont) begrenzt, z. B. um bei sehr tiefstehender oder senkrecht einfallender Sonne nicht zu beschatten. Die Lamellenposition wird entweder automatisch aus Lamellenbreite/-abstand berechnet – so, dass kein direktes Licht eindringt, der Raum aber möglichst hell bleibt – oder pro Elevationsstufe manuell vorgegeben; getrennte Wertetabellen existieren für den normalen Beschattungsbetrieb und für die temporäre „Beschattungspause".

### Parameterseite „Sonnenautomatik"

| Parameter | Werte | Standard |
|---|---|---|
| Aktivierung der Sonnenautomatik | Über Objekt / Über Dämmerungsschwelle | Über Objekt |
| Reaktion auf Morgendämmerung | Hochfahren & Sonnenautom. EIN / Sonnenautom. EIN aber nicht fahren | Hochfahren & Sonnenautom. EIN |
| Reaktion auf Abenddämmerung | Sonnenautomatik AUS & hochfahren / & abfahren / aber nicht fahren | Sonnenautomatik AUS & hochfahren |
| Reaktion auf Sonnenautomatik EIN (nur bei Aktivierung über Objekt) | Hochfahren & Sonnenautom. EIN / Erst bei Dämmerung Hochfahren / Sonnenautom. EIN aber nicht fahren | Hochfahren & Sonnenautom. EIN |
| Reaktion auf Sonnenautomatik AUS | Sonnenautom. AUS & hochfahren / & abfahren / & bei Dämmerung abfahren / aber nicht fahren | Sonnenautom. AUS & hochfahren |
| Bei Unterschreiten der Helligkeitsschwelle während Sonnenautomatik aktiv | Keine Reaktion / Hochfahren / Lamelle anpassen | Keine Reaktion |
| Lamellenposition (bei Unterschreiten) | 0–100 % | 20 % |
| Fahren in Endposition nach Dämmerung | 1-Bit-Objekt (Auf/Ab) / % Höhe | – |

**Erläuterung:** Diese Seite regelt, wann die automatische Beschattung generell aktiv ist – entweder fest an die Dämmerungsschwelle gekoppelt oder über ein separates Freigabeobjekt (z. B. durch eine Schaltuhr oder manuellen Schalter), das morgens ein- und abends ausgeschaltet wird. „Keine Reaktion" bei kurzzeitigem Unterschreiten der Helligkeitsschwelle (z. B. durch vorbeiziehende Wolken) verhindert unruhiges, ständiges Auf-/Abfahren des Behangs.

### Parameterseite „Sicherheit"

| Parameter | Werte | Standard |
|---|---|---|
| Sicherheitszustand wird ausgelöst durch | Eingangsobjekt / Bedingung C1–C10 / Status Schwellwertkanal C14–C17 / Verknüpfungsergebnis Logikkanal C18–C23 | Eingangsobjekt |
| Reaktion auf Sicherheit Beginn | Keine Reaktion / Antrieb hochfahren / Antrieb herunterfahren | Keine Reaktion |
| Reaktion auf Sicherheit Ende | Keine Reaktion / Position aktualisieren / Szene aktualisieren | Position aktualisieren |
| Fahren in Endposition bei Sicherheit | 1-Bit-Objekt (Auf/Ab) / % Höhe | – |

**Erläuterung:** Der Sicherheitszustand eines Sonnenschutzkanals kann direkt über ein Objekt oder – häufig praktikabler – aus dem Ergebnis eines Universal-, Schwellwert- oder Logikkanals abgeleitet werden (z. B. Wind ODER Frost ODER Regen als ODER-verknüpfter Universalkanal). „Keine Reaktion" wird empfohlen, wenn die eigentliche Schutzreaktion im nachgeschalteten Antriebsaktor hinterlegt ist, da während aktiver Sicherheit ohnehin keine Höhen-/Lamellentelegramme mehr gesendet werden.

### Parameterseiten „Schwellwertkanal C14..C17: Funktion"

| Parameter | Werte | Standard |
|---|---|---|
| Art des Schwellwertobjekts | Prozent (DPT 5.001) / Zählwert 0..255 (DPT 5.010) / Zählwert 0..65535 (DPT 7.001) / EIS5 z. B. CO₂, Helligkeit (DPT 9.x) | Prozent |
| Schwellwert (Prozent) | 1–99 | 50 |
| Hysterese (Prozent) | 1–99 | 5 |
| Schwellwert (Zählwert 0..255) | 1–254 | 127 |
| Schwellwert (Zählwert 0..65535) | 1–65534 | 1000 |
| Schwellwert (EIS5) | -9999..99999 | 20,0 |
| Hysterese (EIS5) | 0,00..9999 | 1,0 |
| Verzögerung bei Überschreiten/Unterschreiten | keine, 5 s .. 20 min | keine |

**Erläuterung:** Der Schwellwertkanalblock ist unabhängig von den Wettersensoren der Station und vergleicht einen frei über den Bus empfangenen Wert (z. B. von einem CO₂-Sensor oder einem anderen Helligkeitssensor) mit der eingestellten Schwelle. Über der Schwelle gilt die Bedingung als erfüllt, darunter als nicht erfüllt; die Hysterese wirkt dabei einseitig negativ (z. B. Ein bei 50, Aus erst bei 50 minus Hysterese), um Flattern zu vermeiden.

### Parameterseiten „Logikkanal C18..C23: Funktion"

| Parameter | Werte | Standard |
|---|---|---|
| Art der Verknüpfung | UND (2–4 Eingänge) / ODER (2–4 Eingänge) / XOR (2 Eingänge) | UND |
| Eingang 1–4 verwenden | Nein / Ja / Ja, invertiert (Eingänge 3+4: zusätzlich „Nein" möglich) | Eingang 1+2: Ja, Eingang 3+4: Nein |
| Eingangsgröße für Eingang 1–4 | Eingangsobjekt / Bedingung C1–C10 / Status Schwellwertkanal C14–C17 / Verknüpfungsergebnis eines anderen Logikkanals | Eingangsobjekt |

**Erläuterung:** Die Logikkanäle sind ebenfalls unabhängig von den Wetterdaten und lassen sich für beliebige KNX-Verknüpfungsaufgaben nutzen. Jeder Eingang kann invertiert werden; ein Logikkanal kann nicht mit seinem eigenen Ergebnis verknüpft werden, wohl aber mit dem Ergebnis eines anderen Logikkanals, wodurch sich mehrstufige Verknüpfungen bilden lassen.

## Inbetriebnahme / Hinweise

- **GPS vs. ohne GPS:** Für eine funktionierende Sonnenstandnachführung benötigt die Nicht-GPS-Ausführung zwingend Uhrzeit/Datum über den Bus sowie manuell eingetragene Standortkoordinaten. Bei der GPS-Ausführung (dieses Modell, Art.-Nr. 1409208) liefert das Gerät Zeit und Standort eigenständig; eine manuelle Standorteingabe ist trotzdem möglich und ist Werkseinstellung.
- **Regensensor:** Regen wird erst erkannt, wenn der Sensor ausreichend benetzt ist; je nach Regenart kann es daher zu einer spürbaren Erkennungsverzögerung kommen. Eine zu kurze Abfallverzögerung (unter 5 min) kann bei leichtem Regen zu häufigem Wechsel zwischen „Regen"/„kein Regen" führen, daher wird mindestens 10 min empfohlen. Bei sehr empfindlicher Einstellung und deaktivierter Tauunterdrückung kann hohe Luftfeuchte bei hoher Temperatur fälschlich als Regen erkannt werden.
- **Windmessung:** Da Beschattungssysteme mehrere Minuten Fahrzeit benötigen, sollte die Windschwelle sicherheitshalber deutlich unter der vom Behang-Hersteller angegebenen Grenzgeschwindigkeit liegen. Bei frontal stark windexponierten Fassaden kann sich vor der Fassade ein Luftpolster bilden, in dem die gemessene Windgeschwindigkeit niedriger ausfällt als die tatsächliche Windstärke – hier kann eine Mastmontage statt Wandmontage Abhilfe schaffen.
- **Temperaturmessung:** Da die Station typischerweise an sonnenbeschienenen Stellen montiert wird, kann die gemessene Temperatur durch Sonneneinstrahlung deutlich über der „echten" Schattentemperatur liegen; dies ist bei der Interpretation von Temperaturschwellen zu berücksichtigen.
- **Fassadenausrichtung/Sonnenschutzbereich:** Die Parameter „vor der Fassade" und „nach der Fassade" sind bezogen auf einen Beobachter im Gebäude zu verstehen, der aus dem Fenster schaut. Nördlich des nördlichen Wendekreises (u. a. Europa, Nordamerika, Russland) ist „vor der Fassade" die linke, „nach der Fassade" die rechte Fensterseite; südlich davon (z. B. Südafrika, Australien) kehrt sich diese Zuordnung um.
- **Applikationswechsel:** Meteodata 140 und Meteodata 140 S benötigen laut Hersteller unterschiedliche ETS-Applikationsprogramme; bei Austausch oder Neuinstallation ist zwingend die zur jeweiligen Geräteversion passende Applikation von der Theben-Downloadseite zu verwenden.
- **Typische Anwendungsfälle laut Handbuch** (als Planungsbeispiele, nicht abschließend): einfache helligkeitsgesteuerte Beschattung ohne Sonnenstandnachführung; Beschattung mit Sonnenstandnachführung; Dachrinnenbeheizung, bei der ein Universalkanal als reiner Temperatursensor (Schwelle „unter 3 °C") ein Heizband über einen Schaltaktor ansteuert. In allen Beispielen wird ein ODER-verknüpfter Universalkanal (Temperatur/Wind/Regen) als Sicherheitsquelle für die Sonnenschutzkanäle verwendet, dessen Schaltobjekt auf ein zyklisch überwachtes Sicherheitsobjekt im Antriebsaktor geführt wird.

## Quelle

Theben AG – Meteodata 140 S Wetterstation, Technisches Handbuch, Stand: Apr-18.
Datei: `originals/KNX/Theben_Meteodata_140_S_Handbuch.pdf`
