---
title: MDT Raumtemperatur-/Feuchtesensor SCN-TFS63.01
device_type: Raumtemperatur-/Feuchtesensor
manufacturer: MDT
article_number: [SCN-TFS63.01]
bus: KNX TP
source_pdf: originals/KNX/MDT_THB_SCN_01_Objektregler_Raumtemperatur_FeuchteSensor_V10.pdf
last_updated: 2026-07-25
synonyms: [Raumtemperaturregler, Objektregler, Feuchtesensor, Raumklimasensor]
tags: [knx, raumtemperatur-feuchtesensor, mdt]
---

## Übersicht

Der SCN-TFS63.01 ist ein reiner Mess-Sensor für Raumtemperatur und relative Luftfeuchtigkeit im KNX/EIB-System, in der Studioweiß-glänzend-Ausführung (63er Rahmenserie). Im Gegensatz zum baugleichen "Objektregler" (SCN-RTRxxO.01) besitzt dieses Gerät **keinen** integrierten Temperaturregler, keine Lüftungssteuerung und keine Binäreingänge – es liefert ausschließlich Messwerte (Temperatur, relative/absolute Luftfeuchte, Taupunkt, Behaglichkeitsindex) auf den Bus. Diese Werte können von einem separaten Regler (z. B. einem anderen KNX-Aktor/Controller) weiterverarbeitet werden.

Das Gerät wird über den KNX-Bus versorgt und programmiert (Programmiertaste + LED auf der Geräterückseite). Ein zusätzlicher externer Sensor-Eingang erlaubt es, einen zweiten Messwert (z. B. von einer Nebenstelle) einzubinden und mit dem internen Sensor zu einem Mischwert zu verrechnen.

## Technische Daten

| Merkmal | Wert |
|---|---|
| Artikelnummer | SCN-TFS63.01 |
| Bezeichnung | Raumtemperatur-/Feuchtesensor 63, Studioweiß glänzend |
| Busanschluss | KNX/EIB TP (Busanschlussklemme) |
| Funktionen | Temperatur- und Luftfeuchtemessung (intern + optional extern) |
| Anzeige-/Bedienelemente | Programmierknopf und Programmier-LED |
| Handbuch-Version | Stand 06/2020, V1.0 |

Genaue mechanische Maße, Messtoleranzen (Genauigkeitsangaben in °C/%) sowie Umgebungsbedingungen sind im vorliegenden technischen Handbuch **nicht spezifiziert** – hierzu wird auf das separate Datenblatt verwiesen (siehe Verweis "Weitere Dokumente" im Original-PDF).

Hinweis aus dem Handbuch: Nach Erstinstallation/Programmierung benötigen die Messwerte ca. 30 Minuten, bis sie stabil sind.

## Kommunikationsobjekte

Für den Raumtemperatur-/Feuchtesensor sind nur die Objekte des Funktionsblocks "Temperatur- und Luftfeuchtemessung" relevant (Objektnummern 53–73). Die Objektblöcke für Temperaturregler, Lüftungssteuerung und Binäreingänge existieren nur beim Objektregler (SCN-RTRxxO.01) und entfallen hier.

### Temperatur

| Nr. | Name | Funktion | DPT/Größe | Flags |
|---|---|---|---|---|
| 53 | Temperatur | Messwert senden | 2 Byte | K, L, Ü |
| 54 | Temperatur | Externer Temperatursensor (Messwert empfangen) | 2 Byte | K, S, Ü, A |
| 55 | Temperatur | Max. Wert überschritten | 1 Bit | K, L, Ü |
| 56 | Temperatur | Min. Wert unterschritten | 1 Bit | K, L, Ü |
| 57 | Temperatur | Max. Temperaturwert auslesen | 2 Byte | K, L, Ü |
| 58 | Temperatur | Min. Temperaturwert auslesen | 2 Byte | K, L, Ü |
| 59 | Temperatur | Min/Max-Werte-Speicher zurücksetzen | 1 Bit | K, S |
| 60 | Temperatur | Fehler externer Sensor | 1 Bit | K, L, Ü |

Objekt 53 sendet den aktuellen (ggf. mit dem Abgleichwert korrigierten und/oder mit einem externen Sensor gemischten) Temperaturmesswert. Wird zusätzlich ein externer Sensor über Objekt 54 eingebunden, berechnet das Gerät je nach eingestellter Gewichtung einen Mischwert aus internem und externem Messwert, der dann über Objekt 53 ausgegeben wird. Fällt der externe Sensor länger als 30 Minuten aus, meldet Objekt 60 einen Fehler und das Gerät fällt automatisch auf den internen Sensor (100 %) zurück. Die Objekte 57–59 dienen dem Auslesen und Zurücksetzen von Minimal-/Maximalwerten, sofern diese Funktion aktiviert ist. Objekte 55/56 lösen eine 1-Bit-Meldung aus, sobald ein parametrierter oberer bzw. unterer Grenzwert über-/unterschritten wird (jeweils mit automatischer Rücknahme der Meldung).

### Relative Luftfeuchtigkeit

| Nr. | Name | Funktion | DPT/Größe | Flags |
|---|---|---|---|---|
| 61 | Relative Luftfeuchtigkeit | Messwert senden | 2 Byte | K, L, Ü |
| 62 | Relative Luftfeuchtigkeit | Externer Feuchtesensor (Messwert empfangen) | 2 Byte | K, S, Ü, A |
| 63 | Relative Luftfeuchtigkeit | Max. Wert überschritten | 1 Bit | K, L, Ü |
| 64 | Relative Luftfeuchtigkeit | Min. Wert unterschritten | 1 Bit | K, L, Ü |
| 65 | Relative Luftfeuchtigkeit | Max. relative Feuchte auslesen | 2 Byte | K, L, Ü |
| 66 | Relative Luftfeuchtigkeit | Min. relative Feuchte auslesen | 2 Byte | K, L, Ü |
| 67 | Relative Luftfeuchtigkeit | Min/Max-Werte-Speicher zurücksetzen | 1 Bit | K, S |
| 68 | Relative Luftfeuchtigkeit | Fehler externer Sensor | 1 Bit | K, L, Ü |

Funktional identisch zur Temperaturmessung: Objekt 61 sendet den (ggf. gemischten) relativen Feuchtewert, Objekt 62 nimmt einen externen Feuchtemesswert entgegen, Objekt 68 meldet einen Ausfall des externen Sensors (Überwachungszeit ebenfalls 30 Minuten, danach Rückfall auf internen Sensor). Min/Max-Auslesung und Grenzwertmeldungen funktionieren analog zur Temperatur.

### Absolute Luftfeuchtigkeit

| Nr. | Name | Funktion | DPT/Größe | Flags |
|---|---|---|---|---|
| 69 | Absolute Luftfeuchtigkeit | Messwert senden (g/m³) | 2 Byte | K, L, Ü |

Die absolute Feuchte gibt an, wie viel Wasser (in g/m³) tatsächlich in der Luft enthalten ist, und wird aus Temperatur und relativer Feuchte berechnet. Es gibt hierfür keinen externen Sensoreingang, da der Wert vollständig aus den beiden anderen Messgrößen abgeleitet wird.

### Taupunkttemperatur

| Nr. | Name | Funktion | DPT/Größe | Flags |
|---|---|---|---|---|
| 70 | Taupunkttemperatur | Messwert senden | 2 Byte | K, L, Ü |
| 71 | Taupunkttemperatur | Vergleichswert empfangen | 2 Byte | K, S |
| 72 | Taupunkttemperatur | Alarm senden | 1 Bit | K, L, Ü |

Die Taupunkttemperatur wird aus der absoluten Feuchte berechnet und zeigt an, ab welcher Oberflächentemperatur mit Kondensatbildung zu rechnen ist. Über Objekt 71 kann ein externer Vergleichswert (z. B. die Temperatur einer Kühl-/Fensteroberfläche) eingespeist werden; unterschreitet die Differenz zur Taupunkttemperatur den parametrierten Schwellwert, sendet Objekt 72 einen Taupunktalarm (z. B. zur Ansteuerung einer externen Kühl-/Lüftungslogik, da dieses Gerät selbst keinen Regler enthält).

### Behaglichkeit

| Nr. | Name | Funktion | DPT/Größe | Flags |
|---|---|---|---|---|
| 73 | Behaglichkeit | Status senden | 1 Bit* | K, L, Ü |

*Hinweis: In der Objekt-Übersichtstabelle des Handbuchs ist die Größe mit "1 Bit" angegeben, im Detailkapitel mit "2 Byte" – im PDF nicht eindeutig konsistent dokumentiert.

Das Behaglichkeits-Objekt vergleicht den aktuellen Temperatur- und Feuchtewert gegen zwei parametrierbare "Wohlfühlbereiche" (Min/Max Temperatur, Min/Max rel. Feuchte). Liegt mindestens einer der beiden Messwerte außerhalb seines Bereichs, wird eine "1" gesendet (z. B. zur Ansteuerung einer Komfort-Warnung), andernfalls eine "0".

### Allgemeine Objekte

| Nr. | Name | Funktion | DPT/Größe | Flags |
|---|---|---|---|---|
| 105 | In Betrieb | zyklisches Lebenszeichen-Telegramm | 1 Bit | K, L, Ü |
| 106 | Tag/Nacht | Empfang Tag/Nacht-Status | 1 Bit | K, S, Ü, A |

Objekt 105 kann zyklisch ein "In Betrieb"-Telegramm senden (Watchdog-Funktion). Objekt 106 nimmt einen extern vorgegebenen Tag/Nacht-Status entgegen (z. B. von einer Zeitschaltuhr); da dieses Gerät keinen Regler besitzt, hat diese Information hier lediglich informativen Charakter bzw. kann von nachgelagerten Logikbausteinen genutzt werden.

## ETS-Parameter

### Allgemeine Einstellungen

| Parameter | Werte | Standard |
|---|---|---|
| Geräteanlaufzeit | 2–240 s | 2 s |
| "In Betrieb" zyklisch senden | nicht aktiv, 1 min–24 h | nicht aktiv |
| Wert für Tag/Nacht | (nur beim Objektregler sichtbar) | – |
| Verhalten bei Busspannungswiederkehr – Tag/Nacht-Objekt | nicht abfragen / abfragen | abfragen |
| Sprache | (nur beim Objektregler sichtbar) | – |
| Reaktionszeit bei Tastendruck / Zeit langer Tastendruck | (nur beim Objektregler sichtbar, da keine Binäreingänge) | – |

Die Geräteanlaufzeit definiert die Wartezeit zwischen Busspannungswiederkehr und dem funktionalen Start des Sensors. Parameter, die sich auf Tasten, Sprache oder Betriebsart-Umschaltung des Reglers beziehen, sind beim reinen Feuchtesensor ausgeblendet, da diese Funktionen (Display-Diagnosetext, Tastenentprellung) nur beim Objektregler existieren.

### Temperaturmessung

| Parameter | Werte | Standard |
|---|---|---|
| Messwert senden bei Änderung | nicht aktiv / aktiv | aktiv |
| Messwert senden bei Änderung von | 0,1–2 K | 0,1 K |
| Messwert zyklisch senden | nicht senden, 1–60 min | 5 min |
| Min/Max Werte | nicht aktiv / aktiv | nicht aktiv |
| Meldungen | nicht aktiv / aktiv | nicht aktiv |
| Oberer Meldewert | 20–45 °C | 28 °C |
| Unterer Meldewert | 3–30 °C | 18 °C |
| Abgleichwert für internen Sensor | -5 bis +5 K | 0 K |
| Sensor intern/extern | 100 % intern … 100 % extern (10 %-Schritte) | 100 % intern |

"Messwert senden bei Änderung" bestimmt, ab welcher Temperaturdifferenz ein neuer Wert gesendet wird; "Messwert zyklisch senden" sorgt unabhängig davon für ein regelmäßiges Update, auch ohne Wertänderung. Der Abgleichwert dient zur Kompensation eines ungünstigen Einbauorts (z. B. Zugluft- oder Wärmequellennähe) durch Anheben/Absenken des gemessenen Werts. Über "Sensor intern/extern" lässt sich ein zweiter (externer) Fühler einbinden und gewichtet mit dem internen Wert mischen; bei 100 % intern bleibt der externe Sensor deaktiviert und die zugehörigen Objekte werden ausgeblendet.

### Relative Luftfeuchtigkeit

| Parameter | Werte | Standard |
|---|---|---|
| Messwert senden bei Änderung | nicht aktiv / aktiv | aktiv |
| Messwert senden bei Änderung von | 1–10 % | 1 % |
| Messwert zyklisch senden | nicht senden, 1–60 min | 5 min |
| Min/Max Werte | nicht aktiv / aktiv | nicht aktiv |
| Meldungen | nicht aktiv / aktiv | nicht aktiv |
| Oberer Meldewert | 25–100 % | 70 % |
| Unterer Meldewert | 0–75 % | 30 % |
| Abgleichwert für internen Sensor | -20 bis +20 % | 0 % |
| Sensor intern/extern | 100 % intern … 100 % extern (10 %-Schritte) | 100 % intern |

Aufbau und Wirkungsweise entsprechen exakt der Temperaturmessung (Sendebedingungen, Kalibrierung, Mischung mit externem Sensor), lediglich mit Werten in Prozent statt Kelvin.

### Absolute Luftfeuchtigkeit

| Parameter | Werte | Standard |
|---|---|---|
| Messwert senden bei Änderung | nicht aktiv / aktiv | aktiv |
| Messwert senden bei Änderung von | 1–10 % | 1 % |
| Messwert zyklisch senden | nicht senden, 1–60 min | 5 min |

Für die absolute Feuchte gibt es keine Kalibrierungs- oder Min/Max-Parameter, da der Wert rein rechnerisch aus Temperatur und relativer Feuchte abgeleitet wird.

### Taupunkttemperatur

| Parameter | Werte | Standard |
|---|---|---|
| Taupunkttemperatur | nicht aktiv / aktiv | aktiv |
| Messwert senden bei Änderung | nicht aktiv / aktiv | nicht aktiv |
| Messwert senden bei Änderung von | 1–10 K | 1 K |
| Messwert zyklisch senden | nicht senden, 1–60 min | 5 min |
| Taupunktalarm | nicht aktiv / aktiv mit Objekt-Vergleichswert | aktiv mit Objekt Vergleichswert |
| Alarm wenn Differenz kleiner gleich | 0–10 K | 2 K |

Der Taupunktalarm wird ausgelöst, sobald die Differenz zwischen dem über Objekt 71 empfangenen Vergleichswert (z. B. Oberflächentemperatur eines Fensters oder Kühlelements) und der berechneten Taupunkttemperatur den eingestellten Schwellwert unterschreitet – ein Hinweis auf drohende Kondensatbildung.

### Behaglichkeit

| Parameter | Werte | Standard |
|---|---|---|
| Objekt Behaglichkeit | nicht aktiv / aktiv | aktiv |
| Min. Temperatur | 10–45 °C | 18 °C |
| Max. Temperatur | 10–45 °C | 26 °C |
| Min. rel. Luftfeuchtigkeit | 0–100 % | 30 % |
| Max. rel. Luftfeuchtigkeit | 0–100 % | 70 % |
| Wert zyklisch senden | nicht aktiv, 1–60 min | nicht aktiv |

Über die vier Grenzwerte wird ein "Komfortfenster" für Temperatur und Feuchte definiert. Verlässt einer der beiden Messwerte diesen Bereich, meldet das Behaglichkeits-Objekt "1" (außerhalb) bzw. "0" (innerhalb).

## Inbetriebnahme / Hinweise

- Nach dem Verdrahten wird zunächst die physikalische Adresse über die Programmiertaste (Geräterückseite, LED-Anzeige) geladen, anschließend die Applikation mit der gewünschten Parametrierung.
- Messwerte benötigen nach Erstinstallation/Neuprogrammierung ca. 30 Minuten, bis sie sich stabilisiert haben – Kalibrierungen oder Plausibilitätsprüfungen sollten erst danach vorgenommen werden.
- Der externe Sensor-Eingang (Temperatur und/oder Feuchte) wird nach 30 Minuten Inaktivität als fehlerhaft erkannt; das Gerät schaltet dann automatisch auf 100 % internen Sensor um und meldet dies über die jeweiligen Fehlerobjekte (60 bzw. 68).
- Da dieses Gerät (SCN-TFS63.01) ausschließlich Messfunktionen besitzt, sind alle Objekte/Parameter zu Temperaturregler, Lüftungssteuerung und Binäreingängen aus dem gemeinsamen Handbuch **nicht relevant** und wurden hier bewusst weggelassen. Für eine Regelfunktion muss ein separater Regler-Kanal (z. B. Objektregler SCN-RTRxxO.01 oder ein anderer KNX-Temperaturregler) die hier gesendeten Mess-Objekte auswerten.
- Detaillierte mechanische/elektrische Spezifikationen (Messtoleranzen, Abmessungen) sind laut vorliegendem technischem Handbuch nicht enthalten und müssen dem separaten Datenblatt entnommen werden.

## Quelle

MDT Technisches Handbuch – Objektregler 55/63 (SCN-RTRxxO.01) / Temperatur-/Feuchtesensor 55/63 (SCN-TFSxx.01), Stand 06/2020, Version V1.0.
Datei: `originals/KNX/MDT_THB_SCN_01_Objektregler_Raumtemperatur_FeuchteSensor_V10.pdf`