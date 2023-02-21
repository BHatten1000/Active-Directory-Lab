<h1>Active Directory Home Lab</h1>

 ### [Preview Screenshots]

<p align="center">
The script that was utilized: <br/>
<img src="https://i.imgur.com/l3ojy6T.png" height="80%" width="80%" alt="Screenshot_of_Script"/>
<br />
<br />

<h2>Description</h2>
This project consists of Creating a virtual environment that runs Active Directory (AD) and adding users to it with PowerShell
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Virtual Box</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b> Windows Server 2019 </b>

<h2>Program walk-through:</h2>

<p align="center">
Spin up a VM using virtualbox to act as our Domain Controller: <br/>
<img src="https://i.imgur.com/Kr5aMSy.png" height="80%" width="80%" alt="Virtual Box Screenshot"/>
 
 - Utilize an ISO for Server 2019 or whatever is used at your organization.
 - Be sure to setup two NICs. One running NAT and the other for the internal network.
 - Select either of the Desktop Experience options and proceed through the installation wizard & set up your Admin account
 
 <p align="center">
Windows Setup: <br/>
<img src="https://i.imgur.com/kO44dfo.png height="80%" width="80%" alt="Windows Setup Wizard"/>


 <p align="center">
<img src="https://i.imgur.com/8bpidBh.jpg height="80%" width="80%" alt="Windows Setup Wizard"/>                                                                                             
                                                                                                                                                         
<br />
<br />
Name and Configure Network Adapters:  <br/>
<img src="https://i.imgur.com/eaQchnK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
  - Name your NICs for ease of use.
  - Configure the one facing the "Internet" to use DHCP
  - Configure the internal NIC with its own static IP and subnet mask. This machine is our "default gateway" so in the DNS field enter the loopback address of 127.0.0.1 as seen below:
  
  <p align="center">
<img src="https://i.imgur.com/RX9wJVg.png" height="80%" width="80%" alt="Windows Setup Wizard"/>

<br />
<br />
Install Active Directory Domain Services (ADDS): <br/>
<img src="https://i.imgur.com/y66oisa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
   
   - Launch Server Manager and select 'Add roles and features'; Proceed through the menu, selecting the Domain Controller and selecting 'Active Directory Domain Services'
   <p align="center">
 <img src="https://i.imgur.com/pZ4Mkm3.png" height="80%" width="80%"
      
   - Once the role has been installed select the caution icon in Server Manager and promote the server to a domain controller.
   - In the following menu select 'Add a new forest' and proceed to name your domain. Proceed by hitting 'Next' and finally 'Install' Your DC will reboot.
    
   <p align="center">
 <img src="https://i.imgur.com/4Trxrvy.png" height="80%" width="80%"
      
   <p align="center">
 <img src="https://i.imgur.com/wXFlsuY.png" height="80%" width="80%"
 
<br />
<br />
Create your Domain Admin Account:  <br/>
<img src="https://i.imgur.com/SIZoCcK.png" height="80%" width="80%" alt="Create Domain Admin"/>
    
   - Launch AD Users and Computers and create an OU for Admins.
   - Within that OU create your Domain Admin account and make it a member of the "Domain Admins" default group.
   - Logout and then login wiith your Domain Admin credentials.
    
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
