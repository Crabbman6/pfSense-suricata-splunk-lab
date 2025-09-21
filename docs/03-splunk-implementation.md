Phase 3 - Now I will be configuring pfSense to forward the logs into Splunk 

First im enabling SSH through the pfSense web GUI, this will be used in a later step in the configuration 

<img width="728" height="371" alt="image" src="https://github.com/user-attachments/assets/44767339-6ec7-4748-88fe-90c478e6a9a4" />

The next screenshot is verification that SSH is enabled using PowerShell on the Windows 11 VM 

<img width="960" height="1040" alt="image" src="https://github.com/user-attachments/assets/413e1980-ca10-4f36-b8c5-ccd36a8d1936" />

After this I create an index called 'network'. I leave all of the default settings as they are. 

<img width="800" height="785" alt="image" src="https://github.com/user-attachments/assets/9ffeaf04-82cf-4b27-9f32-86ff4923494b" />

I also create an index called 'ids'. 

<img width="798" height="784" alt="image" src="https://github.com/user-attachments/assets/dca15164-00b4-40ea-8ef7-e9a1c914168f" />

Next I install 3 packages for Splunk 

Splunk Common Information Model (CIM)
TA-pfsense
Splunk TA for Suricata

Here is an image of the installed applications on Splunk's manage applications view 

<img width="1894" height="267" alt="image" src="https://github.com/user-attachments/assets/2aa8c552-fc98-4658-8305-cedb4a612949" />

Next I'm going to configure the data inputs on Splunk to receive the logs from pfSense using UDP 

Image of the Review page on the UDP input using port 5147

<img width="1003" height="281" alt="image" src="https://github.com/user-attachments/assets/5a67239b-4112-46ce-97bc-f95b9cb627c2" />

Image showing on Splunk we have set up a receiving port on 9997 

<img width="1897" height="197" alt="image" src="https://github.com/user-attachments/assets/215b46b2-37a0-4be2-8cbb-418357afb07d" />

After this has been configured I need to configure pfSense to send the logs to the Splunk server 

On the following image I'm configuring remote logging, using 192.168.0.194 (Splunk server IP) with the port 5147. 

<img width="1200" height="995" alt="image" src="https://github.com/user-attachments/assets/0728fba8-c686-4f75-a557-5cca9f300d4d" />

After doing this I want to verify that the logs are successfully being ingested into splunk. I do this by searching 'index="network" sourcetype="pfsense"', this returns events as expected.

Image of me doing the search with successful logs including Suricata logs 

<img width="1919" height="895" alt="image" src="https://github.com/user-attachments/assets/83582a54-a4a2-4fe4-ba4b-a03cda62a072" />

At this point I have configured the pfSense logs to send to Splunk correctly under the network index. Now I'm going to configure the IDS Suricata part. 

Inside the pfSense Suricata configuration I have enabled the ETOpen Emerging Threats Rules 

<img width="947" height="332" alt="image" src="https://github.com/user-attachments/assets/c42689ef-cd47-4aa7-aa76-feea15fe4794" />

In the 'Updates' tab I've updated the rules to make sure they are up to date, the following screenshot shows this with the signature 

<img width="1200" height="995" alt="image" src="https://github.com/user-attachments/assets/eeb2d4a8-d09f-4586-8b4d-9b32b33a4629" />

Next in the 'Interfaces' tab I am configuring the WAN interface. 

(Screenshot of me configuring showing the WAN part in pfSense) 
<img width="945" height="426" alt="image" src="https://github.com/user-attachments/assets/0283be7c-01a0-4d08-9a74-0b5d9dccf08f" />

(Logging settings screenshot)
<img width="1148" height="813" alt="image" src="https://github.com/user-attachments/assets/9b565fbd-36f6-4f7d-a361-a129c3c9de66" />

(EVE Output settings, with me enabling the EVE JSON Log option) 
<img width="1146" height="824" alt="image" src="https://github.com/user-attachments/assets/7934cc89-af17-49f2-b5dd-0639817cbbfd" />

I enable the block hosts option, this tells pfSense to block any hosts that trigger a Suricata alert 

<img width="1147" height="674" alt="image" src="https://github.com/user-attachments/assets/1e602f43-06c5-407e-9404-0b59c8932fc3" />

Now I'm checking the Categories tab within the WAN settings to make sure the rules are enabled 

<img width="1161" height="799" alt="image" src="https://github.com/user-attachments/assets/e367a502-596f-4f67-9fa9-19f881febab0" />

I have now activated LAN and WAN Suricata within pfSense

<img width="1200" height="846" alt="image" src="https://github.com/user-attachments/assets/d59df5e8-2bdb-48b2-8b20-d78d3fb18781" />







