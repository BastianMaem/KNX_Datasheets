# Gruppenadressen – Projekt "Wohnung OG Links"

**Startdatum:** Mittwoch, 22. Oktober 2025
**Druckdatum:** Samstag, 25. Juli 2026
**Status:** In Bearbeitung

---

## Schema- und Aufbau-Analyse

Die Gruppenadressen folgen einer klassischen **3-stufigen ETS-Struktur** (Hauptgruppe / Mittelgruppe / Untergruppe) im Format `X/Y/Z`.

### 1. Hauptgruppen (Ebene 1) = Räume

Jede Hauptgruppe (0–8) entspricht einem Raum bzw. einer übergeordneten Funktion:

| HG | Raum |
|----|------|
| 0 | Global / Zentral (raumübergreifende Funktionen) |
| 1 | Kinderzimmer 1 |
| 2 | Kinderzimmer 2 |
| 3 | Schlafzimmer |
| 4 | Büro |
| 5 | Wohnessküche |
| 6 | Badezimmer |
| 7 | Gäste-WC |
| 8 | Flur |

### 2. Mittelgruppen (Ebene 2) = Funktionsbereiche

Für die Wohnräume (HG 1–8) wird durchgängig dasselbe Schema für die Mittelgruppen verwendet:

| MG | Funktionsbereich |
|----|-------------------|
| 0 | Beleuchtung |
| 1 | Steckdosen |
| 2 | Beschattung |
| 3 | Heizung / Klima |
| 4 | Präsenz / Sensorik |
| 5 | Szenen / Zentral |
| 6 | Status / Rückmeldung |

Die Hauptgruppe 0 (Global/Zentral) weicht davon ab und bildet stattdessen zentrale, raumübergreifende Themen ab: Zentralfunktionen, Szenen Zentral, Zeit/Datum, Wetter, Logik/Sperren sowie Status/Rückmeldungen.

### 3. Untergruppen (Ebene 3) = einzelne Datenpunkte

Die eigentlichen Gruppenadressen folgen einer einheitlichen **Namenskonvention**:

```
[RAUM-KÜRZEL]_[FUNKTIONS-KÜRZEL]_[GERÄT/DETAIL]_[AKTIONS-SUFFIX]
```

**Beispiel:** `KZ1_BEL_LI-Lampe_DIMABS`
→ Raum: Kinderzimmer 1 · Funktion: Beleuchtung · Gerät: Licht-Lampe · Aktion: Dimmen absolut

**Verwendete Raum-Kürzel:** GL (Global), KZ1/KZ2 (Kinderzimmer), SZ (Schlafzimmer), BÜ (Büro), WEK (Wohnessküche), BAD (Badezimmer), GWC (Gäste-WC), FL (Flur)

**Verwendete Funktions-Kürzel:** BEL (Beleuchtung), STK (Steckdosen), BES (Beschattung), HEA (Heizung/Klima), SEN (Sensorik), SZ (Szenen), STA (Status)

**Wiederkehrende Aktions-Suffixe** (über alle Räume konsistent verwendet):

| Suffix | Bedeutung |
|--------|-----------|
| `_SW` | Schalten |
| `_DIMREL` | Dimmen relativ (Schritt) |
| `_DIMABS` | Dimmen absolut (Prozent) |
| `_SP` | Sollwert/Stellwert (Temperatur oder Prozent) |
| `_MODE` | Betriebs-/HVAC-Modus |
| `_AUFAB` | Auf/Ab-Fahrbefehl (Beschattung) |
| `_STOP` | Stopp-Auslöser |
| `_BELTIME` | Lamellen-/Beschattungslaufzeit (Start/Stop) |
| `_ACTIVE` / `_STA` | Status-Rückmeldung |
| `_FANSPEED` | Lüfterstufe (Zählimpulse) |
| `_BIN` | Binärer Sensorwert (z. B. Reedkontakt) |

### 4. Status-/Rückmeldungsgruppen als Spiegel

Die jeweils letzte Mittelgruppe eines Raums (`X/6`, bei Global `0/5`) bündelt die Rückmeldeobjekte und spiegelt nahezu 1:1 die Stellgrößen der übrigen Mittelgruppen (Beleuchtung, Beschattung, Heizung/Klima etc.) als Status-Kommunikationsobjekte.

### 5. Trennzeichen-Konvention

Innerhalb der Untergruppen-Namen werden zwei Trennzeichen bewusst unterschiedlich eingesetzt:

- **Unterstrich `_`**: trennt die Hauptsegmente (Raum, Funktion, Gerät, Aktion), z. B. `KZ1_BEL_LI-Lampe_SW`
- **Bindestrich `-`**: verbindet ein Funktionskürzel mit seiner konkreten Orts-/Geräteangabe, z. B. `BES-Küche`, `REED-Dach`, `PRÄ-Eingang`
- **Schrägstrich `/`**: ausschließlich zur Verknüpfung zweier gemeinsam angesprochener Gerätearten reserviert, z. B. `LI/SD_ALL` (Licht **und** Steckdose gemeinsam)

Diese Konvention wurde in der aktuellen Fassung durchgängig bereinigt und konsequent angewendet (u. a. `AUF/AB` → `AUFAB`, `DAY/NIGHT` → `DAYNIGHT`, uneinheitliche Bindestrich-/Unterstrich-Stellen bei Steckdosen und Beschattung sowie `PRÄ-Slave` vereinheitlicht). Auch das zuvor abweichende Temperatur-Kürzel im Badezimmer wurde inzwischen auf das projektweit einheitliche `SEN_SEN_TMP` angeglichen.

---

## 0 – Global / Zentral

### 0/0 Zentralfunktionen
*(keine Untergruppen vorhanden)*

### 0/1 Szenen Zentral

| Adresse | Name | Typ |
|---------|------|-----|
| 0/1/0 | GL_SZ_LI/SD_ALL | Schalten |
| 0/1/1 | GL_SZ_LI_ALL | Schalten |

### 0/2 Zeit / Datum

| Adresse | Name | Typ |
|---------|------|-----|
| 0/2/0 | GL_TIDA_DATE | Datum |
| 0/2/1 | GL_TIDA_TIME | Tageszeit |
| 0/2/2 | GL_TIDA_DATETIME | Datum/Zeit |

### 0/3 Wetter

| Adresse | Name | Typ |
|---------|------|-----|
| 0/3/0 | GL_WE_TEMP | Temperatur (°C) |
| 0/3/1 | GL_WE_WIND | Geschwindigkeit (m/s) |
| 0/3/2 | GL_WE_REG | Schalten |
| 0/3/3 | GL_WE_LUX-max | Lux (Lux) |
| 0/3/4 | GL_WE_DAYNIGHT | Schalten |
| 0/3/5 | GL_WE_LUX-vorne | Lux (Lux) |
| 0/3/6 | GL_WE_LUX-li | Lux (Lux) |
| 0/3/7 | GL_WE_LUX-re | Lux (Lux) |

### 0/4 Logik / Sperren

| Adresse | Name | Typ |
|---------|------|-----|
| 0/4/0 | GL_LO_Orient | Boolesch |

### 0/5 Status / Rückmeldungen

| Adresse | Name | Typ |
|---------|------|-----|
| 0/5/0 | STA_LI-Wohnung_ACTIVE | Status |
| 0/5/1 | STA_LI-Wohnung_DARK | Boolesch |

---

## 1 – Kinderzimmer 1

### 1/0 Beleuchtung

| Adresse | Name | Typ |
|---------|------|-----|
| 1/0/0 | KZ1_BEL_LI-Lampe_SW | Schalten |
| 1/0/1 | KZ1_BEL_LI-Lampe_DIMREL | Dimmer Schritt |
| 1/0/2 | KZ1_BEL_LI-Lampe_DIMABS | Prozent (0..100%) |

### 1/1 Steckdosen

| Adresse | Name | Typ |
|---------|------|-----|
| 1/1/0 | KZ1_STK_SD-Bett_SW | Schalten |
| 1/1/1 | KZ1_STK_SD-Tv_SW | Schalten |

### 1/2 Beschattung

| Adresse | Name | Typ |
|---------|------|-----|
| 1/2/0 | KZ1_BES_BES-Gaube_AUFAB | Auf/Ab |
| 1/2/1 | KZ1_BES_BES-Gaube_STOP | Auslöser |
| 1/2/2 | KZ1_BES_BES-Gaube_SP | Prozent (0..100%) |
| 1/2/3 | KZ1_BES_BES-Gaube_BELTIME | Start/Stop |
| 1/2/4 | KZ1_BES_BES-Gesamt_SP | Prozent (0..100%) |

### 1/3 Heizung / Klima

| Adresse | Name | Typ |
|---------|------|-----|
| 1/3/0 | KZ1_HEA_FUS_SP | Temperatur (°C) |
| 1/3/1 | KZ1_HEA_FUS_MODE | HVAC Modus |
| 1/3/2 | KZ1_HEA_KLI_SW | Schalten |
| 1/3/3 | KZ1_HEA_KLI_MODE | HVAC Kontrollmodus |
| 1/3/4 | KZ1_HEA_KLI_SP | Temperatur (°C) |
| 1/3/5 | KZ1_HEA_KLI_FANSPEED | Zählimpulse (0..255) |
| 1/3/6 | KZ1_HEA_FUS_SW | Freigeben |

### 1/4 Präsenz / Sensorik

| Adresse | Name | Typ |
|---------|------|-----|
| 1/4/0 | KZ1_SEN_SEN_TMP | Temperatur (°C) |
| 1/4/1 | KZ1_SEN_SEN_HUM | Feuchtigkeit (%) |
| 1/4/2 | KZ1_SEN_REED-Gaube_BIN | Schalten |

### 1/5 Szenen / Zentral

| Adresse | Name | Typ |
|---------|------|-----|
| 1/5/0 | KZ1_SZ_LI/SD_ALL | Schalten |
| 1/5/1 | KZ1_SZ_SD_ALL | Schalten |

### 1/6 Status / Rückmeldung

| Adresse | Name | Typ |
|---------|------|-----|
| 1/6/0 | KZ1_STA_SD-Bett_ACTIVE | Status |
| 1/6/1 | KZ1_STA_SD-Tv_ACTIVE | Status |
| 1/6/2 | KZ1_STA_FUS_SP | Temperatur (°C) |
| 1/6/3 | KZ1_STA_FUS_ACTIVE | Status |
| 1/6/4 | KZ1_STA_FUS_MODE | HVAC Modus |
| 1/6/5 | KZ1_STA_BES-Gaube_SP | Prozent (0..100%) |
| 1/6/6 | KZ1_STA_LI-Lampe_ACTIVE | Schalten |
| 1/6/7 | KZ1_STA_LI-Lampe_DIMVAL | Prozent (0..100%) |
| 1/6/8 | KZ1_STA_KLI_ACTIVE | Schalten |
| 1/6/9 | KZ1_STA_KLI_Mode | HVAC Kontrollmodus |
| 1/6/10 | KZ1_STA_KLI_SP | Temperatur (°C) |
| 1/6/11 | KZ1_STA_KLI_FANSPEED | Zählimpulse (0..255) |

---

## 2 – Kinderzimmer 2

### 2/0 Beleuchtung

| Adresse | Name | Typ |
|---------|------|-----|
| 2/0/0 | KZ2_BEL_LI-Lampe_SW | Schalten |
| 2/0/1 | KZ2_BEL_LI-Lampe_DIMREL | Dimmer Schritt |
| 2/0/2 | KZ2_BEL_LI-Lampe_DIMABS | Prozent (0..100%) |

### 2/1 Steckdosen

| Adresse | Name | Typ |
|---------|------|-----|
| 2/1/0 | KZ2_STK_SD-Bett_SW | Schalten |
| 2/1/1 | KZ2_STK_SD-Tv_SW | Schalten |

### 2/2 Beschattung

| Adresse | Name | Typ |
|---------|------|-----|
| 2/2/0 | KZ2_BES_BES-Gaube_AUFAB | Auf/Ab |
| 2/2/1 | KZ2_BES_BES-Gaube_STOP | Auslöser |
| 2/2/2 | KZ2_BES_BES-Gaube_SP | Prozent (0..100%) |
| 2/2/3 | KZ2_BES_BES-Fenster_AUFAB | Auf/Ab |
| 2/2/4 | KZ2_BES_BES-Fenster_STOP | Auslöser |
| 2/2/5 | KZ2_BES_BES-Fenster_SP | Prozent (0..100%) |
| 2/2/6 | KZ2_BES_BES-Gaube_BELTIME | Start/Stop |
| 2/2/7 | KZ2_BES_BES-Fenster_BELTIME | Start/Stop |
| 2/2/8 | KZ2_BES_BES-Gesamt_SP | Prozent (0..100%) |

### 2/3 Heizung / Klima

| Adresse | Name | Typ |
|---------|------|-----|
| 2/3/0 | KZ2_HEA_FUS_SP | Temperatur (°C) |
| 2/3/1 | KZ2_HEA_FUS_MODE | HVAC Modus |
| 2/3/2 | KZ2_HEA_KLI_SW | Schalten |
| 2/3/3 | KZ2_HEA_KLI_MODE | HVAC Kontrollmodus |
| 2/3/4 | KZ2_HEA_KLI_SP | Temperatur (°C) |
| 2/3/5 | KZ2_HEA_KLI_FANSPEED | Zählimpulse (0..255) |
| 2/3/6 | KZ2_HEA_FUS_SW | Freigeben |

### 2/4 Präsenz / Sensorik

| Adresse | Name | Typ |
|---------|------|-----|
| 2/4/0 | KZ2_SEN_SEN_TMP | Temperatur (°C) |
| 2/4/1 | KZ2_SEN_SEN_HUM | Feuchtigkeit (%) |
| 2/4/2 | KZ2_SEN_REED-Fenster_BIN | Schalten |
| 2/4/3 | KZ2_SEN_REED-Gaube_BIN | Schalten |
| 2/4/4 | KZ2_SEN_REED-Gesamt_BIN | Schalten |

### 2/5 Szenen / Zentral

| Adresse | Name | Typ |
|---------|------|-----|
| 2/5/0 | KZ2_SZ_LI/SD_ALL | Schalten |
| 2/5/1 | KZ2_SZ_SD_ALL | Schalten |

### 2/6 Status / Rückmeldung

| Adresse | Name | Typ |
|---------|------|-----|
| 2/6/0 | KZ2_STA_SD-Bett_ACTIVE | Status |
| 2/6/1 | KZ2_STA_SD-Tv_ACTIVE | Status |
| 2/6/2 | KZ2_STA_FUS_SP | Temperatur (°C) |
| 2/6/3 | KZ2_STA_FUS_ACTIVE | Status |
| 2/6/4 | KZ2_STA_FUS_MODE | HVAC Modus |
| 2/6/5 | KZ2_STA_BES-Gaube_SP | Prozent (0..100%) |
| 2/6/6 | KZ2_STA_BES-Fenster_SP | Prozent (0..100%) |
| 2/6/7 | KZ2_STA_LI-Lampe_ACTIVE | Schalten |
| 2/6/8 | KZ2_STA_LI-Lampe_DIMVAL | Prozent (0..100%) |
| 2/6/9 | KZ2_STA_KLI_ACTIVE | Schalten |
| 2/6/10 | KZ2_STA_KLI_Mode | HVAC Kontrollmodus |
| 2/6/11 | KZ2_STA_KLI_SP | Temperatur (°C) |
| 2/6/12 | KZ2_STA_KLI_FANSPEED | Zählimpulse (0..255) |

---

## 3 – Schlafzimmer

### 3/0 Beleuchtung

| Adresse | Name | Typ |
|---------|------|-----|
| 3/0/0 | SZ_BEL_LI-Lampe_SW | Schalten |
| 3/0/1 | SZ_BEL_LI-Lampe_DIMREL | Dimmer Schritt |
| 3/0/2 | SZ_BEL_LI-Lampe_DIMABS | Prozent (0..100%) |

### 3/1 Steckdosen

| Adresse | Name | Typ |
|---------|------|-----|
| 3/1/0 | SZ_STK_SD-Bett-re_SW | Schalten |
| 3/1/1 | SZ_STK_SD-Bett-li_SW | Schalten |

### 3/2 Beschattung

| Adresse | Name | Typ |
|---------|------|-----|
| 3/2/0 | SZ_BES_BES-Fenster_AUFAB | Auf/Ab |
| 3/2/1 | SZ_BES_BES-Fenster_STOP | Auslöser |
| 3/2/2 | SZ_BES_BES-Fenster_SP | Prozent (0..100%) |
| 3/2/3 | SZ_BES_BES-Dach_AUFAB | Auf/Ab |
| 3/2/4 | SZ_BES_BES-Dach_STOP | Auslöser |
| 3/2/5 | SZ_BES_BES-Dach_SP | Prozent (0..100%) |
| 3/2/6 | SZ_BES_BES-Fenster_BELTIME | Start/Stop |
| 3/2/7 | SZ_BES_BES-Dach_BELTIME | Start/Stop |
| 3/2/8 | SZ_BES_BES-Gesamt_SP | Prozent (0..100%) |

### 3/3 Heizung / Klima

| Adresse | Name | Typ |
|---------|------|-----|
| 3/3/0 | SZ_HEA_FUS_SP | Temperatur (°C) |
| 3/3/1 | SZ_HEA_FUS_MODE | HVAC Modus |
| 3/3/2 | SZ_HEA_KLI_SW | Schalten |
| 3/3/3 | SZ_HEA_KLI_MODE | HVAC Kontrollmodus |
| 3/3/4 | SZ_HEA_KLI_SP | Temperatur (°C) |
| 3/3/5 | SZ_HEA_KLI_FANSPEED | Zählimpulse (0..255) |
| 3/3/6 | SZ_HEA_FUS_SW | Freigeben |

### 3/4 Präsenz / Sensorik

| Adresse | Name | Typ |
|---------|------|-----|
| 3/4/0 | SZ_SEN_SEN_TMP | Temperatur (°C) |
| 3/4/1 | SZ_SEN_SEN_HUM | Feuchtigkeit (%) |
| 3/4/2 | SZ_SEN_REED-Dach_BIN | Schalten |
| 3/4/3 | SZ_SEN_REED-Fenster_BIN | Schalten |
| 3/4/4 | SZ_SEN_REED-Gesamt_BIN | Schalten |

### 3/5 Szenen / Zentral

| Adresse | Name | Typ |
|---------|------|-----|
| 3/5/0 | SZ_SZ_LI/SD_ALL | Schalten |
| 3/5/1 | SZ_SZ_SD_ALL | Schalten |

### 3/6 Status / Rückmeldung

| Adresse | Name | Typ |
|---------|------|-----|
| 3/6/0 | SZ_STA_SD-Bett-re_ACTIVE | Status |
| 3/6/1 | SZ_STA_SD-Bett-li_ACTIVE | Status |
| 3/6/2 | SZ_STA_FUS_SP | Temperatur (°C) |
| 3/6/3 | SZ_STA_FUS_ACTIVE | Status |
| 3/6/4 | SZ_STA_FUS_MODE | HVAC Modus |
| 3/6/5 | SZ_STA_BES-Fenster_SP | Prozent (0..100%) |
| 3/6/6 | SZ_STA_BES-Dach_SP | Prozent (0..100%) |
| 3/6/7 | SZ_STA_LI-Lampe_ACTIVE | Schalten |
| 3/6/8 | SZ_STA_LI-Lampe_DIMVAL | Prozent (0..100%) |
| 3/6/9 | SZ_STA_KLI_ACTIVE | Schalten |
| 3/6/10 | SZ_STA_KLI_Mode | HVAC Kontrollmodus |
| 3/6/11 | SZ_STA_KLI_SP | Temperatur (°C) |
| 3/6/12 | SZ_STA_KLI_FANSPEED | Zählimpulse (0..255) |
| 3/6/13 | SZ_STA_BES-Gesamt_SP | Prozent (0..100%) |

---

## 4 – Büro

### 4/0 Beleuchtung

| Adresse | Name | Typ |
|---------|------|-----|
| 4/0/0 | BÜ_BEL_LI-Lampe_SW | Schalten |

### 4/1 Steckdosen

| Adresse | Name | Typ |
|---------|------|-----|
| 4/1/0 | BÜ_STK_SD-Pc_SW | Schalten |

### 4/2 Beschattung

| Adresse | Name | Typ |
|---------|------|-----|
| 4/2/0 | BÜ_BES_BES-Dach_AUFAB | Auf/Ab |
| 4/2/1 | BÜ_BES_BES-Dach_STOP | Auslöser |
| 4/2/2 | BÜ_BES_BES-Dach_SP | Prozent (0..100%) |
| 4/2/3 | BÜ_BES_BES-Dach_BELTIME | Start/Stop |
| 4/2/4 | BÜ_BES_BES-Gesamt_SP | Prozent (0..100%) |

### 4/3 Heizung / Klima

| Adresse | Name | Typ |
|---------|------|-----|
| 4/3/0 | BÜ_HEA_FUS_SP | Temperatur (°C) |
| 4/3/1 | BÜ_HEA_FUS_MODE | HVAC Modus |
| 4/3/2 | BÜ_HEA_KLI_SW | Schalten |
| 4/3/3 | BÜ_HEA_KLI_MODE | HVAC Kontrollmodus |
| 4/3/4 | BÜ_HEA_KLI_SP | Temperatur (°C) |
| 4/3/5 | BÜ_HEA_KLI_FANSPEED | Zählimpulse (0..255) |
| 4/3/6 | BÜ_HEA_FUS_SW | Freigeben |

### 4/4 Präsenz / Sensorik

| Adresse | Name | Typ |
|---------|------|-----|
| 4/4/0 | BÜ_SEN_SEN_TMP | Temperatur (°C) |
| 4/4/1 | BÜ_SEN_SEN_HUM | Feuchtigkeit (%) |
| 4/4/2 | BÜ_SEN_REED-Dach_BIN | Schalten |

### 4/5 Szenen / Zentral
*(keine Untergruppen vorhanden)*

### 4/6 Status / Rückmeldung

| Adresse | Name | Typ |
|---------|------|-----|
| 4/6/0 | BÜ_STA_SD-Pc_ACTIVE | Status |
| 4/6/1 | BÜ_STA_LI-Lampe_ACTIVE | Status |
| 4/6/2 | BÜ_STA_FUS_SP | Temperatur (°C) |
| 4/6/3 | BÜ_STA_FUS_ACTIVE | Status |
| 4/6/4 | BÜ_STA_FUS_MODE | HVAC Modus |
| 4/6/5 | BÜ_STA_BES-Dach_SP | Prozent (0..100%) |
| 4/6/6 | BÜ_STA_KLI_ACTIVE | Schalten |
| 4/6/7 | BÜ_STA_KLI_Mode | HVAC Kontrollmodus |
| 4/6/8 | BÜ_STA_KLI_SP | Temperatur (°C) |
| 4/6/9 | BÜ_STA_KLI_FANSPEED | Zählimpulse (0..255) |

---

## 5 – Wohnessküche

### 5/0 Beleuchtung

| Adresse | Name | Typ |
|---------|------|-----|
| 5/0/0 | WEK_BEL_LI-KücheSpots_SW | Schalten |
| 5/0/1 | WEK_BEL_LI-EssenLampe_SW | Schalten |
| 5/0/2 | WEK_BEL_LI-WohnzSpots_SW | Schalten |
| 5/0/3 | WEK_BEL_LI-WohnzSpots_DIMREL | Dimmer Schritt |
| 5/0/4 | WEK_BEL_LI-WohnzSpots_DIMABS | Prozent (0..100%) |
| 5/0/5 | WEK_BEL_LI-WohnzWand_SW | Schalten |
| 5/0/6 | WEK_BEL_LI-WohnzWand_DIMREL | Dimmer Schritt |
| 5/0/7 | WEK_BEL_LI-WohnzWand_DIMABS | Prozent (0..100%) |

### 5/1 Steckdosen

| Adresse | Name | Typ |
|---------|------|-----|
| 5/1/0 | WEK_STK_SD-Tv_SW | Schalten |
| 5/1/1 | WEK_STK_SD-Balkon_SW | Schalten |
| 5/1/2 | WEK_STK_SD-Vitrine_SW | Schalten |
| 5/1/3 | WEK_STK_SD-Sideboard_SW | Schalten |
| 5/1/4 | WEK_STK_SD-Küche_SW | Schalten |

### 5/2 Beschattung

| Adresse | Name | Typ |
|---------|------|-----|
| 5/2/0 | WEK_BES_BES-Küche_AUFAB | Auf/Ab |
| 5/2/1 | WEK_BES_BES-Küche_STOP | Auslöser |
| 5/2/2 | WEK_BES_BES-Küche_SP | Prozent (0..100%) |
| 5/2/3 | WEK_BES_BES-Balkon_AUFAB | Auf/Ab |
| 5/2/4 | WEK_BES_BES-Balkon_STOP | Auslöser |
| 5/2/5 | WEK_BES_BES-Balkon_SP | Prozent (0..100%) |
| 5/2/6 | WEK_BES_BES-Wohnz_AUFAB | Auf/Ab |
| 5/2/7 | WEK_BES_BES-Wohnz_STOP | Auslöser |
| 5/2/8 | WEK_BES_BES-Wohnz_SP | Prozent (0..100%) |
| 5/2/9 | WEK_BES_BES-Küche_BELTIME | Start/Stop |
| 5/2/10 | WEK_BES_BES-Balkon_BELTIME | Start/Stop |
| 5/2/11 | WEK_BES_BES-Wohnz_BELTIME | Start/Stop |
| 5/2/12 | WEK_BES_BES-Gesamt_SP | Prozent (0..100%) |

### 5/3 Heizung / Klima

| Adresse | Name | Typ |
|---------|------|-----|
| 5/3/0 | WEK_HEA_FUS_SP | Temperatur (°C) |
| 5/3/1 | WEK_HEA_FUS_MODE | HVAC Modus |
| 5/3/2 | WEK_HEA_KLI_SW | Schalten |
| 5/3/3 | WEK_HEA_KLI_MODE | HVAC Kontrollmodus |
| 5/3/4 | WEK_HEA_KLI_SP | Temperatur (°C) |
| 5/3/5 | WEK_HEA_KLI_FANSPEED | Zählimpulse (0..255) |
| 5/3/6 | WEK_HEA_FUS_SW | Freigeben |

### 5/4 Präsenz / Sensorik

| Adresse | Name | Typ |
|---------|------|-----|
| 5/4/0 | WEK_SEN_SEN_TMP | Temperatur (°C) |
| 5/4/1 | WEK_SEN_SEN_HUM | Feuchtigkeit (%) |
| 5/4/2 | WEK_SEN_REED-KücheRe_BIN | Schalten |
| 5/4/3 | WEK_SEN_REED-KücheLi_BIN | Schalten |
| 5/4/4 | WEK_SEN_REED-Balkon_BIN | Schalten |
| 5/4/5 | WEK_SEN_REED-Wohnz_BIN | Schalten |
| 5/4/6 | WEK_SEN_REED-Gesamt_BIN | Schalten |

### 5/5 Szenen / Zentral
*(keine Untergruppen vorhanden)*

### 5/6 Status / Rückmeldung

| Adresse | Name | Typ |
|---------|------|-----|
| 5/6/0 | WEK_STA_SD-Tv_ACTIVE | Status |
| 5/6/1 | WEK_STA_SD-Balkon_ACTIVE | Status |
| 5/6/2 | WEK_STA_SD-Vitrine_ACTIVE | Status |
| 5/6/3 | WEK_STA_SD-Sideboard_ACTIVE | Status |
| 5/6/4 | WEK_STA_SD-Küche_ACTIVE | Status |
| 5/6/5 | WEK_STA_LI-KücheSpots_ACTIVE | Status |
| 5/6/6 | WEK_STA_LI-EssenLampe_ACTIVE | Status |
| 5/6/7 | WEK_STA_FUS_SP | Temperatur (°C) |
| 5/6/8 | WEK_STA_FUS_ACTIVE | Status |
| 5/6/9 | WEK_STA_FUS_MODE | HVAC Modus |
| 5/6/10 | WEK_STA_BES-Küche_SP | Prozent (0..100%) |
| 5/6/11 | WEK_STA_BES-Balkon_SP | Prozent (0..100%) |
| 5/6/12 | WEK_STA_BES-Wohnz_SP | Prozent (0..100%) |
| 5/6/13 | WEK_STA_LI-WohnzSpots_ACTIVE | Schalten |
| 5/6/14 | WEK_STA_LI-WohnzSpots_DIMVAL | Prozent (0..100%) |
| 5/6/15 | WEK_STA_LI-WohnzWand_ACTIVE | Schalten |
| 5/6/16 | WEK_STA_LI-WohnzWand_DIMVAL | Prozent (0..100%) |
| 5/6/17 | WEK_STA_KLI_ACTIVE | Schalten |
| 5/6/18 | WEK_STA_KLI_Mode | HVAC Kontrollmodus |
| 5/6/19 | WEK_STA_KLI_SP | Temperatur (°C) |
| 5/6/20 | WEK_STA_FUS_SPDIFF | Temperaturdifferenz (K) |
| 5/6/21 | WEK_STA_KLI_FANSPEED | Zählimpulse (0..255) |

---

## 6 – Badezimmer

### 6/0 Beleuchtung

| Adresse | Name | Typ |
|---------|------|-----|
| 6/0/0 | BAD_BEL_LI-Spots_SW | Schalten |
| 6/0/1 | BAD_BEL_LI-Spots_DIMREL | Dimmer Schritt |
| 6/0/2 | BAD_BEL_LI-Spots_DIMABS | Prozent (0..100%) |
| 6/0/3 | BAD_BEL_LI-Spiegel_SW | Schalten |
| 6/0/4 | BAD_BEL_LI-Zentral_OFF | Schalten |

### 6/1 Steckdosen
*(keine Untergruppen vorhanden)*

### 6/2 Beschattung

| Adresse | Name | Typ |
|---------|------|-----|
| 6/2/0 | BAD_BES_BES-Dach_AUFAB | Auf/Ab |
| 6/2/1 | BAD_BES_BES-Dach_STOP | Auslöser |
| 6/2/2 | BAD_BES_BES-Dach_SP | Prozent (0..100%) |
| 6/2/3 | BAD_BES_BES-Dach_BELTIME | Start/Stop |
| 6/2/4 | BAD_BES_BES-Gesamt_SP | Prozent (0..100%) |

### 6/3 Heizung / Klima

| Adresse | Name | Typ |
|---------|------|-----|
| 6/3/0 | BAD_HEA_FUS_SP | Temperatur (°C) |
| 6/3/1 | BAD_HEA_FUS_MODE | HVAC Modus |

### 6/4 Präsenz / Sensorik

| Adresse | Name | Typ |
|---------|------|-----|
| 6/4/0 | BAD_SEN_SEN_TMP | Temperatur (°C) |
| 6/4/1 | BAD_SEN_SEN_HUM | Feuchtigkeit (%) |
| 6/4/2 | BAD_SEN_REED-Dach_BIN | Schalten |
| 6/4/3 | BAD_SEN_PRÄ_DUNKEL | Schalten |
| 6/4/4 | BAD_SEN_PRÄ_LUX | Lux (Lux) |

### 6/5 Szenen / Zentral

| Adresse | Name | Typ |
|---------|------|-----|
| 6/5/0 | BAD_SZE_LI-Spots_SZ1 | Szenensteuerung |

### 6/6 Status / Rückmeldung

| Adresse | Name | Typ |
|---------|------|-----|
| 6/6/0 | BAD_STA_FUS_SP | Temperatur (°C) |
| 6/6/1 | BAD_STA_FUS_ACTIVE | Status |
| 6/6/2 | BAD_STA_FUS_MODE | HVAC Modus |
| 6/6/3 | BAD_STA_BES-Dach_SP | Prozent (0..100%) |
| 6/6/4 | BAD_STA_LI-Spots_STA | Schalten |
| 6/6/5 | BAD_STA_LI-Spots_DIMVAL | Prozent (0..100%) |
| 6/6/6 | BAD_STA_TAS_STA | Schalten |
| 6/6/7 | BAD_STA_PRA-HLK_STA | Boolesch |
| 6/6/8 | BAD_STA_LI-Spiegel_STA | Status |

---

## 7 – Gäste-WC

### 7/0 Beleuchtung

| Adresse | Name | Typ |
|---------|------|-----|
| 7/0/0 | GWC_BEL_LI-Spots_SW | Schalten |

### 7/1 Steckdosen
*(keine Untergruppen vorhanden)*

### 7/2 Beschattung

| Adresse | Name | Typ |
|---------|------|-----|
| 7/2/0 | GWC_BES_BES-Dach_AUFAB | Auf/Ab |
| 7/2/1 | GWC_BES_BES-Dach_STOP | Auslöser |
| 7/2/2 | GWC_BES_BES-Dach_SP | Prozent (0..100%) |
| 7/2/3 | GWC_BES_BES-Dach_BELTIME | Start/Stop |
| 7/2/4 | GWC_BES_BES-Gesamt_SP | Prozent (0..100%) |

### 7/3 Heizung / Klima

| Adresse | Name | Typ |
|---------|------|-----|
| 7/3/0 | GWC_HEA_FUS_SP | Temperatur (°C) |
| 7/3/1 | GWC_HEA_FUS_MODE | HVAC Modus |

### 7/4 Präsenz / Sensorik

| Adresse | Name | Typ |
|---------|------|-----|
| 7/4/0 | GWC_SEN_REED-Dach_BIN | Schalten |
| 7/4/1 | GWC_SEN_PRÄ_LUX | Lux (Lux) |

### 7/5 Szenen / Zentral
*(keine Untergruppen vorhanden)*

### 7/6 Status / Rückmeldung

| Adresse | Name | Typ |
|---------|------|-----|
| 7/6/0 | GWC_STA_LI-Lampe_STA | Status |
| 7/6/1 | GWC_STA_BES-Dach_SP | Prozent (0..100%) |
| 7/6/2 | GWC_STA_FUS_SP | Temperatur (°C) |
| 7/6/3 | GWC_STA_FUS_ACTIVE | Status |
| 7/6/4 | GWC_STA_FUS_MODE | HVAC Modus |

---

## 8 – Flur

### 8/0 Beleuchtung

| Adresse | Name | Typ |
|---------|------|-----|
| 8/0/0 | FL_BEL_LI-Spots_SW | Schalten |
| 8/0/1 | FL_BEL_LI-Wand_SW | Schalten |

### 8/1 Steckdosen
*(keine Untergruppen vorhanden)*

### 8/2 Beschattung
*(keine Untergruppen vorhanden)*

### 8/3 Heizung / Klima
*(keine Untergruppen vorhanden)*

### 8/4 Präsenz / Sensorik

| Adresse | Name | Typ |
|---------|------|-----|
| 8/4/0 | FL_SEN_TAS_TMP | Temperatur (°C) |
| 8/4/1 | FL_SEN_TAS_HUM | Feuchtigkeit (%) |
| 8/4/2 | FL_SEN_PRÄ-Slave | Schalten |
| 8/4/3 | FL_SEN_PRÄ-Eingang_LUX | Lux (Lux) |
| 8/4/4 | FL_SEN_PRÄ-Kind_LUX | Lux (Lux) |

### 8/5 Szenen / Zentral

| Adresse | Name | Typ |
|---------|------|-----|
| 8/5/0 | FL_TeachIn | Schalten |

### 8/6 Status / Rückmeldung

| Adresse | Name | Typ |
|---------|------|-----|
| 8/6/0 | FL_STA_LI-Spots_ACTIVE | Status |
| 8/6/1 | FL_STA_LI-Wand_ACTIVE | Schalten |
