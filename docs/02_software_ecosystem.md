# Software Ecosystem

This document outlines the software stack, applications, and integrations required to power the dashboard. The architecture leverages Home Assistant Add-ons for system services and Google integrations for user data synchronization.

## 1. System Applications
System applications are deployed via the Home Assistant Add-on Store, running as containers within the HAOS environment.

### A. Remote Access & Networking
*   **Component:** Tailscale
*   **Role:** Provides secure remote access and mesh networking without port forwarding.
*   **Configuration:**
    *   Install official Tailscale Add-on.
    *   Authenticate to the Tailnet.
    *   Enable "Subnet Router" (optional) if LAN access is required from remote locations.

### B. Development & Maintenance
*   **Terminal & SSH:** Provides CLI access to the HAOS environment for advanced debugging and HACS installation.
*   **Studio Code Server (VS Code):** Enables direct editing of YAML configuration files (`configuration.yaml`, `ui-lovelace.yaml`) via the browser.

## 2. User Applications (Data Layer)
The dashboard relies on external "Sources of Truth" for calendar and task data to ensure seamless synchronization with mobile devices.

### A. Calendar
*   **Service:** Google Calendar
*   **Integration:** Native Home Assistant Google Calendar Integration.
*   **Sync Direction:** Two-way.
*   **Requirements:** OAuth2 credential setup via Google Cloud Console.

### B. Chores & Groceries
*   **Service:** Google Tasks
*   **Integration:** Native Home Assistant Google Tasks Integration.
*   **Rationale:** Google Tasks integrates natively into the Google Calendar mobile app, providing a unified view for the user.
*   **Required Lists (Entities):**
    *   `todo.grocery_list`: Shared grocery shopping list.
    *   `todo.house_chores`: Recurring household maintenance tasks.

### C. Meal Planning
*   **Service:** Google Tasks (Initial Implementation)
*   **List Name:** "Menu"
*   **Future Expansion:** The architecture supports migrating to the **Mealie** Add-on if a dedicated recipe manager is required later.
