# Virtual-Private-Networks-VPNs

<p align="center" height="10%" width="10%">


<img width="250" alt="image" src="https://github.com/user-attachments/assets/f4c0951f-ab2d-4d5d-9ed3-1b4e4589ed39" alt="VPN Schematic"/>
</p>


<h1>Azure Computing and Networking</h1>
Here we will discuss and show what VPNs are, how to set them up, and how to use them. 
Used to securely link 2 computers or networks across an unsecured network like the internet by sending encapsulated and encrypted data
<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Create A Virtual Machine And Use It-Coming Soon](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
  - Virtual Machines (Windows)
- Remote Desktop
- Proton VPN (free trial account)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Account
- [Azure Compute and Networking](https://github.com/victoriadeery/azure-computing-and-networking) for detailed steps on how to create a VM on Azure

<h2>A. Steps</h2>

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
2. When you browse the Internet when you are connected to a VPN located somewhere where you are not, it appears as if you were browsing from where the VPN server is. This may make it more difficult for advertisers to target you specifically based on where you are.
</p>
<br />

<p>
  3. Compare locale and IP addresses from your computer, an Azure virtual machine (VM), and a ProtonVPN on your VM by connecting to www.whatismyipaddress.com on each of them.
<p>
<img src="https://github.com/user-attachments/assets/ea4a810c-73a4-4119-8986-1e62cd4b8055" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. First create the VM. For detailed steps on how to create a VM on Azure go to my repository: [Azure Compute and Networking](https://github.com/victoriadeery/azure-computing-and-networking). You'll see your computer, the VM, and the VPN display different IP addresses and regions. I have kept track of the info from www.whatismyipaddress.com on each of them on a notepad (displayed).
</p>
<br />
Note: you can log into a VPN on your computer itself. Using the VM was to emphasize that a VM is also creating a tunnel and can change your IP address in a more expensive yet more functional way as it is a whole other desktop. You have options.
