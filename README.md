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
•	Create an Azure free account, sign into my Azure Portal <br />
•	Click on virtual machine tab, create virtual machine
: <br/>
<img src="https://i.imgur.com/DRL8p1C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
o	Subscription- Pay as you go <br/>
o	Resource group- name Honeypotlab <br/>
o	Virtual machine name- name Honeypot-vm <br/>
o	Region- choose (US) EAST US <br/>
o	Leave rest of options on this page as default and created username and password for VM <br/>
o	Leave disks tab as default <br/>

<img src="https://i.imgur.com/pQ3wog5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
o	Click on Networking tab- Find NIC network security group- change to advanced <br />
o	Find configure network security group- Click “create new” <br />
o	Remove default inbound rule- add an inbound rule- Port ranges=*, priority=100, name= DANGER_UNSECURE <br />
o	Click Review+Create
 <br/>
<img src="https://i.imgur.com/z1cTm4P.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
•	Create Log Analytics workspace:  <br/>
<img src="https://i.imgur.com/FNQEtPd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
o	Subscription- Pay as you go <br />
o	Resource group- Choose the honeypotlab <br />
o	Name- LAWhoneypot <br />
o	Region- East US <br />
<img src="https://i.imgur.com/Frw9slq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
•	Go to Microsoft Defender for the Cloud <br />
o	Find management section- go to Environment Settings- click LAWhoneypot
:  <br/>
<img src="https://i.imgur.com/c1dASBA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
o	Go to “SQL servers on machines” and turn off <br />
o	Click save <br />
o	Click “Data collection”- Choose “All Events”- Save <br />
<br/>
<br/>
<img src="https://i.imgur.com/mBe955t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
•	Go back to Log Analytics workspace :  <br/>
 o	Find virtual machine section- Click “Connect” to connect workspace to VM <br/>
<img src="https://i.imgur.com/AUACOYB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br/>
•	Setup Microsoft Sentinel- Find and click create   <br/>
 o	Click Log Analytics workspace that was created- Add <br/>
<img src="https://i.imgur.com/10QRh8c.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
•	Find Virtual Machine- Go to Public IP Address and copy <br />
•	Open remote desktop on computer <br />
o	 paste the IP- Connect <br />
o	Go to more choices- Use a different account <br />
o	Use username and password that was used for the VM <br />
o	Log in <br/>
<br/>
<br/>
<img src="https://i.imgur.com/fauv14e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br/>
<br/>
<img src="https://i.imgur.com/ZwCCffm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/> 
<br/>
<br/>
•	Now Operate within Virtual Machine <br/> 
•	Setup browser <br/> 
•	Click start- Find “Event Viewer”- Open <br/> 
<br/>
<br/>
<img src="https://i.imgur.com/jIeWydP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
o	Go to windows logs- Click security <br />
o	Find any event with keywords “Audit Failure” (This shows failed attempts to log into VM)- Find Source Network Address <br />
 <br/>
 <br/>
•	Click start- open windows defender firewall  <br/>
o	Click Windows Defender Firewall Properties   <br/>
o	Go to domain/private/public profile- Firewall state: Off   <br/>
o	Apply   <br/>
o	Close out everything   <br/>
<img src="https://i.imgur.com/uYdRTeq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<br/>
<br/>
<br/> 
•	Go to Github- find joshmadakor1 <br/>
o	Download PowerShell script- Custom_Security_Log_Exporter.ps1 <br/>
<br/>
•	Open Windows Powershell ISE <br/>
o	Paste and save script as Log_Exporter <br/>
<br/>
<br/>
<br/>
•	Go to https://ipgeolocation.io/ <br/>
o	Signup- Copy API Key <br/>
o	Paste into Script <br/>
o	Run Script <br/>
<br/>
<img src="https://i.imgur.com/9rKy9co.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<br/>
<br/>
•	The script is now running and will pull the failed attempts IP addresses, insert into the ipgeolocation website, takes that information and creates a failed login file. <br/>
<img src="https://i.imgur.com/JpBgZri.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
<br/>
<br/>
<br/>
•	Find failed_rdp file <br/>
o	Copy contents of file <br/>
<br/>
<img src="https://i.imgur.com/fdR6ykr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<br/>
<br/>
•	Go back to main computer <br />
•	Open notepad- Paste contents of file, Save on desktop as failed_rdp <br />
<br/>
<br/>
<br/>
•	Go to azure portal- Log analytics, click on workspace  <br/>
<img src="https://i.imgur.com/Hap66vO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
<br/>
<br/> 
o	Go to custom log- add custom log <br/> 
o	select file in custom log <br/> 
o	Click next, under Collection paths choose Windows for type <br/> 
o	For path- copy the path from the VM- C:\ProgramData\failed_rdp.log * Needs to be accurate <br/>
<img src="https://i.imgur.com/zaLlfwd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<br/>
<br/> 
•	Click next, Details Custom log name= FAILED_RDP_WITH_GEO <br/>
o	Next, and create <br/>
<br/>
<img src="https://i.imgur.com/kwrY6Yy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
<br/>
<br/> 
•	Go to Logs <br/>
o	Type->  FAILED_RDP_WITH_GEO_CL <br/>
o	Run (Will now show all failed logs) <br/>
<br/>
<img src="https://i.imgur.com/98OCu6i.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<br/>
<br/> 
•	Click one of the logs- Extract fields <br/> 
o	Highlight latitude- Change field title to latitude and Field type as Numeric, Extract <br/> 
o	(If search results bring up other data than latitude then modify highlight) <br/> 
o	Repeat with longitude, destination host (text, not numeric), username, sourcehost, state, country, label, and timestamp <br/>  
<br/>
<img src="https://i.imgur.com/9d7DHzL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
•	Re-run script, Wait to repopulate with new fields
<br/> 
<br/>
<br/>
<br/> 
•	Open new tab, go to azure portal <br/> 
o	Type Sentinel- click on log_analytics_workspace_honeypot <br/> 
o	Click on “Workbooks”- Add new <br/> 
<br/>
<br/> 
<img src="https://i.imgur.com/TG18quu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/> 
<br/>
<br/>
o	Edit- remove default widgets <br/> 
o	Add Query- type in-> 	FAILED_RDP_WITH_GEO_CL | summarize event_count=count() by sourcehost_CF, latitude_CF, longitude_CF, country_CF, label_CF, destinationhost_CF | where destinationhost_CF != “samplehost”
| where sourcehost_CF != “” <br/> 
<br/>  
<br/>
•	Run Query <br/>
o	Fill in settings <br/>
<br/>
<img src="https://i.imgur.com/eZRLSZG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br/>
<br/>
<br/>
<br/> 
•	Save with title: Failed RDP World Map, US Central for location <br/> 
o	Click done editing, will now have map (will take some time for hackers to make attempts)! <br/> 
<br/>
<img src="https://i.imgur.com/Fkaoq2b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
