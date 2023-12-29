p<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial is a guide on how to create Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Active directory and Configuration Steps</h2>

- Step 1. On Azure set up Resource group, VPN, DC1 (windows server), Client1 (windows 10)
  - Change DC1 DNS from dynamic to static on Azure
  - Enable rules on DC1 to allow Client1 to ping to DC1
  - Install Active Directory on DC1, promote DC1 and set up mydomain.com .

- Step 2. Create organizational units (2 folders) on DC1 name them _EMPLOYEES and _ADMIN
  - Create administrative user account under _ADMIN folder
  - Log out of DC1 then log back in using created admin account 
  - Change Client1 DNS to DC1 domain's DNS.
  
- Step 3. Rename Client1 PC to mydomain.com
  - Client1 Set-up all domain users to be able to log-in
  - DC1 download, install users using script provided
  - Log-in Client1 using a downloaded script user profile.

<h2>Deployment and Configuration Steps</h2>  

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p
          
- Step 1. On Azure create RG, VPN, DC1 (window server), and Client1 (windows 10)
    - DC1 menu, networking, networking interferface, IPconfig, change dynamic to static (save)
  - Copy DC1 public Ipaddress, paste it to remote desktop to connect, start (type) wf.msc (firewall menu) inbound rules, click on protocol located top bar on the right,
look for the first 3 ICMP rules (right click) to enable rules, (copy) Client1 public ip address connect remote desktop command prompt ping (Client1 private ip) it should communicate
  - DC1 desktiop go to server manager, add roles and features, (click on) Active directory Domain Services, install, (server mode dashboard) go to (triangle emblem),
Promote this server as main controller, (display config menu) add new forest, (example) root name: mydomain.com, password: Password1, install (it may restart automatically) 
log back in using mydomain.com\username .

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p
  
  - Step 2. Server manager dashboard go to tools, active directory users and computers, (right click) mydomain.com, new, organizational unit, create _EMPLOYEE and _ADMIN files
    - Inside _ADMIN file (right click) new, admin user name,(example) jane, last name doe, username janeadm, password Password1 (uncheck box where user changes password)
(right click) jane doe, properties, (members tab) add, (type) domain (check names) domain admin, apply
    - log out of DC1 then back in using admin mydomain.com\janeadm
    - Azure (copy) DC1 private ip go to Client1, networking, NIC-IP, dns server, dns custom (paste) DC1 private ip, (save) Client1 restart.

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p
  
  - Step 3. Log into Client1 go to start, system, rename this pc (advanced), change, members of domain, it will ask for admin log in mydomain.com\janeadm password Password1
(computer will restart)
    - log in Client1 adm, start, system, remtote desktop, select users that can remotely access pc, add, (type) domain users, check names, 
(all domain users should be able to log in)
    - DC1 (admin) start, type Windows Powershell ISE (run as admin) copy script 
(https://docs.google.com/document/d/1MqWdlE974hhtshnOsROZ3Yr8xaLd7YuhYbmXhMCiYLY/edit)https://docs.google.com/document/d/1MqWdlE974hhtshnOsROZ3Yr8xaLd7YuhYbmXhMCiYLY/edit
(powershell ise menu) new script, paste, run script users files will start downloading.
    - In _EMPLOYEE file (copy a user id) log out of Client1 and back in using user 
mydomain.com\username 



