# 🏠 Home Assistant Blueprints

Custom Blueprints für Home Assistant — präsenzbasierte Raumbeleuchtung und modulare Schalter-Steuerung.

---

## 💡 Room Lighting

Präsenzbasierte Raumbeleuchtung mit allen Features in **einer Automation pro Raum**.

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Ftimfast03%2Fha-blueprints%2Fblob%2Fmain%2Froom_lighting.yaml)

### Features (alle optional ein-/abschaltbar)

| Feature | Beschreibung |
|---|---|
| **Dunkelheitserkennung** | Sun Elevation + LUX-Sensor (Zwei-Stufen-Logik) |
| **Tageslicht-Abschaltung** | Licht aus wenn Sonne > 10° oder LUX stabil über Schwelle |
| **Nachtmodus** | Eigene Szene bei Gute-Nacht-Schalter |
| **Besuch-Modus** | Eigene Szene + längerer Timeout + Dimm-Warnung |
| **Szenen-Gedächtnis** | Merkt sich die letzte Szene, stellt sie bei Rückkehr wieder her |
| **3× Bypass** | Licht AN (bleibt an), Pause (eingefroren), Licht AUS (sofort aus) |
| **Modus-Wechsel bei Anwesenheit** | Sofortiger Szenen-Wechsel wenn Modi getoggelt werden |
| **Adaptive Lighting kompatibel** | Standard-Licht ohne Parameter → AL steuert frei |

### Benötigte Helper pro Raum

**Pflicht:**
- `timer.licht_aus_[raum]` — Timer (Ausschalt-Verzögerung)
- `input_boolean.auto_licht_[raum]` — Schalter (Hauptschalter)

**Je nach aktiviertem Feature:**
- `input_boolean.gute_nacht` — Schalter (global, 1× pro Wohnung)
- `input_boolean.besuch_modus` — Schalter (global, 1× pro Wohnung)
- `input_text.letzte_szene_[raum]` — Text (Szenen-Gedächtnis)
- `input_boolean.szene_aktiv_[raum]` — Schalter (Szenen-Flag)
- `input_datetime.szene_aus_[raum]` — Datum & Uhrzeit (Zeitstempel)
- `input_boolean.bypass_licht_an_[raum]` — Schalter (BP: AN)
- `input_boolean.bypass_licht_pause_[raum]` — Schalter (BP: Pause)
- `input_boolean.bypass_licht_aus_[raum]` — Schalter (BP: AUS)
- `input_button.szene_reset_[raum]` — Button (optional, Reset)

---

## 🔘 Room Switch (4 Tasten)

Modularer 4-Tasten-Schalter für Aqara und Zigbee. Jede Taste individuell konfigurierbar. Kompatibel mit Room Lighting.

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Ftimfast03%2Fha-blueprints%2Fblob%2Fmain%2Froom_switch.yaml)

### Aktionen pro Taste

| Aktion | Beschreibung |
|---|---|
| **Toggle Licht** | Deckenlampe aus → an, an → Szene hell |
| **Szene aktivieren** | Szene direkt aktivieren |
| **Raum AUS** | Bypass AUS + Lichter aus + Gedächtnis leeren |
| **Alles AUS** | Bypass + Besuch off + alle Lichter + Area aus |
| **Besuch-Szene** | Bypass off + Besuch on + Gedächtnis leeren + Szene |
| **Entity toggeln** | Beliebige Entity an/aus |

---

## Installation

### Variante 1: Import über Button (empfohlen)

Klicke oben auf den **"Import Blueprint"** Button → Home Assistant öffnet sich → Bestätigen → Fertig.

### Variante 2: Manuell

1. Datei herunterladen
2. In Home Assistant ablegen:
   ```
   /config/blueprints/automation/timfast03/room_lighting.yaml
   /config/blueprints/automation/timfast03/room_switch.yaml
   ```
3. **Entwicklerwerkzeuge → YAML → Automatisierungen neu laden**

### Blueprint aktualisieren

1. Neue Version von GitHub laden (oder Import-Button erneut klicken)
2. Lokale Datei ersetzen
3. **Entwicklerwerkzeuge → YAML → Automatisierungen neu laden**
4. Bestehende Automationen übernehmen die Änderungen automatisch

---

## Changelog

### Room Lighting v1.2
- Fix: LUX-Abfall überschreibt keine manuell aktivierten Szenen mehr (szene_aktiv Check)

### Room Lighting v1.1
- LUX-Abfall-Trigger mit 5-Sekunden-Stabilisierung (verhindert Fehlauslösung bei Lichtänderungen)
- Szenen-Gedächtnis Reset bei Bypass AUS
- Optionaler Reset-Button für Szenen-Gedächtnis

### Room Lighting v1.0
- Erstveröffentlichung

### Room Switch v1.0
- Erstveröffentlichung
