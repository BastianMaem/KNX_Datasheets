---
title: MDT Schaltaktor AKS-Serie
device_type: Schaltaktor
manufacturer: MDT
article_number: [AKS-2416.03, AKS-01UP.03]
bus: KNX TP
source_pdf: originals/KNX/MDT_THB_AKI_03_04_AKS_03_Schaltaktor_V16.pdf
last_updated: 2026-07-25
synonyms: [Schaltausgang, Relaisaktor, Treppenlichtautomat, Schaltrelais]
tags: [knx, schaltaktor, mdt]
---

## Varianten

| Artikelnummer | Ausführung | Kanäle | Baubreite | Schaltleistung |
|---|---|---|---|---|
| AKS-2416.03 | REG (Reiheneinbau) | 24 | 12TE | 16A je Kanal |
| AKS-01UP.03 | UP (Unterputz) | 1 | – | 16A |

## Übersicht

Beide Varianten sind Schaltaktoren mit bistabilen Relais zum Schalten von 230VAC-Verbrauchern über den KNX-Bus. Jeder Kanal kann wahlweise als reiner Schaltausgang, als Treppenlichtkanal oder als Schaltimpuls-Ausgang (Kurzimpuls, z. B. für Türöffner/Klingel) betrieben werden. Die Parametrierung erfolgt pro Kanal individuell über die ETS.

Die REG-Variante AKS-2416.03 ist ein Reiheneinbaugerät mit 24 unabhängigen Kanälen, das für den Verteilerschrank vorgesehen ist. Sie besitzt Tasten zur Handbedienung mit LED-Statusanzeige sowie eine Sparmodus-Funktion zum automatischen Abschalten der LEDs.

Die UP-Variante AKS-01UP.03 ist ein Unterputzgerät mit nur einem Kanal, das direkt in einer Unterputzdose z. B. hinter einem Schalter oder einer Leuchte verbaut wird. Sie besitzt keine Tasten und keine Status-LEDs, wodurch die Parameter zur Handbedienung und zum LED-Sparmodus hier entfallen.

Funktional (Kanalparametrierung, Kommunikationsobjekte je Kanal, Treppenlicht-/Schaltimpulslogik) sind beide Varianten identisch; sie unterscheiden sich im Wesentlichen durch Bauform, Kanalanzahl und das Vorhandensein einer Handbedienung.

## Technische Daten

| Merkmal | AKS-2416.03 | AKS-01UP.03 |
|---|---|---|
| Nennspannung | 230VAC | 230VAC |
| Schaltleistung je Kanal | 16A | 16A |
| Kanalanzahl | 24 | 1 |
| Bauform | REG, 12TE | UP |
| C-Last (kapazitive Last) | 140µF | 140µF |
| Relaistyp | bistabiles Relais | bistabiles Relais |
| Handbedienung | ja (Tasten mit grüner Kanal-LED) | nicht vorhanden |
| Status-LEDs / Sparmodus | ja | nicht vorhanden |
| Anschluss | Schraubklemmen | Anschlusskabel |
| Schutzart | nicht im Datenblatt spezifiziert | nicht im Datenblatt spezifiziert |
| Montage | Hutschiene (DIN-Rail) | Unterputzdose |

## Kommunikationsobjekte

**Hinweis zur Objektnummerierung:** Bei AKS-2416.03 beginnen die Objekte mit Nr. 1 statt mit Nr. 0 wie bei den übrigen Geräten der Serie; alle nachfolgenden Objekte verschieben sich dadurch um eine Position. Bei AKS-01UP.03 gilt die Standardnummerierung ab Nr. 0. Objektnummern für Zentralfunktionen stehen bei allen Geräten am Ende der Objektliste und hängen von der Kanalanzahl ab (z. B. weit hinten bei 24 Kanälen, entsprechend früher bei nur 1 Kanal).

### Allgemeine Objekte (geräteweit)

| Nr. | Name | Funktion | DPT | Flags | Gilt für Variante(n) |
|---|---|---|---|---|---|
| * | Handbedienung sperren | Sperrt/entsperrt die Tasten am Gerät | 1 Bit | K, S | AKS-2416.03 |
| * | In Betrieb | Zyklisches "In Betrieb"-Telegramm | 1 Bit | K, L, A | AKS-2416.03, AKS-01UP.03 |

Das Objekt "In Betrieb" sendet zyklisch ein Telegramm, solange das Gerät normal arbeitet; bleibt dieses Telegramm aus, kann dies zur Ausfallüberwachung genutzt werden. "Handbedienung sperren" ist nur bei der REG-Variante relevant, da die UP-Variante keine Tasten besitzt.

### Kanalobjekte – Betriebsart "Schalten"

| Nr. (Basis) | Name | Funktion | DPT | Flags | Gilt für Variante(n) |
|---|---|---|---|---|---|
| 0 | Schalten Ein/Aus | Schaltet den Kanal (Relais) | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 4 | Sperren | Aktiviert/deaktiviert eine Kanalsperre | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 5 | Priorität | 1 Bit-Zwangsstellung EIN/AUS | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 5 | Zwangsführung | 2 Bit-Zwangsstellung (Control/Value) | 2 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 6 | Szene | Ruft eine Szene ab bzw. speichert sie | 1 Byte | K, S | AKS-2416.03, AKS-01UP.03 |
| 7 | Status | Meldet den aktuellen Schaltzustand | 1 Bit | K, L, Ü | AKS-2416.03, AKS-01UP.03 |
| 8 | invertierter Status | Meldet den invertierten Schaltzustand | 1 Bit | K, L, Ü | AKS-2416.03, AKS-01UP.03 |
| 9 | Logik 1 | Eingang für Logikverknüpfung | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 10 | Logik 2 | Eingang für Logikverknüpfung | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 11 | Schwellwertschalter | Empfängt den Analogwert für die Schwellwertfunktion | 1 Byte / 2 Byte | K, S | AKS-2416.03, AKS-01UP.03 |

Objektnummern erhöhen sich je Folgekanal um jeweils 12 (Basisblock pro Kanal).

Das Objekt "Schalten Ein/Aus" ist der zentrale Schalteingang des Kanals. "Sperren" blockiert die Bedienung des Kanals unabhängig davon, ob dies über Bus, Handbedienung oder Priorität geschieht – solange gesperrt ist, reagiert der Kanal nicht auf reguläre Schaltbefehle. "Priorität" und "Zwangsführung" erlauben eine übergeordnete, erzwungene Schaltstellung; dabei kann entweder ein einfaches 1-Bit-Objekt (fest EIN oder fest AUS je nach Parametrierung) oder das 2-Bit-Zwangsführungsobjekt mit den drei Zuständen "Zwangsführung EIN", "Zwangsführung AUS" und "Zwangsführung inaktiv" verwendet werden. Das Szenenobjekt dient dem Abrufen und optionalen Einlernen einer Szene mit zugeordnetem Verhalten (siehe ETS-Parameter Szenen). Die Statusobjekte (normal und invertiert) melden den aktuellen Schaltzustand des Kanals und eignen sich zur Rückmeldung an Taster/Visualisierung oder als Eingang für Logikfunktionen. Logik 1/2 sind die externen Eingänge für die im Kanal aktivierbare Verknüpfungslogik (UND/ODER/XOR/Tor), das Schwellwertschalter-Objekt nimmt einen Analogwert (Prozent, Zahlenwert, Temperatur oder Helligkeit) entgegen, anhand dessen der Kanal bei Über-/Unterschreitung eines Schwellwerts schalten kann.

### Kanalobjekte – Betriebsstundenzähler (optional je Kanal)

| Nr. (Basis) | Name | Funktion | DPT | Flags | Gilt für Variante(n) |
|---|---|---|---|---|---|
| 1 | Service erforderlich | Meldet anstehenden Servicebedarf | 1 Bit | K, L, A | AKS-2416.03, AKS-01UP.03 |
| 2 | Zeit bis zum nächsten Service | Verbleibende Servicestunden | 2 Byte / 4 Byte | K, L, A | AKS-2416.03, AKS-01UP.03 |
| 2 | Rückmeldung Betriebsstunden | Gesendete Betriebsstunden | 2 Byte / 4 Byte | K, L, A | AKS-2416.03, AKS-01UP.03 |
| 3 | Betriebsstunden rücksetzen | Setzt den Betriebsstundenzähler zurück | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 3 | Servicemeldung rücksetzen | Setzt die Servicestundenmeldung zurück | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |

Diese Objekte erscheinen nur, wenn im Kanal der Betriebsstundenzähler aktiviert wurde. Je nach gewählter Betriebsart (aufwärts zählender Betriebsstundenzähler oder Rückwärtszähler bis zum Service) stehen unterschiedliche Objekte zur Verfügung: Der aufwärts zählende Modus meldet fortlaufend die gesammelten Betriebsstunden, der Rückwärtszähler meldet die verbleibende Zeit bis zu einem Servicetermin und kann eine separate Servicemeldung auslösen.

### Kanalobjekte – Betriebsart "Treppenlicht"

| Nr. (Basis) | Name | Funktion | DPT | Flags | Gilt für Variante(n) |
|---|---|---|---|---|---|
| 0 | Schalten Ein/Aus | Zusätzliches, von der Treppenlichtzeit unabhängiges Schaltobjekt | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 1 | Treppenlicht | Löst die Treppenlichtzeit aus | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 3 | Vorwarnen | Meldet/steuert die Vorwarnung vor dem Ausschalten | 1 Bit | K, A | AKS-2416.03, AKS-01UP.03 |
| 4 | Sperren | Aktiviert/deaktiviert eine Kanalsperre | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 5 | Priorität | 1 Bit-Zwangsstellung | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 5 | Zwangsführung | 2 Bit-Zwangsstellung | 2 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 6 | Szene | Ruft eine Szene ab bzw. speichert sie | 1 Byte | K, S | AKS-2416.03, AKS-01UP.03 |
| 7 | Status | Meldet den aktuellen Schaltzustand | 1 Bit | K, L, Ü | AKS-2416.03, AKS-01UP.03 |
| 8 | invertierter Status | Meldet den invertierten Schaltzustand | 1 Bit | K, L, Ü | AKS-2416.03, AKS-01UP.03 |
| 33 | Treppenlicht mit Zeit | Startet die Treppenlichtzeit mit variabler, im Telegramm übertragener Dauer | 1 Byte | K, S | AKS-2416.03, AKS-01UP.03 |

Bei Kanalbetriebsart "Treppenlicht" stehen Logikfunktion, Schwellwertschalter und Betriebsstundenzähler nicht zur Verfügung. Das Objekt "Treppenlicht" startet den Ausschaltzeitgeber; nach Ablauf der parametrierten Zeit schaltet der Kanal automatisch ab. Über das Objekt "Treppenlicht mit Zeit" kann statt einer festen Zeit ein variabler Byte-Wert gesendet werden, aus dem sich die tatsächliche Treppenlichtzeit über einen parametrierbaren Zeitfaktor berechnet (Zeitfaktor × gesendeter Wert = Treppenlichtzeit) – nützlich, um z. B. je Etage eines Treppenhauses unterschiedliche Laufzeiten zu realisieren. Das optionale, zusätzliche Schaltobjekt "Schalten Ein/Aus" arbeitet unabhängig von der Treppenlichtzeit und ermöglicht ein dauerhaftes Ein-/Ausschalten desselben Kanals, z. B. für eine parallele Lüftungsfunktion. Das Vorwarnobjekt sendet bzw. reagiert auf eine Vorwarnung kurz vor dem automatischen Ausschalten. Sperren, Priorität/Zwangsführung, Szene sowie Status/invertierter Status funktionieren analog zur Schaltausgang-Betriebsart, wirken aber auf die Treppenlichtsteuerung.

### Kanalobjekte – Betriebsart "Schaltimpuls"

| Nr. (Basis) | Name | Funktion | DPT | Flags | Gilt für Variante(n) |
|---|---|---|---|---|---|
| 1 | Schaltimpuls | Löst den Schaltimpuls aus | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |
| 4 | Sperren | Objekt für den Sperrvorgang | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |

In dieser Betriebsart erzeugt der Kanal beim Empfang einer "1" auf das Objekt "Schaltimpuls" einen kurzen, parametrierbaren Schaltimpuls (z. B. für Garagentor- oder Klingelansteuerung). Andere Funktionen wie Logik, Szenen, Schwellwertschalter oder Betriebsstundenzähler stehen in dieser Betriebsart nicht zur Verfügung.

### Kanalobjekte – Zentralfunktion

| Nr. | Name | Funktion | DPT | Flags | Gilt für Variante(n) |
|---|---|---|---|---|---|
| * | Zentralfunktion – Schalten EIN/AUS | Schaltet gleichzeitig alle Kanäle mit aktivierter Zentralfunktion | 1 Bit | K, S | AKS-2416.03, AKS-01UP.03 |

Wird für einzelne Kanäle die Zentralfunktion aktiviert, so schalten diese Kanäle gemeinsam über dieses eine Zentralobjekt, ohne dass jeder Kanal einzeln adressiert werden muss. Die Objektnummer dieses Objekts liegt immer am Ende der Objektliste und ist daher von der Kanalanzahl abhängig (bei 24 Kanälen entsprechend hoch, bei der 1-kanaligen UP-Variante entsprechend niedrig).

## ETS-Parameter

### Allgemeine Einstellungen (geräteweit)

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Geräteanlaufzeit | 1 – 60 s | 1 s | AKS-2416.03, AKS-01UP.03 |
| "In Betrieb" zyklisch senden (0 = nicht aktiv) | 0 … 30000 min | 0 | AKS-2416.03, AKS-01UP.03 |
| Handbedienung | aktiv / gesperrt / sperrbar über Objekt | – | AKS-2416.03 |
| Sparmodus, LEDs abschalten nach | nicht aktiv / 30 s – 1 h | nicht aktiv | AKS-2416.03 |

Die Geräteanlaufzeit legt fest, wie lange nach einem Neustart vergeht, bis das Gerät funktionsbereit ist. Über das zyklische "In Betrieb"-Senden lässt sich der Aktor auf Busausfall überwachen. "Handbedienung" bestimmt, ob die Tasten am Gerät aktiv, dauerhaft gesperrt oder per Bus-Objekt sperrbar sind – dieser Parameter existiert nur bei der REG-Variante, da die UP-Variante keine Tasten besitzt. Ebenso ist der LED-Sparmodus, der die Status-LEDs nach einer definierten Zeit abschaltet, nur bei der REG-Variante relevant.

### Kanalauswahl

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Kanal X – Betriebsart | nicht aktiv / Schalten / Treppenlicht / Schaltimpuls / Einstellungen von Kanal A verwenden / synchron mit Kanal A schalten | nicht aktiv | AKS-2416.03, AKS-01UP.03 |

Für jeden Kanal wird individuell festgelegt, in welcher Betriebsart er arbeitet. Mit "Einstellungen von Kanal A verwenden" übernimmt ein Kanal automatisch die komplette Parametrierung von Kanal A (verfügbar ab Kanal B), was die Projektierung gleichartiger Kanäle beschleunigt. Mit "synchron mit Kanal A schalten" schaltet ein Kanal gleichzeitig mit Kanal A – diese Funktion ist auf jeweils maximal drei zusammengehörige Kanäle begrenzt (z. B. B und C synchron zu A) und eignet sich z. B. zur direkten Ansteuerung eines Drehstromverbrauchers ohne externes Schaltschütz. Da die UP-Variante nur einen Kanal besitzt, sind die Optionen "Einstellungen von Kanal A verwenden" und "synchron schalten" dort ohne praktische Bedeutung.

### Schaltausgang – Betriebsart und Verzögerungen

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Betriebsart | Schließer / Öffner | Schließer | AKS-2416.03, AKS-01UP.03 |
| Einschaltverzögerung | 0 … 30000 s | 0 s | AKS-2416.03, AKS-01UP.03 |
| Ausschaltverzögerung | 0 … 30000 s | 0 s | AKS-2416.03, AKS-01UP.03 |

Die Betriebsart legt fest, ob das Relais bei logisch "1" schließt (Schließer) oder öffnet (Öffner). Ein- und Ausschaltverzögerung verschieben den tatsächlichen Schaltzeitpunkt gegenüber dem Empfang des Bus-Telegramms; beide Verzögerungen lassen sich kombinieren. Wichtig: Diese Verzögerungen wirken nur bei Schaltbefehlen über Bus-Objekt (Kanal-Schaltobjekt oder Zentralfunktion) – die Handbedienung an der Taste reagiert stets sofort. Wird während der laufenden Verzögerung ein neuer, gegensätzlicher Schaltbefehl empfangen, gilt der zuletzt empfangene Befehl.

### Zentralfunktion (je Kanal)

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Zentralfunktion | nicht aktiv / aktiv | nicht aktiv | AKS-2416.03, AKS-01UP.03 |

Wird die Zentralfunktion für einen Kanal aktiviert, reagiert er zusätzlich auf das geräteweite Zentralfunktions-Objekt und schaltet dann gemeinsam mit allen anderen Kanälen, bei denen diese Option ebenfalls aktiv ist.

### Statusfunktionen (je Kanal)

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Status senden | nicht senden (passiv) / bei Änderung / bei Änderung und Sperre / immer bei Telegrammeingang | bei Änderung | AKS-2416.03, AKS-01UP.03 |
| Status zyklisch senden (0 = nicht aktiv) | 0 … 30000 s | 0 s | AKS-2416.03, AKS-01UP.03 |
| Zusätzlicher invertierter Status | nicht aktiv / aktiv | nicht aktiv | AKS-2416.03, AKS-01UP.03 |

Über "Status senden" wird festgelegt, unter welcher Bedingung das Statusobjekt aktiv auf den Bus sendet. Bei "bei Änderung und Sperre" wird der Status auch während eines aktiven Sperrvorgangs gesendet, sodass angeschlossene Taster stets den korrekten Zustand anzeigen. Über das zyklische Senden lässt sich der Status zusätzlich in festen Intervallen wiederholen (z. B. für Visualisierungen). Der zusätzliche invertierte Status stellt ein zweites Objekt bereit, das den jeweils entgegengesetzten Zustand meldet – nützlich für Logikverknüpfungen oder Folgefunktionen.

### Verhalten bei Sperren/Entsperren (Schaltausgang)

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Verhalten bei Sperren | AUS / EIN / keine Änderung | keine Änderung | AKS-2416.03, AKS-01UP.03 |
| Verhalten bei Entsperren | AUS / EIN / keine Änderung / vorheriger Zustand, Schalten nachholen / vorheriger Zustand | keine Änderung | AKS-2416.03, AKS-01UP.03 |

Solange ein Kanal gesperrt ist, ignoriert er reguläre Schaltbefehle. Beim Sperren kann der Kanal wahlweise aus- oder eingeschaltet werden oder seinen Zustand beibehalten. Beim Entsperren stehen zusätzlich die Optionen zur Verfügung, den Zustand vor dem Sperren wiederherzustellen – optional inklusive eines während der Sperre empfangenen, aber nicht ausgeführten Schaltbefehls ("Schalten nachholen").

### Priorität/Zwangsführung (Schaltausgang)

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Priorität/Zwangsführung | nicht aktiv / 2 Bit Zwangsführung / 1 Bit Priorität EIN / 1 Bit Priorität AUS | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Rückfallzeit (0 = nicht aktiv) | 0 … 600 min | 0 min | AKS-2416.03, AKS-01UP.03 |
| Verhalten nach Deaktivierung der Priorität | AUS / EIN / keine Änderung / vorheriger Zustand, Schalten nachholen / vorheriger Zustand | keine Änderung | AKS-2416.03, AKS-01UP.03 |

Ist eine Priorität oder Zwangsführung aktiv, wird der Kanal in einen festen Zustand gezwungen und kann währenddessen weder von Hand noch über das normale Schaltobjekt bedient werden. Über die Rückfallzeit lässt sich einstellen, nach welcher Zeit die Priorität/Zwangsführung automatisch wieder aufgehoben wird, ohne dass ein explizites Rücksetz-Telegramm nötig ist. Nach Deaktivierung der Priorität kann der Kanal AUS, EIN, unverändert bleiben oder – ähnlich wie beim Entsperren – den vorherigen Zustand (ggf. mit Nachholen eines zwischenzeitlichen Schaltbefehls) wiederherstellen.

### Verhalten bei Busspannungswiederkehr/-ausfall (Schaltausgang)

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Verhalten bei Busspannungswiederkehr | AUS / EIN / keine Änderung | keine Änderung | AKS-2416.03, AKS-01UP.03 |
| Verhalten bei Busspannungsausfall | AUS / EIN / keine Änderung | keine Änderung | AKS-2416.03, AKS-01UP.03 |

Legt fest, welchen Schaltzustand der Kanal beim Ausfall der Busspannung bzw. nach deren Rückkehr einnimmt.

### Logik (optional je Kanal, nur Betriebsart "Schalten")

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Logikfunktion | mit Schaltobjekt und einem Logikobjekt / mit Schaltobjekt und zwei Logikobjekten | mit Schaltobjekt und einem Logikobjekt | AKS-2416.03, AKS-01UP.03 |
| Logische Operation | ODER / UND / XODER / Tor offen mit Logikobjekt = 0 / Tor offen mit Logikobjekt = 1 | ODER | AKS-2416.03, AKS-01UP.03 |
| Eingänge invertieren | keine / diverse Kombinationen aus Schaltobjekt, Logikobjekt 1, Logikobjekt 2 | nicht invertieren | AKS-2416.03, AKS-01UP.03 |
| Ausgang invertieren | nicht invertieren / invertieren | nicht invertieren | AKS-2416.03, AKS-01UP.03 |
| Objekte nach Busspannungswiederkehr auf Wert setzen | nicht aktiv / aktiv (mit Werten je Objekt) | nicht aktiv | AKS-2416.03, AKS-01UP.03 |

Das Kanal-Schaltobjekt ist stets ein Eingang der Logik; zusätzlich lassen sich ein oder zwei externe Logikobjekte einbinden. Das Ergebnis der Verknüpfung wirkt direkt auf den Schaltausgang (Relais), ein separates Ausgangsobjekt gibt es nicht. Je nach gewählter Operation schaltet der Ausgang bei UND nur, wenn alle Eingänge aktiv sind, bei ODER bereits bei einem aktiven Eingang, bei XOR nur bei genau einem aktiven Eingang. Die "Tor"-Funktionen sperren bzw. geben das Schaltobjekt frei, abhängig vom Zustand der Logikobjekte. Eingänge und Ausgang lassen sich unabhängig voneinander invertieren. Über "Objekte nach Busspannungswiederkehr auf Wert setzen" kann verhindert werden, dass die Logikobjekte nach einem Reset einen undefinierten bzw. unerwünschten Zustand annehmen.

### Szenen (optional je Kanal)

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Szene lernen | nicht aktiv / aktiv / eingelernte Szenen behalten (keine Übernahme der Parameter) | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Szene A–H aktiv | nicht aktiv / aktiv | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Szene Nummer | 1 – 64 | – | AKS-2416.03, AKS-01UP.03 |
| Szene Verhalten (Schalten) | AUS / EIN / sperren / entsperren | AUS | AKS-2416.03, AKS-01UP.03 |
| Szene Verhalten (Treppenlicht) | AUS / EIN (= Treppenlichtzeit starten) / sperren / entsperren | AUS | AKS-2416.03, AKS-01UP.03 |

Jedem Kanal lassen sich bis zu 8 Speicherplätze (Szene A–H) zuordnen, denen jeweils eine Szenennummer (1–64) und ein auszuführendes Verhalten zugewiesen werden. Beim Aufruf über das Szenenobjekt wird der übertragene Wert immer um 1 kleiner interpretiert als die eingestellte Szenennummer (Szene 1 wird z. B. durch den Wert 0 aufgerufen; zum Speichern wird auf denselben Wert 128 addiert). Ist "Szene lernen" aktiviert, kann über einen entsprechend konfigurierten Taster ein neuer Wert für eine Szene dauerhaft gespeichert werden. Mit "eingelernte Szenen behalten" bleiben so gespeicherte Werte auch nach einer Neuprogrammierung der Applikation erhalten. Bei der Treppenlicht-Betriebsart bedeutet "EIN" als Szenenverhalten das Starten der Treppenlichtzeit, nicht ein dauerhaftes Einschalten.

### Schwellwertschalter (optional je Kanal, nur Betriebsart "Schalten")

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Werte Einstellung | 1 Byte Prozentwert (0…100%) / 1 Byte Wert (0…255) / 2 Byte Wert (0…65500) / 2 Byte Temperaturwert (-100…250°C) / 2 Byte Helligkeitswert (0…100000 Lux) | 1 Byte Prozentwert | AKS-2416.03, AKS-01UP.03 |
| Verhalten bei Unterschreitung | nicht aktiv / AUS / EIN | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Unterer Schwellwert | freie Eingabe | – | AKS-2416.03, AKS-01UP.03 |
| Verhalten bei Überschreitung | nicht aktiv / AUS / EIN | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Oberer Schwellwert | freie Eingabe | – | AKS-2416.03, AKS-01UP.03 |

Der Schwellwertschalter schaltet den Kanal in Abhängigkeit eines empfangenen Analogwertes (z. B. Temperatur, Helligkeit). Überschreitet der Wert den oberen Schwellwert, wird die dafür festgelegte Aktion ausgeführt; unterschreitet er den unteren Schwellwert, die dortige Aktion. Werte, die zwischen unterem und oberem Schwellwert liegen, verändern den Ausgangszustand nicht (Hystereseverhalten) – der Kanal schaltet also nur bei tatsächlichem Über- bzw. Unterschreiten der jeweiligen Grenze.

### Betriebsstundenzähler (optional je Kanal, nur Betriebsart "Schalten")

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Art des Betriebsstundenzählers | Betriebsstundenzähler / Rückwärtszähler bis zum Service | Betriebsstundenzähler | AKS-2416.03, AKS-01UP.03 |
| Datentyp | 4 Byte Wert in s (DPT 13.100) / 2 Byte Wert in h (DPT 7.007) | 4 Byte Wert in s | AKS-2416.03, AKS-01UP.03 |
| Melden der Betriebs-/Servicestunden alle … (0 = nicht aktiv) | 0 … 10000 h | 0 h | AKS-2416.03, AKS-01UP.03 |
| Betriebsstunden zyklisch senden | nicht aktiv / 10, 20, 30 min / 1, 2, 3, 4 h | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Servicemeldung in Abständen von | 0 … 60000 h | 0 h | AKS-2416.03, AKS-01UP.03 |

Der Betriebsstundenzähler summiert die Zeit, in der das Relais des Kanals geschlossen ist. In der Betriebsart "Betriebsstundenzähler" werden die aufgelaufenen Stunden gemeldet und können per Objekt zurückgesetzt werden. In der Betriebsart "Rückwärtszähler bis zum Service" zählt der Kanal ausgehend vom parametrierten Serviceintervall rückwärts und löst nach dessen Ablauf eine Servicemeldung aus (z. B. für einen anstehenden Filterwechsel); auch hier lässt sich der Zähler per Objekt auf den Ausgangswert zurücksetzen.

### Treppenlicht – Betriebsart und Grundzeit

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Betriebsart (Relais) | Schließer / Öffner | Schließer | AKS-2416.03, AKS-01UP.03 |
| Schaltobjekt (zusätzlich) | nicht aktiv / aktiv | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Treppenlichtzeit | 1 … 30000 s | 120 s | AKS-2416.03, AKS-01UP.03 |

Die Treppenlichtzeit legt fest, nach welcher Dauer der Kanal nach dem Auslösen automatisch wieder ausschaltet. Über das optionale zusätzliche Schaltobjekt kann derselbe Kanal parallel wie ein normaler Schaltausgang dauerhaft bedient werden (z. B. für Dauerlicht oder Lüftung), ohne die Treppenlichtlogik zu beeinflussen.

### Treppenlicht – Vorwarnung

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Vorwarnung | nicht aktiv / Licht Ein-/Ausschalten / Vorwarnobjekt / Licht Ein-/Ausschalten und Vorwarnobjekt | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Vorwarndauer | 0 … 30000 s | 1 s | AKS-2416.03, AKS-01UP.03 |
| Vorwarnzeit | 0 … 30000 s | 10 s | AKS-2416.03, AKS-01UP.03 |

Die Vorwarnung kündigt das bevorstehende automatische Ausschalten an. Bei "Licht Ein-/Ausschalten" wird das Licht kurz (Vorwarndauer) abgeschaltet und danach für die Vorwarnzeit nochmals eingeschaltet, bevor es endgültig ausgeht. Bei "Vorwarnobjekt" bleibt das Licht durchgehend an, während ein separates Objekt eine "1" sendet (z. B. zum Blinken einer Taster-LED); dies verlängert die Gesamtlaufzeit um die Vorwarnzeit. Die Kombination beider Varianten ist ebenfalls möglich. Insgesamt ergibt sich die Gesamtablaufzeit aus Treppenlichtzeit + Vorwarndauer + Vorwarnzeit.

### Treppenlicht – Manuelles Ausschalten und Zeitverlängerung

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Manuelles Ausschalten | nicht aktiv / aktiv | aktiv | AKS-2416.03, AKS-01UP.03 |
| Treppenlichtzeit verlängern | Zeit nicht verlängern / Zeit neu starten / Zeit aufaddieren | Zeit neu starten | AKS-2416.03, AKS-01UP.03 |
| Zeitfaktor für Objekt "Treppenlicht mit Zeit" | 1 s / 10 s / 1 min | 1 s | AKS-2416.03, AKS-01UP.03 |

Ist "Manuelles Ausschalten" aktiviert, kann der Kanal auch vor Ablauf der Treppenlichtzeit durch Senden einer "0" auf das Treppenlicht-Objekt vorzeitig abgeschaltet werden; andernfalls schaltet er stets erst nach vollständigem Zeitablauf. "Treppenlichtzeit verlängern" bestimmt das Verhalten bei erneuter Betätigung während einer laufenden Treppenlichtzeit: entweder wird die laufende Zeit ignoriert, komplett neu gestartet, oder die verbleibende Zeit wird um die volle Treppenlichtzeit aufaddiert (Mehrfachbetätigung verlängert damit die Gesamtlaufzeit). Der Zeitfaktor bestimmt, wie ein über das Objekt "Treppenlicht mit Zeit" gesendeter 1-Byte-Wert (0–255) in eine tatsächliche Zeit umgerechnet wird (Zeitfaktor × Wert = Treppenlichtzeit).

### Treppenlicht – Zentralfunktion, Status, Sperren

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Zentralfunktion | nicht aktiv / aktiv | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Status senden | nicht senden / bei Änderung / bei Änderung und Sperre / immer bei Telegrammeingang | bei Änderung | AKS-2416.03, AKS-01UP.03 |
| Status zyklisch senden (0 = nicht aktiv) | 0 … 30000 s | 0 s | AKS-2416.03, AKS-01UP.03 |
| Zusätzlicher invertierter Status | nicht aktiv / aktiv | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Verhalten bei Sperren | AUS / EIN / keine Änderung | keine Änderung | AKS-2416.03, AKS-01UP.03 |
| Verhalten bei Entsperren | AUS / Treppenlichtzeit starten | AUS | AKS-2416.03, AKS-01UP.03 |

Diese Parameter entsprechen inhaltlich den gleichnamigen Parametern der Betriebsart "Schalten". Ein wesentlicher Unterschied besteht beim Entsperren: Statt eines dauerhaften EIN kann hier nur die Treppenlichtzeit neu gestartet werden, da ein Treppenlichtkanal konzeptionell nicht dauerhaft eingeschaltet bleiben soll.

### Treppenlicht – Priorität/Zwangsführung, Busspannung

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Priorität/Zwangsführung | nicht aktiv / 2 Bit Zwangsführung / 1 Bit Priorität EIN / 1 Bit Priorität AUS | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Rückfallzeit (0 = nicht aktiv) | 0 … 600 min | 0 min | AKS-2416.03, AKS-01UP.03 |
| Verhalten nach Deaktivierung der Priorität | AUS / Treppenlichtzeit starten | AUS | AKS-2416.03, AKS-01UP.03 |
| Verhalten bei Busspannungswiederkehr | AUS / Treppenlichtzeit starten / Zustand vor Busspannungsausfall | Zustand vor Busspannungsausfall | AKS-2416.03, AKS-01UP.03 |
| Verhalten bei Busspannungsausfall | AUS / EIN / keine Änderung | keine Änderung | AKS-2416.03, AKS-01UP.03 |

Auch hier gilt bei Treppenlicht-Kanälen: Statt eines dauerhaften EIN nach Freigabe der Priorität/Zwangsführung oder nach Busspannungswiederkehr steht wiederum nur das Starten der Treppenlichtzeit zur Verfügung, um ein unkontrolliert dauerhaft eingeschaltetes Treppenlicht zu vermeiden.

### Schaltimpuls – Betriebsart und Impulszeiten

| Parameter | Werte | Standard | Gilt für Variante(n) |
|---|---|---|---|
| Betriebsart (Relais) | Schließer / Öffner | Schließer | AKS-2416.03, AKS-01UP.03 |
| Impulszeit | 300 ms – 30 s | 500 ms | AKS-2416.03, AKS-01UP.03 |
| Impulssignal einmal wiederholen | nicht aktiv / aktiv | nicht aktiv | AKS-2416.03, AKS-01UP.03 |
| Zeit bis zum nächsten Impuls | 0,5 s – 30 s | 0,5 s | AKS-2416.03, AKS-01UP.03 |
| Verhalten bei Sperren | AUS / keine Änderung | keine Änderung | AKS-2416.03, AKS-01UP.03 |
| Verhalten bei Entsperren | AUS / Schaltimpuls starten | AUS | AKS-2416.03, AKS-01UP.03 |

Die Betriebsart "Schaltimpuls" erzeugt bei Empfang einer "1" auf das Schaltimpuls-Objekt einen kurzen Ausgangsimpuls mit parametrierbarer Dauer (auch unterhalb einer Sekunde), z. B. zur Ansteuerung eines Garagentorantriebs. Optional lässt sich der Impuls nach einer definierten Pause automatisch ein weiteres Mal auslösen (z. B. doppeltes Klingeln). Beim Entsperren kann statt eines festen Zustands ebenfalls direkt ein neuer Schaltimpuls ausgelöst werden.

## Inbetriebnahme / Hinweise

- Bei AKS-2416.03 beginnt die Objektnummerierung mit 1 statt 0 wie bei den übrigen Geräten der Serie; dies ist bei der ETS-Programmierung sowie bei Referenzen auf Objektnummern zu beachten, da sich alle Folgeobjekte um eine Position verschieben.
- Objektnummern für Zentralfunktionen liegen stets am Ende der Objektliste und sind daher von der Kanalanzahl abhängig – bei AKS-2416.03 entsprechend hoch (viele Kanäle), bei AKS-01UP.03 entsprechend niedrig (nur 1 Kanal).
- Die Parameter "Handbedienung" und "Sparmodus, LEDs abschalten" sind ausschließlich bei der REG-Variante AKS-2416.03 verfügbar, da die UP-Variante keine Tasten und keine Status-LEDs besitzt.
- Bei Kanalbetriebsart "Treppenlicht" stehen die Funktionen Logik, Schwellwertschalter und Betriebsstundenzähler nicht zur Verfügung; bei "Schaltimpuls" stehen diese Zusatzfunktionen ebenfalls nicht zur Verfügung.
- Ein- und Ausschaltverzögerungen (Betriebsart "Schalten") wirken ausschließlich bei Schaltbefehlen über Bus-Objekte; die Handbedienung an der Taste (nur REG-Variante) reagiert stets unverzögert.
- Szenenwerte: Die parametrierte Szenennummer (1–64) unterscheidet sich vom über den Bus gesendeten Aufrufwert (0–63) um den Betrag 1; zum Speichern eines neuen Szenenwerts wird zusätzlich 128 auf den Aufrufwert addiert.
- Die grundlegende Inbetriebnahme (Busanschluss, Vergabe der physikalischen Adresse über die Programmiertaste, Laden der Applikation) läuft bei beiden Varianten identisch ab; die UP-Variante besitzt statt Schraubklemmen feste Anschlusskabel.
- Bei Verwendung eines Long-Frame-fähigen Programmier-Interfaces verkürzt sich die Programmierzeit ab ETS5 spürbar (gilt geräteübergreifend, nicht variantenspezifisch dokumentiert).

## Quelle

MDT Technisches Handbuch Schaltaktor AKI/AKS, Stand 06/2022, Version 1.6 – `originals/KNX/MDT_THB_AKI_03_04_AKS_03_Schaltaktor_V16.pdf`