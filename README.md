<h1>Active Directory Home Lab</h1>

 ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)

<h2>Description</h2>
Project consists of a simple PowerShell script that walks the user through "zeroing out" (wiping) any drives that are connected to the system. The utility allows you to select the target disk and choose the number of passes that are performed. The PowerShell script will configure a diskpart script file based on the user's selections and then launch Diskpart to perform the disk sanitization.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Oracle Virtual Box</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b>Windows Server 2019</b> (21H2)
<h2>Program walk-through:</h2>

<p align="center">
Download and Install Oracle Virtual Box <br/>
<img src="https://i.imgur.com/hla54vK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<p align="center">
Download an ISO for Windows 10 <br/>
<img src="https://i.imgur.com/39FgOBt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<p align="center">
 Download an ISO for Windows Server 2019  <br/>
<img src="https://i.imgur.com/omzwuPD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Create a VM for both the domain controller (Windows Server 2019) as well as a Windows client (Windows 10) and allocate appropriate resources to both <br/>
<img src="https://i.imgur.com/3zMBWme.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
In the Network Settings for the Domain Controller, activate 2 adapters. On the first adapter, configure for NAT as this will be facing the internet. On adapter 2, configure for internal network, as this will be the adapter for the internal network  <br/>
<img src="https://i.imgur.com/s9A09pq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Open your domain controller and run through the Windows setup process  <br/>
<img src="https://i.imgur.com/O1x2G1b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
When you try to navigate on the domain controller, you will notice that the VM will not expand to fullscreen as well as some low quality movement when using the mouse. This can be fixed by going to Devices > Insert Guest editions CD Image. Then when you open file explorer and under "This PC" you will find "Virtual Box Guest Editions. Run this setup program and restart the VM.  <br/>
<img src="https://i.imgur.com/xnFGdMT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 Open your domain controller and run through the Windows setup process  <br/>
<img src="https://i.imgur.com/O1x2G1b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 Open your domain controller and run through the Windows setup process  <br/>
<img src="https://i.imgur.com/O1x2G1b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 Open your domain controller and run through the Windows setup process  <br/>
<img src="https://i.imgur.com/O1x2G1b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 
 Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
