# System Architecture

This document defines the infrastructure and virtualization layer for the Skylight Home Assistant wall panel. The system is designed to run as a virtualized appliance on top of a Windows 11 host, ensuring robust performance and stability while maintaining the host's original utility.

## 1. Host Hardware
The physical host for the system is a small form-factor PC.

*   **Platform:** Lenovo Tiny PC
*   **Host OS:** Windows 11 Pro
*   **Role:** Hypervisor Host

## 2. Virtualization Layer
The system utilizes Microsoft Hyper-V (Type 1 Hypervisor) native to Windows 11 Pro.

### VM Configuration Specification
The Home Assistant Operating System (HAOS) Virtual Machine must be configured as follows:

| Setting | Value | Rationale |
| :--- | :--- | :--- |
| **Generation** | Generation 2 | Required for modern HAOS UEFI boot. |
| **Memory** | 4096 MB (4 GB) | **Static Assignment.** Dynamic Memory must be disabled to ensure stability. |
| **Processors** | 2 Virtual Processors | Minimum requirement for responsive dashboard rendering. |
| **Boot Security** | Secure Boot Enabled | Template: "Microsoft UEFI Certificate Authority". |

### Network Configuration
Connectivity is provided via a dedicated virtual switch to ensure the VM acts as a distinct device on the LAN.

*   **Switch Type:** External Virtual Switch
*   **Bridge Interface:** Ethernet or WiFi adapter of the host.
*   **Constraint:** Do *not* use the "Default Switch" (NAT). The VM must request its own IP address from the LAN router (e.g., `192.168.1.50`) to ensure discoverability by local devices like the Fire Tablet.

## 3. Guest Operating System
*   **OS:** Home Assistant Operating System (HAOS)
*   **Architecture:** Generic x86-64 (UEFI)
*   **Deployment Method:** Imported VHDX image.
*   **Capabilities:** Full "Supervised" experience, including:
    *   Add-on Store support
    *   One-click OS updates
    *   Full system backup/restore snapshots
