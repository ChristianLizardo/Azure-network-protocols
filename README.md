
# Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines

![image0](https://github.com/user-attachments/assets/73a50df9-4196-4d30-a942-2cad86322510)

In this tutorial, we analyze network traffic to and from Azure Virtual Machines using Wireshark and explore the functionality of Network Security Groups.

## Environments and Technologies Used 
- Microsoft Azure ( Virtual Machines/Computer )
- Remote Desktop 
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (Protocol Analyzer)

## Operating Systems Used
- Windows 10 (21H2)
- Ubuntu Server 20.04

## Observation Steps
- Create Resources
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

## Actions and Monitoring 

<h1 align="center"> Setup Virtual Machine </h1>

## Step 1 : Create a Resource Group

![image0-1](https://github.com/user-attachments/assets/56fecb7d-488e-45f4-ab54-ade2c3bcad0c)

## Step 2 : Create a Windows Virtual Machine 

When creating the VM, choose the previously created Resource Group and allow the system to generate a new Virtual Network (VNet) and Subnet. Ensure you select the password option under the Administrator Account section (not visible in the image).

![IMG_1377](https://github.com/user-attachments/assets/eb66c426-b83a-4fa9-b221-f59e0b652281)

## Step 3 : Create an Unbuntu VM 

When creating the VM, choose the previously created Resource Group and configure it to create a new Virtual Network (VNet) and Subnet. Ensure you select the password option under the Administrator Account section (not visible in the image).

Insert Image here 

## Step 4 : Observe Your Virtual Network within Network Watcher:

Insert Image Here


<h1 align="center"> ICMP Traffic Observation </h1>

Remote into your Windows 10 Virtual Machine, install Wireshark, open it and filter for ICMP traffic only. If you are using a Mac like me, you'll have to download Microsoft Remote Desktop from the app store:

Insert Image Here

Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM. Observe ping requests and replies within WireShark:

Insert Image Here

Insert Image Here

Attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark:

Insert Image Here

Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM:

Insert Image Here

Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic, while back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity:

Insert Image Here

Insert Image Here

Re-enable ICMP traffic for the Network Security Group in your Ubuntu VM and back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line ping activity (should start working again).Finally, stop the ping activity:

Insert Image Here

<h1 align="center"> SSH Observation Traffic </h1>

Back in Wireshark, filter for SSH traffic only and from your Windows 10 VM, “SSH into” your Ubuntu virtual machine (via its private IP address). Type commands (ls, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark.

Exit the SSH connection by typing ‘exit’ and pressing [return]:

Insert Image Here

<h1 align="center"> DHCP Observation Traffic </h1>

Back in Wireshark, filter for DHCP traffic only. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)

Observe the DHCP traffic appearing in WireShark:

Insert Image Here

<h1 align="center"> DNS Observation Traffic </h1>

Back in Wireshark, filter for DNS traffic only.

From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are and observe the DNS traffic being shown in WireShark:

Insert Image here 

<h1 align="center"> RDP Observation Traffic </h1>

Back in Wireshark, filter for RDP traffic only (tcp.port == 3389).

Oserve the immediate non-stop spam of traffic? Why is it non-stop spamming vs only showing traffic when a command is inputted?

The answer is because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted:

Insert Image Here

<h1 align="center"> Conclusion and Analysis </h1>

I hope this tutorial helped you learn a little bit about network security protocols and observe traffic between virtual machines. And although I ran this on a my MacBook Air, this can be easily done on a PC without having to download a remote desktop app since Windows provides that with it's software.

And now that we're done, DON'T FORGET TO CLEAN UP YOUR AZURE ENVIRONMENT so that you don't incur unnecessary charges.

Close your Remote Desktop connection, delete the Resource Group(s) created at the beginning of this tutorial, and verify Resource Group deletion.
