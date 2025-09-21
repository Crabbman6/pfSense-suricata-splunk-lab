# Network Security Monitoring Lab with pfSense, Suricata, and Splunk

![pfSense](https://img.shields.io/badge/pfSense-CE-blue?style-for-the-badge&logo=pfsense)
![Suricata](https://img.shields.io/badge/Suricata-IDS-orange?style-for-the-badge&logo=suricata)
![Splunk](https://img.shields.io/badge/Splunk-SIEM-000000?style-for-the-badge&logo=splunk)

---

## 🎯 Project Overview

This project expands on the previous SOC home lab by adding a dedicated network security monitoring (NSM) pipeline. The goal is to build a more realistic network topology using a **pfSense** firewall to segment and control traffic from the lab's endpoints.

The firewall is equipped with the **Suricata** Intrusion Detection System (IDS) to inspect all network traffic in real-time. Firewall and IDS logs are then forwarded to the **Splunk** SIEM for analysis, detection, and alerting, creating a comprehensive view of both host-based and network-based threats.

---

## 🛠️ Lab Architecture

The lab environment consists of two distinct network segments: the main LAN (the user's home network) and a private, internal lab network (`soc-net`). The pfSense firewall acts as the router and gateway between these two networks.

| Component | Technology / OS | Network | Purpose |
| :--- | :--- | :--- | :--- |
| **SIEM Host**| Linux Mint 21 | Home LAN | Runs Splunk Enterprise and VirtualBox. |
| **Firewall / IDS**| pfSense (VM) | WAN: Home LAN<br>LAN: `soc-net` | Routes traffic, enforces firewall rules, and inspects traffic with Suricata. |
| **Windows Endpoint**| Windows 11 (VM) | `soc-net` | The target Windows machine to be monitored. |



---

## 🚀 Project Library & Documentation

This project was completed in several phases, each with its own detailed write-up documenting the process, challenges, and outcomes.

* **[Phase 1: pfSense Firewall Deployment](./docs/01-pfSense-lab-configuration.md)**
    * This phase covers the creation of the pfSense VM, the critical two-adapter network configuration (WAN/LAN), and the initial setup via the web interface to establish a segmented, internal lab network.

* **[Phase 2: Suricata IDS Implementation](./docs/02-suricata-implementation.md)**
    * This document details the installation and configuration of the Suricata IDS package within pfSense. It includes enabling the ET Open ruleset, updating threat signatures, and troubleshooting hardware offloading conflicts to ensure proper operation.

* **[Phase 3: Log Ingestion & SIEM Integration](./docs/03-splunk-integration.md)**
    * This write-up covers the final step of the pipeline: forwarding network logs to Splunk. It details the preparation of the Splunk server (creating indexes, installing add-ons) and the configuration of both pfSense and Suricata to send syslog and EVE JSON data to the SIEM for centralized analysis.

---

## 💡 Skills Demonstrated

This project showcases the following critical cybersecurity skills:
* **Network Security Monitoring (NSM)**
* **Firewall Administration (pfSense)**
* **Intrusion Detection (IDS/IPS)** with Suricata
* **Virtual Networking** and network segmentation
* **SIEM Integration** and log source onboarding
* **Systematic Troubleshooting** of network hardware and software package conflicts
