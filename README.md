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
<img src="https://i.imgur.com/bSj60xq.png"/>
</p>
<p>
Log into the client VM and use the command line to ping mainframe and notice that it fails
<br />

<p>
<img src="https://i.imgur.com/KqoamI8.png"/>
</p>
<p>
From the Domain Controller go to tools and then the DNS to open the DNS manager. Open forward lookup zones and right click the center box to create a new A record called mainframe that points to the Domain Controller's private IP address.
</p>
<br />

<p>
<img src="https://i.imgur.com/lP1oTc7.png"/>
</p>
<p>
You can now ping mainframe and it will work as shown in the above screenshot.
</p>
<br />

<p>
<img src="https://i.imgur.com/wv35OZ4.png"/>
</p>
<p>
After you've pinged the DNS and notice that it's still to the Domain Controller's private IP address; Open command line as an administrator and use command ipconfig/flushdns and then ping mainframe again to make the Client access the new DNS.
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
