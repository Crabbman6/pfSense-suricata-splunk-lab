# Network Security Monitoring Lab with pfSense, Suricata, and Splunk

![pfSense](https://img.shields.io/badge/pfSense-CE-blue?style=for-the-badge&logo=pfsense)
![Suricata](https://img.shields.io/badge/Suricata-IDS-orange?style=for-the-badge&logo=suricata)
![Splunk](https://img.shields.io/badge/Splunk-SIEM-000000?style=for-the-badge&logo=splunk)
![Wireshark](https://img.shields.io/badge/Wireshark-Analysis-1679A7?style=for-the-badge&logo=wireshark)

---

## 🎯 Project Overview

This project expands on the previous SOC home lab by adding a dedicated network security monitoring (NSM) pipeline. The goal is to build a more realistic network topology using a **pfSense** firewall to segment and control traffic from the lab's endpoints.

The firewall is equipped with the **Suricata** Intrusion Detection System (IDS) to inspect all network traffic in real-time. Firewall and IDS logs are then forwarded to the **Splunk** SIEM for analysis, detection, and alerting, creating a comprehensive view of both host-based and network-based threats.

---

## 🛠️ Lab Architecture

The lab environment now consists of two distinct network segments: the main LAN (the user's home network) and a private, internal lab network (`soc-net`). The pfSense firewall acts as the router and gateway between these two networks.

| Component | Technology / OS | Network | Purpose |
| :--- | :--- | :--- | :--- |
| **SIEM Host**| Linux Mint 21 | Home LAN | Runs Splunk Enterprise and VirtualBox. |
| **Firewall / IDS**| pfSense (VM) | WAN: Home LAN<br>LAN: `soc-net` | Routes traffic, enforces firewall rules, and inspects traffic with Suricata. |
| **Windows Endpoint**| Windows 11 (VM) | `soc-net` | The target Windows machine to be monitored. |
| **Attacker Machine**| Kali Linux (VM) | `soc-net` | Simulates attacks against other VMs on the internal lab network. |



---

## 🚀 Project Phases

This project will be completed in the following phases:

* **1. pfSense Firewall Deployment:**
    * Create the pfSense VM with two network interfaces (WAN and LAN).
    * Install and configure pfSense to act as the router for a new `soc-net` internal network.
    * Re-configure the Windows and Kali VMs to connect to `soc-net` and use pfSense as their gateway.

* **2. Suricata IDS Implementation:**
    * Install the Suricata package directly within pfSense.
    * Download and enable IDS rule sets (like the Snort VRT or ET Open rules).
    * Configure Suricata to monitor the `soc-net` LAN interface for suspicious traffic.

* **3. Log Ingestion into Splunk:**
    * Configure pfSense to forward its firewall logs and Suricata's alert logs via syslog to the Splunk instance.
    * Set up a new data input in Splunk to listen for and index the incoming network logs.

* **4. Detection & Analysis:**
    * Write new SPL queries to analyze the network data.
    * Create new panels on the "SOC Overview" dashboard for firewall traffic and high-severity Suricata alerts.
    * Configure new alerts for critical network-based threats.

---

## 💡 Skills Demonstrated

This project will showcase the following critical cybersecurity skills:
* **Network Security Monitoring (NSM)**
* **Firewall Administration (pfSense)**
* **Intrusion Detection (IDS/IPS)**
* **Network Traffic Analysis**
* **Virtual Networking**
* **SIEM Integration**
