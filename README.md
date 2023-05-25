# configure-ad
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Deploy VMs and ensure connectivity
- Install Active Directory and Create Administrator
- Connect Client-1 to Newly-created Domain
- Create Users to Access Client-1

<h2>Deployment and Configuration Steps</h2>

<h3>Virtual Machine Setup</h3>


<p>
<h4>DC-1 -> Networking</h4>
<img src="https://i.imgur.com/OnWBg3I.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Network Interface -> IP Configuration</h4>
<img src="https://i.imgur.com/R1hUhYY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Assign IP to 'Static'</h4>
<img src="https://i.imgur.com/fMczCTQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To set up an Active Directory within the Azure Virtual Machine, first we'll set up and configure two different Virtual Machines (VM) on Azure. The first VM will be named DC-1 using the 2022 Windows Server. The 2nd VM will be named Client-1 and will use Windows 10 Pro. Make sure the 2nd VM is using same resource group and Vnet that was created for DC-1.

Next we will set DC-1 NIC Private IP Address to "Static". To do this, go to DC-1 and click on "Networking" under settings to the left. From there, click on the hyperlink next to Network Interface. In the first image above it should say "dc-1304_z1". From the left panel, navigate to "IP Configurations". Clicking on that link will send you to the 2nd image above. Next, click where it says "ipconfig1". After clicking on ipconfig1, it will take you to the the final image above and from there, under the Assignment section, click on "Static" and Save.
</p>
<br />

<h3>Client to Domain Connection</h3>

<p>
<h4>Ping to DC-1</h4>
<img src="https://i.imgur.com/3VygnHR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After setting DC-1's Private IP Address to "Static", log in to the Client-1 VM via Remote Desktop Connection, and open up the command prompt. Send a perpetual ping to DC-1 Private IP Address with "Ping (Private IP Address) -t". For this example the Private IP is "10.0.0.5". Notice how the ping does not go through and is unable to verify a connection to the Domain Controller. To fix this, minimize the Client-1 VM and login to the DC-1 VM.
</p>
<br />

<p>
<h4>Server Manager on DC-1</h4>
<img src="https://i.imgur.com/P9k6qm6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Navigate to Windows Defender Firewall, Enable ICMPv4-in</h4>
<img src="https://i.imgur.com/X9LOD9Z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Client-1 Successful Ping to DC-1</h4>
<img src="https://i.imgur.com/a1qS8Ii.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Accessing DC-1 will immediately start up the Server Manager program shown in the first image above upon first logging in. To enable the Client VM to ping our Domain Controller, first click on the Start Menu and navigate to Windows Defender Firewll, and on the left click on "Advanced Settings". On the left side of the Advanced Settings, click on "Inbound Rules" and look for "Core Networking Diagnostics - ICMP Echo Request (ICMPv4-in). There will be two of them: One for Domain and another for Public, Private. Right-click on each of them and enable both rules. One you finish that, go back to CLient-1 and you will see that there is now a verified ping from the Client VM to the Domain VM. Once a ping is established, press Ctrl+C to cancel the perpetual ping.</p>
<br />

<h3>Active Directory Installation Setup</h3>

<p>
<h4>Enable Active Directory Domain Services</h4>
<img src="https://i.imgur.com/fTlqShB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Placement</h4>
<img src="https://i.imgur.com/fTlqShB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Placement</h4>
<img src="https://i.imgur.com/fTlqShB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Deploy Config, Add New Forest</h4>
<img src="https://i.imgur.com/8PKp778.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To begin installing the Active Diretory, go back to the "Server Manager" Dashboard in DC-1 and click on "Add Roles and Features". Click Next until you reach 'Server Roles' and check the box for "Active Directory Domain Services". Click next from there and "Install".
  
 After installing, go back to the "Server Manager" Dashboard and at the upper right of the program, there will be a flag with a notification on it. Click on it and click "Promote this server to a domain controller". Click on "Setup a new forest" and it will give you the option to set up a new domain name. For this tutorial we will go with "Mydomain.com". Set up the password and click 'Next' until you hit "Install". Installing will reset the VM as well as the Remote Desktop Connection.
  
Once the VM has successfully rebooted, you will be required to log back in. However, instead of using the username created for the VM, you will use the name you set for the server. In this tutorial's case, it will be "mydomain.com\labuser". Keep in mind that the password itself for logging in has not changed, only the username.
</p>
<br />

<h3>Administrator User Setup</h3>

<p>
<h4>Accessing Active Directory</h4>
<img src="https://i.imgur.com/HwVT6RG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>New Folders in Active Directory</h4>
<img src="https://i.imgur.com/dlOZkBQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Log into DC-1 as New Admin</h4>
<img src="https://i.imgur.com/3hi73Kx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now that we have our Active Directory up and running, open up the Start Menu and type in "Active Directory Users and Computers", then navigate to "mydomain.com", or what you have chosen to name your domain controller. Right-click on the domain controller's name, and we will create two new Organizational Units (OUs) labeling them as _EMPLOYEES & _ADMINS (This is to make the changes transparent for this tutorial). 
  
In the _ADMINS folder we will create a new employee (user) who will be an administrator named "Jane Doe", with the usename "Jane_Admin", and with the same password we gave domain controller (for simplicity). When filling out the password, make sure not to check the box requiring password reset at first login. To add Jane Doe to the Domain Admins Security Group, first we will right click on her user and go down to 'properties'. Next navigate to the tab 'member of' and you'll see that she is a member of "Domain Users". Click on the "Add" button and type in "Domain Admins". Check Names to see if the security group exists. Once confirmed, click "OK", then "Apply" and "OK" under Jane Doe Properties. Jane Doe should now be considered an Administrator for our newly-created Active Directory. To verify this, log out of DC-1 and log back in as Jane_Admin (Do not just close and reopen the VM, you will have to actively sign out of the user within the VM). Once we are logged in we can open up the command prompt and type in "whoami", and we will see that we are in-fact logged in as Jane_Admin. From here on out we will continue using Jane_Admin for DC-1.
</p>
<br />

<h3>Joining Client-1 to DC-1</h3>

<p>
<h4>Failed Computer Connection to Active Directory</h4>
<img src="https://i.imgur.com/GvSjZs9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Change Client-1's DNS to DC-1 Private IP</h4>
<img src="https://i.imgur.com/aTxhhEs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Client-1 Successful Connection to Active Directory</h4>
<img src="https://i.imgur.com/ZWM6GZs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Next we will now attempt to join Client-1 to the DC-1 Active Directory. To do this, return to Client-1's VM, and type in "About" in the Start Menu. Go to "Rename this PC (Advanced) at the right, and click on the "Change" button. Change the setting from "workgroup", to "Domain", and fill in "mydomain.com". You'll immedaitely notice that it does not work because 'mydomain.com' could not be contacted. This is because Client-1 is currently using a public DNS and is unable to establish a connection to the Active Directory. To fix this, we need to go into Azure and change Client-1's DNS to DC-1's Private IP Address.
  
Go back to Client-1 in Azure and go to "Networking". From there, click on the client name next to "Network Interface" and it will take you into Client-1's Networking. On the left, go to "DNS Servers" and change the DNS Server from "Inherit from Virtual Network" to "Custom". Fill in the Custom DNS with DC-1's Private IP Address, and click Update. Once the update is completed, restart Client-1, log back in to the VM and try again. Go to the "About" page of Client-1, go to "Rename this PC (Advanced)", click on "Change" and switch from workgroup to domain. Type in the domain name, in this case "mydomain.com", and Client-1 will have a successful connection to the Active Directory this time and restart one more time. After Client-1 restarts, we can now log in to it with our Jane_Admin credentials because it is not connected to the domain.
</p>
<br />

<p>
<h4>Client-1 in Active Directory</h4>
<img src="https://i.imgur.com/0cRWToW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Allow Domain Users to log into Client-1</h4>
<img src="https://i.imgur.com/ca2uN9W.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Going back to the DC-1 Active Directory Computers and Users page, we can see that Client-1 is connected to the Domain Controller now, and can receive and send data to and from the Domain.
  
However, we want all users within the domain to be able to access this computer. So what we will do is log into Client-1 as Jane_Admin, open up the "About" Page from the start menu again, but this time open up the "Remote Desktop" tab in the right. Under "User Accounts" click on "Select Users that can remotely access this PC" Click Add and type in "Domain Users" and click ok. This will allow any user registered within the domain to be able to access this computer remotely, not just administrative users. 
</p>
<br />

<h3>Creating New Users</h3>

<p>
<h4>Script to Make New users</h4>
<img src="https://i.imgur.com/cqR7Ezg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h4>Successful Login to Client-1 with New Username</h4>
<img src="https://i.imgur.com/1cIiHNA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To test this, we'll need to create a bunch of users that have access to this remote desktop. Return to DC-1's VM, logged in as Jane_Admin and open up Powershell ISE (As an Administrator). To speed things up we'll be using a script created to generate a bunch of random accounts in our _EMPLOYEES Folder that we created earlier. Every user generated from this script will have a random first and last name, and every user will have the same password assigned to them.
  
Lastly to test that these accounts do in-fact work, we will log into Client-1 with one of the newly created Usernames. For this example we will log in with Fico.Xidu.
  
As you can see in the final image above, we have successfully logged in with a randomly generated account. Using the command prompt we can see that we are still in Client-1 and we have indeed logged in with Fico Xidu. And our Client-1's DNS Server is the same as DC-1.
</p>
<br />

