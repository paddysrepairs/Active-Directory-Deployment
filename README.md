# Active Directory Deployment
An overview of setting up on premise active directory using Microsoft Azure Virtual Machines
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This is an outline of showcasing an implementation of on-premises Active Directory within Azure Virtual Machines by moi!<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps Overview</h2>

- Step 1- In Azure, create "Resource Group".
- Step 2- In Azure, create "Virtual Network".
- Step 3- Create your virtual machines in Azure.
- Step 3 Part 2- First VM, create Client-1 (Windows 10 Enterprise VM).
- Step 3 Part 3- 2nd VM, create Domain-Controller "DC-1" (Windows 2022 server).
- Step 3 Part 4- Setup VMs in your chosen RDP client. (My case is in Linux Nobara using Remmina)
- Step 4- Login into your domain controller "DC-1" and turn off Windows firewall for connectivity testing.
- Step 5- Change "Client 1's" DNS server settings to land and connect to your domain controller's private IP address (Found in Azure's settings for the VM.
- Step 6- Set your domain controllers private IP address to be static so its not changing throughout the course of this process.
- Step 7- In client 1. Run Powershell and see if you can ping DC-1 domain controllers private IP address succesfully.
- Step 8- Select DNS server back in server management that we setup in previous steps.
- Step 9- Install "Active Domain Services" on "DC-1"
- Step 10- Restart domain controller after servers if required after install selected.
- Step 11- Run Install and wait for it to finish.
- Step 12- Promote "Domain Controller" in server manager.
- Step 13- Name domain controller/ directory
- Step 14- Set DSRM password just in case.
- Step 15- Finish up DC promotion.
- Step 16- Login back into your domain controller with RDP setup in Remmina.

 
<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To be added*
</p>
<br />
To be added*
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To be added*
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To be added*
</p>
<br />
