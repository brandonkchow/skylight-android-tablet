# Automations & Maintenance

This document details the operational logic required to maintain the hardware health and software reliability of the wall panel. It includes the automation strategies for battery management ("Anti-Spicy Pillow" protocol) and screen lifecycle management.

## 1. Battery Safety Automation
**Goal:** Prevent battery swelling and extend device lifespan by keeping the lithium battery charge between 25% and 80%.

*   **Hardware:** Smart Plug (e.g., Kasa, Sonoff) controlling the tablet's charger.
*   **Sensor:** `sensor.fire_tablet_battery_level` (Exposed via Fully Kiosk integration).
*   **Logic:**
    *   **IF** battery < 25% **THEN** Turn Plug ON.
    *   **IF** battery > 80% **THEN** Turn Plug OFF.

### YAML Implementation
```yaml
alias: "Wall Panel - Battery Manager"
description: "Cycles the charger to keep battery healthy (25-80%)"
mode: single
trigger:
  - platform: numeric_state
    entity_id: sensor.fire_tablet_battery_level
    below: 25
    id: "battery_low"
  - platform: numeric_state
    entity_id: sensor.fire_tablet_battery_level
    above: 80
    id: "battery_high"
action:
  - choose:
      # If battery is low -> Turn Plug ON
      - conditions:
          - condition: trigger
            id: "battery_low"
        sequence:
          - action: switch.turn_on
            target:
              entity_id: switch.tablet_charger
      # If battery is high -> Turn Plug OFF
      - conditions:
          - condition: trigger
            id: "battery_high"
        sequence:
          - action: switch.turn_off
            target:
              entity_id: switch.tablet_charger
```

## 2. Screen Lifecycle Management
**Goal:** Automate screen brightness and ensure long-term stability by refreshing the browser daily.

*   **Morning Routine (06:30):** Wake screen, maximize brightness, and force a page reload to clear memory leaks.
*   **Night Routine (22:30):** Turn screen off to conserve power and reduce light pollution.

### YAML Implementation
```yaml
alias: "Wall Panel - Daily Cycle"
description: "Manages screen brightness and memory refresh"
trigger:
  - platform: time
    at: "06:30:00"
    id: "morning"
  - platform: time
    at: "22:30:00"
    id: "night"
action:
  - choose:
      - conditions:
          - condition: trigger
            id: "morning"
        sequence:
          # Wake the screen
          - action: fully_kiosk.screen_on
            target:
              entity_id: media_player.fire_tablet
          # Set Brightness to High
          - action: fully_kiosk.set_config
            target:
              entity_id: media_player.fire_tablet
            data:
              key: "screenBrightness"
              value: "255"
          # Reload the page to clear memory leaks (Crucial for 24/7 uptime)
          - action: fully_kiosk.load_start_url
            target:
              entity_id: media_player.fire_tablet

      - conditions:
          - condition: trigger
            id: "night"
        sequence:
          # Turn screen off immediately
          - action: fully_kiosk.screen_off
            target:
              entity_id: media_player.fire_tablet
```

## 3. Disaster Recovery (Backup Strategy)
To ensure system resilience, the following backup policy is enforced via the **Home Assistant Google Drive Backup** Add-on.

*   **Frequency:** Daily at 03:00 AM.
*   **Retention Policy:**
    *   Local: Keep last 3 backups.
    *   Cloud (Google Drive): Keep last 5 backups.
*   **Recovery RTO (Recovery Time Objective):** < 30 minutes (Reinstall HAOS -> Restore Snapshot).
