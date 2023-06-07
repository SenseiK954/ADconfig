<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Windows Active Directory Deployed in the Cloud (Azure)</h1>
Hey, I'm Kenneth, an IT Professional. This is a tutorial that outlines the implementation of on-premises Active Directory (Windows) within Microsoft Azure Virtual Machines (VM).<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (VMs/Compute)
- RDP (Port: 3389) (testing only; use SSH if need secure)
- Active Directory Domain Services (Windows Server 2022)
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

1. Create VM with Windows Server OS and create a VM with Windows 10/11 OS. 
2. Install/enable Active Directory (AD) Domain Services in the Server VM, make the server a Domain Controller, and then add the Client VM to that Domain.
3. Within AD, create a organizational units for Admin, Employees, and Clients, then create a couple user accounts with one having Admin permissions. 
4. Using a Powershell script, create randomized user accounts in AD and attempt to login to the client as one.
5. Mess around with capabilities of AD.

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/O9UXrQ5.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p> 1. First, we need to setup two virtual machinces in Microsoft Azure. One will be for our Server which will host AD and one will act as a client attached to the same Domain as our Server. The server will act as the Domain Controller for this network. In Azure, we need to create a resource group (RG) and then our virtual machines (or u can start creating VMs and it will allow u to create a RG from there). Make sure to give your VMs distinct names (so not to get them confused) and right down login information if neccesary. Next step...
</p>

<b>Note: Before we hop on to our machines we need to set the private IP address of our Server VM to static (this way it doesn't change even if turned off and the client can join the domain easier). You can do this by going to the VM>Networking>Network Interface (NIC)>IP configurations>click first listed ipconfig>then set from dynamic to static then save. Back to the steps... </b>
</p>
<p>
<img src="https://i.imgur.com/nPrVo5h.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
2a. Next, we log into our server VM using RDP for windows (if using MacOS use alternative app that supports RDP for windows). Once logged on, open "Server Manager" (if not already open). From here click "Add roles and features". In the installation wizard, click next until you get to "Server Roles" then select/enable "Active Directory Domain Services"(add features). Then click next all the way until you click install. Now you can click close on the wizard then you should see a indicator by "Notifications" (the flag). Click on notifications and then click "Promote this server to a domain controller". Once open, click "add a new forest and type in "mydomain.com" or a random domain name in the box (make sure its not real for lab purposes and <b> WRITE IT DOWN</b>). Click next, then enter a password (it is not necessary for the lab but write it down just in case). Click next the rest of the wizard and then install. Once installed, it will restart the machince, so log back into the VM.
Next step...

<img src="https://i.imgur.com/vOUjHa4.png" height="60%" width="70%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/UsWWf3v.png" height="60%" width="70%" alt="Disk Sanitization Steps"/>
  
2b. Now that AD is installed, we need to join the client VM to the domain. To do that we need to change the DNS settings of our client VM and make our server a temporary DNS server in the client's eyes. Minimize your RDP connections and go to the Azure portal. From Azure, go to the server VM and copy the PRIVATE ip address (located in the networking section, make sure its not the public ip). Now go to your client VM, click the networking section> click the NIC> click DNS Servers> click custom> enter the private ip address of your server VM (make sure no spaces), then save. Restart your client VM and relogin once ready. Once logged on, open Settings> go to System> go to About> then click "Rename this PC(advanced)"> click change> then enter your domain name that you wrote down in step 2a. Then it will prompt you to login, use the login credentials for your server VM (before it became a domain, don't add a .com). Next step...
</p>

<img src="https://i.imgur.com/9bjp0Rz.png" height="50%" width="50%" alt="Disk Sanitization Steps"/><img src="https://i.imgur.com/dJDGlpP.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>
3a. To continue, open up and log in to the server VM. Search and open up Active Directory Users and Computers. On the left panel, click the drop down arrow of the domain name (ex. mydomain.com). You can click on Computers to see your client VM there and on Domain Controllers to see the server VM there by clicking on those respective links. After, right click to domain name> go to new> then click "Organizational Unit"(OU)> name it _ADMINS. Then create two more: one named _EMPLOYEES (this one has to be named exactly like this for future steps in this lab) and the other named CLIENTS. Next, we will create a admin user by the name of Jane Doe (it can be any name you want). Right click your Adnin OU> go to new> then click user. Enter the name of your user and username (no spaces, use underscores instead). Then hit next, enter a password (you can reuse your current one or make another just make sure ot keep track of it), before you clcik next <b>UNCHECK</b> the "user must change password at next logon" (this is for lab only, in real world you should keep it). Then click next and OK. Next step...
  
<img src="https://i.imgur.com/lfCsTkP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

3b. Further, we created a user profile and now we need to grant it admin permissions. To do so, right click the user profile (for us its Jane Doe)> click properties> click "Member Of" at the top> click Add> type in the box "domain admin" then click "Check Names"> then click OK> apply and OK (to close). Now log out of your server VM and log back in using the admin user credentials (the user name and password you created in 3a, make sure to add the domain name before the username). Now you are logged in as a Admin in your server VM. Go back into AD Users and Computers and create a user account for both employees and client OUs. Next step...
</p>
<img src="https://i.imgur.com/OOBDnzL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
4.  Moving on, now that we have our AD up, we are going to populate it with random user accounts and try to logon to them using our client VM. Before that, we need to open our client VM up to RDP connections of non-administrative users in the domain (this way any user in the domain can log into the client VM). Now, login to the client VM using the ADMIN credentials (Jane doe). Once loaded, navigate to Settings> System> left panel click "Remote Desktop"> click the hyperlink under "User accounts"> click add> type in "domain users" then check names> then OK out. Afterward, log into your AD server VM (using your admin account). Search and open the Powershell.ise as <b>ADMINISTRATOR</b> (right click then click run as administrator). 
Click this <a href="https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1">link</a> and copy the script (this is a powershell script , which will help us automatically generate randomized domain user accounts which we can use to test the login of of our client VM. <b> Note: Scripting is a great resourse to automate repetitive tasks.</b> In Powershell, click new and then paste the script. Run the script (press the play button at top) then you can let it run until complete or you can stop it prematurely if you wish. Now you can navigate to the _EMPLOYEES OU in AD Users and Computers and observe that users created.

</p>

