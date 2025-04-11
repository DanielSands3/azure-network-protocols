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

- Create Virtual Machines in Azure
- Install Wireshark
- Observe ICMP traffic
- Configure a Firewall(Network Security Group)
- Observe SSH traffic
- Observe DHCP
- Observe DNS traffic
- Observe RDP traffic

<h2>Actions and Observations</h2>

<p>
<img width="238" alt="image" src="https://github.com/user-attachments/assets/0e8f278f-58ab-487c-8eb7-0ec230228669" />
</p>
<p>
Firstly we create a Resource Group in Microsoft Azure. Next we create a Windows 10 Virtual Machine, while creating the VM, allow it to create a new Virtual Network and Subnet. Next we create a Linux Virtual Machine, select the previously made Resource Group and Virtual Network.
</p>
<br />

<p>
<img width="94" alt="image" src="https://github.com/user-attachments/assets/68b32c2f-9f91-4c5b-b2c7-4837cca2beb7" />
</p>
<p>
Next we install Wireshark. Open Microsoft Edge and install Wireshark from the Wireshark site.
</p>
<br />

<p>
<img width="656" alt="image" src="https://github.com/user-attachments/assets/f1ce483d-3225-4988-9950-80ca73de24ce" />
</p>
<p>
Now using Remote Desktop, connect to your Windows 10 Virtual Machine. From within Wireshark, filter for ICMP traffic only. Retrieve the private IP address of the Linux VM and attempt to ping it from the Widnows 10 VM. Observe traffic in Wireshark.
</p>
<br />

<p>
<img width="266" alt="image" src="https://github.com/user-attachments/assets/5274c7d1-c703-4934-a0b9-db926d3b57a2" />
</p>
<p>
Now we open Network Security Group in the Linux VM and disable incoming (inbound) ICMP traffic. Back in the Windows 10 VM ping traffic should be blocked. Once the ICMP traffic rule is lifted, ping activity from the Windows 10 VM should start working. 
</p>
<br />

<p>
<img width="575" alt="image" src="https://github.com/user-attachments/assets/ba8931aa-8b97-44ad-a497-510d38564366" />
</p>
<p>
From Wireshark within the Windows 10 VM, start a packet capture and filter for SSH traffic only. From the Windows 10 VM, "SSH" into the Linux VM via its private IP address. Open Powershell and type ssh labuser@<private IP address>. Type command id and observe traffic in Wireshark.
</p>
<br />

<p>
<img width="707" alt="image" src="https://github.com/user-attachments/assets/30e6a8d9-3130-45b4-b75c-dd7d4f5f5978" />
</p>
<p>
Next, filter for DHCP traffic only in Wireshark. From the Windows 10 VM, attempt to issue your VM a new IP address from the command line using ipconfig /renew. Observe DHCP traffic in Wireshark. 
</p>
<br />

<p>
<img width="701" alt="image" src="https://github.com/user-attachments/assets/c3fc0aa2-d4a6-4c2c-be2c-adfb798c4a35" />
</p>
<p>
Back in Wireshark, filter for DNS traffic only and from your command line utilize nslookup to see what Disney.com's IP address is. Observe the DNS traffic in Wireshark.
</p>
<br />

<p>
<img width="494" alt="image" src="https://github.com/user-attachments/assets/6c5106b0-b680-4d9a-9343-aa017dca77cc" />
</p>
<p>
Finally we observe RDP traffic. In Wireshark filter for RDP traffic by typing tcp.port == 3389 and observe the non stop traffic, this is because the RDP protocol is constantly showing a livestream of data from one computer to another.  
</p>
<br />

