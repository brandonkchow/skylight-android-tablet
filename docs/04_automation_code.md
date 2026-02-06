Here is the final piece of your toolkit. You can paste this directly into your Cursor/Gemini Agent to generate the automation file, or paste it directly into your automations.yaml.
This code handles Part 4 (Operations & Safety).
The "Day 2" Operations Prompt
> Context:
> I need to protect the lithium battery of my wall-mounted Fire Tablet and manage its screen state.
> Requirements:
>  * Battery Protection: Toggle a smart plug (switch.tablet_charger) based on the tablet's battery level (sensor.fire_tablet_battery_level) to keep it between 25% and 80%.
>  * Morning Refresh: At 6:30 AM, wake the screen, set brightness to 100%, and reload the dashboard (to clear any browser memory leaks).
>  * Night Mode: At 10:30 PM, turn the screen off completely to save power.
> Output:
> Please write the Home Assistant Automation YAML for these logic flows. Use modern Home Assistant syntax (using action: instead of service:).
> 
The Manual Code (If you prefer to copy-paste)
If you want to verify the code yourself, here is the robust YAML implementation.
1. Battery Protection (Anti-Swell)
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

2. Morning/Night Lifecycle
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

Project Summary: Your Next Steps
You now have the complete blueprint. Here is your execution order:
 * The Host: Install Hyper-V and Home Assistant OS on your Lenovo Tiny.
 * The Bridge: Install HACS inside Home Assistant.
 * The Look: Use the Part 3 Prompt to generate the Dashboard YAML.
 * The Brain: Use the Part 4 Code (above) to set up the automations.
 * The Hardware: Debloat the Tablet (Fire Toolbox), install Fully Kiosk, and mount it.
Would you like me to combine all these prompts (Part 3 & 4) into a single "Master Instruction File" that you can save as a markdown document? This way you have the entire project documentation in one file.
