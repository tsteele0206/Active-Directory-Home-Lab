<h1>Active Directory Home Lab</h1>


<h2>Description</h2>
In this project I am attempting to create an Active Directory domain to simulate a corporate network using Oracle Virtualbox as well as a Windows Server 2019 ISO and a Windows 10 ISO. I will create a list of users using a PowerShell script on the domain controller. I will add the Windows 10 client to the domain and it will be able to log in as any of the users on said list. This environment will be useful to me for upcoming labs as well as to familiarize myself with Active Directory.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Oracle Virtual Box</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b>Windows Server 2019</b> (21H2)
<h2>Lab walk-through:</h2>

<p align="center">
Download and Install Oracle Virtual Box. <br/>
<img src="https://i.imgur.com/hla54vK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<p align="center">
Download an ISO for Windows 10. <br/>
<img src="https://i.imgur.com/39FgOBt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<p align="center">
 Download an ISO for Windows Server 2019.  <br/>
<img src="https://i.imgur.com/omzwuPD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
I created a VM for the domain controller (Windows Server 2019) and allocated appropriate resources. <br/>
<img src="https://i.imgur.com/3zMBWme.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
In the Network Settings for the Domain Controller, I activated 2 adapters. I configured the first adapter for NAT as this will be facing the internet. I then configured the second adapter for the internal network.  <br/>
<img src="https://i.imgur.com/s9A09pq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Then I opened the domain controller and ran through the Windows setup process.  <br/>
<img src="https://i.imgur.com/O1x2G1b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
When I tried to navigate on the domain controller, I noticed that the VM will not expand to fullscreen as well as some low quality movement when using the mouse. I remedied this by going to Devices > Insert Guest editions CD Image. Then looking in file explorer and under "This PC" I found "Virtual Box Guest Editions". I ran this program and restarted the VM.  <br/>
<img src="https://i.imgur.com/xnFGdMT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 Next I wanted to rename the adapters so I could differentiate between the two. So I opened Network Connections to show my active adapters. Right clicking on both and under properties revealed which adapter had the APIPA address, this being for the internal network. I renamed the remaining adapter for the external internet.  <br/>
<img src="https://i.imgur.com/ETUT1mB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 I then went and renamed the computer "DC".  <br/>
<img src="https://i.imgur.com/63vNhce.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now its time to configure IP addressing for the internal network adapter. I selected 172.16.0.1 as this is a private address different from the range on my external router. I set the subnet mask to 255.255.255.0. The Default Gateway can be left blank as this host will act as the default gateway once Active Directory is installed. The DNS server address can either be set to our own IP address or the loopback address (127.0.0.1)  <br/>
<img src="https://i.imgur.com/8pAzWPA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select roles and features in the Server Manager  <br/>
<img src="https://i.imgur.com/1uI1iLj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Selecting Active Directory Domain Services  <br/>
<img src="https://i.imgur.com/AgcpvE2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
When prompted I clicked install.  <br/>
<img src="https://i.imgur.com/u99ZJca.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
I now have Active Directory Domain Services installed on the DC.  <br/>
<img src="https://i.imgur.com/kVcdJCq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
I named my domain mydomain.com.  <br/>
<img src="https://i.imgur.com/91undwL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
I created an organizational unit for administrators through Active Directory Users and Computers.  <br/>
<img src="https://i.imgur.com/rvCl3r9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
I then created a user for myself within my _ADMINS O.U.  <br/>
<img src="https://i.imgur.com/YK7v6Ob.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
I made my account a domain admin through my account properties.  <br/>
<img src="https://i.imgur.com/ZrwSdcX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next I need to install RAS/NAT so our Windows 10 host can comunicate effectively to the internet while being on its own virtual private network.  <br/>
<img src="https://i.imgur.com/eyU8Ut1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next I configure NAT so that all internal clients receive an internal private IP address.  <br/>
<img src="https://i.imgur.com/3TPV9yK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
I then install a DHCP server to allocate IP addresses to internal clients.  <br/>
<img src="https://i.imgur.com/s64c3uH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next I set my DHCP scope to 172.16.0.100-200 with a subnet mask of 255.255.255.0. This will allow for 100 internal IP addresses.  <br/>
<img src="https://i.imgur.com/wYGgrZf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
I set this to the IP address of the domain controller as the NAT gateway is installed on the domain controller.  <br/>
<img src="https://i.imgur.com/BF7jW5n.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next I run a PowerShell script to create users from a previously generated names list. This creates a _USERS O.U. on the domain controller and creates the user accounts within that O.U. <br/>
<img src="https://i.imgur.com/vLh5Mv1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
This is the result of the PowerShell script.  <br/>
<img src="https://i.imgur.com/OpaSNq9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now that everything is set up on the DC, its time to create a Windows 10 Client VM. I created the VM using the ISO file I downloaded previously. I allocated 4GB of memory and 4 CPU cores.  <br/>
<img src="https://i.imgur.com/JKILbge.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next before starting the VM I opened the network settings for the VM and changed the adapter settings from NAT to "internal network". This will allow the VM to obtain an IP address from the DHCP server on the DC rather than reaching out to my home router.  <br/>
<img src="https://i.imgur.com/FNjZzi3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now I run through the Windows 10 setup process, making sure to select Windows 10 Pro when asked which edition I want to install.  <br/>
<img src="https://i.imgur.com/D0yWdFx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now on the DC, I want to enable the router under Server Settings in the DHCP menu as well as set the server IP address as the default gateway. This will allow the client to obtain a IP address from the domain controller as well as use the domain controller as its default gateway.  <br/>
<img src="https://i.imgur.com/xmlVqNH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
This is showing that the client has successfully connected to the DHCP server on the domain controller. The first ipconfig I had ran wasnt showing a default gateway but the second one shows the IP address of the domain controller. Next I ran a ping to google.com to test the connectivity to the internet and I received responses. This shows that our DNS is working as google.com resolved to the correct IP address. This also shows that our router on our domain controller is successfully passing our traffic to the internet.  <br/>
<img src="https://i.imgur.com/0Umk2cs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next on the client I rename the computer "CLIENT1" as well as join "mydomain.com".  <br/>
<img src="https://i.imgur.com/1PcYUuH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now when I select log in as "Other User" on the client it gives me the option to log into a domain account. This means I can log in using any user on the list of accounts I created previously using the PowerShell script.  <br/>
<img src="https://i.imgur.com/uWOLgyC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
