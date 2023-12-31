<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1> Using On-premises Active Directory Deployed in the Cloud to build intuition for DNS (Azure)</h1>
This tutorial outlines the basics of Domanin Naming System (DNS) Using ano on-premises Active Directory enviroment within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Command Line

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Ping Mainframe from the client and notice it fails
- Create a DNS A-record for mainframe and set it to the Domain Controller's private IP address
- Change the mainframe to 8.8.8.8
- ping the mainframe flush the DNS and then ping it again.
- Create a CNAME record search and have it point to www.google.com
- Use the nslookup command with search to test the CNAME record you made.


<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/b6985cc1-7d9f-4cf6-bda3-e5d068a03437"/>
</p>
<p>
Log into the client VM and use the command line to ping mainframe and notice that it fails
<br />

<p>
<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/91b4344f-117d-4583-a6dd-a34b60836063"/>
</p>
<p>
Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall

</p>
<br />

<p>
<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/17b04fa1-4ae5-4a9f-8456-a5e9d660c80a"/>
</p>
<p>
Check back at Client-1 to see the ping succeed
</p>
<br />


<p>
<h2>Install Active Directory</h2> 
<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/4b61bbdf-451a-497b-9959-e20021f37850"/>
  
Login to DC-1 and install Active Directory Domain Services
</p>
<br />

<p>
Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/06d9aae0-52a8-4078-bedd-dde04634d7f8)"/>
Restart and then log back into DC-1 as user: mydomain.com\labuser
</p>
<p>
  
<h2>Create an Admin and Normal User Account in AD</h2>
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” and one called _ADMINS

<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/b699c7b7-a260-4618-83dd-e88b4ad7772d"/>

Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”. Always make sure to save passwords during labs. It's bad practice to do this at work, but since it's just a lab saving it in a word doc will be ok.

<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/ab8fbdf9-33e6-4608-a0a6-ee0da263b839"/>

Add jane_admin to the built in “Domain Admins” Security Group

<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/972db7b5-9958-4ffa-8603-b4870d447b9e"/>

Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”. Use jane_admin as your admin account from now on.
</p>


<p>
<h2>Join Client-1 to your domain (mydomain.com)</h2>
From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
  
<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/704ff53b-672a-44c4-8787-91394f50ee87"/>

- From the Azure Portal, restart Client-1
- Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
- Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain

<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/140dd6f7-69ab-45a0-bfc8-c66baee05aa9"/>
</p>
<p>

</p>
<h2>Setup Remote Desktop for non-administrative users on Client-1</h2>
Now that the servers are connected we can log into Client-1 as mydomain.com\jane_admin even though that account doesn't exist on Client-1. Once you do that open system properties, click “Remote Desktop”
allow “domain users” access to remote desktop

<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/463eedd1-7a11-4917-8b13-9d36ad51e408"/>

You can now log into Client-1 as a normal, non-administrative user now
Normally you’d want to do this with Group Policy that allows you to change MANY systems at once 

<br /><p>

<h2>Create a bunch of additional users and attempt to log into client-1 with one of the users
</h2>
- Login to DC-1 as jane_admin
- Open PowerShell_ise as an administrator
- Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/bb7ac5ad-4e58-444b-8791-51c4db7398e0"/>

Run the script and observe the accounts being created

<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/2eaa0f6e-b461-4cbd-bc06-1d414120514c"/>

When finished, open ADUC and observe the accounts in the appropriate OU

<img src="https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/c03dea24-fa5e-4c37-80b9-cc2b3abf331e"/>

Attempt to log into Client-1 with one of the accounts (take note of the password in the script)

<img src=""/>
</p>
