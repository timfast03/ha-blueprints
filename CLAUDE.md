# CLAUDE.md — ha-blueprints

Dieses Repository enthält Home Assistant Blueprints für präsenzbasierte Raumbeleuchtung und modulare Schalter-Steuerung.

## Projektstruktur

```
ha-blueprints/
├── room_lighting.yaml   # Blueprint: Automatische Raumbeleuchtung (v1.1)
├── room_switch.yaml     # Blueprint: 4-Tasten-Schalter (v1.0)
└── README.md            # Dokumentation mit Import-Links
```

## Blueprints

### room_lighting.yaml
Präsenzbasierte Raumbeleuchtung — **eine Automation pro Raum**.

**Pflicht-Inputs:**
- `presence_sensor` — Präsenzsensor (binary_sensor)
- `main_light` — Hauptlicht (light)
- `all_lights` — Alle Lichter im Raum (light, multiple)
- `auto_light_boolean` — Hauptschalter (input_boolean)
- `off_timer` — Timer Helper (timer)

**Optionale Feature-Blöcke** (jeweils per select-Input aktivierbar):
- `lux_settings` — LUX-Sensor zur Dunkelheitserkennung
- `daylight_settings` — Tageslicht-Abschaltung
- `night_settings` — Nachtmodus mit eigener Szene
- `guest_settings` — Besuch-Modus mit Dimm-Warnung
- `scene_memory_settings` — Szenen-Gedächtnis (input_text + input_boolean + input_datetime)
- `bypass_settings` — 3 Bypass-Modi (AN / Pause / AUS)

**Automatisierungs-Modus:** `restart`

### room_switch.yaml
Modularer 4-Tasten-Schalter, kompatibel mit room_lighting.

**Pro Taste konfigurierbar** (Aktion per select-Input):
- `toggle_light` — Licht aus→an, an→Szene hell
- `activate_scene` — Szene direkt aktivieren
- `room_off` — Bypass AUS + Lichter aus + Gedächtnis leeren
- `all_off` — Bypass + Besuch off + alle Lichter + Area aus
- `guest_on` — Besuch-Modus aktivieren + Szene
- `toggle_entity` — Beliebige Entity toggeln

**Automatisierungs-Modus:** `single`

## Konventionen

- Blueprints sind in YAML geschrieben und folgen dem Home Assistant Blueprint-Schema (`blueprint.domain: automation`)
- Feature-Sektionen werden mit `collapsed: true` und trennenden Kommentar-Blöcken (`# ══════`) strukturiert
- Optionale Features werden über `select`-Inputs mit `enable_*` / `disable_*` Werten gesteuert
- Jede Variable wird im `variables:`-Block aus `!input` berechnet und im Template mit Jinja2 ausgewertet
- Alle Inputs sind auf Deutsch beschriftet und haben Beschreibungstexte
- Helper-Naming-Convention: `timer.licht_aus_[raum]`, `input_boolean.auto_licht_[raum]`, etc.

## Änderungen vornehmen

1. Blueprint-Datei direkt bearbeiten (`room_lighting.yaml` oder `room_switch.yaml`)
2. Version in `blueprint.description` aktualisieren
3. Changelog in `README.md` ergänzen
4. `source_url` in `blueprint.source_url` zeigt auf den `main`-Branch — nach dem Merge passt der Link automatisch

## YAML-Validierung

Home Assistant validiert Blueprints beim Import. Vor einem Commit prüfen:
- Keine doppelten Keys in YAML
- `!input`-Referenzen zeigen auf existierende Input-Namen
- `default: []` für optionale Entities (erlaubt leere Selektion)
- Templates (`{{ }}`) müssen gültige Jinja2-Syntax haben
