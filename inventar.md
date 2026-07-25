# KNX Datasheets – Inventar

Übersicht aller erfassten Komponenten, gruppiert nach den geplanten Ziel-Dateien im `docs/`-Ordner. Basis: ETS-Projektexport ("Wohnung OG Links", Topologie + Stückliste) – das ist die verlässlichste verfügbare Quelle, da sie die tatsächlich installierten Geräte inkl. Stückzahl zeigt.

**Stand:** 20 PDFs in `originals/` (17 in `originals/KNX/`, 3 in `originals/Klimaanlage/`) → **13 Zieldateien**

**Status-Legende:** ⬜ Konvertierung offen · 🔶 in Arbeit · ✅ fertig

⚠️ **Zu prüfen:** Im Ordner `originals/KNX/` liegen zwei ähnliche Schaltaktor-PDFs (`MDT_THB_AKI_03_04_AKS_03_Schaltaktor.pdf` ohne Versionsangabe und `MDT_THB_AKI_03_04_AKS_03_Schaltaktor_V16.pdf`). Vermutlich ist eine davon eine veraltete Version – bitte einmal gegenprüfen, welche aktuell ist, bevor die Konvertierung startet.

---

## Übersicht der Zieldateien

| Zieldatei | Komponenten | Anzahl verbaut | Konvertierung |
|---|---|---|---|
| `heizaktor.md` | AKH-0800.03 | 1 | ⬜ |
| `jalousieaktor.md` | JAL-0810M.02, JAL-0410M.02 | 2 | ⬜ |
| `schaltaktor.md` | AKS-2416.03, AKS-01UP.03 | 2 | ⬜ |
| `binaereingang.md` | BE-16024.02 | 1 | ⬜ |
| `praesenzmelder.md` | SCN-P360K4.03, SCN-P360L2.03, SCN-P360D1.01 | 5 | ⬜ |
| `taster.md` | BE-TAS63T4.01, BE-GTSP6TX.01S, BE-TAL6301.01, BE-TAL6302.01 | 20 | ⬜ |
| `busspannungsversorgung.md` | STC-0960.01 | 1 | ⬜ |
| `ip-interface.md` | SCN-IP000.03 | 1 | ⬜ |
| `dali-gateway.md` | SCN-DALI64.03 | 1 | ⬜ |
| `logikmodul.md` | SCN-LOG1.02 | 1 | ⬜ |
| `raumtemperatur-feuchtesensor.md` | SCN-TFS63.01 | 6 | ⬜ |
| `wetterstation.md` | Meteodata 140 S GPS | 1 | ⬜ |
| `klima-gateway.md` | Intesis ME-AC-KNX-1-V2 + 3 Mitsubishi-Klimageräte (Funktionsumfang) | 5 (Gateway) | ⬜ |

---

## Details je Zieldatei

### `heizaktor.md`
| Artikelnummer | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|
| AKH-0800.03 | 1 | MDT_THB_AKH_03_Heizungsaktor_V12.pdf |

### `jalousieaktor.md`
| Artikelnummer | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|
| JAL-0810M.02 | 1 | MDT_THB_JAL_02_Jalousieaktor_Fahrzeitmessung_V11.pdf |
| JAL-0410M.02 | 1 | MDT_THB_JAL_02_Jalousieaktor_Fahrzeitmessung_V11.pdf *(gleiche Quelle)* |

### `schaltaktor.md`
| Artikelnummer | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|
| AKS-2416.03 | 1 | MDT_THB_AKI_03_04_AKS_03_Schaltaktor_V16.pdf ⚠️ *(Duplikat prüfen, siehe oben)* |
| AKS-01UP.03 | 1 | MDT_THB_AKI_03_04_AKS_03_Schaltaktor_V16.pdf *(gleiche Quelle)* |

### `binaereingang.md`
| Artikelnummer | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|
| BE-16024.02 | 1 | MDT_THB_BE_02_Binaereingang_Tasterinterface.pdf |

### `praesenzmelder.md`
| Artikelnummer | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|
| SCN-P360K4.03 | 1 | MDT_TM_SCN-x360xx-03_V17_DE.pdf |
| SCN-P360L2.03 | 2 | MDT_TM_SCN-x360xx-03_V17_DE.pdf *(gleiche Quelle)* |
| SCN-P360D1.01 | 2 | MDT_THB_Praesenzmelder_1_fach_01.pdf |

### `taster.md`
*Drei Abschnitte für drei Produktfamilien in einer Datei.*

| Artikelnummer | Produktfamilie | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|---|
| BE-TAS63T4.01 | Smart 55/63 | 2 | MDT_THB_BE_01_Taster_Smart_55_63.pdf |
| BE-GTSP6TX.01S | Glastaster GTS | 6 | MDT_BE-GTSx6Tx-01S_MDT_TM_V13_DE.pdf |
| BE-TAL6301.01 | TAL-Serie (1-fach) | 11 | MDTBE-TAL55_63xx.x1_MDT_TM_V14_DE.pdf |
| BE-TAL6302.01 | TAL-Serie (2-fach) | 1 | MDTBE-TAL55_63xx.x1_MDT_TM_V14_DE.pdf *(gleiche Quelle)* |

### `busspannungsversorgung.md`
| Artikelnummer | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|
| STC-0960.01 | 1 | MDT_TM_STC-xxx0-01_V11_DE.pdf |

### `ip-interface.md`
| Artikelnummer | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|
| SCN-IP000.03 | 1 | MDT_THB_SCN_03_IP_Interface.pdf |

### `dali-gateway.md`
| Artikelnummer | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|
| SCN-DALI64.03 | 1 | MDT_THB_DaliControl_IP64_Gateway_03.pdf |

### `logikmodul.md`
| Artikelnummer | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|
| SCN-LOG1.02 | 1 | MDT_TM_SCN-LOG1-02_V10_DE.pdf |

### `raumtemperatur-feuchtesensor.md`
| Artikelnummer | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|
| SCN-TFS63.01 | 6 | MDT_THB_SCN_01_Objektregler_Raumtemperatur_FeuchteSensor_V10.pdf |

### `wetterstation.md`
| Artikelnummer | Hersteller | Anzahl | Quelle (Datei in `originals/KNX/`) |
|---|---|---|---|
| Meteodata 140 S GPS | Theben *(nicht MDT!)* | 1 | Theben_Meteodata_140_S_Handbuch.pdf |

### `klima-gateway.md`
*Enthält KNX-Kommunikationsobjekte/ETS-Parameter des Gateways UND den Funktionsumfang der angeschlossenen Klimageräte (kein separates File für die Klimageräte, siehe Entscheidung).*

| Komponente | Rolle | Anzahl | Quelle |
|---|---|---|---|
| Intesis ME-AC-KNX-1-V2 | KNX-Gateway (eigentliches KNX-Gerät) | 5 | originals/KNX/Intesis_INKNXMIT001I000.pdf |
| MSZ-LN18VG2W | Innengerät (Funktionsumfang) | – | originals/Klimaanlage/MSZ-LN18VG2W._Innengeraet.pdf |
| SLZ-M35FA2 | Innengerät (Funktionsumfang) | – | originals/Klimaanlage/SLZ-M35FA2_Innengeraet.pdf |
| MXZ-3F54VF4 | Außengerät (Funktionsumfang) | – | originals/Klimaanlage/MXZ-3F54VF4_Aussengeraet.pdf |

---

## Nächste Schritte
1. Schaltaktor-PDF-Duplikat klären (siehe ⚠️ oben)
2. Template final festlegen (inkl. Sonderfall `klima-gateway.md` mit zusätzlicher Sektion "Angeschlossene Klimageräte – Funktionsumfang")
3. Pilotgruppe auswählen und durcharbeiten (Vorschlag weiterhin: `jalousieaktor.md` oder `schaltaktor.md`)
4. Status-Spalte "Konvertierung" nach Fertigstellung jeweils aktualisieren
