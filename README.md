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

-  Install Active Directory
-  Create a Domain Admin user within the domain
-  Join Client-1 to the domain (mydomain.com)

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/Y4DTdED.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Setup Domain Controller in Azure:

- Create a Resource Group
- Create a Virtual Network and Subnet
- Create the Domain Controller VM (Windows Server 2022) named “DC-1”
- After VM is created, set Domain Controller’s NIC Private IP address to be static
- Log into the VM and disable the Windows Firewall (for testing connectivity)

Setup Client-1 in Azure

- Create the Client VM (Windows 10) named “Client-1”
- Attach it to the same region and Virtual Network as DC-1
- After VM is created, set Client-1’s DNS settings to DC-1’s Private IP address
-  From the Azure Portal, restart Client-1

</p>
<br />

<p>
<img src="https://i.imgur.com/25ZyRK7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  Installing Active directory:
  
- Login to DC-1 (VM) and install Active Directory Domain Services
- Promote as a DC: Setup a new forest as mydomain.com (can be any name)
- Restart and then log back into DC-1 as user

</p>
<br />

<p>
<img src="https://i.imgur.com/qMXSe4i.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  Creating Domain Admin:
  
- In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
- Create a new OU named “_ADMINS”
- Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
- Add jane_admin to the “Domain Admins” Security Group
- Log out / close the connection to DC-1 and log back in as “mydomain.com\jane_admin”

</p>
<br />

<p>
<img src="https://i.imgur.com/ge0Mde9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  Join Client one to the domain:
  
- Login to Client-1 as the original local admin (labuser) and join it to the domain (computer will restart)
- Login to the Domain Controller and verify Client-1 shows up in ADUC
- Create a new OU named “_CLIENTS” and drag Client-1 into there

</p>
<br />
