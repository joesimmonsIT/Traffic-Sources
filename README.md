<p align="center">
<img src="https://i.imgur.com/ZfjorFh.png"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic sources to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)
- Windows Powershell

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04
  

<h2>High-Level Steps</h2>

- Wireshark Basics
- Perpectual Traffic
- Network Security Groups
- SSH Traffic
- DHCP Traffic
- DNS Traffic
- RDP Traffic

<h2>Wireshark Basics</h2>

<p>
<img src="https://i.imgur.com/2vhraCH.png"/>
</p>
<p>
<a href="https://github.com/joesimmonsIT/Wireshark/">Download Wireshark</a> <br /> <br />
Click the above link for the tutorial to Download Wireshark prior to proceeding with this tutorial. <br /> <br />
We can notice the non-stop traffic in the picture above.<br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/nPWt41b.png"/>
</p>
<p>
The current traffic is ran primarily off of "icmp" traffic. <br /> <br />
Go to the search bar and type "icmp". <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/9rtm3k8.png"/>
</p>
<p>
Press "Enter". <br /> <br />
Notice all the traffic stops. <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/BeZNUBQ.png"/>
</p>
<p>
Go back to Azure: "Portal.Azure.com".
</p>
<br />

<p>
<img src="https://i.imgur.com/6WFXxMc.png"/>
</p>
<p>
In the search bar type "Virtual Machines". <br /> <br />
Select "Virtual Machines" from the search results. <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/fWucLIP.png"/>
</p>
<p>
Select "VM2".
</p>
<br />

<p>
<img src="https://i.imgur.com/ti1erkt.png"/>
</p>
<p>
Collapse the "Networking" selection. <br /> <br />
Select "Network settings". <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/4yZh2R9.png"/>
</p>
<p>
Select "Network interface."
</p>
<br />

<p>
<img src="https://i.imgur.com/EGQsE0N.png"/>
</p>
<p>
Copy the Private IP Address for VM2.
</p>
<br />

<p>
<img src="https://i.imgur.com/ZOEhbOm.png"/>
</p>
<p>
Return back to Remote Desktop Connection. <br /> <br />
Go to the Windows Pane (located at the bottom of the computer screen). <br /> <br />
In the search bar type "Powershell". <br /> <br />
Select "Windows Powershell ISE". <br /> <br />
Click the search result or "Press Enter" to open the application. <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/igh0nn1.png"/>
</p>
<p>
Type "ping, (press the space bar), and Paste the IP Address for VM2 (10.0.0.5)", and Press "Enter". <br /> <br />
Notice the 4 traffic source results. <br /> <br />
</p>
<br />

<h2>Perpectual Ping </h2>
<p>
<img src="https://i.imgur.com/RVPRj11.png"/>
</p>
<p>
Go back to Wireshark and in the search bar type "icmp" and Press "Enter", to clear all the traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/9NG41JI.png"/>
</p>
<p>
Select the "green icon" above the search bar to clear all the saving of previous traffic. <br /> <br />
Select "Continue without saving". <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/eONFv4W.png"/>
</p>
<p>
Return to Powershell. <br /> <br />
Type "ping, (press the space bar), -, t" and Press "Enter"; this will send perpectual traffic to VM2. <br /> <br />
</p>
<br />

<h2>Network Security Groups </h2>
<p>
<img src="https://i.imgur.com/TNkuZHP.png"/>
</p>
<p>
Go to the Azure Portal: "Portal.Azure.com"
</p>
<br />

<p>
<img src="https://i.imgur.com/V4dmOG6.png"/>
</p>
<p>
In the search bar type "network security groups". <br /> <br />
Select "Network security groups" from the search results. <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/UEsGnI2.png"/>
</p>
<p>
Select "VM2-nsg".
</p>
<br />

<p>
<img src="https://i.imgur.com/5Ev3r9A.png"/>
</p>
<p>
Take notice of the commands of the left side of the Home Page for the VM2 Network Security Group.
</p>
<br />

<p>
<img src="https://i.imgur.com/zbGWwdF.png"/>
</p>
<p>
Select "Settings". <br /> <br />
Collapse the Settings tab. <br /> <br />
Select "Inbound security rules". <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/bIaV0E6.png"/>
</p>
<p>
Select "+ Add" to add a new inbound security rule to the VM2 Network Security Group.
</p>
<br />

<p>
<img src="https://i.imgur.com/jFhLqIg.png"/>
</p>
<p>
Keep the current settings. <br /> <br />
Go to Protocol and make sure "ICMP" is selected; a blue circle should appear next to the option. <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/2Pa0gne.png"/>
</p>
<p>
Action: Change the option to "Deny". <br /> <br />
Priority: Change to "200". <br /> <br />
Name: Change to "DenyICMPPingFromAnywhere". <br /> <br />
Select "Add". <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/uumtg4Z.png"/>
</p>
<p>
Go back to Powershell. <br /> <br />
Notice the new inbound security rule has taken affect and now all "ICMP" traffic has been blocked. <br /> <br />
Displaying the following result "Request timed out" repeatedly since we are participating in perpectual traffic to VM2. <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/j0gp4Us.png"/>
</p>
<p>
Go back to the VM2-nsg inbound security rules. <br /> <br />
Select "DenyICMPPing......". <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/JvKoQvv.png"/>
</p>
<p>
Change Action to "Allow". <br /> <br />
Click "Save". <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/i4pnkro.png"/>
</p>
<p>
Inbound Security Rule has been updated. <br /> <br />
ICMP Traffic is now flowing back perpectually. <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/n6DkVyM.png"/>
</p>
<p>
Type "Ctrl + C" to stop perpectual traffic.
</p>
<br />

<h2>SSH Traffic </h2>
<p>
<img src="https://i.imgur.com/Cy5tdQg.png"/>
</p>
<p>
Go back to Wireshark and in the search bar type "ssh".
</p>
<br />

<p>
<img src="https://i.imgur.com/YP9BFKf.png"/>
</p>
<p>
Click the "green icon" above the search bar.
</p>
<br />

<p>
<img src="https://i.imgur.com/mvS1wb6.png"/>
</p>
<p>
Select "Continue without Saving".
</p>
<br />

<p>
<img src="https://i.imgur.com/VLno8JC.png"/>
</p>
<p>
Press "Enter", to display "ssh" traffic.
</p>
<br />

<h2>DHCP Traffic </h2>
<p>
<img src="https://i.imgur.com/0ROUtEe.png"/>
</p>
<p>
Type "dhcp" in the search bar.
</p>
<br />

<p>
<img src="https://i.imgur.com/WvJcRdP.png"/>
</p>
<p>
Return back to Powershell. <br /> <br />
Type "ipconfig (press the space bar), /renew" and Press "Enter". <br /> <br />
Note the Private IP Address and the Subnet for VM1. <br /> <br />
</p>
<br />

<p>
<img src="https://i.imgur.com/5i34FuL.png"/>
</p>
<p>
Return back to Wireshark. <br /> <br />
Press "Enter" to display the "dhcp" traffic. <br /> <br />
</p>
<br />

<h2>DNS Traffic </h2>
<p>
<img src="https://i.imgur.com/5dWGOso.png"/>
</p>
<p>
Type "dns" in the search bar.
</p>
<br />

<p>
<img src="https://i.imgur.com/OQLEjph.png"/>
</p>
<p>
Press "Enter", to display "dns" traffic.
</p>
<br />

<h2> RDP Traffic </h2>
<p>
<img src="https://i.imgur.com/r23g8yC.png"/>
</p>
<p>
Type "tcp.port==3389" and Press "Enter" to display the RDP Traffic. <br /> <br />
The RDP Port number is 3389. <br /> <br />
Congratulations you have completed this tutorial! <br /> <br />
</p>
<br />

