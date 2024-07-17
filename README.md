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
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Creation of Virtual Machines using Microsoft Azure
- Using Server Manager to install Active Directory
- Adding users to Active Directory
- Setting permissions to users within Active Directory

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/ZD4wdJP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We begin by creating two seperate virtual machines within Microsoft Azure, Setting up one as a Domain Controller
  (DC-1) and a virtual machine of a normal computer running Windows 10 (Client-1). As well as setting DC-1's NIC Private IP adress to static.
</p>
<br />

<p>
<img src="https://i.imgur.com/8Ur6K0I.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We test the connection between Client-1 and DC-1 to ensure that Client-1 is able to connect with DC-1 by first enabling ICMPv4 in DC-1's firewall settings, then sending a ping from Client-1 to DC-1's private IP address.
</p>
<br />

<p>
<img src="https://i.imgur.com/tyigGiJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />
Open Server Manager by searching for it in your windows search bar, and click on "Add roles and features" and be sure to enable Active Directory Domain Services when prompted.
<p>
<img src="https://i.imgur.com/MGKj6h1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After installing Active Directory, head to the top right and click on the flag icon and select "Promote this server to a domain controller". Select "add a new forest" and add whatever you'd like (ex: mydomain.com). 
</p>
<br />

<p>
<img src="https://i.imgur.com/iXTLEnc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Server Manager, head to tools and select "Active Directory Users and Computers". Select whatever you created in the last section and create two new organazational units. In this picture I created, "_EMPLOYEES" and "_ADMINS". From there you can create new users and assign them to a new unit that was created. In the admins folder under properties of the new user created, add the user to the "Domain Admins" group.
</p>
<br />

<p>
<img src="https://i.imgur.com/2mnNPPQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back in Azure, we need to switch the DNS settings of Client-1 to DC-1's static IP address. After Client-1 is set to DC-1's IP address, join it to the domain by going on Client-1 and opening settings by searching for settings in the Windows search bar, and selecting "Rename this PC (advanced)" and setting it to a member of the domain you created.
</p>
<br />

<p>
<img src="https://i.imgur.com/9CUzSuT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Using Power Shell ISE as an administrator we are able to run a script that allows us to make a lot of random users that we can assign to the organazational unit that was created prior. From there we can assign users to the "Domain Users" group in Active Directory.
</p>
<br />
