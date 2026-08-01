---
title: MDT Präsenzmelder 360°-Serie
device_type: Präsenzmelder
manufacturer: MDT
article_number: [SCN-P360K4.03, SCN-P360L2.03, SCN-P360D1.01]
bus: KNX TP
source_pdf:
  - originals/KNX/MDT_TM_SCN-x360xx-03_V17_DE.pdf
  - originals/KNX/MDT_THB_Praesenzmelder_1_fach_01.pdf
last_updated: 2026-07-25
synonyms: [Bewegungsmelder, Präsenzsensor, Anwesenheitsmelder]
tags: [knx, praesenzmelder, mdt]
---

## Varianten

| Artikelnummer | Ausführung | Sensoren | Quelle |
|---|---|---|---|
| SCN-P360K4.03 | 360°, KLR (Konstantlichtregelung) | 4 | MDT_TM_SCN-x360xx-03_V17_DE.pdf |
| SCN-P360L2.03 | 360°, IP44, für abgehängte Decken | 2 | MDT_TM_SCN-x360xx-03_V17_DE.pdf |
| SCN-P360D1.01 | Mini, Deckeneinbau (Schalterdose) | 1 (Pyro-Detektor) | MDT_THB_Praesenzmelder_1_fach_01.pdf |

## Übersicht

Alle drei Varianten sind Deckenpräsenzmelder, die über passive Infrarotsensoren Bewegung/Anwesenheit erfassen und diese mit einer gemessenen Raumhelligkeit verknüpfen, um Licht bzw. eine HLK-Funktion (Heizung/Lüftung/Klima) bedarfsabhängig zu schalten. Grundprinzip bei allen Geräten: Solange Präsenz erkannt wird und die eingestellte Helligkeitsschwelle unterschritten ist, bleibt der Ausgang aktiv; nach der letzten Bewegungserkennung läuft eine parametrierbare Nachlaufzeit ab, bevor abgeschaltet wird.

**SCN-P360K4.03** ist das umfangreichste Modell: 4 Sensoren erlauben bis zu 4 unabhängige Lichtkanäle, zusätzlich HLK- und Alarm/Meldekanal, LED-Konfiguration, Szenen, Logikfunktionen sowie eine Konstantlichtregelung (KLR), die bis zu drei Lichtbänder (Wand/Mitte/Fenster) proportional so ansteuert, dass die Raumhelligkeit trotz wechselnden Sonnenlichteinfalls konstant bleibt.

**SCN-P360L2.03** basiert auf derselben Gerätegeneration/Applikation wie das K4.03, besitzt jedoch nur 2 Sensoren (max. 2 Lichtkanäle) und keine Konstantlichtregelung. Bauartbedingt (Montage in abgehängte Decken) ist es zusätzlich in Schutzart IP44 ausgeführt; die Programmiertaste wird hier per beiliegendem Magnet an einem Reedkontakt ausgelöst statt über eine klassische Taste.

**SCN-P360D1.01** ist ein älteres, funktional reduziertes Gerät mit nur einem Sensor und genau einer festen Lichtgruppe plus HLK-Kanal. Es besitzt weder Alarm/Meldekanal, noch Szenen-, Logik- oder LED-Konfigurationsmenü, noch Konstantlichtregelung. Die Helligkeitskalibrierung erfolgt über ein einfaches Teach-In-Verfahren mit festem Korrekturwert und Reflexionsfaktor.

## Technische Daten

| Merkmal | SCN-P360K4.03 | SCN-P360L2.03 | SCN-P360D1.01 |
|---|---|---|---|
| Anzahl Sensoren | 4 | 2 | 1 (Pyro-Detektor) |
| Montagehöhe | 2–4 m | 2–4 m | 2–4 m |
| Erfassungsbereich Präsenz (max.) | 8 m | 5 m | 3–4 m |
| Erfassungsbereich Bewegung/Reichweite (max.) | 16 m | 9 m | 5 m |
| Montageart | Deckenmontage, Schalterdose | Montage in abgehängte Decke | Deckenmontage, Schalterdose |
| Schutzart | nicht im Datenblatt spezifiziert | IP44 | nicht im Datenblatt spezifiziert |
| Max. Lichtkanäle | 4 | 2 | 1 (feste Lichtgruppe) |
| HLK-Kanal | ja | ja | ja |
| Alarm/Meldekanal | ja | ja | nein |
| Konstantlichtregelung (KLR) | ja (bis zu 3 Lichtbänder) | nein | nein |
| Temperaturmessung | nicht verfügbar (laut Quelle nur bei MR16-, L3-TS- und Glas-Ausführungen) | nicht verfügbar (s. o.) | nicht im Datenblatt spezifiziert |
| LED-Konfigurationsmenü (grün/rot/weiß) | ja | ja | nur Programmier-LED erwähnt, kein eigenes Konfigurationsmenü |
| Szenenfunktion | bis zu 8 Szenen | bis zu 8 Szenen | nicht verfügbar |
| Logikfunktion | bis zu 4 Logiken | bis zu 4 Logiken | nicht verfügbar |
| Master/Slave-Betrieb | ja | ja | ja |

## Kommunikationsobjekte

Die Objektnummerierung unterscheidet sich zwischen der Gerätegeneration K4.03/L2.03 (Applikation V4.4, Objekt-Templates mit Blockgröße +15 je zusätzlichem Lichtkanal, HLK ab Nr. 60, Alarm ab Nr. 75) und dem älteren D1.01 (fortlaufende, feste Nummerierung 0–29 für die eine Lichtgruppe, HLK, Tag/Nacht, Helligkeit und Teach-In).

### Lichtkanal (Ausgang, Eingänge, Status)

| Nr. (K4.03/L2.03) | Nr. (D1.01) | Name | Funktion | DPT | Gilt für |
|---|---|---|---|---|---|
| 0 | 0 | Lichtkanal/-gruppe 1 – Ausgang 1 | Schalten | 1 Bit | alle |
| 0 | 0 | Lichtkanal/-gruppe 1 – Ausgang 1 | Dimmen absolut | 1 Byte | alle |
| 0 | 0 | Lichtkanal/-gruppe 1 – Ausgang 1 | Szene | 1 Byte | alle |
| 1 | 1 | Lichtkanal/-gruppe 1 – Ausgang 1 (Nacht) | Schalten | 1 Bit | alle |
| 2 | – | Lichtkanal 1 – Ausgang 2 (Zusatz) | Schalten | 1 Bit | K4.03, L2.03 |
| 3 | 2 | Externer Taster kurz / Externer Eingang | Schalten | 1 Bit | alle |
| 4 | – | Externer Taster lang | Schalten | 1 Bit | K4.03, L2.03 |
| 5 | 3 | Externe Bewegung (Slave) | Schalten | 1 Bit | alle |
| 6 | – | Status Aktorkanal | Schalten | 1 Bit | K4.03, L2.03 |
| 7 | – | Bewegungserkennung sperren | Schalten | 1 Bit | K4.03, L2.03 |
| 8 | 4 | Zwangsführung | 2 Bit | 2 Bit | alle |
| 8 | 5 | Sperrobjekt | Schalten | 1 Bit | alle |
| 9 | 6 | Sperrobjekt EIN | Schalten | 1 Bit | alle |
| 10 | – | Status Automatikbetrieb / Sperre-Handbetrieb | Schalten | 1 Bit | K4.03, L2.03 |
| 11 | – | Dunkel schalten | Schalten | 1 Bit | K4.03, L2.03 |
| 12 | – | Dimmwert für EIN einlernen | Wert | 1 Byte | K4.03, L2.03 |
| 13 | – | Nachlaufzeit 10–65000 s | Wert | 2 Byte | K4.03, L2.03 |
| +15 je weiterer Kanal | – | nächster Lichtkanal | – | – | K4.03 (bis Kanal 4), L2.03 (bis Kanal 2) |

Der Ausgang liefert je nach eingestelltem Objekttyp entweder ein Schalt-, ein absolutes Dimm- oder ein Szenentelegramm; bei den neueren Geräten kann zusätzlich ein separates Ausgangsobjekt für den Nachtbetrieb sowie ein zweites, reines Schaltobjekt (Ausgang 2, z. B. für eine Status-LED) aktiviert werden. „Externer Taster kurz/lang“ (K4.03/L2.03) bzw. der einfache „Externe Eingang“ (D1.01) dienen dazu, den Kanal unabhängig von einer erkannten Bewegung manuell zu schalten bzw. in den Handbetrieb zu versetzen. „Externe Bewegung (Slave)“ nimmt im Master/Slave-Verbund die Meldung weiterer Melder entgegen. Zwangsführungs- bzw. Sperrobjekt erlauben eine externe Übersteuerung des Kanals (fest EIN/AUS/verriegelt), unabhängig von Präsenz und Helligkeit. Die Statusobjekte (Nr. 10 bzw. implizit über LED bei D1.01) melden, ob sich der Kanal im Automatik- oder im Hand-/Sperrbetrieb befindet.

### HLK-Kanal

| Nr. (K4.03/L2.03) | Nr. (D1.01) | Name | Funktion | DPT | Gilt für |
|---|---|---|---|---|---|
| 60 | 7 | HLK – Ausgang 1 | Schalten / Wert senden / Szene | 1 Bit / 1 Byte | alle |
| 63 | 9 | HLK – Externer Taster kurz / Externer Eingang | Schalten | 1 Bit | alle |
| 64 | – | HLK – Externer Taster lang | Schalten | 1 Bit | K4.03, L2.03 |
| 65 | 10 | HLK – Externe Bewegung | Schalten | 1 Bit | alle |
| 66 | – | HLK – Status Aktorkanal | Schalten | 1 Bit | K4.03, L2.03 |
| 67 | – | HLK – Bewegungserkennung sperren | Schalten | 1 Bit | K4.03, L2.03 |
| 68 | 11 | HLK – Zwangsführung | 2 Bit | 2 Bit | alle |
| 68 | 12 | HLK – Sperrobjekt | Schalten | 1 Bit | alle |
| 69 | 13 | HLK – Sperrobjekt EIN | Schalten | 1 Bit | alle |
| 70 | – | HLK – Status Automatikbetrieb / Sperre-Handbetrieb | Schalten | 1 Bit | K4.03, L2.03 |
| 72 | – | HLK – Dimmwert für EIN einlernen | Wert | 1 Byte | K4.03, L2.03 |
| 73 | – | HLK – Nachlaufzeit 10–65000 s | Wert | 2 Byte | K4.03, L2.03 |

Der HLK-Kanal ist funktional die Schnittstelle des Präsenzmelders zu anderen Gewerken (z. B. Lüftung, Heizung, Klima) und dient primär dazu, Anwesenheit im Raum an andere Systeme zu melden. Er ist immer nur mit einem einzigen Ausgangsobjekt für Tag/Nacht kombiniert (kein separates Nachtobjekt wie beim Lichtkanal). Anders als der Lichtkanal kann der HLK-Kanal über sogenannte Beobachtungszeitfenster arbeiten, wodurch das Einschalten erst nach mehrfacher Bewegungsdetektion innerhalb definierter Zeitabschnitte erfolgt – dies reduziert Fehlauslösungen und macht den Kanal robuster für träge Folgeprozesse wie Lüftungssteuerung.

### Alarm/Meldekanal (nur K4.03, L2.03)

| Nr. | Name | Funktion | DPT |
|---|---|---|---|
| 75 | Alarm – Ausgang (gemeinsam) | Schalten | 1 Bit |
| 76 | Alarm – Ausgang (Tag) | Schalten | 1 Bit |
| 76 | Alarm – Ausgang (Nacht) | Schalten | 1 Bit |
| 83 | Alarm – Eingang Sperren | Schalten | 1 Bit |
| 83 | Alarm – Eingang Freigeben | Schalten | 1 Bit |

Der Alarm/Meldekanal dient der Überwachung eines Raums bei Abwesenheit: Er ist grundsätzlich helligkeitsunabhängig und löst bei erkannter Bewegung aus, wenn er zuvor über ein Freigabe- bzw. Sperrobjekt aktiviert wurde. Er verfügt über eigene, von den Lichtkanälen unabhängige Empfindlichkeitseinstellungen sowie eigene Beobachtungszeitfenster zur Vermeidung von Fehlauslösungen (z. B. durch Zugluft). Bei D1.01 existiert diese Funktion nicht.

### Allgemein: Tag/Nacht, In-Betrieb, Präsenz

| Nr. (K4.03/L2.03) | Nr. (D1.01) | Name | Funktion | DPT | Gilt für |
|---|---|---|---|---|---|
| 90 | 14 | Tag/Nacht | Umschalten Tag/Nacht | 1 Bit | alle |
| 95 | 29 | In Betrieb | zyklisches Statustelegramm | 1 Bit | alle |
| – | 15 | Präsenz | Meldung erkannter Anwesenheit | 1 Bit | D1.01 |

Das Tag/Nacht-Objekt schaltet zwischen zwei Parametersätzen um (z. B. unterschiedliche Nachlaufzeiten oder Helligkeitsschwellen für Tag/Nacht) und kann optional nach Busspannungswiederkehr aktiv abgefragt werden. Das „In Betrieb“-Objekt sendet zyklisch ein Lebenszeichen, mit dem sich über eine Visualisierung oder einen Server prüfen lässt, ob der Melder noch am Bus aktiv ist. Bei D1.01 gibt es zusätzlich ein eigenständiges „Präsenz“-Objekt, das unabhängig vom eigentlichen Lichtkanal meldet, ob im Raum Bewegung erkannt wurde (z. B. nutzbar für eine einfache Alarmfunktion, da D1.01 keinen dedizierten Alarmkanal besitzt).

### LED (nur K4.03, L2.03)

| Nr. | Name | Funktion | DPT |
|---|---|---|---|
| 91 | LED Grün – Schalten | nur bei „aktiv über externes Objekt“ | 1 Bit |
| 92 | LED Rot – Blinken | Ansteuerung der roten LED | 1 Bit |
| 93 | LED Weiß – Schalten | nur bei „aktiv über externes Objekt“ (Nachtlicht) | 1 Bit |

Diese Objekte erlauben es, das Leuchtverhalten der eingebauten grünen, roten und weißen LED (Nachtlicht) extern zu steuern, statt sie nur automatisch (z. B. bei Bewegungserkennung oder nachts) leuchten zu lassen. Bei aktiver weißer LED (Nachtlicht) wird laut Hersteller der gemessene Helligkeitswert nicht mehr ausgewertet. D1.01 besitzt kein eigenes LED-Objektmenü.

### Szene (nur K4.03, L2.03)

| Nr. | Name | Funktion | DPT |
|---|---|---|---|
| 94 | Szene – Eingang | Aufruf einer Szene | 1 Byte |

Über gesendete Szenennummern lassen sich vordefinierte Aktionen für die Lichtkanäle auslösen (z. B. Sperre aktivieren/deaktivieren, externen Tastereingang simulieren, Tag/Nacht umschalten). Aktionen können nur für tatsächlich aktivierte Lichtkanäle konfiguriert werden.

### Helligkeit

| Nr. (K4.03/L2.03) | Nr. (D1.01) | Name | Funktion | DPT | Gilt für |
|---|---|---|---|---|---|
| 96 | 16 | Helligkeit – Schwellwertschalter | Schalten bei Über-/Unterschreitung | 1 Bit | alle |
| 97 | 17 | Helligkeit – Messwert | gemessener Helligkeitswert | 2 Byte | alle |
| 98 | – | Helligkeit – Einschaltschwelle für Lichtkanäle einstellen | Wert | 2 Byte | K4.03, L2.03 |
| 99 | 18 | Eingang Teach-in – Kalibrierung starten | Wert | 1 Bit | alle |
| 100 | – | Eingang Teach-in – Status absoluter Dimmwert | Wert | 1 Byte | K4.03 (nur bei aktiver KLR) |

Der Melder sendet den gemessenen Helligkeitswert (in Lux) sowie einen 1-Bit-Schwellwertschalter, der bei Über-/Unterschreitung eines parametrierten Grenzwerts (mit Hysterese) auslöst. Über Objekt 98 (nur K4.03/L2.03) lässt sich die im Parameter hinterlegte Einschaltschwelle zur Laufzeit per Bustelegramm verändern; betroffen ist dabei immer der gerade aktive Betrieb (Tag oder Nacht). Das Teach-In-Objekt startet eine Kalibrierung der internen Helligkeitsmessung anhand eines extern (z. B. per Luxmeter) ermittelten Referenzwerts; Objekt 100 wird zusätzlich benötigt, wenn die Konstantlichtregelung aktiv ist, da dort auch der zugehörige Dimmwert des Aktors eingelernt werden muss.

### Logik (nur K4.03, L2.03)

| Nr. | Name | Funktion | DPT |
|---|---|---|---|
| 110–113 | Logik 1 – Eingang C–F | externe Logikeingänge | 1 Bit |
| 114 | Logik 1 – Ausgang 1 | Ergebnis der Logikverknüpfung | 1 Bit / 2 Bit / 1 Byte |
| +5 je weiterer Logik | nächste Logik (bis zu 4 Logiken) | – | – |

Jede der bis zu vier Logikfunktionen verknüpft bis zu zwei interne und bis zu vier externe 1-Bit-Objekte über UND/ODER/XOR und gibt das Ergebnis wahlweise als Schalt-, Szenen-, Wert- oder 2-Bit-Zwangsführungstelegramm aus. D1.01 besitzt keine Logikfunktion.

### Konstantlicht (nur K4.03)

| Nr. | Name | Funktion | DPT |
|---|---|---|---|
| 130 | Konstantlicht – Schalten Ein/Aus | Aktivierung/Deaktivierung der Regelung | 1 Bit |
| 131 | Konstantlicht – Dimmen relativ | manuelles Verstellen des Sollwerts | 4 Bit |
| 132 | Konstantlicht – Dimmen absolut | Sollwert direkt setzen | 1 Byte |
| 134 | Konstantlicht – Sperre | Regelung sperren | 1 Bit |
| 135 | Konstantlicht – Szenen steuern | Szenenaufruf für die KLR | 1 Bit |
| 136 | Konstantlicht – Dimmen absolut Ausgang (Mitte) | Ansteuerung Lichtband Mitte | 1 Byte |
| 137 | Konstantlicht – Dimmen absolut Wandseite | Ansteuerung Lichtband Wand | 1 Byte |
| 138 | Konstantlicht – Dimmen absolut Fensterseite | Ansteuerung Lichtband Fenster | 1 Byte |
| 139 | Konstantlicht – Status | aktueller Betriebszustand | 1 Bit |

Diese Objekte steuern die Master/Slave-Konstantlichtregelung: Ein Soll-Helligkeitswert wird intern proportional auf bis zu drei getrennte Ausgangsobjekte (Wand-, Mitte-, Fensterband) verteilt, sodass äußere Störeinflüsse wie Sonnenlicht ausgeglichen werden. Nur SCN-P360K4.03 verfügt über diese Funktion; L2.03 und D1.01 besitzen keine Konstantlichtregelung.

## ETS-Parameter

### Allgemeine Einstellungen

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| In Betrieb zyklisch senden | nicht aktiv / 1 min – 24 h (K4.03, L2.03); nicht senden / 2 min – 24 h (D1.01) | nicht aktiv | alle |
| Tag/Nacht Objekt verwenden | nicht aktiv / aktiv, nicht abfragen / abfragen nach Reset | abfragen nach Reset | alle |
| Polarität Tag/Nacht | Tag=0/Nacht=1 oder Tag=1/Nacht=0 | Tag=1/Nacht=0 | alle |
| Tag/Nacht umschalten | bei nächster Präsenz / direkt bei Umschaltung | bei nächster Präsenz | K4.03, L2.03 |
| Auslöseempfindlichkeit Tag/Nacht | 1–8 | Tag 6 / Nacht 3 | K4.03, L2.03 |
| Präsenzempfindlichkeit | 1–10 | 8 | K4.03, L2.03 |
| Empfindlichkeit reduzieren für einzelne Sensoren | nicht aktiv / je nach Sensoranzahl wählbar | nicht aktiv | K4.03, L2.03 |
| Einschaltschwelle Tag/Nacht (Lux) | 5–1000 Lux | 400 Lux | K4.03, L2.03 |
| Ausschalten bei Überschreiten | nicht aktiv / aktiv, 75–1000 Lux | nicht aktiv / 800 Lux | K4.03, L2.03 |
| Meldefunktion Präsenz | aus / bei Tag / bei Nacht / bei Tag und Nacht melden | aus | D1.01 |
| Rückfallzeit Zwangsführung | nicht aktiv / nach Präsenz+Nachlaufzeit / nach fester Zeit | nach Situation | alle |
| Rückfall externer Taster lang (Hand→Auto) | nicht verwenden / nach Präsenz+Nachlaufzeit / nach fester Zeit | nach Präsenz und Nachlaufzeit | K4.03, L2.03 |

Diese globalen Einstellungen legen die Grundverhaltensweise des Geräts fest, bevor die einzelnen Kanäle separat konfiguriert werden. Über das Tag/Nacht-Objekt lässt sich der Melder zwischen zwei kompletten Parametersätzen umschalten (z. B. andere Nachlaufzeiten oder Empfindlichkeiten bei Nacht). Die Empfindlichkeitsparameter beeinflussen den effektiven Erfassungsbereich: niedrigere Werte erkennen Bewegung erst näher am Melder, höhere Werte bereits in größerer Entfernung. Die Rückfallzeit-Parameter definieren, ob und wie ein per Zwangsführung oder Handtaster übersteuerter Zustand automatisch wieder in den Automatikbetrieb zurückfällt.

### Lichtkanal/HLK – Grundeinstellungen

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Aktive Sensoren | Kombination aus vorhandenen Sensoren (z. B. "1--" bis "1234") | alle aktiv | alle |
| Betriebsart des Kanals | Vollautomat / Halbautomat | Vollautomat | alle |
| Nachlaufzeit Tag/Nacht | 1 s – 4 h (K4.03/L2.03); 1 s – 4 h (D1.01) | Tag 3 min / Nacht 30 s | alle |
| Verkürzung der Nachlaufzeit (Kurzzeit-Präsenz) | nicht aktiv / aktiv, mit Zeitfenster 10–30 s und eigener Nachlaufzeit | nicht aktiv | K4.03, L2.03 |
| Bewegungsfilter bei Bereitschaft | nicht aktiv / aktiv | nicht aktiv | K4.03, L2.03 |
| Helligkeit je Kanal | Grundeinstellung / helligkeitsunabhängig | Grundeinstellung | alle |
| Sensoraktivierung unterhalb (Lux) | 0–2000 Lux | 400 Lux | D1.01 |
| Abschaltung bei (Lux) | nicht verwenden / 10–2000 Lux | nicht verwenden | D1.01 |
| Beobachtungszeitfenster (nur HLK): Anzahl / Länge | 1–30 Fenster, 0–30000 (K4.03/L2.03); 0–32 Fenster, 0–3000 s (D1.01) | 3 Fenster / 30 s | alle (nur HLK-Kanal) |

Die Betriebsart bestimmt, ob der Kanal jede erkannte Bewegung selbstständig einschaltet (Vollautomat) oder erst nach zusätzlichem manuellem Tastendruck aktiv wird (Halbautomat). Die Nachlaufzeit legt fest, wie lange der Ausgang nach der letzten erkannten Bewegung noch eingeschaltet bleibt; jede neue Bewegung setzt sie zurück. Beobachtungszeitfenster (nur HLK-Kanal) verlangen mehrfache Detektionen über mehrere Zeitabschnitte hinweg, bevor geschaltet wird – dies verhindert unnötig kurzes Ein-/Ausschalten bei trägen Folgesystemen. Die Aktiv-Sensoren-Auswahl erlaubt eine räumliche Eingrenzung des Erfassungsbereichs, z. B. wenn nur ein Teilbereich eines Flurs überwacht werden soll.

### Zwangsführung/Sperrobjekt

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Zwangsführungsobjekt oder Sperrobjekt | Zwangsführungsobjekt (2 Bit) / Sperrobjekt / Sperrobjekt + Sperrobjekt EIN | Zwangsführungsobjekt | alle |
| Aktion beim Sperren (nur bei Sperrobjekt) | Bewegung sperren (verriegeln) / schaltet EIN / schaltet AUS | Bewegung sperren | K4.03, L2.03 |
| Rückfall Zwangsführung/Sperre nutzen | nicht aktiv / aktiv | je nach Kanal | K4.03, L2.03 |

Zwangsführung erlaubt eine bedingungslose Übersteuerung des Ausgangs (EIN, AUS oder zurück in Automatik), wobei die normale Bewegungsauswertung währenddessen unterbunden ist. Das alternative Sperrobjekt friert den aktuellen Zustand ein oder erzwingt einen festen Zustand, bis die Sperre wieder aufgehoben wird; ein optionales zweites Sperrobjekt kann den Kanal zusätzlich dauerhaft einschalten.

### Ausgangsobjekte (Schalten/Dimmen absolut/Szene) und Sendebedingungen

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Objekttyp für Ausgang | Schalten / Dimmen absolut / Szene | Schalten | alle |
| Ausgangsobjekte für Tag/Nacht | ein gemeinsames Objekt / getrennte Objekte | getrennte Objekte / gemeinsam, je Gerät | alle |
| Dimmwert bei Tag/Nacht für EIN/AUS | 0–100 % | Tag 100/0 %, Nacht 100/0 % (D1.01); je Kanal einstellbar (K4.03/L2.03) | alle |
| Orientierungslicht zum Verlassen | sofort ausschalten / anderer Dimmwert mit Ausschaltverzögerung | sofort ausschalten | K4.03, L2.03 (nur bei Dimmen absolut) |
| Ausgangsobjekt sendet | nur EIN / nur AUS / EIN und AUS | EIN und AUS | alle |
| Ausgangsobjekt sendet zyklisch | nicht aktiv / Intervall (Sekunden bis Minuten) | nicht aktiv | alle |

Der Objekttyp bestimmt, welches Telegramm der Kanal beim Ein-/Ausschalten sendet. Bei „Dimmen absolut“ lassen sich getrennte Dimmwerte für Tag/Nacht sowie ein optionales Orientierungslicht definieren, das nach Ablauf der Nachlaufzeit statt eines sofortigen Abschaltens kurzzeitig auf eine reduzierte Helligkeit dimmt, um das sichere Verlassen des Raums zu erleichtern. Die Sendebedingung filtert, welche der beiden Zustände (EIN/AUS) überhaupt auf den Bus gesendet werden, das zyklische Senden wiederholt den zuletzt gültigen Wert in festen Abständen zur Überwachung durch andere Busteilnehmer.

### Externer Taster kurz/lang und Totzeit

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Externer Taster kurz/lang reagiert auf | EIN und AUS / nur EIN / nur AUS / Umschalten bei Telegrammeingang | EIN und AUS | K4.03, L2.03 |
| Verhalten bei aktivem Nachtlicht (Taster kurz) | schaltet auf Taglicht / bleibt bei Nachtlicht | bleibt bei Nachtlicht | K4.03, L2.03 |
| Totzeit nach externer Taster kurz AUS | 1–30 s | 5 s | K4.03, L2.03 |
| Totzeit nach Ausschalten (allgemein) | 0–60 s | 1 s | K4.03, L2.03 |

„Externer Taster kurz“ dient dem manuellen Umschalten bzw. Einschalten des Kanals (z. B. im Halbautomat-Modus), „Externer Taster lang“ schaltet dauerhaft in den Handbetrieb. D1.01 kennt stattdessen nur einen einfachen „Externen Eingang“ ohne kurz/lang-Unterscheidung. Die Totzeit sperrt den Kanal nach dem Ausschalten für eine definierte Zeit gegen erneute Bewegungsauslösung, damit ein Verlassen des Raums nicht sofort wieder ein Wiedereinschalten bewirkt.

### Statusinformation

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Statusinformation (Lichtkanal/HLK) | nicht aktiv / sendet 1 bei Automatikbetrieb / sendet 1 bei Sperre/Handbetrieb | nicht aktiv | K4.03, L2.03 |

Aktiviert ein 1-Bit-Objekt, das dem Bus mitteilt, ob sich der Kanal aktuell im Automatik- oder im übersteuerten Hand-/Sperrzustand befindet, z. B. zur Visualisierung.

### Master-Slave-Betrieb (Licht- und HLK/Alarm-Kanäle)

| Parameter (empfohlene Slave-Einstellung) | Wert | Gilt für |
|---|---|---|
| Helligkeit | helligkeitsunabhängig | alle |
| Betriebsart | Vollautomat | alle |
| Nachlaufzeit Slave | deutlich kürzer als Master (z. B. 1 min) | alle |
| Objekttyp Ausgang | Schalten, sendet nur EIN | alle |
| Zyklisches Senden EIN | ca. 30 s | alle |

In größeren Räumen mit mehreren Meldern wird ein Gerät als Master parametriert (normale Voll-/Halbautomat-Einstellung, Nachlaufzeit 3–5 min empfohlen), während beliebig viele weitere Melder als Slave fungieren: Sie schalten helligkeitsunabhängig, senden bei Bewegung zyklisch ein EIN-Telegramm an das „Externe Bewegung (Slave)“-Objekt des Masters und geben so ihre Präsenzinformation an diesen weiter, der zentral über Schaltverhalten und Nachlaufzeit entscheidet. Bei D1.01 heißt das entsprechende Master-Objekt „Externe Bewegung – Lichtgruppe 1“. Für HLK/Alarm gilt dasselbe Prinzip, jedoch ohne Helligkeitsparameter; zu beachten ist, dass sich die Nachlaufzeiten von Master und Slave in der Gesamtwirkung addieren können, solange der Slave noch aktiv sendet.

### Alarm/Meldekanal (nur K4.03, L2.03)

| Parameter | Werte | Standard |
|---|---|---|
| Auslöseempfindlichkeit Tag/Nacht | 1–6 | Tag 3 / Nacht 2 |
| Präsenzempfindlichkeit | 1–8 | 6 |
| Stör-/Bewegungsfilter | nicht aktiv / aktiv mit Beobachtungszeitfenstern (Länge 1–5 s, Anzahl 2–5) | nicht aktiv |
| Nachlaufzeit Tag/Nacht | 1 s – 4 h | 3 min |
| Sperrobjekt oder Freigabeobjekt | Sperrobjekt / Freigabeobjekt | Sperrobjekt |
| Ausgangsobjekte für Tag/Nacht | ein gemeinsames Objekt / getrennte Objekte | gemeinsames Objekt |
| Ausgangsobjekt sendet zyklisch | nicht aktiv / 10 s – 60 min | nicht aktiv |

Der Alarmkanal arbeitet unabhängig von der Helligkeit und dient primär der Überwachung eines Raums bei Abwesenheit. Der optionale Stör-/Bewegungsfilter verlangt mehrere Detektionen über aufeinanderfolgende kurze Zeitfenster, um Fehlauslösungen (z. B. durch Zugluft) zu vermeiden, wodurch sich die effektive Reaktionszeit entsprechend verlängert. Über Sperr- bzw. Freigabeobjekt lässt sich die Überwachung ein- und ausschalten.

### LED (nur K4.03, L2.03)

| Parameter | Werte | Standard |
|---|---|---|
| LED grün | nicht aktiv / aktiv bei Bewegung / aktiv bei Bewegung nur tagsüber / aktiv über externes Objekt (ggf. blinkend) | aktiv bei Bewegung |
| LED weiß (Nachtlicht) | nicht aktiv / nachts aktiv bei Bewegung je Lichtkanal / nachts über externes Objekt / nachts immer aktiv | nicht aktiv |
| Helligkeit bei Nacht (LED weiß) | 0–100 % | 10 % |
| Handbetrieb/Sperre EIN/AUS mit LED grün/rot anzeigen (Lichtkanal 1) | nicht aktiv / aktiv | nicht aktiv |

Die grüne LED signalisiert normalerweise erkannte Bewegung, kann aber auch komplett deaktiviert oder extern (z. B. für andere Statusanzeigen) angesteuert werden. Die weiße LED dient als einstellbares Nachtlicht; bei aktivem Nachtlicht wird laut Hersteller die Helligkeitsmessung des Melders nicht mehr berücksichtigt. Zusätzlich kann für Lichtkanal 1 angezeigt werden, ob sich der Kanal im Hand- oder Sperrbetrieb befindet.

### Szenen (nur K4.03, L2.03)

| Parameter | Werte | Standard |
|---|---|---|
| Szene A–H Nummer | 1–64 / nicht aktiv | nicht aktiv |
| Aktion je Lichtkanal bei Szenenaufruf | nicht aktiv / Sperre aktiv (ein/aus/verriegeln) / Sperre deaktivieren / externen Taster simulieren / Tag/Nacht setzen | nicht aktiv |

Bis zu acht Szenen können per 1-Byte-Telegramm aufgerufen werden und lösen dabei je konfiguriertem Lichtkanal eine definierte Aktion aus (z. B. Sperre setzen, Handbetrieb simulieren, Tag/Nacht-Zustand erzwingen). Es lassen sich nur Aktionen für tatsächlich aktivierte Lichtkanäle konfigurieren.

### Helligkeit

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Lichtkanäle beeinflussen Helligkeitsmessung | ja (mehrere Lichtquellen im Raum) / nein (separate Funktionen) | ja | K4.03, L2.03 |
| Helligkeit senden bei Änderung von | nicht senden / 5–50 % (K4.03/L2.03); 20–1800 Lux (D1.01) | 10 % / 50 Lux | alle |
| Messwert zyklisch senden | nicht verwenden / 5 s – 30 min (K4.03/L2.03); 5 s – 30 min (D1.01) | nicht verwenden | alle |
| Korrektur Luxwert | -50 % bis 70 % (K4.03/L2.03); -100 bis 100 Lux (D1.01) | 0 % / 0 Lux | alle |
| Raum-Reflexionsfaktor | 0,2–1 (K4.03/L2.03); feste Auswahl 0,2–1 (D1.01) | 0,4 | alle |
| Schwellwertschalter aktiv | nicht aktiv / aktiv | aktiv (D1.01) / nicht aktiv (K4.03/L2.03) | alle |
| Schwellwertschalter schaltet bei | 5–1000 Lux (K4.03/L2.03); 60–1000 Lux (D1.01) | 300 Lux | alle |
| Hysterese des Schwellwertschalters | 5–200 Lux | 30 Lux | alle |

Über den Reflexionsfaktor wird der gemessene Helligkeitswert rechnerisch auf die Arbeitsplatzhöhe umgerechnet, da der Sensor an der Decke typischerweise weniger Licht misst als am Boden reflektiert wird; Richtwerte reichen von ca. 0,25 (dunkle/reflexionsarme Böden) bis ca. 0,7 (helle Wände/Decken). Der Korrekturwert verschiebt den gemessenen Wert zusätzlich um einen festen Betrag bzw. Prozentsatz. Der Schwellwertschalter sendet ein 1-Bit-Telegramm bei Über-/Unterschreiten eines Grenzwerts; die Hysterese sorgt dafür, dass Ein- und Ausschaltpunkt auseinanderliegen, um häufiges Umschalten bei schwankender Helligkeit zu vermeiden. Der Parameter „Lichtkanäle beeinflussen die Helligkeitsmessung“ (nur K4.03/L2.03) legt fest, ob beim Einschalten eines Kanals die übrigen Kanäle automatisch helligkeitsunabhängig werden, um ein gegenseitiges Verhindern des Einschaltens durch das eigene Kunstlicht zu vermeiden.

### Kalibrierung Helligkeitswert / Teach-In

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Luxwert für Teach-In | 200–1000 Lux (K4.03/L2.03); 200–1000 Lux (D1.01, im Text als 200–100 vertippt) | 450 Lux | alle |
| Teach-In-Wert beim Laden der Applikation | Teach-In-Wert halten / Werkseinstellung bzw. Default-Wert laden | Werkseinstellung/Default laden | alle |

Beim Teach-In wird mit einem externen Luxmeter ein Referenzwert ermittelt und über das Kalibrierungsobjekt eingelesen; der Melder gleicht daraufhin seine interne Helligkeitsmessung mit diesem Referenzwert ab, was die Genauigkeit gegenüber der reinen Parametrierung erhöht. Bei aktiver Konstantlichtregelung (nur K4.03) lernt das Teach-In zusätzlich den zur Zielhelligkeit gehörenden Dimmwert des angeschlossenen Aktors ein und sollte grundsätzlich bei verdunkeltem Raum bzw. in der Dämmerung durchgeführt werden, da Tages-/Sonnenlicht die Messung verfälscht.

### Konstantlicht (nur K4.03)

| Parameter | Werte | Standard |
|---|---|---|
| Konstantlichtregler | nicht aktiv / aktiv | nicht aktiv |
| Sonnenlicht ausregeln | normal / wenig / sehr wenig | normal |
| Auswahl Lichtbänder | 1 Lichtband / Mitte+Wand / Mitte+Fenster / Mitte+Wand+Fenster | Mitte+Wand+Fenster |
| Einfluss proportionale Zonenregelung Wand | kein Einfluss (x1) bis sehr stark (x2) | mittel (x1,6) |
| Einfluss proportionale Zonenregelung Fenster | kein Einfluss (x1) bis sehr stark (x0,5) | mittel (x0,7) |
| Konstantlicht schalten mit | externem Objekt / Präsenz Lichtkanal 1 | Präsenz Lichtkanal 1 |
| Regler schaltet Licht aus | nicht aktiv / aktiv | aktiv |
| Minimaler/Maximaler Dimmwert am Dimmausgang | 0–50 % / 50–100 % | 0 % / 100 % |
| Einschaltwert Tag/Nacht | Parameter (fester Dimmwert) / Teach-In-Wert / Einschaltwert berechnen | Parameter |
| Standby/Orientierungslicht | nicht verwenden / verwenden (Sollwert 5–100 %, Zeit 5 s–60 min) | nicht verwenden |
| Sperrobjekt aktiv | nein / ja, mit einstellbarem Verhalten bei Wert 0/1 | nein |
| Szenen für KLR | nicht aktiv / aktiv, bis zu 8 Sollwerte 25–750 Lux | nicht aktiv |

Die Konstantlichtregelung hält die Raumhelligkeit über eine proportionale Master/Slave-Logik konstant, indem sie bis zu drei Lichtbänder (Wand, Mitte, Fenster) unterschiedlich stark dimmt: Bei zunehmendem Sonnenlichteinfall wird zuerst die fensterseitige Beleuchtung stärker heruntergeregelt als die wandseitige, sodass die Gesamthelligkeit im Raum ausgeglichen bleibt. Die Regelfaktoren je Zone bestimmen, wie stark sich die Dimmwerte der einzelnen Bänder bei gleicher Zielhelligkeit voneinander unterscheiden dürfen; ein Faktor von 1 (kein Einfluss) lässt alle Bänder gleich hell leuchten. Der Parameter „Sonnenlicht ausregeln“ dämpft die Regelaggressivität, falls der Melder bei Sonneneinstrahlung zu stark herunterregelt. Diese Funktion ist ausschließlich beim SCN-P360K4.03 verfügbar.

### Logik (nur K4.03, L2.03)

| Parameter | Werte | Standard |
|---|---|---|
| Logikfunktion 1–4 aktivieren | nicht aktiv / aktiv | nicht aktiv |
| Funktion | UND / ODER / XOR | UND |
| Ausgangsobjekt | Schalten / Szene / Wert / Zwangsführung 2 Bit | Schalten |
| Sendebedingung | bei Eingangstelegramm / bei Änderung Ausgang / nur 0 oder 1 senden bei Änderung/Eingang | bei Änderung Ausgang |
| Interner Eingang A/B | nicht aktiv / normal / invertiert, Objektnummer 0–99 | nicht aktiv |
| Externer Eingang C–F | nicht aktiv / normal / invertiert | nicht aktiv |
| Logikeingang nach Reset vorbelegen mit | Wert 0 / Wert 1 | Wert 0 |

Jede der bis zu vier Logikfunktionen verknüpft interne (geräteeigene) und externe (per Bus empfangene) 1-Bit-Signale über eine wählbare logische Funktion und gibt das Ergebnis als Schalt-, Szenen-, Wert- oder Zwangsführungstelegramm aus. Über die Sendebedingung lässt sich steuern, ob nur bei tatsächlicher Änderung des Ergebnisses oder bei jedem eingehenden Eingangstelegramm gesendet wird. D1.01 bietet keine Logikfunktion.

## Inbetriebnahme / Hinweise

Bei allen Varianten erfolgt die Inbetriebnahme in der üblichen KNX-Reihenfolge: Busanschluss herstellen, Busspannung zuschalten, Programmiertaste betätigen (rote Programmier-LED leuchtet), physikalische Adresse aus der ETS laden, anschließend die Applikation mit gewünschter Parametrierung übertragen. Beim SCN-P360L2.03 wird der Programmiermodus abweichend nicht über eine mechanische Taste, sondern durch Halten eines mitgelieferten Magneten an einen Reedkontakt aktiviert.

Der Melder sollte möglichst mittig im Raum montiert werden. Für die Konstantlichtregelung (K4.03) ist zusätzlich ein Mindestabstand von 60 cm zur nächsten Leuchte einzuhalten, und der Melder sollte in der Achse der mittleren Leuchtengruppe positioniert werden, damit die Zonenzuordnung (Wand/Mitte/Fenster) korrekt funktioniert.

Die Empfindlichkeitseinstellungen (K4.03/L2.03: „Auslöseempfindlichkeit“ und „Präsenzempfindlichkeit“, D1.01: implizit über Helligkeits-/Sensorparameter) sowie die Auswahl der aktiven Sensoren erlauben eine Anpassung an bauliche Gegebenheiten – z. B. lässt sich in Fluren nur ein Teilbereich erfassen oder die Empfindlichkeit einzelner Sensorsegmente gezielt reduzieren, wenn diese z. B. auf angrenzende, nicht zu überwachende Bereiche gerichtet sind. Aufgrund der Linsenoptik überlappen sich die Erfassungsbereiche benachbarter Sensoren leicht, sodass keine scharfe Trennlinie zwischen den Bereichen existiert.

Für eine möglichst genaue Helligkeitsregelung empfiehlt der Hersteller in allen drei Handbüchern, einmalig ein Teach-In mit einem externen Luxmeter durchzuführen; bei aktivierter Konstantlichtregelung (K4.03) ist dies sogar Voraussetzung für ein zufriedenstellendes Regelverhalten. Das Teach-In sollte grundsätzlich bei verdunkeltem Raum bzw. während der Dämmerung erfolgen, da Tageslicht die Kalibrierung verfälscht.

Beim Aufbau mehrerer Melder im selben Raum (Master/Slave-Betrieb) ist zu beachten, dass sich Nachlaufzeiten von Master und Slave-Geräten in ihrer Gesamtwirkung addieren können, solange der Slave noch aktiv ein Bewegungssignal an den Master sendet.

## Quelle

- MDT technologies GmbH: *Technisches Handbuch – Präsenzmelder SCN-x360xx.03*, Stand 10/2023, Version 1.7 – `originals/KNX/MDT_TM_SCN-x360xx-03_V17_DE.pdf`
- MDT technologies GmbH: *Technisches Handbuch – MDT Präsenzmelder SCN-P360D1.01*, Stand 6/2019, Version 1.0 – `originals/KNX/MDT_THB_Praesenzmelder_1_fach_01.pdf`