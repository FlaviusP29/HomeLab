# Windows Server 2022 VM Configuration

## Hardware Specifications
*   **RAM:** 8 GB
*   **vCPUs:** 6
*   **OS:** Windows Server 2022

## Initial Configuration & AD DS Setup
Post-installation, the server was configured as an **Active Directory Domain Controller** following these steps:

### 1. Network Configuration
*   Assigned a static IP address.
*   Set the hostname.
*   Configured the network interface for the LAN segment.
*   **Default Gateway / Internet Uplink:** `172.16.100.1` (NSv).

### 2. Role Installation
*   Installed **Active Directory Domain Services (AD DS)** via Server Manager (*Add Roles and Features*).

* ![AD DS Installation Screenshot](https://github.com/user-attachments/assets/0348a94f-679d-46e3-aff3-20d4b7ab5fe4)


### Navigation
*Previous: [Hardening SonicWall NSv Security](../Hardening_Firewall/README.md)*
