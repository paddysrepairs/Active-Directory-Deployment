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
- Step 17- In "DC-1", go to Windows Administrator Tools and select Active Directory and Users. Right click on your domain, create new organizational group. Make sure spelling of group "_EMPLOYEES" is correct for later. Create another organization group called "_ADMINS"
- Step 18- Setup administrator account.
- Step 19- Add Administrator we just created to the group we created in previous step.
- Step 20- From here on we are going to use Admin Account for exercise. Can log into DC-1 with those creds at this point as well.
- Step 21- Switch back into Client-1. Adding it to the domain we setup.
- Step 22- Restart Client-1 when changes are accepted after adding the VM to the Domain.
- Step 23- Logged back into DC-1 with our admin account and check that it was added to domain okay.
- Step 24- Add it into "_CLIENT" Folder.
- Step 25- Logged into Client-1 with our admin account.
- Step 26- Change remote access on Client-1 so that all domain users can access the machine remotely.
- Step 27- Pulled script to create our _EMPLOYEES directory for this exercise. Save to easy access location.
- Step 28- Double check your active directory users and computers organization unit for spelling to match script.
- Step 29- Run powershell script. Employee roster created successfully!
- Step 30- Try logging in with one of the accounts we created on Client-1. Check to see if account is listed in powershell with command "whoami" if it lists the account you have successfully setup the account running it from active directory.
- Step 31- Open group policy and set lock-out threshold for login attempts.
- Step 32- Go back into DC-1 and reset password from account we used to test lockout policy.
- Step 33- Log back in with account we are were using and check out the event viewer to see the activity. Overview Complete!

<h2>Deployment and Configuration Steps</h2>

<h2>Step 1- Create Resource Group in Azure</h2>
<p>
<img width="1920" height="1080" alt="Step_1_Resource_Group" src="https://github.com/user-attachments/assets/3bdd91aa-8575-4a14-afeb-bb19a83524d5" />
</p>
<p>
Logged into Microsoft Azure account. Go to resource groups and create new "Resource Group".
</p>
<br />
<h2>Step 2- Create Virtual Network</h2>
<p>
<img width="1920" height="1080" alt="Step_2_Virtual_Network" src="https://github.com/user-attachments/assets/86855109-5aa4-4639-a768-19ca1504cdc6" />
</p>
<p>
Created new vnet with in newly created resource group. Named relatively similar to the exercise and made sure to set the region to what we are going to be putting our virtual machines in.
</p>
<br />

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
