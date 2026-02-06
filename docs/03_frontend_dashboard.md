# Frontend & Dashboard Specification

This document defines the user interface (UI) design, layout, and configuration for the wall-mounted dashboard. The design goal is to replicate the "Skylight Calendar" aesthetic using a minimalist, high-contrast layout suitable for viewing from a distance.

## 1. Prerequisites (HACS)
The following frontend repositories must be installed via the Home Assistant Community Store (HACS) to support the design specifications.

| Repository | Purpose |
| :--- | :--- |
| `atomic-calendar-revive` | Rendering engine for the detailed "Agenda" view. |
| `lovelace-mushroom` | UI components for header chips and weather status. |
| `lovelace-layout-card` | Grid layout engine required for the 35/65 split. |
| `lovelace-card-mod` | CSS injection tool for removing borders and backgrounds. |
| `kiosk-mode` | Utility to hide the Home Assistant header and sidebar. |

## 2. Dashboard Design Specification
The dashboard is optimized for a Fire Tablet 10 (1920x1200 resolution).

### A. Layout Structure
*   **View Type:** `custom:grid-layout`
*   **Grid Definition:** Two-column split.
    *   **Left Column (35%):** "Daily Info Stack" (Weather, Menu, Groceries).
    *   **Right Column (65%):** "Master Agenda" (Calendar events).

### B. Component Specifications

#### Right Column: Master Agenda
*   **Card Type:** `custom:atomic-calendar-revive`
*   **Data Sources:** `calendar.family`, `calendar.birthdays`
*   **Mode:** Agenda View (List)
*   **Visual Configuration:**
    *   **Scope:** Next 7 days.
    *   **Typography:**
        *   Event Title: Large (18px)
        *   Time: Small/Subtle (14px)
    *   **Elements:** Hide "ProgressBar".
    *   **Date Format:** Full format (e.g., "Monday, February 5").

#### Left Column: Info Stack
1.  **Top Card (Weather):**
    *   **Type:** `custom:mushroom-chips-card`
    *   **Content:** Current Date, Time, `weather.home` status.
    *   **Alignment:** Center.

2.  **Middle Card (Dinner Menu):**
    *   **Type:** `todo-list`
    *   **Source:** `todo.weekly_menu`
    *   **Styling:** Use `card_mod` to hide the "Add Item" input bar (Read-only view).

3.  **Bottom Card (Groceries):**
    *   **Type:** `todo-list`
    *   **Source:** `todo.groceries`

### C. Theming (The "Matte" Look)
A custom theme file (`themes/skylight.yaml`) is required to enforce the minimalist aesthetic.

*   **Background:** `#ffffff` (Pure White)
*   **Card Background:** `transparent` (Simulates text floating on the wall)
*   **Text Color:** `#222222` (Dark Grey/Black)
*   **Shadows:** `none` (Flat design)

## 3. Tablet Configuration (Fully Kiosk Browser)
The physical display is managed by the Fully Kiosk Browser app on the Fire Tablet.

*   **Start URL:** `http://<HA_IP>:8123/lovelace-wallpanel/0?kiosk`
    *   *Note: The `?kiosk` query parameter forces Kiosk Mode immediately.*
*   **Interface:**
    *   Address Bar: Hidden
    *   Status Bar: Hidden (No Android battery/clock icons)
*   **Power Management:**
    *   Keep Screen On: Enabled
    *   Screensaver: Enabled (Google Photos via URL) after 5 minutes of inactivity.
*   **Motion Detection:**
    *   Visual Motion Detection: Enabled
    *   Action: Turn Screen On
