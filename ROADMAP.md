# Project Roadmap

## Epic 1: Infrastructure Setup
*Target: Lenovo Tiny PC & Hyper-V*

- [ ] Setup Lenovo Tiny PC with Windows 11 Pro
- [ ] Enable Hyper-V in Windows Features
- [ ] Configure BIOS/UEFI (Secure Boot -> Microsoft UEFI CA)
- [ ] Create "External Virtual Switch" in Hyper-V Manager
- [ ] Create & Configure HAOS Virtual Machine (Gen 2, 4GB RAM, 2 vCPU)
- [ ] Boot HAOS and verify IP address accessibility

## Epic 2: Ecosystem & Data Integration
*Target: Home Assistant Add-ons & Integrations*

- [ ] Install Tailscale Add-on (Remote Access)
- [ ] Install Terminal & SSH Add-on
- [ ] Install Studio Code Server (VS Code) Add-on
- [ ] Configure Google Calendar Integration (Two-way sync)
- [ ] Configure Google Tasks Integration (Grocery & Chores)
- [ ] Verify entities (`calendar.family`, `todo.grocery_list`) are populating

## Epic 3: Frontend & Dashboard
*Target: "Skylight" UI Replication*

- [ ] Install HACS (Home Assistant Community Store)
- [ ] Install Frontend Repositories via HACS:
    - [ ] `atomic-calendar-revive`
    - [ ] `lovelace-mushroom`
    - [ ] `lovelace-layout-card`
    - [ ] `lovelace-card-mod`
    - [ ] `kiosk-mode`
- [ ] Create Theme `themes/skylight.yaml` (Minimalist White, Transparent Cards)
- [ ] Implement Dashboard Layout (35% Info Stack / 65% Master Agenda)
- [ ] Configure "Master Agenda" with `atomic-calendar-revive`
- [ ] Configure "Info Stack" with Mushroom Chips & Todo Lists

## Epic 4: Operations & Maintenance
*Target: Reliability & Safety*

- [ ] Implement "Anti-Spicy Pillow" Automation (Battery 25% <-> 80%)
- [ ] Implement Morning Routine (06:30 AM: Wake, Brightness 100%, Reload)
- [ ] Implement Night Routine (10:30 PM: Screen Off/Screensaver)
- [ ] Install & Configure "Home Assistant Google Drive Backup" Add-on
- [ ] Test Backup & Restore procedure

## Epic 5: Hardware & Mounting
*Target: Fire Tablet & Physical Install*

- [ ] Debloat Fire Tablet (using Fire Toolbox)
- [ ] Install Fully Kiosk Browser
- [ ] Configure Fully Kiosk (Start URL, Kiosk Mode, Motion Detection)
- [ ] Acquire 180-degree U-Shape USB-C Adapter
- [ ] Select & Print/Buy Wall Mount (Front-loading design recommended)
- [ ] Final Installation & Cable Management
