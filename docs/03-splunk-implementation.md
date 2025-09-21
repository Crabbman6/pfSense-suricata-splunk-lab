# Phase 3: Log Ingestion & SIEM Integration

This document details the process of configuring the pfSense firewall and the Suricata IDS to forward their logs to the Splunk SIEM. This creates a centralized location for analyzing both host-based and network-based security data.

---
## 1. Preparing Splunk (The Receiver)

Before configuring pfSense, the Splunk instance was prepared to receive, store, and correctly parse the new network log data.

### 1.1 - Index Creation
As a best practice for data segregation and management, two new indexes were created:
* `network`: For storing firewall traffic logs.
* `ids`: For storing Suricata Intrusion Detection System alerts.

<img width="800" height="785" alt="image" src="https://github.com/user-attachments/assets/9ffeaf04-82cf-4b27-9f32-86ff4923494b" />
<img width="798" height="784" alt="image" src="https://github.com/user-attachments/assets/dca15164-00b4-40ea-8ef7-e9a1c914168f" />

### 1.2 - Add-on Installation
To ensure Splunk can correctly parse and categorize the incoming data, three applications were installed:
* **Splunk Common Information Model (CIM):** Standardizes data fields for correlation.
* **TA-pfsense:** Provides field extractions specifically for pfSense firewall logs.
* **Splunk TA for Suricata:** Provides field extractions for Suricata IDS alerts.

<img width="1894" height="267" alt="image" src="https://github.com/user-attachments/assets/2aa8c552-fc98-4658-8305-cedb4a612949" />

### 1.3 - Data Input Configuration
A new UDP data input was configured on port `5147` to listen for incoming syslog data from the pfSense firewall.

<img width="1003" height="281" alt="image" src="https://github.com/user-attachments/assets/5a67239b-4112-46ce-97bc-f95b9cb627c2" />

---
## 2. Configuring pfSense & Suricata (The Senders)

With Splunk ready, the pfSense firewall and Suricata IDS were configured to forward their logs.

### 2.1 - pfSense Remote Logging
The pfSense system logger was configured to send **Firewall Events** to the Splunk server's IP address (`192.168.0.194`) on the designated UDP port `5147`.

<img width="1200" height="995" alt="image" src="https://github.com/user-attachments/assets/0728fba8-c686-4f75-a557-5cca9f300d4d" />

A search in Splunk for `index="network" sourcetype="pfsense"` confirmed that firewall logs were being successfully ingested.

<img width="1919" height="895" alt="image" src="https://github.com/user-attachments/assets/83582a54-a4a2-4fe4-ba4b-a03cda62a072" />

### 2.2 - Suricata IDS Configuration
To get the most detailed alert data, Suricata was configured to log in the **EVE JSON** format, which is ideal for SIEM integration. The configuration was applied to both the **WAN** and **LAN** interfaces for comprehensive threat visibility. The "Block Hosts" option was also enabled, turning the IDS into an active Intrusion Prevention System (IPS).

<img width="945" height="426" alt="image" src="https://github.com/user-attachments/assets/0283be7c-01a0-4d08-9a74-0b5d9dccf08f" />
<img width="1148" height="813" alt="image" src="https://github.com/user-attachments/assets/9b565fbd-36f6-4f7d-a361-a129c3c9de66" />
<img width="1146" height="824" alt="image" src="https://github.com/user-attachments/assets/7934cc89-af17-49f2-b5dd-0639817cbbfd" />
<img width="1147" height="674" alt="image" src="https://github.com/user-attachments/assets/1e602f43-06c5-407e-9404-0b59c8932fc3" />

After enabling the ET Open rule categories and starting the services, both interfaces were confirmed to be actively inspecting traffic.

<img width="1200" height="846" alt="image" src="https://github.com/user-attachments/assets/d59df5e8-2bdb-48b2-8b20-d78d3fb18781" />

