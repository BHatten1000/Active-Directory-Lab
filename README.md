<h1>Active Directory Home Lab</h1>

 ### [Preview Screenshots]

<p align="center">
The script that was utilized to create users: <br/>
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

   <p align="center">
Configure Remote Access Server and Network Address Translation: <br/>
<img src="https://i.imgur.com/9IT5RHh.png" width="80%" alt="Windows Setup Wizard"/>  

  - In Server Manager select 'Tools', 'Routing and Remote Access', and then right click on your DC and 'Configure and Enable'
  - Continue by hitting 'Next' and select 'Network Address Translation' this will enable our client or user machines to connect to the internet through the DC's IP.
  - When prompted select your internet facing network adapter and select 'Finish'    
    
   <p align="center">
 Completed RAS & NAT Configuration: <br/>   
 <img src="https://i.imgur.com/9R91Xvp.png" height="80%" width="80%"


<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%"/>
<br />
<br />
Setup DHCP on Domain Controller(to give client machines IP addresses):  <br/>
<img src="https://i.imgur.com/6R4b85W.png" height="80%" width="80%"/>
    
   - Return to Server Manager and select 'Add Roles and Features'. 
   - Select your DC, proceed with 'Next' and select 'DHCP' and 'Add Role'.
   - After a short wait your DHCP role will finish installing but still needs a scope. 
   - Return to the 'Tools' menu and select 'DHCP' 
   - In the DHCP configuration menu right click on 'IPv4' and select 'New Scope' then name and define your scope. These IP addresses represent the available addresses for any host machines that you add to your test enviornment in the future.
   - Define exlusions (if you have any) and lease duration
    
 <img src="https://i.imgur.com/eLK8ZMi.png" height="80%" width="80%"/>
    
 <img src="https://i.imgur.com/tTSG2oD.png" height="80%" width="80%"/>
    
   - When prompted select 'Yes, I want to configure these options now' and proceed to specify the default gateway (in our case this is the DC's IP address), DNS servers, and Domain name as shown below:
    
 <img src="https://i.imgur.com/4CmGcpr.png" height="80%" width="80%"/>
<br />
<br />
    
   <p align="center">
Finally, Powershell to create 1000 users: <br/>
     
   - Modify the script located [here](https://github.com/BHatten1000/Active-Directory-Lab/blob/main/Generate-Names-Create-Users) to your use case. You may want to change the default password or increase or reduce the number of Users. (The script will create a new OU called _Users and generate a number of users within it. It will also create usernames in FLast format. Finally it will and apply the plain text password to ALL of them to build out a userbase for our AD lab.)
    
   - Remember to download the txt file of randomly generated names located [here](https://github.com/BHatten1000/Active-Directory-Lab/blob/main/names.txt) or utilize a file of your own in the same format called names.txt 
    
   - After configuring and running the script linked above (from the directory that names.txt is stored in) you should have a large userbase to experiment with:

 <img src="https://i.imgur.com/bGL1VLn.png" height="80%" width="80%"/>
<br />
<br />
       
       
<!--Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
--!>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
