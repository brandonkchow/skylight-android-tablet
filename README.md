# Skylight Clone - Home Assistant Wall Panel

This project aims to replicate the functionality and aesthetic of the "Skylight Calendar" using robust, self-hosted hardware and software. It leverages a Lenovo Tiny PC running Home Assistant OS via Hyper-V and a Fire Tablet acting as the wall-mounted display.

## Project Overview

The goal is to build a reliable, WAF-approved (Wife/Partner Acceptance Factor) family dashboard that handles:
-   **Shared Calendars**: Syncing with Google Calendar.
-   **Chores & Groceries**: Managing household tasks via Google Tasks.
-   **Smart Home Control**: Basic weather and home status monitoring.
-   **Maintenance-Free Operation**: Automated battery management and screen scheduling.

## Documentation

The project specification is broken down into the following documents:

-   **[01. Infrastructure & Ecosystem](docs/01_infrastructure_and_ecosystem.md)**
    -   *Part 1: Infrastructure (The Virtual Hardware)* - Setting up Hyper-V on Windows 11.
    -   *Part 2: Ecosystem & Data Layer* - Configuring Tailscale, VS Code, and Google Sync.
-   **[02. Frontend & Dashboard](docs/02_frontend_spec.md)**
    -   *Part 3: Frontend Specification* - Setting up HACS, Layout Card, Mushroom, and Atomic Calendar Revive to achieve the "Skylight" look.
-   **[03. Operations & Maintenance](docs/03_operations_and_maintenance.md)**
    -   *Part 4: Operations & Physical Logic* - Battery safety automations, morning/night routines, and backup strategies.
-   **[04. Automation Code Snippets](docs/04_automation_code.md)**
    -   Ready-to-use YAML code for battery management and screen lifecycle automations.

## Roadmap

For a detailed breakdown of tasks and progress, see the **[Project Roadmap](ROADMAP.md)**.
