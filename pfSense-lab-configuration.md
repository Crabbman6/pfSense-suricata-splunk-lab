# Phase 1: pfSense Firewall Deployment

This document details the initial deployment of the pfSense firewall, which will serve as the gateway and security boundary for the internal lab network. The primary goal is to create a segmented network where all endpoint traffic can be controlled and monitored.

---
## 1. Virtual Machine Network Configuration

The pfSense VM was configured in VirtualBox with two distinct network adapters to create a proper firewall topology: one for the external network (WAN) and one for the internal lab network (LAN).

### 1.1 - WAN Interface (Adapter 1)
The first adapter was configured in **`Bridged Adapter`** mode. This connects the firewall's WAN interface directly to the physical home network, allowing it to receive an IP address from the main router and access the internet.

<img width="1157" height="567" alt="image" src="https://github.com/user-attachments/assets/7202e53d-3de6-44c2-b676-da9f52d8f645" />

### 1.2 - LAN Interface (Adapter 2)
The second adapter was configured as an **`Internal Network`** named **`soc-net`**. This creates a private, isolated network segment that is completely separate from the home network. All lab endpoints (like the Windows and Kali VMs) will be connected to this network.

<img width="742" height="497" alt="image" src="https://github.com/user-attachments/assets/45e7664b-7f48-4996-bc77-f132be1c2e08" />

---
## 2. Installation and Verification

After the network adapters were configured, pfSense was installed onto the VM. Upon rebooting, the console screen confirmed a successful installation.

The console shows that the **WAN** interface (`em0`) correctly received an IP address (`192.168.0.197`) from the home network's DHCP server. The **LAN** interface (`em1`) was assigned the default IP address of `192.168.1.1`, which will now serve as the gateway for all devices inside the `soc-net` internal network.

<img width="720" height="472" alt="image" src="https://github.com/user-attachments/assets/f4ef95e6-feba-46ad-b6de-2c6e1e47ae4d" />

With this step complete, the pfSense firewall is now operational. The next step is to perform the initial configuration via the web interface.
