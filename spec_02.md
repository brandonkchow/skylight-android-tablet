Here is Part 3: Frontend & Dashboard Specification.
This is the final piece of the puzzle. It defines exactly how the "Face" of the application looks and functions. You will use this specification to generate the code using your AI agent.
3.1 Frontend Prerequisites (The "HACS" Stack)
Before you ask the AI to write code, you must manually install these 4 repositories from HACS (Frontend tab). The AI cannot do this step for you.
| Card Name | Repository in HACS | Purpose |
|---|---|---|
| Atomic Calendar Revive | atomic-calendar-revive | The engine for the "Agenda" view. Standard HA calendars cannot do the "Skylight" list style. |
| Mushroom | lovelace-mushroom | For the header and weather chips. Gives the "rounded UI" look. |
| Layout Card | lovelace-layout-card | Required to force the 35% / 65% split layout on the tablet. |
| Card Mod | lovelace-card-mod | Allows CSS injection to hide borders and backgrounds (Essential for the "Matte" look). |
| Kiosk Mode | kiosk-mode | Hides the top header and sidebar. |
3.2 The Master Agent Prompt
Copy and paste the block below into Cursor (or Gemini). It contains the complete architectural context so the AI generates the correct YAML the first time.
[BEGIN PROMPT]
I am building a wall-mounted dashboard in Home Assistant for a Fire Tablet 10 (1920x1200).
I have installed the following HACS plugins: atomic-calendar-revive, mushroom, layout-card, card-mod.
Goal: Replicate the "Skylight Calendar" UI exactly.
Architecture & Layout:
 * View Type: Use custom:layout-card with a grid-layout.
 * Grid Columns: Two columns.
   * Left Column (35%): "Daily Info Stack"
   * Right Column (65%): "Master Agenda"
 * Theme: Minimalist White. No shadows, no card borders.
Component Specifications:
A. The Right Column (Master Agenda):
 * Card: custom:atomic-calendar-revive
 * Entities: calendar.family, calendar.birthdays (Assume these exist).
 * Mode: Agenda View (List).
 * Design:
   * Show next 7 days.
   * Important: Make the font size for the Event Title large (18px) and the Time small (14px).
   * Hide the "ProgressBar".
   * Date Format: "dddd, MMMM D" (e.g., "Monday, February 5").
B. The Left Column (Info Stack):
 * Top Card (Weather): custom:mushroom-chips-card showing Date, Time, and weather.home status. Center aligned.
 * Middle Card (Dinner Menu):
   * Use a type: todo-list card pointing to todo.weekly_menu.
   * Styling: Use card_mod to hide the "Add Item" bar at the bottom. I only want to see the list.
 * Bottom Card (Groceries):
   * Use a type: todo-list card pointing to todo.groceries.
C. Global Styling (The "Matte" Look):
 * Please provide the YAML for a Theme file (themes/skylight.yaml) that sets:
   * Background: #ffffff
   * Card Background: transparent (so it looks like text floating on the wall)
   * Text Color: #222222
   * Shadows: none
Output:
 * Provide the themes/skylight.yaml code.
 * Provide the complete dashboard.yaml code.
[END PROMPT]
3.3 Tablet Configuration (Fully Kiosk)
Once the code is deployed, configure the Fully Kiosk Browser on the Fire Tablet to "lock" this view.
 * Web Content Settings:
   * Start URL: http://<YOUR_HA_IP>:8123/lovelace-wallpanel/0?kiosk
     * Note: Appending ?kiosk forces Kiosk Mode to activate immediately.
 * Toolbars and Appearance:
   * Show Address Bar: Off
   * Show Status Bar: Off (Hides the Android battery/clock icons for a clean look).
 * Power Settings:
   * Keep Screen On: Enabled.
   * Screensaver: Set to Google Photos (via Fotoo app or URL) after 5 minutes.
 * Motion Detection:
   * Enable Visual Motion Detection: On.
   * Turn Screen On on Motion: On.
Next Step
You now have the Infrastructure (Hyper-V), the Data Strategy (Google Sync), and the Frontend Spec (The Prompt).
Are you ready to execute this? I can help you troubleshoot the first time you paste that prompt into Cursor if the output isn't perfect.
