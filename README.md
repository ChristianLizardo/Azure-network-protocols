
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

## Step 3 : Create an Ubuntu VM 

When creating the VM, choose the previously created Resource Group and configure it to create a new Virtual Network (VNet) and Subnet. Ensure you select the password option under the Administrator Account section (not visible in the image).

![IMG_1378](https://github.com/user-attachments/assets/911fd260-b301-4f59-84bb-5892057be0c5)

## Step 4 : Observe Your Virtual Network within Network Watcher:

![IMG_1379](https://github.com/user-attachments/assets/ee9aa9de-3966-48d4-a8c2-64f4e2a52272)

<h1 align="center"> ICMP Traffic Observation </h1>

Remote into your Windows 10 Virtual Machine, install Wireshark, open it and filter for ICMP traffic only. If you are using a Mac like me, you'll have to download Microsoft Remote Desktop from the app store:

![IMG_1397](https://github.com/user-attachments/assets/839e2436-8d0b-4cce-9f61-30fa87ce2f0c)

Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM. Observe ping requests and replies within WireShark:

![IMG_1382](https://github.com/user-attachments/assets/cf6da31d-cf9a-45dd-8190-db56efd9a012)

![IMG_1383](https://github.com/user-attachments/assets/48bcf645-049d-4b5f-a1c3-939a12b724b1)

Attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark:

![IMG_1384](https://github.com/user-attachments/assets/61f2c75c-3296-4a17-826a-9b6f08f402a5)

Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM:

![IMG_1385](https://github.com/user-attachments/assets/9805c87b-9e88-41a7-adaf-ec74864c0ce4)

Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic, while back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity:

![IMG_1386](https://github.com/user-attachments/assets/1d047b04-5b67-4967-ad15-604bfe6fba99)

![IMG_1387](https://github.com/user-attachments/assets/2e0bd9e4-01a0-4d93-8343-e068239630ba)

Re-enable ICMP traffic for the Network Security Group in your Ubuntu VM and back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line ping activity (should start working again).Finally, stop the ping activity:

![IMG_1389](https://github.com/user-attachments/assets/5b3bce75-6da5-46c1-ab62-1f7c2ddbd162)

<h1 align="center"> SSH Observation Traffic </h1>

Back in Wireshark, filter for SSH traffic only and from your Windows 10 VM, “SSH into” your Ubuntu virtual machine (via its private IP address). Type commands (ls, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark.

Exit the SSH connection by typing ‘exit’ and pressing [return]:

![IMG_1391](https://github.com/user-attachments/assets/f1dc7f1f-97a4-465a-a497-9679c93fd0a7)

<h1 align="center"> DHCP Observation Traffic </h1>

Back in Wireshark, filter for DHCP traffic only. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)

Observe the DHCP traffic appearing in WireShark:

![IMG_1392](https://github.com/user-attachments/assets/858ec473-c3ce-4f67-8685-93643524c416)

<h1 align="center"> DNS Observation Traffic </h1>

Back in Wireshark, filter for DNS traffic only.

From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are and observe the DNS traffic being shown in WireShark:

![IMG_1394](https://github.com/user-attachments/assets/cf0e4150-897c-4c65-b400-cb5050e771f3)

<h1 align="center"> RDP Observation Traffic </h1>

Back in Wireshark, filter for RDP traffic only (tcp.port == 3389).

Oserve the immediate non-stop spam of traffic? Why is it non-stop spamming vs only showing traffic when a command is inputted?

The answer is because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted:

![IMG_1395](https://github.com/user-attachments/assets/eed61ae2-912d-48c8-9b5e-c98ae4f3bd77)

<h1 align="center"> Conclusion and Analysis </h1>

I hope this tutorial helped you learn a little bit about network security protocols and observe traffic between virtual machines. And although I ran this on a my MacBook Air, this can be easily done on a PC without having to download a remote desktop app since Windows provides that with it's software.

And now that we're done, DON'T FORGET TO CLEAN UP YOUR AZURE ENVIRONMENT so that you don't incur unnecessary charges.

Close your Remote Desktop connection, delete the Resource Group(s) created at the beginning of this tutorial, and verify Resource Group deletion.
