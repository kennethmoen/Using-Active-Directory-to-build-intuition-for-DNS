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
<img src="https://i.imgur.com/wv35OZ4.png"/>
</p>
<p>
<h2>Install Active Directory</h2> 
<img src:"https://github.com/kennethmoen/Using-Active-Directory-to-build-intuition-for-DNS/assets/145589069/4b61bbdf-451a-497b-9959-e20021f37850"/>
  
Login to DC-1 and install Active Directory Domain Services
</p>
<br />

<p>
<img src="https://i.imgur.com/Julbyug.png"/>
</p>
<p>
From the DNS manager right click again and create a CNAME or ALias that points to wwww.google.com
</p>
<br />

<p>
<img src="https://i.imgur.com/Julbyug.png"/>
</p>
<p>
From the DNS manager right click again and create a CNAME or ALias that points to wwww.google.com
</p>
<br /><p>
<img src="https://i.imgur.com/kKSiQve.png"/>
</p>
<p>
Use the command nslookup search and it should search the DNS for www.google.com as shown in the above screenshot. This concludes our DNS demonstration. 
</p>
<br />
