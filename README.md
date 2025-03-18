# Virtual-Private-Networks-VPNs

<p align="center" height="10%" width="10%">


$<img width="250" alt="image" src="https://github.com/user-attachments/assets/050bfbe1-5971-4f4f-8ffe-971cd04f2b3b" alt="Azure logo"/>
</p>


<h1>Azure Computing and Networking</h1>
Here we will discuss and show what VPNs are, how to set them up, and how to use them. 
Used to securely link 2 computers or networks across an unsecured network like the internet by sending encapsulated and encrypted data
<br />


<h2>Video Demonstration</h2>

$- ### [YouTube: How To Create A Virtual Machine And Use It-Coming Soon](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
  - Virtual Machines (Windows)
  - Azure Network Security Groups (Firewall Resource)
- Remote Desktop
- Powershell
- Proton VPN (free trial account)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

$<h2>List of Prerequisites</h2>

- Azure Account
- Each Section below builds off the previous sections above it

<h2>A. Creation Steps</h2>

 1. What is a VPN? How is a VPN used to work outside of the office?
     <p>
       
     </p>
<img src="https://github.com/user-attachments/assets/e697933a-f6c5-405e-94ca-89ba4da9bd5f" height="80%" width="80%" alt="VPN Tunnel"/>
</p>
<p>
<p>  
1. A VPN can be used to securely link 2 computers or networks across an insecure network like the Internet by sending encapsulated and encrypted data. VPNs are not completely anonymous, but you have an additional layer of privacy. VPNs change the location from which the IP address of your device seems to be. VPNs are often used to connect to resources at work from home. The VPN creates a secure tunnel through to the corporate network, and then regular traffic can flow through it as if you were at the corporate office using their network.
<p>

  2. How does a VPN work for consumer use?
<img src="https://github.com/user-attachments/assets/be35c22f-998b-4604-a3c7-fa3af88589f5" height="80%" width="80%" alt="public VPNs"/>
</p>
<p>
2. When you browse the Internet when you are connected to a VPN to located somewhere where you are not, it appears as if you were browsing from where the VPN server is. This may make it more difficult for advertisers to target you specifically based on where you are.
</p>
<br />

<p>
  3. Compare locale and IP addresses from your computer, an azure virtual machine (VM), and from a ProtonVPN on your VM by connecting to www.whatismyipaddress.com on each of them
<p>
$<img src="https://github.com/user-attachments/assets/6af09202-acbc-4203-8a85-de063185c7ff" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. 
</p>
<br />

<h2>B. ICMP traffic between  the two Virtual Machines Observation Steps</h2>

<p>
  1. Use Remote Desktop to connect to the Windows VM
<p>
1. Mac users must install "Microsoft Remote Desktop" whereas Windows users need to search "Remote Desktop Connection" in their computer search bar. In Azure, go to "Virtual Machine", and select the Windows virtual machine we made in a previous step. From the information listed, find and copy the public IP address. Paste this IP address into the Remote desktop connection for "computer" or "pc name." If it then shows your personal name, select "more choices," "use a different account," and use the username and password that you used to create the VMs. Decline all the setup offers it makes to you. Congrats! You're on the VM you made! 
</p>
2. Install Wireshark, a protocol analyzer aka a packet sniffer, to visualize network traffic
<p>
$  <img src="https://github.com/user-attachments/assets/228f4e4e-6996-4216-a9fc-cc0c903b78c7" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
2. On the Windows VM, open a browser tab, search "www.wireshark.org", select "download," then click the x64 installer. Once installed, open the file. Select "yes" and "noted" through the installation process, making sure the "install Npcap" is selected when the page presents during the installation; a USB cap is not needed at this time. select "agree" without selecting any of the 3 boxes. select "install," "next," and "finish." Close the web browser and then in the Windows VM Windows search bar, search and select "Wireshark." 
</p>
In Wireshark, select "ethernet," and then click the shark fin icon below "file" in the upper left. These constantly changing numbers are all of the network traffic happening on the backend of the VM, more specifically, the numbers are different packets going to and from the VM.

<p>
  3. Filter for ICMP traffic. The picture below shows ping executed using ICMP, confirming a connection between the 2 VMs created. 

$  <img src="https://github.com/user-attachments/assets/6025a801-4619-4587-b9f8-c2e2838efc09" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <p>
    <p>
3. Recall the ping uses ICMP to test connectivity between devices. Since there is constant traffic, filtering for ICMP makes it easier to see this traffic in Wireshark. So in the search bar above the running numbers, above the column headers, next to the bookmark icon, where it says "Apply a display filter," type "icmp" and hit enter so that we only see ICMP (ping) traffic.
</p>
Next retrieve the private IP address of the Linux VM from Azure and ping it from the Windows 10 VM PowerShell by typing ping followed by the Linux VM private IP address. Notice in Wireshark that there are both requests and replies.
<p>
  <p>
    
  </p>
4. Looking Deeper
</p>
<br />


$  <img src="https://github.com/user-attachments/assets/6e4ab849-0958-4139-9ccd-aebec5887f78" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
4. Expanding "Ethernet II" shows source and destination MAC addresses, layer 2 addressing in the OSI Model. The VM appears to be uniquely sequential, seeing as the manufacturer cannot burn a MAC address onto software. 
<p>
Expanding "Internet Protocol" shows source and destination private IP addresses, the network layer 3 in the OSI model
</p>
Expanding "Internet Control Message Protocol," ICMP, can even show you the payload of the ping, including the data sent and how many bytes it was.
</p>
5. In summary, use the Windows public IP to sign into Remote Desktop> Use Wireshark to filter ICMP> Retrieve Linux private IP address> Open Windows VM PowerShell then type ping followed by the Linux VM private IP> If Wireshark shows requests and replies, the two devices are connected.
<br />
<p>
</p>

</p>
<h2>C. Configure a Firewall (Network Security Group) Steps</h2>
<p>
  
</p>
  1. Use the Linux VM's Network Security Group to initiate Firewall Configuration and a Windows PowerShell non-stop ping to watch it in action
$<img src="https://github.com/user-attachments/assets/5c4f3a0b-97ad-43fc-a503-e97dba283447" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
1. To witness firewall blocking activity, restart capture without saving on your Windows VM Wireshark by clicking the green fin under "edit." Then in the Windows VM PowerShell, initiate non-stop ping by typing "ping <private IP address of the Linux VM> -t" and hit enter. In Azure, locate the Ubuntu VM. Then on the left select "Networking" followed by "Network Settings" underneath that. In the information generated to the right, find "Network Security Group" and select the blue text beneath it "linux-vm-nsg"
</p>
</p>
    2. Make ICMP blocking rule
  <p>
$<img src="https://github.com/user-attachments/assets/b5e1ee94-d49c-428c-93d8-33da9924f7e4" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
2. Click "settings" on the left, and "inbound security rules" underneath it. Now at the top left, select "+Add" and a Side panel will open on the right. Make the following changes in there: change port ranges to any by putting an asterisk (*) in there, (ICMP does not use a port). Change protocol to ICMPv4. Change Action to "Deny" so that the Network Security Group, aka the FireWall, will drop this ICMP traffic. Change priority to 290 so that it is above all rules, including SSH ranked at 300. Lastly, click "Add" at the bottom.

</p>
</p>
  3. Watch changes from reply and request in Wireshark to requests only. powershell requests time out because the Linux VM network security group blocked traffic
  <p>
<p>
$<img src="https://github.com/user-attachments/assets/c4567250-ee2f-4a1e-9c77-35949a0083f8" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. Ping still works until the Linux VM ignores and does not reply to the traffic as we have set up in the previous step. To undo this ICMP blocking rule in Azure, simply hit the trash barrel emoji to the far right of the rule. Then in the Windows VM PowerShell, hit enter a couple of times and replies resume. You should also see ping traffic restart with both requests and replies on Wireshark. You may type ctrl + C twice to stop ping activity in PowerShell.
</p>
</p>


</p>
<h2>D. SSH, DHCP, DNS, RDP Traffic Observation Steps</h2>
<p>
</p>
  1. SSH uses TCP Port 22 for a secure connection between computers. Connect to the Linux VM via SSH & type in its command lines
  <p>
$<img src="https://github.com/user-attachments/assets/68c16097-7186-4e91-928a-3a442557fdf2" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
1. In Wireshark, clear filters using the x at the far right side of the filter box. Now filter for "SSH" as we have before for ICMP or filter via tcp.port==22. In the Windows VM PowerShell type ssh <username>@<privateIPaddressofLinux> then type "yes" then type the password (which will not appear but is being registered) and select enter. Notice the PowerShell Prompt now changes to the Linux computer <username>@Linux-vm . Since SSH is encrypted, selecting the data will only show you scrambled keystrokes and filler, unlike telnet, which is clear text. Selecting Transmission control will show you the source and distribution ports, one of which will be random and the other will be port 22, SSH, and it is flipped when items are sent back.
</p>
</p> 2. SSH commands in Linux VM Continued
  <p>
$<img src="https://github.com/user-attachments/assets/84e2808d-ce62-4255-8054-ef345d651f64" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
2. $touch file.text is a command you may try which creates a file. $ls shows this file was created. $pwd stands for print working directory. type "exit" to exit the Linux VM.
</p>
    3. DHCP Traffic Observation work-around using a file
</p>
$<img src="https://github.com/user-attachments/assets/3875084e-11be-4fa0-842f-74e1547a740c" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
3. In Wireshark, use the green fin to clear without saving, and filter for DHCP or udp.port==67_udp.port==68. You may notice only two traffic notifications in Wireshark. However, we can add steps to observe the whole DHCP protocol (The client broadcasts for an IP, DHCP makes the client an offer, the Client Requests from DHCP, and DHCP acknowledges the client). First open Notepad in the Windows VM, name it dhcp.bat, inside the note type "ipconfig /release" hit enter to start a new line and type "ipconfig /renew" then save this file for example in documents. In the Windows VM Powershell, change the directory to documents or wherever you saved this file by using the command cd for change directory and the location you stored it. Then type ls to list what is inside this directory and make sure your file is there. Then run the file by typing .\dhcp.bat or .\thefilenameyouchose. This will automatically run the code in our note, first releasing all IP addresses, temporarily terminate the network connection too, but then auto renew an IP address, and then all parts of the DHCP protocol can be viewed in Wireshark. Note 255 255 255 255 is the broadcast.
</p>
<p>
  
</p>
  4. Observe DNS Traffic 
<p>
  
</p>
4. Clear filters in Wireshark with he x at the right of the filter bar, and clear without saving using the green fin. Now in Wireshark filter for dns or udp.port==53||tcp.port==53 meanwhile in the Powershell, use nslookup. For example, type nslookup disney.com to look for the IP address for Disney.com. You will see DNS traffic appear in Wireshark and Disney's IP address appear in the PowerShell.
<p>
  
</p> 
  5. RDP Traffic Observation
<p>
  
</p>
5. To filter for remote desktop traffic,  use Wireshark filtered by tcp.port==3389. Since we are using RDP to do this work, you will see constant traffic appear in Wireshark. Also, unlike SSH traffic which sends traffic for keystrokes, RDP sends traffic for photographs constantly, so that the whole desktop screen is conveyed, leading to spam/lots of traffic.
<p>
  
</p> 
  6. Important Final step -  Close the Virtual machines
<p>
  
</p>
6. Go to the top of the VM and click the "x" to exit. And go to Azure and delete the VM's or better yet, delete the whole resource group. When you delete the resource group, you will need to copy and paste or rewrite the resource group name for deletion confirmation, and select the box at the bottom saying "apply force delete for Virtual Machines" then delete the resource group. Refresh the resource group page in Azure to make sure the resource group is no longer there.
