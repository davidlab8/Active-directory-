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

![C21D7F2E-992E-4CAA-9E36-E2C7B1A56CC4](https://github.com/davidlab8/Active-directory-/assets/154483052/8a536f4b-d844-495e-aa2d-7b30dd70b520)

 ![6959EA7C-A466-400B-948C-4B0B5E266F55](https://github.com/davidlab8/Active-directory-/assets/154483052/5db12451-d7c8-4f7b-844b-101e104bbb39)

![5696E6CF-4D0A-4656-B8D7-06D0FB7796B4](https://github.com/davidlab8/Active-directory-/assets/154483052/a453f589-faab-46e3-bd05-673857b6312b)

![527D43EB-BB76-45A3-974B-921E99A41DB1](https://github.com/davidlab8/Active-directory-/assets/154483052/23116f9b-2077-4cac-a34b-897e0fda5375)


![E246D448-3B20-4F43-ACA9-A83C910FDC9D](https://github.com/davidlab8/Active-directory-/assets/154483052/0d7915b2-bc8a-4b55-badb-3334fc1ce47c)

![1AE1438A-40A6-4FF2-8B46-513ABB01BE0D](https://github.com/davidlab8/Active-directory-/assets/154483052/9d063b72-ad51-4623-b066-26748a38817d)

![5F487FFA-786C-44DB-9CFA-CB12C079FD9F](https://github.com/davidlab8/Active-directory-/assets/154483052/1effcc5c-7cff-489c-b9f5-8a957ca75514)

![6158E548-4752-4397-8374-7403A15B0A80](https://github.com/davidlab8/Active-directory-/assets/154483052/5136d321-4b98-4c07-9c2b-83162e7ca26d)

- Step 1. On Azure create RG, VPN, DC1 (window server), and Client1 (windows 10)
    - DC1 menu, networking, networking interferface, IPconfig, change dynamic to static (save)
  - Copy DC1 public Ipaddress, paste it to remote desktop to connect, start (type) wf.msc (firewall menu) inbound rules, click on protocol located top bar on the right,
look for the first 3 ICMP rules (right click) to enable rules, (copy) Client1 public ip address connect remote desktop command prompt ping (Client1 private ip) it should communicate
  - DC1 desktiop go to server manager, add roles and features, (click on) Active directory Domain Services, install, (server mode dashboard) go to (triangle emblem),
Promote this server as main controller, (display config menu) add new forest, (example) root name: mydomain.com, password: Password1, install (it may restart automatically) 
log back in using mydomain.com\username .

![0BDCF1DF-14E1-4FE1-8047-12060A6DA772](https://github.com/davidlab8/Active-directory-/assets/154483052/81cd1ce5-a7da-442d-af13-484432230ec5)

![FA45F6DD-7125-4BEB-9B61-439F8797D0AF](https://github.com/davidlab8/Active-directory-/assets/154483052/c036bebf-c1a4-48ad-a786-5753ecf45728)
  
  ![2D29FD48-C70A-416A-A150-4655441C72EF](https://github.com/davidlab8/Active-directory-/assets/154483052/5cb5a074-74e9-4f64-bb66-ec6e8fe52725)

![B3AC7DD8-D6BD-42E0-B9A9-BF6AB26B5A26](https://github.com/davidlab8/Active-directory-/assets/154483052/1ac4fb86-08fd-41a7-8292-1fe6a32bd6e8)

![05A67A85-3940-4DFE-8721-BA66F3E1FF86](https://github.com/davidlab8/Active-directory-/assets/154483052/0c36617b-cf74-46b4-ab0d-614e9f90ca87)







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



