---
title: Oventrop Regtronic PQ – Frischwasserregler
device_type: Regler für Frischwasserbereitung (eigenständiger Regler, kein KNX-Teilnehmer)
manufacturer: Oventrop / Prozeda GmbH
article_number: Typ 1317 (Regtronic PQ)
bus: kein KNX – eigenständiger Mikrocontroller-Regler mit 230V-Schaltausgängen und PT1000-Fühlereingängen
source_pdf: Reglerbeschreibung_RegtronicPQ_1317BED033-20A-E.pdf
last_updated: 2026-08-01
synonyms: [Regtronic PQ, Frischwasserstation Regler, Oventrop Frischwasserregler, Prozeda Regtronic, Typ 1317]
tags: [heizung, frischwasser, warmwasser, zirkulation, desinfektion, nachheizen, multifunktionsregler, pt1000, wärmetauscher]
---

# Oventrop Regtronic PQ – Frischwasserregler

> **Hinweis zur Einordnung:** Dieses Gerät ist kein KNX-Teilnehmer. Es besitzt keine Kommunikationsobjekte und keine ETS-Parametrierung, sondern wird über ein eigenes Display-/Tastenmenü direkt am Gerät parametriert. Die Gliederung dieses Dokuments weicht daher vom KNX-Standardtemplate ab (statt „Kommunikationsobjekte"/„ETS-Parameter" werden hier „Ein-/Ausgänge" und „Bedienmenü & Parameter" verwendet).

## Übersicht

Der Regtronic PQ ist ein mikrocontrollergesteuerter Regler für Frischwasserstationen. Er sorgt für eine hygienische und energiesparende Warmwasserbereitung über einen Wärmetauscher und hält dabei eine möglichst konstante Warmwasser-Ausgangstemperatur.

Kernfunktionen:
- Regelung auf konstante Warmwasser-Ausgangstemperatur über die Primärpumpe des Wärmetauschers
- Ansteuerung einer Zirkulationsfunktion
- Nachheizen des Pufferspeichers durch eine externe Wärmequelle
- Thermische Desinfektion der Zirkulationsleitung (Legionellenschutz)
- Temperaturmessung, Erfassung der Entnahmemenge (l/min) sowie Verbrauchs- und Energieerfassung
- Optional ein frei konfigurierbarer Multifunktionsregler (Heizen/Kühlen/Differenzregler/Alarm) anstelle der Nachheizfunktion

## Technische Daten

| Kategorie | Wert |
|---|---|
| Material Gehäuse | 100 % recyclingfähiges ABS-Gehäuse für Wandmontage |
| Maße (L x B x T) | 175 x 134 x 56 mm |
| Gewicht | ca. 360 g |
| Schutzart | IP20 nach VDE 0470 (senkrechte Betriebslage) |
| Betriebsspannung | AC 230 V, 50 Hz, -10…+15 % |
| Funkstörgrad | N nach VDE 0875 |
| max. Leitungsquerschnitt 230V-Anschlüsse | 2,5 mm² fein-/eindrahtig |
| Temperaturfühlertyp | PT1000 (1 kΩ bei 0 °C) |
| Messbereich Fühler | -30 °C … +250 °C |
| Prüfspannung | 4 kV, 1 min nach VDE 0631 |
| Schaltspannung | 230 V∼ |
| Leistung je Schaltausgang | 1 A / ca. 230 VA (cos φ = 0,7–1,0) |
| Gesamtleistung aller Ausgänge | 4 A / ca. 900 VA maximal |
| Absicherung | Feinsicherung 5 x 20 mm, 4A/T (träge) |
| Durchflussgeber | PVM 1,5/90, 1500 l/h, Tmax ≥ 90 °C, 40 Impulse/Liter |
| Betriebstemperatur Gerät | 0 … +50 °C |
| Lagertemperatur | -10 … +65 °C |

## Ein-/Ausgänge

### Eingänge (Messstellen)

| Bezeichnung | Funktion | Bemerkung |
|---|---|---|
| T1 | Temperatur Wärmetauscher Primärseite Vorlauf | Bezugsfühler für Betriebsart „WT-Warm" |
| T2 | Temperatur Wärmetauscher Sekundärseite, Warmwasseraustritt | — |
| T3 | Temperatur Wärmetauscher Sekundärseite, Kaltwassereintritt / Zirkulationsrücklauf | Doppelfunktion je nach Anlagenkonfiguration |
| T5 | Temperatur Pufferspeicher oben | Nur für Zusatzfunktion „Nachheizen"; Fühler nicht im Lieferumfang |
| T6 | Temperatur Pufferspeicher Mitte | Nur für Zusatzfunktion „Rückschichten"; Fühler nicht im Lieferumfang |
| DFZ | Digitalsignal Durchflussgeber | Erfassung der Entnahmemenge |

Alle Fühler T1–T6 stehen zusätzlich für die freie Zuordnung im Multifunktionsregler (MFR) zur Verfügung.

### Ausgänge

| Bezeichnung | Funktion | Bemerkung |
|---|---|---|
| A1 | Primärseitige Umwälzpumpe für Wärmetauscher | Elektronisch geschalteter 230V-Ausgang |
| A2 | Umwälzpumpe für Zirkulationsleitung | Elektronisch geschalteter 230V-Ausgang |
| A3 | Anforderungssignal Nachheizfunktion **oder** Ausgang des Multifunktionsreglers | Funktion softwareseitig umschaltbar, siehe Abschnitt „Funktionsumschaltung Ausgang 3" |
| A4 | Ventilansteuerung für temperaturabhängige Speicherrücklaufeinleitung | Elektronisch geschalteter 230V-Ausgang |
| A7 | Potentialfreier Schließer für Sicherheitsabschaltung | Einzig potentialfreier Ausgang; für potentialfreie Nachheiz-Ansteuerung ist ein externes Relais erforderlich |

## Bedienmenü & Parameter

Die Bedienung erfolgt über vier Menüs am Gerätedisplay: **Info**, **Programmieren**, **Handbetrieb** und **Grundeinstellung**. Je nach aktivierten Zusatzfunktionen werden im laufenden Betrieb nur die jeweils relevanten Menüpunkte angezeigt.

| Menü | Zweck |
|---|---|
| Info | Anzeige aller Messwerte, Betriebszustände und Fehlermeldungen (Hauptmenü im Automatikbetrieb) |
| Programmieren | Änderung der laufenden Betriebsparameter (Sollwerte, Zeitfenster) |
| Handbetrieb | Manuelles Ein-/Ausschalten der Ausgänge für Service-/Testzwecke |
| Grundeinstellung | Grundlegende Funktionsauswahl und Systemeinstellungen (nur eingeschränkt editierbar, siehe unten) |

### Menü „Programmieren" (Auszug wichtiger Werte)

| Parameter | Bedeutung |
|---|---|
| Warmwasser Sollwerttemperatur | Sollwert für die Warmwasserbereitung |
| WT-Betriebsart | Betriebsartauswahl für die Wärmetauscherbeladung (Kalt/Warm/Zeitgesteuert) |
| Zeit 1–3: Start/Stopp | Zeitfenster für zeitgesteuerte Wärmetauscherbeladung |
| WT-Sollwert / WT-Hysterese | Sollwert bzw. Hysterese, gültig bei Betriebsart „Warm + Zeitgesteuert" |
| WW-Spitzenwertzeit | Zeitschwelle, nach der bei dauerhaft zu hoher WW-Temperatur ein Fehler generiert wird (nach 3 Fehlern Zwangsabschaltung) |
| Zirkulation VL-Sollwerttemperatur | Sollwert für die Vorlauftemperatur der Zirkulationsleitung |
| Wochenplan | 3 Zeitfenster je Wochentag; im Master-Tag eingegebene Werte werden für alle Wochentage übernommen |
| Nachheizen SP-Sollwerttemperatur | Sollwert für den Start der Heizfunktion des Pufferspeichers |
| Zeit / Datum / Wochentag | Systemuhr |
| Zeitumstellung | Automatische Sommer-/Winterzeit-Umstellung Ein/Aus |

### Menü „Handbetrieb"

| Punkt | Funktion |
|---|---|
| Ausgang 1–4 | Manuelles Ein-/Ausschalten (Ausgang 1 schaltet A7 mit) |
| Ausgang 7 | Manuell schaltbar, nur wenn Ausgang 1 ausgeschaltet ist |
| Kennlinienabgleich | Startet den automatischen Systemabgleich (Läuft/Aus) |
| Zirkulationsabgleich | Ermittelt den Zirkulationsdurchfluss (Läuft/Aus) |

Im Handbetrieb erfolgt keine automatische Regelung; nach ca. 8 Stunden schaltet der Regler automatisch zurück ins Menü „Info" mit aktiver Regelung, um unzulässige Betriebszustände zu vermeiden.

### Menü „Grundeinstellung" (Service-/Systemebene)

| Untermenü | Parameter | Bemerkung |
|---|---|---|
| Regler-Info | System-Nr., System-Ver., Software-Nr., Software-Ver. | Identifikation von Anlagenschema und Softwarestand |
| Regler (nach Servicefreischaltung) | Ein, WW-max, VL DeltaT, P10–P60 | Grundlegende Reglerfreigabe und Regelparameter |
| Kennlinie | Durchfluss/Leistung min/mid/max, Korrektur, Abgl. T-VL, Abgl. T-KW, Abgl. T-WWsoll, Regelanteil | Ergebniswerte des Systemabgleichs bzw. manuelle Feinjustage |
| Reglermodus | Normal / Gleittemperatur / Wärmepumpe | Auswahl des Regelungstyps, siehe Abschnitt „Regelungsarten" |
| Zirkulation | Ein, Zirk. Modus, Laufzeit, Ruhezeit, Abschaltdifferenz | Grundparameter der Zirkulationsfunktion |
| Funktionsauswahl A3 | Nachheizen / Multireg | Legt fest, welche Funktion Ausgang A3 nutzt |
| Nachheizen | Ein, SP-Sollwert (Absolut/Relativ) | Absolut = fester Sollwert; Relativ = WW-Sollwert bzw. Desinfektionssollwert + Spreizung |
| Rückschichtung | Ein | Temperaturabhängige Umleitung des Speicherrücklaufs |
| Verbrauchserfassung | Ein, Anzeige (Reset) | Berechnung läuft immer, Anzeige nur bei „Ein" |
| Desinfektion | Ein, Sollwert, Laufzeit, Start (Tag), Start (Zeit) | Nur aktivierbar bei vorhandener und eingeschalteter Zirkulation |
| Multireg | Ein, Heizen, Kühlen, Differenzregler, Alarm | Bei aktiver Funktion wird A3 mit 230V geschaltet |
| Werkskonfiguration | Werkseinstell., Freigabe, Ausgangsüberw., Parameter | Werksreset, Servicemenü-Freigabe, Rücklesbarkeit A1, Parameter-Sicherung auf DataStick |
| Systemauswahl | Aus | Funktionsauswahl, nur bei Multifunktionssystemen relevant |

**Wichtig zur Editierbarkeit:** Das Menü „Grundeinstellung" ist im Normalbetrieb nur zur Anzeige sichtbar und gegen versehentliche Änderungen gesperrt. Editierbar ist es nur, wenn es innerhalb der ersten Minute nach dem Einschalten des Geräts angewählt wird – dann zeitlich unbegrenzt. Es verriegelt sich automatisch wieder eine Minute nach Verlassen des Menüs bzw. eine Minute nach dem Einschalten.

## Regelfunktionen

### Frischwasserbereitung über Wärmetauscher

Der Regler hält die Warmwasser-Austrittstemperatur am Wärmetauscher möglichst konstant. Energiequelle ist ein Pufferspeicher mit einer möglichst gleichbleibenden Temperatur (typisch 60–85 °C, mindestens jedoch 3 K über dem Warmwasser-Sollwert); eine variable Speichertemperatur wird ebenfalls unterstützt. Die Primärpumpe wird drehzahlgeregelt angesteuert, um die gewünschte Temperatur zu halten – die übliche Regelgenauigkeit liegt bei ±2 K vom Sollwert. Bei sehr geringen Durchflussmengen (unter ca. 15 % der maximalen Durchflussmenge) sind aus physikalischen Gründen größere Abweichungen zu erwarten.

Bei Zapfbeginn mit ausgekühlten Leitungen steuert der Regler die Primärpumpe für eine berechnete Zeit mit 100 % an; die Dauer ergibt sich aus der Abweichung der aktuellen Warmwassertemperatur am Fühler T2. Steht über 5 Minuten keine ausreichende Vorlauftemperatur zur Verfügung, erscheint eine Fehlermeldung. Im Wärmepumpenmodus läuft die Primärpumpe grundsätzlich mit 100 %, in den Modi Normal und Gleittemperatur zapfmengenproportional.

#### Regelungsarten

- **Standardregelung (Normal):** Es wird auf die eingestellte Warmwasser-Solltemperatur geregelt. Die Vorlauftemperatur muss dabei um den Parameter „VL_DeltaT" (Werkseinstellung 3 K) über dem Sollwert liegen. Unterschreitet die Vorlauftemperatur diesen Wert, arbeitet die Primärpumpe zapfmengenabhängig; nach 5 Minuten erscheint die Fehlermeldung „VL zu niedrig".
- **Gleitende Temperaturregelung:** Reicht die Vorlauftemperatur nicht mehr für den Sollwert plus VL_DeltaT, senkt der Regler die Warmwasser-Regeltemperatur automatisch ab, wobei die Differenz VL_DeltaT zur Vorlauftemperatur konstant erhalten bleibt. Die Absenkung endet spätestens bei einer Regeltemperatur von 37 °C; erst danach erfolgt nach 5 Minuten die Fehlermeldung „VL zu niedrig".
- **Wärmepumpenregelung:** Bei eingestellter Warmwassersolltemperatur unter 45 °C und unzureichender Vorlauftemperatur läuft die Primärpumpe zunächst kurz zapfmengenangepasst, danach mit voller Leistung, bis die Zapfung endet oder die Vorlauftemperatur wieder ausreicht. In diesem Modus sollte die Zusatzfunktion „Nachheizen" aktiviert und deren Sollwert entsprechend angepasst sein.

#### Betriebsarten für die Wärmetauscherbeladung

- **Wärmetauscher – Kalt:** Der Wärmetauscher bleibt im Ruhezustand kalt; A1 wird nur bei sekundärseitiger Entnahme aktiviert.
- **Wärmetauscher – Warm:** Der Wärmetauscher wird laufend auf einer konstanten Betriebstemperatur (Bezugsfühler T1) gehalten. Bei Unterschreitung von WT-Sollwert minus Hysterese aktiviert der Regler A1 mit 25 % Leistung, bis der Sollwert wieder erreicht ist. Dadurch kann bei einer Warmwasserentnahme sofort mit der berechneten Pumpenleistung geregelt werden.
- **Wärmetauscher – Zeitgesteuert:** Entspricht der Betriebsart „Warm", jedoch begrenzt auf 3 einstellbare Zeitfenster.

#### Systemabgleich

Bei üblicher Anlagenauslegung genügt die Werkseinstellung. Weicht die Anlage ab (z. B. geringere Leitungsquerschnitte, stark abweichende Speicher-/Kaltwassertemperaturen), kann ein Systemabgleich die Regelung optimieren. Dabei wird die Pumpenleistung an drei Arbeitspunkten ermittelt.

Voraussetzungen für einen guten Abgleich:
- Speichertemperatur auf dem später verwendeten Niveau
- konstante Kaltwasser-Zulauftemperatur (ggf. vorher etwas Wasser laufen lassen)
- alle Absperrhähne in der späteren Betriebsstellung
- Wahlschalter der Zirkulationspumpenleistung auf dem benötigten Wert (Stufenschalter stets auf Stufe 3)

Ablauf: Menü „Handbetrieb" → „Kennlinienabgleich" → Punkt einschalten → Menüanweisungen folgen → nach Meldung „fertig" sind die ermittelten Werte im Menü „Grundeinstellungen/Kennlinie" gespeichert → Menü mit „ESC" verlassen. Der Vorgang kann je nach Anlage mehrere Minuten dauern. Ein integrierter Korrekturmechanismus sorgt auch bei sich ändernden Bedingungen laufend für ein optimiertes Ergebnis.

### Zirkulation

Zusätzlich zur Frischwasserbereitung stehen 5 Zirkulationsmodi zur Auswahl (im Menü „Grundeinstellung"), jeweils bezogen auf innerhalb/außerhalb eines Zeitfensters:

| Modus | Verhalten |
|---|---|
| Aus | Keine Zirkulation |
| Dauer/Aus | Dauerbetrieb / keine Zirkulation |
| Dauer/Bedarf | Dauerbetrieb / bedarfsgesteuert |
| Temp/Aus | Temperaturgesteuert / keine Zirkulation |
| Temp/Bedarf | Temperaturgesteuert / bedarfsgesteuert |

Ist die Funktion aktiviert, lassen sich im Menü „Programmieren" 3 Zeitfenster pro Tag mit individueller Start-/Endzeit festlegen.

- **Temperaturgesteuert:** Die Zirkulationspumpe schaltet ein, sobald der Zirkulationsrücklauffühler die berechnete Schaltschwelle (Zirkulations-VL-Sollwert minus Abschaltdifferenz) um 3 K unterschreitet, und schaltet bei Überschreitung wieder aus.
- **Bedarfsgesteuert:** Ein kurzes Öffnen und Schließen eines Wasserhahns (1–3 Sekunden) löst die Zirkulationspumpe für die programmierte Laufzeit aus. Eine erneute Aktivierung ist erst nach Ablauf der Ruhezeit möglich.
- **Dauerbetrieb:** Die Pumpe läuft während des gesamten aktiven Zeitfensters und wird nur durch eine Zapfung unterbrochen.

Eine Zapfung oder ein auftretender Fehler unterbricht die Zirkulationsfunktion in jedem Modus. Der Parameter „Zirkulation VL-Sollwert" ist an den „Warmwasser Sollwert" gekoppelt: Bei dessen Änderung verschiebt sich der Zirkulationswert gleichsinnig, die ursprüngliche Differenz bleibt erhalten.

**Verwendete Eingänge:** T2 (Warmwasseraustritt), T3 (Zirkulationstemperatur/Kaltwassereintritt), DFZ (Durchflussgeber)
**Verwendete Ausgänge:** A1 (Primärpumpe WT), A2 (Zirkulationspumpe)

#### Abgleich Zirkulation

Damit der Regler eine Entnahmemenge erkennen kann, muss ihm die Umwälzleistung der Zirkulationspumpe bekannt sein ("Anlernen"). Voraussetzung: alle Entnahmestellen sind geschlossen. Ablauf: Menü „Handbetrieb" → „Zirkulationsabgleich" → Punkt einschalten → Menüanweisungen folgen → nach Meldung „fertig" wird der gemessene Wert angezeigt und gespeichert → Menü mit „ESC" verlassen.

### Funktion Rückschichtung

Ist die Anlage mit einem Dreiwege-Verteilventil ausgestattet, lässt sich diese Zusatzfunktion im Menü „Grundeinstellung" aktivieren. Das Ventil schaltet die Rücklaufeinspeisung in den mittleren Speicherbereich, wenn die Zirkulationsrücklauftemperatur mindestens der Temperatur am Fühler „Speicher Mitte" entspricht und die Zirkulationspumpe läuft. Unterschreitet die Rücklauftemperatur die Speicher-Mitte-Temperatur um 1 K, oder ist die Zirkulationspumpe aus, leitet das Ventil den Rücklauf stattdessen in den unteren Speicherbereich.

**Verwendete Eingänge:** T3 (Zirkulationsrücklauf), T6 (Speicher Mitte)
**Verwendeter Ausgang:** A4 (Dreiwege-Verteilventil)

### Funktion Verbrauchserfassung

Die Berechnung von Warmwasserverbrauch und zugehörigem Energieverbrauch läuft grundsätzlich immer; die Zusatzfunktion schaltet lediglich deren Anzeige im Menü „Info" frei. Angezeigt werden Gesamt- und Tagesverbrauch an Warmwasser (m³) sowie an Energie (kWh), bezogen auf die gezapfte Warmwassermenge. Der Tagesverbrauch wird beim Uhrzeitwechsel von 23:59 auf 00:00 zurückgesetzt, der Gesamtverbrauch kann im Menü „Grundeinstellung" manuell zurückgesetzt werden (z. B. nach Jahresablesung, Verriegelung beachten).

Messumfang: 655 m³ bzw. 6553 kWh. Messtoleranz: ca. 5 %, bedingt durch die Streuung von Temperaturfühler und Durchflusssensor.

> ⚠️ **Wichtig:** Die Geräte sind nicht kalibriert und dürfen nicht zur Abrechnung von Mietnebenkosten oder Ähnlichem verwendet werden. Die Anzeige dient nur zur Orientierung.

### Funktion Desinfektion

> ⚠️ **Sicherheitshinweis:** Bei eingeschalteter Funktion besteht während und bis ca. 1 Stunde nach dem Desinfektionsvorgang Verbrühungsgefahr. Die Funktionszeit ist so zu legen, dass keine unbeaufsichtigte Wasserentnahme stattfindet. Die Warmwasserbegrenzung während der Desinfektion ist auf die maximal zulässige Rohrleitungstemperatur der bestehenden Installation abzustimmen.

Die Desinfektion lässt sich im Menü „Grundeinstellung" nur aktivieren, wenn ein Zirkulationsleitungsnetz vorhanden und die Zirkulationsfunktion eingeschaltet ist. Einstellbar sind Solltemperatur, Dauer und Startzeitpunkt (bestimmter Wochentag oder täglich).

Maßgeblich für die Funktion ist die Zirkulationsrücklauftemperatur am Fühler T3; diese muss für die eingestellte Zeitdauer erreicht werden. Kurzzeitige Unterschreitungen werden ausgeregelt – gezählt wird nur die effektive Zeit auf Solltemperatur. Die Warmwassertemperatur wird während der Desinfektion automatisch geregelt, kann aber auf einen Maximalwert begrenzt werden.

Ist die Funktion „Nachheizen" aktiviert (Betriebsart „relativ"), kann vor Desinfektionsbeginn eine einstellbare Vorheizzeit gestartet werden: Der Speicher wird dabei auf Desinfektionssollwert zuzüglich Vorlauferhöhung (aus der Zirkulations-Abschaltdifferenz) und Spreizung (Nachheizeinstellung) aufgeheizt. Reicht die Vorlauftemperatur für die Regelung nicht aus, erscheint nach 5 Minuten die Fehlermeldung „T-VL zu niedrig"; die Desinfektion pausiert dann für 15 Minuten, wird aber wieder freigegeben, sobald die Vorlauftemperatur ausreicht – spätestens jedoch nach 1 Stunde (dann wird auch die Fehlermeldung gelöscht).

Werden während der Desinfektion Zapfstellen zu deren Desinfektion geöffnet, regelt der Regler weiterhin auf die Desinfektionstemperatur; die Zeiterfassung läuft weiter, solange die Solltemperatur am Warmwasserausgang nicht unterschritten wird. Nach Erreichen der eingestellten Desinfektionsdauer läuft die Funktion noch 10 Minuten nach und endet dann (oder durch manuelles Ausschalten im Menü „Grundeinstellung"). Für die gesamte Desinfektion steht ein Zeitrahmen von maximal 120 Minuten zur Verfügung; wird die Solltemperatur bei ausreichender Vorlauftemperatur bis dahin nicht für die effektive Zeit erreicht, erscheint die Fehlermeldung „T-VL Desinfekt" im Menü „Info". Diese Meldung lässt sich über die rechte Taste zurücksetzen.

### Funktionsumschaltung für Ausgang 3

Die Belegung von Ausgang A3 ist per Software umschaltbar zwischen „Nachheizen" und „Multifunktionsregler" (Einstellung im Menü „Grundeinstellung" unter „Funktion Ausgang 3"). Die jeweils nicht angewählte Funktion wird im Menü ausgeblendet.

#### Funktion: Nachheizen

Diese Zusatzfunktion vergleicht einen einstellbaren Sollwert mit der Temperatur am Pufferfühler und gibt an Ausgang A3 eine Spannung aus, um eine externe Wärmequelle zum Nachheizen des Pufferspeichers auf das Sollniveau einzuschalten. Voraussetzung ist, dass die externe Wärmequelle das gewünschte Temperaturniveau tatsächlich liefern kann.

Der Sollwert für die Speichertemperatur ist wählbar:
- **Absolut:** fester, einstellbarer Temperaturwert
- **Relativ:** gleitender Wert, gekoppelt an Warmwasser-Sollwert bzw. Desinfektionssollwert plus einstellbare Spreizung

Wird der Sollwert um 3 K unterschritten, aktiviert der Regler die externe Wärmequelle, bis der Sollwert wieder erreicht ist. Im Zusammenhang mit der Desinfektionsfunktion kann vor deren Start eine Nachheizanforderung gestartet werden, damit der Pufferspeicher eine ausreichende Vorlauftemperatur für die thermische Desinfektion liefern kann.

**Verwendeter Eingang:** T5 (Speichertemperatur oben) – als normaler PT1000-Tauchfühler ausführbar; Fühler ist nicht im Lieferumfang enthalten und wird nur für diese Funktion benötigt.
**Verwendeter Ausgang:** A3 (230V-Anforderungssignal)

#### Multifunktionsregler (MFR/MultiReg)

Der Multifunktionsregler nutzt denselben Ausgang A3 wie die Nachheizfunktion; die Auswahl zwischen beiden erfolgt im Menü „Grundeinstellung". Er erlaubt dem Anwender, eine Reihe unterschiedlicher Zusatzfunktionen auf dem zugeordneten Schaltausgang zu realisieren:

- freie Wahl der Temperaturfühler für Wärmequelle und -abnehmer (T1 bis T6)
- funktionale Variabilität durch Auswahl der gewünschten Betriebsart
- Regelbetrieb innerhalb mehrerer Zeitfenster möglich

Wählbare Funktionen auf Ausgang A3: **Heizen**, **Kühlen**, **Differenzregler**, **Alarm**.

##### Heizen

Unterschreitet die gemessene Temperatur den Sollwert, schaltet A3 ein, bis die gemessene Temperatur den Sollwert minus Hysterese erreicht.

| | |
|---|---|
| Eingang | Temperatur Speicher oben |
| Ausgang | A3 |
| Anzeigewerte | Info: Heizen; Funktion aktiv: Heizen |
| Programmierwerte | MultiReg: Heizen; Zeit 1–3 Start/Stopp; Start; Stopp |
| Grundeinstellung | MultiReg Funktion: Heizen |

##### Kühlen

Überschreitet die gemessene Temperatur den Sollwert, schaltet A3 ein, bis die gemessene Temperatur den Sollwert minus Hysterese unterschreitet (invertierte Logik zu „Heizen").

| | |
|---|---|
| Eingang | Temperatur Speicher oben |
| Ausgang | A3 |
| Anzeigewerte | Info: Kühlen; Funktion aktiv: Kühlen |
| Programmierwerte | MultiReg: Kühlen; Start; Stopp |
| Grundeinstellung | MultiReg Funktion: Kühlen |

##### Differenzregler

Frei konfigurierbarer Temperaturdifferenzregler mit fest zugeordnetem Ausgang. Übersteigt die Differenz zwischen zwei frei wählbaren Temperaturfühlern die eingestellte Hysterese, schaltet A3 ein. Zusätzlich sind eine Maximaltemperatur für den Energieabnehmer und eine Minimaltemperatur für die Energiequelle definierbar.

| | |
|---|---|
| Eingänge | 2 frei zuordenbare Temperaturfühler |
| Ausgang | A3 |
| Anzeigewerte | Info: Diff.-Regler; Funktion aktiv: Diff.-Regler |
| Programmierwerte | MultiReg: Diff.-Regler; maximal (Maximaltemperatur Abnehmer); minimal (Mindesttemperatur Quelle); dTmax; dTmin; Zeit 1–3 Start/Stopp |
| Grundeinstellung | MultiReg Funktion: Diff.-Regler; Fühler Quelle; Fühler Abnehmer |

##### Alarm

Erkennt der Regler eine Störung (z. B. Fühlerkurzschluss oder -unterbrechung), aktiviert er bei eingeschalteter Alarmfunktion Ausgang A3. Das Signal kann z. B. von einer Gebäudeleittechnik erfasst und angezeigt werden.

| | |
|---|---|
| Eingang | – |
| Ausgang | A3 – 230V-Ausgang, z. B. für Sirene oder Blinklicht |
| Anzeigewerte | Funktion aktiv: Alarm |
| Programmierwerte | MultiReg: Alarm; Signaldauer (getaktet); Zeit 1–3 Start/Stopp |
| Grundeinstellung | MultiReg Funktion: Alarm |

### Notabschaltung

Durch eine spezielle Verkabelung der Primärpumpe – die Pumpenspannung wird zusätzlich über den Relaiskontakt A7 geführt – entsteht zusätzliche Sicherheit gegen Überhitzung des Wärmetauschers bei einem Defekt des elektronischen Ausgangs A1. Im Normalbetrieb werden A1 und A7 bei einer Pumpenansteuerung gleichzeitig aktiviert.

Die Notabschaltung greift, wenn die Temperatur am Warmwasserausgang den im Menü „Programmieren" eingestellten Sollwert um 10 K übersteigt (bzw. 7 K, wenn der WW-Sollwert über 55 °C liegt). Liegt die Warmwassertemperatur dauerhaft über dem Sollwert, wird nach der eingestellten Spitzenwertzeit ein Merker gesetzt; nach 3 solchen Ereignissen wird der Sicherheitsausgang A7 dauerhaft abgeschaltet. Die Reaktivierung erfolgt erst wieder um Mitternacht oder wenn der Regler mindestens 5 Sekunden vom Netz getrennt wurde.

**Verwendeter Ausgang:** A7 (Sicherheitsabschaltung)

### Notbetrieb

Fallen Fühler aus und läuft die Warmwasserregelung nicht mehr ordnungsgemäß, kann die Beladung des Wärmetauschers über einen Notbetrieb erfolgen. Der Notbetrieb wird durch gleichzeitiges kurzes Betätigen der rechten und linken Taste aufgerufen; anschließend lässt sich die Pumpenleistung manuell über die Auf-/Ab-Tasten erhöhen bzw. senken. Ein erneutes Betätigen der linken Taste verlässt den Menüpunkt wieder und setzt die Pumpenleistung zurück.

> ⚠️ In diesem Betriebsmodus muss die Vorlauftemperatur manuell begrenzt werden – es findet keine automatische Überwachung statt.

## Störungsbehebung

### Störungen mit Fehlermeldung (Symbol „!" blinkend)

| Fehlerdarstellung | mögliche Ursachen | Maßnahmen |
|---|---|---|
| „!" blinkend | Fühlerleitung unterbrochen; Fühler defekt | Leitung prüfen; Fühlerwiderstand prüfen, ggf. Fühler austauschen |
| „!" blinkend | Kurzschluss in der Fühlerleitung; Fühler defekt | Leitung prüfen; Fühlerwiderstand prüfen, ggf. Fühler austauschen |
| „!" blinkend, Fehlertext im Menü „Info": „Fühler" | Fühler defekt | Fühlerleitung überprüfen |
| „!" blinkend, Fehlertext: „Ausgang1" | Defekt des Pumpensteuerausgangs | Ansteuerbaugruppe austauschen lassen |
| „!" blinkend, Fehlertext: „T-VL Desinfekt" | zu geringe Vorlauftemperatur für Desinfektion | Speicher nachheizen |
| „!" blinkend, Fehlertext: „VL zu niedrig" | zu geringe Vorlauftemperatur | Speicher nachheizen |
| „!" blinkend, Fehlertext: „Pumpenfehler" | Primärpumpe oder Ansteuerausgang defekt | Ausgang 1 und Pumpe überprüfen; Ansteuerbaugruppe austauschen lassen |

### Störungen ohne Fehlermeldung

| Fehlerbild | mögliche Ursachen | Maßnahmen |
|---|---|---|
| Keine Anzeigenfunktion | 230V-Netzspannung nicht vorhanden | Regler einschalten/anschließen; Haussicherung prüfen |
| Keine Anzeigenfunktion | geräteinterne Sicherung defekt | Sicherung prüfen, ggf. durch neuen Typ 2A/T ersetzen; 230V-Komponenten auf Kurzschluss prüfen |
| Keine Anzeigenfunktion | Gerät defekt | Rücksprache mit dem Lieferanten |
| Regler arbeitet nicht | Regler ist im Handbetrieb | Menü „Handbetrieb" verlassen |
| Regler arbeitet nicht | Einschaltbedingung nicht erfüllt | Warten, bis Einschaltbedingung erfüllt ist |
| Symbol „Pumpe" dreht, Pumpe arbeitet aber nicht | Anschluss zur Pumpe unterbrochen | Kabel zur Pumpe prüfen |
| Symbol „Pumpe" dreht, Pumpe arbeitet aber nicht | Pumpe sitzt fest | Pumpe gängig machen |
| Symbol „Pumpe" dreht, Pumpe arbeitet aber nicht | keine Spannung am Schaltausgang | Rücksprache mit dem Lieferanten |
| Temperaturanzeige schwankt stark in kurzen Zeitabständen | Fühlerleitungen nahe 230V-Leitungen verlegt | Fühlerleitungen anders verlegen bzw. abschirmen |
| Temperaturanzeige schwankt stark in kurzen Zeitabständen | lange Fühlerleitungen ohne Schirmung verlängert | Fühlerleitungen abschirmen |
| Temperaturanzeige schwankt stark in kurzen Zeitabständen | Gerät defekt | Rücksprache mit dem Lieferanten |

**Software-Reset** (ohne Parameteränderung): gleichzeitig die Tasten Rechts und Links drücken, anschließend einmal die Taste Links.

## Widerstandstabelle PT1000

| Temperatur (°C) | Widerstand (Ω) | Temperatur (°C) | Widerstand (Ω) |
|---|---|---|---|
| -10 | 960 | 60 | 1232 |
| 0 | 1000 | 70 | 1271 |
| 10 | 1039 | 80 | 1309 |
| 20 | 1077 | 90 | 1347 |
| 30 | 1116 | 100 | 1385 |
| 40 | 1155 | 120 | 1461 |
| 50 | 1194 | 140 | 1535 |

## Inbetriebnahme / Sicherheitshinweise

- Montage- und Verdrahtungsarbeiten am Regler dürfen nur im spannungslosen Zustand erfolgen. Anschluss und Inbetriebnahme dürfen nur durch fachkundiges Personal unter Beachtung der geltenden nationalen und örtlichen Sicherheitsbestimmungen erfolgen.
- Die Anschlüsse des Schutzkleinspannungsbereichs (Fühler, Durchflussgeber) dürfen niemals mit den 230V-Anschlüssen vertauscht werden – es besteht sonst Gefahr von Zerstörung und lebensgefährlicher Spannung an Gerät und angeschlossenen Fühlern/Geräten.
- Bei der Montage der Temperaturfühler besteht Verbrennungsgefahr, da die Anlage hohe Temperaturen erreichen kann.
- Verbrühungsgefahr während und bis ca. 1 Stunde nach der Desinfektion (siehe Abschnitt „Funktion Desinfektion").
- Der Regler ist so zu montieren, dass keine unzulässigen Betriebstemperaturen (> 50 °C) durch Wärmequellen entstehen; die Montage muss an einem trockenen Ort erfolgen, da der Regler nicht spritz- und tropfwassergeschützt ist (Schutzart IP20).
- Der Handbetrieb darf aus Sicherheitsgründen nur zu Testzwecken genutzt werden, da in diesem Modus keine Maximaltemperaturen und Fühlerfunktionen überwacht werden.
- Bei erkennbaren Schäden am Regler, an Kabeln oder an angeschlossenen Pumpen/Ventilen darf die Anlage nicht in Betrieb genommen werden.
- Verrohrung, Dämmung, Pumpen und Ventile müssen für die in der Anlage auftretenden Temperaturen geeignet sein.

**Gehäuse öffnen:** Kein Werkzeug nötig. Das Gehäuseoberteil rastet in das Unterteil ein; durch leichtes Ziehen an den Seitenlaschen lässt es sich entriegeln und nach oben aufklappen, bis es einrastet.

**Hinweis DVGW W551:** Der Hersteller verweist auf die Vorgaben der Deutschen Vereinigung des Gas- und Wasserfaches (DVGW), Arbeitsblatt W551, bezüglich Planung, Anforderungen und Betrieb von Trinkwassererwärmungs- und Leitungsanlagen. Der Hersteller schließt jede Haftung für Schäden aus, die infolge von Fehlern bei Installation, Einstellung oder Bedienung auftreten.

**Konformität:** Hersteller ist die Prozeda GmbH. Das Produkt (Regtronic Typ 1317) erfüllt die Anforderungen der Richtlinien zur elektromagnetischen Verträglichkeit (2004/108/EG), zu elektrischen Betriebsmitteln innerhalb bestimmter Spannungsgrenzen (2006/95/EG) sowie zur CE-Kennzeichnung (93/68/EWG). Angewandte Normen: DIN EN 60730-1, DIN EN 61326-1, DIN EN 61326-2-2.

## Quelle

Oventrop Regtronic PQ – Reglerbeschreibung (Montage- und Bedienungsanleitung), Prozeda GmbH, Dokument-Nr. 138106081, 1317BED033-20A-E, Stand 01/2012.
