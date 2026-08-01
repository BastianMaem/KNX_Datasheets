---
title: MDT Jalousieaktor JAL-Serie mit Fahrzeitmessung
device_type: Jalousieaktor
manufacturer: MDT
article_number: [JAL-0810M.02, JAL-0410M.02]
bus: KNX TP
source_pdf: originals/KNX/MDT_THB_JAL_02_Jalousieaktor_Fahrzeitmessung_V11.pdf
last_updated: 2026-07-25
synonyms: [Rollladenaktor, Storenaktor, Beschattungsaktor, Jalousie-Rolladenaktor]
tags: [knx, jalousieaktor, mdt]
---

## Varianten

| Artikelnummer | Kanäle | Baubreite | Besonderheit |
|---|---|---|---|
| JAL-0810M.02 | 8 | 8TE | mit Fahrzeitmessung |
| JAL-0410M.02 | 4 | 4TE | mit Fahrzeitmessung |

Beide Geräte sind funktional identisch aufgebaut und unterscheiden sich ausschließlich in der Anzahl der Kanäle bzw. der Baubreite. Alle im Folgenden beschriebenen Kommunikationsobjekte und Parameter gelten – sofern nicht anders vermerkt – für beide Varianten gleichermaßen. Bei den kanalbezogenen Kommunikationsobjekten wiederholt sich der Objektblock je Kanal (Offset +29 zum jeweils nächsten Kanal), sodass das 8-fach-Gerät entsprechend mehr Objektinstanzen besitzt als das 4-fach-Gerät.

## Übersicht

Der Jalousieaktor steuert wahlweise Jalousien (mit Lamellen) oder Rollläden an; ebenso lässt er sich für Lüftungsklappen, Garagentore oder Markisen einsetzen. Jeder Kanal wird individuell als "Jalousie", "Rollladen" oder "nicht aktiv" konfiguriert; ab Kanal B kann außerdem die Konfiguration von Kanal A übernommen werden, um Parametrierarbeit zu sparen.

Zentrale Funktionsmerkmale:

- **Automatische Fahrzeitmessung**: Der Aktor kann die für Auf- und Abwärtsfahrt benötigte Zeit je Kanal selbstständig einmessen (kompatibel zu Motoren mit mechanischer und elektronischer Endabschaltung) und diese Zeit im laufenden Betrieb nachkorrigieren, sodass witterungsbedingte Laufzeitschwankungen (z. B. im Winter) ausgeglichen werden. Alternativ können die Verfahrzeiten manuell per Stoppuhr ermittelt und eingetragen werden.
- **Sonnenstandsberechnung mit automatischer Beschattung/Lamellennachführung**: Der Aktor berechnet aus Datum/Uhrzeit und Helligkeitswerten selbstständig Sonnenazimut und -elevation und kann darauf basierend Rollläden auf eine Beschattungsposition fahren bzw. bei Jalousien die Lamellen dem Sonnenstand nachführen.
- **Lüftungsfunktion über Fensterkontakt**: Bei gekipptem Fenster kann der Behang auf eine Lüftungsposition fahren, bei geöffnetem Fenster/geöffneter Terrassentür kann automatisiertes Verfahren gesperrt werden, während die Handbedienung weiterhin aktiv bleibt – dies verhindert ein versehentliches Aussperren.
- **"Single Object Control"**: Komfortable Handbedienung von Rollläden über ein einziges Objekt (kurzer Tastendruck = fahren/stoppen, langer Tastendruck = Gruppensteuerung mehrerer Rollläden).
- **Brandalarmfunktion**: Bei Auslösung fahren die konfigurierten Kanäle sofort in eine feste Fluchtposition nach oben und werden gesperrt.
- **Frost-/Eisschutz**: Sperrt Kanäle bei Temperaturen unter 3 °C in Kombination mit Niederschlag und gibt sie nach Erwärmung über einen einstellbaren Schwellwert wieder frei.
- **Erweiterte Sperrfunktion**: Ermöglicht feingranulare Sperren einzelner Funktionsgruppen (Handbedienung, Auf/Ab, absolute Position/Beschattung, Automatik, Szene, Lüftung, zentrale Objekte) über separate Objekte, z. B. für eine "Kinderschlaf"-Funktion.
- **Erweiterte Szenenfunktion**: Szenen können nicht nur Positionen anfahren, sondern auch Sperren setzen/löschen oder eine untere Positionsbegrenzung definieren.
- **Erweiterte Automatikfunktion**: Zwei unabhängige Automatikblöcke (A/B) mit je vier über 1-Bit-Objekte aufrufbaren Positionen je Kanal.
- **Umfangreiche Statusrückmeldungen** für Visualisierungen sowie ein 14-Byte-Klartext-Diagnoseobjekt je Kanal und ein globales 14-Byte-Diagnoseobjekt für die Beschattung.
- **Long-Frame-Unterstützung** zur Verkürzung der Programmierzeit (ab ETS5, benötigt long-frame-fähiges Schnittstellengerät).
- **Update-Fähigkeit per DCA** (ab Geräteversion R6.0) über das MDT Update Tool.

## Technische Daten

| Merkmal | JAL-0410M.02 | JAL-0810M.02 |
|---|---|---|
| Kanäle | 4 | 8 |
| Baubreite (TE) | 4TE | 8TE |
| Bemessungsstrom | 8 A | 8 A |
| Max. Motorleistung je Kanal | 300 W | 300 W |
| Motorspannung | 230V AC | 230V AC |
| Handbedienung am Gerät | ja, über Tasten am Gehäuse | ja, über Tasten am Gehäuse |
| Busspannung | KNX TP (Busklemme) | KNX TP (Busklemme) |
| Zusätzliche Versorgungsspannung | 230V AC (zwingend erforderlich, sonst keine Bedienbarkeit) | 230V AC (zwingend erforderlich, sonst keine Bedienbarkeit) |
| Montageart | Reiheneinbaugerät (REG) | Reiheneinbaugerät (REG) |
| Zulassung | CE, UKCA (Betrieb in EU und Vereinigtem Königreich zugelassen) | CE, UKCA (Betrieb in EU und Vereinigtem Königreich zugelassen) |
| Einsatz in USA/Kanada | nicht gestattet | nicht gestattet |
| Gehäuseabmessungen | nicht im Datenblatt spezifiziert | nicht im Datenblatt spezifiziert |
| Schutzart | nicht im Datenblatt spezifiziert | nicht im Datenblatt spezifiziert |
| Zulässiger Betriebstemperaturbereich | nicht im Datenblatt spezifiziert | nicht im Datenblatt spezifiziert |

Ohne die zusätzliche 230V-AC-Hilfsspannung lässt sich der Aktor nicht bedienen: Ist nur die Busspannung angeschlossen, bleibt die Programmier-LED dunkel. Ist nur die 230V-Hilfsspannung angeschlossen, blinkt die rote Programmier-LED im Muster "lang Aus/kurz An".

## Kommunikationsobjekte

Die Objektnummern beziehen sich auf Kanal A. Für jeden weiteren Kanal verschiebt sich die Nummerierung um +29 (z. B. Kanal B: Objekt 23 → 52, Kanal C: 23 → 81 usw.). Spalte "Gilt für" bezieht sich auf die Geräteanwendung: "beide" = JAL-0410M.02 und JAL-0810M.02 gleichermaßen (unterscheiden sich nur in der Anzahl vorhandener Kanalinstanzen); "nur Jalousie" bzw. "nur Rollladen" bezieht sich auf die Kanal-Betriebsart, die je Kanal in der ETS gewählt wird.

### Zentrale Objekte (Sammelbefehle für alle Kanäle)

| Nr. | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 0 | Zentrale Funktion Rollladen Auf/Ab | Fahrbefehl für alle Kanäle mit aktivierten zentralen Objekten | 1 Bit | beide |
| 1 | Zentrale Funktion Lamellenverstellung/Stopp | Lamellenverstellung/Stopp für alle Jalousiekanäle mit aktivierten zentralen Objekten | 1 Bit | nur Jalousie |
| 2 | Zentrale Funktion Stopp | Stoppbefehl für alle Kanäle mit aktivierten zentralen Objekten | 1 Bit | beide |
| 3 | Zentrale Funktion absolute Position | Absoluter Höhenpositionsbefehl für alle Kanäle mit aktivierten zentralen Objekten | 1 Byte | beide |
| 4 | Zentrale Funktion absolute Lamellenposition | Absoluter Lamellenpositionsbefehl für alle Jalousiekanäle mit aktivierten zentralen Objekten | 1 Byte | nur Jalousie |
| 5 | In Betrieb | Sendet ein (optional zyklisches) "In-Betrieb"-Telegramm | 1 Bit | beide |

Diese sechs Objekte sind unabhängig von der kanalweisen Aktivierung dauerhaft sichtbar. Ob ein einzelner Kanal auf sie reagiert, wird pro Kanal über den Parameter "Zentrale Objekte" festgelegt (siehe ETS-Parameter, Abschnitt Zentrale Objekte). Das Auf/Ab-Objekt (0) folgt der KNX-Konvention: "0" = Aufwärtsfahrt, "1" = Abwärtsfahrt.

### Allgemeine/globale Objekte (Eisschutz, Zeit, Helligkeit, Außentemperatur, Beschattungsfreigabe)

| Nr. | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 6 | Handbedienung sperren | Sperrt die Handbedienung am Gerät, wenn Parameter "sperrbar über Objekt" gewählt ist | 1 Bit | beide |
| 6 | Regenalarm für Eisschutz | Überwachung des Regenalarms für die erweiterte Eis-/Frostschutzfunktion | 1 Bit | beide |
| 7 | Datum/Uhrzeit Aktuelle Werte | Empfang von Datum und Uhrzeit als ein gemeinsames Objekt | 8 Byte | beide |
| 7 | Uhrzeit Aktuellen Wert | Empfang der Uhrzeit als separates Objekt | 3 Byte | beide |
| 8 | Datum Aktuellen Wert | Empfang des Datums als separates Objekt | 3 Byte | beide |
| 9 | Zentrale Funktion Helligkeit 1 | Empfang des ersten Helligkeitswertes (für Sonnenstands-/Beschattungsberechnung) | 2 Byte oder 1 Bit (je nach Parametrierung) | beide |
| 10 | Zentrale Funktion Helligkeit 2 | Empfang des zweiten Helligkeitswertes | 2 Byte oder 1 Bit | beide |
| 11 | Zentrale Funktion Helligkeit 3 | Empfang des dritten Helligkeitswertes | 2 Byte | beide |
| 12 | Zentrale Funktion Außentemperatur | Empfang der Außentemperatur für Eis-/Frostschutz und Beschattungssperre | 2 Byte | beide |
| 12 | Zentrale Funktion Außentemperatur Schwelle | Empfang eines 1-Bit-Schwellwertsignals anstelle eines Temperaturwertes | 1 Bit | beide |
| 13 | Zentrale Funktion Beschattung sperren/freigeben | Zentrales Sperren bzw. Freigeben der automatischen Beschattung | 1 Bit | beide |
| 14 | Zentrale Funktion Beschattung Diagnose | Klartext-Diagnoseobjekt für den globalen Beschattungszustand | 14 Byte | beide |

Diese Objekte versorgen die kanalübergreifende Automatik (Eis-/Frostschutz, Sonnenstandsberechnung, Beschattung) mit den nötigen Umgebungsdaten. Werden mehrere Helligkeitswerte gesendet (z. B. Ost/Süd/West einer Wetterstation), wertet der Aktor für die Schwellwertauswertung immer den höchsten anliegenden Wert aus. Bleiben Außentemperatur oder Regenmeldung länger als die parametrierte Überwachungszeit aus, aktiviert der Aktor sicherheitshalber den Eis-/Frostschutz.

### Kanalobjekte – Fahrbefehle und Szene

| Nr. (Kanal A) | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 23 | Jalousie Auf/Ab | Fahrbefehl: "0" = Auffahrt, "1" = Abfahrt | 1 Bit | nur Jalousie |
| 23 | Rollladen Auf/Ab | Fahrbefehl: "0" = Auffahrt, "1" = Abfahrt | 1 Bit | nur Rollladen |
| 23 | Single Object Control | Ein Objekt für Auf/Ab/Stopp bei aktivierter Single-Object-Control-Funktion | 1 Bit | nur Rollladen |
| 24 | Lamellenverstellung/Stopp | Verstellt die Lamellen und stoppt gleichzeitig eine laufende Fahrt | 1 Bit | nur Jalousie |
| 24 | Kurzzeitbetrieb/Stopp | Aktiviert den Kurzzeit-/Tastbetrieb für exaktes Positionieren; stoppt eine laufende Fahrt | 1 Bit | nur Rollladen |
| 25 | Stopp | Stoppt eine laufende Fahrt unabhängig vom gesendeten Wert | 1 Bit | nur Rollladen |
| 26 | Szene | Aufruf/Speichern einer der bis zu 8 Kanalszenen | 1 Byte | beide |

Das Fahrobjekt folgt bei beiden Betriebsarten der KNX-Standardlogik (0 = auf, 1 = ab). Bei Jalousie-Kanälen übernimmt "Lamellenverstellung/Stopp" zusätzlich die Stoppfunktion; bei Rollladen-Kanälen ist dafür ein eigenes Stopp-Objekt vorhanden. Der Kurzzeitbetrieb bewegt den Behang bei jedem weiteren Signal um die parametrierte Kurzzeit-Verfahrzeit weiter und eignet sich zum exakten Anfahren spezieller Positionen. Das Szenenobjekt nimmt Werte 0–63 zum Aufruf bzw. 128–191 zum Speichern entgegen (siehe Abschnitt Szenen unten).

### Fahrzeitmessung und Referenzfahrt

| Nr. (Kanal A) | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 35 | Fahrzeitmessung starten | Startet die automatische Fahrzeitmessung durch Senden einer "1" | 1 Bit | beide, bei aktivierter automatischer Fahrzeitmessung |
| 35 | Referenzfahrt starten | Startet eine Referenzfahrt in eine Endlage | 1 Bit | beide, bei deaktivierter automatischer Fahrzeitmessung |

Ist die automatische Fahrzeitmessung aktiv, übernimmt Objekt 35 das Starten der Fahrzeitmessung; die gemessenen Zeiten für Auf- und Abfahrt werden anschließend automatisch über das Diagnoseobjekt (51) ausgegeben – auch wenn dessen Sendebedingung sonst auf "nicht aktiv" steht. Ist die automatische Fahrzeitmessung deaktiviert, dient dasselbe Objekt stattdessen dem Auslösen einer Referenzfahrt, die den Aktor in eine bekannte Endlage bringt und damit die interne Positionsberechnung neu kalibriert.

### Absolute Position / Positionsbegrenzung

| Nr. (Kanal A) | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 30 | absolute Position | Fährt eine absolute Höhenposition (0 % = ganz offen, 100 % = ganz geschlossen) an | 1 Byte | beide |
| 31 | absolute Lamellenposition | Fährt eine absolute Lamellenposition an | 1 Byte | nur Jalousie |
| 36 | Position anfahren/begrenzen | Fährt eine feste, parametrierte Position an bzw. begrenzt die untere Position über ein 1-Bit-Signal | 1 Bit | beide |

Die absoluten Positionsobjekte berechnen aus dem Prozentwert automatisch die notwendige Verfahrzeit auf Basis der eingestellten Verfahrzeiten und der aktuellen Position. Objekt 36 ermöglicht es, ohne 1-Byte-Wert eine fest hinterlegte Position anzufahren oder die maximale Ausfahrtiefe (untere Position) dauerhaft zu begrenzen – die Begrenzung wirkt dann auch gegen Handbedienung, wird jedoch von Alarmen und der normalen Sperrfunktion überfahren.

### Statusobjekte

| Nr. (Kanal A) | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 27 | Status akt. Richtung | "0" = zuletzt Aufwärtsfahrt, "1" = zuletzt Abwärtsfahrt | 1 Bit | beide |
| 28 | Verfahrstatus | "1" solange eine Fahrt läuft (Ein-Objekt-Variante) | 1 Bit | beide |
| 28 | Verfahrstatus Auf | Meldet aktive Aufwärtsfahrt (Zwei-Objekt-Variante) | 1 Bit | beide |
| 29 | Verfahrstatus Ab | Meldet aktive Abwärtsfahrt (Zwei-Objekt-Variante) | 1 Bit | beide |
| 32 | Status aktuelle Position | Aktuelle Höhenposition in % | 1 Byte | beide |
| 33 | Status akt. Lamellenposition | Aktuelle Lamellenposition in % | 1 Byte | nur Jalousie |
| 34 | Status Sperre/Alarme | "1" = aktiver Alarm oder aktive Sperre | 1 Bit | beide |
| 37 | Status obere Position | "1" = obere Endlage (0 %) erreicht | 1 Bit | beide |
| 38 | Status untere Position | "1" = untere Endlage (100 %) erreicht | 1 Bit | beide |

Die Positionsstatusobjekte (32/33) senden je nach Parametrierung entweder nur nach Fahrtende oder zusätzlich zyklisch während der Fahrt und ermöglichen so eine synchron mitlaufende Visualisierung, auch wenn der Kanal gerade gesperrt ist und über absolute Position angesteuert wird. Die Endlagen-Statusobjekte (37/38) wechseln zurück auf "0", sobald die jeweilige Endlage wieder verlassen wird.

### Erweiterte Sperrfunktion

| Nr. (Kanal A) | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 39 | Sperren zentrale Objekte | Sperrt die für diesen Kanal festgelegten zentralen Objekte | 1 Bit | beide |
| 40 | Absolute Position/Beschattung sperren | Sperrt absolute Positionsbefehle und die automatische Beschattung des Kanals (zentrale Auf/Ab-Befehle bleiben möglich) | 1 Bit | beide |
| 41 | Funktionen sperren | Sperrt die in den Parametern ausgewählte Kombination aus Handbedienung, Auf/Ab, absoluter Position/Beschattung, Automatik, Szene und Lüftungsfunktion | 1 Bit | beide |

Diese drei Objekte erscheinen nur, wenn die "Erweiterte Sperrfunktion" im Kanal aktiviert wurde (siehe ETS-Parameter). Sie ermöglichen eine deutlich feinere Sperrlogik als die "normale Sperrfunktion" und eignen sich z. B. zur Realisierung einer raumbezogenen "Kinderschlaf"-Sperre, bei der gezielt einzelne Bedienwege blockiert werden, während andere (z. B. Handbedienung) weiter funktionieren.

### Alarm- und normale Sperrfunktion

| Nr. (Kanal A) | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 42 | Windalarm | Aktiviert/deaktiviert den Windalarm des Kanals | 1 Bit | beide |
| 43 | Regenalarm | Aktiviert/deaktiviert den Regenalarm des Kanals | 1 Bit | beide |
| 43 | Brandalarm | Aktiviert/deaktiviert den Brandalarm des Kanals (alternative Belegung zu Regenalarm) | 1 Bit | beide |
| 44 | Frostalarm | Aktiviert/deaktiviert den Frostalarm des Kanals | 1 Bit | beide |
| 45 | Sperren | Aktiviert/deaktiviert die "normale Sperrfunktion" des Kanals | 1 Bit | beide |

Jeder Alarm wird über "1" ausgelöst und über "0" zurückgenommen. Sind mehrere Alarme gleichzeitig aktiv, führt der Aktor nur die Aktion des Alarms mit der laut Parameter "Alarmreihenfolge" höchsten Priorität aus; die Aktion niedriger priorisierter Alarme wird erst nach Rücknahme des höher priorisierten Alarms nachgeholt. Regenalarm und Brandalarm teilen sich dasselbe Objekt 43 – welche Variante aktiv ist, hängt von der gewählten Alarmreihenfolge ab. Während ein Alarm oder die normale Sperre aktiv ist, ist keine Fernbedienung des Kanals möglich; die Handbedienung am Gerät bleibt jedoch auch bei aktiven Alarmen/Sperren nutzbar.

### Lüftungsfunktion (Fensterkontakt)

| Nr. (Kanal A) | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 46 | Fensterkontakt | Zustand des Fensterkontakts bei Verwendung eines einzelnen Kontakts | 1 Bit | beide |
| 46 | Fensterkontakt 1 | Erster von zwei Fensterkontakten (z. B. für "gekippt"/"geöffnet") | 1 Bit | beide |
| 47 | Fensterkontakt 2 | Zweiter von zwei Fensterkontakten | 1 Bit | beide |

Über die Kombination der beiden Kontaktzustände unterscheidet der Aktor zwischen "gekippt" und "geöffnet" und löst je nach Parametrierung eine Lüftungsposition, eine Funktionssperre oder eine Kombination aus beidem aus (siehe ETS-Parameter, Abschnitt Lüftungsfunktion).

### Raumtemperatur und kanalbezogene Beschattung

| Nr. (Kanal A) | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 48 | Raumtemperatur | Empfang eines Raumtemperaturwertes zur temperaturabhängigen Beschattungsfreigabe | 2 Byte | beide |
| 48 | Raumtemperatur Schwelle | Empfang eines 1-Bit-Schwellwertsignals anstelle eines Temperaturwertes | 1 Bit | beide |
| 48 | Stellwert Heizen | Empfang des Heizungsstellwertes zur stellwertabhängigen Beschattungsfreigabe | 1 Byte | beide |
| 49 | Beschattung sperren/freigeben | Sperrt bzw. gibt die automatische Beschattung dieses Kanals frei | 1 Bit | beide |
| 49 | Lamellennachführung sperren/freigeben | Sperrt bzw. gibt die Lamellennachführung dieses Kanals frei | 1 Bit | nur Jalousie |
| 50 | Status Beschattung Zustand | "1" = Beschattungsposition ist aktiv angefahren | 1 Bit | beide |
| 50 | Status Beschattung bereit | "1" = Beschattung ist berechnungsbereit (Uhrzeit/Datum liegen vor) | 1 Bit | beide |
| 50 | Status Beschattung sperren | "1" = Beschattung ist gesperrt | 1 Bit | beide |

Objekt 48 erlaubt drei alternative Freigabelogiken: klassischer Temperaturwert, 1-Bit-Schwelle oder Heizungsstellwert – dahinter steht die Idee, im Winter die Sonneneinstrahlung als kostenlose Heizquelle zu nutzen und die Beschattung erst zu aktivieren, wenn die gewünschte Raumtemperatur erreicht bzw. die Heizleistung ausreichend reduziert ist.

### Diagnose

| Nr. (Kanal A) | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 51 | Diagnosetext | Gibt die zuletzt ausgeführte Kanalaktion als Klartext-String aus | 14 Byte | beide |

Das Diagnoseobjekt kann auf "nicht aktiv", "bei Abfrage senden" oder "bei Änderung senden" parametriert werden und liefert kurze Klartext-Codes (z. B. "Up", "Down", "Wind Alarm", "Locked", "Saved 023s Up") zur schnellen Fehlersuche und Inbetriebnahme, ohne dass eine Visualisierung mit Bitmuster-Interpretation nötig ist. Während einer über Objekt gestarteten Fahrzeitmessung wird der Diagnosetext nach jeder Teilaktion automatisch gesendet, unabhängig von der sonst eingestellten Sendebedingung.

Wichtige Diagnose-Klartexte (Auszug): `Up`/`Down` (Fahrt), `absolut Pos` (absolute Position angefahren), `Scene` (Szenenaufruf), `Auto Position` (Automatikposition), `Manual Oper` (Handbedienung), `Window open`/`Window close` (Fensterkontakt), `Auto Sun Pos` (automatische Beschattung), `Locked` (Kanal gesperrt), `Wind Alarm`/`Rain/Fire Alarm`/`Frost Alarm`/`Alarm End`, `Bus Reset`, `Reference` (Referenzfahrt), `Meas Start Up`, `Cur .XXXX Up/Dn` (Motorstrom während Fahrzeitmessung), `Saved XXXs Up/Dn` (gemessene Fahrzeit), `Meas Fail`/`Meas Abort` (Messfehler/-abbruch), `Lower Limit` (untere Positionsbegrenzung erreicht).

### Automatikfunktion (Blöcke A/B)

| Nr. | Name | Funktion | Größe | Gilt für |
|---|---|---|---|---|
| 15–18 | Automatik A – Automatikposition 1–4 | Aufruf der jeweiligen Automatikposition in Block A | 1 Bit | beide |
| 19–22 | Automatik B – Automatikposition 1–4 | Aufruf der jeweiligen Automatikposition in Block B | 1 Bit | beide |

Diese acht Objekte sind kanalübergreifend nutzbar: Ihr Aufruf löst in allen Kanälen, die auf den entsprechenden Block und dieselbe Automatikposition parametriert sind, gleichzeitig die hinterlegte Aktion aus (z. B. Höhenposition, Lamellenposition). So lassen sich Gruppen von Kanälen (z. B. alle Fenster eines Raums) mit einem einzigen Telegramm gemeinsam ansteuern, während andere Kanäle unbeteiligt bleiben.

## ETS-Parameter

### Allgemeine Einstellungen

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Geräteanlaufzeit | 2–240 s | 2 s | beide |
| Handbedienung | aktiv / gesperrt / sperrbar über Objekt | aktiv | beide |
| Sparmodus, LEDs abschalten nach | nicht aktiv / 30 s–60 min | nicht aktiv | beide |
| "In Betrieb" zyklisch senden | nicht aktiv / 1 min–24 h | nicht aktiv | beide |
| Aktuelle Position speichern | nicht aktiv / beim Laden der Applikation und bei Netzspannungsausfall / beim Laden der Applikation / bei Netzspannungsausfall | beim Laden der Applikation und bei Netzspannungsausfall | beide |
| Eingelernte Szenen überschreiben | eingelernte Szenen behalten / Parameter laden | Parameter laden | beide |
| Automatische Beschattung | nicht aktiv / aktiv | nicht aktiv | beide |
| Erweiterter Eis-/Frostschutz | nicht aktiv / aktiv | nicht aktiv | beide |
| Regenauswertung (bei Eis-/Frostschutz) | nicht aktiv / aktiv | nicht aktiv | beide |
| Alarmende wenn Außentemperatur höher als | 4 °C–10 °C | 5 °C | beide |
| Verzögerung Alarmende | 0–240 h | 2 h | beide |
| Überwachungszeit für Außentemperatur (und Regen) | nicht aktiv / 1 min–4 h | nicht aktiv | beide |
| Automatik Block A | nicht aktiv / aktiv | nicht aktiv | beide |
| Automatik Block B | nicht aktiv / aktiv | nicht aktiv | beide |

Die "Geräteanlaufzeit" definiert die Wartezeit zwischen Neustart (z. B. nach Busspannungswiederkehr) und funktionsbereitem Anlauf. "Aktuelle Position speichern" erlaubt es, nach Netzspannungsausfall oder Neuprogrammierung auf eine erneute Referenzfahrt zu verzichten, da die letzte Position remanent gespeichert wird. "Eingelernte Szenen überschreiben" steuert, ob durch den Nutzer per Taster veränderte Szenenwerte eine erneute Programmierung überstehen oder auf die ETS-Werte zurückgesetzt werden. Der "Erweiterte Eis-/Frostschutz" setzt automatisch den Frostalarm in allen betroffenen Kanälen, wenn die Außentemperatur unter 3 °C liegt (optional zusätzlich Regen erforderlich), und hebt ihn erst nach der eingestellten Verzögerung wieder auf, sobald die Außentemperatur den Alarmende-Schwellwert überschreitet. Bleiben Außentemperatur/Regen länger als die Überwachungszeit aus, wird der Frostschutz sicherheitshalber automatisch aktiviert. Die Aktivierung von "Automatische Beschattung" bzw. "Automatik Block A/B" blendet die jeweils zugehörigen Untermenüs und Kommunikationsobjekte erst ein.

### Kanal Auswahl

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Kanal A–x | nicht aktiv / Jalousie / Rollladen / Einstellungen aus Kanal A verwenden | herstellerseitig je Kanal vorbelegt | beide (ab Kanal B: "Einstellungen aus Kanal A verwenden" wählbar) |
| Kanal-/Objektbeschreibung | Freitext, bis 30 Zeichen | leer | beide |
| Zusatztext | Freitext, bis 80 Zeichen | leer | beide |

Jeder Kanal wird unabhängig als Jalousie, Rollladen oder inaktiv konfiguriert; ein inaktiver Kanal blendet sein Untermenü und seine Objekte vollständig aus. Ab Kanal B kann statt einer eigenen Parametrierung "Einstellungen aus Kanal A verwenden" gewählt werden – der Kanal übernimmt dann sämtliche Parameter und Kommunikationsobjekte von Kanal A, was die Projektierung baugleicher Kanäle vereinfacht. Die Kanal-/Objektbeschreibung erscheint sowohl im ETS-Kanalmenü als auch an den zugehörigen Kommunikationsobjekten und dient der Wiedererkennung (z. B. "Küche"); der Zusatztext ist reine Projektierungsnotiz ohne weitere Sichtbarkeit.

### Verfahrzeiten – Automatische Fahrzeitmessung

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Automatische Fahrzeitmessung | nicht aktiv / aktiv | nicht aktiv | beide |
| Laufende Fahrzeitkorrektur | nicht aktiv / aktiv | – | beide, bei aktiver automatischer Fahrzeitmessung |
| Relais ausschalten | nach Fahrzeitverlängerung / über Motorstrom | über Motorstrom | beide, bei aktiver automatischer Fahrzeitmessung |

Bei aktivierter automatischer Fahrzeitmessung entfällt die manuelle Zeitermittlung: Über das Objekt "Fahrzeitmessung starten" misst der Aktor Auf- und Abfahrzeit selbstständig und gibt die Ergebnisse über den Diagnosetext aus. Bei Erstinbetriebnahme oder nach einem Motortausch muss diese Messung zwingend einmal über das Objekt gestartet werden. "Laufende Fahrzeitkorrektur" gleicht im Betrieb jahreszeitlich bedingte Laufzeitänderungen (z. B. zähere Mechanik im Winter) automatisch schrittweise aus. "Relais ausschalten – über Motorstrom" schaltet das Relais direkt nach tatsächlichem Fahrtende ab (erkannt am Motorstrom), was bei Jalousien eine unmittelbar folgende Lamellenverstellung ermöglicht.

### Verfahrzeiten – Manuelle Messung

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Verfahrzeit für Auf/Ab | gleich / unterschiedlich | – | beide, bei deaktivierter automatischer Fahrzeitmessung |
| Verfahrzeit / Verfahrzeit Fahrtrichtung Auf / Verfahrzeit Fahrtrichtung Ab | 0–1000 s | 45 s | beide, bei deaktivierter automatischer Fahrzeitmessung |

Bei deaktivierter automatischer Fahrzeitmessung müssen die Verfahrzeiten (Zeit von einer Endlage zur anderen) manuell per Stoppuhr ermittelt und eingetragen werden. Sind Auf- und Abfahrzeit annähernd gleich lang, genügt ein gemeinsamer Wert; unterscheiden sie sich (häufig bei schwerkraftunterstützter Abfahrt), können getrennte Werte für Auf- und Abfahrt hinterlegt werden. Nach Ablauf der eingestellten Zeit schaltet der Aktor das Relais unabhängig davon ab, ob die tatsächliche Endlage erreicht wurde – ein zu klein gewählter Wert führt daher dazu, dass die Endlage nicht ganz erreicht wird.

### Verfahrzeiten – Weitere Parameter

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Fahrzeitverlängerung | keine Verlängerung / 2 % / 5 % / 10 % / 15 % / 20 % | 5 % | beide |
| Schrittweite für Lamellenverstellung | 50–5000 ms | 200 ms | nur Jalousie |
| Lamellenverstellzeit | 100–10000 ms | 1200 ms | nur Jalousie |
| Kurzzeitbetrieb (Tastbetrieb für genaue Position) | nicht aktiv / aktiv | aktiv | nur Rollladen |
| Verfahrzeit für Kurzzeitbetrieb | 50–5000 ms | 200 ms | nur Rollladen, bei aktivem Kurzzeitbetrieb |
| Auf/Ab kann stoppen (Single Object Control) | nicht aktiv / aktiv | nicht aktiv | nur Rollladen |
| Umkehrpause | 100–2000 ms | 500 ms | beide |
| Einschaltverzögerung Motor | 0–500 ms | 200 ms | beide |
| Ausschaltverzögerung Motor | 0–500 ms | 200 ms | beide |
| Motor Auf/Ab vertauschen | normal / Auf/Ab vertauscht | normal | beide |
| Position der Lamellen nach Fahrtende (Abfahrt) | 0–100 % | 100 % | nur Jalousie |

Die "Fahrzeitverlängerung" fährt bewusst etwas über die berechnete Verfahrzeit hinaus, um den mechanischen Endanschlag sicher zu erreichen, ohne die Berechnung absoluter Positionen zu verfälschen. Bei Jalousien bestimmen "Schrittweite" und "Lamellenverstellzeit" gemeinsam, in wie vielen diskreten Stufen sich die Lamellen von 0 % auf 100 % drehen lassen (Schrittweite als Vielfaches der Verstellzeit ergibt die Stufenzahl); die Mindest-Lamellenverstellzeit muss dabei größer sein als die kürzeste vorkommende Verfahrzeit. Bei Rollläden ermöglicht der "Kurzzeitbetrieb" das feinschrittige Nachjustieren einer Position; "Single Object Control" reduziert die Bedienung auf ein Objekt, bei dem ein erneuter Befehl eine laufende Fahrt stoppt. Die "Umkehrpause" schützt den Motor vor sofortigem Richtungswechsel, indem der Aktor bei gegenläufigem Befehl zunächst beide Fahrtrichtungen abschaltet und erst nach Ablauf der Pause die neue Richtung einschaltet – zu kurz gewählte Werte können den Motor beschädigen. "Position der Lamellen nach Fahrtende" definiert, welchen Winkel die Lamellen nach einer über das 1-Bit-Objekt ausgelösten Abfahrt automatisch einnehmen (nicht bei durch Stopp unterbrochener Fahrt).

### Referenzfahrt / Absolute Position / 1-Bit-Position

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Objekt für Referenzfahrt | nicht aktiv / aktiv | – | beide, nur bei deaktivierter automatischer Fahrzeitmessung sichtbar |
| Aktion nach Referenzfahrt | keine Aktion / vorherige Position anfahren | keine Aktion | beide |
| Objekte für absolute Position | nicht aktiv / aktiv | aktiv | beide |
| 1Bit Objekt für "Position anfahren/begrenzen" | nicht aktiv / aktiv | nicht aktiv | beide |
| Aktion bei Wert = 1 | Position anfahren / Position anfahren wenn oben / Position anfahren wenn unten / Untere Position begrenzen und anfahren / Untere Position begrenzen (nicht anfahren) | Position anfahren | beide |
| Rollladenposition / Jalousieposition / Lamellenposition (bei Wert=1) | 0–100 % | 50 % (Höhe) / 100 % (Lamelle) | beide |
| Aktion bei Wert = 0 (nur wenn Position gültig) | keine Aktion / nach oben fahren / nach unten fahren / Begrenzung untere Position löschen | keine Aktion | beide |

Die Referenzfahrt kalibriert die interne Positionsberechnung neu, indem gezielt eine Endlage angefahren wird; sie ist besonders relevant, wenn viel mit absoluten Positionsbefehlen unterhalb 100 % bzw. oberhalb 0 % gearbeitet wird, da sich sonst durch ungenaue Verfahrzeiten Positionsfehler aufsummieren können. Ist "Aktuelle Position speichern" (allgemeine Einstellungen) aktiv, entfällt die Notwendigkeit einer Referenzfahrt nach Programmierung/Netzausfall weitgehend. Das 1-Bit-Objekt "Position anfahren/begrenzen" erlaubt es, ohne 1-Byte-Telegramm eine feste Position anzufahren oder die maximale Ausfahrtiefe dauerhaft zu begrenzen; bei "Untere Position begrenzen (nicht aktiv)" kann während aktiver Begrenzung auch per Hand nicht tiefer gefahren werden, Alarme und die normale Sperrfunktion überfahren die Begrenzung jedoch. Diese Funktion bleibt bei gekipptem Fenster nutzbar, wird aber bei geöffnetem Fenster deaktiviert, um ein Aussperren zu vermeiden.

### Statusobjekte

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Status aktuelle Position | nicht aktiv / aktiv | aktiv | beide |
| Status senden | nach Fahrtende / alle 2 s / alle 5 s / alle 10 s | nach Fahrtende | beide |
| Objekte für Verfahrstatus | nicht aktiv / fährt (1 Objekt) / Auffahrt + Abfahrt (2 Objekte) | Auffahrt + Abfahrt (2 Objekte) | beide |
| Status akt. Richtung/Position oben/unten | nicht aktiv / aktiv | aktiv | beide |
| Status für aktuelle Sperre/Alarme | nicht aktiv / aktiv | aktiv | beide |
| Diagnose in Klartext | nicht aktiv / bei Abfrage Senden / bei Änderung senden | bei Abfrage Senden | beide |

Diese Parameter blenden die zugehörigen Statusobjekte (Abschnitt "Statusobjekte" oben) ein bzw. aus und legen ihr Sendeverhalten fest. "Status senden – alle 2/5/10 s" bewirkt ein zyklisches Senden der aktuellen Positionswerte während der Fahrt (zusätzlich zum Senden bei Fahrtende), was für flüssig mitlaufende Visualisierungen sinnvoll ist, aber die Busauslastung erhöht.

### Zentrale Objekte (kanalbezogene Reaktion)

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Zentrale Objekte | nicht aktiv / nur Auf / nur Ab / nur Auf/Ab / nur absolute Position / nur absolute Position und Auf / nur absolute Position und Ab / absolute Position und Auf/Ab | absolute Position und Auf/Ab | beide |

Dieser Parameter legt je Kanal fest, auf welche der global sichtbaren zentralen Objekte (0–4) der Kanal reagieren soll. Damit lassen sich Kanäle gezielt aus zentralen Sammelbefehlen ausschließen oder nur teilweise einbeziehen (z. B. nur zentrales "Auf", aber keine zentrale absolute Position).

### Verhalten bei Busspannungsausfall/-wiederkehr

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Verhalten bei Busspannungsausfall | keine Aktion / nach oben fahren / nach unten fahren / Fahrt stoppen / "Position anfahren" | keine Aktion | beide |
| Verhalten bei Busspannungswiederkehr | keine Aktion / nach oben fahren / nach unten fahren / "Position anfahren" | keine Aktion | beide |

Die Option "Position anfahren" wird nur angeboten, wenn zuvor die Funktion "1Bit Objekt für Position anfahren/begrenzen" aktiviert wurde; es wird dann die dort definierte Position angefahren. Ist beim Eintreten von Busspannungsausfall/-wiederkehr eine Sperre oder ein Alarm aktiv, hat diese/dieser stets Vorrang vor dem hier parametrierten Verhalten.

### Szenen

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Szene (Kanalfreigabe) | nicht aktiv / aktiv | aktiv | beide |
| Szenen Speichern | nicht aktiv / aktiv | nicht aktiv | beide |
| Szene Nummer A–H | nicht aktiv / 1–64 | – | beide |
| Szene X – Höhenposition | nicht aktiv / 0–100 % | – | beide |
| Szene X – Lamellenposition | nicht aktiv / 0–100 % | – | nur Jalousie |
| Szene X – Funktionen sperren/freigeben | nicht aktiv / Sperre abs. Position/Beschattung setzen / löschen / "Funktionen sperren" setzen / löschen / "Funktionen sperren" und Sperre abs. Position/Beschattung setzen / löschen / Beschattung freigeben / sperren / "Sperre zentrale Objekte" setzen / löschen / "Begrenzung untere Position" setzen und anfahren / löschen | nicht aktiv | beide |

Jeder Kanal kann auf bis zu 8 Szenen (A–H) reagieren; die Szenennummer (1–64) bestimmt, welcher am Kommunikationsobjekt "Szene" empfangene Wert (0–63 zum Abrufen, 128–191 zum Speichern) die jeweilige Szene auslöst. Sollen mehrere Kanäle gemeinsam auf dieselbe Szenennummer reagieren, müssen deren Szenen-Kommunikationsobjekte auf dieselbe Gruppenadresse verknüpft werden. Ist "Szenen Speichern" aktiv, kann der aktuelle Kanalzustand über einen langen Tastendruck (Taster ebenfalls mit "speichern" parametriert) unter der Szene abgelegt werden. Über "Funktionen sperren/freigeben" lassen sich per Szenenaufruf zusätzlich Sperren setzen/lösen oder eine untere Positionsbegrenzung definieren; wird dabei die Szenenfunktion selbst gesperrt, sind weitere Szenenaufrufe erst nach Aufheben dieser Sperre wieder möglich. Die Szenenfunktion bleibt bei gekipptem Fenster aktiv, wird jedoch bei geöffnetem Fenster deaktiviert (Aussperrschutz).

Kodierung Szenenabruf/-speicherung (Auszug):

| Szene | Abrufen (dez.) | Speichern (dez.) |
|---|---|---|
| 1 | 0 | 128 |
| 2 | 1 | 129 |
| … | … | … |
| 64 | 63 | 191 |

### Automatikfunktion

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Automatikfunktionen (Kanalfreigabe) | nicht aktiv / aktiv | nicht aktiv | beide |
| Verwendete Automatikobjekte | Block A / Block B | Block A | beide |
| Automatikposition 1–4 | nicht aktiv / aktiv | – | beide |
| Höhenposition (je Automatikposition) | nicht aktiv / 0–100 % | – | beide |
| Lamellenposition (je Automatikposition) | nicht aktiv / 0–100 % | – | nur Jalousie |
| Position anfahren (Wert = 1) | immer / wenn Position oben / wenn Position unten | immer | beide |
| Aktion bei Rücknahme der Automatikposition (Wert = 0) | nicht aktiv / nach oben fahren / nach unten fahren | nicht aktiv | beide |

Die Automatikfunktion muss zunächst im Kanal aktiviert werden; zusätzlich muss der verwendete Block (A und/oder B) unter "Allgemeine Einstellungen" aktiv sein, da sonst dessen Kommunikationsobjekte nicht existieren. Je Kanal lassen sich bis zu vier Positionen (Höhe, bei Jalousie zusätzlich Lamelle) hinterlegen, die durch die entsprechenden 1-Bit-Objekte (15–22) ausgelöst werden. "Position anfahren (Wert=1)" schränkt ein, aus welcher Ausgangslage heraus der Aufruf wirkt. Die "Aktion bei Rücknahme" wird nur ausgeführt, wenn der Kanal sich noch exakt in der zuvor über die Automatik angefahrenen Position befindet – wurde er zwischenzeitlich anderweitig verfahren, unterbleibt die Rücknahmeaktion. Sollen mehrere Kanäle gemeinsam reagieren, müssen sie auf denselben Block und dieselbe Automatikposition parametriert werden.

### Alarm- und Sperrfunktionen

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Alarm Reihenfolge | Windalarm/Regenalarm/Frostalarm/Sperrfunktion (in verschiedenen Reihenfolgen) / Brandalarm-Varianten | Windalarm, Regenalarm, Frostalarm, Sperrfunktion | beide |
| Normale Sperrfunktion | nicht aktiv / aktiv | aktiv | beide |
| Aktion beim Sperren (Wert=1) | keine Aktion / nach oben fahren / nach unten fahren / Höhenposition anfahren | – | beide |
| Aktion bei Rücknahme der Sperre | nicht aktiv / nach oben fahren / nach unten fahren / vorherige Position anfahren | – | beide |
| Erweiterte Sperrfunktion (Kanalfreigabe) | nicht aktiv / aktiv | nicht aktiv | beide |
| Windalarm (Kanalfreigabe) | nicht aktiv / aktiv | aktiv | beide |
| Überwachungszeit (Windalarm, 0 = nicht aktiv) | 0–120 min | 0 min | beide |
| Aktion bei Windalarm | keine Aktion / nach oben fahren / nach unten fahren / Höhenposition anfahren | nach oben fahren | beide |
| Aktion bei Rücknahme des Windalarms | keine Aktion / nach oben fahren / nach unten fahren / vorherige Position anfahren | vorherige Position anfahren | beide |
| Regenalarm/Brandalarm (Kanalfreigabe) | nicht aktiv / aktiv | nicht aktiv | beide |
| Frostalarm (Kanalfreigabe) | nicht aktiv / aktiv | nicht aktiv | beide |
| Jalousieposition/Lamellenposition für Alarme/Sperre | 0–100 % | 0 % | beide |

Die "Alarm Reihenfolge" bestimmt die Priorität, mit der konkurrierende Alarme/Sperren behandelt werden; bei gleichzeitig aktiven Alarmen wird nur die Aktion des höchstpriorisierten ausgeführt, die übrigen erst nach dessen Rücknahme. Über die Wahl einer Reihenfolge mit "Brandalarm" an erster Stelle wird das Objekt 43 vom Regen- zum Brandalarm umfunktioniert: Bei Brandalarm fährt der Kanal fest "nach oben" (Fluchtwegfreigabe) und bleibt gesperrt, solange der Alarm ansteht – diese Aktion ist nicht änderbar. Für Wind-, Regen- und Frostalarm lässt sich je eine zyklische Überwachungszeit einstellen: Bleibt innerhalb dieser Zeit kein Signal am zugehörigen Objekt aus, wird der Alarm automatisch ausgelöst (Erkennung eines Sensorausfalls); empfohlen wird ein Verhältnis von zyklischer Sendezeit des Sensors zu Überwachungszeit von etwa 1:3. Bei "Aktion ... Höhenposition anfahren" wird die unter "Jalousieposition/Lamellenposition für Alarme/Sperre" definierte, kanalweit einheitliche Position angefahren (gilt für alle Alarme und die normale Sperre dieses Kanals, außer Brandalarm).

### Erweiterte Sperrfunktion (Untermenü)

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Objekt "Absolute Position/Beschattung sperren" | nicht aktiv / aktiv | – | beide |
| Objekt sendet Status | nicht aktiv / aktiv | – | beide |
| Automatisch "Sperren absolute Position/Beschattung" bei Auf/Ab Telegramm | nicht aktiv / aktiv | – | beide |
| Sperre aufheben, wenn obere Position erreicht ist | nicht aktiv / aktiv | – | beide (empfohlen bei automatischer Beschattung) |
| Objekt "Funktionen sperren" | nicht aktiv / aktiv | – | beide |
| Objekt sendet Status | nicht aktiv / aktiv | – | beide |
| Handbedienung Gerät sperren / Auf/Ab sperren (auch Zentral) / Absolute Position/Beschattung sperren (auch Zentral) / Automatikpositionen sperren / Szene sperren / Lüftungsfunktion sperren | jeweils nicht aktiv / aktiv | jeweils nicht aktiv | beide |
| Objekt "Sperren zentrale Objekte" | nicht aktiv / sperrt nur Auf / nur Ab / nur Auf/Ab / abs. Position / abs. Position+Auf / abs. Position+Ab / abs. Position+Auf/Ab | – | beide |
| Objekt sendet Status | nicht aktiv / aktiv | – | beide |
| Automatisch "Sperren zentrale Objekte" bei "Ab" Telegramm | nicht aktiv / aktiv | – | beide |
| "Sperren zentrale Objekte" aufheben, wenn obere Position erreicht ist | nicht aktiv / aktiv | – | beide |

Diese Untermenü-Parameter konfigurieren die drei Objekte 39–41 im Detail. "Automatisch Sperren ... bei Auf/Ab Telegramm" ist besonders für Szenarien relevant, in denen eine Wetterstation den Sonnenschutz aktiviert hat, der Nutzer aber manuell verfahren möchte: Durch den manuellen Fahrbefehl wird der Empfang weiterer automatischer Positionsbefehle für diesen Kanal automatisch gesperrt, sodass die manuelle Fahrt nicht sofort wieder überschrieben wird; die Sperre kann automatisch beim Erreichen der oberen Position oder manuell über das Sperrobjekt zurückgenommen werden. Bei aktiver automatischer Beschattung wird diese automatische Sperrung intern ebenfalls automatisch gesetzt. Über "Funktionen sperren" lässt sich gezielt festlegen, welche Bedienwege (Handbedienung, Fahrbefehle, absolute Position/Beschattung, Automatik, Szene, Lüftung) gemeinsam gesperrt werden sollen – Lüftungsfunktion, Automatikpositionen (1 Bit) und "Position anfahren" (1 Bit) sind hiervon standardmäßig ausgenommen, sofern sie nicht ebenfalls hier ausgewählt werden. "Sperren zentrale Objekte" erlaubt eine feingranulare, kanalindividuelle Sperre der zentralen Sammelbefehle, z. B. sinnvoll, wenn eine Zeitschaltuhr alle Jalousien zentral verfährt, ein einzelner, manuell bedienter Kanal davon aber automatisch ausgenommen werden soll.

### Lüftungsfunktion

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Lüftungsfunktion über Fensterkontakte (Kanalfreigabe) | nicht aktiv / aktiv | nicht aktiv | beide |
| Fensterkontakte | 1 Kontakt für "geöffnetes" Fenster / 2 Kontakte für "geöffnetes"/"gekipptes" Fenster | 2 Kontakte | beide |
| Wert für "geöffnet" / "gekippt" | Kontaktkombinationen 0/1 je nach Anzahl Kontakte | – | beide |
| Verhalten wenn Fenster "geöffnet" wird | Lüftungsfunktion ausführen / Sperrfunktion setzen / Lüftungsposition ausführen und zentrale Objekte sperren / … und abs. Position/Beschattung sperren / … abs. Position/Beschattung und zentrale Objekte sperren | Lüftungsfunktion ausführen | beide |
| Aktion wenn Fenster "geöffnet" wird | nicht aktiv / Position anfahren wenn unten / wenn niedriger / wenn niedriger und untere Position begrenzen | Position anfahren wenn niedriger und untere Position begrenzen | beide |
| Höhenposition/Lamellenposition "geöffnet" | 0–100 % | 0 % | beide (Lamelle nur Jalousie) |
| Aktion wenn Fenster "gekippt" wird | nicht aktiv / Position anfahren wenn unten / wenn niedriger / wenn niedriger und untere Position begrenzen | Position anfahren wenn niedriger | beide (nur bei 2 Kontakten) |
| Höhenposition/Lamellenposition "gekippt" | 0–100 % | 100 % / 70 % | beide (Lamelle nur Jalousie, nur bei 2 Kontakten) |
| Aktion wenn Fenster geschlossen wird | nicht aktiv / nach oben fahren / nach unten fahren / vorherige Position anfahren | vorherige Position anfahren | beide |

Bei zwei Kontakten unterscheidet der Aktor zwischen "gekippt" (Lüftungsposition, z. B. Behang etwas hochgefahren) und "geöffnet" (weitergehende Aktion, z. B. Behang ganz auf und Sperrung automatischer Positionsbefehle). "Sperrfunktion setzen" nutzt die normale Sperrfunktion inkl. deren parametrierten Auf/Ab-Aktionen und eignet sich besonders für Terrassentüren, um ein Aussperren zu verhindern. Die Varianten mit "... und zentrale Objekte sperren" bzw. "... und abs. Position/Beschattung sperren" fahren stattdessen gezielt eine Lüftungsposition an und blockieren gleichzeitig automatisierte zentrale bzw. absolute Positionsbefehle (inklusive interner Beschattung), wobei während der Sperre eintreffende Befehle gespeichert und nach Freigabe nachgeholt werden; die Handbedienung sowie die kanaleigene Auf/Ab-Bedienung bleiben in allen Varianten nutzbar. Bei aktiver Lüftungsfunktion (Fenster offen) werden Alarme nur noch mit höheren (sichereren) Positionen ausgeführt, um ein Aussperren zu vermeiden; die Begrenzung der unteren Position greift dabei nicht bei Alarm oder normaler Sperrfunktion.

### Automatische Beschattung – Grundeinstellungen

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Helligkeitswerte über | Helligkeitswert 2 Byte / Helligkeitsschwelle 1 Bit | Helligkeitswert 2 Byte | beide |
| Anzahl der Objekte (bei 2 Byte) | 1–3 | 3 | beide |
| Helligkeitsschwelle 1 | 0–95.000 Lux | 30.000 Lux | beide |
| Helligkeitsschwelle 2 | 0–95.000 Lux | 45.000 Lux | beide |
| Hysterese | 0–20.000 Lux | 10.000 Lux | beide |
| Verzögerung der Helligkeitsschwelle 1 nach 2 | 0–30 min | 10 min | beide |
| Verzögerung der Helligkeitsschwelle 2 nach 1 | 0–60 min | 25 min | beide |
| Außentemperatursperre | nicht aktiv / Temperaturwert / Temperaturschwelle | Temperaturwert | beide |
| Beschattung sperren bei Temperatur kleiner | 5 °C–30 °C | 12 °C | beide |
| Funktion Zentrales Objekt "Beschattung" | Beschattung sperren bei Wert 1 / Beschattung freigeben bei Wert 1 | Beschattung sperren bei Wert 1 | beide |
| Automatische Umschaltung der Sommerzeit | nicht aktiv / aktiv | aktiv | beide |
| Standortbestimmung durch | Koordinaten / Ort | Ort | beide |
| Land / Stadt (bei "Ort") | beliebiges Land/Stadt | Deutschland / Engelskirchen | beide |
| Breite/Länge in Grad/Minuten (bei "Koordinaten") | Breite 0–90°, Länge 0–180° | ca. 50°56' N, 6°57' O (Werkseinstellung Engelskirchen) | beide |
| Zeitdifferenz zur Weltzeit (UTC+…) | beliebige Zeitzone | UTC+01:00 Amsterdam, Berlin | beide |
| Objekte für Datum/Uhrzeit | separate Objekte / ein gemeinsames Objekt | separate Objekte | beide |
| Diagnoseobjekt für Beschattung | nicht aktiv / bei Abfrage senden / bei Änderung senden | – | beide |

Für die Schwellwertauswertung müssen bis zu drei 2-Byte-Helligkeitswerte (z. B. Ost/Süd/West einer Wetterstation) oder alternativ 1-Bit-Schwellwertsignale angebunden werden; ausschlaggebend ist stets der höchste anliegende Wert. Helligkeitsschwelle 1 muss kleiner als Helligkeitsschwelle 2 sein. Einschaltwert ist jeweils die Schwelle selbst, der Ausschaltwert ergibt sich aus Schwelle minus Hysterese; die "Verzögerung der Helligkeitsschwelle" verhindert zu häufiges Verfahren bei kurzzeitig wechselnder Bewölkung. Die "Außentemperatursperre" blockiert die automatische Beschattung unterhalb einer parametrierten Außentemperatur (mit fest hinterlegter Freigabe-Hysterese von +2 K) bzw. über ein 1-Bit-Schwellensignal. Für die Sonnenstandsberechnung wird entweder ein Land/Ort aus einer Liste oder alternativ direkte geografische Koordinaten sowie die passende UTC-Zeitzone hinterlegt; die automatische Sommerzeitumschaltung kann in Ländern ohne Sommerzeit deaktiviert werden. Das globale Diagnoseobjekt (14 Byte, Objekt 14) liefert Beschattungsmodus (bereit/gesperrt/temperaturgesperrt, bit-codiert), überschrittene Helligkeitsschwelle sowie den aktuell berechneten Azimut und Elevationswinkel im Klartext (z. B. `M1 S1 A150 E30`); fehlt Datum/Uhrzeit, erscheint stattdessen `ERR: Date`.

### Automatische Beschattung – Einstellungen je Kanal

| Parameter | Werte | Standard | Gilt für |
|---|---|---|---|
| Beschattung (Kanal) | deaktiviert (Einstellungen bleiben erhalten) / aktiviert | aktiviert | beide |
| Himmelsrichtung | Ost / Südost / Süd / Südwest / West / Nord (mit zwei Bereichen) / Dachfläche / keine Azimutauswertung | Süd | beide |
| Beschattung aktiv wenn Azimut von…bis | 20°–340° (himmelsrichtungsabhängige Voreinstellung) | z. B. 120°–240° bei Süd | beide |
| Beschattung aktiv wenn Höhenwinkel von…bis | 0–45° … 10–90° | 2°…90° | beide |
| Beschatten wenn Höhenwinkel größer (alternativ, nur Nord/Dachfläche) | nicht aktiv / 10–90° | nicht aktiv | beide |
| Verzögerung Beschattung Ein | 0–30 min | 2 min | beide |
| Verzögerung Beschattung Aus | 0–60 min | 20 min | beide |
| Freigabe über (Temperatur/Stellwert) | nicht aktiv / Temperaturwert / Temperaturschwelle / Stellwert Heizen | nicht aktiv | beide |
| Freigabe wenn Temperaturwert größer | 15–35 °C | 21 °C | beide |
| Freigabe wenn Stellwert Heizen kleiner | 0–50 % | 5 % | beide |
| Objekt Beschattung | nicht aktiv / sperren bei Wert 1 / freigeben bei Wert 1 / Lamellennachführung sperren bei Wert 1 / Lamellennachführung freigeben bei Wert 1 | freigeben bei Wert 1 | beide |
| Sperren der Sonnenschutzposition mit Auf/Ab Telegramm | nicht aktiv / aktiv | aktiv | beide |
| Beschattung wieder aktivieren mit 0 % Position, nach Deaktivierung durch Auf/Ab | nicht aktiv / aktiv | aktiv | beide |
| Status automatische Beschattung | nicht aktiv / in Beschattungszustand (Wert 1) / in Bereitschaftszustand (Wert 1) / in Sperrzustand (Wert 1) | nicht aktiv | beide |
| Aktion bei Helligkeitsschwelle (Jalousie) | keine automatische Beschattung / Position anfahren ohne Lamellennachführung / mit Lamellennachführung / Position einer Szene verwenden (einlernbar) | Position anfahren mit Lamellennachführung | nur Jalousie |
| Beschatten ab Helligkeitsschwelle | Helligkeitsschwelle 1 / Helligkeitsschwelle 2 | Helligkeitsschwelle 1 | nur Jalousie |
| Jalousieposition | 10–100 % | 100 % | nur Jalousie |
| Lamellenposition | 0–100 % | 50 % | nur Jalousie |
| Lamellennachführung wenn Höhenwinkel kleiner (0 = nicht aktiv) | 0–90° | 45° | nur Jalousie |
| Mindeständerung Lamellennachführung | 5–30 % | 10 % | nur Jalousie |
| Offset Lamellennachführung | -25…25 | 0 | nur Jalousie |
| Lamelle ist waagerecht bei | 0 % / 50 % | 50 % | nur Jalousie |
| Verhalten nach Beschattung (Jalousie) | keine Änderung / nach oben fahren / Lamellen waagerecht | keine Änderung | nur Jalousie |
| Aktion bei Helligkeitsschwelle 1/2 (Rollladen) | keine automatische Beschattung / nicht aktiv / Position anfahren / Position einer Szene verwenden (einlernbar) | Position anfahren | nur Rollladen |
| Rollladenposition 1 / 2 | 10–100 % | 30 % / 60 % | nur Rollladen |
| Verhalten nach Beschattung (Rollladen) | keine Änderung / nach oben fahren / Position der Helligkeitsschwelle 1 anfahren | keine Änderung | nur Rollladen |

Die "Himmelsrichtung" liefert einen Vorschlag für den relevanten Azimutbereich, der individuell nachjustiert werden kann (z. B. bei Verschattung durch Nachbargebäude); "keine Azimutauswertung" macht die Beschattung ganztägig nur höhenwinkelabhängig aktiv. Über "Beschattung aktiv wenn Höhenwinkel" lässt sich der wirksame Elevationsbereich einschränken, etwa um bei niedrigem Sonnenstand (Hindernisse wie Bäume/Nachbargebäude) oder bei sehr hohem Sonnenstand (weiter Dachüberstand) keine unnötige Beschattung auszulösen. Die Ein-/Ausschaltverzögerungen dämpfen kurzzeitige Wolkenlücken. Die temperatur- bzw. stellwertabhängige Freigabe nutzt die Sonne als kostenlose Heizquelle, solange der Raum noch nicht die Zieltemperatur erreicht hat bzw. die Heizung noch aktiv läuft. "Sperren der Sonnenschutzposition mit Auf/Ab Telegramm" verhindert, dass ein manueller Fahrbefehl sofort wieder von der automatischen Beschattung überschrieben wird; "Beschattung wieder aktivieren mit 0 % Position" hebt diese interne Deaktivierung automatisch auf, sobald die obere Endlage erreicht wird (alternativ über das Freigabeobjekt). Bei Jalousie-Kanälen bestimmt die Lamellennachführung zusätzlich zur Höhenposition den Lamellenwinkel abhängig vom aktuellen Sonnen-Höhenwinkel; "Mindeständerung" und "Offset" steuern Schrittweite bzw. Verschiebung der Nachführung. Bei Rollladen-Kanälen stehen zwei unabhängige Helligkeitsschwellen mit je eigener Zielposition zur Verfügung, sodass bei stärkerer Einstrahlung weiter abgedunkelt werden kann als bei schwächerer.

## Inbetriebnahme / Hinweise

- **Inbetriebnahmereihenfolge**: Busschnittstelle anschließen → Netzspannung (230V-Hilfsspannung) zuschalten → Busspannung zuschalten → Programmiertaste am Gerät länger als 1 s drücken (rote LED leuchtet dauerhaft) → physikalische Adresse aus der ETS laden (LED erlischt) → Applikation mit gewünschter Parametrierung laden → Funktionsprüfung.
- **Ohne 230V-Hilfsspannung ist keine Bedienung möglich** – auch nicht über den Bus –, da diese für die Motoransteuerung zwingend benötigt wird.
- **Fahrzeitmessung starten**: entweder über das Kommunikationsobjekt "Fahrzeitmessung starten" oder direkt am Gerät durch Kanalauswahl mit den Pfeiltasten und anschließendes gleichzeitiges Drücken und Halten der Auf-/Ab-Tasten. Bei Erstinbetriebnahme oder nach Motortausch ist dies zwingend erforderlich, wenn die automatische Fahrzeitmessung genutzt wird.
- **Manuelle Fahrzeitermittlung**: Bei sehr kurzen Verfahrzeiten empfiehlt sich, zunächst einen etwas zu klein geschätzten Wert einzutragen und ihn anschließend durch Testfahrten in kleinen Schritten zu erhöhen, bis die Endlagen sicher erreicht werden, statt direkt mit einer möglicherweise zu großen Stoppuhr-Messung zu beginnen. Für die Lamellenverstellzeit bei kleinen Werten empfiehlt sich, die Anzahl benötigter Schrittbefehle zwischen den Endlagen zu zählen und mit der Schrittweite zu multiplizieren.
- **Unterschied Jalousie vs. Rollladen bei der Inbetriebnahme**: Bei "Jalousie" sind zusätzlich Lamellenverstellzeit, Schrittweite und Lamellenposition nach Fahrtende zu parametrieren; bei "Rollladen" entfallen diese, dafür stehen Kurzzeitbetrieb und Single Object Control zur Verfügung. Diese Unterscheidung gilt pro Kanal, nicht pro Gerätevariante – beide Artikelnummern unterstützen beide Betriebsarten gleichermaßen, lediglich die verfügbare Kanalanzahl unterscheidet sich (4 bei JAL-0410M.02, 8 bei JAL-0810M.02).
- **Referenzfahrt vs. Positionsspeicherung**: Wird "Aktuelle Position speichern" nicht genutzt, muss nach jeder Programmierung und jedem Netzspannungsausfall eine Referenzfahrt (manuell oder per Objekt) erfolgen, da der Aktor sonst seinen aktuellen Positionsstatus nicht kennt; bei einer absoluten Positionsfahrt ohne vorherige Referenzfahrt führt der Aktor selbstständig zunächst eine Fahrt in eine Endlage aus, bevor die eigentliche Zielposition angefahren wird.
- **Long-Frame-Programmierung**: Für kürzere Programmierzeiten ab ETS5 wird ein long-frame-fähiges Schnittstellengerät benötigt (z. B. MDT SCN-USBR.01 oder SCN-IP000.02/SCN-IP100.02).
- **Zulassung/Einsatzgebiet**: Die Geräte sind für den Betrieb in der EU und im Vereinigten Königreich zugelassen (CE, UKCA); ein Einsatz in den USA und Kanada ist nicht gestattet.
- **Montage**: Ausschließlich durch Elektrofachkräfte unter Beachtung der länderspezifischen Vorschriften und gültigen KNX-Richtlinien; vor Arbeiten am Gerät ist grundsätzlich über die vorgeschalteten Sicherungen freizuschalten, da nach Einbau und Netzzuschaltung an den Ausgängen Spannung anliegen kann und ein KNX-Telegramm die Ausgänge jederzeit spannungsführend schalten kann.

## Quelle

MDT technologies GmbH, Technisches Handbuch "MDT Jalousieaktor mit Fahrzeitmessung" (JAL-0410M.02 / JAL-0810M.02), Stand 08/2025, Version 1.1.
Originaldatei: `originals/KNX/MDT_THB_JAL_02_Jalousieaktor_Fahrzeitmessung_V11.pdf`
