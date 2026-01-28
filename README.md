<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Domain Controller in Azure
- Setup Client-1 in Azure
- Install Active Directory

<h2>Deployment and Configuration Steps</h2>

<p>
<b>1. CREATE RESOURCE GROUP. </b> 
<br />Log into Azure Portal, and in the search bar type "Resource Groups", select Resource Groups and press "+ Create" to create a resouce group. Name your resource group "rg-ad-lab" and select "Review + Create", finally "Create".
<br />
</p>

<details>
<summary><b>See screenshots</b></summary>
<p>
  <img src="https://github.com/user-attachments/assets/f3d3aa89-cc91-4b4b-aca9-9935a52704d6" width="48%" />
  <img src="https://github.com/user-attachments/assets/0ba247ce-8e26-472a-aeda-0a1985f1ab6e" width="48%" />
</p>
</details>

<br />

<p><b>2. CREATE VIRTUAL NETWORK. </b> 
<br />In the search bar, type "Virtual Networks", select Virtual Networks and press "+ Create" to start creation of your Virtual Network. Select the resource group we just made and name your virtual network "vnet-ad-lab", select "Review + Create" and finally "Create".
</p>

<details>
<summary><b>See screenshots</b></summary>
<p>
<img width="1124" height="917" alt="image" src="https://github.com/user-attachments/assets/334aad79-f8c4-4397-8ad0-2dc2176f0359" />
</p>
</details>  

<br />



<p><b>3. CREATE VM DOMAIN CONTROLLER</b> <br />
In the search bar, type "VM", select Virtual Machines and press "+ Create" and select "Virtual Machines" to start creation of your Virtual Machine. Select the "rg-ad-lab" as the resource group, name your vm "vm-dc-1".  For Image, select "Windows Server 2022, Datacenter: Azure Edition - x64 Gen2" For Size, select any with 2 VCPUs and at least 16 GB Ram. Set your username and password in the Admin Account section. Near the bottom, select "Next : Disk >" continue on to "Next : Networking >".
</p>

<details>
<summary><b>See screenshots</b></summary>
<p>
<img width="1035" height="871" alt="image" src="https://github.com/user-attachments/assets/580cc793-f5d1-430b-ae61-cdc3f62327a9" />
</p>
</details>  
<p>In the Nerwoking screen, for Virtual Network, select our created vnet from Step 2. "vnet-ad-lab".  for Subnet, select default. We're finished with Networking settings, select "Review + Create" and finally "Create". 

<details>
<summary><b>See screenshots</b></summary>
<img width="1044" height="882" alt="image" src="https://github.com/user-attachments/assets/93e8e7c1-6186-4197-816c-10d1f5bd3b17" />
</details>
  
<br />Now we will set the NIC Private IP Address to Static. Once your Domain Controller VM is deployed, view the VM by typing "vm" in the search bar > select "Virtual Machines" > select "vm-dc-1".  On the left pane, find "Network" > "Network Settings". Here, select your "Network Interface" under "Essentials", Near the bottom select "Configure Your IPs" > Select "ipconfig1" and set Private IP Allocation settings to Static. And now "Save". Go back to your listed VMs, and note/copy the Public IP of the Domain Controller.
<br />

<img width="457" height="314" alt="image" src="https://github.com/user-attachments/assets/1fca2cfd-3d12-4034-97fa-71a051ec2c92" />

On your local computer (Windows or macOS), open a Remote Desktop client and connect to the VM using public IP address, you'll be prompted to enter your credentials you created when creating this VM. Next prompt, select yes, and your Domain Controller will now boot. Once booted, open "Windows Defender Firewall with Advanced Security", go to "Windows Defender Firewall Properties", and for Firewall State: Select "Off" for Domain, Public and Private Profiles and select Apply. (We will be testing connectivity.) Leave your RDP connection on, we will return in Step 5.
</p>

<p><b>4. CREATE VM CLIENT 1. </b> <br />
In the search bar, type "VM", select Virtual Machines and press "+ Create" and select "Virtual Machines" to start creation of your Virtual Machine. Select the "rg-ad-lab" as the resource group, name your vm "vm-client-1".  For Image, select "Windows 10 Enterprise, version 22H2 - x64 Gen 2" For Size, select any with 2 VCPUs and at least 16 GB Ram. Set your username and password in the Admin Account section. Near the bottom, mark the checkbox in the Licensing section and select "Next : Disk >" continue on to "Next : Networking >".
</p>
<details>
<summary><b>See screenshots</b></summary>
<p>
<img width="1032" height="902" alt="image" src="https://github.com/user-attachments/assets/1e7e49ce-9120-47d0-96ec-1cce40f3ad46" />
</p>
</details>  
<br />
<p>In the Nerwoking screen, for Virtual Network, select our created vnet from Step 2. "vnet-ad-lab".  for Subnet, select default. We're finished with Networking, now select "Review + Create" and finally "Create". 

<br /><br />

Once deployed, back out to your list of VMs, and select "vm-dc-1" > Select "Network Settings" on the left pane. Copy/Note the Private IP Addess of vm-dc-1. Back out to list of VMs, select vm-client-1 > Select "Network Settings" on the left pane > Select your Network Interface Card

</p>




<br />
<p><b>5. INSTALL ACTIVE DIRECTORY </b> <br />
Login to vm-dc-1
</p>

<details>
<summary><b>See screenshots</b></summary>
<p>
Image Here
</p>
</details>  

<br />
