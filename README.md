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
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<h3>Virtual Machine Setup</h3>


<p>
<img src="https://i.imgur.com/OnWBg3I.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/R1hUhYY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/fMczCTQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To set up an Active Directory within the Azure Virtual Machine, first we'll set up and configure two different Virtual Machines (VM) on Azure. The first VM will be named DC-1 using the 2022 Windows Server. The 2nd VM will be named Client-1 and will use Windows 10 Pro. Make sure the 2nd VM is using same resource group and Vnet that was created for DC-1.

Next we will set DC-1 NIC Private IP Address to "Static". To do this, go to DC-1 and click on "Networking" under settings to the left. From there, click on the hyperlink next to Network Interface. In the first image above it should say "dc-1304_z1". From the left panel, navigate to "IP Configurations". Clicking on that link will send you to the 2nd image above. Next, click where it says "ipconfig1". After clicking on ipconfig1, it will take you to the the final image above and from there, under the Assignment section, click on "Static" and Save.
</p>
<br />

<h3>Client to Domain Connection</h3>

<p>
<img src="https://i.imgur.com/3VygnHR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After setting DC-1's Private IP Address to "Static", log in to the Client-1 VM via Remote Desktop Connection, and open up the command prompt. Send a perpetual ping to DC-1 Private IP Address with "Ping (Private IP Address) -t". For this example the Private IP is "10.0.0.5". Notice how the ping does not go through and is unable to verify a connection to the Domain Controller. To fix this, minimize the Client-1 VM and login to the DC-1 VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/P9k6qm6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/X9LOD9Z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/a1qS8Ii.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Accessing DC-1 will immediately start up the Server Manager program shown in the first image above upon first logging in. To enable the Client VM to ping our Domain Controller, first click on the Start Menu and type in "Control Panel". Navigate to "System and Security" -> Windows Defender Firewall, and on the left click on "Advanced Settings". On the left side of the Advanced Settings, click on "Inbound Rules" and look for "Core Networking Diagnostics - ICMP Echo Request (ICMPv4-in). There will be two of them: One for Domain and another for Public, Private. Right-click on each of them and enable both rules. One you finish that, go back to CLient-1 and you will see that there is now a verified ping from the Client VM to the Domain VM.</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
