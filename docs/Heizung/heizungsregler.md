# Danfoss ECL Comfort 210 – Reglerkonfiguration

*(Anwendungsschlüssel A267, Master/Slave-Verbund)*

## 1. Geräte-Übersicht

Zwei baugleiche **Danfoss ECL Comfort 210** mit Anwendungsschlüssel **A267**, im **Master/Slave-Verbund** über den internen ECL-485-Bus gekoppelt:

- **Regler 1 – Master**: steuert HK1 (Nahwärme) und HK2 (Heizung)
- **Regler 2 – Slave**: steuert HK3 (Fußbodenheizung), bezieht die Außentemperatur vom Master

Die Warmwasserbereitung läuft über einen **separaten Regler (Oventrop Regtronic PQ)** an der Frischwasserstation – dieser ist nicht Teil des Danfoss-Systems und wird hier nicht behandelt.

## 2. Begriffe / Abkürzungen am ECL Comfort 210

| Kürzel | Bedeutung |
|---|---|
| S | Fühlereingang (Sensor) |
| R | Relaisausgang (schaltet Pumpen ein/aus) |
| Tr | Triac-Ausgang (elektronisches Relais, steuert i. d. R. 3-Punkt-Stellantriebe/Mischer; je zwei Triacs = "auf"/"zu"-Richtung eines Mischers) |
| M | Mischer/Stellantrieb (im Display z. B. "M1", "M2") |
| P | Pumpe (im Display z. B. "P1", "P4") |
| HK | Heizkreis |

**Offizielle Pumpen-/Mischer-Zuordnung laut A267-Anwendungshandbuch:**

| Bezeichnung | Offizielle Funktion |
|---|---|
| M1 | Mischer Kreis 1 (bei uns: Nahwärme) – laut Handbuch technisch auch für Kreis 3/WW mitgenutzt, bei uns aber nicht relevant, siehe Abschnitt 5 |
| M2 | Mischer Kreis 2 (bei uns: Heizung) |
| P1 | Umwälzpumpe Kreis 1 |
| P2 | WW-Tauscherladepumpe, Kreis 3 |
| P3 | WW-Zirkulationspumpe, Kreis 3 |
| P4 | Umwälzpumpe Kreis 2 |

**Wichtig:** Diese P1–P4-Bezeichnungen sind pro Regler vergeben (jeder der beiden Regler hat seinen eigenen "Kreis 1", "Kreis 2" usw.). Am Master ist "Kreis 1" = Nahwärme und "Kreis 2" = Heizung. Am Slave ist "Kreis 1" = Fußbodenheizung (dort als "HK3" beschriftet).

## 3. Klemmenbelegung Master (HK1 + HK2)

| Ausgang/Eingang | Klemme | Bezeichnung (eigene Beschriftung) | Funktion |
|---|---|---|---|
| Tr1 | 7 | HK1-M1 (auf) | Nahwärme – Mischer auf |
| Tr2 | 6 | HK1-M1 (zu) | Nahwärme – Mischer zu |
| Tr3 | 4 | HK2-M2 (auf) | Heizung – Mischer auf |
| Tr4 | 3 | HK2-M2 (zu) | Heizung – Mischer zu |
| R4 | 15 | HK2-P4 | Heizung – Umwälzpumpe (offiziell P4) |
| S1 | 29 | Außenfühler | Außentemperatur |
| S2 | 28 | HK2 Rücklauf | Heizung – Rücklauf |
| S3 | 27 | HK1 Vorlauf | Nahwärme – Vorlauf (in Wärmetauscher WT1) |
| S4 | 26 | HK2 Vorlauf | Heizung – Vorlauf |
| S5 | 25 | HK1 Rücklauf | Nahwärme – Rücklauf (aus Wärmetauscher WT2, zum Netz) |
| S6 | 24 | Puffer oben | Anlegefühler, liegt im (ungenutzten) Kreis-3-Slot |
| S8 | 22 | Puffer unten | Anlegefühler, liegt im (ungenutzten) Kreis-3-Slot |

*Hinweis: R1, R2, R3 sowie die zu Kreis 3 gehörenden Pumpenausgänge (P2/P3) sind am Master nicht verdrahtet.*

## 4. Klemmenbelegung Slave (HK3)

| Ausgang/Eingang | Klemme | Bezeichnung (eigene Beschriftung) | Funktion |
|---|---|---|---|
| Tr1 | 7 | HK3-M1 (auf) | Fußbodenheizung – Mischer auf |
| Tr2 | 6 | HK3-M1 (zu) | Fußbodenheizung – Mischer zu |
| R1 | 11 | HK3-P1 | Fußbodenheizung – Umwälzpumpe (offiziell P1) |
| S3 | 27 | HK3 Vorlauf | Fußbodenheizung – Vorlauf |
| S5 | 25 | HK3 Rücklauf | Fußbodenheizung – Rücklauf |

## 5. Besonderheit: Kreis 3 (offiziell "WW") am Master

Im Display des Masters ist ein dritter Kreis mit den Pumpen **P2** (WW-Tauscherladepumpe) und **P3** (WW-Zirkulationspumpe) sowie einem Wärmetauscher-Symbol sichtbar. Das ist die im A267-Anwendungsschlüssel vorgesehene Warmwasser-Regelfunktion.

**Bei uns ist dieser Kreis funktionslos:** P2 und P3 sind nicht verdrahtet, es hängt keine reale Pumpe daran. Die Fühler **S6** und **S8** (Puffer oben/unten) wurden lediglich in diesen sonst ungenutzten Kreis-3-Fühler-Slot gelegt, um die Puffertemperatur oben/unten anzeigen zu können – sie lösen aber keine aktive Regelung über Kreis 3 aus. Die eigentliche Warmwasserbereitung läuft komplett getrennt über die externe Frischwasserstation (siehe Systemschema-Dokument).

## 6. Sollwerte / Heizkurven-Parameter

*Noch zu ergänzen – wird nachgereicht, sobald die Parametereinstellungen der beiden Regler vorliegen.*

Geplante Inhalte dieses Abschnitts:
- Heizkurve HK2 (Vorlauftemperatur je nach Außentemperatur)
- Heizkurve HK3 (falls witterungsgeführt genutzt)
- Puffer-Solltemperatur (Ziel für Kreis 1 / Nahwärme-Ladekreis)
- Rücklaufbegrenzung HK1 (Grenzwert Richtung Nahwärmenetz)
- Komfort-/Absenktemperaturen, Zeitprogramme, falls relevant
