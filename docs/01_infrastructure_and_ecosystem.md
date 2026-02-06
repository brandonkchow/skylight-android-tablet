This is the revised Architectural Specification using the Hyper-V (Virtual Machine) approach. This is the professional standard for running Home Assistant on Windows 11.
Architectural Specification: The "Skylight" Clone
Part 1: Infrastructure (The Virtual Hardware)
This section defines how we turn your Lenovo Tiny PC into a robust Home Automation server without erasing Windows.
 * Host Hardware: Lenovo Tiny PC (Windows 11 Pro).
 * Hypervisor: Microsoft Hyper-V (Native Windows Feature).
 * Guest OS: Home Assistant Operating System (HAOS).
   * Why: This gives you the full "Supervised" experience (Add-on Store, One-click Updates, Backups) that Docker lacks.
Hyper-V VM Configuration (The Spec):
 * Generation: Generation 2 (Required for modern HAOS).
 * Boot Security: Secure Boot Enabled -> Select "Microsoft UEFI Certificate Authority".
 * Memory: 4096 MB (4GB). Note: Uncheck "Enable Dynamic Memory" to prevent stability issues.
 * Processors: 2 Virtual Processors (Minimum).
 * Network: External Virtual Switch.
   * Critical: Do not use the "Default Switch." Create a new "External Switch" bridged to your Ethernet/WiFi adapter. This gives Home Assistant its own IP address on your LAN (e.g., 192.168.1.50), making it discoverable by the Tablet.
Part 2: Ecosystem & Data Layer
Now that we have the "Add-on Store" capability, we can simplify the software stack. We will still lean on Google for the data synchronization to keep it phone-friendly.
A. The "System" Apps (Installed via Home Assistant Add-on Store)
These run inside the VM with one-click installation.
 * Tailscale:
   * Role: Remote Access & Mesh Networking.
   * Config: Install the official Add-on, log in. It instantly connects your HA instance to your Tailnet. No port forwarding required.
 * Terminal & SSH:
   * Role: The tool needed to install HACS.
 * Studio Code Server (VS Code):
   * Role: Allows you to edit your YAML configuration files directly in the browser.
B. The "User" Apps (The Source of Truth)
 * Calendar: Google Calendar (Native Integration).
   * Sync: Two-way sync.
 * Chores & Groceries: Google Tasks (Native Integration).
   * Why: It appears natively inside the Google Calendar app on your phone.
   * Entities: todo.grocery_list, todo.house_chores.
 * Meal Planning: Google Tasks (Simple) or Mealie (Advanced).
   * Recommendation: Start with a Google Task list named "Menu".
   * Advanced Option: Since you now have the Add-on store, you can install the Mealie Add-on if you want a dedicated recipe manager later. For now, stick to Google Tasks for simplicity.
Checkpoint:
Does this Hyper-V and Add-on based architecture look correct to you? (This setup allows you to install Tailscale and VS Code with a single click).
If yes, I will proceed to Part 3, which is the detailed Frontend/Dashboard Specification (the part you will feed to the AI Agent).
