---
title: MDT Heizungsaktor AKH-0800.03
device_type: Heizaktor
manufacturer: MDT
article_number: [AKH-0800.03]
bus: KNX TP
source_pdf: originals/KNX/MDT_THB_AKH_03_Heizungsaktor_V12.pdf
last_updated: 2026-07-24
synonyms: [Heizungsaktor, Stellantriebsaktor, Heizungsstellantrieb, Ventilaktor, Heizkreisaktor, Stellantriebssteuerung, Heizungsventilaktor]
tags: [knx, heizaktor, mdt, ventilsteuerung, heizungsregelung, raumtemperaturregelung]
---

## Übersicht

Der MDT Heizungsaktor der Serie AKH-0x00.03 ist eine KNX-Aktorlinie zur Ansteuerung von elektrothermischen Stellantrieben (Heizkörperventile, Fußbodenheizkreise, Kühldecken etc.). Er ist in drei Baugrößen erhältlich:

| Typ | Kanäle | Baubreite | Versorgung |
|---|---|---|---|
| AKH-0400.03 | 4 | 2 TE REG | 24–230 V AC |
| AKH-0600.03 | 6 | 3 TE REG | 24–230 V AC |
| **AKH-0800.03** | **8** | **4 TE REG** | **24–230 V AC** |

Dieses Dokument bezieht sich auf **AKH-0800.03** (8 Kanäle). Alle Angaben zu Kommunikationsobjekten, Funktionsblöcken und Parametern gelten baugleich für die gesamte Serie; Unterschiede bestehen nur in der Kanalanzahl und in den daraus resultierenden Objektnummern (siehe Abschnitt Kommunikationsobjekte).

Jeder Kanal kann wahlweise in einer von drei Regelungsarten betrieben werden:
- **Schaltend (1 Bit):** Der Kanal ist "passiv" und übernimmt einen extern berechneten, bereits schaltenden Stellwert (0/1), z. B. von einem Zweipunktregler.
- **Stetig (1 Byte):** Der Kanal ist ebenfalls "passiv" und wandelt einen extern übergebenen Prozent-Stellwert (0–100 %) intern per PWM in ein Schaltsignal um.
- **Integrierter Regler:** Der Kanal ist "aktiv" – er empfängt nur einen Ist-Temperaturwert (z. B. vom Glastaster mit Temperaturfühler) und berechnet Sollwert, Regelabweichung sowie Stellgröße selbst (2-Punkt- oder PI-Regler).

Zusätzlich bietet der Aktor u. a. einen Festsitzschutz für Ventile, eine Klartext-Diagnosefunktion pro Kanal, eine Energieoptimierung über Pumpenabschaltung (Heiz-/Kühlanforderung), automatische Sommer/Winter- bzw. Heizen/Kühlen-Umschaltung, eine erweiterte Sollwertverschiebung sowie eine Szenenfunktion.

## Technische Daten

| Merkmal | Wert |
|---|---|
| Artikelnummer (dieses Dokument) | AKH-0800.03 |
| Kanäle | 8, zur Steuerung elektrothermischer Stellantriebe |
| Baubreite | 4 TE, Reiheneinbaugerät (REG) |
| Versorgungsspannung | 24 V AC **oder** 230 V AC (pro Gerät nur eine der beiden Spannungen zulässig, keine Mischung) |
| Betriebsspannungsart | zwingend Wechselspannung (Ausgänge sind TRIACs, keine Gleichspannung möglich) |
| Anschluss Phasen | 8-fach: eine gemeinsame Phase für Kanäle A–D, eine weitere für Kanäle E–H |
| Statusanzeige | grüne Kanal-LED je Kanal (Schaltzustand + Störungscodes), rote Programmier-LED |
| Bedienelement | Programmiertaste (>1 s: Programmiermodus, >5 s: Testbetrieb) |
| Testbetrieb | bestromt alle aktiven Kanäle nacheinander für je 3 Minuten; Weiterschalten per kurzem Tastendruck, Abbruch am letzten Kanal per kurzem Tastendruck |
| Diagnose | 14-Byte-Klartext-Diagnoseobjekt je Kanal, Sprache Deutsch/Englisch wählbar |
| Programmierung | Long-Frame-fähig (schnellere ETS5-Programmierung, erfordert Long-Frame-fähiges Interface, z. B. MDT SCN-IP100.03 / SCN-IP000.03 / SCN-USBR.02) |
| Update | Firmware-Update über MDT Update Tool (DCA) möglich |

**Wichtiger Sicherheitshinweis (Netzstörungserkennung):** Beim 8-fach-Aktor werden die Kanäle A–D sowie E–H jeweils gemeinsam mit einer Phase versorgt. Kanal A (für die Gruppe A–D) und Kanal E (für die Gruppe E–H) müssen zwingend als erste Kanäle der jeweiligen Gruppe belegt/aktiviert werden – andernfalls erkennt der Aktor fälschlich eine Störung und alle Kanal-LEDs blinken gleichzeitig.

## Kommunikationsobjekte

### Nummerierungsschema

Die Kommunikationsobjekte gliedern sich in **kanalbezogene Objekte** (pro Kanal ein eigener Satz, Nummernblock rückt je Kanal um 40 weiter) und **zentrale/geräteweite Objekte** (am Ende der Objektliste, Nummer abhängig von der Kanalanzahl des Geräts).

Kanalbezogene Nummern (Basis = Kanal A, Objekte 1–38). Für AKH-0800.03 ergibt sich pro Kanal ein Versatz von +40:

| Kanal | Versatz zu Kanal A |
|---|---|
| A | +0 |
| B | +40 |
| C | +80 |
| D | +120 |
| E | +160 |
| F | +200 |
| G | +240 |
| H | +280 |

Beispiel: "Eingang Stellwert" ist bei Kanal A Objekt Nr. 1, bei Kanal E entsprechend Nr. 161.

### Standard-Objekte pro Kanal (Basis Kanal A)

| Nr. | Funktion | DPT/Größe | Regelungsart | Flags (Standard) |
|---|---|---|---|---|
| 1 | Eingang Stellwert | 1 Bit | schaltend | K, S, Ü, A |
| 1 | Eingang Stellwert | 1 Byte | stetig | K, S, Ü, A |
| 1 | Temperaturwert empfangen | 2 Byte | integrierter Regler | K, S, Ü, A |
| 2 | Sollwert vorgeben | 2 Byte | integrierter Regler | K, S |
| 3 | Komfort Sollwert vorgeben / (Basis) Komfort Sollwert vorgeben | 2 Byte | integrierter Regler | K, S |
| 3 | Kombiobjekt: Sollwert vorgeben / Kombiobjekt (Heizen): Sollwert vorgeben | 8 Byte | integrierter Regler | K, S |
| 4 | Standby Sollwert vorgeben | 2 Byte | integrierter Regler | K, S |
| 5 | Nacht Sollwert vorgeben | 2 Byte | integrierter Regler | K, S |
| 6 | Hitzeschutz-/Frostschutz Sollwert vorgeben | 2 Byte | integrierter Regler | K, S |
| 7 | Kombiobjekt (Kühlen): Sollwert vorgeben | 8 Byte | integrierter Regler | K, S |
| 8 | Aktueller Sollwert senden | 2 Byte | integrierter Regler | K, S, Ü |
| 9 | Manuelle Sollwertverschiebung (2 Byte) | 2 Byte | integrierter Regler | K, S |
| 10 | Manuelle Sollwertverschiebung (1=+/0=-) | 1 Bit | integrierter Regler | K, S |
| 10 | Manuelle Sollwertverschiebung (1 Byte) | 1 Byte | integrierter Regler | K, S |
| 11 | Status Sollwertverschiebung senden | 2 Byte | integrierter Regler | K, S, Ü |
| 12 | Stellwert / Stellwert Heizen: Status senden | 1 Byte | stetig / integrierter Regler | K, S, Ü |
| 13 | Stellwert Kühlen: Status senden | 1 Byte | stetig / integrierter Regler | K, S, Ü |
| 14 | Stellwert > 0 %: Status senden | 1 Bit | stetig / integrierter Regler | K, S, Ü |
| 15 | Ventilzustand senden (1=geöffnet, 0=geschlossen) / Ventilzustand Heizen senden | 1 Bit | alle | K, S, Ü |
| 16 | Zusatzstufe: Stellwert Heizen senden | 1 Bit | integrierter Regler (Heizen, Zusatzstufe aktiv) | K, S, Ü |
| 17 | Betriebsartvorwahl | 1 Byte (DPT 20.102) | integrierter Regler | K, S |
| 18 | Betriebsart Komfort: Komfortverlängerung | 1 Bit | integrierter Regler | K, S |
| 19 | Betriebsart Komfort schalten | 1 Bit | integrierter Regler | K, S |
| 20 | Betriebsart Nacht schalten | 1 Bit | integrierter Regler | K, S |
| 21 | Betriebsart Frostschutz/Hitzeschutz/Frost-Hitzeschutz schalten | 1 Bit | integrierter Regler | K, S |
| 22 | DPT_HVAC Status / DPT_HVAC Mode: Reglerstatus senden | 1 Byte | integrierter Regler | K, S, Ü |
| 23 | DPT_RTSM / DPT_RTC / DPT_HVAC / DPT_RHCC kombinierter Status: Reglerstatus senden | 1 Byte / 2 Byte | integrierter Regler | K, S, Ü |
| 24 | Frostalarm | 1 Bit | integrierter Regler | K, S, Ü |
| 25 | Hitzealarm | 1 Bit | integrierter Regler | K, S, Ü |
| 26 | Vorlauftemperatur Heizung empfangen | 2 Byte | stetig / integrierter Regler | K, S, Ü |
| 27 | Oberflächentemperatur Kühlung empfangen | 2 Byte | stetig / integrierter Regler | K, S, Ü |
| 28 | Diagnose Status | 14 Byte | alle | K, S, Ü |
| 29 | Fensterkontakt (1=geschlossen/0=geöffnet oder invertiert) | 1 Bit | integrierter Regler | K, S, Ü, A |
| 30 | Sperrobjekt Heizen / Freigabeobjekt Heizen | 1 Bit | alle | K, S, Ü, A |
| 31 | Sperrobjekt Kühlen / Freigabeobjekt Kühlen | 1 Bit | alle | K, S, Ü, A |
| 32 | Zwangsstellung / Taupunktalarm | 1 Bit | schaltend / stetig / integrierter Regler | K, S |
| 33 | Übersteuerung: Minimaler Stellwert | 1 Byte | stetig / integrierter Regler | K, S |
| 34 | Übersteuerung: Maximaler Stellwert | 1 Byte | stetig / integrierter Regler | K, S |
| 35 | Störung bei Netzausfall/Kurzschluss/Stellwertfehler | 1 Bit | alle | K, S, Ü |
| 36 | Führungswert in Lux / in Prozent | 2 Byte / 1 Byte | integrierter Regler (Führung aktiv) | K, S |
| 37 | Status Führung | 1 Bit | integrierter Regler (Führung aktiv) | K, S, Ü |
| 38 | Sperre Führung | 1 Bit | integrierter Regler (Führung aktiv) | K, S |

*Welche dieser Objekte tatsächlich sichtbar sind, hängt von der gewählten Regelungsart (schaltend/stetig/integrierter Regler) und von aktivierten Zusatzfunktionen (Zwangsstellung, Führung, Fensterkontakt usw.) im jeweiligen Kanal-Parametermenü ab.*

### Zentrale Objekte (gerätespezifisch für AKH-0800.03)

Zentrale Objekte stehen am Ende der Objektliste. Ihre Nummer hängt von der Kanalanzahl ab (Differenz je Ausbaustufe 4-/6-/8-fach beträgt jeweils 80). Für **AKH-0800.03** ergeben sich folgende Nummern:

| Nr. (AKH-0800.03) | Funktion | DPT/Größe |
|---|---|---|
| 321 | Sommer/Winter – Umschaltung, Übersteuerung für 7 Tage | 1 Bit |
| 322 | Sommer/Winter – Status | 1 Bit |
| 323 | Heizen/Kühlen – Umschaltung | 1 Bit |
| 324 | Heizen/Kühlen – Status | 1 Bit |
| 325 | Heizanforderung / Heiz-Kühlanforderung | 1 Bit |
| 326 | Kühlanforderung | 1 Bit |
| 327 | Störung (Netzausfall/Kurzschluss, zentral) | 1 Bit |
| 328 | Max. Stellwert (Heizen) – Ausgang / Max. Stellwert – Ausgang | 1 Byte |
| 329 | Max. Stellwert (Heizen) – Eingang / Max. Stellwert – Eingang | 1 Byte |
| 330 | Max. Stellwert (Kühlen) – Ausgang | 1 Byte |
| 331 | Max. Stellwert (Kühlen) – Eingang | 1 Byte |
| 332 | Szene – Aktivieren | 1 Byte |
| 333 | Zentrale Funktion – In Betrieb | 1 Bit |
| 334 | Außentemperatur / Führungswert – Messwert empfangen | 2 Byte |
| 335 | Uhrzeit – aktuellen Wert empfangen | 3 Byte |
| 336 | Datum – aktuellen Wert empfangen | 3 Byte |
| 337 | Uhrzeit/Datum – aktuellen Wert empfangen | 8 Byte |

### Erläuterungen zu den Objektgruppen

**Stellwert-/Temperatureingang (Objekt 1, je nach Regelungsart):**
Dieses Objekt hat je nach Kanal-Regelungsart eine andere Bedeutung: bei "schaltend" nimmt es einen fertigen 1-Bit-Schaltwert entgegen, bei "stetig" einen 1-Byte-Prozentwert, bei "integrierter Regler" den Ist-Temperaturwert des Raums. Nur im letzten Fall berechnet der Aktor selbst eine Regelabweichung und daraus die Stellgröße.

**Sollwertvorgabe (Objekte 2–7, nur integrierter Regler):**
Über diese Objekte werden die Sollwerte der einzelnen Betriebsarten (Komfort/Basis, Standby, Nacht, Frost-/Hitzeschutz) vorgegeben. Objekt 2 ist ein "universelles" Sollwertobjekt: Es verändert immer den Sollwert der gerade aktiven Betriebsart. Die Kombiobjekte (8 Byte) erlauben die gleichzeitige Übergabe aller vier HLK-Modus-Sollwerte in einem Telegramm, z. B. aus einer Visualisierung. Ob sich Standby/Nacht relativ zum Komfort-Basiswert (in Kelvin) oder als völlig unabhängige Absolutwerte verhalten, hängt vom Reglerparameter "Sollwerte für Standby/Nacht" ab (siehe ETS-Parameter, Abschnitt Regler).

**Sollwertverschiebung (Objekte 9–11):**
Neben der festen Sollwertvorgabe kann der aktuell gültige Sollwert manuell verschoben werden – wahlweise per 1-Bit (Schrittweite je Flanke), 1-Byte oder 2-Byte-Differenzwert in Kelvin. Objekt 11 gibt den aktuellen Verschiebungsstatus zurück, was z. B. für Visualisierungen wichtig ist, die den Verschiebungswert korrekt darstellen wollen. Die 2-Byte-Verschiebung ist immer aktiv, 1-Bit/1-Byte müssen per Parameter freigeschaltet werden.

**Status-/Rückmeldeobjekte (Objekte 12–15, 8):**
Diese Objekte melden den aktuellen Stellwert (getrennt für Heizen/Kühlen), ob der Stellwert über 0 % liegt, sowie den tatsächlichen Ventilzustand (offen/zu). Bei PWM-Betrieb (stetig/integrierter Regler) wird der Ventilzustand aus dem aktuellen PWM-Zyklus abgeleitet, nicht direkt aus dem Prozentwert – dadurch kann er sich innerhalb eines Zyklus zeitversetzt zur Stellgrößenänderung verhalten.

**Zusatzstufe (Objekt 16):**
Nur im integrierten Regler mit aktivierter Zusatzstufe verfügbar. Dieses 1-Bit-Objekt schaltet eine zweite (schnellere) Heizquelle zusätzlich zur trägen Grundstufe (z. B. Heizkörper zusätzlich zur Fußbodenheizung), um die Aufheizzeit zu verkürzen.

**Betriebsartenumschaltung (Objekte 17, 19–21):**
Die Betriebsart kann entweder über je ein eigenes 1-Bit-Objekt pro Betriebsart (Komfort/Nacht/Frost-Hitzeschutz; Standby ergibt sich automatisch, wenn keine andere Betriebsart aktiv ist) oder über ein gemeinsames 1-Byte-Objekt nach DPT 20.102 (Hex-codiert) gesteuert werden. Der Regler reagiert immer auf den zuletzt empfangenen Befehl – es gibt keine feste Priorität zwischen 1-Bit- und 1-Byte-Umschaltung.

**HVAC-/Reglerstatusobjekte (Objekte 22–23):**
Diese Objekte bilden den aktuellen Reglerzustand (aktive Betriebsart, Heiz-/Kühlmodus, Alarme, Zusatzstufe usw.) bitcodiert für Visualisierungen ab. Zur Auswahl stehen der herstellerspezifische "HVAC Status", der genormte "HVAC Mode" (DPT 20.102) sowie – als zusätzliches Statusobjekt – RHCC-, RTC- oder RTSM-kombinierte Status nach DPT 22.x, die zusätzliche Informationen wie Fehlerstatus, Fensterstatus oder Komfortverlängerung enthalten.

**Alarme (Objekte 24–25):**
Melden das Über- bzw. Unterschreiten einstellbarer Temperaturschwellen (Frost-/Hitzealarm), unabhängig von der aktiven Betriebsart. Rücksetzung erfolgt automatisch, sobald der Grenzwert wieder eingehalten wird.

**Zusätzliche Fühler (Objekte 26–27):**
Ermöglichen den Anschluss eines zweiten Temperaturfühlers zur Vorlauftemperatur-Begrenzung (Heizen) bzw. zur Betauungsvermeidung am Kühlmedium (Kühlen). Beide wirken direkt auf die berechnete Stellgröße ein (siehe ETS-Parameter).

**Diagnose Status (Objekt 28):**
14-Byte-Klartextobjekt, das den aktuellen Betriebs- bzw. Fehlerzustand des Kanals als lesbaren Text ausgibt (siehe Tabelle "Diagnosetexte als Klartext" unten). Sendebedingung (nicht aktiv/bei Abfrage/bei Änderung) ist pro Kanal im Ausgangsmenü einstellbar.

**Fensterkontakt (Objekt 29, nur integrierter Regler):**
Meldet den Zustand eines Fensterkontakts. Bei geöffnetem Fenster erzwingt der Regler Frost-/Hitzeschutz und unterbricht damit den normalen Heiz-/Kühlbetrieb, bis das Fenster wieder geschlossen wird (siehe ETS-Parameter, Fensterkontakt).

**Sperr-/Freigabeobjekte (Objekte 30–31):**
Pro Kanal je ein Objekt für Heizen und Kühlen, wahlweise als Sperr- oder als Freigabeobjekt parametrierbar. Ein aktiver Sperrzustand setzt den Stellwert auf 0 %; nach Aufhebung wird der zuletzt gültige Wert wieder übernommen. Wichtig: Nach einem Neustart ist der Kanal immer im Normalbetrieb – auch ein als Freigabeobjekt konfiguriertes Objekt muss daher zuerst eine "0" (Sperre) erhalten, bevor eine "1" die Freigabe bewirkt.

**Zwangsstellung/Taupunktalarm (Objekt 32):**
Erzwingt einen festen, parametrierbaren Stellwert (Zwangsstellung, Heiz- und Kühlbetrieb) bzw. setzt den Stellwert fest auf 0 % (Taupunktalarm, nur Kühlbetrieb). Bei aktiver Zwangsstellung arbeitet der Kanal weiterhin im PWM-Takt. Eine "0" auf das Objekt beendet die Zwangsstellung/den Alarm und der Kanal übernimmt wieder den zuletzt empfangenen Regelwert.

**Übersteuerung Stellwertbegrenzung (Objekte 33–34):**
Erlauben eine zeitlich befristete (parametrierbare Dauer) Übersteuerung der minimalen bzw. maximalen Stellwertbegrenzung über den Bus, z. B. um morgens kurzzeitig eine höhere Mindesttemperatur im Bad zu erzwingen.

**Störungsobjekt (Objekt 35):**
Meldet Netzausfall (nur bei 230-V-Betrieb erkennbar) bzw. Kurzschluss/Stellwertfehler am Kanal. Eine aktive Störung kann durch Drücken der Programmiertaste am Gerät zurückgesetzt werden.

**Führung (Objekte 36–38, nur integrierter Regler):**
Ermöglichen eine kontinuierliche Sollwert-Anpassung in Abhängigkeit einer externen Führungsgröße (Lux, Prozent oder – über das zentrale Außentemperatur-Objekt – Grad Celsius). Objekt 37 meldet, ob die Führung aktuell wirkt, Objekt 38 kann die Führung komplett sperren.

**Zentrale Objekte:** Die zentralen Objekte (Sommer/Winter, Heizen/Kühlen-Umschaltung, Heiz-/Kühlanforderung, max. Stellwert, Störung, Szene, In-Betrieb, Außentemperatur/Führungswert, Uhrzeit/Datum) wirken geräteweit auf alle Kanäle, sofern die jeweiligen Kanäle nicht per "Eigenständiges System" davon entkoppelt wurden. Die Heiz-/Kühlanforderung dient z. B. der Ansteuerung der Umwälzpumpe und sendet zusätzlich zyklisch alle 30 Minuten.

### Diagnosetexte als Klartext (Objekt 28, 14 Byte)

Der 14-Byte-Diagnosetext ist byteweise aufgeteilt: Byte 0–1 (Sommer/Winter), Byte 3 (Heizen/Kühlen), Byte 5–11 (Betriebsart bzw. Sondermeldung/Kanalbetriebsart), Byte 13 (Stellwert > 0 %, ja=1/nein=0).

| Kategorie | Mögliche Texte |
|---|---|
| Sommer/Winter | Wi (Winter), So (Sommer) |
| Heizen/Kühlen | H (Heizen), K (Kühlen) |
| Betriebsart | Komfort, Standby, Nacht, Frost, Hitze, KomVerl (Komfortverlängerung) |
| Modushinweise | Mode K / Mode H (Kanal-Betriebsart weicht vom aktuellen Aktormodus ab), Mode ER (abweichendes Heizsystem parametriert), BIT (Kanal ist schaltend 1 Bit), PWM BYTE (Kanal ist stetig 1 Byte) |
| Sondermeldungen | Gesperrt, Fenster (offen), Notbetrieb, Zwangsbetrieb, Taupunktalarm, H=0% (Sommer), K=0% (Winter), Tempwert fehlt, Stelllw. fehlt, No H/K Info, 230V Fehler, Lastfehler, Testmodus |
| Warnungen (zyklisch, 1x/Min.) | Soll Führung, Stell Vorlauf, Stell Taupunkt |

Diese Kurztexte dienen der schnellen Fehlerlokalisierung während der Inbetriebnahme, ohne dass eine Visualisierung nötig ist.

## ETS-Parameter

### 1. Allgemeine Einstellungen (gerätweit, wirken auf alle Kanäle)

#### 1.1 Gerätekonfiguration

| Parameter | Werte | Standard |
|---|---|---|
| Geräteanlaufzeit | 2–240 s | 2 s |
| "In Betrieb" zyklisch senden | nicht aktiv / 1 min – 24 h | nicht aktiv |
| Thermischer Antrieb | 24 V AC / 230 V AC | 230 V AC |
| Festsitzschutz (alle 6 Tage 5 min Ventil auf/zu) | nicht aktiv / aktiv | aktiv |

Die Geräteanlaufzeit verzögert den Start nach Busspannungswiederkehr/Download, z. B. damit dieses Gerät erst startet, nachdem andere relevante Werte (z. B. von Sensoren) am Bus verfügbar sind. Das zyklische "In-Betrieb"-Telegramm eignet sich zur Ausfallüberwachung: Bleibt es aus, kann eine Störung des Geräts angenommen werden. Die Einstellung "Thermischer Antrieb" beeinflusst nur die Störungserkennung (bei 230 V werden Netzausfall UND Kurzschluss erkannt, bei 24 V nur Kurzschluss) – die eigentliche Regelfunktion bleibt gleich. Der Festsitzschutz fährt ungenutzte Ventile alle 6 Tage automatisch für 5 Minuten komplett auf und zu, um ein Festsetzen zu verhindern; der Status kann über das jeweilige Kanal-Objekt "Ventilzustand senden" nachvollzogen werden.

#### 1.2 Betriebsart / Heizsystem / Umschaltung Heizen-Kühlen

| Parameter | Werte | Standard |
|---|---|---|
| Auswahl Betriebsart | Heizen / Kühlen / Heizen und Kühlen | Heizen |
| Heizen Stellwerte bei Sommerbetrieb auf 0 % setzen | nicht aktiv / aktiv | aktiv |
| Kühlen Stellwerte bei Winterbetrieb auf 0 % setzen | nicht aktiv / aktiv | aktiv |
| Auswahl Heizsystem (nur bei "Heizen und Kühlen") | 2-Rohr-System (Heizen ODER Kühlen) / 4-Rohr-System (Heizen UND Kühlen getrennt) | 2-Rohr |
| Umschaltung für Heizen/Kühlen (nur 2-Rohr) | über Objekt Sommer/Winter / über Objekt Heizen/Kühlen / automatisch | über Objekt Sommer/Winter |
| Statusobjekt Heizen/Kühlen zyklisch senden | nicht aktiv / 5–30 min / 1–4 h | nicht aktiv |
| Referenzkanal für automatische Umschaltung (2-Rohr) | Kanal A–H | Kanal A |

Beim **2-Rohr-System** existiert nur ein gemeinsamer Kreislauf für Heizen und Kühlen – beide Betriebsarten sind gegeneinander verriegelt, es kann also nie gleichzeitig geheizt und gekühlt werden. Beim **4-Rohr-System** gibt es zwei getrennte Kreisläufe, sodass gleichzeitiges Heizen und Kühlen möglich ist; welcher Kanal heizt bzw. kühlt, wird im jeweiligen Kanal separat festgelegt. Die Umschaltung zwischen Heizen und Kühlen (nur 2-Rohr) kann über das globale Sommer/Winter-Objekt, ein eigenes Heizen/Kühlen-Objekt oder automatisch anhand eines Referenzkanals erfolgen (der Referenzkanal muss selbst auf "Heizen und Kühlen, 2-Rohr" stehen). Die beiden "…auf 0 % setzen"-Optionen verhindern unerwünschtes Mitheizen im Sommer bzw. Mitkühlen im Winter, auch wenn die reine Temperatur dies zulassen würde.

#### 1.3 Sommer-/Winterbetrieb

| Parameter | Werte | Standard |
|---|---|---|
| Bestimmung von Sommer/Winter | über Objekt / automatische Berechnung | über Objekt |
| Polarität für Objekt "Sommer/Winter" | Sommer=1/Winter=0 / Sommer=0/Winter=1 | Sommer=1/Winter=0 |
| Temperaturschwelle Sommer→Winter (nur automatisch) | 10–25 °C | 16 °C |
| Reaktionsgeschwindigkeit (nur automatisch) | schnell / mittel / langsam | mittel |

Bei "automatischer Berechnung" ermittelt der Aktor Sommer/Winter selbst anhand von Uhrzeit, Datum und Außentemperatur (dafür müssen die entsprechenden Objekte am Bus versorgt werden). Zusätzlich steht in diesem Modus ein Objekt "Übersteuerung für 7 Tage" zur Verfügung, mit dem unabhängig von der Berechnung ein fester Sommer- oder Winterbetrieb für eine Woche erzwungen werden kann.

#### 1.4 Sollwert Frost-/Hitzeschutz (geräteweit)

| Parameter | Werte | Standard |
|---|---|---|
| Sollwert Frostschutz für alle Kanäle | 7–14 °C | 7 °C |
| Sollwert Hitzeschutz für alle Kanäle | 24–40 °C | 35 °C |

Diese Werte gelten als Vorgabe für alle Kanäle, können aber im jeweiligen Kanal (integrierter Regler) individuell überschrieben werden.

#### 1.5 Objekt max. Stellwert

| Parameter | Werte | Standard |
|---|---|---|
| Objekt max. Stellwert Heizen / Kühlen | nicht aktiv / senden bei Änderung / senden bei Änderung + zyklisch 30 min | nicht aktiv |

Gibt den höchsten aktuell benötigten Stellwert aller (dafür freigegebenen) Kanäle als 1-Byte-Wert aus – nützlich, um eine modulierende Wärme-/Kälteerzeugung entsprechend dem tatsächlichen Bedarf herunterzuregeln. Mehrere Aktoren lassen sich verketten, indem der Ausgang des einen mit dem Eingang des nächsten Aktors verbunden wird; der letzte Aktor der Kette gibt dann den Gesamt-Maximalwert aus.

#### 1.6 Anforderung Heizen/Kühlen

| Parameter | Werte | Standard |
|---|---|---|
| Objekt für Anforderung Heizen/Kühlen | nicht aktiv / aktiv / aktiv mit 10/20/30 min Ausschaltverzögerung | nicht aktiv |
| Heiz-/Kühlanforderung in Abhängigkeit von | Ventilzustand / Stellwert | Ventilzustand |

Meldet, ob mindestens ein (dafür freigegebener) Kanal aktuell Wärme/Kälte anfordert – z. B. zur Ansteuerung der Umwälzpumpe. Bei Abhängigkeit "Ventilzustand" schaltet die Anforderung bereits während der PWM-Pause auf 0, alle Ausgänge werden gleichzeitig eingeschaltet; bei "Stellwert" bleibt die Anforderung aktiv, solange der Stellwert > 0 % ist, und die Ausgänge werden dabei zeitversetzt angesteuert, um die Pumpenlast gleichmäßiger zu verteilen. Eine Ausschaltverzögerung (Pumpennachlauf) von bis zu 30 Minuten ist möglich; die Anforderung sendet zusätzlich intern fest alle 30 Minuten zyklisch.

#### 1.7 Verhalten nach Busspannungswiederkehr (geräteweit)

| Parameter | Werte | Standard |
|---|---|---|
| Stell-/Temperaturwerte abfragen | nicht aktiv / aktiv | aktiv |
| Sommer/Winter | Winterbetrieb / Sommerbetrieb / Objekt abfragen / Zustand wiederherstellen | Zustand wiederherstellen |
| Heizen/Kühlen (nur 2-Rohr + Objektumschaltung) | Heizen / Kühlen / Objekt abfragen / Zustand wiederherstellen | Zustand wiederherstellen |

Legt fest, wie sich der Aktor nach einem Spannungsausfall verhält. "Zustand wiederherstellen" stellt jeweils den letzten Zustand vor dem Ausfall wieder her; dies gilt nur für eine Busspannungswiederkehr – nach einer Neuprogrammierung startet das Gerät immer im Winterbetrieb/Heizen (Ausnahme: Betriebsart ausschließlich Kühlen).

#### 1.8 Sprache für Diagnosetext

| Parameter | Werte | Standard |
|---|---|---|
| Sprache für Diagnosetext | Deutsch / Englisch | Deutsch |

Legt nur die Sprache der unter "Diagnosetexte als Klartext" beschriebenen Ausgabe fest; Aktivierung/Sendebedingung erfolgt separat je Kanal.

### 2. Kanal Auswahl

| Parameter | Werte | Standard |
|---|---|---|
| Kanal A–H | nicht aktiv / aktiv / aktiv, Stellwert von Kanal X | nicht aktiv |
| Betriebsart elektrischer Ausgang (nur bei "Stellwert von Kanal X" + Heizen&Kühlen 4-Rohr) | Heizen / Kühlen | – |

Aktiviert die einzelnen Kanäle. Mit "aktiv, Stellwert von Kanal X" übernimmt ein Kanal intern den Stellwert eines anderen, bereits konfigurierten Kanals – sinnvoll bei großen Räumen mit mehreren parallel benötigten Ventilausgängen, da nur ein Kanal vollständig parametriert werden muss und keine zusätzliche Gruppenadressen-Verknüpfung nötig ist. Im 4-Rohr-System kann dabei festgelegt werden, ob der übernehmende Kanal für Heizen oder Kühlen steht, während der Ursprungskanal die jeweils andere Funktion behält.

### 3. Kanal – Grundeinstellung (Regelungsart)

| Parameter | Werte | Standard |
|---|---|---|
| Kanal-/Objektbeschreibung | Freitext, bis 30 Zeichen | – |
| Zusatztext | Freitext, bis 80 Zeichen | – |
| Regelungsart | schaltend (1 Bit-Objekt) / stetig (1 Byte-Objekt) / integrierter Regler | – |

Die Kanal-/Objektbeschreibung erscheint sowohl im ETS-Kanalmenü als auch an den zugehörigen Kommunikationsobjekten, der Zusatztext dient nur als interne Notiz für den Programmierer. Die Regelungsart bestimmt grundlegend, ob der Kanal einen fertigen Schaltwert (schaltend), einen fertigen Prozentwert (stetig) oder nur einen Ist-Temperaturwert (integrierter Regler, mit vollständiger Regelberechnung im Aktor) verarbeitet; die im Folgenden verfügbaren Untermenüs unterscheiden sich entsprechend.

### 4. Kanal Konfiguration – Schaltend (1 Bit-Objekt)

#### 4.1 Grundeinstellung

| Parameter | Werte | Standard |
|---|---|---|
| Betriebsart | Heizen / Kühlen (abhängig von globaler "Auswahl Betriebsart") | Heizen |
| Eigenständiges System | nicht aktiv / aktiv | nicht aktiv |

"Eigenständiges System" entkoppelt den Kanal von der globalen Heizen/Kühlen-Umschaltung, sodass er z. B. weiter kühlen kann, während das restliche Haus bereits auf Heizen umgeschaltet ist.

#### 4.2 Ausgang

| Parameter | Werte | Standard |
|---|---|---|
| Ventilart | spannungslos geschlossen / spannungslos geöffnet | spannungslos geschlossen |
| Ventilzustand zyklisch senden | nicht aktiv / 1–60 min | 5 min |
| Kanal in Heiz-/Kühlanforderung und max. Stellwert berücksichtigen | nicht aktiv / aktiv | aktiv |
| Zwangsstellung (Heizen) | nicht aktiv / aktiv | nicht aktiv |
| Zwangsstellung/Taupunktalarm (Kühlen) | nicht aktiv / Zwangsstellung / Taupunktalarm | nicht aktiv |
| Stellwert für Zwangsstellung | 0–100 % | 0 % |
| Notbetrieb | nicht aktiv / aktiv | aktiv |
| Notbetrieb bei Ausfall des Stellwertes nach | 30–90 min | 30 min |
| Stellwert für Notbetrieb | 0–100 % | 50 % |
| Sperrobjekt Stellwert Heizen/Kühlen | nicht aktiv / aktiv, Freigabeobjekt / aktiv, Sperrobjekt | nicht aktiv |
| Diagnosetext senden | nicht aktiv / senden bei Abfrage / senden bei Änderung | nicht aktiv |

Die Ventilart passt den Ausgang an Schließer- oder Öffner-Ventile an ("spannungslos geöffnet" invertiert das Ausgangssignal). Die Zwangsstellung erzwingt bei aktivem 1-Signal einen festen Stellwert; der Kanal arbeitet dabei als PWM-Regler mit fester Zykluszeit von 10 Minuten, unabhängig vom sonst empfangenen Stellwert. Der Taupunktalarm (nur Kühlbetrieb) setzt den Stellwert bei aktivem Signal fest auf 0 %. Der Notbetrieb schützt vor dauerhaftem Volllastbetrieb bzw. Auskühlen, falls der Eingangs-Stellwert für die eingestellte Zeit ausbleibt (z. B. bei Ausfall des vorgeschalteten Reglers); er nutzt ebenfalls einen festen PWM-Takt von 10 Minuten und wird über die Kanal-LED (2x Blinken – Pause) signalisiert. Sperrobjekte schalten den Kanal komplett aus (0 %) bzw. geben ihn wieder frei; nach Neustart ist jeder Kanal zunächst freigegeben, unabhängig von der Objektpolarität.

### 5. Kanal Konfiguration – Stetig (1 Byte-Objekt)

#### 5.1 Grundeinstellung

Identisch zur schaltenden Regelungsart (Betriebsart, Eigenständiges System – siehe Abschnitt 4.1).

#### 5.2 Ausgang

| Parameter | Werte | Standard |
|---|---|---|
| Ventilart | spannungslos geschlossen / spannungslos geöffnet | spannungslos geschlossen |
| PWM Zyklus | 10 s – 30 min | 10 min |
| Minimale/Maximale Begrenzung des Stellwertes | 0–50 % / 20–100 % | 0 % / 100 % |
| Begrenzung über Objekt | nicht aktiv / aktiv für 1–24 h | nicht aktiv |
| Stellwert bei Unterschreitung der minimalen Begrenzung | 0%=0%, sonst Mindeststellwert nutzen / 0%=Mindeststellwert | 0%=0%, sonst Mindeststellwert |
| Status Stellwert zyklisch senden | nicht aktiv / 1–60 min | 5 min |
| Objekt Ventilzustand | Ventilzustand (1=offen/0=zu) / 1 wenn Stellwert > 0 % | Ventilzustand |
| Kanal in Heiz-/Kühlanforderung und max. Stellwert berücksichtigen | nicht aktiv / aktiv | aktiv |
| Zwangsstellung/Taupunktalarm | wie Abschnitt 4.2 | nicht aktiv |
| Zusätzlicher Fühler für Vorlauftemperatur (nur Heizen) | nicht aktiv / aktiv | nicht aktiv |
| Maximale/Minimale Vorlauftemperatur beim Heizen | 0–60 °C | 40 °C / 20 °C |
| Zusätzlicher Fühler für Kühlmedium (nur Kühlen) | nicht aktiv / aktiv | nicht aktiv |
| Minimale Temperatur Kühlmedium | 0–60 °C | 10 °C |
| Notbetrieb | wie Abschnitt 4.2 | aktiv |
| Sperrobjekt Stellwert Heizen/Kühlen | wie Abschnitt 4.2 | nicht aktiv |
| Diagnosetext senden | wie Abschnitt 4.2 | nicht aktiv |

**PWM Zyklus:** Bestimmt, über welchen Zeitraum ein 0–100 %-Stellwert in ein Ein-/Aus-Verhältnis umgerechnet wird (z. B. 75 % bei 10 min Zyklus = 7,5 min ein, 2,5 min aus). Zwei Einstellphilosophien haben sich bewährt: Ein **Zyklus deutlich größer als die Ventil-Verstellzeit** lässt das Ventil je Zyklus einmal komplett auf- und zufahren (präzisere Regelung, aber mehr mechanische Belastung und größere lokale Temperaturschwankung nahe der Heizquelle) – geeignet für träge Systeme wie Fußbodenheizungen. Ein **Zyklus deutlich kleiner als die Verstellzeit** bewegt das Ventil nur in kleinen Schritten und pendelt sich auf einen Mittelwert ein (schonender für das Ventil, gleichmäßigere Temperatur, aber bei mehreren Ventilen schwerer exakt auf einen gemeinsamen Mittelwert zu bringen) – geeignet für schnelle Systeme mit nur einem Ventil, z. B. Heizkörper. Bei mehreren gemeinsam angesteuerten Ventilen empfiehlt sich die Einstellung nach dem trägsten beteiligten System.

**Stellwertbegrenzung:** Minimal-/Maximalwert kappen den effektiv wirksamen Stellwert, bevor die PWM-Berechnung erfolgt. Ein tatsächlicher 0 %-Stellwert bleibt dabei immer 0 % (kein Energieverbrauch bei Nichtbedarf); erst Werte oberhalb 0 % werden auf den Mindeststellwert angehoben. Über "Begrenzung über Objekt" lässt sich die Begrenzung zusätzlich zeitlich befristet (1–24 h) fernsteuern.

**Objekt Ventilzustand:** Kann entweder den tatsächlichen, aus dem PWM-Takt abgeleiteten Zustand (zeitlich versetzt zum Stellwert) oder einfach "1 sobald Stellwert > 0 %" senden.

**Zusätzliche Fühler:** Ein zweiter Temperaturfühler (z. B. im Estrich) kann die Vorlauf- bzw. Kühlmediumtemperatur begrenzen. Bei Überschreiten der Maximal- bzw. Unterschreiten der Minimal-Vorlauftemperatur wird der Stellwert anhand einer definierten Regelkurve (siehe Diagramm im Originaldatenblatt) bis auf 0 % zurückgeregelt – nützlich z. B. zum Schutz von Bodenbelägen bei Fußbodenheizungen oder zur Betauungsvermeidung bei Kühlsystemen.

### 6. Kanal Konfiguration – Integrierter Regler

#### 6.1 Grundeinstellung

| Parameter | Werte | Standard |
|---|---|---|
| Betriebsart | Heizen / Kühlen / Heizen und Kühlen | Heizen |
| System (nur Heizen und Kühlen) | 2-Rohr (1 Kreis) / 4-Rohr (2 Kreise, getrennt) | gemäß Allg. Einstellung |
| Eigenständiges System | nicht aktiv / aktiv | nicht aktiv |
| Stellgröße | stetige PI-Regelung / 2-Punkt-Regelung | stetige PI-Regelung |
| Schalthysterese (nur 2-Punkt) | 0,5–5,0 K | 0,5 K |
| Heizsystem (nur PI, Heizen) | Wasserheizung (4K/120 min) / Fußbodenheizung (4K/150 min) / Split Unit (4K/60 min) / Anpassung über Regelparameter | Fußbodenheizung |
| Kühlsystem (nur PI, Kühlen) | Split Unit (4K/60 min) / Kühldecke (4K/150 min) / Anpassung über Regelparameter | Kühldecke |
| Proportionalbereich (nur "Anpassung über Regelparameter") | 1–20 K | 4 K |
| Nachstellzeit (nur "Anpassung über Regelparameter") | 15–240 min | 150 min |
| Zusatzstufe (nur Heizen) | nicht aktiv / aktiv | nicht aktiv |
| Wirksinn bei steigender Temperatur (Zusatzstufe) | Objekt sendet 1 beim Heizen / sendet 0 beim Heizen | sendet 1 |
| Stellgröße Zusatzstufe | 2-Punkt-Regelung / PWM (schaltende PI-Regelung, fix 15 min) | 2-Punkt |
| Abstand Zusatzstufe | 0,5–5,0 K | 2,0 K |

"Eigenständiges System" entkoppelt auch hier den Kanal von der globalen Heizen/Kühlen-Umschaltung; bei Aktivierung wird intern immer das 4-Rohr-System angenommen, unabhängig von der globalen Einstellung.

Bei **2-Punkt-Regelung** schaltet der Ausgang bei Über-/Unterschreiten von Sollwert ± halber Schalthysterese ein bzw. aus. Eine große Hysterese führt zu größerer Temperaturschwankung, eine sehr kleine Hysterese zu häufigem Takten.

Bei **stetiger PI-Regelung** legt das gewählte Heiz-/Kühlsystem die voreingestellten P- und I-Regelparameter fest (aus der Praxis abgeleitete Erfahrungswerte); alternativ können Proportionalbereich und Nachstellzeit frei parametriert werden (nur für Anwender mit regelungstechnischem Hintergrund empfohlen). Ein **kleiner Proportionalbereich** lässt den Regler bereits bei geringer Abweichung nahezu auf 100 % stellen (schnell, aber überschwingungsanfällig); ein **größerer Wert** ergibt einen sanfteren, proportionalen Anstieg. Die **Nachstellzeit** bestimmt, wie schnell der Integralanteil die Stellgröße dem P-Anteil-Wert annähert – eine kurze Nachstellzeit reagiert stärker/schneller (Überschwingungsgefahr bei zu kurzer Einstellung), eine lange Nachstellzeit passt zu trägen Systemen.

Die **Zusatzstufe** (nur Heizbetrieb) schaltet bei trägen Grundsystemen (z. B. Fußbodenheizung) eine schnellere Zusatzheizquelle zu, um die Aufheizphase zu verkürzen; ihr Sollwert ergibt sich aus dem aktuellen Sollwert der Grundstufe abzüglich des parametrierten "Abstands" in Kelvin.

##### 6.1.1 Regler – Sollwerte, Totzone, Betriebsarten, Prioritäten

| Parameter | Werte | Standard |
|---|---|---|
| Sollwerte für Standby/Nacht | unabhängige Sollwerte / abhängig von Sollwert Komfort (Basis) | abhängig von Komfort (Basis) |
| Sollwert Komfort (Basis) | 7–35 °C | 21 °C (Heizen) / 23 °C (Kühlen, unabhängig) |
| Absenkung/Anhebung Standby (relativ) bzw. Sollwert Standby (absolut) | 0–10 K bzw. 7–35 °C | 2,0 K bzw. 19/24 °C |
| Absenkung/Anhebung Nacht (relativ) bzw. Sollwert Nacht (absolut) | 0–10 K bzw. 7–35 °C | 3,0 K bzw. 18/25 °C |
| Sollwert Frostschutz/Hitzeschutz Einstellung | allgemein / individuell | allgemein |
| Sollwert Frostschutz (individuell) | 3–12 °C | 7 °C |
| Sollwert Hitzeschutz (individuell) | 24–40 °C | 35 °C |
| Totzone zwischen Heizen und Kühlen | 0–10 K (bei "abhängig") bzw. entfällt (bei "unabhängig") | 2,0 K |
| Priorität der Betriebsarten | Frost(Hitzeschutz)/Komfort/Nacht/Standby / Frost(Hitzeschutz)/Nacht/Komfort/Standby | Frost/Komfort/Nacht/Standby |
| Separate Objekte für Sollwerte (nur "unabhängige Sollwerte") | nicht aktiv / aktiv Einzelobjekte / aktiv Kombiobjekt (DPT 275.100) | nicht aktiv |

Bei **"abhängig vom Komfort-Sollwert (Basis)"** beziehen sich Standby und Nacht relativ (in Kelvin) auf den Basis-Komfortwert; ändert sich dieser, verschieben sich Standby/Nacht automatisch mit. Bei **"unabhängigen Sollwerten"** wird jeder Betriebsart ein eigener Absolutwert in °C zugewiesen, ohne Bezug zueinander – dadurch entfällt auch die feste Totzone; stattdessen wird jeder Sollwert (Heizen wie Kühlen) getrennt vorgegeben.

Die **Totzone** (nur "Heizen und Kühlen", abhängige Sollwerte) beschreibt den Temperaturbereich zwischen Heiz- und Kühlsollwert, in dem der Regler weder heizt noch kühlt; der Kühlsollwert ergibt sich damit aus Komfort-Basiswert + Totzone. Eine kleine Totzone führt zu häufigerem Umschalten zwischen Heizen/Kühlen, eine große zu stärkeren Temperaturschwankungen.

Die **Betriebsart "Standby"** wird automatisch aktiv, sobald keine andere Betriebsart (Komfort/Nacht/Frost-Hitzeschutz) eingeschaltet ist – sie besitzt daher kein eigenes Schaltobjekt. Die **Priorität** legt fest, welche Betriebsart bei gleichzeitig aktiven Signalen den Vorrang erhält.

##### 6.1.2 Betriebsartenumschaltung

Siehe Kommunikationsobjekte, Abschnitt "Betriebsartenumschaltung" – Umschaltung wahlweise per 1-Bit-Objekten je Betriebsart oder per 1-Byte-Objekt nach DPT 20.102 mit Hex-Codierung:

| Betriebsart | Hex-Wert (1-Byte-Umschaltung) |
|---|---|
| Komfort | 0x01 |
| Standby | 0x02 |
| Nacht | 0x03 |
| Frost-/Hitzeschutz | 0x04 |

Der Regler folgt jeweils dem zuletzt empfangenen Umschaltweg (1-Bit oder 1-Byte); es gibt keine feste Priorität zwischen beiden.

##### 6.1.3 Sollwertverschiebung

| Parameter | Werte | Standard |
|---|---|---|
| Maximale Sollwertverschiebung | 0–10 K | 3 K |
| Sollwertverschiebung über 1Bit/1Byte-Objekt | nicht aktiv / 1 Bit / 1 Byte | nicht aktiv |
| Schrittweite (1Bit/1Byte) | 0,1–1 K | 0,5 K |
| Status Sollwertverschiebung | nicht aktiv / aktiv | nicht aktiv |
| Sollwertverschiebung gilt für | Komfort / Komfort+Nacht+Standby | Komfort |
| Aktion wenn Verschiebung in Nacht/Standby (nur bei "gilt für Komfort") | keine Aktion / Wechsel in Komfort | keine Aktion |
| Sollwertverschiebung löschen nach Betriebsartenwechsel | nicht aktiv / aktiv | nicht aktiv |
| Sollwertverschiebung löschen nach neuem absolutem Sollwert (nur unabhängige Sollwerte) | nicht aktiv / aktiv | – |
| Sollwertverschiebung löschen nach neuem Basissollwert (nur abhängige Sollwerte) | nicht aktiv / aktiv | aktiv |
| Basissollwert auf Parametrierung zurücksetzen nach Betriebsartenwechsel (nur abhängige Sollwerte) | nicht aktiv / aktiv | nicht aktiv |
| Sollwertänderung senden | nicht aktiv / aktiv | nicht aktiv |
| Aktuellen Sollwert zyklisch senden | nicht aktiv / 5 min – 4 h | nicht aktiv |

Die Sollwertverschiebung erlaubt eine temporäre, additive Anpassung (in Kelvin) des jeweils aktiven Sollwerts, ohne den parametrierten Basiswert dauerhaft zu verändern. Die 2-Byte-Verschiebung ist immer verfügbar; 1-Bit (feste Schrittweite je Flanke) und 1-Byte müssen zusätzlich freigeschaltet werden. Über "maximale Sollwertverschiebung" wird der zulässige Verschiebebereich begrenzt (z. B. ±3 K um den Basiswert). Ob die Verschiebung nur im Komfortbetrieb oder auch in Nacht/Standby wirkt, ist einstellbar; ebenso, ob und wie sie nach einem Betriebsartenwechsel oder nach Vorgabe eines neuen Basis-/Absolutsollwerts automatisch gelöscht wird. Das allgemeine Sollwert-Vorgabeobjekt verhält sich je nach gewählter Grundeinstellung unterschiedlich: Bei "abhängig vom Komfort-Sollwert" springt der Regler beim Empfang eines neuen absoluten Sollwerts über dieses Objekt automatisch in den Komfortmodus und löscht eine bestehende Verschiebung; bei "unabhängigen Sollwerten" verändert das Objekt gezielt nur den Sollwert der aktuell aktiven Betriebsart.

##### 6.1.4 Komfortverlängerung mit Zeit

| Parameter | Werte | Standard |
|---|---|---|
| Komfortverlängerung mit Zeit | nicht aktiv / aktiv | nicht aktiv |
| Komfort Verlängerungszeit | 30 min – 4 h (in 30-min-Schritten) | 30 min |

Ermöglicht eine zeitlich befristete Rückkehr in den Komfortmodus, wenn sich der Regler aktuell im Nachtmodus befindet (z. B. bei spontanem Besuch). Nach Ablauf der Verlängerungszeit fällt der Regler automatisch wieder in den Nachtmodus zurück; ein erneutes 1-Signal während der Verlängerung startet die Zeit neu, ein 0-Signal beendet sie vorzeitig. Die Funktion wirkt ausschließlich zwischen den Modi Nacht und Komfort, nicht bei anderen Betriebsartenwechseln.

##### 6.1.5 Betriebsart nach Reset

| Parameter | Werte | Standard |
|---|---|---|
| Betriebsart nach Reset | Komfort mit parametriertem Sollwert / Standby mit parametriertem Sollwert / alten Zustand und Sollwert halten | Komfort mit parametriertem Sollwert |
| Betriebsart nach Neuprogrammierung (nur bei "alten Zustand halten") | Komfort / Standby | Komfort |

Legt fest, mit welcher Betriebsart/welchem Sollwert der Regler nach einer Busspannungswiederkehr startet.

##### 6.1.6 HVAC-Statusobjekte

| Parameter | Werte | Standard |
|---|---|---|
| HVAC-Statusobjekt | HVAC Status (non-standard DPT) / HVAC Mode (DPT 20.102) | HVAC Mode |
| Zusätzliches HVAC-Statusobjekt | nicht aktiv / HVAC Status / HVAC Mode / RHCC Status (DPT 22.101) / RTC kombinierter Status (DPT 22.103) / RTSM kombinierter Status (DPT 22.107) | nicht aktiv |
| HVAC-Statusobjekte zyklisch senden | nicht senden / 5 min – 4 h | nicht senden |

Der herstellerspezifische "HVAC Status" codiert mehrere gleichzeitig zutreffende Zustände (Komfort/Standby/Nacht/Frost-Hitzeschutz/Heizen-Kühlen/Frostalarm) additiv als Hex-Wert (z. B. 0x21 = Heizbetrieb + Komfort aktiv). RHCC-, RTC- und RTSM-Status nach DPT 22.x sind genormte kombinierte Statuswerte mit zusätzlichen Informationen wie Fehlerstatus, Taupunktstatus, Zusatzstufe, Fensterstatus oder Komfortverlängerung – geeignet für standardkonforme Visualisierungen.

##### 6.1.7 Führung

| Parameter | Werte | Standard |
|---|---|---|
| Führung | nicht aktiv / Kühlen über Außentemperatur / Kühlen über Prozentwert / Heizen über Außentemperatur / Heizen über Prozentwert / Heizen über Luxwert | nicht aktiv |
| Führungsgröße Minimum/Maximum | je nach Führungsart (°C, %, Lux) | z. B. 28/38 °C (Kühlen), 18/30 °C (Heizen) |
| Sollwertänderung bei maximaler Führungsgröße | Kühlen: 1–10 K / Heizen: −5 bis −0,5 K | 10 K bzw. −2 K |
| Schwellwert Außentemperatur (nur Heizen über %/Lux) | nicht aktiv / aktiv | nicht aktiv |
| Freigabe Führung ab | 5–35 °C | 15 °C |
| Aktueller Sollwert berücksichtigt Führung | nicht aktiv / aktiv | nicht aktiv |

Die Führung passt den Sollwert linear in Abhängigkeit einer externen Führungsgröße (Außentemperatur, Prozentwert oder Helligkeit) an: Zwischen Führungsgröße-Minimum und -Maximum wird der Sollwert proportional bis zum Wert "Sollwertänderung bei maximaler Führungsgröße" verschoben; außerhalb dieses Bereichs bleibt der Sollwert unverändert. Ein Anwendungsbeispiel: Bei hoher Außentemperatur (Kühlen über Außentemperatur) wird der Kühlsollwert angehoben, um den Temperaturunterschied zwischen innen und außen zu begrenzen. "Heizen über Luxwert" reduziert umgekehrt den Heizsollwert bei hoher Sonneneinstrahlung, um Überhitzung durch passive Solargewinne zu vermeiden. Bei den prozent-/luxbasierten Heizvarianten kann zusätzlich ein Außentemperatur-Schwellwert die Führung erst ab einer bestimmten Temperatur freigeben. Der Führungswert (Außentemperatur) wird über das zentrale, geräteweite Objekt eingelesen und gilt für alle Kanäle gemeinsam.

##### 6.1.8 Alarme

| Parameter | Werte | Standard |
|---|---|---|
| Alarme | nicht aktiv / aktiv | nicht aktiv |
| Frostalarm wenn Temperatur < | 3–10 °C | 7 °C |
| Hitzealarm wenn Temperatur > | 25–40 °C | 35 °C |

Frost- bzw. Hitzealarm melden das Unter-/Überschreiten der eingestellten Temperaturschwellen unabhängig von der aktiven Betriebsart über je ein eigenes Objekt; die Meldung wird automatisch zurückgenommen, sobald die Temperatur wieder im zulässigen Bereich liegt.

##### 6.1.9 Fensterkontakt

| Parameter | Werte | Standard |
|---|---|---|
| Fensterkontakt | nicht aktiv / aktiv | nicht aktiv |
| Zustand Fenster (Polarität) | 0=geschlossen/1=geöffnet (Standard-DPT) / 1=geschlossen/0=geöffnet | 0=geschlossen/1=geöffnet |
| Verzögerungszeit | 0–240 s | 5 s |
| Aktion beim Öffnen des Fensters | Frost-/Hitzeschutz erzwingen (fest) | – |
| Aktion beim Schließen des Fensters | HVAC Modus vor Sperre / HVAC Modus nachholen | HVAC Modus vor Sperre |
| Rückfallzeit | nicht aktiv (nicht empfohlen) / 1–24 h | 12 h |

Beim Öffnen eines Fensters wird der Kanal in Frost- bzw. Hitzeschutz gezwungen (Heiz-/Kühlbetrieb pausiert), um Energieverluste zu vermeiden. Die Verzögerungszeit verhindert eine sofortige Reaktion bei nur kurzzeitigem Öffnen. Beim Schließen kann entweder in den Modus vor der Sperre zurückgekehrt werden, oder ein während der Sperre ggf. per Zeitschaltuhr/Visualisierung geänderter Modus wird nachträglich übernommen. Die Rückfallzeit sorgt dafür, dass der Regler auch bei versehentlich offen gelassenem Fenster nach einer bestimmten Zeit automatisch wieder in den Normalbetrieb zurückkehrt (Auskühl-/Überhitzungsschutz); von "nicht aktiv" wird ausdrücklich abgeraten.

#### 6.2 Ausgang (integrierter Regler)

Die Ausgangsparameter des integrierten Reglers entsprechen inhaltlich denen der stetigen Regelungsart (Abschnitt 5.2: PWM-Zyklus, Stellwertbegrenzung, Objekt Ventilzustand, Zwangsstellung/Taupunktalarm, zusätzliche Fühler für Vorlauf-/Kühlmedium, Notbetrieb, Sperrobjekte, Diagnosetext), zusätzlich jeweils getrennt für Heizen und Kühlen bei "Heizen und Kühlen"-Betrieb:

| Parameter | Werte | Standard |
|---|---|---|
| Ventilart | spannungslos geschlossen / geöffnet | spannungslos geschlossen |
| PWM Zyklus | 10 s – 30 min | 10 min |
| Minimale/Maximale Begrenzung des Stellwertes (separat Heizen/Kühlen bei 4-Rohr) | 0–50 % / 20–100 % | 0 % / 100 % |
| Stellwert zyklisch senden (Heizen bzw. Heizen+Kühlen) | nicht aktiv / 1–60 min | 5 min |
| Notbetrieb bei Ausfall des Temperaturwertes nach | 30–90 min | 30 min |
| Stellwert für Notbetrieb Heizen/Kühlen (getrennt) | 0–100 % | 50 % |

Ein wesentlicher Unterschied zur stetigen Regelungsart: Der Notbetrieb überwacht hier den Eingang des **Temperaturmesswertes** (nicht des Stellwertes), da der Regler selbst rechnet – bleibt dieser Wert aus, wird auf den parametrierten Notbetrieb-Stellwert (separat für Heizen/Kühlen einstellbar) umgeschaltet. Beim Objekt "Ventilzustand Heizen senden" ist zu beachten, dass bei der Betriebsart "Heizen und Kühlen" der aktuelle elektrische Ausgang des Kanals stets der Heizausgang ist – daher wird dort auch nur der Ventilzustand für Heizen ausgegeben.

### 7. Szenen

| Parameter | Werte | Standard |
|---|---|---|
| Szene A–P | nicht aktiv / aktiv | Szene A: aktiv, B–P: nicht aktiv |
| Szenennummer (je aktivierte Szene) | 1–64 | 1 |
| Betriebsart (je Szene) | keine Änderung / Komfort / Standby / Nacht / Frost-/Hitzeschutz | keine Änderung |
| Sollwertvorgabe (nur bei "keine Änderung" der Betriebsart) | keine Änderung / 7–25 °C (0,5-K-Schritte) | keine Änderung |
| Änderung für Kanal x (je Kanal) | nicht aktiv / aktiv | Kanal A: aktiv |

Bis zu 16 Szenen können angelegt werden; jede Szene kann pro Kanal entweder eine Betriebsart oder – bei "keine Änderung" der Betriebsart – einen festen Sollwert setzen, und ist pro Kanal einzeln aktivierbar. **Wichtig:** Die intern verwendeten Szenennummern (1–64) unterscheiden sich von den am Bus zu sendenden Aufrufwerten (0–63) – zum Aufruf der Szene 1 muss der Wert 0 gesendet werden, für Szene 2 der Wert 1 usw.

## Inbetriebnahme / Hinweise

- **Erstinbetriebnahme:** Schnittstelle an den Bus anschließen → Busspannung zuschalten → Programmiertaste >1 s drücken (rote LED leuchtet dauerhaft) → physikalische Adresse aus der ETS laden (LED erlischt bei Erfolg) → Applikation mit gewünschter Parametrierung laden → Funktion prüfen.
- **Testbetrieb:** Programmiertaste >5 s gedrückt halten aktiviert den Testbetrieb; alle aktiven Kanäle werden nacheinander für je 3 Minuten bestromt (Kanal-LED leuchtet dauerhaft). Kurzer Tastendruck schaltet zum nächsten Kanal weiter; am letzten Kanal beendet ein weiterer kurzer Druck den Testbetrieb.
- **Kanalbelegung beachten:** Beim 8-fach-Aktor müssen Kanal A (Gruppe A–D) und Kanal E (Gruppe E–H) zuerst belegt werden, da sonst eine Störung ausgelöst wird (siehe Abschnitt Technische Daten).
- **Nur eine Versorgungsspannung je Gerät:** 24 V AC und 230 V AC dürfen nicht gemischt an einem Aktor angeschlossen werden; die Betriebsspannung muss zwingend Wechselspannung sein (TRIAC-Ausgänge).
- **Kanal-LED-Störcodes:** 2x Blinken + Pause = Notbetrieb (Stell-/Messwertausfall); 3x Blinken + Pause = Netzausfall (230-V-Betrieb, betrifft jeweils eine ganze Phasengruppe); 4x Blinken + Pause = Überlast/Kurzschluss am Ausgang. Eine aktive Störung lässt sich durch Drücken der Programmiertaste am Gerät zurücksetzen.
- **Freigabe-/Sperrobjekte:** Nach einem Neustart ist jeder Kanal zunächst freigegeben – auch wenn das Objekt als Freigabeobjekt parametriert wurde. Ein Freigabeobjekt muss daher zuerst eine "0" (Sperre) erhalten, bevor eine "1" wirksam freigibt.
- **2-Rohr- vs. 4-Rohr-System:** Beim 2-Rohr-System sind Heizen und Kühlen softwareseitig gegeneinander verriegelt (nur eines von beidem gleichzeitig). Beim 4-Rohr-System ist gleichzeitiges Heizen und Kühlen möglich – wird dies nicht gewünscht, muss dies über die kanalindividuelle Sperrfunktion sichergestellt werden, insbesondere wenn "Eigenständiges System" aktiviert ist.
- **PWM-Zyklus-Wahl:** Bei mehreren gemeinsam angesteuerten, unterschiedlich trägen Ventilen empfiehlt sich, den PWM-Zyklus nach dem trägsten beteiligten System auszurichten.
- **Objektnummern sind gerätetypabhängig:** Für andere Ausbaustufen (AKH-0400.03/AKH-0600.03) verschieben sich sowohl die kanalbezogenen als auch die zentralen Objektnummern; siehe Abschnitt Kommunikationsobjekte.
- Nicht im Datenblatt spezifiziert: genaue elektrische Kenndaten wie maximale Ausgangsleistung je Kanal, Gehäusematerial-Details und mechanische Maße wurden im ausgewerteten Handbuch nicht tabellarisch aufgeführt (Verweis auf separates Datenblatt).

## Quelle

MDT technologies GmbH – Technisches Handbuch "MDT Heizungsaktor AKH-0400.03 / AKH-0600.03 / AKH-0800.03", Stand 11/2022, Version 1.2.
Datei: `originals/KNX/MDT_THB_AKH_03_Heizungsaktor_V12.pdf`
