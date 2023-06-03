<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Windows Active Directory Deployed in the Cloud (Azure)</h1>
Hey, I'm Kenneth, an IT Professional. This is a tutorial that outlines the implementation of on-premises Active Directory (Windows) within Microsoft Azure Virtual Machines (VM).<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (VMs/Compute)
- RDP (Port: 3389)
- Active Directory Domain Services (Windows Server 2022)
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

1. Create VM with Windows Server OS and create a VM with Windows 10/11 OS. 
2. Install/enable Active Directory (AD) Domain Services in the Server VM, make the server a Domain Controller, and then add the Client VM to that Domain.
3. Within AD create a organizational unit for Admin and create a user account and grant admin permissions. 
4. Using Powershell script, create randomized user accounts in AD and attempt to login to the client as one.
5. Mess around with capabilities of AD.

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> 1. First, we need to setup two virtual machinces in Microsoft Azure. One will be for our Server which will host AD and one will act as a client attached to the same Domain as our Server. The server will act as the Domain Controller for this network. In Azure, we need to create a resource group (RG) and then our virtual machines (or u can start creating VMs and it will allow u to create a RG from there). Make sure to give your VMs distinct names (so not to get them confused) and right down login information if neccesary. Next Step...

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
