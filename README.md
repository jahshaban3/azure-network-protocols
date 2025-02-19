<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Virtual Machines
- Observe ICMP Traffic
- Configure a Firewall (Network Security Group)
- Observe SSH, DHCP, DNS, and RDP Traffic

<h2>Actions and Observations</h2>

<p>
<img src="https://i.gyazo.com/12ebc665421d75076e5bbc1df9931c94.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
<img src="https://i.gyazo.com/a4d021ef7b93f320efbc2029eb944210.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
<img src="https://i.gyazo.com/fa1201a085a12bd543df669a529ec57c.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
First, I created a resource group on Azure, followed by a Windows 10 virtual machine and a Linux virtual machine.
</p>
<br />

<p>
<img src="https://i.gyazo.com/e541b033f5b78dfdec6a297e9391b1fa.png" height="80%" width="80%" alt="Azure Network Protocolss"/>
</p>
<p>
<img src="https://i.gyazo.com/7520919cc7d472f3d218f08497ee083e.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
After verifying that both virtual machines were on the same network and ensuring everything was properly configured, I started the Windows virtual machine using Remote Desktop Connection. I then monitored all ICMP traffic between the two virtual machines using Wireshark and the ping command in Windows PowerShell. ICMP is utilized for network diagnostics and error reporting, and this traffic helps confirm connectivity and assess network performance.
</p>
<br />

<p>
<img src="https://i.gyazo.com/76d48a6ad8975922be2afffa5b5b92e6.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
<img src="https://i.gyazo.com/2c112cde1b8422bd2992ab3d70d99fa7.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
<img src="https://i.gyazo.com/f0659314f7206e6b99bce2d495a4c207.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
Next, I created an inbound security rule in the Linux virtual machine's network security group on Azure to block incoming ping traffic. I observed the results of this rule, which caused the ping requests to time out as expected. Additionally, Wireshark was unable to capture any replies, confirming that the rule was effective. After deleting the rule, traffic returned to normal.
</p>
<br />

<p>
<img src="https://i.gyazo.com/ba56235e299416dce8b662fd0d5f7857.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
I then monitored all SSH traffic by logging into the Linux virtual machine via SSH in Windows PowerShell and filtering it in Wireshark. SSH is a protocol that enables secure access and management of remote systems over a network, providing encrypted communication between the client and server to keep data confidential and protected from interception. During this session, I also performed several tasks in PowerShell, including creating a text file and running various commands.
</p>
<br />

<p>
<img src="https://i.gyazo.com/cd8f32b45df4e5590622637723aec201.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
<img src="https://i.gyazo.com/34704c69643a795a0c32af7072786376.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
Next, I monitored all DHCP traffic after creating a .bat file. Upon running the file in Windows PowerShell, I tracked the traffic in Wireshark, filtering it specifically for DHCP. The sequence shown in Wireshark displayed the standard DHCP lease cycle, where the client requests an IP address, receives an offer, confirms it, and later releases the IP address.
</p>
<br />

<p>
<img src="https://i.gyazo.com/8bdce5af630cfa5ba7f0c39a325a1583.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
I also monitored all DNS traffic in Wireshark after running the nslookup command in PowerShell. In this case, I queried the domain "disney.com." As observed, the nslookup query returned an IP address from a non-authoritative DNS server.
</p>
<br />

<p>
<img src="https://i.gyazo.com/d2880b9537f7d3a5e9935cd898f6b064.png" height="80%" width="80%" alt="Azure Network Protocols"/>
</p>
<p>
Finally, I monitored all RDP traffic and filtered it for TCP port 3389, the port used by RDP. I observed a continuous stream of traffic, as the RDP protocol consistently transmits live data between computers.
</p>
<br />
