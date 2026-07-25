---
title: MDT IP-Interface SCN-IP000.03
device_type: IP-Schnittstelle
manufacturer: MDT
article_number: [SCN-IP000.03]
bus: KNX TP / IP
source_pdf: originals/KNX/MDT_THB_SCN_03_IP_Interface.pdf
last_updated: 2026-07-25
synonyms: [IP-Router, KNX-IP-Gateway, Email-Gateway, IP-Schnittstelle mit Secure]
tags: [knx, ip-interface, mdt]
---

## Übersicht

Das MDT IP-Interface SCN-IP000.03 koppelt den KNX-Bus (TP) mit einem Ethernet-Netzwerk (KNXnet/IP) und dient als Programmier- und Tunneling-Schnittstelle für die ETS sowie für andere KNXnet/IP-fähige Anwendungen. Zusätzlich enthält das Gerät auf der TP-Seite einen eigenständigen Email-Client, der bei bestimmten Bus-Ereignissen Emails versenden kann, sowie eine Zeitserver-Funktion (NTP-Client, der Datum/Uhrzeit als „Master" an weitere KNX-Geräte verteilt). Der Zugriff auf Konfiguration und Status erfolgt über ein integriertes Web-Interface.

Das Gerät besteht funktional aus zwei unabhängigen Applikationen, die getrennt in der ETS eingespielt und mit jeweils eigener physikalischer Adresse programmiert werden müssen:
- **IP-Interface-Applikation**: KNX/IP-Kopplung, Tunneling (Punkt-zu-Punkt-Verbindung), Busmonitor-Funktion.
- **TP-Applikation (Email/Zeitserver)**: Email-Versand, Zeitserver, Web-Interface-Zugriff.

Das Gerät bezieht seine Spannungsversorgung ausschließlich über den KNX-Bus, eine zusätzliche Netzteilversorgung ist nicht erforderlich.

KNX-Sicherheit wird über zwei getrennte Mechanismen abgebildet:
- **IP Secure** für die IP-Interface-Applikation (verschlüsselte/authentifizierte KNXnet/IP-Kommunikation, z. B. Tunneling).
- **Data Secure** für die Email-Applikation (sichere Inbetriebnahme und verschlüsselte Gruppenadressenkommunikation).

Beide Sicherheitsmechanismen sind optional aktivierbar; das Gerät kann auch vollständig „ohne Secure" (Plain Mode) betrieben werden. Für Data Secure/IP Secure wird mindestens ETS 5.7.2 vorausgesetzt; in ETS4 kann nur die Applikationsvariante „ohne Secure" verwendet werden.

## Technische Daten

| Merkmal | Wert |
|---|---|
| Spannungsversorgung | Ausschließlich über KNX-Bus, keine zusätzliche Spannungsversorgung notwendig |
| Physikalische Adressen | 2 (eine je Applikation: IP-Interface und Email/TP-Applikation) |
| Max. gleichzeitige Tunneling-Verbindungen | 4 |
| Max. Email-Empfängeradressen | 3 (gleichzeitiger Versand an bis zu 3 Adressen) |
| Max. Statuselemente (Email) | 30 |
| Max. Bit-Alarme (Email) | 10 |
| Max. Text-Alarme (Email) | nicht im Datenblatt spezifiziert (Anzahl nicht explizit als Maximalwert genannt) |
| Max. Statusberichte (Email) | 3 |
| Email-Puffer | 10 Emails (ab der 8. gepufferten Email wird ein Busalarm ausgesendet; bei vollem Puffer werden weitere Anfragen verworfen) |
| Max. sichere Gruppenadressen (Data Secure) | 255, mit maximal 64 unterschiedlichen Secure-Geräten |
| HTTP-Port Web-Interface | wählbar 80 oder 8080 (Default 8080) |
| LAN-Geschwindigkeit | bis zu 10 Mbit/s |
| FDSK (Factory Default Setup Key) | 2 Stück, je einer pro Applikation, aufgedruckt auf der rechten bzw. linken Geräteseite |
| Voraussetzung Data Secure/IP Secure | ETS 5.7.2 oder höher (ETS4 unterstützt nur Betrieb ohne Secure) |
| LEDs | LED1 Bus Status LAN, LED2 Bus Status KNX, LED3 Traffic LAN, LED4 Traffic KNX, LED5/LED6 ohne Funktion, LED8 Programmier-LED |
| Bedienelemente | Funktionsknopf (Master Reset), Programmierknopf |

### LED-Übersicht

| LED | Grün | Rot |
|---|---|---|
| LED 1 – Bus Status LAN | Aus: LAN Error / An: LAN OK | – |
| LED 2 – Bus Status KNX | Aus: KNX Bus Error oder nicht verbunden / An: KNX Bus OK | – |
| LED 3 – Traffic LAN | Blinkend: Buslast auf LAN-Seite / Aus: keine Buslast | Blinkend: Übertragungsfehler auf LAN-Seite |
| LED 4 – Traffic KNX | Blinkend: Buslast auf KNX-Seite / Aus: keine Buslast | Blinkend: Übertragungsfehler auf KNX-Seite |

Der Programmierknopf hat eine Doppelfunktion: Kurzes Drücken aktiviert den Programmiermodus der IP-Interface-Applikation (Programmier-LED leuchtet dauerhaft rot), langes Drücken aktiviert den Programmiermodus der Email-Applikation (Programmier-LED blinkt rot).

## Kommunikationsobjekte

Kommunikationsobjekte existieren ausschließlich in der Email/TP-Applikation. Die reine IP-Interface-Applikation (Tunneling/Routing) besitzt keine eigenen KNX-Gruppenobjekte, da sie als reine Schnittstelle arbeitet.

### Allgemeine Objekte

| Nr. | Name | Funktion | DPT/Größe | Flags |
|---|---|---|---|---|
| 1 | In Betrieb | Status senden | 1 Bit | K, L, Ü |
| 2 | Uhrzeit | Aktuelle Zeit senden | 3 Byte | K, L, Ü |
| 3 | Datum | Aktuelles Datum senden | 3 Byte | K, L, Ü |
| 4 | Datum / Uhrzeit | Aktuelles Datum und Zeit senden | 8 Byte | K, L, Ü |
| 51 | E-Mail Pufferspeicher | Überlauf | 1 Bit | K, L, Ü |
| 52 | E-Mail | Fehlercode | 1 Byte | K, L, Ü |
| 53 | NTP Zeitserver | Fehler | 1 Bit | K, L, Ü |
| 54 | Web Interface | Sperrstatus | 1 Bit | K, L, Ü |
| 55 | Web Interface | Sperren | 1 Bit | K, S |

Das Objekt „In Betrieb" kann zyklisch gesendet werden und ermöglicht eine externe Ausfallerkennung des Geräts (Watchdog-Funktion). Die Objekte 2–4 dienen der Zeitserver-Funktion: Das Gerät bezieht Datum/Uhrzeit per NTP und verteilt diese Werte wahlweise als 3-Byte-Uhrzeit, 3-Byte-Datum oder kombiniert als 8-Byte-Wert zyklisch auf den Bus, sodass andere KNX-Geräte (z. B. Schaltuhren) sich daran synchronisieren können.

Objekt 53 zeigt an, ob aktuell eine gültige NTP-Zeit vorliegt (stündliche Überwachung); fällt die Zeitsynchronisation aus, wird eine „1" gesendet, bei Wiederherstellung eine „0". Da Emails nur mit einer validen Systemzeit ausgesendet werden, hängt die korrekte Zeit-Zustellung von Objekt 2–4/53 indirekt mit der Zuverlässigkeit der Email-Funktion zusammen.

Objekt 51 signalisiert einen Überlauf des internen Email-Puffers (ab der 8. gepufferten Email wird bereits ein Alarm ausgegeben), Objekt 52 gibt bei wiederholt fehlgeschlagenem Email-Versand einen Fehlercode aus (siehe Abschnitt „Inbetriebnahme / Hinweise" für die Fehlercode-Bedeutung).

Die Objekte 54/55 steuern den Zugriffsschutz auf das Web-Interface: Objekt 55 erlaubt das Sperren/Freigeben unabhängig von den zeitgesteuerten Web-Interface-Parametern, Objekt 54 meldet den aktuellen Sperrstatus zurück.

### Email-Funktionen

| Nr. | Name | Funktion | DPT/Größe | Flags |
|---|---|---|---|---|
| 5 (+1 je weiterem) | Statusbericht 1…3 | E-Mail senden (auslösen) | 1 Bit | K, S |
| 8 (+1 je weiterem) | Text Alarm 1…n | E-Mail senden (Text-String) | 14 Byte | K, S |
| 11 (+1 je weiterem) | Bit Alarm 1…10 | E-Mail senden (Trigger) | 1 Bit | K, S |
| 21 (+1 je weiterem) | Statuselement 1…30 | Wert für Statuselement setzen | 1 Bit / 1 Byte / 2 Byte / 4 Byte / 14 Byte (je nach parametriertem Datenpunkttyp) | K, L, Ü |

**Statuselemente (Objekt 21 ff.):** Jedem der bis zu 30 Statuselemente ist ein Kommunikationsobjekt zugeordnet, dessen Größe vom parametrierten Datenpunkttyp abhängt. Der aktuell empfangene Wert wird intern gespeichert und kann sowohl in Bit-/Text-Alarm-Emails als auch in Statusberichten per Makro angezeigt werden.

**Bit-Alarme (Objekt 11 ff.):** Ein 1-Bit-Objekt löst bei Empfang eines konfigurierten Wertes (bzw. einer konfigurierten Flankenänderung) den Versand einer Email aus. Der Inhalt der Email wird über einen parametrierbaren Text inkl. Makros bestimmt.

**Text-Alarme (Objekt 8 ff.):** Ein 14-Byte-Zeichenobjekt löst bei jedem Schreibvorgang einen Email-Versand aus. Da 14 Byte für längere Nachrichten oft nicht ausreichen, sammelt das Gerät innerhalb eines parametrierbaren Zeitfensters mehrere nacheinander gesendete Strings und reiht sie zu einer gemeinsamen Email aneinander.

**Statusberichte (Objekt 5 ff.):** Ein 1-Bit-Objekt löst (wenn die Sendebedingung auf „Objekt" parametriert ist) das Aussenden eines Sammelberichts aus, der die Werte aller dafür freigegebenen Statuselemente im Format „Name: Wert" auflistet. Alternativ kann der Versand zeitgesteuert (fester Wochentag oder festes Datum im Monat) erfolgen, ohne dass das Objekt benötigt wird.

## ETS-Parameter

### IP-Interface-Applikation – mit Secure

**Allgemein**

| Parameter | Werte | Standard |
|---|---|---|
| Langsame Tunneling-Verbindungen unterstützen | Ja / Nein | Nein |
| Web-Interface mit aktivierter Sicherheit | Einstellungen aktiv / nur Statusanzeige / Einstellungen gesperrt | Einstellungen gesperrt |
| HTTP Port | 80 / 8080 | 8080 |
| DNS Server | freie IP-Eingabe | 0.0.0.0 |

„Langsame Tunneling-Verbindungen unterstützen" verlängert das UDP-Timeout für Tunnelverbindungen, was insbesondere bei Verbindungen über das Internet (hohe Latenz) notwendig sein kann; im Normalfall (LAN) bleibt der Wert auf „Nein". Die Einstellung „Web-Interface mit aktivierter Sicherheit" steuert, wie weit sicherheitskritische Funktionen (Firmware-Update, Tunneling-Adressvergabe) über das Web-Interface erreichbar sind – von voller Bedienbarkeit über reine Statusanzeige bis zur vollständigen Sperre.

**Gerät – Einstellungen**

| Parameter | Werte | Standard |
|---|---|---|
| Name | Freitext, max. 50 Zeichen | – |
| Sichere Inbetriebnahme | Aktiviert / Deaktiviert | Aktiviert (ETS-Standard beim Einfügen) |
| Secure Tunneling | Aktiviert / Deaktiviert | – |

Wird „Sichere Inbetriebnahme" deaktiviert, arbeitet das Gerät ungesichert (Plain Mode) und alle Secure-Funktionen sind wirkungslos. „Secure Tunneling" bestimmt zusätzlich, ob die eigentliche Tunneling-Kommunikation verschlüsselt (Secure) oder unverschlüsselt (Plain) übertragen wird – dies ist unabhängig von der sicheren Inbetriebnahme separat einstellbar.

**Gerät – IP Konfiguration**

| Parameter | Werte | Standard |
|---|---|---|
| IP-Adresse automatisch beziehen / Feste IP-Adresse verwenden | Auswahl | – |
| IP-Adresse | freie Eingabe | 255.255.255.255 (Platzhalter) |
| Subnetzmaske | freie Eingabe | 255.255.255.255 (Platzhalter) |
| Standardgateway | freie Eingabe | 255.255.255.255 (Platzhalter) |
| MAC-Adresse | vom Gerät vorgegeben, nicht änderbar | – |
| Multicast-Adresse | vom Backbone vorgegeben, änderbar im Reiter „Topologie Backbone" | 224.0.23.12 (Beispielwert) |
| Inbetriebnahmepasswort | freie Eingabe (optional, wird von ETS automatisch vergeben) | von ETS vergeben |
| Authentifizierungscode | freie Eingabe (optional, wird von ETS automatisch vergeben) | von ETS vergeben |

Bei „IP-Adresse automatisch beziehen" muss ein DHCP-Server im Netzwerk vorhanden sein. Subnetzmaske und Gateway werden nur bei fester IP-Adresse benötigt und bestimmen, ob Kommunikationspartner als „lokal" erkannt werden bzw. über welches Gateway entfernte Partner erreicht werden. Das Inbetriebnahmepasswort dient der Authentifizierung der ETS gegenüber dem Gerät während der gesamten Konfiguration/des Downloads; der Authentifizierungscode ersetzt nach der Erstinbetriebnahme den anfänglichen FDSK für die weitere gesicherte Kommunikation.

### IP-Interface-Applikation – ohne Secure

**Allgemein**

| Parameter | Werte | Standard |
|---|---|---|
| Gerätename (30 Zeichen) | Freitext | MDT KNX IP Interface |

**IP-Konfiguration**

| Parameter | Werte | Standard |
|---|---|---|
| HTTP Port | 80 / 8080 | 8080 |
| DHCP | benutzen / nicht benutzen | benutzen |
| IP-Adresse (nur bei DHCP „nicht benutzen") | (0-255).(0-255).(0-255).(0-255) | 0.0.0.0 |
| Netzmaske (nur bei DHCP „nicht benutzen") | (0-255).(0-255).(0-255).(0-255) | 255.255.255.0 |
| Gateway (nur bei DHCP „nicht benutzen") | (0-255).(0-255).(0-255).(0-255) | 0.0.0.0 |
| DNS (nur bei DHCP „nicht benutzen") | (0-255).(0-255).(0-255).(0-255) | 0.0.0.0 |

Steht bei aktivem DHCP kein Server zur Verfügung, vergibt sich das Gerät nach einer Wartezeit selbst eine Auto-IP-Adresse aus dem Bereich 169.254.1.0–169.254.254.255, bis wieder ein DHCP-Server erreichbar ist.

### Email/TP-Applikation – Allgemein

| Parameter | Werte | Standard |
|---|---|---|
| Geräteanlaufzeit | numerisch (Sekunden) | 10 |
| In Betrieb Telegramm | Zeitintervall (Auswahl) | 10 min |
| Sprache für Email Inhalt | Deutsch / Englisch | Deutsch |
| Gerätename | Freitext, max. 30 Zeichen | MDT IP Interface |

Die Geräteanlaufzeit verzögert den funktionalen Start nach Buspannungswiederkehr. Das zyklische „In Betrieb"-Telegramm ermöglicht eine externe Ausfallüberwachung. Die Sprachauswahl wirkt sich auf fest vorgegebene Infotexte innerhalb der versendeten Emails aus. Der Gerätename erscheint im Betreff der Email und kann per Makro `$D$` in eigene Textvorlagen eingebunden werden.

### Email/TP-Applikation – Web Interface

| Parameter | Werte | Standard |
|---|---|---|
| Passwort | Freitext (ISO 8859-1, ohne Leerzeichen und ohne `" &'`´€ŠšŽžŒœŸ`) | admin |
| Zeitüberschreitung für gültige Login | Zeitintervall | 30 min |
| Zeit bis Deaktivierung des Webinterfaces nach Reset | Zeitintervall | 30 min |
| Temporäre Aktivierung des Webinterfaces nach Email-Event | Zeitintervall | 30 min |
| Aktivierung/Deaktivierung des Webinterfaces über Objekt | aktiv / nicht aktiv | nicht aktiv |

Diese Parameter regeln, wie lange und unter welchen Bedingungen das Web-Interface aus Sicherheitsgründen erreichbar bleibt: nach Login, nach einem Geräteneustart oder temporär nach einem ausgelösten Email-Ereignis. Wird „Aktivierung/Deaktivierung über Objekt" aktiviert, erscheint zusätzlich Kommunikationsobjekt 55, über das der Zugriff busseitig freigegeben/gesperrt werden kann – dies ist die empfohlene Vorgehensweise, um das Web-Interface im Regelbetrieb deaktiviert zu halten und nur bei Bedarf freizuschalten.

### Email/TP-Applikation – Uhrzeit/Datum

| Parameter | Werte | Standard |
|---|---|---|
| Systemzeit zyklisch senden jede… | Zeitintervall (Auswahl) | 10 min |
| Sommer/Winterzeit Zeitumstellung | aktiv / nicht aktiv | aktiv |
| Zeitdifferenz zur Weltzeit (UTC+…) | Auswahl Zeitzone | UTC+01:00 Amsterdam, Berlin, Bern, Rom, Wien |

Diese Einstellungen konfigurieren die Zeitserver-Funktion (NTP-Client mit Master-Verteilung über die Objekte 2–4) inklusive automatischer Sommer-/Winterzeitumstellung und Zeitzonenbezug.

### Email/TP-Applikation – Statuselemente (je Element, 1…30)

| Parameter | Werte | Standard |
|---|---|---|
| Statuselement x | nicht aktiv / aktiv | nicht aktiv |
| Beschreibung des Statuselements | Freitext | – |
| Datenpunkttyp | siehe Tabelle unten | – |

Verfügbare Datenpunkttypen je Größe:

| Größe | Datenpunkttyp | Wert/Bereich |
|---|---|---|
| 1 Bit | Schalten | 1=Ein, 0=Aus |
| 1 Bit | Sperren | 1=gesperrt, 0=nicht gesperrt |
| 1 Bit | Oben/Unten | 1=Unten, 0=Oben |
| 1 Bit | Offen/Geschlossen | 1=Geschlossen, 0=Offen |
| 1 Bit | Heizen/Kühlen | 1=Heizen, 0=Kühlen |
| 1 Bit | Ja/Nein | 1=Ja, 0=Nein |
| 1 Bit | Anwesend/Abwesend | 1=Anwesend, 0=Abwesend |
| 1 Bit | Tag | 1=Tag, 0=Nacht |
| 1 Bit | Nacht | 1=Nacht, 0=Tag |
| 1 Byte | Wert | 0-255 |
| 1 Byte | Prozentwert | 0-100% |
| 1 Byte | HVAC Status | 0x01 Komfort, 0x02 Standby, 0x03 Nacht, 0x04 Frost-/Hitzeschutz |
| 1 Byte | HVAC Modus | Bitweise: Bit0=Komfort, Bit1=Standby, Bit2=Nacht, Bit3=Frost-/Hitzeschutz, Bit5(0=Kühlen/1=Heizen), Bit7=Frostalarm |
| 2 Byte | Wert vorzeichenlos | 0 – 65535 |
| 2 Byte | Wert vorzeichenbehaftet | -32768 – 32767 |
| 2 Byte | Gleitkommawert | -670760 – 670760 |
| 4 Byte | Wert vorzeichenlos | 0 – 4.294.967.295 |
| 4 Byte | Wert vorzeichenbehaftet | -2.147.483.648 – 2.147.483.647 |
| 4 Byte | Gleitkommawert | gemäß IEEE 754 |
| 14 Byte | Zeichen (ISO 8859-1) | beliebiger String, max. 14 Zeichen |

Jedes aktivierte Statuselement erhält einen frei wählbaren Anzeige-Namen; dieser Name sowie der aktuelle Wert können per Makro (`$Nxx$` / `$Vxx$`) in Bit-Alarm-Texten und Statusberichten eingebunden werden.

### Email/TP-Applikation – Bit-Alarme (je Alarm, 1…10)

| Parameter | Werte | Standard |
|---|---|---|
| Bit Alarm x | nicht aktiv / aktiv | nicht aktiv |
| Text für Email | Freitext, alternativ Makros | – |
| Sendeverhalten | senden bei Ein / senden bei Aus / senden bei Änderung auf Aus oder Ein / senden bei Änderung auf Ein / senden bei Änderung auf Aus | senden bei Ein |
| Email an Empfänger Adresse 1 senden | ja / nein | nein |
| Email an Empfänger Adresse 2 senden | ja / nein | nein |
| Email an Empfänger Adresse 3 senden | ja / nein | nein |

**Makros für Email-Texte** (gültig für Bit-Alarme, Text-Alarme und Statusberichte):
- `$D$` – wird durch den parametrierten Gerätenamen ersetzt.
- `$T$` – wird durch Datum/Uhrzeit des auslösenden Ereignisses ersetzt.
- `$Nxx$` – wird durch den Namen des Statuselements „xx" ersetzt (z. B. `$N1$` für Statuselement 1).
- `$Vxx$` – wird durch den aktuellen Wert des Statuselements „xx" ersetzt.
- Ein Semikolon `;` im Text erzeugt einen Zeilenumbruch bzw. trennt (beim ersten Semikolon) den Betreff vom eigentlichen Email-Text.

### Email/TP-Applikation – Text-Alarme

| Parameter | Werte | Standard |
|---|---|---|
| Wartezeit bis gesammelte 14-Byte-Telegramme gemeinsam ausgesendet werden | 1 – 120 s | 10 s |
| Email an Empfänger Adresse 1 senden | ja / nein | nein |
| Email an Empfänger Adresse 2 senden | ja / nein | nein |
| Email an Empfänger Adresse 3 senden | ja / nein | nein |

### Email/TP-Applikation – Statusberichte (je Bericht, 1…3)

| Parameter | Werte | Standard |
|---|---|---|
| Statusbericht x | nicht aktiv / aktiv | nicht aktiv |
| Sendebedingung | fester Tag in der Woche / festes Datum im Monat / Objekt „Statusbericht senden" | Objekt „Statusbericht senden" |
| Email an Empfänger Adresse 1/2/3 senden | ja / nein | nein |
| Statuselement 1-30 in Email | in Email nicht enthalten / in Email enthalten | in Email nicht enthalten |

Ein Statusbericht fasst alle dafür freigegebenen Statuselemente im Format „Name: Wert" in einer Email zusammen und kann zyklisch (Wochentag/Monatsdatum) oder busgesteuert per Objekt ausgelöst werden.

## Inbetriebnahme / Hinweise

**Zwei getrennte Applikationen mit zwei physikalischen Adressen:** Da IP-Interface- und Email-Applikation unabhängig voneinander programmiert werden, sind zwei physikalische Adressen zu vergeben und beide Applikationen einzeln per ETS-Download zu übertragen (kurzer Tastendruck → IP-Interface-Applikation, langer Tastendruck → Email-Applikation).

**Empfohlene Reihenfolge (ohne Data Secure):**
1. Applikation „IP Interface" einfügen, konfigurieren und per kurzem Tastendruck programmieren.
2. Applikation „IP Interface mit Email-Funktion" einfügen, konfigurieren und per langem Tastendruck programmieren.
3. Web-Interface über `http://IP-Adresse:Port` aufrufen und Email-Adressen konfigurieren.

**Empfohlene Reihenfolge (mit Data Secure):** analog, jedoch wird vor jedem Applikations-Download jeweils der zugehörige FDSK (Aufkleber links/rechts am Gerät) in der ETS hinterlegt. Jede Applikation besitzt einen eigenen FDSK.

**Wichtig bei IP-Adressänderung:** Wird die IP-Adresse des IP-Interface nachträglich geändert, übernimmt das Gerät die Änderung erst nach einem manuellen Neustart (Rechtsklick → „Gerät zurücksetzen" oder kurzes Ziehen des Busankers) – ein automatischer Neustart nach dem ETS-Download erfolgt nicht.

**Master Reset (Werksreset):** Erforderlich z. B. beim Wechsel von Secure auf „ohne Secure" oder bei falscher Reihenfolge der Applikationsprogrammierung. Ablauf: Funktionsknopf mindestens 15 Sekunden gedrückt halten (LEDs 1,2,5,6 leuchten rot/orange), loslassen, danach erneut mindestens 3 Sekunden drücken bis alle LEDs erlöschen. Das Gerät startet neu und erscheint anschließend wieder mit der Werksadresse 15.15.255. Ein Master Reset setzt auch die Secure-Konfiguration auf den ursprünglichen FDSK zurück, sodass ein erneuter Download nur mit dem FDSK möglich ist.

**Firmware-Update:** Wird über den integrierten Webbrowser-Zugang durchgeführt (Update-Datei im „hex"-Format). Nach einem Update ist das Gerät auf Werkseinstellungen zurückgesetzt – physikalische Adresse und Applikationen müssen neu geladen werden, ebenso müssen alle Web-Interface-Einstellungen (u. a. Email-Adressen) neu eingetragen werden.

**IP-Secure-Grundbegriffe:**
- **FDSK**: Werksseitiger Auslieferungsschlüssel, wird bei Erstinbetriebnahme durch einen von der ETS generierten, gerätespezifischen Schlüssel abgelöst; danach nicht mehr benötigt (außer nach Master Reset).
- **Secure Mode / Plain Mode**: Vollständig verschlüsselte bzw. vollständig unverschlüsselte Kommunikation.
- **Backbone-Key**: Von der ETS automatisch vergebener, nicht änderbarer Schlüssel für die Kommunikation zwischen zwei per Data Secure verbundenen IP-Routern.
- **Inbetriebnahmepasswort**: Authentifiziert die ETS gegenüber dem Gerät für Konfiguration/Download; sollte pro Gerät individuell vergeben werden.
- **Authentifizierungscode**: Ersetzt nach Erstinbetriebnahme den FDSK für die laufende Kommunikation zwischen ETS und Gerät.
- **Secure Tunneling**: Getrennt aktivierbare Verschlüsselung der Tunneling-Verbindung (unabhängig von der sicheren Inbetriebnahme selbst).

**Mischbetrieb:** Bei IP Secure können gesicherte Geräte ausschließlich mit anderen gesicherten Geräten kommunizieren – eine Mischung mit unverschlüsselten IP-Geräten ist nicht möglich. Bei Data Secure ist Mischbetrieb möglich: Data-Secure-fähige Geräte können auch mit nicht-Data-Secure-fähigen Geräten kommunizieren, dann jedoch nur ungesichert. Sollen alle Telegramme einer Gruppenadresse verschlüsselt übertragen werden, müssen alle daran beteiligten Geräte Data Secure unterstützen.

**Erweiterte Netzwerk-Sicherheitsempfehlungen:** keine Portfreigaben von Routern Richtung Internet, LAN/WLAN per Firewall absichern, Standardgateway bei fehlendem externem Zugriffsbedarf auf 0 setzen, externen Zugriff nur per VPN realisieren.

**Beispiel IP-Adressvergabe:** PC mit IP 192.168.1.30 / Subnetz 255.255.255.0 → das IP-Interface muss im selben Subnetz liegen, z. B. IP-Adresse 192.168.1.31 mit Subnetz 255.255.255.0 (jede freie Adresse im Bereich 1–254 außer der bereits verwendeten).

**Tunneling-Adressvergabe ohne Secure:** Die erste Tunneling-Adresse wird in den ETS-Verbindungseinstellungen festgelegt; die drei weiteren physikalischen Adressen können im Web-Interface (Menü Prog.-Mode, Button „Set") automatisch fortlaufend vergeben werden (z. B. ausgehend von 15.15.241 → .242, .243, .244). Wird als erste Adresse eine Adresse mit Hostteil 255 vergeben, erfolgt keine automatische Zuweisung der weiteren Adressen.

**Tunneling-Adressvergabe mit Secure:** Erfolgt direkt in der ETS5-Topologie, wo unterhalb des Geräts vier Tunneling-Kanäle mit eigenen physikalischen Adressen und Namen angelegt und über die Eigenschaften individuell angepasst werden können.

**Web-Interface-Einrichtung Email:** Im Menü „Email" → „Settings" werden Postausgangsserver (SMTP-Adresse, Port), sendende Email-Adresse, Benutzername/Passwort sowie bis zu drei Ziel-Email-Adressen hinterlegt. Beispielhafte, im Handbuch getestete SMTP-Serverdaten (Stand des Handbuchs, ohne Gewähr):

| Anbieter | SMTP-Server | Port |
|---|---|---|
| web.de | smtp.web.de | 587 |
| gmx.de | mail.gmx.net | 587 |
| 1&1 | smtp.1und1.de | 587 |
| Telekom | smtpmail.t-online.de | 465 |
| Hotmail/Outlook.com | smtpmail.live.com | 587 |
| Strato | smtp.strato.de | 587 |

Bei manchen Anbietern (z. B. web.de) muss der Versand über externe Programme im jeweiligen Email-Konto zusätzlich freigeschaltet werden.

**Email-Fehlercodes (Objekt 52 / Web-Interface-Status):**

| Code | Bedeutung | Mögliche Ursache/Behebung |
|---|---|---|
| 0 | No error | letzte Email erfolgreich versendet |
| 4 | unable to connect to server | falscher Port → Port prüfen |
| 6 | invalid sending Email address | Sende-Adresse ungültig/vom Server abgelehnt → Einstellungen prüfen |
| 8 | invalid receiving Email address | Ziel-Adresse ungültig → prüfen |
| 9 | Socket unexpectedly closed | Gerät neu starten, ggf. neu programmieren |
| 12 | Unknown/unsupported server authentication request | ungültiger Benutzername/Passwort → prüfen |

Bei fehlgeschlagenem Versand unternimmt das Gerät bis zu 4 Versuche mit gestaffelten Verzögerungen (10 s, 1 min, 10 min) und setzt danach das Fehlercode-Objekt; Fehlercode und Email-Puffer werden bei erfolgreicher Übertragung bzw. bei Wegfall der Fehlerbedingung automatisch zurückgesetzt. Zwischen zwei erfolgreichen Email-Versendungen liegt aus technischen Gründen stets eine Pause von 5 Sekunden. Ohne jemals empfangene NTP-Zeit werden Emails nach 5 Minuten mit dem Startdatum 01.01.1970 00:00 versendet.

**Push-Nachrichten / SMS:** Emails können über Drittdienste (z. B. „Prowl" für Apple-Geräte) als Push-Benachrichtigung empfangen werden. Für den Empfang als SMS bieten manche Provider (z. B. Telekom) einen entsprechenden Service an; alternativ können Drittanbieter wie sms77 genutzt werden.

## Quelle

MDT Technisches Handbuch – MDT IP Interface SCN-IP000.03, Stand 12/2020, Version 1.1.
Originaldatei: `originals/KNX/MDT_THB_SCN_03_IP_Interface.pdf`
