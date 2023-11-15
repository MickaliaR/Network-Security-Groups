<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, observations with various network traffic to and from Azure Virtual Machines with Wireshark will be made as well as experimentations with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Windows Remote Desktop
- Various Command-Line Tools
- Network Protocols 
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Objectives</h2>

- Observe ICMP traffic
- Observe SSH traffic
- Observe DCHP traffic 
- Observe DNS traffic
- Observe RDP traffic

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/5xv8JwB.png"/>
</p>
<p>
- Within Azure portal, create two Virtual Machines sharing the same Vnet. The first Virtual Machine (VM1) will be made with Windows 10 while the second Virtual Machine (VM2) will be created using Linux (Ubantu).
</p>
<br />

<p>
<img src="https://i.imgur.com/SPgmHJV.png"/>
</p>
<p>
- Use Windows Remote Desktop to coonect to the Windows 10 Virtual Machine (VM1). 
</p>
<br />

<p>
<img src="https://i.imgur.com/M6sXb6b.png"/>
</p>
<p>
- Within the Windows 10 Virtual Machine, download and install Wireshark Installer. 
</p>
<br /> 

<p> 
<img src="https://i.imgur.com/EqIANg3.png"/> 
</p> 
<p> 
- Open the Wireshark app and filter for "ICMP" traffic only. Open the command line within the Windows 10 Virtual Machine and ping the Linux Virtual Machine by using it's private IP address. Ping requests and replies will be seen within the Wireshark app. (Prompt: Ping 10.0.0.5)
</p> 
<br /> 

<p> 
<img src="https://i.imgur.com/IvtC1N1.png"/> 
</p> 
<p> 
- Observe ICMP traffic from within the Wireshark app by pinging a public website (wwww.google.com). (Prompt: ping wwww.google.com)
</p> 
<br /> 

<p> 
<img src="https://i.imgur.com/hfh8bM0.png"/) 
</p>
<p> 
- Initiate a non-stop ping from the Windows 10 Virtual Machine to the Linux Virtual Machine. (Prompt: ping 10.0.0.5 -t) Take note of the continous traffic within the Wireshark app. 
</p> 
<br /> 

<p> 
<img src="https://i.imgur.com/vtWQKO2.png"/) 
</p> 
<p> 
- Within the Azure Portal, open the Network Security Group of the Linux Virtual Machine. Within the Inbound security rules, add a new rule that denies all inbound ICMP traffic.
</p> 
<br /> 

<p> 
<img src="https://i.imgur.com/uvxt8kz.png"/) 
</p> 
<p> 
- Within the Windows 10 Virtual Machine via Windows Remote Desktop, take note of the "Request Timed Out" on both the command line and the Wireshark app. Since an inbound security rule of blocking all ICMP traffic was made, no ICMP traffic can be requested or sent from Linux Virtual Machine. 
</p> 
<br /> 

<p> 
<img src="https://i.imgur.com/Rud6Nk6.png"/) 
</p> 
<p> 
- Within the Azure Portal, open the Network Security Group of the Linux Virtual Machine. Within the Inbound security rules, change the ICMP rule to allow all inbound ICMP traffic. 
</p> 
<br /> 

<p> 
<img src="https://i.imgur.com/rruAnW1.png"/) 
</p> 
<p> 
- Within the Windows 10 Virtual Machine via Windows Remote Desktop, take note of the new changes on both the command line and the Wireshark app. Since the ICMP rule has now been set to allow all inbound ICMP traffic, all ICMP traffic is now able to be requested and sent by the Linux Virtual Machine. 
</p> 
<br /> 

<p> 
<img src="https://i.imgur.com/VnztOqL.png"/) 
</p> 
<p> 
- Within the Wireshark app on the Windows 10 Virtual Machine, filter for SSH traffic only. Within the command line on the Windows 10 Virtual Machine, use the SSH prompt to access the Linux Virtual Machine. (Prompt: ssh VM2@10.0.0.5). Observe the SSH traffic within the Wireshark app. 
</p> 
<br /> 

<p> 
<img src="https://i.imgur.com/R29XnIv.png"/) 
</p> 
<p> 
- Within the Wireshark app on the Windows 10 Virtual Machine, filter for DHCP traffic only. Within the command line on the Winows 10 Virtual Machine, attempt to issue the Windows 10 Virtual Machine a new IP address. (Prompt: ipconfig/renew). Observe the DHCP traffic within the Wireshark app and the new IP address issued by the DHCP prompt. 
</p> 
<br /> 

<p> 
<img src="https://i.imgur.com/WhYuh7X.png"/) 
</p> 
<p> 
- Within the Wireshark app on the Windows 10 Virtual Machine, filter for DNS traffic only. Within the command line on the Windows 10 Virtual Machine, use "nslookup" to observe what 'wwww.google.com' IP address is. (Prompt: nslookup wwww.google.com). Observe the DNS traffic within the Wireshark app. 
</p> 
<br /> 

<p> 
<img src="https://i.imgur.com/PRaiR8c.png"/) 
</p> 
<p> 
- Within the Wireshark app on the Windows 10 Virtual Machine, filter for RDP traffic (tcp.port==3389) only. Observe the continous RDP traffic within the Wireshark app.

