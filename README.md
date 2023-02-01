# SIEM-Walkthrough
SIEM Walkthrough | Microsoft Sentinel Map with Live Cyber Attacks
<h2>Description</h2>
In this lab I created a vulnerable VM as a honeypot for attacks and then created a log analytics workspace to ingest logs from my VM by using Microsoft Sentinel. I downloaded a PowerShell script and was able to input the IP addresses, that were found using the VM’s Event Viewer under “failed audits”, into the script. The script took those IP addresses and inserted them onto https://ipgeolocation.io/ . From there it created a file that was copied onto my main computer and inserted into a log analytics workspace. I was able to use these logs to make a query in Sentinel to create geographic locations that discover where attacks were coming from.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Azure Virtual Machine</b>
- <b>Microsoft Sentinel</b>

<h2>Environments Used </h2>

- <b>Windows 11</b> 

<h2>Program walk-through:</h2>

<p align="center">
•	Create an Azure free account, sign into my Azure Portal
•	Click on virtual machine tab, create virtual machine
: <br/>
<img src="https://imgur.com/DRL8p1C" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
o	Subscription- Pay as you go <br/>
o	Resource group- name Honeypotlab <br/>
o	Virtual machine name- name Honeypot-vm <br/>
o	Region- choose (US) EAST US <br/>
o	Leave rest of options on this page as default and created username and password for VM <br/>
o	Leave disks tab as default <br/>

<img src="https://imgur.com/pQ3wog5" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
