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
- Linux Konsole
- Remmina RDP client

<h2>Operating Systems Used </h2>

- Nobara Linux, KDE Plasma interface (Fork of Fedora)
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
<H2>Step 3- Create the Virtual Machines in Azure</H2>
<p>
<img width="1920" height="1080" alt="Step_3_Create_VMS" src="https://github.com/user-attachments/assets/eae2d8d7-7a47-4d3e-9acb-d9cef0d08a90" />
</p>
<p>
Created the virtual machines within Azure. For this activity. Creating only 2 virtual machines. A domain controller and a single client machine.
</p>
<br />
<h2>Client Machine Settings "Client 1"</h2>
<p>
<img width="1920" height="1080" alt="Step_3_Create_VMS_Client-1" src="https://github.com/user-attachments/assets/5ec39018-503c-42df-9b63-a463fe315efe" />
</p>
<h2>Domain Controller "DC-1" Settings</h2>
<p>
<img width="1920" height="1080" alt="Step_3_Create_VMS_DC-1" src="https://github.com/user-attachments/assets/ee6b6bb6-44de-4a51-8b1f-33997329aca6" />
</p>
<br />
<H2>Setting up the Virtual Machines in Remmina</H2>
<p>
<img width="1920" height="1080" alt="Step_3_Setup_VMS_In_Remmina" src="https://github.com/user-attachments/assets/8d7d03a2-fb69-4f95-a4d3-27777b709c42" />
</p>
Next up, since I am using Linux Nobara as my main operating system for this exercise. I am using the the remote desktop client Remmina. At this stage, added the virtual machines I created in Azure to the client. Pulled all required information and inputed in for both Client-1 and DC-1.
</p>
<br />
<h2>Step 4- Disable Firewall for DC-1</h2>
<p>
<img width="1920" height="1080" alt="Step_4_DC-1_Firewall_Disabled" src="https://github.com/user-attachments/assets/5b2c63ee-8b42-4e17-8c62-d43a90193a87" />
</p>
<img width="1920" height="1080" alt="Step_4_DC-1_Firewall_Disabled_2" src="https://github.com/user-attachments/assets/e25a1a07-bf85-4469-a1a8-2ca11893592b" />
<p>
For the purpose of this activity. I turned off the domain controller VM's firewall for the sake of testing and making sure connectivity will work and can be tested properly within the VM's and network.
</p>
<br />
<h2>Step 5- Change Client-1's DNS server to Private IP of DC-1</h2>
<p>
<img width="1920" height="1080" alt="Step_5_Client_1_DNS_Settings" src="https://github.com/user-attachments/assets/2a009c0f-1cda-4501-9369-4f67609aa4db" />
</p>
<p>
<img width="1920" height="1080" alt="Step_5_Client_1_DNS_Settings_2" src="https://github.com/user-attachments/assets/27b8924d-78db-40b0-9aeb-4ecfb61d947c" />
</p>
Made sure to find DC-1's private IP address on Azure and set it as the DNS server on Client-1 in the network card attributes as pictured.
<br />
<H2>Step 6- Set DC-1's Private IP address to "Static"</H2>
<p>
<img width="1920" height="1080" alt="Step_6_DC-1_Static_IP" src="https://github.com/user-attachments/assets/0e6cf60d-5823-4942-ac52-1d9851d84391" />
</p>
<p>
Since we want to make sure the DNS server is not interrupted and remains unchanged. Made sure to set DC-1's Private IP to static so that no matter what through this exercise that it would remain unchanged.
</p>
<br />

<H2>Step 7- Log back into Client-1 and Ipconfig /all and ping in Powershell to Check DNS"</H2>
<p>
<img width="1920" height="1080" alt="Step_6_DC-1_Static_IP" src="https://github.com/user-attachments/assets/b93866b2-68c3-45b8-a4e9-256901ed444b" />
</p>
<img width="1920" height="1080" alt="Step_7_Ping_DNS_Client_1" src="https://github.com/user-attachments/assets/fe1d3c3b-343a-4321-aebd-8395af330328" />
<p>
At this stage we want to make sure that the DNS is correct. Logged into DC-1 and double checked that the DNS changes we made are reflected in Powershell through the "ipconfig /all" command. It is a good idea to restart the domain controller and client with this updates in Azure to make sure that the setting changes are reflected in the VM's.
</p>
<br />

<H2>Step 8- On DC-1, Finalize Setup for DNS Server"</H2>
<p>
<img width="1920" height="1080" alt="Step_8_Select_Server" src="https://github.com/user-attachments/assets/3ac88d2c-0fdf-46ad-b464-43c707168140" />
</p>
<p>
Need to finish the process of setting up the DNS server in our domain controller. Go into server manager and select the server we wish to use as pictured.
</p>
<br />

<H2>Step 9- Install Active Directory Services"</H2>
<p>
<img width="1920" height="1080" alt="Step_9_Install_Active_Direc_Services" src="https://github.com/user-attachments/assets/fa048436-22eb-4a3e-af8b-8d3ddef0e191" />
</p>
<p>
Continued forth and install the "Active Directory Services" required to run our ADS for this activity. Made sure it is selected as shown and clicked onto the next steps.
</p>
<br />

<H2>Step 10- Restart DC-1 if Required"</H2>
<p>
<img width="1920" height="1080" alt="Step_10_Install_Restart_If_Required" src="https://github.com/user-attachments/assets/e94ab81e-f70e-402b-919a-9f711c61172f" />
</p>
<p>
The domain controller machine "DC-1" will more than likely need a restart after the active directory services install. Just accept it and proceed to the install.
</p>
<br />

<H2>Step 11- Install Active Direc Services Final"</H2>
<p>
<img width="1920" height="1080" alt="Step_11_Installing" src="https://github.com/user-attachments/assets/d51d07ff-f527-4123-bb1d-9579a45055be" />
</p>
<p>
Continue and finish Install of "Active Directory Services".
</p>
<br />

<H2>Step 12- Domain Controller Promotion"</H2>
<p>
<img width="1920" height="1080" alt="Step_12_DC_Promotion" src="https://github.com/user-attachments/assets/933bdbdf-daeb-44d3-bc82-037c73d16a3f" />
</p>
<img width="1920" height="1080" alt="Step_12_DC_Promotion_2" src="https://github.com/user-attachments/assets/6648c31c-1bb8-4fd1-b0b2-f126a689c285" />
<p>
Now that all the good stuff is installed that we need for active directory. It is time to promote the domain machine as the domain since we have not technically done it yet.
</p>
<br />

<H2>Step 13- Domain Controller Naming</H2>
<p>
<img width="1920" height="1080" alt="Step_13_DC_Promotion_Name" src="https://github.com/user-attachments/assets/b295f00e-d596-444d-8ea7-de4733d4980f" />
<p>
In the deployment configuration settings, I created a new forest. In this case naming convention activedirec.com to keep with the excercise.
</p>
<br />

<H2>Step 14- Directory Service Restore Mode Password (DSRM)</H2>
<p>
<img width="1920" height="1080" alt="Step_14_Promotion_DSRM_Password" src="https://github.com/user-attachments/assets/f0df8490-1573-4bdc-9b8b-99133e3a81d6" />
<p>
Just in case add a DSRM. Always a good option to have recovery for any system you have implented.
</p>
<br />

<H2>Step 15- Directory Service Restore Mode Password(DSRM)</H2>
<p>
<img width="1920" height="1080" alt="Step_15_Promotion_Finished" src="https://github.com/user-attachments/assets/8654d01d-6160-4689-a1eb-190fa3326213" />
<p>
Domain controller is finished setting up! WOOT WOOT.
</p>
<br />

<H2>Step 16- Switch DC-1 to domain</H2>
<p>
<img width="1920" height="1080" alt="Step_16_Login_with_Domain" src="https://github.com/user-attachments/assets/0fa660f9-cc8d-4899-8dde-e0c2dcc2513c" />
<p>
Now that the domain is all set up. Be sure to set up the updates in Remmina for DC-1 and Client-1 VM's.
</p>
<br />

<H2>Step 17- Log back into DC-1 and Open Active Directory Users and Computers</H2>
<p>
<img width="1920" height="1080" alt="Step_17_Admin_Tools" src="https://github.com/user-attachments/assets/ea0d5248-92f3-4a3f-941a-7caf721c6457" />
<p>
Now that the domain is all set up. Be sure to set up the updates in Remmina for DC-1 and Client-1 VM's.
</p>
<img width="1920" height="1080" alt="Step_17_Organizational_Unit" src="https://github.com/user-attachments/assets/8bb47fa5-70a1-4695-89f7-cd47bc0fe466" />
<p>
<img width="1920" height="1080" alt="Step_17_EMPLOYEES" src="https://github.com/user-attachments/assets/92b7f661-f872-4199-8a79-93cb49f59c23" />
</p>
Create organizational group in Active directory users called "_EMPLOYEES" and make sure the spelling is 100% correct as shown.
<p>
<img width="1920" height="1080" alt="Step_17_ADMINS" src="https://github.com/user-attachments/assets/df38a4e2-cd48-4491-9146-0464b501de31" />
</p>
<p>
Create a 2nd organizational group called "_ADMINS" making sure that spelling is 100% correct.
</p>
<br />

<h2>Step 18- Create a New Admin User</h2>
<p>
<img width="1920" height="1080" alt="Step_18_Create_Admin" src="https://github.com/user-attachments/assets/fcb6a719-efe1-42f2-ba78-4b026115938f" />
</p>
<img width="2050" height="1210" alt="Step_18_Create_Admin_Password" src="https://github.com/user-attachments/assets/ba4ef46a-b528-4972-9015-def127346d74" />
<p>
<img width="2050" height="1210" alt="Step_18_Create_Admin_Password" src="https://github.com/user-attachments/assets/e33e0644-3f8f-433e-9433-ed22a71d0427" />
</p>
<img width="2050" height="1210" alt="Step_18_Create_Admin_Prof_Sada" src="https://github.com/user-attachments/assets/9d41eace-ae1b-4299-b43b-54c934878340" />
</p>
Created the admin account we are going to be used on going for the rest of the exercise.

<h2>Step 19- Add Admin to the Group that was Created</h2>
<p>
<img width="2050" height="1210" alt="Step_19_Add_Admin_Group" src="https://github.com/user-attachments/assets/4caabe48-86d7-4d9a-a490-2f231ba562eb" />
<p>
<img width="2050" height="1210" alt="Step_19_Add_Admin_Group_2" src="https://github.com/user-attachments/assets/b79a607f-5749-4ca5-8bba-5197456229ad" />
<p>
<img width="2050" height="1210" alt="Step_19_Add_Admin_Group_3" src="https://github.com/user-attachments/assets/69383ad3-4ae0-4f82-bea7-c1a65c993e78" />
</p>
Add new Admin as a member of "Domain Admins".
<br />

<h2>Step 20- Login to DC-1 as our New Admin Account</h2>
<p>
<img width="930" height="758" alt="Step_20_Login_Sada_Admin" src="https://github.com/user-attachments/assets/761b0a4d-d650-4177-8883-5aedaadd1112" />
</p>
Logged into with our fresh new admin account to DC-1 so it is in use on going.
<br />

<h2>Step 21- Add Client-1 to the Domain</h2>
<p>
<img width="1920" height="1080" alt="Step_21_Add_Client-1_Domain" src="https://github.com/user-attachments/assets/9ce59f49-749e-473a-80a8-b389c3f71c87" />
<p>
<img width="1920" height="1080" alt="Step_21_Add_Client-1_Domain_2" src="https://github.com/user-attachments/assets/8d1e31e6-d6ac-4cdf-bc4b-b19ab4ca49e2" />
<p>
<img width="1920" height="1080" alt="Step_21_Add_Client-1_Domain_3" src="https://github.com/user-attachments/assets/9011723d-a756-4c85-8193-3fccadedae52" />
</p>
Followed the steps above to add Client-1 to the domain created "activedirec".
<br />

<h2>Step 22- Restart VM after adding it to the Domain</h2>
<p>
<img width="1920" height="1080" alt="Step_22_Restart_After_Add" src="https://github.com/user-attachments/assets/7155c29a-9785-46e9-a9b1-7fb7dca44b29" />
</p>
After adding Client-1 to the domain. It will prompt to restart the machine. Go ahead and do so.
<br />

<h2>Step 23, Check that the Client Machine has been Added!</h2>
<p>
<img width="1920" height="1080" alt="Step_23_Check_Client_Added" src="https://github.com/user-attachments/assets/68a3418f-71e2-45aa-b269-2d89512b00fd" />
</p>
Go into Active Directory Users and Computers and check to make sure that the Client-1 VM has been added to the domain all good.

<h2>Step 24, Organize Further</h2>
<p>
<img width="1920" height="1080" alt="Step_24_Add_Client_Folder" src="https://github.com/user-attachments/assets/71bf4a95-9e10-4793-a620-bd03433df8ad" />
</p>
To keep things organized and cleaned up further. Add Client-1 to its own folder "_CLIENTS".
