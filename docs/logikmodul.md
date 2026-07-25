---
title: MDT Logikmodul SCN-LOG1.02
device_type: Logikmodul
manufacturer: MDT
article_number: [SCN-LOG1.02]
bus: KNX TP
source_pdf: originals/KNX/MDT_TM_SCN-LOG1-02_V10_DE.pdf
last_updated: 2026-07-25
synonyms: [Logikbaustein, KNX-Logik, Verknüpfungsmodul]
tags: [knx, logikmodul, mdt]
---

## Übersicht

Das MDT Logikmodul SCN-LOG1.02 ist ein KNX-TP-Reiheneinbaugerät (2TE) mit 24 unabhängig
parametrierbaren Funktionsblöcken ("F1" bis "F24"). Jeder dieser 24 Blöcke kann in der ETS
mit genau einer von 17 Hauptfunktionen belegt werden – die Blöcke sind gleich aufgebaut und
lassen sich beliebig und unabhängig voneinander konfigurieren. Zusätzlich besitzt das Gerät
einen internen Zeit-/Datumsserver (für Empfang von Uhrzeit/Datum über den Bus, Berechnung von
Sonnenauf-/-untergang und Dämmerung) sowie 4 frei belegbare Status-LEDs auf der Frontseite.

Verfügbare Hauptfunktionen je Funktionsblock:
- **Universal-Logik** – WENN/DANN/SONST-Verknüpfung verschiedenster Datenpunkttypen (nicht nur boolesch)
- **Logikgatter / Inverter** – UND/ODER/EXKLUSIV-ODER-Verknüpfung von bis zu 8 Eingängen bzw. 4-fach-Inverter
- **Nach Reset senden/abfragen** – Objekt nach Busspannungswiederkehr abfragen oder mit Wert vorbelegen
- **Wert speichern und nach Reset senden** – letzten empfangenen Wert speichern und nach Busausfall wiederherstellen
- **Zyklisch senden/abfragen** – Werte zyklisch senden oder abfragen (z. B. Nachrüstung fehlenden zyklischen Sendens)
- **Telegrammüberwachung** – Ausbleiben eines erwarteten Telegramms erkennen und Störmeldung senden
- **Szenensteuerung / Steuertabelle** – bis zu 7 Bit-Eingänge zu bis zu 8 Bedingungen/Ausgangswerten verknüpfen
- **Multiplexer / Trennwand** – Datenaustausch zwischen zwei Objekten schaltbar ein-/auskoppeln
- **Vervielfacher / Sequenzer** – ein Eingangsereignis löst bis zu 4 vordefinierte Ausgangswerte aus
- **Universal-Rechner** – zwei (plus ein verknüpfender dritter) Rechenblöcke für +, −, ×, ÷
- **Formatwandler** – Umwandlung zwischen verschiedenen Datenformaten (1 Bit bis 4 Byte, Text) in 22 Varianten
- **Filter / Begrenzer** – Werte filtern, auf zwei Objekte aufteilen oder auf Min/Max begrenzen
- **Temperatur-/Wertevergleicher** – Vergleich zweier Werte/Objekte mit Hysterese, optional 2. Vergleich UND/ODER
- **Min/Max/Mittelwert** – aus bis zu 4 Eingangswerten Minimum, Maximum oder Mittelwert bilden
- **Zeitfunktion** – Ein-/Ausschaltverzögerung, Treppenlicht, Wiedereinschalten nach Zeit
- **Nachlaufsteuerung mit Lüftungsstufe** – Ein-/Ausschaltverzögerung mit zusätzlicher Lüfterstufenanhebung
- **Umwandlung in PWM** – 1-Byte-Stellwert (0–100 %) in ein pulsweitenmoduliertes 1-Bit-Signal wandeln

Typische Einsatzszenarien sind komplexe Verknüpfungslogiken, die in einzelnen Aktoren/Sensoren
nicht abgebildet werden können: bedingte Beschattungssteuerung (Helligkeit UND Anwesenheit UND
Uhrzeitfenster), Nachlauf- und WC-Lüftungssteuerungen, Ersatz fehlender zyklischer Sendefunktionen
älterer Geräte, Formatanpassung zwischen Sensor- und Aktor-DPTs sowie Grenzwert-/Störmeldelogik.

## Technische Daten

| Merkmal | Wert |
|---|---|
| Artikelnummer | SCN-LOG1.02 |
| Bauform | Logikmodul, 2 TE, Reiheneinbaugerät (REG) |
| Busanschluss | KNX TP, über Busanschlussklemme |
| Anzahl Funktionsblöcke | 24, unabhängig konfigurierbar |
| Bedienelemente | 1× Programmiertaste, 1× Programmier-LED (rot), 4× frei belegbare Funktions-LEDs |
| Geräteanlaufzeit | 2 … 240 s (Standard 2 s) nach Busspannungswiederkehr |

Maße, Gewicht, Schutzart, zulässige Umgebungstemperatur, Leistungsaufnahme sowie weitere
mechanische/elektrische Kenndaten sind im vorliegenden technischen Handbuch **nicht
spezifiziert** (nicht im Datenblatt enthalten; ggf. separates Datenblatt heranziehen).

## Kommunikationsobjekte

Jeder der 24 Funktionsblöcke belegt einen Bereich von 10 Objektnummern (0–9), die Funktion des
nächsten Blocks (F2) beginnt entsprechend bei Nummer 10 usw. ("+10 nächste Funktion"). Welche
Objekte innerhalb dieses 10er-Blocks tatsächlich aktiv sind, hängt von der gewählten
Hauptfunktion ab. Die Flags K/L/S/Ü/A (Kommunikation, Lesen, Schreiben, Übertragen,
Aktualisieren) sind je Objekt anpassbar.

### Universal-Logik

| Nr. | Name | Funktion | DPT/Länge | Flags (Standard) |
|---|---|---|---|---|
| 0 | F1: | Eingang 1 | 1 Bit … 1 Byte | K,Ü,A |
| 1 | F1: | Eingang 1 – Vergleichswert | 2 Bit … 4 Byte | K,Ü,A |
| 2 | F1: | Eingang 2 | 2 Byte | K,Ü,A |
| 3 | F1: | Eingang 2 – Vergleichswert | 4 Byte | K,Ü,A |
| 4 | F1: | Eingang 3 | 1 Bit / 1 Byte | K,Ü,A |
| 5 | F1: | Eingang 4 | 1 Bit / 1 Byte | K,Ü,A |
| 6 | F1: | Eingang 5 | 1 Bit / 1 Byte | K,Ü,A |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |
| 9 | F1: | Ausgang | 1 Bit / 1 Byte | K,Ü |

Die fünf Bedingungseingänge nehmen je nach gewähltem Datenpunkttyp der Bedingung
unterschiedliche Formate an; für Bedingung 1 und 2 kann zusätzlich ein eigenes
Vergleichswert-Objekt aktiv sein. Der Ausgang sendet das Ergebnis der WENN/DANN/SONST-
Verknüpfung.

### Logikgatter / Inverter

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Logik-/Invertereingang 1 | 1 Bit | K,Ü,A |
| 1 | F1: | Logikeingang 2 / Inverterausgang 1 | 1 Bit | siehe unten |
| 2–7 | F1: | Logikeingänge 3–8 bzw. Invertereingänge/-ausgänge 2–4 | 1 Bit | – |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |
| 9 | F1: | Logikausgang | 1 Bit / 1 Byte | K,Ü |

Je nach gewählter Unterfunktion ("Logikgatter, 8 Eingänge mit Sperre" oder "Logikinverter, 4x
mit Sperre") sind die Objektnummern 0–7 entweder 8 Logikeingänge (Gatter) oder 4 Eingang-/
Ausgang-Paare (Inverter) belegt.

### Nach Reset senden/abfragen

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Nach Reset senden | 1 Bit … 1 Byte | K,S,Ü |
| 0 | F1: | Nach Reset abfragen | 2 Byte … 14 Byte | K,S,Ü |

Nur eines der beiden Objekte ist je nach Parametrierung ("senden" vs. "abfragen") sichtbar.

### Wert speichern und nach Reset senden

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Nach Reset senden | 1 Bit … 4 Byte | K,Ü,A |

Ein einzelnes Objekt, dessen DPT über den Parameter "Datenpunkttyp" festgelegt wird.

### Zyklisch senden/abfragen

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Wert zyklisch abfragen | 1 Bit … 1 Byte | K,A |
| 0 | F1: | Wert zyklisch senden | 2 Byte … 14 Byte | K,A |
| 7 | F1: | Abfrage Anforderung | 1 Bit | K,S |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |

Das Objekt "Abfrage Anforderung" löst bei Bedarf sofort eine zusätzliche Leseanfrage aus.

### Telegrammüberwachung

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Telegrammüberwachung Eingang | 1 Bit … 14 Byte | K,Ü,A |
| 4 | F1: | Telegrammüberwachung Meldung | 1 Bit … 14 Byte | K,Ü |

Bleibt am Eingangsobjekt innerhalb der eingestellten Überwachungszeit kein Telegramm aus, wird
über das Meldeobjekt eine Störmeldung (Wert, Szenennummer oder Klartext) gesendet.

### Szenensteuerung / Steuertabelle

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0–6 | F1: | Szenensteuerung Eingang 1–7 | 1 Bit | K,Ü,A |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |
| 9 | F1: | Logikausgang | 1 Bit / 1 Byte | K,Ü |

Die 7 Bit-Eingänge bilden zusammen eine 7-stellige Bitkombination, die gegen bis zu 8
parametrierte Bedingungsmuster (Steuertabelle) geprüft wird.

### Multiplexer / Trennwand

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Multiplexer Ein-/Ausgang 1 | 1 Bit … 2 Byte | K,L,S,Ü,A |
| 1–3 | F1: | Multiplexer Ein-/Ausgang 2–4 | 1 Bit … 2 Byte | K,L,S,Ü,A |
| 4 | F1: | Multiplexer Steuereingang | 1 Bit | K,S |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |

Objekt 3/4 (zweites Paar) ist nur aktiv, wenn "Betriebsart für Objekt 3 und 4" nicht auf
"nicht aktiv" steht.

### Vervielfacher / Sequenzer

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Sequenzer Eingang | 1 Bit / 1 Byte | K,Ü,A |
| 1–4 | F1: | Sequenzer Ausgang 1–4 | 1 Bit … 2 Byte | K,Ü |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |

Trifft am Eingang die parametrierte Bedingung (EIN/AUS bzw. Szenennummer) zu, werden bis zu 4
Ausgänge mit individuell vorbelegbaren Werten und eigenem DPT gesendet.

### Universal-Rechner

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0–3 | F1: | Eingang 1–4 | 1 Bit … 4 Byte | K,Ü,A |
| 4–6 | F1: | Ausgang 1–3 | 4 Byte | K,Ü |
| 7 | F1: | Impulseingang | 1 Bit | K,S |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |

Eingang 1/2 bilden Rechenblock 1 (Ausgang 1), Eingang 3/4 Rechenblock 2 (Ausgang 2); Ausgang 3
verknüpft die Ergebnisse aus Ausgang 1 und Ausgang 2 mit einer weiteren Operation.

### Formatwandler

Alle 22 Wandlungsvarianten teilen sich ein Sperr-/Freigabeobjekt (Nr. 8) und belegen darüber
hinaus je nach gewählter Umwandlung eine variable Anzahl an Ein- und Ausgangsobjekten (z. B.
1 Bit-Eingang + 1 Steuereingang + 1 Byte-Ausgang bei "1 Bit → 1 Byte"; bis zu 8 Bit-Ein-/
Ausgänge bei "8 x 1 Bit → 1 Byte"). Die genaue Objektbelegung jeder der 22 Varianten ist der
Quell-PDF (Kapitel 5.11.1–5.11.22, Tabellen 64–113) zu entnehmen; sie folgt jedoch durchgehend
dem Muster: Eingangsobjekt(e) im gewählten Quellformat, optionales Steuer-/Prioritätsobjekt,
Ausgangsobjekt(e) im gewählten Zielformat, plus Sperre/Freigabe.

Verfügbare Umwandlungsrichtungen: 1 Bit ↔ 1 Byte (0–255 / 0–100 %), 1 Bit → 2 Byte
(Temperatur/Gleitkomma), 1 Bit → 14 Byte Text, 2×1 Bit ↔ 2 Bit Zwang, 8×1 Bit ↔ 1 Byte
(bitcodiert/Stufenschalter/Prozent), 1 Byte invertieren, 2/3/4×1 Byte ↔ 2/3/4 Byte,
2 Byte Temperatur/Gleitkomma ↔ 1 Bit, 14 Byte Text ↔ Bit/Byte sowie eine "Universal"-Variante
für beliebige 1-Bit-bis-4-Byte-Kombinationen.

### Filter / Begrenzer

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Filter Eingang | 1 Bit … 4 Byte | K,Ü,A |
| 1 | F1: | Filter Steuereingang | 1 Bit | K,S |
| 4 | F1: | Filter Ausgang EIN / AUS / (Wert) | 1 Bit … 4 Byte | K,Ü |

Bei 1-Bit-DPT kann der Ausgang wahlweise nur "EIN"- oder nur "AUS"-Telegramme durchlassen oder
auf zwei getrennte Ausgangsobjekte aufteilen; bei numerischen DPTs wirkt stattdessen eine
Minimal-/Maximalwertbegrenzung.

### Temperatur-/Wertevergleicher

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Vergleicher Wert/Temperaturwert 1 Eingang | 1 Byte … 4 Byte / 2 Byte | K,Ü,A |
| 1 | F1: | Vergleicher Wert/Temperaturwert 2 Eingang | 1 Byte … 4 Byte / 2 Byte | K,Ü,A |
| 2 | F1: | Vergleicher Wert/Temperaturwert 3 Eingang | 1 Byte … 4 Byte / 2 Byte | K,Ü,A |
| 3 | F1: | Vergleicher Wert/Temperaturwert 4 Eingang | 1 Byte … 4 Byte / 2 Byte | K,Ü,A |
| 4 | F1: | Vergleicher Ausgang | 1 Bit | K,Ü |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |

Objekte 1–2 gehören zur ersten Vergleichsfunktion, Objekte 3–4 zur optionalen zweiten (UND/
ODER-verknüpften) Vergleichsfunktion.

### Min/Max/Mittelwert

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0–3 | F1: | Mindest-/Maximal-/Mittelwert Eingang 1–4 | 1 Byte … 4 Byte | K,Ü,A |
| 4 | F1: | Mindest-/Maximal-/Mittelwert Ausgang | wie Eingang | K,Ü |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |

Eingang 1 und 2 sind fest aktiv, Eingang 3 und 4 optional zuschaltbar. Welche der drei
Berechnungen (Minimum/Maximum/Mittelwert) durchgeführt wird, legt der Parameter
"Ausgangsberechnung" fest.

### Zeitfunktion

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Zeitfunktion Eingang | 1 Bit | K,Ü,A |
| 1 | F1: | Zeitfunktion Ausgang | 1 Bit / 1 Byte | K,Ü |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |

### Nachlaufsteuerung mit Lüftungsstufe

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | Nachlaufsteuerung Eingang | 1 Bit | K,Ü,A |
| 1 | F1: | Zeitfunktion Ausgang | 1 Bit / 1 Byte | K,Ü |
| 4 | F1: | Lüftung Eingang | 1 Byte | K,Ü,A |
| 5 | F1: | Lüftung Ausgang | 1 Byte | K,Ü |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |

"Lüftung Eingang" liefert den Grundwert (z. B. Grundstufe des Lüfters), "Lüftung Ausgang" den
tatsächlich ausgegebenen, temporär angehobenen Arbeitswert.

### Umwandlung in PWM

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 0 | F1: | PWM Eingang | 1 Byte | K,Ü,A |
| 1 | F1: | PWM Ausgang | 1 Bit | K,Ü |
| 8 | F1: | Sperre / Freigabe | 1 Bit | K,S |

### LED (geräteweit, nicht pro Funktionsblock)

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 240 | LED 1 | Schalten | 1 Bit | K,S |
| 241 | LED 2 | Schalten | 1 Bit | K,S |
| 242 | LED 3 | Schalten | 1 Bit | K,S |
| 243 | LED 4 | Schalten | 1 Bit | K,S |

### Allgemein (Zeit-/Datumsserver, geräteweit)

| Nr. | Name | Funktion | DPT/Länge | Flags |
|---|---|---|---|---|
| 244 | Datum / Uhrzeit | Empfangen | 8 Byte | K,S |
| 244 | Uhrzeit | Empfangen | 3 Byte | K,S |
| 245 | Datum | Empfangen | 3 Byte | K,S |
| 246 | Minutentakt | Ausgang | 1 Bit / 1 Byte | K,Ü |
| 247 | Stundentakt | Ausgang | 1 Bit / 1 Byte | K,Ü |
| 248 | Tagestakt | Ausgang | 1 Bit / 1 Byte | K,Ü |
| 249 | Sonnenaufgang | Ausgang | 1 Bit | K,Ü |
| 250 | Sonnenuntergang | Ausgang | 1 Bit | K,Ü |
| 251 | Abenddämmerung | Ausgang | 1 Bit | K,Ü |
| 252 | Sommer-/Winterzeit Umschalten | 1 Bit | K,Ü | zyklisch alle 60 min |
| 253 | Tag / Nacht | Ausgang | 1 Bit | K,Ü |
| 254 | In Betrieb | Status | 1 Bit | K,Ü |

Diese Objekte versorgen die zeitbasierten Bedingungen der Universal-Logik (DPT "Uhrzeit" /
"Wochentag") mit einer aktuellen Zeitbasis; dazu muss ein externer Zeitserver angebunden
werden.

## ETS-Parameter

### Allgemeine Einstellungen (geräteweit)

| Parameter | Werte | Standard |
|---|---|---|
| Geräteanlaufzeit | 2 … 240 s | 2 s |
| In Betrieb zyklisch senden | nicht aktiv / 1 min – 24 h | nicht aktiv |
| Zyklisches Senden während der Sperre | sperren / erlauben | – |
| Objekte für Datum und Uhrzeit | gemeinsames Objekt / getrennte Objekte | – |
| Zeitumstellung | keine / automatisch Sommer-/Winterzeit | – |
| Standortbestimmung durch | Koordinaten / Ort | – |
| Land / Stadt (bei "Ort") | frei wählbar | Deutschland / Engelskirchen |
| Breite / Länge in Grad und Minuten (bei "Koordinaten") | 0–90° / 0–180° | 50° 56′ N / 6° 57′ O |
| Zeitdifferenz zur Weltzeit (UTC+…) | beliebige Zeitzone | UTC+01:00 |
| Objekt für Sommer-/Winterzeit | nicht aktiv / Sommer=1 / Winter=1 | – |
| Objekt für Sonnenaufgang, Offset | nicht aktiv / sendet Wert 0 od. 1; −120…120 min | 0 min |
| Objekt für Abenddämmerung, Offset | nicht aktiv / sendet Wert 0 od. 1; −120…120 min | −30 min |
| Objekt für Sonnenuntergang, Offset | nicht aktiv / sendet Wert 0 od. 1; −120…120 min | 0 min |
| Objekt für Minuten-/Stundentakt | nicht aktiv / Wert 0 / Wert 1 / Bytewert | – |
| Objekt für Tagestakt | nicht aktiv / Wert 0 / Wert 1 / Bytewert | – |

Diese Parameter konfigurieren den internen Zeit-/Astroserver (Standort- bzw. Koordinaten­
berechnung von Sonnenauf-/-untergang und Dämmerung, Ausgabe von Zeittakten) sowie das
zyklische "In-Betrieb"-Telegramm. Sie wirken geräteweit und stellen die Zeitbasis für alle
Funktionsblöcke bereit, die Uhrzeit-/Datumsvergleiche verwenden (z. B. Universal-Logik).

### Identische Parameter (in jedem Funktionsblock vorhanden)

| Parameter | Werte | Standard |
|---|---|---|
| Beschreibung der Funktion | Text, bis 40 Zeichen | – |
| Zusatztext | Text, bis 40 Zeichen | – |
| Hauptfunktion | eine der 17 Hauptfunktionen / nicht aktiv | nicht aktiv |

"Beschreibung der Funktion" erscheint sowohl im ETS-Funktionsmenü als auch als Präfix bei den
zugehörigen Kommunikationsobjekten und dient rein der Übersichtlichkeit; "Zusatztext" ist nur
im Parametermenü selbst sichtbar.

### Universal-Logik

| Parameter | Werte | Standard |
|---|---|---|
| Text für Bedingung 1–5 | Text, bis 25 Zeichen | – |
| Auswahl Datenpunkttyp Eingang 1–5 | Bool / 2 Bit Priorität / Szenenummer / 1-4 Byte Werte / Uhrzeit / Wochentag (Bedingung 3–5 nur Teilmenge) | – |
| Bedingung 3–5 aktiv | nicht aktiv / aktiv | nicht aktiv |
| Bewertung (bei numerischen DPT) | gleich / ungleich / ≥ / > / ≤ / < / zwischen 2 Vergleichswerten | – |
| Vergleichswert über | Objekt / Parameter | – |
| Zweiten Eingang mit Wert belegen | nicht aktiv / aktiv | – |
| Auswahl DPT Ausgang | Bool / Szenenummer / Dezimalwert / Prozentwert | – |
| Wert wenn Ausgang Wahr/1, Falsch/0 | je nach Ausgangs-DPT | – |
| SONST aktiv | nicht aktiv / aktiv | – |

Bis zu 4 Bedingungen werden UND-verknüpft, das Ergebnis wird mit einer 5. Bedingung ODER-
verknüpft ("(B1 UND B2 UND B3 UND B4) ODER B5"). Für Bedingung 1 und 2 steht die volle
Palette an Datenpunkttypen zur Verfügung (inkl. Uhrzeit, Wochentag, alle numerischen DPTs),
für Bedingung 3–5 nur eine eingeschränkte Auswahl (Bool, Szenennummer, Dezimal-/
Prozentwert). Bei Uhrzeit-/Wochentag-Vergleichen muss das Objekt "Uhrzeit" bzw. "Datum" mit
einem Zeitserver verbunden sein; die Bewertung "zwischen 2 Vergleichswerten" ist dabei nur
für Bedingung 1 und 2 verfügbar. Trifft die Gesamtbedingung zu, wird der DANN-Wert gesendet;
ist "SONST" aktiviert, wird bei Nichterfüllung der SONST-Wert gesendet.

### Logikgatter / Inverter

| Parameter | Werte | Standard |
|---|---|---|
| Unterfunktion | Logikgatter (8 Eingänge, Sperre) / Logikinverter (4x, Sperre) | – |
| Logikfunktion (Gatter) | UND / ODER / EXKLUSIV-ODER | – |
| Eingang 1–8 aktiv, Polarität | nicht aktiv/aktiv; normal/invertiert | – |
| Objektauswahl | externes / internes Objekt | – |
| Ausgang Polarität | normal / invertiert | – |
| Objekttyp Ausgang | Ein/Aus / Szene / Wert 0-255 / Wert 0-100 % | – |
| Wert wenn Ausgang Wahr/1, Falsch/0 | je nach Objekttyp | – |
| Sperre/Freigabe, Ausgangswert bei Sperre | nicht aktiv / Sperre bei 1 / Freigabe bei 1; halten / auf Wert setzen | – |
| Sendebedingung | bei Änderung Ausgang / bei Eingangstelegramm | – |
| Sende bei Telegrammeingang auf | alle / Eingang x / individuell | – |
| Ausgang filtern | nicht aktiv / nur EIN / nur AUS | – |
| Sendeverzögerung / zyklisches Senden, Zeitbasis, Zeit | nicht aktiv/Sendeverzögerung/zyklisch; s/min/h; 0…240 | 10 |
| Eingänge nach Reset abfragen | nicht aktiv / aktiv | – |

Beim Logikgatter werden bis zu 8 Eingänge (jeder einzeln invertierbar, wahlweise mit
internem oder externem Objekt verknüpft) über UND/ODER/XOR verknüpft; das Ergebnis kann
ebenfalls invertiert werden. Der Logikinverter invertiert stattdessen bis zu 4 unabhängige
Objekte. Über "Sperre/Freigabe" kann bei aktivierter Sperre wahlweise der letzte Wert
gehalten oder ein fester Ersatzwert ausgegeben werden.

### Nach Reset senden/abfragen

| Parameter | Werte | Standard |
|---|---|---|
| Wert | nach Reset abfragen / nach Reset senden | – |
| Datenpunkttyp | Bool, 2 Bit, 4 Bit, Szenennummer, Dezimal-/Prozentwert, 2/4 Byte Werte, RGB, 14 Byte Text u. a. | – |
| Wert (nur bei "senden") | je nach DPT | – |
| Zeitbasis | Sekunde / Minute | – |
| Verzögerung nach Reset | 1 … 240 | 10 |

Nach einem Reset/Busausfall wird das Objekt zeitverzögert entweder gelesen ("abfragen") oder
mit einem vorgegebenen Wert beschrieben ("senden"). Die Verzögerung stellt sicher, dass
andere über dieselbe Gruppenadresse verbundene Geräte zu diesem Zeitpunkt bereits einen
definierten Zustand haben.

### Wert speichern und nach Reset senden

| Parameter | Werte | Standard |
|---|---|---|
| Datenpunkttyp | Bool, 2 Bit, Szenennummer, Dezimal-/Prozentwert, 2/4 Byte Werte, RGB u. a. | – |
| Zeitbasis | Sekunde / Minute | – |
| Sendeverzögerung nach Reset | 1 … 240 | 1 |

Der zuletzt empfangene Wert wird im Gerät nichtflüchtig gespeichert und nach
Busspannungswiederkehr verzögert erneut gesendet, sodass der Zustand vor dem Ausfall
wiederhergestellt wird.

### Zyklisch senden/abfragen

| Parameter | Werte | Standard |
|---|---|---|
| Wert | zyklisch abfragen / zyklisch senden | – |
| Datenpunkttyp | Bool, 2/4 Bit, Szenennummer, Dezimal-/Prozentwert, 2/4 Byte Werte, RGB, 14 Byte Text | – |
| Abfragen alle (bei "abfragen") | Sekunde/Minute/Stunde/nur über Objekt; 1…240 | 10 |
| Wert Auswahl (bei "senden") | fester Wert / empfangener Wert | – |
| Wert | je nach DPT-Bereich | – |
| Senden alle | Sekunde/Minute/Stunde; 0…240 | 10 |
| Sperre/Freigabe | nicht aktiv / Sperre bei 1 / Freigabe bei 1 | – |

Ergänzt Geräte ohne eigenes zyklisches Sendeverhalten: entweder wird ein Objekt in
festgelegtem Takt abgefragt (Lesetelegramm), oder ein fester bzw. der zuletzt empfangene Wert
wird zyklisch gesendet. Ein zusätzliches Objekt "Abfrage Anforderung" löst bei Bedarf eine
sofortige Zusatzabfrage aus.

### Telegrammüberwachung

| Parameter | Werte | Standard |
|---|---|---|
| Datenpunkttyp | Bool, 2 Bit, Szenennummer, Dezimal-/Prozentwert, 2/4 Byte Werte, RGB, 14 Byte Text | – |
| Gültiger Zustand für Überwachung (nur 1 Bit) | Ein oder Aus / nur Ein / nur Aus | – |
| Zeitbasis, Überwachungszeit | Sekunde/Minute/Stunde; 1…240 | 60 s / 60 min / 1 h |
| Einstellung DPT für Meldung | Bool, 2 Bit Priorität, Szenennummer, Dezimal-/Prozentwert, 14 Byte Text | – |
| Sende bei Ausfall (Wert/Priorität/Szene/Dezimal/Prozent/Text) | je nach gewähltem DPT | 0 / 1 / 0 % |
| Sende wenn O.K. nach Ausfall | nicht aktiv / aktiv | – |

Bleibt innerhalb der Überwachungszeit kein gültiges Telegramm am Eingang aus, wird über das
Meldeobjekt eine parametrierbare Störmeldung (bis hin zu Klartext, 14 Byte) gesendet; optional
kann bei Wiederkehr zusätzlich eine "O.K."-Bestätigung gesendet werden.

### Szenensteuerung / Steuertabelle

| Parameter | Werte | Standard |
|---|---|---|
| Bedingung 1–8 (7-stellige Ziffernfolge) | 0 / 1 / X (keine Auswertung) je Eingang 1–7 | – |
| Objekttyp Ausgang | Ein/Aus / Szene / Wert 0-255 / Wert 0-100 % | – |
| Ausgangswert wenn Wahr (je Bedingung) | je nach Objekttyp | 0 |
| Sperre/Freigabe, Ausgangswert bei Sperre | wie Logikgatter | – |
| Sendebedingung | bei Änderung Ausgang / bei Eingangstelegramm | – |
| Sende bei Telegrammeingang auf | alle / Eingang x / individuell | – |
| Sendeverzögerung / zyklisches Senden | nicht aktiv/Sendeverzögerung/zyklisch; 0…240 | 10 |
| Eingänge nach Reset abfragen | nicht aktiv / aktiv | – |
| Ausgang sendet erst wenn alle Eingänge gültig | nicht aktiv / aktiv / Eingänge nach Reset vorbelegen | – |

Jede der bis zu 8 Bedingungszeilen vergleicht die 7 Bit-Eingänge (Priorität von Eingang 1,
höchste, bis Eingang 7, niedrigste) gegen ein Muster aus "0", "1" oder "X" (nicht bewerten).
Passt die aktuelle Eingangskombination auf eine Zeile, wird der zugehörige Ausgangswert
gesendet. Sendezeitpunkt und Verzögerung/zyklische Wiederholung sind wie beim Logikgatter
konfigurierbar.

### Multiplexer / Trennwand

| Parameter | Werte | Standard |
|---|---|---|
| Betriebsart für Objekt 1 und 2 | Ein/Aus, 2 Bit Zwang, 4 Bit Dimmen, Dezimal-/Prozentwert, Gleitkomma, Szenennummer | – |
| Betriebsart für Objekt 3 und 4 | nicht aktiv / wie oben | nicht aktiv |
| Multiplexer bei Steuereingang = 0 / = 1 | Objekt A ǁ B / A⇒B / A⇐B / A⇔B (bzw. gemischt bei zwei Paaren) | – |
| Sperre/Freigabe | nicht aktiv / Sperre bei 1 / Freigabe bei 1 | – |

Über den Steuereingang wird umgeschaltet, ob zwei (bzw. zwei Paare von) Objekten unabhängig
("ǁ", Trennwand-Funktion), einseitig gekoppelt ("⇒"/"⇐") oder bidirektional synchronisiert
("⇔") sind. Bei "⇔" übernimmt jede Änderung an A den Wert auf B und umgekehrt; bei "⇒"/"⇐"
wirkt die Kopplung nur in einer Richtung.

### Vervielfacher / Sequenzer

| Parameter | Werte | Standard |
|---|---|---|
| Eingang Datenpunkttyp | Ein/Aus / Szenennummer | – |
| Gültige Szenennummer (bei Szenennummer) | 1–64 | 1 |
| Ausgang 1–4 aktiv/sendet | nicht aktiv / wenn Eingang Aus / Ein / Ein oder Aus | – |
| Datenpunkttyp je Ausgang | Ein/Aus, 2 Bit Priorität, Szenennummer, Dezimal-/Prozentwert, Temperaturwert | – |
| Wert/Szenennummer wenn Eingang AUS/EIN (je Ausgang, je DPT) | je nach DPT-Bereich | z. B. 0/255, 1/2, 0 %/100 % |

Beim Eintreffen des Eingangsereignisses (EIN/AUS-Wechsel oder passende Szenennummer) werden
bis zu 4 unabhängige Ausgangsobjekte mit individuell vorbelegten Werten und eigenem DPT
geschrieben – nützlich um z. B. aus einer Szene mehrere Aktorbefehle unterschiedlichen Formats
abzuleiten.

### Universal-Rechner

| Parameter | Werte | Standard |
|---|---|---|
| Eingang 1–4 | Objekt / fester Wert / fester Prozentwert | – |
| Operation Ausgang 1/2 | + / − / × / ÷ | – |
| Operation Ausgang 3 | Ausgang1 +/−/×/÷ Ausgang2 | – |
| Datenpunkttyp je Ausgang | Bool, Dezimal-/Prozentwert, 1-4 Byte Werte | – |
| Sperre/Freigabe | nicht aktiv / Sperre bei 1 / Freigabe bei 1 | – |
| Sendebedingung | bei Änderung Ausgang / bei Eingangstelegramm / nicht automatisch | – |
| Senden bei Impulseingang | alle Ausgänge bei AUS/EIN / Ausgang 1 bei Aus + 2 bei Ein / umgekehrt | – |
| Sendeverzögerung / zyklisches Senden, Zeitbasis, Zeit | nicht aktiv/Sendeverzögerung/zyklisch; s/min/h; 1…240 | 10 |
| Eingänge nach Reset abfragen, Ausgang sendet erst wenn gültig | nicht aktiv / aktiv | – |

Rechenblock 1 verknüpft Eingang 1 und 2, Rechenblock 2 Eingang 3 und 4 (wobei Ausgang 1 auch
als Eingang für Rechenblock 2 dienen kann); Rechenblock 3 verrechnet die Ergebnisse aus
Ausgang 1 und 2 erneut. Hinweis: Bei Prozentrechnung können durch das 1-Byte-Datenmodell
Rundungsfehler auftreten (z. B. 14 % + 7 % = 21,2 % statt 21 %), die Rückumwandlung erfolgt
kaufmännisch gerundet. Über das Objekt "Impulseingang" lässt sich das Senden der Ausgänge
gezielt bei AUS- bzw. EIN-Flanke triggern.

### Formatwandler

| Parameter | Werte | Standard |
|---|---|---|
| Funktion | eine von 22 Wandlungsvarianten (siehe Übersicht oben) | – |
| Sendebedingung | bei Änderung Ausgang / bei Eingangstelegramm | – |
| Sperre/Freigabe | nicht aktiv / Sperre bei 1 / Freigabe bei 1 | – |

Beispiel "1 Bit ⇒ 1 Byte Wert 0–255": einem 1-Bit-Eingang wird für Zustand "0" und Zustand "1"
je ein fester Byte-Wert (0–255) zugeordnet; über einen optionalen Steuereingang lässt sich
zwischen zwei Wertepaaren umschalten (4 parametrierbare Werte insgesamt). Die übrigen 21
Varianten folgen demselben Prinzip einer festen Zuordnungstabelle bzw. Bit-für-Bit-
Umschichtung zwischen den Formaten; ihre jeweils spezifischen Parameter (z. B. Schwellwerte
bei Analog-→Digital-Wandlungen, Bitreihenfolge bei Bitcodierungen) sind in den Unterkapiteln
5.11.1–5.11.22 der Quell-PDF im Detail beschrieben.

### Filter / Begrenzer

| Parameter | Werte | Standard |
|---|---|---|
| Datenpunkttyp | Bool, Szenennummer, Dezimal-/Prozentwert, 1-4 Byte Werte, 14 Byte Text | – |
| Filterfunktion (bei 1 Bit) | nur AUS durchlassen / nur EIN durchlassen / auf 2 Objekte aufteilen | – |
| Minimal-/Maximalwert (bei numerischen DPT) | je nach DPT-Bereich | DPT-Grenzen |
| Filterbedingung | filtern wenn Steuereingang=0 / =1 / immer filtern | – |
| Verhalten bei Über-/Unterschreitung | nur gültige Werte senden / Minimal-/Maximalwerte senden | – |
| Sendebedingung | bei Änderung Ausgang / bei Eingangstelegramm | – |
| Sperre/Freigabe | nicht aktiv / Sperre bei 1 / Freigabe bei 1 | – |

Bei 1-Bit-Werten wirkt die Funktion als reiner Durchlassfilter (nur EIN, nur AUS oder Aufteilung
auf zwei Objekte); bei numerischen Datenpunkttypen begrenzt sie den Wertebereich, wobei
außerhalb des zulässigen Bereichs liegende Werte entweder verworfen oder auf den Minimal-/
Maximalwert geklemmt werden. Bei DPTs wie 2 Bit Priorität, 4 Bit Dimmen, RGB oder 14 Byte Text
wird der Eingang ungefiltert durchgereicht; hier greift nur die Sperr-/Freigabefunktion.

### Temperatur-/Wertevergleicher

| Parameter | Werte | Standard |
|---|---|---|
| Unterfunktion | DPT 9.001 Temperaturwert / andere numerische DPTs | – |
| Funktion 1 Vergleiche | Wert1 </>/= Vergleichswert; Wert1 </>/= Wert2; Wert1−Wert2 </> Vergleichswert | – |
| Hysteresewert | 0,2…5 K (Temperatur) bzw. DPT-abhängig | 0,5 K |
| Vergleichswert | −50…600 °C bzw. DPT-Bereich | 0 °C |
| Funktion 2 | nicht aktiv / UND- / ODER-Verknüpfung mit Funktion 1 | nicht aktiv |
| Sendebedingung | bei Änderung Ausgang / bei Eingangstelegramm | – |
| Ausgang Invertieren | nicht aktiv / aktiv | – |
| Sperre/Freigabe | nicht aktiv / Sperre bei 1 / Freigabe bei 1 | – |
| Eingänge nach Reset abfragen | nicht aktiv / aktiv | – |

Der Hysteresewert wird hälftig unter- und oberhalb des Vergleichswerts angewendet, um ein
Schaltflattern am Schwellwert zu vermeiden (z. B. Vergleichswert 10, Hysterese 4 ⇒
Einschaltpunkt 8, Ausschaltpunkt 12). Optional kann ein zweiter, gleich aufgebauter Vergleich
UND- oder ODER-verknüpft werden, um z. B. zwei Temperaturfühler gemeinsam auszuwerten.

### Min/Max/Mittelwert

| Parameter | Werte | Standard |
|---|---|---|
| Datenpunkttyp | Dezimal-/Prozentwert, 1/2/4 Byte Werte | – |
| Eingang 3, Eingang 4 | nicht aktiv / aktiv | nicht aktiv |
| Ausgangsberechnung | Mindestwert / Maximalwert / Mittelwert | – |
| Sperre/Freigabe | nicht aktiv / Sperre bei 1 / Freigabe bei 1 | – |
| Sendebedingung | bei Änderung Ausgang / bei Eingangstelegramm | – |
| Sendeverzögerung / zyklisches Senden, Zeitbasis, Zeit | nicht aktiv/Sendeverzögerung/zyklisch; s/min/h; 0…240 | 10 |
| Eingänge nach Reset abfragen, Ausgang sendet erst wenn gültig | nicht aktiv / aktiv | – |

Eingang 1 und 2 sind immer aktiv, Eingang 3 und 4 optional zuschaltbar; aus den aktiven
Eingängen wird je nach Einstellung Minimum, Maximum oder arithmetischer Mittelwert gebildet
und über das Ausgangsobjekt gesendet.

### Zeitfunktion

| Parameter | Werte | Standard |
|---|---|---|
| Unterfunktion | Verzögerung / Treppenlicht / Wiedereinschalten nach Zeit | – |
| Funktion (bei Verzögerung) | Ein-/Ausschaltverzögerung / nur Ausschaltverzögerung / nur Einschaltverzögerung | – |
| Zeitbasis Ein-/Ausschalten, Verzögerung | s/min/h; 1…240 | Ein 10, Aus 1 |
| Zeit nachtriggerbar | nicht aktiv / aktiv | – |
| Bei Eingangswert=0 ausschalten (Treppenlicht) | nicht aktiv / aktiv | – |
| Bei Eingangswert=1 einschalten (Wiedereinschalten) | nicht aktiv / aktiv | – |
| Datenpunkttyp Ausgang | Ein/Aus / Szenennummer / Dezimal-/Prozentwert | – |
| Wert/Szenennummer wenn Eingang EIN/AUS | je nach DPT | – |
| Sperre/Freigabe | nicht aktiv / Sperre bei 1 / Freigabe bei 1 | – |

Drei Betriebsarten: (1) "Verzögerung" – nachtriggerbare Ein-, Aus- oder Ein-/Ausschalt­
verzögerung; (2) "Treppenlicht" – EIN-Signal schaltet den Ausgang, der nach Ablauf der Zeit
automatisch wieder abschaltet (vorzeitiges Abschalten über AUS-Signal am Eingang möglich);
(3) "Wiedereinschalten nach Zeit" – AUS-Signal schaltet sofort ab, nach Ablauf der Zeit schaltet
der Ausgang automatisch wieder ein (nachtriggerbar durch erneutes AUS-Signal).

### Nachlaufsteuerung mit Lüftungsstufe

| Parameter | Werte | Standard |
|---|---|---|
| Zeitbasis/Einschaltverzögerung, Zeitbasis/Ausschaltverzögerung | s/min/h; 1…240 | Ein 10, Aus 1 |
| Datenpunkttyp Ausgang | Ein/Aus / Szenennummer / Dezimal-/Prozentwert | – |
| Wert/Szenennummer wenn Eingang EIN/AUS | je nach DPT | – |
| Lüftungssteuerung | nicht aktiv / aktiv | – |
| Eingangswert (Lüftung) | Bytewert in Stufen / Wert in % | – |
| Erhöhung um (Stufen) | 1–3 Stufen | – |
| Maximalwert des Ausgangs (Stufen) | 3–8 | 8 |
| Erhöhung um (%) | 5–50 % | 20 % |
| Maximalwert des Ausgangs (%) | 50–100 % | 100 % |
| Sperre/Freigabe | nicht aktiv / Sperre bei 1 / Freigabe bei 1 | – |

Kombiniert eine Ein-/Ausschaltverzögerung mit einer zusätzlichen Anhebung eines Lüfter-
Stellwertes: Nach der Einschaltverzögerung schaltet der Ausgang und der Lüftungswert wird um
die eingestellte Stufenanzahl bzw. den Prozentsatz erhöht; nach der Ausschaltverzögerung wird
sowohl der Schaltausgang zurückgesetzt als auch die Lüftungsstufe wieder abgesenkt. Typisches
Beispiel: WC-Lüftung, die bei Nutzung von Stufe 30 % auf 50 % angehoben wird und nach Ablauf
der Nachlaufzeit auf 30 % zurückfällt.

### Umwandlung in PWM

| Parameter | Werte | Standard |
|---|---|---|
| Ausgang Invertieren | nein / ja | nein |
| Zeitbasis | Sekunde / Minute / Stunde | – |
| Zeit | 1…240 s | 10 s |
| Sperre/Freigabe | nicht aktiv / Sperre bei 1 / Freigabe bei 1 | – |

Aus dem 1-Byte-Stellwert (0–100 %) am Eingang wird über die eingestellte PWM-Zykluszeit ein
pulsweitenmoduliertes 1-Bit-Ausgangssignal berechnet (Verhältnis Einschalt- zu Ausschaltzeit
entspricht dem Prozentwert) – z. B. zur Ansteuerung einer Elektroheizung über einen
Schaltaktor.

### LED

| Parameter | Werte | Standard |
|---|---|---|
| LED 1–4 | nicht aktiv / über externes Objekt schalten / über internes Objekt schalten | nicht aktiv |
| Internes Objekt auswählen | 0…254 | 0 |
| Verhalten | Dauer / Blinken | – |
| Zustand | LED AN bei Wert=1 / LED AN bei Wert=0 (invertiert) | – |

Jede der 4 Front-LEDs kann unabhängig entweder direkt über ein eigenes Kommunikationsobjekt
(240–243) oder über den aktuellen Wert eines beliebigen internen Objekts einer anderen
Funktion angesteuert werden – nützlich zur Statusanzeige einer Logikfunktion direkt am Gerät.

## Inbetriebnahme / Hinweise

- **Inbetriebnahmeschritte**: Gerät nach Anschlussschema verdrahten → Busspannung zuschalten →
  Programmiertaste > 1 s drücken (rote Programmier-LED leuchtet dauerhaft) → physikalische
  Adresse in der ETS programmieren (LED erlischt) → Applikationsprogramm parametrieren und
  laden.
- **Objektnummerierung**: Da jeder Funktionsblock stets 10 Objektnummern belegt (F1 = 0–9,
  F2 = 10–19 usw.), verschieben sich bei einer Änderung der Hauptfunktion in einem Block auch
  die verwendeten Objektnummern und ggf. deren DPT – bestehende Gruppenadressenverknüpfungen
  sollten danach überprüft werden.
- **Auswertereihenfolge Universal-Logik**: Die Verknüpfung ist fest als "(B1 UND B2 UND B3 UND
  B4) ODER B5" definiert und nicht umstellbar; Bedingung 3–5 unterstützen nur eine
  eingeschränkte DPT-Auswahl gegenüber Bedingung 1/2.
- **Zeitbasierte Bedingungen** (Uhrzeit/Wochentag in der Universal-Logik, Astro-Funktionen)
  benötigen zwingend einen extern angebundenen Zeitserver auf dem Objekt "Uhrzeit" bzw.
  "Datum/Uhrzeit" – ohne aktuelle Zeitbasis liefern diese Bedingungen keine sinnvollen
  Ergebnisse.
- **Verhalten nach Reset/Busausfall**: Viele Funktionen (Logikgatter, Szenensteuerung,
  Universal-Rechner, Min/Max/Mittelwert, Temperatur-/Wertevergleicher) bieten die Option,
  Eingänge nach einem Reset aktiv abzufragen und/oder das Senden des Ausgangs so lange
  zurückzuhalten, bis alle relevanten Eingänge einen gültigen Wert erhalten haben. Ohne diese
  Einstellung kann direkt nach Busspannungswiederkehr ein Ausgangswert auf Basis unvollständiger
  bzw. veralteter Eingangsdaten gesendet werden.
- **Rundungsverhalten Universal-Rechner**: Bei Prozentrechnungen (1-Byte-Modell) können
  Rundungsfehler auftreten (z. B. 14 % + 7 % → 21,2 % statt 21 %); die Rückrundung erfolgt
  kaufmännisch.
- **Formatwandler**: Da 22 unterschiedliche Wandlungsfunktionen existieren, die jeweils eigene
  Kommunikationsobjekte belegen, sollte die konkrete Objektbelegung stets anhand des in der ETS
  gewählten Unterfunktionstyps geprüft werden – die Objektzahl und -reihenfolge unterscheidet
  sich zwischen den 22 Varianten teils erheblich.

## Quelle

MDT Technisches Handbuch – KNX Logikmodul SCN-LOG1.02, Stand 03/2025, Version 1.0.
Datei: `originals/KNX/MDT_TM_SCN-LOG1-02_V10_DE.pdf`
