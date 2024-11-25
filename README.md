<p align="center">

<img src="https://marketplace.radiantlogic.com/wp-content/uploads/bw_store_facet_images/bw_activedirectory_bw_activedirectory-900x0.png" alt="Active Directory logo"/>
 
 <h1>#DeployingActiveDirectory</h1>
This tutorial outlines the installation of Active Directory and its dependencies to create our mock environment.
<br />


<h2>Environments and Technologies</h2>

- <b>Microsoft Azure</b> 
- <b>Remote Desktop</b>

<h2>Operating Systems</h2>

- <b>Windows 10</b> (22H2)
- <b>Windows Server</b> (2022)
  <br />

<h2>List of Prerequisites</h2>

- <b>Azure Resource Group</b> - acts as a folder for our resources
- <b>Azure Virtual Network and Subnet</b> - functions as our network environment
- <b>Client-1 and DC-1 Virtual Machines</b> (VMs)

<h2>Installing Active Directory:</h2>
Log into DC-1 via remote connection. You will first use the login credentials from the first part of this lab. We must install Active Directory Services from the Server Manager interface, which can be accessed by right-clicking the start icon. Click "add roles and features" within the Server Manager.

  <br />
  <br />
<img src="https://i.imgur.com/r18mIyq.png" height="60%" width="60%" alt="Server Manager Interface: Add roles and features."/>
<br />
<br />

Click Next until you see the option to Install "Active Directory Domain Services". Click "add features," then next several times until the "Install" feature appears. There is also the option of checking a box that will automatically restart the VM once the installation is complete.
<br /> Within the Server Manager Dashboard, click the flag in the top rght corner and select "Promote this server to a domain controller."
<br />
<br />
<img src="https://i.imgur.com/ZtXorpi.png" height="60%" width="60%" alt="AD Install"/><br />
<br />
<br />

Next, we will promote the server to a Domain Controller (DC). *This simply means we will be promoting a server to a domain controller means converting it into a system that manages user logins, security policies, and directory services within a domain.*
<br />
<br />
<img src="https://i.imgur.com/bajkVZp.png" height="60%" width="60%" alt="Promote DC-1"/>
<br />
<br />

Under "Deployment Configuration," select "add a new forest" and enter "mydomain.com". 
  <br/>

<img src="https://i.imgur.com/SuiSvQv.png" height="60%" width="60%" alt="set up a new forest"/>
<br />
<br />

We will come to another menu where we are prompted to create a password for "Directory Sevices Restore Mode," which is a data-recovery service native to the application. For the purposes of this lab, it is unlikely we will have to use this, but make sure to write it down.
<br />

<img src="https://i.imgur.com/HAz4rZk.png" height="60%" width="60%" alt="DSRM"/>

<br />
<br />
Deselect "DNS delegation" when prompted, then click next until you reach the option for Installation. Proceed.
  <br />
  <br />
<img src="https://i.imgur.com/AqzI1h4.png" height="60%" width="60%" alt="DNS delegation"/>
<br />
<br />

Restart when the installation is complete. Remote connection will end. You will log back in with new credentials as a result of our changes. For example, I will log back in with "mydomain.com\labuser" as the username and use the same password. *Please pay close attention and use the backslash to enter your credentials.*

<br/>
<img src="https://i.imgur.com/Ei5YOZd.png" height="50%" width="50%" alt="login as mydomain user"/>
<br />
<br />


<h2>Create a Domain Admin user within the domain</h2>

Open Active Directory Users and Computers (ADUC).
<br/>
<img src="https://i.imgur.com/LY98lzT.png" height="60%" width="60%" alt="ADUC"/>
<br />
<br />

In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”. 
<br/>

<img src="https://i.imgur.com/DVML3WQ.png" height="60%" width="60%" alt="ADUC _EMPLOYEES"/>
<br />
<br />


Here we name our folder or OU. It is *incredibly* important that we add the underscore (_) before EMPLOYEES for later steps.
<br/>

<img src="https://i.imgur.com/kHBydhn.png" height="60%" width="60%" alt="_EMPLOYEES"/>
<br />
<br />

Repeat the above with another OU called "_ADMINS".
<br/>

<img src="https://i.imgur.com/IZMkwQJ.png" height="60%" width="60%" alt="Ensure ping succeeded"/>
<br />
<br />


Now under the _ADMINS OU, we will create a new user.
<br/>

<img src="https://i.imgur.com/9OBq9qL.png" height="60%" width="60%" alt="new admin user."/>
<br />
<br />

Our User will be named Jane Doe and the username will be jane_admin. 
<br/>

<img src="https://i.imgur.com/sdnSU3O.png" height="60%" width="60%" alt="credentials"/>
<br />
<br />


Next, we will configure the propertes for our new admin to give her special permissions. Make her a member of the group "domain admins." The steps in reaching this menu are listed below. Use this account and password to login to the DC from now on.
<br/>

<img src="https://i.imgur.com/SFcbx8W.png" height="60%" width="60%" alt="Jane Doe properties"/>
<br />
<br />


<h2>Join Client-1 to your domain (mydomain.com)</h2>

Login to Client-1 as the original local admin (labuser) and join it to the domain. Under Settings, click Rename this pc (advanced)>System Properties>Change>Domain:> enter mydomain.com and enter the admin password to apply the changes. The computer will restart.
<br/>

<img src="https://i.imgur.com/97Tvfnx.png" height="60%" width="60%" alt="Join Client-1 to the Domain."/>
<br />
<br />

Login to the Domain Controller and verify Client-1 shows up in ADUC.
<br/>

<img src="https://i.imgur.com/qWNWTuz.png" height="60%" width="60%" alt="Client-1 in ADUC"/>
<br />
<br />


Lastly, we will create a new OU named “_CLIENTS”.
<br/>

<img src="https://i.imgur.com/NxI8OwA.png" height="60%" width="60%" alt="Create new OU called _CLIENTS."/>
<br />
<br />
Drag Client-1 into our new OU called _CLIENTS.
<br/>
<br />

Finish the lab, but do not delete the VMs in Azure. We will use them for upcoming labs.
If you are done for the day and want to save money, simply “Stop”/turn off the VMs within the Azure Portal
