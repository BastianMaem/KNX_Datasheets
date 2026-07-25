---
title: MDT Taster – Übersicht aller Produktfamilien
device_type: Taster
manufacturer: MDT
article_number: [BE-TAS63T4.01, BE-GTSP6TX.01S, BE-TAL6301.01, BE-TAL6302.01]
bus: KNX TP
source_pdf:
  - originals/KNX/MDT_THB_BE_01_Taster_Smart_55_63.pdf
  - originals/KNX/MDT_BE-GTSx6Tx-01S_MDT_TM_V13_DE.pdf
  - originals/KNX/MDTBE-TAL55_63xx.x1_MDT_TM_V14_DE.pdf
last_updated: 2026-07-25
synonyms: [Wandtaster, Glastaster, Bedienelement, KNX-Taster, Lichtschalter]
tags: [knx, taster, mdt]
---

## Übersicht

Ein KNX-Taster ist ein Bedienelement für die Gebäudeautomation, das per Tastendruck (bzw. bei
Glastastern per Touch-Bedienung) Telegramme auf dem KNX-Bus auslöst und damit andere Geräte
wie Schalt-, Dimm-, Jalousie- oder Heizungsaktoren ansteuert. Zusätzlich können Taster Status-
Rückmeldungen anderer Geräte empfangen und über LEDs oder ein Display visualisieren. Viele
MDT-Taster verfügen außerdem über einen Temperatursensor zur Raumtemperaturerfassung und
über interne Logikfunktionen, mit denen einfache Verknüpfungen direkt im Gerät realisiert werden
können, ohne einen zusätzlichen Logikbaustein zu benötigen.

Diese Datei bündelt drei unterschiedliche MDT-Taster-Produktfamilien in einer gemeinsamen
Wissensbasis:

- **Smart 55/63** – klassischer Taster mit Farbdisplay, Status-LEDs und optionalem Temperatur-/
  Feuchtesensor (Beispielgerät: BE-TAS63T4.01, 4-fach).
- **Glastaster GTS (Glas Touch Smart / Smart Plus)** – Vollflächiges Touch-Farbdisplay mit bis zu
  64 frei konfigurierbaren Funktionskacheln, zwei Raumtemperaturreglern, Zeitschaltuhr,
  Logikfunktionen, KNX Secure u.v.m. (Beispielgerät: BE-GTSP6TX.01S, 6 Zoll, "Plus"-Variante).
- **TAL-Serie (Taster Light 55/63)** – schlanker, tastenbasierter Taster ohne Display mit RGBW-
  Status-LEDs (Beispielgeräte: BE-TAL6301.01 1-fach, BE-TAL6302.01 2-fach, jeweils NEUTRAL-
  Ausführung ohne Temperatursensor).

Die Abschnitte zu **Smart 55/63** und **Glastaster GTS** basieren auf den vollständigen technischen
Handbüchern (direkt eingelesen, nicht nur auszugsweise) und sind entsprechend detailliert
ausgearbeitet. Der Abschnitt zur **TAL-Serie** ist bewusst kompakter gehalten, da dieser Taster
funktional deutlich einfacher aufgebaut ist (kein Display, kein Regler, keine Zeitschaltuhr).

Jede Familie hat eine eigene Applikation, eigene Kommunikationsobjekte und eigene ETS-Parameter
und wird deshalb im Folgenden in einem eigenen Abschnitt beschrieben. Die drei Familien sind
technisch nicht miteinander kompatibel und dürfen nicht vermischt werden.

---

## Familie: Smart 55/63 (BE-TAS63T4.01)

### Übersicht

Das Handbuch (Stand 08/2020, Version 1.0) deckt vier Geräte ab: BE-TAS5504.01 und BE-TAS6304.01
(jeweils 4-fach mit Farbdisplay, ohne Sensor) sowie BE-TAS55T4.01 und BE-TAS63T4.01 (baugleich,
zusätzlich mit integriertem Temperatur-/Feuchtesensor). Alle vier Geräte besitzen 4 Tasterflächen
und 4 RGBW-Status-LEDs; der Unterschied zwischen "55" und "63" liegt im Rahmendesign (Reinweiß
glänzend bzw. Studioweiß glänzend). BE-TAS63T4.01 ist damit die 63er-Ausführung mit Temperatur-/
Feuchtesensor. Der Aufbau besteht aus 4 Sensorflächen zur Bedienung, einer RGBW-Statusanzeige,
einer Programmiertaste und einer Busanschlussklemme.

Gegenüber einem einfachen Taster bietet die Applikation deutlich mehr Funktionsumfang: Neben
klassischem Schalten, Dimmen, Jalousiesteuerung und Szenenaufruf lassen sich auch Werte wie
HSV-Farbwerte oder Farbtemperaturen senden. Jede Taste kann über kurzen, langen und – als
Besonderheit – einen "extra langen" Tastendruck bis zu vier unterschiedliche Funktionen auslösen
(Mehrfach-Tippfunktion). Die sogenannte "innovative Gruppensteuerung" erlaubt es, mit
unterschiedlich langen Tastendrücken hierarchisch gestaffelte Gruppen anzusteuern (z. B. kurz =
Raum, lang = Etage, extra lang = Gebäude); die Status-LED zeigt dabei den Fortschritt des
Tastendrucks durch ihr Verhalten (leuchtet/blinkt/erlischt) an. Vier interne Logikblöcke erlauben
verschachtelte Verknüpfungen, z. B. die Freigabe eines Szenenaufrufs nur im Tagbetrieb. Bei den
T4-Varianten kommt ein integrierter Temperatur- und Feuchtesensor hinzu, dessen Messwert direkt
an einen Regler (z. B. MDT AKH-0x00.02) gesendet werden kann, wodurch ein separater Raumfühler
entfällt. Zusätzlich unterstützt das Gerät "Long Frames" für kürzere Programmierzeiten ab der ETS5,
sofern das verwendete Schnittstellen-Interface dies unterstützt (z. B. MDT SCN-USBR.02 oder
SCN-IP000.02/03 bzw. SCN-IP100.02/03). Ab Gerätefirmware R1.0 ist ein Update über die MDT
DCA-App möglich; im Bootloader-Modus verhalten sich die Programmier-LEDs anders als im
Normalbetrieb (MDT-Symbol leuchtet rot statt des abwechselnden Blinkens).

### Technische Daten

| Merkmal | Wert |
|---|---|
| Busanschluss | KNX TP (Busanschlussklemme) |
| Bauform | UP-Taster mit 4 Sensorflächen (Tastenfunktionen) und Farbdisplay |
| Status-LEDs | 4 × RGBW (eine pro Taste), Farben Rot/Grün/Gelb/Blau/Pink/Cyan/Weiß |
| Temperatursensor | integriert, nur bei BE-TAS**T**4.01-Varianten (inkl. BE-TAS63T4.01) |
| Feuchtesensor | integriert, nur bei BE-TAS**T**4.01-Varianten |
| Long-Frame-Unterstützung | ja (verkürzt Programmierzeit ab ETS5, benötigt kompatibles Interface) |
| Update-Funktion | über MDT Update-Tool (DCA), ab Gerätefirmware R1.0 |
| Elektrische Kenndaten (Busspannung, Stromaufnahme) | nicht im Handbuch spezifiziert (nur im separaten Datenblatt) |
| Schutzart, Abmessungen, Gewicht | nicht im Handbuch spezifiziert |

### Kommunikationsobjekte

Die Objektnummerierung folgt einem klaren Baukastenprinzip: Für jede Taste (Basisnummer, +10 für
die nächste Taste) blendet die ETS je nach gewähltem Funktionstyp (Schalten, Werte senden,
Jalousie, Dimmen, Szene, HSV, Tunable White, Temperaturverschiebung, Betriebsartenumschaltung
…) automatisch die passenden Objekte ein. Daneben existieren feste Blöcke für allgemeine Objekte,
Alarme/Status, Status-LEDs, Logik und Temperatur/Feuchte.

**Block: Tasten (Basisnummer 0, +10 je weitere Taste)**

| Nr. | Name | Objektfunktion | Größe |
|---|---|---|---|
| 0 | Taste 1 / Tasten 1/2 | Schalten, Umschalten, Zustand senden | 1 Bit |
| 0 | Taste 1 / Tasten 1/2 | Zwangsführung | 2 Bit |
| 0 | Taste 1 / Tasten 1/2 | Prozentwert, Dezimalwert, Szene | 1 Byte |
| 0 | Taste 1 / Tasten 1/2 | Farbtemperatur, Temperatur, Helligkeitswert | 2 Byte |
| 0 | Taste 1 / Tasten 1/2 | RGB-Wert, HSV-Wert | 3 Byte |
| 0 | Taste 1 / Tasten 1/2 | Jalousie Auf/Ab, Dimmen Ein/Aus | 1 Bit |
| 1 | Taste 1 | Dimmen relativ | 4 Bit |
| 1 | Taste 1 | Status für Umschaltung/Anzeige | 1 Bit |
| 1 | Tasten 1/2 | Stopp/Lamellen Auf/Zu | 1 Bit |
| 2 | Taste 1 Gruppe lang / Taste 1 lang | (gleiche Datentypen wie Objekt 0, für langen Tastendruck) | 1 Bit…3 Byte |
| 2 | Taste 1 | Szene, Status für Richtungswechsel/Umschaltung | 1 Byte / 1 Bit |
| 3 | Taste 1 / Tasten 1/2 | Status für Anzeige, Status Prozentwert/Dezimalwert | 1 Bit / 1 Byte |
| 4 | Taste 1 Gruppe extra lang | (gleiche Datentypen wie Objekt 0, für extra langen Tastendruck) | 1 Bit…3 Byte |
| 5 | Taste 1 / Tasten 1/2 | Status für Anzeige, Status Jalousie/Rollladen | 1 Byte |
| 9 | Taste 1 / Tasten 1/2 | Sperrobjekt | 1 Bit |

Jede Taste stellt je nach gewähltem Funktionstyp ("Schalten", "Werte senden", "Jalousie/Rollladen",
"Dimmen", "Szene", "HSV-Farbsteuerung", "Farbtemperatur" usw.) passende Objekte unter derselben
Basisnummer bereit. Das Sperrobjekt (Nr. 9) blockiert bei "1" jede weitere Bedienung der Taste bzw.
des Tastenpaares; mit "0" wird die Sperre aufgehoben.

**Block: Allgemeine Objekte**

| Nr. | Name | Funktion | Größe |
|---|---|---|---|
| 71 | In Betrieb | Ausgang (zyklisches Lebenszeichen) | 1 Bit |
| 72 | Tag/Nacht | Eingang, Polarität parametrierbar | 1 Bit |
| 73 | Präsenz | Eingang (schaltet Display/LEDs ein) | 1 Bit |
| 74 | Tastenbetätigung | Ausgang bei jeder Tastenbetätigung (z. B. für Orientierungslicht) | 1 Bit |
| 75 | Helligkeit | Eingang für dynamische Display-/LED-Helligkeit | 1 Byte / 2 Byte |
| 77 | Uhrzeit | Aktuellen Wert empfangen | 3 Byte |
| 78 | Datum | Aktuellen Wert empfangen | 3 Byte |
| 79 | Uhrzeit/Datum | Aktuelle Werte empfangen (Kombiobjekt) | 8 Byte |

Das "In Betrieb"-Objekt zeigt durch ein zyklisches EIN-Telegramm, dass das Gerät busseitig aktiv ist.
Das Objekt "Tastenbetätigung" sendet bei jeder Bedienung eine "1" (z. B. für ein Orientierungslicht)
und startet danach ein 30-Sekunden-Timeout, in dem kein weiteres Telegramm gesendet wird.

**Block: Status/Meldungen (Alarme, Statuswerte, Statustexte)**

| Nr. | Name | Funktion | Größe |
|---|---|---|---|
| 61–64 | Meldung 1–4 | Eingang, je Meldung eigene Priorität (1 = höchste) | 1 Bit |
| 65 | Meldung Text | Eingang, niedrigste Priorität, beliebiger Text | 14 Byte |
| 66/67 | Statustext 1/2 | Eingang eines frei anzeigbaren Textes | 14 Byte |
| 68+ | Statuswert 1 (+1 je weiterem) | Ein/Aus, Prozent, Dezimal, mA, Lux, °C, m/s, %, ppm | 1 Bit / 1–2 Byte |

Über bis zu vier priorisierte Bit-Meldungen und eine niedrig priorisierte Textmeldung lassen sich
Warnungen/Alarme anderer Geräte auf dem Display anzeigen; das Anzeigeverhalten (z. B. ob eine
Meldung im Standby sofort erscheint, geblinkt wird oder erst beim nächsten Tastendruck angezeigt
wird) hängt von der gewählten Standby-Darstellung ab. Statuswerte und Statustexte liefern
zusätzliche, frei belegbare Anzeigefelder z. B. für Sensormesswerte aus anderen Geräten.

**Block: Status-LED**

| Nr. | Name | Funktion | Größe |
|---|---|---|---|
| 52 (+1 je weiterer) | LED 1 | Schalten / Prozentwert / Dezimalwert (Ansteuerung) | 1 Bit / 1 Byte |
| 56 (+1 je weiterer) | LED 1 Priorität | Schalten (übersteuert die normale LED-Logik) | 1 Bit |
| 60 | LED | Sperrobjekt (schaltet alle LEDs aus) | 1 Bit |
| 76 | Synchron-LED | Blinkstatus als Master senden / als Slave empfangen | 1 Bit |

Jede Status-LED kann auf ein externes Objekt (z. B. Aktorstatus), ein internes Objekt oder auf
Tastenbetätigung reagieren, wahlweise auch auf eine Kombination aus Objekt und Tastendruck. Über
das Prioritätsobjekt lässt sich eine LED unabhängig von ihrer normalen Logik in einen definierten
Zustand zwingen (z. B. für eine Störmeldung). Das Synchronisierungsobjekt gleichtaktet das Blinken
mehrerer Taster (ein Gerät als Master, andere als Slave).

**Block: Logikfunktion**

| Nr. | Name | Funktion | Größe |
|---|---|---|---|
| 40 (+3 je weiterer Block) | Logik 1 Eingang 1A/1B | Eingänge der Verknüpfung | 1 Bit |
| 42 (+3 je weiterer Block) | Logik 1 Ausgang 1 | Schalten / Szene / Wert / Zwangsführung | 1 Bit, 1 Byte, 2 Bit |

Vier Logikblöcke (UND, ODER oder "Wert senden bei Tastenbetätigung") verknüpfen je bis zu zwei
externe Objekte und bis zu zwei Tasten (normal oder invertiert eingebunden) zu einem Ausgangswert
mit wählbarem Datenpunkttyp; die Sendebedingung (z. B. nur bei Änderung, nur 0 oder nur 1 senden)
und eine Ausgangsinvertierung sind beim Objekttyp "Schalten" zusätzlich einstellbar.

**Block: Temperatur- und Luftfeuchtemessung (nur BE-TASxxT4.01)**

| Nr. | Name | Funktion | Größe |
|---|---|---|---|
| 80 | Temperatur | Messwert senden | 2 Byte |
| 81 | Temperatur | Externer Temperatursensor (Eingang) | 2 Byte |
| 82/83 | Temperatur | Max./Min. Wert über-/unterschritten | 1 Bit |
| 84 | Relative Luftfeuchtigkeit | Messwert senden | 2 Byte |
| 85 | Relative Luftfeuchtigkeit | Externer Feuchtesensor (Eingang) | 2 Byte |
| 86/87 | Relative Luftfeuchtigkeit | Max./Min. Wert über-/unterschritten | 1 Bit |
| 88 | Taupunkttemperatur | Messwert senden | 2 Byte |
| 89 | Taupunkttemperatur | Vergleichswert (Eingang) | 2 Byte |
| 90 | Taupunkttemperatur | Alarm senden | 1 Bit |

Dieser Block ist nur bei den T4-Varianten vorhanden. Neben dem reinen Messwert liefert er
Grenzwert-Meldeobjekte für Temperatur und Feuchte sowie eine berechnete Taupunktüberwachung,
mit der sich z. B. eine Fußbodenkühlung vor Kondensatbildung schützen lässt. Interner und ein
optionaler externer Sensor können gewichtet gemischt werden (0–100 % in 10-%-Schritten); bei
Ausfall des externen Sensors (Überwachungszeit 30 min) fällt das Gerät automatisch auf den
internen Sensor zurück. Nach Erstinstallation/Programmierung sind die Messwerte laut Handbuch
erst nach ca. 30 Minuten stabil.

### ETS-Parameter

**Block: Allgemeine Einstellungen**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Geräteanlaufzeit | 2–240 s [2 s] | Wartezeit zwischen Neustart und Betriebsbereitschaft |
| „In Betrieb“ zyklisch senden | nicht aktiv, 1 min–4 h | Aktiviert das zyklische Lebenszeichen-Telegramm |
| Wert für Tag/Nacht | Tag=1/Nacht=0 oder umgekehrt | Polarität der Tag/Nacht-Umschaltung; nach Neuprogrammierung startet das Gerät immer im Tagbetrieb |
| Verhalten nach Busspannungswiederkehr (Wert für Umschaltung / Tag-Nacht-Objekt / Uhrzeit-Datum-Objekte) | nicht abfragen / abfragen | Steuert, ob die Objekte nach einem Reset aktiv abgefragt werden |
| Sprache | Deutsch / Englisch | Wirkt sich u. a. auf HVAC-Status-, Zwangsführungs- und Wochentagsanzeige aus |

**Block: Displayeinstellung**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Hintergrundfarbe | 4 Kombinationen Schwarz/Weiß für Tag/Nacht [Tag=Weiß/Nacht=Schwarz] | Displayhintergrund getrennt für Tag/Nacht |
| Schriftgröße (Funktionsname/Wert/Tastenbeschriftung) | klein / groß [groß] | Gilt global für alle Tasten; Statuselemente im Standby immer klein |
| Verhalten bei Präsenz | Display wird eingeschaltet / zusätzlich Standby verlassen | Reaktion auf das Präsenzobjekt, z. B. bei Bewegungsmelder |
| Display-Helligkeit Tag/Nacht | dynamisch, 0–100 % | Feste oder dynamische (Lux-/Prozent-Objekt-gesteuerte) Displayhelligkeit |
| Globale Helligkeit für LEDs Tag/Nacht | ausgeschaltet, wie Display, Stufe 1–5 | Helligkeit aller Status-LEDs |
| Datenpunkttyp für dynamische Helligkeit | 2 Byte Lux (DPT 9.004) / 1 Byte Prozent (DPT 5.001) | Nur bei mind. einer dynamischen Helligkeitseinstellung sichtbar |
| Minimale/Maximale Helligkeit Tag/Nacht | 0–100 % [10 %/3 % bzw. 100 %/70 %] | Grenzwerte der dynamischen Regelung |
| Umgebungshelligkeit für 100 % Helligkeit | 0–1000 Lux [500 Lux] | Referenzwert bei Lux-Steuerung |
| Nachtabschaltung Display/LEDs im Standby | 0–100 Lux [25 Lux] | Schwelle für vollständiges Ab-/Einschalten (nur Nachtbetrieb) |
| Benutzerdefinierte Farben 1–3 | RGB-Mischung 0–100 % je Kanal | Frei mischbare Zusatzfarben für Symbole |
| Priorität von HVAC-Status | Frost/Komfort/Nacht/Standby oder Frost/Nacht/Komfort/Standby | Reihenfolge muss mit dem angesteuerten Regler übereinstimmen |

Ohne empfangenen Helligkeitswert setzt das Gerät die Helligkeit tagsüber auf 100 % und nachts auf
50 %. Wird der Taster bedient, während das Display aus ist, schaltet es sich unabhängig vom
Wiedereinschaltwert kurz ein und nach ca. 20 s wieder aus, sofern die Helligkeitsschwelle nicht
überschritten wird.

**Block: Infoanzeige (Standby-Darstellung)**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Zeit bis Display in Standby schaltet | 0–60 s (0 = nie) [20 s] | Inaktivitätszeit bis zum Standby |
| Standbyanzeige | Einzeln im Wechsel / in 1–2 Zeilen ohne Wechsel | Darstellungsart im Standby |
| Standbyanzeige wechseln nach | 1–60 s [5 s] | Nur bei „Einzeln im Wechsel“ |
| Standbyanzeige bei Tag/Nacht | kein Standby, Standby oberes Tastenfeld, Standby ganzer Bildschirm, Display aus (mit/ohne LEDs) | Legt fest, wie viele Statuselemente möglich sind (1, 2 oder 4) |
| Statuselement 1–4 | Uhrzeit, Datum, interne Temperatur/Feuchte/Taupunkt (nur T4.01), Statuswert 1–3, Statustext 1–2 | Frei wählbare Anzeigeinhalte je Element |
| Aktion bei Tastenbetätigung wenn Display aus / Standby aktiv | Standby verlassen bzw. anzeigen / Funktion ausführen oder nicht | Steuert, ob der erste Tastendruck schon eine Funktion auslöst |

Uhrzeit und Datum werden nach einem Busspannungsausfall auf die Werkswerte "00:00" und
"01.01.20 Mi" zurückgesetzt, bis neue Werte empfangen werden.

**Block: Status/Meldungen – Parametrierung**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Statuswert 1–3 | Nicht aktiv, DPT 1.001/5.001/5.005/7.012/7.013/9.001/9.004/9.005/9.007/9.008/9.021 | Wählt den Datenpunkttyp für die Anzeige |
| Text für Einheit / Beschreibung für Messwert | frei, 5 bzw. 15 Byte | Frei definierbare Beschriftung im Display |
| Meldung 1–4 (Bit-Objekt) | nicht aktiv / aktiv, Text, Anzeigedauer (bis Tastendruck oder 1 s–8 h) | Bis zu vier priorisierte Bit-Meldungen |
| Meldung Text (14-Byte-Objekt) | nicht aktiv / aktiv, Anzeigedauer | Niedrigste Priorität aller Meldungen |
| Rücknahme der Meldung über Objekt | nur Tastendruck/Dauer / zusätzlich über Wert 0 auf das Meldungsobjekt | Steuert, wie eine Meldung wieder verschwindet |
| Meldung über LEDs signalisieren / Farbe | nicht aktiv/aktiv, Farbwahl | Zusätzliche optische Signalisierung über die Status-LEDs |

Wie eine eintreffende Meldung dargestellt wird, hängt stark vom eingestellten Standby-Verhalten ab:
Bei "Standby im oberen Tastenfeld" wird nur das obere Tastenpaar für die Meldung genutzt und die
zugehörigen LEDs blinken verstärkt; bei "Display aus" wird die Meldung erst durch den nächsten
Tastendruck angezeigt und muss durch weitere Tastendrücke quittiert werden.

**Block: Tasten Einstellung (Grundverhalten)**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Tastenausrichtung für Zwei-Tastenfunktion | horizontal (links/rechts) / vertikal (oben/unten) | Legt fest, wie ein Tastenpaar bedient wird |
| Tasten 1/2 – 3/4 | nicht aktiv / Zwei-Tastenfunktion / Einzel-Tastenfunktion | Betriebsart je Taste bzw. Tastenpaar, auch gemischt möglich |
| Position der Beschriftung/Wert | oberhalb/unterhalb des Symbols | Gilt global für alle Tasten |
| Reaktionszeit bei Tastendruck | schnell/mittel/langsam | Entprellzeit; schnell empfohlen für Tippfunktionen |
| Zeit langer Tastendruck (Grundeinstellung) | 0,1–30 s [0,4 s] | Referenzzeit, auf die andere Funktionsblöcke zurückgreifen können |

**Block: Tastenfunktionen – identische Parameter**

Sperrobjekt (Nr. 9), Darstellung (Symbol + Funktionsname/Wert, siehe oben) sowie zwei Textfelder
("Objektbeschreibung", bis 30 Zeichen, erscheint im Menü und bei den Kommunikationsobjekten; und
"Zusatztext", bis 30 Zeichen, nur intern sichtbar) sind für alle Tastenfunktionen identisch aufgebaut.

**Block: Tastenfunktion Schalten**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Tastenbelegung (1/2) | Ein/Aus / Aus/Ein | Nur Zwei-Tastenfunktion |
| Unterfunktion | Schalten / Umschalten / Zustand senden | Nur Einzel-Tastenfunktion |
| Wert betätigte/losgelassene Taste | Aus/Ein | Bei „Zustand senden“ auch getrennt für Loslassen, ggf. mit Verzögerung |
| Gruppe langer/extra langer Tastendruck | EIN und AUS / nur EIN / nur AUS | Sendeverhalten der „innovativen Gruppensteuerung“ |
| Zeit langer/extra langer Tastendruck | Grundeinstellung, 0,1–30 s [2,0 s] | Erkennungszeiten für lang/extra lang |

Bei "Umschalten" sendet die Taste jeweils den zum zuletzt empfangenen Status invertierten Wert
(das Statusobjekt muss dazu mit dem Aktorstatus verbunden werden). Mit der Gruppensteuerung
lassen sich bis zu drei unterschiedliche Gruppenadressen aus einem einzigen, unterschiedlich lang
gehaltenen Tastendruck ansteuern (z. B. 2 s = "Gruppe lang", 4 s = "Gruppe extra lang" – bei 4 s
Haltezeit werden alle drei Werte nacheinander gesendet).

**Block: Tastenfunktion Werte senden**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Datenpunkttyp | DPT 1.001, 2.001, 5.001, 5.005, 17.001, 7.600, 9.001, 9.004, 232.600 | Legt den gesendeten Werttyp fest |
| Wert Taste 1–4 / Wert | beliebig gemäß DPT | Fester Sendewert je Taste (Zwei-Tasten) bzw. für die Taste (Einzel-Taste) |
| Sonderfunktion | Innovative Gruppensteuerung / Zusätzliches Objekt | Alternative Erweiterungen |
| Unterfunktion „Werte/Szenen umschalten“ | 2–4 Umschaltwerte, Zeitverzögerung 1–10 s, Umschaltart Anschlag/Überlauf | Schaltet zyklisch zwischen mehreren Werten um; optional fester Wert bei langem Tastendruck |
| Unterfunktion „Werte verschieben“ (nur Zwei-Tasten) | Grenzwerte, Schrittweite, Wiederholtes Senden 200 ms–3 s | Erhöht/verringert einen Wert schrittweise innerhalb einstellbarer Grenzen |
| Unterfunktion „Werte senden nach Zustand“ (nur Einzel-Taste) | DPT wie oben | Getrennter fester Wert für Tastendruck und Loslassen |
| Mehrfach-Tippfunktion (nur Einzel-Taste) | 2×/3× Tippen, optional 4. Funktion über langen Tastendruck, max. Zeit zwischen Betätigungen 0,1–30 s [0,5 s] | Bis zu 4 Werte (gleicher oder unterschiedlicher DPT) über eine Taste |

Die "Sonderfunktion Zusätzliches Objekt" blendet ein zweites, unabhängiges Sendeobjekt ein –
damit lässt sich z. B. mit einem Tastendruck gleichzeitig ein Dimmwert an einen Aktor und ein
RGB-Wert an einen LED-Controller senden.

**Block: Tastenfunktion Schalten/Werte senden kurz/lang (mit 2 Objekten)**

Kurzer und langer Tastendruck erhalten hier jeweils ein eigenständiges Objekt mit eigenem
Funktionstyp (Schalten/Schalten Ein/Schalten Aus/Umschalten/Werte senden/nicht aktiv) und bei
"Werte senden" auch einen eigenen Datenpunkttyp. Optional kann der kurze Wert zusätzlich beim
langen Tastendruck mitgesendet werden. Da beide Tastendrücke unterschiedliche Datenpunkte
haben können, ist im Display wahlweise nur die kurze oder nur die lange Funktion darstellbar.

**Block: Tastenfunktion Temperaturverschiebung (nur Zwei-Tasten, nur BE-TASxxT4.01)**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Temperaturverschiebung | 1 Bit / 1 Byte / 2 Byte / 2 Byte Verschiebung des Basis-Komfort-Sollwertes | Vier unterschiedliche Übertragungsarten je nach Reglertyp |
| Internen Temperaturwert verwenden | nicht aktiv / aktiv | Nutzt den eingebauten Sensor für die Ist-Temperatur-Anzeige |
| Schrittweite / unterer / oberer Grenzwert | 0,1–1 K, −10…10 K bzw. 0…45 °C | Grenzen der Sollwertverschiebung (je nach Übertragungsart) |
| Umschaltung berücksichtigt Statusobjekt | ja/nein | Steuert, ob sich der Taster am zuletzt gemerkten oder am tatsächlich empfangenen Sollwert orientiert |

Mit der Taste "−" wird der Sollwert um die Schrittweite gesenkt, mit "+" angehoben. Die Grenzen und
– bei 1-Byte/2-Byte-Verschiebung – die Schrittweite müssen mit dem angesteuerten Regler
übereinstimmen, damit Anzeige und tatsächlicher Sollwert synchron bleiben.

**Block: Tastenfunktion Betriebsartenumschaltung (nur BE-TASxxT4.01)**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Umschaltwerte | Komfort/Standby, Komfort/Nacht, Komfort/Standby/Nacht, Komfort/Standby/Nacht/Frost | Anzahl und Auswahl der zyklisch umschaltbaren Betriebsarten |
| Lange Taste | nicht aktiv / aktiv, feste Betriebsart je Taste (nur Zwei-Tasten) bzw. für die Taste | Fester Direktaufruf einer Betriebsart über langen Tastendruck |
| Umschaltart (nur Zwei-Tasten) | Anschlag / Überlauf | Verhalten am Ende der Umschaltkette |
| Umschaltung berücksichtigt Statusobjekt | ja/nein | wie bei der Temperaturverschiebung |
| Statusanzeige | kein Status / HVAC-Mode / HVAC-Status | Darstellungsart im Display |

**Block: Tastenfunktion Szene**

Kurzer Tastendruck ruft die Szene ab, ein aktivierter langer Tastendruck speichert sie. Szenennummer
1–64; das Kommunikationsobjekt sendet dabei nach KNX-Konvention Werte 0–63 (Abrufen) bzw.
128–191 (Speichern).

**Block: Tastenfunktion Jalousie/Rollladen**

Es entstehen zwei Objekte: ein Bewegobjekt (Auf/Ab bzw. "Fahren") und ein kombiniertes
Stopp-/Schrittobjekt (Stopp bei laufender Fahrt, sonst Lamellenverstellung). Bei Zwei-Tastenfunktion
ist die Tastenbelegung (Auf/Ab oder Ab/Auf) frei wählbar; bei Einzel-Tastenfunktion schaltet jeder
Tastendruck zwischen Auf- und Abfahrt um. "MDT Single Object Control" (nur Zwei-Tasten, im
Jalousieaktor separat zu aktivieren) erlaubt, mit kurzem Tastendruck zu starten und zu stoppen und
optional mit langem Tastendruck ein zentrales Rollladenobjekt (z. B. ganzer Raum) zu bedienen. Über
die "innovative Gruppensteuerung – extra lang" lässt sich nach 0,5 s Einzelfahrt und weiteren 1,5 s
eine Gruppenfahrt starten, die sich nach ca. 90 s wieder auf den Einzelkanal zurücksetzt.

**Block: Tastenfunktion Dimmen**

Start-Stopp-Dimmen: Solange die Taste gehalten wird, sendet der Taster 4-Bit-Telegramme
"heller"/"dunkler"; beim Loslassen folgt ein Stopp-Telegramm. Bei Zwei-Tastenfunktion ist die
Tastenbelegung (heller/dunkler oder umgekehrt) wählbar; bei Einzel-Tastenfunktion kehrt sich die
Richtung anhand des Kommunikationsobjekts "Status für Umschaltung" um.

**Block: Tastenfunktion HSV-Farbsteuerung und Farbtemperatur (Tunable White)**

Die HSV-Farbsteuerung regelt wahlweise Farbton, Sättigung oder Helligkeit eines RGB/RGBW-Dimmers
über einen 4-Bit-Dimmbefehl (Start-Stopp-Prinzip, Durchlauf durch den Farbkreis) plus – nur bei der
Unterfunktion Helligkeit und Einzel-Taste – ein Schaltobjekt zum Ein-/Ausschalten. Die
Tunable-White-Funktion steuert analog dazu die Farbtemperatur eines kompatiblen KNX-Dimmers; der
Status kann wahlweise in Prozent oder in Kelvin (intern auf 2700–6000 K skaliert) dargestellt werden.

### Status-LED, Logik und Temperatureinstellung (ETS-Parameter)

**Status-LED – Grundeinstellungen (gelten für alle 4 LEDs)**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| LED-Farbe bei Tastenbetätigung | Aus, Rot, Grün, Gelb, Blau, Pink, Cyan, Weiß | Nur bei Doppelbelegung „Objekt und Tastenbetätigung“ |
| LEDs Verhalten im Standby | Aus / Orientierungs-LEDs / Status-LEDs | Nutzung der LEDs außerhalb der Bedienung |
| Sperrobjekt für LEDs | nicht aktiv / aktiv | Aktiviert das gemeinsame Sperrobjekt (Nr. 60) |
| Synchronisierungsobjekt für Blinken von LEDs | nicht aktiv / Master / Slave | Gleichtaktet mehrere Taster |

**Status-LED 1–4 (je LED)**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| LED aktiv | Nein/Ja | Schaltet die jeweilige LED frei |
| LED reagiert auf | externes/internes Objekt, Tastenbetätigung, Kombinationen | Ansteuerungsquelle |
| Datenpunkttyp (bei externem Objekt) | 1 Bit Schalten / 1 Byte Prozent / 1 Byte Dezimal | Bei Dezimalwert feste Farbzuordnung 0=Schwarz…7=Cyan |
| Farbe/Verhalten bei Tag bzw. Nacht (Wert EIN/AUS) | 8 Farben, Dauer/Blinken | Getrennt parametrierbar für Tag- und Nachtbetrieb |

Über das zusätzliche Prioritätsobjekt (Nr. 56 je LED) kann eine LED unabhängig vom normalen
Anzeigeverhalten in einen definierten Zustand (Farbe, Dauer/Blinken, für Tag und Nacht getrennt)
gezwungen werden – nützlich für Störmeldungen, die Vorrang vor der normalen Statusanzeige haben.

**Logik – Grundeinstellungen und Logik 1–4**

Jeder der vier Logikblöcke wird per Dropdown aktiviert (Und/Oder/Wert senden bei
Tastenbetätigung) und erhält einen Objekttyp für den Ausgang (Schalten, Szene, Wert,
Zwangsführung 2 Bit). Im Untermenü lassen sich bis zu zwei externe Logikobjekte (mit Vorbelegung
nach Busspannungswiederkehr) sowie bis zu zwei Tasten (normal oder invertiert) als Eingänge
einbinden. Beim Objekttyp "Schalten" ist zusätzlich eine Sendebedingung (nicht automatisch, bei
Eingangstelegramm, bei Änderung, nur 0 oder nur 1) und eine Ausgangsinvertierung wählbar.

**Temperatureinstellung (nur BE-TASxxT4.01)**

Für Temperatur, relative Luftfeuchtigkeit und Taupunkttemperatur existiert jeweils ein eigenes
Untermenü mit nahezu identischer Struktur: "Messwert senden bei Änderung" (Schwellwert in
K bzw. %) und "Messwert zyklisch senden" (1–60 min) bestimmen das Sendeverhalten; ein
"Abgleichwert" (Temperatur ±5 K, Feuchte ±20 %) korrigiert ungünstige Einbausituationen (z. B. über
einem Heizkörper); die Gewichtung "Sensor intern/extern" (0–100 % in 10-%-Schritten) mischt den
internen mit einem optionalen externen Sensor. Für Temperatur und Feuchte lassen sich zusätzlich
ein oberer und ein unterer Meldewert mit je eigenem 1-Bit-Meldeobjekt aktivieren; die
Taupunktfunktion vergleicht die berechnete Taupunkttemperatur mit einem extern empfangenen
Vergleichswert und löst bei Unterschreiten einer Differenzschwelle (0–10 K) einen Taupunktalarm aus.

### Inbetriebnahme / Hinweise

1. Schnittstelle an den Bus anschließen (z. B. MDT USB-Interface).
2. Busspannung zuschalten.
3. Programmiertaste am Gerät drücken – die Status-LEDs blinken abwechselnd rot.
4. Physikalische Adresse über die ETS-Software laden – die LED erlischt nach erfolgreichem Laden.
5. Applikation mit der gewünschten Parametrierung laden.
6. Nach Abschluss die gewünschte Funktion prüfen (auch über die ETS-Software möglich).

Für eine kürzere Programmierzeit empfiehlt sich ein Interface mit Long-Frame-Unterstützung.
Rechtliche Hinweise laut Handbuch: Das Gerät darf nicht in Verbindung mit direkt oder indirekt
lebenssichernden Anwendungen genutzt werden; Montage und Anschluss sind ausschließlich durch
Elektrofachkräfte unter Beachtung der länderspezifischen und KNX-Richtlinien zulässig.

---

## Familie: Glastaster GTS (BE-GTSP6TX.01S)

### Übersicht

Das Handbuch (Stand 04/2026, Version 1.3, 264 Seiten) beschreibt zwei Gerätelinien: "Glas Touch
Smart" (BE-GTS06Tx.01S, Basisvariante) und "Glas Touch Smart Plus" (BE-GTSP6Tx.01S), jeweils in
Weiß oder Schwarz und mit KNX Secure. Konkret werden BE-GTS06TW.01S, BE-GTS06TS.01S,
BE-GTSP6TW.01S und BE-GTSP6TS.01S gelistet. BE-GTSP6TX.01S bezeichnet damit die "Plus"-Variante
mit 6-Zoll-Touch-Farbdisplay. Gegenüber dem Basisgerät bringt die Plus-Variante zusätzlich zwei
Binäreingänge, einen externen Anschluss für einen PT1000-Temperaturfühler, einen zweiten
Raumtemperaturregler, einen Lautsprecher für Audiosignale, eine Zeitschaltuhr sowie bis zu vier statt
einem Codeschloss-Benutzerprofil mit.

Zentrales Merkmal ist das hochauflösende Touch-Farbdisplay, auf dem bis zu 64 Funktionen als frei
positionier- und skalierbare Kacheln über bis zu 13 Seiten verteilt werden können; der Seitenwechsel
erfolgt per Wischgeste, per Sprungfunktion oder über ein 1-Byte-Objekt. Im Standby-Betrieb können
bis zu 12 Statuselemente gleichzeitig angezeigt werden. Das Gerät unterstützt KNX Data Secure und
– bei IP-Verbindung – KNX IP Secure für eine verschlüsselte, authentifizierte Kommunikation. Zwei
unabhängige PI-Raumtemperaturregler mit konfigurierbaren Sollwerten für Komfort, Standby, Nacht
und Frost-/Hitzeschutz ermöglichen die Heizungs-/Kühlungsregelung direkt über den Taster; der
zweite Regler kann wahlweise über den externen PT1000-Fühler arbeiten. Wie bei der Smart-Familie
ist eine "innovative Gruppensteuerung" über den extra langen Tastendruck verfügbar, ergänzt um
eine "Patschfunktion" für großflächige Berührungen (z. B. Zentral-Aus beim Verlassen des
Gebäudes). Acht interne Logikblöcke (Basisgerät: 4) mit Universal-Logik- oder
Logikgatter/Inverter-Funktion erlauben Verknüpfungen direkt im Gerät. Bis zu 20 priorisierte
Meldungen, eine umlaufende Ambientebeleuchtung (weiß bzw. bei "Plus" RGBW) und eine
Audiosteuerung mit Tasten-, Wischgesten- und Hinweistönen runden den Funktionsumfang ab. Das
Gerät ist über die MDT Firmware-Update-App aktualisierbar und unterstützt Long Frames zur
Verkürzung der Programmierzeit.

### Technische Daten

| Merkmal | Wert |
|---|---|
| Busanschluss | KNX TP (Busklemme), zusätzliche Klemme für Hilfsspannung |
| Display | Touch-Farbdisplay, 6 Zoll, bis zu 64 Funktionskacheln über bis zu 13 Seiten |
| Sicherheit | KNX Data Secure, KNX IP Secure (ETS ab Version 5.7 erforderlich) |
| Sensorik intern | Helligkeitssensor, Temperatursensor |
| Sensorik extern (nur "Plus") | Eingang für PT1000-Temperaturfühler |
| Binäreingänge (nur "Plus") | 2 Eingänge, einzeln oder gruppiert konfigurierbar, Entprellzeit 10–150 ms |
| Lautsprecher (nur "Plus") | integriert, für Tastentöne, Wischgesten-, Hinweis- und Patschtöne |
| Raumtemperaturregler | 2 unabhängige PI-/PWM-/2-Punkt-Regler (Komfort/Standby/Nacht/Frost-Hitzeschutz) |
| Zeitschaltuhr (nur "Plus") | mit Astro-/Feiertagsfunktion, bis zu 12 Funktionen |
| Logikfunktionen | 4 (Basisgerät) bzw. 8 (Plus), je Universal-Logik oder Logikgatter/Inverter |
| Update-Funktion | über MDT Firmware Update App |
| Long-Frame-Unterstützung | ja |
| Elektrische Kenndaten (Busspannung, Stromaufnahme), Abmessungen, Gewicht, Schutzart | nicht im Handbuch spezifiziert (nur im separaten Datenblatt) |

### Kommunikationsobjekte

Die folgende Übersicht zeigt die Objektnummernbereiche der wichtigsten Funktionsblöcke – nützlich,
um ein Objekt in der ETS schnell dem richtigen Funktionsblock zuzuordnen:

| Nr.-Bereich | Funktionsblock |
|---|---|
| 1–12 | Allgemeine Objekte (In Betrieb, Tag/Nacht, Uhrzeit/Datum, Seitenwechsel, Display-Helligkeit, Präsenz, Codeschloss, Diagnose) |
| 16 | Geräteeinstellungen über Szenen-Objekt |
| 17–31 | Audiosteuerung (nur „Plus“) |
| 33–72 | Meldungen 1–20 (Eingang + Ausgang je Meldung) |
| 73–81 | Ambientebeleuchtung |
| 82–85 | Temperaturmessung: Intern |
| 91–127 | Temperaturregler 1 |
| 160–199 (=91–127 +39 bzw. +69) | Temperaturregler 2 |
| 169–173 | Externe Eingänge: PT1000 (nur „Plus“) |
| 178–189 | Statuselemente 1–12 (+1 je weiterem) |
| 190–199 (+10 je weiterer Funktion) | Funktionen 1–64 |
| 830–839 | Patschfunktion |
| 840–849 (+10 für Eingang 2) | Externe Eingänge / Binäreingänge (nur „Plus“) |
| 860–869 (+10 je weiterer Logik) | Logikfunktionen (Universal-Logik bzw. Logikgatter/Inverter) |
| 945–961 (+7 je weiterer Zeitschaltuhr-Funktion) | Zeitschaltuhr (nur „Plus“) |

**Block: Allgemeine Objekte**

| Nr. | Name | Objektfunktion | Länge |
|---|---|---|---|
| 1 | In Betrieb | Ausgang (zyklisches Telegramm) | 1 Bit |
| 2 | Tag/Nacht | Eingang, Polarität parametrierbar | 1 Bit |
| 3 | Uhrzeit | Empfangen/Senden | 3 Byte |
| 4 | Datum | Empfangen/Senden | 3 Byte |
| 5 | Uhrzeit/Datum | Empfangen/Senden (kombiniert) | 8 Byte |
| 6 | Seitenwechsel | Eingang eines Wertes zum gezielten Seitenaufruf (0=Standby, 1=Seite 1 …) | 1 Byte |
| 7 | Display – Helligkeit | Eingang (Lux oder %) | 1/2 Byte |
| 8 | Display – Helligkeit | Ausgang | 1 Byte |
| 9 | Präsenz | Eingang | 1 Bit |
| 10 | Codeschloss | Zurücksetzen | 1 Bit |
| 11/12 | Diagnose 1/2 | Diagnosetext für Servicezwecke (ohne Einfluss auf die Gerätefunktion) | 14 Byte |
| 16 | Geräteeinstellung | Szenen-Nummer zum Auslösen interner Geräteeinstellungen | 1 Byte |

**Block: Audiosteuerung (nur "Plus")**

| Nr. | Name | Objektfunktion | Länge |
|---|---|---|---|
| 17/18 | Audiosteuerung | Tastenton / Ton für Seitenwechsel einstellen | 1 Byte |
| 19–23 | Audiosteuerung | Hinweiston 1–5 abspielen | 1 Bit |
| 24 | Audiosteuerung | Stumm-/Lautschalten (0/1) | 1 Bit |
| 25–31 | Audiosteuerung | Lautstärke Tastentöne, Wischgeste, Hinweiston 1–5 | 1 Byte |

Über diesen Block lassen sich Tasten-, Wischgesten- und bis zu fünf frei wählbare Hinweistöne
aktivieren und über den KNX-Bus auslösen bzw. lautstärkeseitig fernsteuern; zusätzlich kann der
Patschfunktion ein eigener Ton zugeordnet werden.

**Block: Meldungen (bis zu 20)**

| Nr. | Name | Objektfunktion | Länge |
|---|---|---|---|
| 33 (+1 je weiterer) | Meldung 1 | Meldung auslösen – Eingang | 1/2/4/14 Byte |
| 53 (+1 je weiterer) | Meldung 1 | Meldung – Ausgang | 1 Bit |

Jede Meldung besitzt eine eigene Priorität (1 = höchste), einen frei definierbaren Meldetext sowie
einen wählbaren Datenpunkttyp bzw. eine Sonderauslösung über "Busausfall" oder
"Programmiermodus"; das Ausgangsobjekt zeigt an, ob die Meldung aktuell aktiv ist.

**Block: Ambientebeleuchtung**

| Nr. | Name | Objektfunktion | Länge |
|---|---|---|---|
| 73 | Ambientebeleuchtung | Farbe Rot / RGB- / RGBW- / HSV-Wert / HSV-Farbton / CO2 / VOC / rel. Feuchte | 1–6 Byte |
| 74/75/76 | Ambientebeleuchtung | Farbe Grün/Blau/Weiß, HSV Sättigung/Helligkeit, Gesamthelligkeit | 1 Byte |
| 77 | Ambientebeleuchtung | Schalten | 1 Bit |
| 78–81 | Ambientebeleuchtung | Status (Farbwerte, Ein/Aus) | 1–6 Byte / 1 Bit |

Die umlaufende Beleuchtung auf der Geräterückseite kann je nach Modell weiß (Basisgerät) oder
RGBW (Plus) sein und wahlweise als Ambiente-Licht (Einzelobjekte, RGB-/RGBW-/HSV-Kombiobjekt)
oder als Signalisierung eines Luftqualitäts- bzw. Feuchtewertes (CO2, VOC, relative Feuchte)
genutzt werden.

**Block: Temperaturmessung: Intern**

| Nr. | Name | Funktion | Länge |
|---|---|---|---|
| 82 | Temperaturmessung: Intern | Messwert senden | 2 Byte |
| 83 | Temperaturmessung: Intern | Externer Sensor – Eingang | 2 Byte |
| 84/85 | Temperaturmessung: Intern | Max./Min. Wert über-/unterschritten | 1 Bit |

**Block: Externe Eingänge – PT1000 (nur "Plus")**

| Nr. | Name | Funktion | Länge |
|---|---|---|---|
| 169 | Temperaturmessung: PT1000 | Messwert senden | 2 Byte |
| 170 | Temperaturmessung: PT1000 | Externer Sensor – Eingang | 2 Byte |
| 171/172 | Temperaturmessung: PT1000 | Max./Min. Wert über-/unterschritten | 1 Bit |
| 173 | Temperaturmessung: PT1000 | Sensorfehler | 1 Bit |

An diesen zusätzlichen Analogeingang kann z. B. ein PT1000-Bodenfühler angeschlossen werden;
dessen Messwert lässt sich unabhängig vom internen Sensor auswerten oder mit einem weiteren
externen Sensor mitteln.

**Block: Temperaturregler 1 (Auszug; Regler 2 identisch mit Offset +39/+69)**

| Nr. | Name | Objektfunktion | Länge |
|---|---|---|---|
| 91–96 | Temperaturregler 1 | Sollwertvorgabe (gesamt, Komfort/Basis, Standby, Nacht, Frost/Hitzeschutz, Kombiobjekte) | 2/8 Byte |
| 97 | Temperaturregler 1 | Aktuellen Sollwert senden | 2 Byte |
| 98/99 | Temperaturregler 1 | Manuelle Sollwertverschiebung (2 Byte / 1 Byte / 1 Bit) | 1–2 Byte / 1 Bit |
| 100 | Temperaturregler 1 | Status Sollwertverschiebung senden | 2 Byte |
| 101/102 | Temperaturregler 1 | Stellwert Heizen/Kühlen: Stellgröße senden | 1 Bit oder 1 Byte |
| 103/104 | Temperaturregler 1 | Stellwert Heizen/Kühlen: Status senden | 1 Byte |
| 105 | Temperaturregler 1 | Zusatzstufe: Stellwert Heizen senden | 1 Bit |
| 106–110 | Temperaturregler 1 | Betriebsartvorwahl, Komfortverlängerung, Betriebsart Komfort/Nacht/Frost-Hitzeschutz | 1 Byte / 1 Bit |
| 111/112 | Temperaturregler 1 | Reglerstatus senden (HVAC Mode/Status, RHCC-, RTC-, RTSM-Status) | 1–2 Byte |
| 113/114 | Temperaturregler 1 | Frost-/Hitzealarm senden | 1 Bit |
| 115 | Temperaturregler 1 | Vorlauftemperatur Heizung empfangen | 2 Byte |
| 117 | Temperaturregler 1 | Diagnose Status | 14 Byte |
| 118 | Temperaturregler 1 | Fensterkontakt (Polarität wählbar) | 1 Bit |
| 119/120 | Temperaturregler 1 | Sperrobjekt Heizen/Kühlen: Stellwert sperren | 1 Bit |
| 123/124 | Temperaturregler 1 | Umschalten/Status Heizen/Kühlen | 1 Bit |
| 125/126 | Temperaturregler 1 | Anforderung Heizen/Kühlen senden | 1 Bit |
| 127 | Temperaturregler 1 | Außentemperatur/Führungsgröße empfangen | 2 Byte |

**Block: Statuselemente (Standby-Seite, bis zu 12)**

| Nr. | Name | Objektfunktion | Länge |
|---|---|---|---|
| 178 (+1 je weiterem) | Statuselement 1 | Schalten, Prozentwert, Dezimalwert, Farbtemperatur, Text … | 1–14 Byte |

**Block: Funktionen (bis zu 64, Basisnummer 190, +10 je weiterer Funktion)**

Analog zur Smart-Familie erhält jede der bis zu 64 Funktionen je nach gewähltem Funktionstyp einen
eigenen, um jeweils 10 Nummern versetzten Objektsatz (Schalten, Zustand senden, Dimmen,
Jalousie/Rollladen, Werte senden, Schalten/Werte senden kurz/lang, Status, Betriebsarten-
umschaltung, Temperaturverschiebung, Temperatursteuerung, Temperatur/Fan-Coil, Szenen,
Farbsteuerung [Schieberegler/Farbwähler], Multimedia, Seitenwechsel). Feste Objekte je Funktion
sind u. a. das Sperrobjekt (Nr. 199) und die Funktionsbeschreibung (Nr. 199, 14 Byte); die konkrete
Objektbelegung (190–198) richtet sich nach dem gewählten Funktionstyp.

| Nr. | Beispiel Objektfunktion | Länge |
|---|---|---|
| 190 | Schalten / Zwangsführung / Prozentwert / Dimmen Ein/Aus / Jalousie Auf/Ab / RGB-/HSV-Wert / Text | 1 Bit–6 Byte |
| 191 | Status, Dimmen relativ, Status für Anzeige, Stopp/Lamellen Auf/Zu | 1 Bit–14 Byte |
| 192 | Dimmen absolut, Status für Richtungswechsel, Gruppe lang, Lange Taste | 1 Bit–14 Byte |
| 193 | Status für Umschaltung, Absolute Höhenposition, Gruppe extra lang | 1 Bit–14 Byte |
| 199 | Sperrobjekt, Funktionsname | 1 Bit / 14 Byte |

**Block: Patschfunktion**

| Nr. | Name | Objektfunktion | Länge |
|---|---|---|---|
| 830 | Patschfunktion | Schalten / Werte senden / Szene je nach Funktionstyp | 1 Bit–14 Byte |
| 831 | Patschfunktion | Status | 1 Bit |
| 839 | Patschfunktion | Sperrobjekt | 1 Bit |

Die Patschfunktion löst durch großflächiges, kurzes Berühren der Sensoroberfläche eine einfache
Aktion aus (Schalten, Werte senden, Szenen oder Seitenwechsel) – typisch für zentrale Funktionen wie
"Alles Aus" beim Verlassen des Raums.

**Block: Externe Eingänge / Binäreingänge (nur "Plus", je Eingang Basisnummer 840, +10 für Eingang 2)**

Die zwei Binäreingänge unterstützen dieselben Funktionstypen wie die Tasten des Displays
(Schalten, Zustand senden, Dimmen, Jalousie/Rollladen, Werte senden, Schalten/Werte senden
kurz/lang) und können einzeln oder gruppiert betrieben werden; ein Sperrobjekt (Nr. 849/859) ist
ebenfalls verfügbar. Damit lassen sich konventionelle Taster oder Kontakte (z. B. Fensterkontakte)
in die KNX-Anlage einbinden.

| Nr. | Name | Objektfunktion | Länge |
|---|---|---|---|
| 840 | Eingang 1 / Eingänge 1-2 | Schalten, Zustand senden, Zwangsführung, Werte, Dimmen Ein/Aus, Jalousie Auf/Ab … | 1 Bit–14 Byte |
| 841–845 | Eingang 1 / Eingänge 1-2 | Status, Dimmen relativ, Stopp/Lamellen, 2. Objekt, Gruppe lang/extra lang | 1 Bit–14 Byte |
| 849/859 | Eingang 1 / Eingang 2 | Sperrobjekt | 1 Bit |

**Block: Logikfunktionen (bis zu 8, Basisnummer 860, +10 je weiterer Logik)**

| Nr. | Name (Universal-Logik) | Objektfunktion | Länge |
|---|---|---|---|
| 860 | Logik 1 | Eingang 1 | 1 Bit / 1 Byte |
| 861 | Logik 1 | Eingang 1 – Vergleichswert | 2 Bit–4 Byte |
| 862–866 | Logik 1 | Eingang 2–5 (+ Vergleichswerte) | 1 Bit–4 Byte |
| 868 | Logik 1 | Sperre / Freigabe | 1 Bit |
| 869 | Logik 1 | Ausgang | 1 Bit / 1 Byte |

Bei der Alternative "Logikgatter/Inverter" stehen stattdessen bis zu 8 Logikeingänge (Nr. 860 ff.) und
4 Inverter mit je eigenem Ausgang zur Verfügung, ebenfalls mit Sperr-/Freigabeobjekt (Nr. 868) und
gemeinsamem Ausgang (Nr. 869).

**Block: Zeitschaltuhr (nur "Plus", 12 Funktionen, +7 je weiterer Funktion ab Basisnummer 955)**

| Nr. | Name | Objektfunktion | Länge |
|---|---|---|---|
| 945–948 | Zeitschaltuhr | Sonnenaufgang/-untergang, Dämmerung, Tag/Nacht – Ausgang | 1 Bit |
| 1039/1040 | Zeitschaltuhr | Zentrale Sperre / Status | 1 Bit |
| 1041/1042 | Zeitschaltuhr | Urlaub Schalten/Anzahl Tage, Status | 1 Bit / 1 Byte |
| 1043/1044 | Zeitschaltuhr | Feiertag Aktivierung/Status | 1 Bit |
| 955–961 | Zeitschaltuhr Funktion 1 | Schalt-/Wert-/Jalousie-/Sollwert-Objekte je Funktionstyp, inkl. Sperre/Freigabe | 1 Bit–4 Byte |

Die Zeitschaltuhr kann über die integrierte Astrofunktion Sonnenauf-/-untergang und Dämmerung
selbst berechnen und daraus u. a. eine automatische Tag/Nacht-Umschaltung ableiten; eine
automatische Feiertagsberechnung sowie eine Urlaubsfunktion (mit Status in Resttagen) ergänzen die
klassische Schaltuhr mit bis zu 12 frei konfigurierbaren Funktionen (Schalten, Werte senden,
Temperaturverschiebung, Betriebsartenumschaltung, Jalousie, Rollladen, Dimmen).

### ETS-Parameter

**Block: Gerätekonfiguration – Geräteauswahl und Allgemeine Einstellungen**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Geräteauswahl | Glas Touch Smart (BE-GTS06TX.01S) / Glas Touch Smart Plus (BE-GTSP6TX.01S) | Legt fest, welche Applikationsvariante geladen wird |
| Geräteanlaufzeit | 00:02–04:00 mm:ss [00:02] | Wartezeit bis zur Betriebsbereitschaft |
| „In Betrieb“ zyklisch senden / Zykluszeit | nicht aktiv/aktiv, 00:01–24:00 hh:mm | Aktiviert das zyklische Lebenszeichen |
| Wert für Tag/Nacht | „Tag“=1/„Nacht“=0 oder umgekehrt | Polarität der Tag/Nacht-Umschaltung |
| Verhalten nach Neustart | „Tag“ / „Nacht“ | Betriebszustand direkt nach dem Start |
| Verhalten nach Programmierung | Parameterwerte laden / Geräteeinstellungen wiederherstellen | Legt fest, ob nach einer Nachprogrammierung die ETS-Werte oder zuletzt gespeicherte Einstellungen gelten |
| Zeit für langen/extra langen Tastendruck | 0,1–30 s [0,6 s bzw. 1,5 s] | Globale Grundzeiten für andere Funktionsblöcke |
| Freie Texte für Wochentage | je bis zu 4 Byte | Für Anzeige in Status-, Standby- und Zeitschaltuhr-Funktionen |

**Block: Codeschloss**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Codeschloss: Benutzer 1 (…4) | nicht aktiv / aktiv, 4-stelliger Code 0–9 | Beim Basisgerät nur 1 Benutzer, bei „Plus“ bis zu 4 |
| Codeschlosseingabe zurücksetzen | nach Standby-Wechsel / nach Zeit / nach Seitenwechsel / über Objekt / nach Display-Abschaltung | Steuert, wann eine unvollständige Eingabe verworfen wird |
| Zeit (bei „nach Zeit“) | 00:01–05:00 mm:ss [00:10] | Rücksetzzeit |

Das Codeschloss kann bestimmten Seiten zugewiesen werden (siehe Einstellungsseite/Seitenaufbau)
und schützt so z. B. Konfigurationsmenüs oder sensible Funktionen vor unbefugter Bedienung; das
Objekt Nr. 10 setzt die Eingabe bei Bedarf per KNX-Telegramm zurück.

**Block: Displayeinstellungen**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Minimale/Maximale Displayhelligkeit „Tag“/„Nacht“ | 0–100 % [10/100 bzw. 5/70] | Ober-/Untergrenzen der Helligkeitsregelung |
| Regelgeschwindigkeit der Displayhelligkeit | langsam/mittel/schnell(/sehr schnell/direkt) | Wie schnell die Helligkeit nachgeführt wird |
| Wert für Displayabschaltung | 0–65535 Lux | Helligkeitsschwelle, unterhalb derer das Display abschaltet |
| Maximale Displayhelligkeit (Lux-Referenz) | 0–65535 Lux | Wert, ab dem die maximale Helligkeit erreicht ist |
| Kurzzeit-Info / Anzeigedauer | nicht aktiv/aktiv, 00:01–04:00 mm:ss [00:20] | Kurzzeitiges Aufleuchten des Displays z. B. bei Statusänderung |
| Startseite / Zeit bis Wechsel zur Startseite | nicht aktiv/Standby/Seite 1–13, 1 s–5 min | Auf welche Seite nach Bedienpause gesprungen wird |
| Displayabschaltung / Zeit bis Abschaltung | nicht aktiv/aktiv, 5 s–2 h | Vollständiges Abschalten des Displays nach Inaktivität |

Die Displayhelligkeit kann wahlweise über feste Werte, über ein 1-Byte-Prozentobjekt oder über ein
2-Byte-Lux-Objekt (mit einstellbaren Minimal-/Maximalwerten) gesteuert werden; bei
Umschaltung zwischen "Vertikal" und "Horizontal" wird eine ggf. vorhandene DCA-Konfiguration
zurückgesetzt.

**Block: Touch-Einstellungen**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Wischgesten | nicht aktiv, 1-/2-Finger-Modus, 1 Finger vom Rand | Definiert, wie zwischen Seiten gewischt wird |
| Reaktion auf „Touch“ | schnell/mittel/langsam | Ansprechzeit auf eine Berührung |
| Touch-Bedienung durch Verdunkelung anzeigen | 0–100 % | Optisches Feedback beim Berühren einer Kachel |
| Farbe für Touch-Anzeige „Tag“/„Nacht“ | frei/definiert | Farbliches Feedback bei Berührung |
| Seitenaufruf beim Wischen (oben/unten) | nicht aktiv/Standby/Seite 1–13/Einstellungsseite | Ordnet Wischgesten feste Zielseiten zu |

**Block: Kacheleinstellungen und Standardwerte**

Hier werden globale Vorgaben für Transparenz (0–100 %) sowie zwei Standard- und zwei individuelle
Farbpaletten (je getrennt für Tag/Nacht, als Hex-Wert oder aus einer Dropdown-Liste) definiert, die
anschließend in Standby-Seite, normalen Seiten und der Einstellungsseite wiederverwendet werden
können.

**Block: Standby / Statuselemente**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Standby-Seite | nicht aktiv / aktiv | Grundsätzliche Aktivierung der Standby-Anzeige |
| Standby-Seite für „Tag“/„Nacht“ | gleich / unterschiedlich | Getrennte Gestaltung für Tag- und Nachtbetrieb möglich |
| Hintergrund / Hintergrundfarbe | nur Farbe / Hintergrundbild 1–2, frei oder definiert | Gestaltung des Standby-Hintergrunds |
| Helligkeitseinstellungen | aus Displayeinstellung übernehmen / individuell (0–100 %) | Eigene Helligkeitsgrenzen für die Standby-Seite |
| Aus Standby-Seite durch Tippen springen / auf Seite | nicht aktiv/aktiv, Seite 1–10 | Direkter Sprung von Standby auf eine Zielseite per Antippen |
| Anzahl: Statuselemente | 1–12 [1] | Anzahl der aktivierten Anzeigefelder; je Feld ein eigenes Konfigurationsmenü |
| Vorlage für Darstellung der Kacheln | 1–19 | Layoutvorlage für die Anordnung der Statuselement-Kacheln |

**Block: Seitenaufbau**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Anzahl: Seiten | 0–13 [1] | 0 = nur Startseite mit Statuswerten; je Seite eigenes Konfigurationsmenü |
| Navigationsleiste | nicht aktiv / aktiv | Dauerhaft sichtbare Seitenleiste zur Navigation |
| Objekt „Seitenwechsel“ | nicht aktiv / aktiv | Blendet Objekt Nr. 6 zum externen Seitenaufruf ein |

**Block: Funktionen – identische Parameter**

Jede der bis zu 64 Funktionen teilt sich unabhängig vom Funktionstyp folgende Grundparameter:
Textfelder (Funktionsblock-Beschreibung bis 40 Byte, Funktions-/Objektbeschreibung sowie
Zusatztext), Art der Darstellung (Symbol/Text/Kachelgröße) sowie ein optionales Sperrobjekt (Nr. 199)
mit zugehörigem Funktionsnamen-Objekt. Acht Funktionsblöcke zu je 8 Funktionen (1–8, 9–16 … bis
57–64) strukturieren die insgesamt 64 Funktionen in der ETS.

**Block: Funktionstypen (Auswahl je Funktion 1–64)**

| Funktionstyp | zentrale Parameter | Kommentar (zusammengefasst) |
|---|---|---|
| Schalten | Unterfunktion Ein-/Zwei-Tastenfunktion, Wert für betätigte Taste, innovative Gruppensteuerung | Klassisches Schalten, analog zur Smart-Familie |
| Zustand senden | Wert für betätigte/losgelassene Taste | Tastende Anwendung mit festen Werten je Flanke |
| Dimmen | Unterfunktion (Dimmen/nur heller/nur dunkler), Tastenbelegung | Start-Stopp-Dimmen wie bei den anderen Familien |
| Jalousie/Rollladen | Unterfunktion Ein-/Zwei-Tasten, Bedienfunktion, MDT Single Object Control, Schieberegler für Absolutwerte | Wie Smart-Familie, zusätzlich mit Absolutwert-Schieberegler für Höhen-/Lamellenposition |
| Werte senden | Unterfunktion Werte senden/umschalten/verschieben, Datenpunkttyp inkl. RGBW und String | Sendet feste/umschaltbare Werte, u. a. auch als Text (DPT 16.000) |
| Schalten/Werte senden kurz/lang | wie bei Smart-Familie, mit 2 unabhängigen Objekten | Getrennte Funktion für kurzen und langen Tastendruck |
| Status | Datenpunkttyp, Darstellung als Symbol/Balken/Text, Unterfunktion „Status: Energie“ | Reine Anzeige eines empfangenen Wertes, u. a. für Momentanleistung/-bezug |
| Betriebsartenumschaltung / Temperaturverschiebung / Temperatursteuerung / Temperatur-Fan-Coil | reglerspezifisch | Bedienelemente zur Beeinflussung eines der beiden Raumtemperaturregler |
| Szenen | Szenen-Nummer 1–64, Szene speichern | Kurz = Abruf, lang = Speichern (wenn aktiviert) |
| Farbsteuerung (Schieberegler/Farbwähler) | HSV-/RGB-/RGBW-Farbraum, Farbtemperatur (3 DPT-Varianten) | Steuerung von Leuchtmitteln über Schieberegler bzw. grafischen Farbwähler auf dem Display |
| Multimedia | Wiedergabe/Pause, Titel-/Interpret-Text (14 Byte) | Zeigt/steuert über den Bus bereitgestellte Medieninformationen |
| Seitenwechsel | Zielseite | Kachel zum gezielten Wechsel auf eine andere Displayseite |

Da die Funktionen direkt auf dem Display dargestellt werden, besitzt jeder Funktionstyp zusätzlich
Darstellungsparameter (Symbol, Farbe, Kachelgröße), die bei der TAL-Familie (ohne Display) entfallen.

**Block: Einstellungsseite**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Codeschloss für die Seite: Benutzer 1 (…4) | nicht aktiv / aktiv | Schützt die Einstellungsseite über das Codeschloss |
| Anzahl: Einstellungen | 1–8 [8] | Anzahl der dargestellten „einfachen Grundfunktionen“ (z. B. Putzfunktion, Programmiermodus-Status) |

**Block: Patschfunktion**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Patschfunktion | nicht aktiv / aktiv | Aktiviert die großflächige Berührungsfunktion |
| Funktionstyp | Schalten / Werte senden / Szenen / Seitenwechsel | Auswahl der auszulösenden Aktion |
| Unterfunktion / Datenpunkttyp / Wert | je nach Funktionstyp | Wie bei den entsprechenden Funktionstypen auf den normalen Seiten |

**Block: Geräteeinstellungen über Szenen-Objekt (ab SW v1.2.0)**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Anzahl: Einstellungen | 0–9 [0] | Aktiviert zusätzliche Einstellungen 2–10 (Einstellung 1 ist immer aktiv/reserviert) |
| Szenen-Nummer je Einstellung | nicht aktiv, 1–64 | Über diese Szenen-Nummer wird die jeweilige Geräteeinstellung ausgelöst |
| Putzfunktion (je Einstellung 2–10) | nicht aktiv / aktivieren über Aktivierungsdauer / deaktivieren / dauerhaft aktivieren | Sperrt das Touch-Display vorübergehend zur Reinigung |
| Display-Verhalten, Ambientebeleuchtung u. a. (je Einstellung) | AUS/EIN/keine Änderung | Weitere Geräteaktionen, die über den Empfang der Szenen-Nummer ausgelöst werden |

Mit diesem Mechanismus lässt sich z. B. per Szenenaufruf aus einer Visualisierung die Putzfunktion
aktivieren, ohne dass dafür ein eigenes Kommunikationsobjekt nötig ist – "Einstellung 1" ist fest für
das Zurücksetzen aller Geräteeinstellungen reserviert.

**Block: Audiosteuerung (nur "Plus")**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Akustische Bestätigung | nicht aktiv / aktiv | Grundsätzliche Aktivierung von Bedientönen |
| Tastenton bei Betätigung / Lautstärke | nicht aktiv, 1–5, 0–100 % [60 %] | Ton und Lautstärke bei Tastendruck |
| Ton bei Seitenwechsel / Lautstärke | nicht aktiv, 1–2, 0–100 % [60 %] | Akustisches Feedback beim Seitenwechsel |
| Hinweistöne über Objekte / Auswahl / Lautstärke | nicht aktiv, 1–5 Objekte, 1–10, 0–100 % [50 %] | Bis zu 5 über KNX auslösbare Hinweistöne |
| Ton für Patschfunktion | nicht aktiv / aktuellen Tasten-/Seitenwechselton / Hinweiston | Akustische Rückmeldung bei der Patschfunktion |

**Block: Meldungen**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Anzahl: Meldungen | 0–20 [1] | Aktiviert die jeweilige Anzahl an Meldungs-Untermenüs |
| Meldungs-/Objektbeschreibung, Meldetext | frei, je bis 40 Byte | Beschriftung und angezeigter Text der Meldung |
| Priorität (1 = höchste) | 1–20 [1] | Reihenfolge bei gleichzeitig aktiven Meldungen |
| Datenpunkttyp/Aktion für Meldung | DPT 1.001/5.*/7.*/9.*/12.*/13.*/14.*/16.*, Busausfall, Programmiermodus | Auslösebedingung der Meldung |
| Meldung auslösen bei | Wert „0“ / Wert „1“ (bei DPT 1.001) bzw. Vergleichsbedingung | Legt fest, wann die Meldung aktiv wird |

**Block: Ambientebeleuchtung**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Ambientebeleuchtung | nicht aktiv / aktiv | Grundaktivierung des umlaufenden Lichts |
| Ansteuerung via | RGBW-Einzelobjekte, RGB-Kombi + Weiß, RGBW-Kombi, HSV-Kombi/-Einzelobjekte, Signalisierung CO2/VOC/rel. Feuchte | Datenformat bzw. Zweckbindung der Ansteuerung (Farbmodi nur bei „Plus“) |
| Einschalten via Objekt | nicht aktiv / mit festem Helligkeitswert / mit letztem Helligkeitswert | Verhalten beim Einschalten über das Schaltobjekt |
| Ambientebeleuchtung aktiv für | „Tag“ und „Nacht“ / nur „Tag“ | Nur beim Basisgerät wählbar |
| Minimale/Maximale Helligkeit begrenzen | nicht aktiv / aktiv | Nur bei „Plus“, getrennt für Tag/Nacht |

Beim Basisgerät (weiße LEDs) dient die Ambientebeleuchtung primär als reines Orientierungs-/
Stimmungslicht, beim "Plus" (RGBW-LEDs) zusätzlich als farbige Signalisierung von Luftqualitäts- oder
Feuchtewerten.

**Block: Logikfunktionen**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Anzahl: Logikfunktionen | 1–4 (Basisgerät) bzw. 1–8 („Plus“) [1] | Anzahl aktivierter Logikblöcke |
| Hauptfunktion (je Logik) | nicht aktiv / Universal-Logik / Logikgatter/Inverter | Wahl des Logiktyps |
| Universal-Logik: Eingänge 1–5, Vergleichswerte | je nach DPT (1 Bit/1 Byte/2 Bit/2 Byte/4 Byte) | Bis zu 5 Bedingungen, die mit UND/ODER verknüpft werden |
| Logikgatter/Inverter: Eingänge 1–8, Inverter 1–4 | 1 Bit | Klassische Gatterlogik mit optionaler Signalinvertierung |
| Sperre/Freigabe (beide Varianten) | 1 Bit | Blockiert bzw. gibt die Logikauswertung frei |

Die Universal-Logik erlaubt es, bis zu fünf Eingänge unterschiedlichster Datenpunkttypen (Boolesch,
Zwangsführung, Szenen-Nummer, Zahlenwerte, Uhrzeit, Wochentag) jeweils gegen einen
Vergleichswert (aus Objekt oder Parameter) zu prüfen und die Teilergebnisse zu einer
Gesamtbedingung zu verknüpfen; die Alternative Logikgatter/Inverter bildet klassische
UND/ODER/XOR-Verknüpfungen mit bis zu 8 Eingängen sowie bis zu 4 unabhängige Inverter ab.

**Block: Temperaturregler 1 und 2**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Betriebsart | nicht aktiv / Heizen / Kühlen / Heizen und Kühlen | Grundaktivierung und -ausrichtung des Reglers |
| Sollwerte für Standby/Nacht | unabhängige Sollwerte / abhängig vom Sollwert Komfort (Basis) | Zwei grundsätzliche Strategien zur Sollwertbildung |
| Regelungsart (Stellgröße) | stetige PI-Regelung / PWM (schaltende PI-Regelung) / 2-Punkt-Regelung | Bestimmt, ob die Stellgröße 1 Byte (variabel) oder 1 Bit (EIN/AUS) ist |
| Wirksinn bei steigender Temperatur | normal / invertiert | Anpassung an stromlos geöffnete Ventile |
| Betriebsarten | Komfort, Standby, Nacht, Frost-/Hitzeschutz | Vier hinterlegte Betriebszustände mit je eigenem Sollwert-Offset |
| Sollwertverschiebung | 1 Bit (Schritt) / 1 Byte (Zählimpulse) / 2 Byte (Differenz oder Absolutwert) | Externe Beeinflussung des Komfort-Sollwertes |
| Betriebsartenumschaltung / HVAC-Statusobjekte | 1 Bit oder 1 Byte je Betriebsart, kombinierte Statusobjekte (RHCC, RTC, RTSM) | Für Visualisierungen und übergeordnete Regler |
| Führung über Außentemperatur | Führungsgröße Minimum/Maximum, Sollwertänderung bei max. Führungsgröße | Passt den Sollwert automatisch an die Außentemperatur an |
| Vorlauftemperaturbegrenzung | 10–60 °C [40 °C] | Begrenzt z. B. die Fußbodenheizung auf eine maximale Vorlauftemperatur |
| Fensterkontakt | Polarität wählbar | Schaltet die Heizung/Kühlung bei geöffnetem Fenster ab |
| Sperrobjekte Heizen/Kühlen | 1 Bit | Sperrt den jeweiligen Stellwert unabhängig von der Regelung |

Der zweite Regler (Temperaturregler 2) teilt sich die gleiche Parameterstruktur wie Regler 1
(Objektnummern um 39 versetzt), kann aber unabhängig konfiguriert und z. B. über den externen
PT1000-Sensor betrieben werden.

**Block: Zeitschaltuhr (nur "Plus")**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Uhrzeit-/Astroeinstellungen | Standort/Zeitzone, Sommerzeitumschaltung | Grundlage für Sonnenauf-/-untergang und Dämmerungsberechnung |
| Automatische Feiertagsberechnung | länderspezifisch aktivierbar | Berücksichtigt Feiertage automatisch in den Schaltzeiten |
| Auswahl der Funktionen / Funktion 1–12 | Schalten, Werte senden, Temperaturverschiebung, Betriebsartenumschaltung, Jalousie, Rollladen, Dimmen | Bis zu 12 unabhängige Schaltuhr-Kanäle |
| Schaltzeiten je Funktion | Uhrzeit/Astro-Ereignis, Wochentage, Wert | Beliebig viele Schaltzeitpunkte je Funktion |
| Sperrobjekt-Typ, Urlaub, Werte zyklisch senden | je nach Funktion | Zusatzoptionen zur Ausnahmebehandlung (z. B. Urlaubsmodus) |

**Block: Externe Eingänge – PT1000 (nur "Plus")**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Temperaturmessung | nicht aktiv / aktiv | Aktiviert den PT1000-Eingang |
| Messwert senden bei Änderung von / zyklisch senden | nicht aktiv, 0,1–5,0 K [0,2 K] / 00:01–04:00 hh:mm [00:20] | Sendebedingungen wie bei der internen Temperaturmessung |
| Aus PT1000 und externem Sensor | Mittelwert bilden / Maximalwert / Minimalwert | Verrechnung mit einem zusätzlichen externen Sensor |
| Sensor PT1000/extern (Gewichtung) | 100 % PT1000 … 100 % extern | Mischverhältnis bei „Mittelwert bilden“ |
| Abgleichwert für PT1000 | −5,0…5,0 K [0] | Korrekturwert für den Messwert |
| Oberer/unterer Meldewert, Hysterese | 20–45 °C bzw. 3–30 °C, 0–10 % [5] | Grenzwertmeldungen mit Hysterese |
| Sensor überwachen (Min./Max. Wert) | −20…60 °C | Erkennt einen fehlerhaften/getrennten Fühler |

**Block: Binäreingänge – Grundeinstellungen und Funktionen der Eingänge (nur "Plus")**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) |
|---|---|---|
| Eingänge 1/2 | nicht aktiv / einzeln / gruppiert | Legt fest, ob zwei unabhängige Kanäle oder ein gemeinsamer Kanal genutzt werden |
| Entprellzeit | 10–150 ms [30 ms] | Fängt das mechanische Kontaktprellen konventioneller Taster ab |
| Sperrobjekt | nicht aktiv / aktiv | Sperrt den jeweiligen Eingang bzw. das Eingangspaar |

Die Binäreingänge unterstützen dieselben Funktionstypen (Schalten, Dimmen, Jalousie/Rollladen,
Werte/Zustände senden) wie die Display-Tasten und erlauben so den Anschluss klassischer
Wandtaster oder Kontakte an das Glastaster-Gerät.

### Sicherheit (KNX Secure)

KNX Secure unterscheidet zwei Mechanismen: IP Secure verschlüsselt und authentifiziert die
Kommunikation auf IP-Ebene (Tunneling/Routing), Data Secure verschlüsselt/authentifiziert die
eigentlichen Telegramme unabhängig vom Medium, sofern beide Kommunikationspartner dies
unterstützen (die Nutzung setzt ETS ab Version 5.7 voraus). Für die gesicherte Inbetriebnahme wird
ein gerätespezifisches Zertifikat benötigt, das einmalig in der ETS hinterlegt wird (Scan des QR-Codes
oder manuelle Eingabe); danach arbeitet das Gerät im "abgesicherten Modus" mit verschlüsselter
Übertragung (erkennbar am blauen Schild-Symbol). Ohne aktiviertes ETS-Projektpasswort ist keine
gesicherte Inbetriebnahme möglich, das Gerät läuft dann im "nicht abgesicherten Modus" (Plain
Mode) mit unverschlüsselter Übertragung.

### Inbetriebnahme / Hinweise

1. Verdrahtung des Gerätes nach Anschlussschema (Busklemme, ggf. Hilfsspannung, externe
   Eingänge/PT1000 bei der Plus-Variante).
2. Schnittstelle an den Bus anschließen, Busspannung zuschalten.
3. Programmiertaste drücken – die rote Programmier-LED leuchtet dauerhaft.
4. Physikalische Adresse in der ETS einstellen und programmieren – die LED erlischt.
5. Bei aktiviertem KNX Secure: Gerätezertifikat einmalig hinterlegen (QR-Code scannen oder
   eintippen); dafür ist ein ETS-Projektpasswort erforderlich, sonst lädt das Gerät ungesichert.
6. Rücksetzen auf Werkseinstellung (z. B. bei fehlgeschlagener Erstinbetriebnahme):
   Programmiertaste mindestens 10 s gedrückt halten, bis die LED blinkt, kurz loslassen, danach
   erneut mindestens 5 s gedrückt halten, bis die LED schnell blinkt; nach dem Loslassen führt das
   Gerät einen Neustart mit Werkseinstellungen durch.

Hinweis: Die Zertifikate aller Geräte eines Projekts sollten nach der Erstinbetriebnahme vom
Geräteaufkleber getrennt und projektbezogen aufbewahrt werden, da sie nur bei einem Master-
Reset erneut benötigt werden. Rechtliche Hinweise laut Handbuch: Die Geräte sind für den Betrieb in
der EU und im Vereinigten Königreich zugelassen (CE/UKCA), die Verwendung in den USA und Kanada
ist nicht gestattet; Montage und Anschluss sind ausschließlich durch Elektrofachkräfte zulässig.

---
## Familie: TAL-Serie (BE-TAL6301.01 / BE-TAL6302.01)

### Varianten

| Artikelnummer | Kanäle |
|---|---|
| BE-TAL6301.01 | 1 |
| BE-TAL6302.01 | 2 |

Beide Artikel gehören zur Baureihe "Taster Light 63" (Studioweiß glänzend) in der NEUTRAL-
Ausführung ohne integrierten Temperatursensor. Das zugrunde liegende technische Handbuch
deckt darüber hinaus die baugleiche "Taster Light 55"-Reihe (anderes Rahmendesign, 1-/2-/4-fach,
mit und ohne Temperatursensor, teils mit vorkonfigurierter Jalousie- oder Schaltfunktion) sowie die
reduzierte "Taster Light 55 Basic"-Reihe (ohne RGBW-Status-LEDs, ohne Tag/Nacht-Objekt) ab. Für
BE-TAL6301.01 und BE-TAL6302.01 ist in der ETS unter "Geräteauswahl" der jeweils passende Typ
("Taster Light 63" bzw. bei 2-fach-Geräten die 2-fach/4-fach-Grundeinstellung) auszuwählen, da
2-fach- und 4-fach-Taster dieselbe Applikation nutzen und sich nur in der Anzahl aktiver Tasten
unterscheiden.

### Übersicht

Die TAL-Serie ist ein tastenbasierter Taster ohne Display. Jede Taste kann per Einzeltaste oder
Tastenpaar eine von mehreren Funktionen auslösen: Schalten, Werte senden, Szene,
"Schalten/Werte senden kurz/lang" (zwei Objekte auf einer Taste), Jalousie/Rollladen und Dimmen.
Wie bei der Smart-Familie steht eine "innovative Gruppensteuerung" zur Verfügung, mit der ein
extra langer Tastendruck eine übergeordnete Gruppenfunktion auslöst (z. B. einzelne Jalousie vs.
alle Jalousien im Raum). Über die "Mehrfach-Tippfunktion" lassen sich einer Einzeltaste bis zu vier
verschiedene Funktionen mit jeweils eigenem Datenpunkttyp zuordnen. Bei den Geräten mit RGBW-
Status-LED (BE-TAL55xx.x1 und BE-TAL63xx.x1 – dazu zählen auch BE-TAL6301.01/6302.01) steht
pro Taste eine farbige Status-LED zur Verfügung, die auf Tastendruck oder auf ein internes/externes
Objekt reagiert; über ein Prioritätsobjekt lassen sich wichtige Zustände hervorgehoben anzeigen.
Vier interne Logikblöcke erlauben einfache Verknüpfungen aus internen und externen Objekten. Ein
integrierter Temperatursensor ist ausschließlich bei den "T"-Varianten (z. B. BE-TAL63T1.01)
vorhanden – **nicht** bei BE-TAL6301.01 und BE-TAL6302.01. Das Gerät unterstützt Long Frames zur
Verkürzung der ETS-Programmierzeit und ist über die MDT Updatetool-App (DCA) aktualisierbar.

### Technische Daten

| Merkmal | Wert |
|---|---|
| Busanschluss | KNX TP (Busklemme) |
| Bauform BE-TAL6301.01 | 1-fach Taster, RGBW-Status-LED, Studioweiß glänzend |
| Bauform BE-TAL6302.01 | 2-fach Taster, 2× RGBW-Status-LED, Studioweiß glänzend |
| Temperatursensor | nicht vorhanden (nur bei "T"-Varianten der Baureihe, z. B. BE-TAL63T1.01/T2.01) |
| Long-Frame-Unterstützung | ja |
| Update-Funktion | über MDT Updatetool-App (DCA) |
| Elektrische Kenndaten (Busspannung, Stromaufnahme), Abmessungen, Gewicht, Schutzart | nicht im Datenblatt spezifiziert |

### Kommunikationsobjekte

**Block: Tasten (Standardeinstellungen, gilt für BE-TAL6301.01 und BE-TAL6302.01)**

| Nr. | Name | Objektfunktion | Länge | Gilt für Variante(n) |
|---|---|---|---|---|
| 0 | T1: / T1/2: | Schalten | 1 Bit | 6301.01, 6302.01 |
| 0 | T1: | Umschalten | 1 Bit | 6301.01, 6302.01 |
| 0 | T1: | Zustand senden | 1 Bit | 6301.01, 6302.01 |
| 0 | T1: / T1/2: | Zwangsführung | 2 Bit | 6301.01, 6302.01 |
| 0 | T1: / T1/2: | Prozentwert / Dezimalwert / Szene | 1 Byte | 6301.01, 6302.01 |
| 0 | T1: / T1/2: | Farbtemperatur / Temperaturwert / Helligkeitswert | 2 Byte | 6301.01, 6302.01 |
| 0 | T1: / T1/2: | RGB-Wert / HSV-Wert | 3 Byte | 6301.01, 6302.01 |
| 0 | T1: / T1/2: | Jalousie/Rollladen Auf/Ab, Dimmen Ein/Aus | 1 Bit | 6301.01, 6302.01 |
| 9 | T1: / T1/2: | Sperrobjekt | 1 Bit | 6301.01, 6302.01 |

Das jeweils sichtbare Objekt hängt – analog zur Smart-Familie – vom in der ETS gewählten
Funktionstyp der Taste ab. Bei BE-TAL6302.01 verdoppeln sich die Tastenobjekte entsprechend für
die zweite Taste bzw. das zweite Tastenpaar. Das Sperrobjekt kann je Taste bzw. Tastenpaar
zugeschaltet werden und blockiert bei "1" jede weitere Bedienung dieser Taste.

**Block: Logikfunktion**

| Nr. | Name | Objektfunktion | Länge | Gilt für Variante(n) |
|---|---|---|---|---|
| 50 | Logik 1 Eingang A | Eingang | 1 Bit | 6301.01, 6302.01 |
| 51 | Logik 1 Eingang B | Eingang | 1 Bit | 6301.01, 6302.01 |
| 52 | Logik 1 Ausgang | Schalten / Wert / Szene | 1 Bit, 2 Bit, 1 Byte | 6301.01, 6302.01 |

Vier Logikblöcke (Basisnummer +3 je weiterem Block) verknüpfen zwei Eingänge zu einem
Ausgangswert; wie bei der Smart-Familie ist der Ausgangsdatenpunkt frei wählbar.

**Block: Status-LED**

| Nr. | Name | Objektfunktion | Länge | Gilt für Variante(n) |
|---|---|---|---|---|
| 62 | LED 1 | Schalten/Prozentwert/Dezimalwert | 1 Bit / 1 Byte | 6301.01, 6302.01 |
| 66 | LED 1 Priorität | Schalten | 1 Bit | 6301.01, 6302.01 |
| 70 | LED | Sperrobjekt | 1 Bit | 6301.01, 6302.01 |
| 78 | LED – Synchronisieren | Blinkstatus als Master/Slave | 1 Bit | 6301.01, 6302.01 |
| 79 | Helligkeit | Eingang für dynamische Helligkeit | 1 Byte / 2 Byte | 6301.01, 6302.01 |

Die Status-LED kann direkt auf Tastendruck reagieren oder mit einem beliebigen internen/externen
Objekt verknüpft werden. Das Prioritätsobjekt erlaubt es, einen wichtigeren Zustand (z. B. eine
Störmeldung) unabhängig von der normalen LED-Logik farblich hervorzuheben. Über das
Synchronisierungsobjekt kann das Blinken mehrerer Taster geräteübergreifend gleichgetaktet
werden (ein Gerät als Master, andere als Slave).

**Block: Temperatur** – *entfällt bei BE-TAL6301.01 und BE-TAL6302.01*, da diese Artikel keinen
integrierten Temperatursensor besitzen. Die Objekte 73–76 (Messwert senden, externer Sensor,
oberer/unterer Grenzwert) existieren nur bei den "T"-Varianten der Baureihe (z. B. BE-TAL63T1.01/
T2.01/T4.01) und sind hier der Vollständigkeit halber nicht als Standardobjekte der Zielgeräte
aufgeführt.

### ETS-Parameter

**Block: Geräteauswahl und Allgemeine Einstellungen**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) | Gilt für Variante(n) |
|---|---|---|---|
| Geräteauswahl | u. a. „BE-TAL55/63T2.01 NEUTRAL 2-fach“ | Wählt die passende Tasterversion innerhalb der Familie; 2-fach- und 4-fach-Geräte teilen sich dieselbe Grundeinstellung und müssen bei 4-fach-Geräten explizit umgestellt werden | 6301.01, 6302.01 |
| Geräteanlaufzeit | 2–240 s [2 s] | Wartezeit bis zur Betriebsbereitschaft | 6301.01, 6302.01 |
| „In Betrieb“ zyklisch senden | nicht aktiv, 1 min–4 h | Aktiviert das zyklische Lebenszeichen-Telegramm | 6301.01, 6302.01 |
| Wert für Tag/Nacht | Tag=1/Nacht=0 oder umgekehrt | Polarität der Tag/Nacht-Umschaltung | 6301.01, 6302.01 |
| Status für Umschaltung / Tag/Nacht-Objekt nach Busspannungswiederkehr | nicht abfragen / abfragen | Steuert automatisches Abfragen der Statuswerte nach Reset | 6301.01, 6302.01 |

**Block: Tastenfunktionen – Schalten / Werte senden / Jalousie / Dimmen / Szene**

| Funktionstyp | zentrale Parameter | Kommentar (zusammengefasst) | Gilt für Variante(n) |
|---|---|---|---|
| Schalten | Wert für betätigte Taste, Zwei-Tastenfunktion | Klassisches Ein-/Ausschalten je Taste bzw. Tastenpaar | 6301.01, 6302.01 |
| Werte senden | Datenpunkttyp (Zwangsführung, Prozent, Dezimal, Szene, Farbtemperatur, Temperatur, Helligkeit, RGB) | Sendet feste Werte unterschiedlichster Datentypen | 6301.01, 6302.01 |
| Schalten/Werte senden kurz/lang | getrennte Aktion für kurzen und langen Tastendruck | Auf einer Taste liegen zwei unabhängige Funktionen mit je eigenem Objekt | 6301.01, 6302.01 |
| Jalousie/Rollladen | Tastenbelegung Auf/Ab, Bedienfunktion, MDT Single Object Control, Gruppensteuerung extra lang | Steuert Fahr- und Lamellenbewegung; Single-Object-Control erlaubt Start/Stopp über eine Taste | 6301.01, 6302.01 |
| Dimmen | Tastenbelegung heller/dunkler, Zeit langer Tastendruck | Start-Stopp-Dimmen wie bei der Smart-Familie | 6301.01, 6302.01 |
| Szene | Szenen-Nummer 1–64, Szene speichern | Kurz = Abruf, lang = Speichern (wenn aktiv) | 6301.01, 6302.01 |

**Block: LED-Grundeinstellung**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) | Gilt für Variante(n) |
|---|---|---|---|
| Sperrobjekt für LEDs | nicht aktiv / aktiv | Schaltet bei Aktivierung alle LEDs gemeinsam aus | 6301.01, 6302.01 |
| Verhalten der LEDs bei Busspannungswiederkehr | LED-Objekte nicht abfragen / abfragen | Steuert automatisches Nachladen des LED-Status nach einem Reset | 6301.01, 6302.01 |
| Synchronisierungsobjekt für Blinken von LEDs | nicht aktiv / Master / Slave | Gleichtaktet das Blinken mehrerer Taster | 6301.01, 6302.01 |
| Globale Helligkeit für LEDs „Tag“/„Nacht“ | nicht aktiv, Stufe 1–5, dynamisch [Stufe 3 / Stufe 1] | Grundhelligkeit der Status-LEDs, wahlweise fest oder dynamisch (über Lux- oder Prozentobjekt) geregelt | 6301.01, 6302.01 |

**Block: LED 1–4 (Zuordnung, Farbe, Verhalten)**

| ETS-Text | Wertebereich [Default] | Kommentar (zusammengefasst) | Gilt für Variante(n) |
|---|---|---|---|
| LED aktiv | Nein / Ja | Schaltet die jeweilige Status-LED frei | 6301.01, 6302.01 |
| LED reagiert auf | externes/internes Objekt, Tastenbetätigung, Kombinationen | Legt fest, wodurch die LED angesteuert wird | 6301.01, 6302.01 |
| Auswahl der Objektnummer | 0–79 [0] | Verknüpft die LED mit einem internen Objekt (nur bei „internes Objekt“) | 6301.01, 6302.01 |

### Inbetriebnahme / Hinweise

1. Verdrahtung des Gerätes nach Anschlussschema.
2. Schnittstelle an den Bus anschließen, Busspannung zuschalten.
3. Programmiertaste am Gerät drücken – die Status-LEDs blinken abwechselnd oben/unten rot.
4. Physikalische Adresse in der ETS einstellen und programmieren – die Status-LEDs erlöschen.
5. Einstellungen im Applikationsprogramm vornehmen und programmieren.

Wichtig: Vor der eigentlichen Parametrierung muss in der ETS unter "Geräteauswahl" der korrekte
Gerätetyp (hier: Taster Light 63, 1-fach bzw. 2-fach) eingestellt werden, da 2-fach- und 4-fach-
Geräte werkseitig auf derselben Grundeinstellung stehen.

---

## Quelle

- **Smart 55/63 (BE-TAS63T4.01):** `originals/KNX/MDT_THB_BE_01_Taster_Smart_55_63.pdf` –
  MDT Technisches Handbuch "Taster Smart 55/63", Stand 08/2020, Version 1.0 (vollständiges
  Dokument, 90 Seiten, direkt ausgewertet).
- **Glastaster GTS (BE-GTSP6TX.01S):** `originals/KNX/MDT_BE-GTSx6Tx-01S_MDT_TM_V13_DE.pdf` –
  MDT Technisches Handbuch "Glas Touch Smart 6 Zoll / Plus 6 Zoll [BE-GTSx6Tx.01S]", Stand
  04/2026, Version 1.3 (vollständiges Dokument, 264 Seiten, direkt ausgewertet).
- **TAL-Serie (BE-TAL6301.01 / BE-TAL6302.01):**
  `originals/KNX/MDTBE-TAL55_63xx.x1_MDT_TM_V14_DE.pdf` – MDT Technisches Handbuch "Taster
  Light 55/63/Basic [BE-TALxxxx.x1]", Stand 09/2024, Version 1.4 (ausgewertet über
  themenbezogene Auszüge, nicht als vollständiges Dokument; siehe Hinweis in der Übersicht).

**Hinweis zur Datentiefe:** Die Abschnitte "Smart 55/63" und "Glastaster GTS" basieren auf den
vollständig eingelesenen Original-PDFs und decken sämtliche Kapitel der jeweiligen Handbücher ab
(bei der GTS-Familie u. a. inklusive Temperaturregler, Zeitschaltuhr, Logikfunktionen,
Ambientebeleuchtung, Audiosteuerung und externer Eingänge). Bei sehr umfangreichen
Reglerkapiteln (z. B. PI-/PWM-/2-Punkt-Regelparameter der GTS-Temperaturregler) wurden die
Kernkonzepte und wichtigsten Parameter zusammengefasst statt jede einzelne Detaileinstellung
tabellarisch zu reproduzieren – dies entspricht dem Ziel dieser Wissensbasis, die funktionalen
Zusammenhänge zu erklären, da die vollständigen ETS-Parametertabellen bereits in der ETS
vorliegen.
