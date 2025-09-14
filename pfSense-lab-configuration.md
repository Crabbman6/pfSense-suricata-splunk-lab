# Phase 1: pfSense Firewall Deployment

This document details the initial deployment of the pfSense firewall, which will serve as the gateway and security boundary for the internal lab network. The primary goal is to create a segmented network where all endpoint traffic can be controlled and monitored.

---
## 1. Virtual Machine Network Configuration

The pfSense VM was configured in VirtualBox with two distinct network adapters to create a proper firewall topology: one for the external network (WAN) and one for the internal lab network (LAN).

### 1.1 - WAN Interface (Adapter 1)
The first adapter was configured in **`Bridged Adapter`** mode. This connects the firewall's WAN interface directly to the physical home network, allowing it to receive an IP address from the main router and access the internet.

<img width="1157" height="567" alt="image" src="https://github.com/user-attachments/assets/7202e53d-3de6-44c2-b676-da9f52d8f645" />

### 1.2 - LAN Interface (Adapter 2)
The second adapter was configured as an **`Internal Network`** named **`soc-net`**. This creates a private, isolated network segment that is completely separate from the home network. All lab endpoints (like the Windows and Kali VMs) will be connected to this network for monitoring.

<img width="742" height="497" alt="image" src="https://github.com/user-attachments/assets/45e7664b-7f48-4996-bc77-f132be1c2e08" />

---
## 2. Installation and Console Verification

After the network adapters were configured, pfSense was installed onto the VM. Upon rebooting, the console screen confirmed a successful installation. The console shows that the **WAN** interface (`em0`) correctly received an IP address from the home network, and the **LAN** interface (`em1`) was assigned the default gateway IP of `192.168.1.1` for the `soc-net` network.

<img width="720" height="472" alt="image" src="https://github.com/user-attachments/assets/f4ef95e6-feba-46ad-b6de-2c6e1e47ae4d" />

---
## 3. Web Interface Configuration

To perform the initial setup, a management machine needed to be connected to the new LAN. The Windows 11 VM's network adapter was reconfigured to the **`soc-net`** Internal Network, placing it behind the firewall.

<img width="742" height="497" alt="image" src="https://github.com/user-attachments/assets/f5f015b7-ddcf-401a-a0a3-e7340c8d3302" />

From a browser inside the Windows 11 VM, the pfSense web GUI was accessed at `http://192.168.1.1`.

<img width="1024" height="840" alt="image" src="https://github.com/user-attachments/assets/7c0b717b-f64f-4410-a63f-b2df3d45a0c1" />

The initial setup was completed using the configuration wizard, which included setting a new admin password and verifying the WAN/LAN interface configurations.

<img width="1024" height="840" alt="image" src="https://github.com/user-attachments/assets/cbc62ae5-3d02-4cd9-ab0f-0e4b73f13954" />

---
## 4. Final Verification

After the wizard completed, the main pfSense dashboard loaded, confirming that the firewall is fully configured, operational, and routing traffic for the internal `soc-net` lab network. The next phase is to install the Suricata IDS package to begin inspecting this traffic.

<img width="1024" height="840" alt="image" src="https://github.com/user-attachments/assets/d497d659-36f3-4392-b5c1-012e37671c92" />
