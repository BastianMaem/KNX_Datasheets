---
title: MDT Binäreingang BE-16024.02
device_type: Binäreingang
manufacturer: MDT
article_number: [BE-16024.02]
bus: KNX TP
source_pdf: originals/KNX/MDT_THB_BE_02_Binaereingang_Tasterinterface.pdf
last_updated: 2026-07-25
synonyms: [Tasterinterface, Binäreingang, Schnittstelle für konventionelle Taster]
tags: [knx, binaereingang, mdt]
---

## Übersicht

Der MDT Binäreingang BE-16024.02 ist ein Reiheneinbaugerät (8 TE) mit 16 Eingangskanälen zum Anschluss konventioneller Taster, Schalter und potentialfreier Kontakte (Fensterkontakte, Reedkontakte etc.) an den KNX-Bus. Diese Geräteausführung ist für Steuersignale im Bereich 24 V AC/DC ausgelegt (im Gegensatz zu den Varianten für potentialfreie Kontakte oder 230 V AC).

Jeder Eingang kann in der ETS entweder einzeln oder paarweise gruppiert (z. B. A/B) betrieben werden. Je nach gewählter Betriebsart stehen unterschiedliche Funktionsblöcke zur Verfügung: einfaches Schalten, Wertsenden (Prozent-, Dezimal-, Farb-, Temperatur-, Helligkeits-, RGB-/HSV-Werte), Szenensteuerung, Jalousie-/Rollladensteuerung, Dimmen sowie eine Zählfunktion für Impuls- und Verbrauchszähler. Zusätzlich stellt das Gerät bis zu 4 unabhängige Logikbausteine (UND/ODER) bereit, die sowohl die eigenen Eingänge als auch extern über den Bus empfangene Werte verknüpfen können.

Eine LED-Ausgangsfunktion (Ansteuerung von Low-Current-LEDs) ist bei dieser Geräteausführung **nicht** verfügbar – diese Funktion ist laut Datenblatt ausschließlich den Unterputz-Tasterschnittstellen (BE-02001.02, BE-04001.02, BE-06001.02, BE-02230.02) vorbehalten.

## Technische Daten

| Merkmal | Wert |
|---|---|
| Artikelnummer | BE-16024.02 |
| Gerätetyp | Binäreingang 16-fach |
| Bauform | Reiheneinbaugerät (REG), 8 TE |
| Eingangsart | Steuersignale 24 V AC/DC |
| Anzahl Eingänge | 16 (einzeln oder paarweise gruppierbar, z. B. A/B, C/D …) |
| Schaltschwelle (24-V-Variante) | typ. 8 V AC / typ. 10 V DC |
| Busanschluss | KNX TP, über Busanschlussklemme |
| Anzahl Logikbausteine | 4 (UND/ODER-Verknüpfungen) |
| Status-LEDs | 1 grüne Kanal-LED je Eingang (zeigt nur den aktuellen Schaltzustand, keinen ETS-Sollzustand) |
| Programmierung | Programmiertaste (>1 s drücken), rote Programmier-LED |
| Long-Frame-Unterstützung | Ja, verkürzt Programmierzeit ab ETS5 (setzt Programmier-Interface mit Long-Frame-Unterstützung voraus, z. B. MDT SCN-USBR.02 oder SCN-IP000/100.02/03) |
| Zulassung | CE, für Betrieb in der EU; Einsatz in USA/Kanada laut Datenblatt nicht gestattet |
| Maße, Gewicht, Leistungsaufnahme | nicht im Datenblatt spezifiziert |
| Schutzart | nicht im Datenblatt spezifiziert |

## Kommunikationsobjekte

Die Objektnummern verschieben sich je nach aktivierter Funktion pro Eingang um einen festen Block ("+6 nächster Eingang" bei den Kanalobjekten); die Logikobjekte folgen erst nach allen Kanalobjekten und verschieben sich pro Logikbaustein um 3 ("+3 nächste Logik"). Flags: K = Kommunikation, L = Lesen, S = Schreiben, Ü = Übertragen, A = Aktualisieren.

### Grundfunktion Schalten / Umschalten / Zustand senden

| Objekt | Funktion | DPT / Größe | Flags |
|---|---|---|---|
| Eingang A / A,B | Schalten | 1 Bit | K, Ü |
| Eingang A | Umschalten | 1 Bit | K, Ü |
| Eingang A | Status für Umschaltung | 1 Bit | K, L, Ü, A |
| Eingang A | Zustand senden | 1 Bit | K, L, Ü |
| Eingang A / A,B | Zwangsführung | 2 Bit | K, Ü |
| Eingang A (kurz/lang/Gruppe lang/Gruppe extra lang) | Schalten, Umschalten, Zwangsführung | 1/2 Bit | K, Ü |
| Eingang A zusätzliches Objekt | Schalten / Umschalten / Zustand senden (auch invertiert) | 1 Bit | K, Ü |
| Eingang A | Sperrobjekt | 1 Bit | K, S, Ü, A |

Das Objekt **„Schalten"** sendet bei Betätigung des Eingangs einen festen oder von der Flanke abhängigen 1-Bit-Wert, je nach eingestellter Unterfunktion (siehe ETS-Parameter). Das Objekt **„Umschalten"** invertiert bei jeder Betätigung den zuletzt bekannten Wert; damit dieser Wert korrekt bekannt ist, muss das zugehörige Objekt **„Status für Umschaltung"** mit dem Statusobjekt des angesteuerten Aktors verknüpft werden – sonst sendet das Gerät nach einem Reset im Zweifel immer eine „1". Das Objekt **„Zustand senden"** wird für tastende Anwendungen wie Fensterkontakte genutzt und ist inhaltlich identisch mit der Funktion „Kontaktzustand senden" (siehe unten). Die **Zwangsführung** dient dazu, einen Aktorkanal in einen definierten Zustand zu zwingen (z. B. bei zentralen Sicherheitsfunktionen). Das **zusätzliche Objekt** (ggf. invertiert) erlaubt es, denselben Tastendruck parallel auf eine zweite Gruppenadresse zu senden. Das **Sperrobjekt** blockiert bei „1" den zugehörigen Kanal bzw. das Kanalpaar vollständig gegen Schaltvorgänge; mit „0" wird die Sperre wieder aufgehoben.

### Werte senden (Prozent-, Dezimal-, Farb-, Temperatur-, Helligkeits-, RGB/HSV-Werte)

| Objekt | Funktion | DPT / Größe | Flags |
|---|---|---|---|
| Eingang A / A,B | Prozentwert / Dezimalwert / Szene | 1 Byte | K, Ü |
| Eingang A / A,B | Farbtemperatur / Temperatur / Helligkeit | 2 Byte | K, Ü |
| Eingang A / A,B | RGB-Wert / HSV-Wert | 3 Byte | K, Ü |
| Eingang A / A,B | Status Prozentwert / Status Dezimalwert / Status Farbtemperatur / Status Temperatur / Status Helligkeit | 1–2 Byte | K, Ü, A |

Diese Objekte senden je nach gewähltem Datenpunkttyp fest parametrierte Werte (z. B. beim Schließen/Öffnen des Kontakts, bei Mehrfach-Tippfunktion oder beim Verschieben eines Werts). Die zugehörigen **Status-Objekte** werden benötigt, wenn ein Wert relativ verschoben werden soll (Funktion „Wert verschieben"), damit das Gerät den zuletzt gültigen Wert kennt, von dem aus es weiterrechnet.

### Zählen

| Objekt | Funktion | DPT / Größe | Flags |
|---|---|---|---|
| Eingang A | Zählimpuls | 1 Bit | K, Ü |
| Eingang A | Schwellwert Zähler | 1 Bit | K, L, Ü |
| Eingang A | Zählerstand | 1/2/4 Byte | K, L, S, Ü |
| Eingang A | Momentanwert | 1/2/4 Byte | K, L, Ü |
| Eingang A | Durchfluss | 2/4 Byte | K, L, Ü |
| Eingang A | Elektrische Leistung | 2/4 Byte | K, L, Ü |
| Eingang A | Zähler zurücksetzen | 1 Bit | K, S, Ü |

Das Objekt **„Zählimpuls"** wird beim einfachen Impulstelegramm (Teiler-Betrieb) genutzt. Der **„Zählerstand"** kann bei aktivem S-Flag auch extern beschrieben werden, um dem Zähler einen individuellen Startwert vorzugeben statt bei „0" zu beginnen. **„Momentanwert"**, **„Durchfluss"** und **„Elektrische Leistung"** stehen nur beim Zählertyp Verbrauchszähler zur Verfügung und geben je nach gewählter Messgröße (Leistung, Wasser/Gas, individuelle Messgröße) die aktuell berechnete Rate aus. Über **„Zähler zurücksetzen"** wird der interne Zählerstand mit einer „1" auf null gesetzt.

### Jalousie/Rollladen

| Objekt | Funktion | DPT / Größe | Flags |
|---|---|---|---|
| Eingang A / A,B | Jalousie Auf/Ab (bzw. „Fahren") | 1 Bit | K, Ü |
| Eingang A / A,B | Stopp/Lamellen Auf/Zu | 1 Bit | K, Ü |
| Eingang A | Status für Richtungswechsel | 1 Bit | K, L, Ü, A |
| Eingang A/B kurz | Rollladen Auf/Ab/Stopp (MDT Single Object Control) | 1 Bit | K, Ü |
| Eingang A/B lang | Zentral Rollladen Auf/Ab/Stopp (MDT Single Object Control) | 1 Bit | K, Ü |

Das **Bewegobjekt** („Jalousie Auf/Ab") startet die Auf- oder Abfahrt, das **Stopp-/Schrittobjekt** stoppt eine laufende Fahrt bzw. verstellt die Lamellen in Schritten. Bei gruppierten Kanälen bestimmt die Eingangsbelegung (Auf/Ab bzw. Ab/Auf), welcher der beiden Eingänge welches Signal auslöst. **MDT Single Object Control** ist ein alternatives, kompaktes Bedienkonzept für Rollladenaktoren, bei dem ein einzelnes Objekt sowohl Start als auch Stopp der Fahrt übernimmt; dazu muss im Jalousieaktor der Parameter „Auf/Ab kann stoppen (Single Object Control)" aktiv sein.

### Dimmen

| Objekt | Funktion | DPT / Größe | Flags |
|---|---|---|---|
| Eingang A / A,B | Dimmen Ein/Aus | 1 Bit | K, Ü |
| Eingang A / A,B | Dimmen relativ | 4 Bit | K, Ü |
| Eingang A | Status für Umschaltung | 1 Bit | K, L, Ü, A |

Beim einzelnen Kanal löst ein kurzer Tastendruck das Schaltobjekt „Dimmen Ein/Aus" aus, ein langer Tastendruck startet über „Dimmen relativ" ein Start-Stopp-Dimmen (Senden von Heller/Dunkler-Telegrammen, solange die Taste gedrückt bleibt, mit abschließendem Stopp-Telegramm beim Loslassen).

### Szene

| Objekt | Funktion | DPT / Größe | Flags |
|---|---|---|---|
| Eingang A | Szene | 1 Byte | K, Ü |

Über dieses Objekt werden Szenen aufgerufen (Werte 0–63) oder – bei aktivierter Speicherfunktion und langem Tastendruck – neu abgespeichert (Werte 128–191, jeweils Szenennummer + 128).

### Logik (pro Logikbaustein)

| Objekt | Funktion | DPT / Größe | Flags |
|---|---|---|---|
| Logik x: Eingang 1A | externes Logikobjekt A | 1 Bit | K, S, Ü, A |
| Logik x: Eingang 1B | externes Logikobjekt B | 1 Bit | K, S, Ü, A |
| Logik x: Ausgang | Ausgang der Verknüpfung | 1 Bit / 1 Byte / 2 Bit | K, L, S |

Die Logikobjekte sind unabhängig von der Kanalkonfiguration und erscheinen erst, wenn der jeweilige Logikbaustein in der ETS aktiviert wurde. Die externen Eingangsobjekte („Eingang 1A/1B") können sowohl mit den eigenen Kanälen als auch mit beliebigen externen Busteilnehmern verknüpft werden.

## ETS-Parameter

### Allgemeine Einstellungen

| Parameter | Wertebereich | Standard |
|---|---|---|
| Geräteanlaufzeit | 2 – 240 s | 2 s |
| „In Betrieb" zyklisch senden | nicht aktiv, 1 min – 4 h | nicht aktiv |
| Eingangswerte für Logiken (nach Busspannungswiederkehr) | nicht abfragen / abfragen | abfragen |
| Status für Umschaltung (nach Busspannungswiederkehr) | nicht abfragen / abfragen | abfragen |
| Entprellzeit Eingänge | 10 – 150 ms | 30 ms |
| Zeit langer Tastendruck (Grundeinstellung) | 0,1 – 30 s | 0,5 s |

Diese Werte gelten geräteweit. Ist „Eingangswerte für Logiken – abfragen" aktiv, fragt das Gerät nach einem Busspannungsausfall die externen Logikobjekte erneut ab und wertet die Logik neu aus; bleibt eine Antwort aus, gilt die parametrierte Vorbelegung. Analog sorgt „Status für Umschaltung – abfragen" dafür, dass nach einem Reset der tatsächliche Aktorstatus abgefragt wird, bevor der nächste Umschaltbefehl gesendet wird – ohne diese Abfrage sendet das Gerät im Zweifel immer eine „1". Die Entprellzeit verhindert Mehrfachtelegramme durch mechanisches Kontaktprellen. Die „Zeit langer Tastendruck (Grundeinstellung)" ist der geräteweite Default-Wert, der überall dort greift, wo für einen Eingang keine individuelle Zeit definiert wurde.

### Eingänge aktivieren

| Parameter | Wertebereich | Standard |
|---|---|---|
| Funktion Eingang A/B – O/P (je Kanalpaar) | nicht aktiv / Kanäle einzeln / Kanäle gruppiert | nicht aktiv |

Jedes der 8 Kanalpaare (A/B … O/P) wird separat auf „nicht aktiv", „Kanäle einzeln" oder „Kanäle gruppiert" gestellt. Bei „nicht aktiv" ist der Kanal nicht weiter parametrierbar. Bei „Kanäle einzeln" verhält sich jeder Eingang eigenständig, bei „Kanäle gruppiert" bilden zwei Eingänge ein funktionales Paar (z. B. Auf/Ab bei Jalousie, Heller/Dunkler bei Dimmen).

### Funktionen der Eingänge – Schalten allgemein

| Parameter | Wertebereich | Standard |
|---|---|---|
| Wert senden beim (nur gruppiert) | Schließen / Öffnen | Schließen |
| Wert 1./2. Eingang (nur gruppiert) | Ein/Aus / Aus/Ein | Ein/Aus |
| Unterfunktion (nur einzeln) | Schalten beim Schließen, Schalten beim Öffnen, Umschalten beim Schließen, Umschalten beim Öffnen, Umschalten beim Schließen und Öffnen, Zustand senden | Schalten beim Schließen |
| Sonderfunktion | Innovative Gruppensteuerung, Zusätzliches Schaltobjekt, Zusätzliches Schaltobjekt invertiert | – |
| Gruppe langer/extra langer Tastendruck | nicht aktiv / aktiv | nicht aktiv |
| Gruppe lang/extra lang sendet | Ein und Aus / Nur Ein / Nur Aus | Ein und Aus |
| Zeit extra langer Tastendruck | 0,1 – 30 s | 2,0 s |
| Zusätzliches Schaltobjekt sendet (ggf. invertiert) | Ein und Aus / Nur Ein / Nur Aus | Ein und Aus |

Bei gruppierten Kanälen bestimmt „Wert senden beim" und „Wert 1./2. Eingang", welcher der beiden Eingänge welchen Wert bei welcher Flanke sendet. Bei einzelnen Kanälen erlaubt die **Unterfunktion**, das Verhalten pro Flanke individuell festzulegen. Die **Innovative Gruppensteuerung** ermöglicht es, mit einem langen bzw. extra langen Tastendruck zusätzliche Telegramme auf eigene Gruppenadressen zu senden (z. B. kurz = Raum, lang = Etage, extra lang = Gebäude); alle Gruppen werden dabei nacheinander ausgelöst, sobald die jeweilige Haltezeit erreicht ist. Das **zusätzliche Schaltobjekt** (ggf. invertiert) dupliziert den Schaltbefehl parallel auf ein zweites Objekt/Gruppenadresse.

### Kontaktzustand senden

| Parameter | Wertebereich | Standard |
|---|---|---|
| Wert Kontakt geschlossen / geöffnet | Aus / Ein / nicht aktiv | Aus / Ein |
| Sendeverzögerung | nicht aktiv, aktiv, aktiv für Kontakt geschlossen, aktiv für Kontakt geöffnet | nicht aktiv |
| Verzögerung | 1 s – 6 h | 10 s |
| Zyklisch senden | nicht aktiv / aktiv | nicht aktiv (im Beispiel: aktiv) |
| Zyklisch senden alle | 1 s – 6 h | 5 min |
| Verhalten bei Busspannungswiederkehr | keine Aktion / Zustand senden | keine Aktion |
| Sonderfunktion | nicht aktiv, zusätzliches Objekt, zusätzliches Objekt invertiert | nicht aktiv |
| Sperrobjekt | nicht aktiv / aktiv | nicht aktiv |
| Verhalten bei Sperre | keine Aktion / Kontakt geschlossen / Kontakt geöffnet (bzw. mit zyklischem Senden kombiniert) | je nach „Zyklisch senden" |

Diese Funktion ist für tastende Anwendungen wie Fensterkontakte gedacht: Für geschlossenen und geöffneten Kontakt können getrennte feste Werte definiert werden. Die **Sendeverzögerung** verzögert das Aussenden eines oder beider Werte um eine feste Zeit; ändert sich der Zustand vor Ablauf dieser Zeit erneut, verfällt die Verzögerung. Mit **„Zyklisch senden"** wird der aktuelle Zustand in festen Abständen wiederholt gesendet, was z. B. bei sicherheitsrelevanten Meldungen (Fenster offen) sinnvoll ist. Das **Sperrobjekt** legt fest, was während einer aktiven Sperre gesendet wird (nichts, ein fester Wert einmalig oder zyklisch, abhängig davon, ob zyklisches Senden aktiv ist).

### Werte senden – Unterfunktionen

**Werte senden (Basisfunktion):**

| Parameter | Wertebereich | Standard |
|---|---|---|
| Wert senden beim | Schließen / Öffnen | Schließen |
| Datenpunkttyp | DPT 1.001, 2.001, 5.001, 5.005, 17.001, 7.600, 9.001, 9.004, 232.600 (RGB) | DPT 5.001 |
| Wert 1./2. Eingang (gruppiert) bzw. Wert (einzeln) | beliebig gemäß DPT | – |
| Sonderfunktion | innovative Gruppensteuerung / zusätzliches Objekt | innovative Gruppensteuerung |

**Werte/Szenen umschalten (bis zu 4 Werte):**

| Parameter | Wertebereich | Standard |
|---|---|---|
| Belegung der Eingänge (gruppiert) | nächster/vorheriger / vorheriger/nächster | nächster/vorheriger |
| Anzahl der Werte | 2 / 3 / 4 | 2 |
| 1.–4. Umschaltwert | beliebig gemäß DPT | – |
| Langer Tastendruck | nicht aktiv / aktiv | nicht aktiv |
| Aktion bei langem Tastendruck | 1.–4. Umschaltwert, 4. wenn vorher 1., 0 senden, Ein/Aus auf zweites Objekt | – |
| Umschaltart (gruppiert) | Anschlag / Überlauf | Anschlag |

Bei kurzem Tastendruck wird nacheinander zum jeweils nächsten Umschaltwert weitergeschaltet. Bei **„Anschlag"** bleibt der letzte Wert stehen, bei **„Überlauf"** springt die Funktion nach dem letzten wieder zum ersten Wert (bei Einzelkanälen ist immer Überlauf fest eingestellt).

**Wert verschieben (nur gruppierte Kanäle):**

| Parameter | Wertebereich | Standard |
|---|---|---|
| Datenpunkttyp | 1 Byte (0…100 %) / 1 Byte (0…255) | 1 Byte (0…100 %) |
| Unterer/Oberer Grenzwert | 0–100 % bzw. 0–255 | 0 % / 100 % |
| Schrittweite | 1–100 % bzw. 1–255 | 10 % |
| Wiederholtes Senden bei gedrückter Taste | nicht aktiv / aktiv | nicht aktiv |
| Wiederholungszeit | 0,1 – 30 s | Grundeinstellung |

Ein Eingang erhöht, der andere verringert den Wert innerhalb der eingestellten Grenzen um die definierte Schrittweite je Tastendruck; bei aktivem wiederholtem Senden läuft der Wert bei gehaltener Taste automatisch bis zur Grenze durch.

**Werte senden nach Zustand:** analog zu „Kontaktzustand senden", jedoch mit frei wählbarem Datenpunkttyp (u. a. DPT 2.001, 5.001, 5.005, 7.600, 9.001, 9.004, 17.001, 232.600) statt fixem 1-Bit-Wert; Sendeverzögerung, zyklisches Senden und Verhalten bei Busspannungswiederkehr funktionieren analog zur Kontaktzustand-Funktion.

**Mehrfach-Tippfunktion (Werte senden nach Anzahl Betätigungen):**

| Parameter | Wertebereich | Standard |
|---|---|---|
| Ausgangsobjekte | gemeinsames Objekt/DPT / verschiedene Objekte/DPT | gemeinsames Objekt/DPT |
| Anzahl Tipp-Betätigungen | 2× / 3× | 2× |
| Wert für 1×/2×/3× tippen | beliebig gemäß DPT | – |
| 3./4. Funktion über langen Tastendruck | nicht aktiv / aktiv | nicht aktiv |
| Max. Zeit zwischen zwei Betätigungen | 0,1 – 30 s | 1,0 s |

Je nachdem, wie oft die Taste innerhalb der „Max. Zeit zwischen zwei Betätigungen" hintereinander gedrückt wird, sendet der Eingang unterschiedliche, frei definierbare Werte. Eine schnelle Reaktionszeit der Bedienung wird laut Datenblatt empfohlen.

### Schalten/Werte senden kurz/lang (mit 2 Objekten)

| Parameter | Wertebereich | Standard |
|---|---|---|
| Aktion kurzer/langer Tastendruck | Schalten (gruppiert) / Schalten Aus / Schalten Ein (einzeln) / Umschalten / Werte senden / nicht aktiv | Schalten |
| Verhalten bei langem Tastendruck | kurz nicht senden / kurz senden | kurz nicht senden |
| Sendebedingung für langen Tastendruck (gruppiert) | 1. und 2. Eingang sendet / nur 1. / nur 2. | 1. und 2. Eingang sendet |

Kurzer und langer Tastendruck können unterschiedliche Funktionen und sogar unterschiedliche Kommunikationsobjekte ansteuern; damit lassen sich z. B. „kurz = Licht schalten" und „lang = Dimmwert senden" auf einem einzigen Taster kombinieren.

### Szene

| Parameter | Wertebereich | Standard |
|---|---|---|
| Szene speichern | nicht aktiv / aktiv | nicht aktiv |
| Wert senden beim | Schließen / Öffnen | Schließen |
| Zeit langer Tastendruck | Grundeinstellung, 0,1–30 s | Grundeinstellung |
| Szenen-Nummer | 1–64 | 1 |

Bei aktivierter Speicherfunktion löst ein kurzer Tastendruck den Szenenaufruf aus, ein langer Tastendruck (≥ eingestellte Zeit) speichert die aktuellen Werte unter derselben Szenennummer ab. Für Abruf und Speichern werden unterschiedliche Codes auf dem 1-Byte-Objekt gesendet (Speichern = Szenennummer − 1 + 128).

### Jalousie/Rollladen

| Parameter | Wertebereich | Standard |
|---|---|---|
| Funktion 1./2. Eingang (gruppiert) | Auf/Ab / Ab/Auf | Auf/Ab |
| Bedienfunktion | Lang=Auf/Ab, Kurz=Stopp/Lamellen; Kurz=Auf/Ab, Lang=Stopp/Lamellen; Kurz=Auf/Ab/Stopp (Single Object Control); Kurz=Auf/Ab/Stopp / Lang=Zentralobjekt (Single Object Control); betätigt=Auf/Ab / losgelassen=Stopp | Lang=Auf/Ab, Kurz=Stopp/Lamellen |
| Zeit langer Tastendruck | Grundeinstellung, 0,1–30 s | Grundeinstellung |
| Gruppensteuerung extra lang | nicht aktiv / aktiv | nicht aktiv |
| Zeit extra langer Tastendruck | 0,1–30 s | 2,0 s |

Das Bedienkonzept legt fest, ob kurzer oder langer Tastendruck die Fahrt startet und was den Stopp bzw. die Lamellenverstellung auslöst. Die Bedienfunktionen mit „MDT Single Object Control" sowie „betätigt/losgelassen" (Totmannschaltung – der Behang verfährt nur, solange die Taste gehalten wird) stehen nur bei gruppierten Kanälen zur Verfügung. Die **innovative Gruppensteuerung (extra lang)** ermöglicht bei extra langem Tastendruck zusätzlich zur Einzeljalousie das zeitversetzte Anfahren einer ganzen Gruppe von Behängen; nach ca. 90 s deaktiviert sich diese Gruppensteuerung automatisch wieder.

### Dimmen

| Parameter | Wertebereich | Standard |
|---|---|---|
| Funktion 1./2. Eingang (gruppiert) | heller/dunkler / dunkler/heller | heller/dunkler |
| Zeit langer Tastendruck | Grundeinstellung, 0,1–30 s | Grundeinstellung |

Kurzer Tastendruck schaltet ein/aus, langer Tastendruck startet ein Start-Stopp-Dimmen in die parametrierte Richtung. Bei Einzelkanälen wird die Dimmrichtung in Abhängigkeit des Objekts „Status für Umschaltung" umgekehrt.

### Zählen

| Parameter | Wertebereich | Standard |
|---|---|---|
| Zählen beim | Schließen / Öffnen | Schließen |
| Entprellzeit für Zählimpuls | 10–150 ms | 10 ms |
| Zählertyp | Impulstelegramm (Teiler) / Einfacher Zähler / Verbrauchszähler | Verbrauchszähler |
| Senden EIN alle (Teiler) | 1–65535 Impulse | 100 |
| Datenpunkt Zähler (einfacher Zähler) | DPT 1.001, 5.005, 7.\*, 8.\*, 9.\*, 12.\*, 13.\*, 14.\* | DPT 9.\* |
| Schwellwert = „Ein" wenn mehr als (bei 1-Bit-Zähler) | 1–50000 Impulse | 1000 |
| Messgröße (Verbrauchszähler) | Leistung (kWh) / Wasser-Gas (m³) / Individuell | Leistung (kWh) |
| Anzahl Impulse je kWh bzw. m³ bzw. Einheit | 1–10000 (kWh/m³), 1–100000 (individuell) | 1000 |
| Senden bei Änderung Zähler (Leistung) | 1 Wh / 10 Wh / 100 Wh / 1 kWh | 1 kWh |
| Senden bei Änderung Zähler (Wasser/Gas) | 0,001 / 0,01 / 0,1 / 1 m³ | – (geräteabhängig eingeschränkt) |
| Zyklisch senden / Zyklisch senden alle | nicht aktiv/aktiv; 1 s – 6 h | nicht aktiv / 5 min |

Der Zähler unterscheidet drei Betriebsarten: Als **Impulstelegramm (Teiler)** wird nur alle X Impulse ein EIN-Telegramm gesendet. Als **einfacher Zähler** wird der Zählerstand in einem frei wählbaren Datenpunkttyp geführt (bei DPT 1.001 als Schwellwert-Schaltfunktion). Als **Verbrauchszähler** berechnet das Gerät zusätzlich Momentanwerte (Leistung, Durchfluss) aus dem Impulsabstand. Der Zählerstand bleibt bei Busspannungsausfall und nach Neuprogrammierung erhalten und kann über das Objekt „Zähler zurücksetzen" auf null gesetzt werden; ein individueller Startwert lässt sich bei aktivem S-Flag direkt auf das Zählerstand-Objekt schreiben. Laut Datenblatt beträgt die Reaktionszeit der Durchflussberechnung 1–10 Minuten, der minimal messbare Durchfluss liegt bei ca. 6 l/h, die minimale erfassbare elektrische Leistung bei ca. 6 W. Bei der Messgröße „Wasser/Gas" gelten geräteabhängige Einschränkungen bei „Senden bei Änderung Zähler" und der Auflösung (z. B. nur ganzzahlige bzw. Zehntel-Werte je nach gewähltem DPT).

### LED-Ausgang

Dieser Parameterblock ist bei der Geräteausführung BE-16024.02 **nicht vorhanden**. Laut Datenblatt steht die LED-Ausgangsfunktion ausschließlich bei den Tasterschnittstellen/-interfaces (BE-02001.02, BE-04001.02, BE-06001.02, BE-02230.02) zur Verfügung.

### Logik

| Parameter | Wertebereich | Standard |
|---|---|---|
| Einstellung Logik 1–4 | nicht aktiv / UND (wahr, wenn alle Eingänge 1) / ODER (wahr, wenn mind. ein Eingang 1) / Wert senden bei Kontakt geschlossen | nicht aktiv |
| Objekttyp | Schalten / Szene / Wert / Zwangsführung 2 Bit | Schalten |
| Szene-Nummer / 1-Byte-Wert / Zwangsführung | beliebig gemäß DPT | – |
| Sendebedingung (nur „Schalten") | nicht automatisch / bei Eingangstelegramm-Kontaktänderung / bei Änderung Ausgang / bei Änderung Ausgang (nur 0) / bei Änderung Ausgang (nur 1) | bei Änderung Ausgang |
| Ausgang invertiert (nur „Schalten") | Nein / Ja | Nein |
| Logikobjekt 1 A/B (extern) | nicht aktiv / normal bzw. invertiert eingeschaltet, mit Vorbelegung 0 bzw. 1 | nicht aktiv |
| Eingang A–P (je nach Gerät) | nicht aktiv / Kontakt geschlossen = Wert 1 / Kontakt geschlossen = Wert 0 | nicht aktiv |

Jeder der vier Logikbausteine verknüpft beliebig viele eigene Eingänge sowie bis zu zwei externe Logikobjekte per UND oder ODER. Ist die Bedingung erfüllt, wird der eingestellte Ausgangswert gesendet; beim Objekttyp „Schalten" lässt sich zusätzlich festlegen, ob und wann gesendet wird (z. B. nur bei Änderung, oder nur „0"/„1"-Werte) und ob der Ausgang invertiert wird. Die **Vorbelegung** der externen Logikobjekte bestimmt den angenommenen Wert direkt nach Busspannungswiederkehr, solange noch kein tatsächliches Telegramm empfangen wurde. Ein typisches Anwendungsbeispiel ist die zentrale Überwachung aller Fensterkontakte eines Geschosses über eine ODER-Verknüpfung: Solange alle Fenster geschlossen sind, meldet der Logikausgang „0"; sobald mindestens ein Fenster offen ist, wird eine „1" gesendet.

## Inbetriebnahme / Hinweise

- Reihenfolge der Inbetriebnahme: Schnittstelle an den Bus anschließen → Busspannung zuschalten → Programmiertaste am Gerät >1 s drücken (rote LED leuchtet) → physikalische Adresse aus der ETS laden (LED erlischt) → Applikation mit gewünschter Parametrierung laden → Netzspannung zuschalten → Funktion prüfen.
- Die grünen Kanal-LEDs zeigen ausschließlich den aktuellen physischen Schaltzustand des Eingangs an, nicht den in der ETS parametrierten Soll-/Sendezustand.
- Für die Umschaltfunktion muss das Objekt „Status für Umschaltung" zwingend mit dem Statusobjekt des angesteuerten Aktors verknüpft werden, damit nach einem Reset korrekt umgeschaltet wird; ohne Aktor kann ersatzweise das eigene „Schalten"-Objekt verknüpft werden.
- Bei der Zählfunktion sollte der Zählerstand nach Erreichen eines Schwellwerts (1-Bit-Zähler) aktiv über das Objekt „Zähler zurücksetzen" zurückgesetzt werden, da sonst dauerhaft nur noch EIN-Telegramme gesendet werden.
- Long-Frame-Unterstützung verkürzt die Programmierzeit ab ETS5 deutlich, setzt aber ein entsprechend fähiges Programmier-Interface voraus (z. B. MDT SCN-USBR.02, SCN-IP000/100.02/03).
- Alle Installations- und Anschlussarbeiten dürfen laut Datenblatt nur durch Elektrofachkräfte erfolgen; vor Arbeiten am Gerät ist die vorgeschaltete Sicherung spannungsfrei zu schalten.

## Quelle

MDT technologies GmbH, Technisches Handbuch „MDT Binäreingang / MDT Tasterschnittstelle/-interface", Serie .02, Stand 01/2022, Version V1.1.
Original-PDF: `originals/KNX/MDT_THB_BE_02_Binaereingang_Tasterinterface.pdf`
