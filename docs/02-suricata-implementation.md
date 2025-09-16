# Phase 2: Suricata IDS Implementation

This document details the process of integrating the **Suricata Intrusion Detection System (IDS)** into the pfSense firewall. Once configured, Suricata will inspect all network traffic on the internal lab network (`soc-net`) for known malicious patterns, significantly enhancing the lab's network security monitoring capabilities.

---
## 1. Installing the Suricata Package

The Suricata IDS was installed as a package directly within the pfSense web interface via the Package Manager. This simplifies deployment and integration.

<img width="1238" height="973" alt="image" src="https://github.com/user-attachments/assets/73b3a83d-534e-4115-9798-5335193f08a2" />

A final check of the "Installed Packages" tab confirmed that Suricata was successfully deployed.

<img width="1238" height="973" alt="image" src="https://github.com/user-attachments/assets/df446dd6-b15b-4ca7-a38b-a501c0d9819c" />

---
## 2. Configuring Global Settings and Rule Updates

After installation, the global settings for Suricata were configured to enable the use of **ET Open Rules**. These are a widely-used, free set of threat intelligence signatures that allow Suricata to identify a broad range of malicious activities.

<img width="1238" height="973" alt="image" src="https://github.com/user-attachments/assets/b1f2c019-5f38-4289-8980-70062b25eb7a" />

The latest rule sets were then downloaded via the "Updates" tab, ensuring Suricata operates with current threat intelligence.

<img width="1238" height="973" alt="image" src="https://github.com/user-attachments/assets/c4d85fe5-ca6a-43ff-9550-361c6eda0232" />

---
## 3. Troubleshooting: Hardware Offloading Conflicts

During the configuration, an important warning message appeared: **"WARNING! Suricata now requires that Hardware Checksum Offloading, Hardware TCP Segmentation Offloading and Hardware Large Receive Offloading all be disabled for proper operation."**

<img width="810" height="271" alt="image" src="https://github.com/user-attachments/assets/f886a2fe-80a0-4b83-a98b-67e26db3d234" />

This error indicated a conflict between Suricata and pfSense's network card offloading features, which are designed to improve performance but can interfere with IDS packet inspection. The solution was to navigate to **System > Advanced > Networking** and disable these specific hardware offloading options. A subsequent reboot of the pfSense VM was performed to apply these changes.

<img width="728" height="662" alt="image" src="https://github.com/user-attachments/assets/53ac84eb-2623-46f9-812e-f23fec8755e8" />

---
## 4. Enabling Suricata on the LAN Interface

With the hardware offloading issue resolved, Suricata was then explicitly enabled on the **LAN interface** of the pfSense firewall. This ensures that all traffic flowing into and out of the `soc-net` internal lab network is actively inspected by the IDS.

After saving the interface settings and starting the Suricata service, the "Interfaces" page confirmed that Suricata was running live on the LAN interface (indicated by the green checkmark).

<img width="960" height="704" alt="image" src="https://github.com/user-attachments/assets/e22a3734-32ac-4906-bf8b-811125737991" />

With Suricata now actively monitoring the internal network, the next critical step is to configure pfSense to forward these valuable IDS alerts and firewall logs to the Splunk SIEM for centralized analysis.
