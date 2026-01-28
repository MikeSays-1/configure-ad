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
<br />
Log into Azure Portal, and in the search bar type "Resource Groups", select Resource Groups and press "+ Create" to create a resouce group. Name your resource group "rg-ad-lab" and select "Review + Create", finally "Create".
</p>

<details>
<summary><i>See screenshots</i></summary>
<p>
  <img src="https://github.com/user-attachments/assets/f3d3aa89-cc91-4b4b-aca9-9935a52704d6" width="48%" />
  <img src="https://github.com/user-attachments/assets/0ba247ce-8e26-472a-aeda-0a1985f1ab6e" width="48%" />
</p>
</details>
<p><b>2. CREATE VIRTUAL NETWORK. </b> 
<br />In the search bar, type "Virtual Networks", select Virtual Networks and press "+ Create" to start creation of your Virtual Network. Select the resource group we just made and name your virtual network "vnet-ad-lab", select "Review + Create" and finally "Create".
</p>

<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="1124" height="917" alt="image" src="https://github.com/user-attachments/assets/334aad79-f8c4-4397-8ad0-2dc2176f0359" />
</p>
</details>  
<p><b>3. CREATE VM DOMAIN CONTROLLER</b> <br />
In the search bar, type "VM", select Virtual Machines and press "+ Create" and select "Virtual Machines" to start creation of your Virtual Machine. Select the "rg-ad-lab" as the resource group, name your vm "vm-dc-1".  For Image, select "Windows Server 2022, Datacenter: Azure Edition - x64 Gen2" For Size, select any with 2 VCPUs and at least 16 GB Ram. Set your username and password in the Admin Account section. Near the bottom, select "Next : Disk >" continue on to "Next : Networking >".
</p>

<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="1035" height="871" alt="image" src="https://github.com/user-attachments/assets/580cc793-f5d1-430b-ae61-cdc3f62327a9" />
</p>
</details>  
<p>In the Nerwoking screen, for Virtual Network, select our created vnet from Step 2. "vnet-ad-lab".  for Subnet, select default. We're finished with Networking settings, select "Review + Create" and finally "Create". 
</p>
<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="1044" height="882" alt="image" src="https://github.com/user-attachments/assets/93e8e7c1-6186-4197-816c-10d1f5bd3b17" />
</details>
</p>
  
<p>
Now we will set the NIC Private IP Address to Static. Once your Domain Controller VM is deployed, view the VM by typing "vm" in the search bar > select "Virtual Machines" > select "vm-dc-1".  On the left pane, find "Network" > "Network Settings". Here, select your "Network Interface" under "Essentials" > On the left pane, in drop down "Settings" select "IP Configurations" > Select "ipconfig1" and set Private IP Allocation settings to Static. And now "Save". Go back to your listed VMs, and note/copy the Public IP of the Domain Controller.
</p>
<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="457" height="314" alt="image" src="https://github.com/user-attachments/assets/1fca2cfd-3d12-4034-97fa-71a051ec2c92" />
</details>
</p>
<p>
On your local computer (Windows or macOS), open a Remote Desktop client and connect to the VM using public IP address, you'll be prompted to enter your credentials you created when creating this VM. Next prompt, select yes, and your Domain Controller will now boot. Once booted, open "Windows Defender Firewall with Advanced Security", go to "Windows Defender Firewall Properties", and for Firewall State: Select "Off" for Domain, Public and Private Profiles and select Apply. (We will be testing connectivity.) Leave your RDP connection on, we will return in Step 5.
</p>

<p><b>4. CREATE VM CLIENT 1. </b> <br />
In the search bar, type "VM", select Virtual Machines and press "+ Create" and select "Virtual Machines" to start creation of your Virtual Machine. Select the "rg-ad-lab" as the resource group, name your vm "vm-client-1".  For Image, select "Windows 10 Enterprise, version 22H2 - x64 Gen 2" For Size, select any with 2 VCPUs and at least 16 GB Ram. Set your username and password in the Admin Account section. Near the bottom, mark the checkbox in the Licensing section and select "Next : Disk >" continue on to "Next : Networking >".
</p>
<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="1032" height="902" alt="image" src="https://github.com/user-attachments/assets/1e7e49ce-9120-47d0-96ec-1cce40f3ad46" />
</p>
</details>  

<p>
In the Nerwoking screen, for Virtual Network, select our created vnet from Step 2. "vnet-ad-lab".  for Subnet, select default. We're finished with Networking, now select "Review + Create" and finally "Create". 
</p>
<p>
Once deployed, back out to your list of VMs, and select "vm-dc-1" > Select "Network Settings" on the left pane. Copy/Note the Private IP Addess of vm-dc-1. Back out to list of VMs, select vm-client-1 > On the left pane, find "Network" > "Network Settings". Here, select your "Network Interface" under "Essentials" > On the left pane, in drop down "Settings" select "DNS Servers".  Under DNS Servers, select "custom", here in the blank field paste the "vm-dc-1" Private IP Address, select "Save" near the top.
</p>

<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="1028" height="855" alt="image" src="https://github.com/user-attachments/assets/fe93bdb0-a714-4340-bad2-851b9e89cc13" />
</p>
</details>  

<p>
Restart "vm-client-1" within the Azure Portal by going to your vm list.  Mark the checkbox for "vm-client-1" and select "Restart" near the top.While on this screen, copy/note "vm-client'1" Public IP Address, we'll need it to Login. 
</p>
<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="1871" height="611" alt="image" src="https://github.com/user-attachments/assets/af75ecec-8450-42a2-8a2e-536b5e7bc0d8" />
</p>
</details> 
<p>
On your local computer (Windows or macOS), open a Remote Desktop client and connect to the VM using public IP address, you'll be prompted to enter your credentials you created when creating this VM. Next prompt, select yes, and your VM Client 1 will now boot. Open PowerShell and attempt to ping your Domain Controller's Private IP Address. Ensure the ping the succeded, run ipconfig /all. The output for DNS Settings should now show "vm-dc-1"'s Private IP Address.
</p>
<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="620" height="681" alt="image" src="https://github.com/user-attachments/assets/b6248308-69b8-4524-a9c3-685712314250" />
</p>
</details> 
 
<p><b>5. INSTALL ACTIVE DIRECTORY</b> <br />
Return to our Domain Controller from Step 3. View or Open "Server Manager > Dashboard". Select option 2. Add roles and features. Select "Next" 3 times, until we arrive at "Server Roles". Here select "Active Directory Domain Services". Select "Next" 3 times again. On the Confirmation screen, mark the checkbox "Restart the destination server automatically..." , and select "Install"</p>
<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="1036" height="742" alt="image" src="https://github.com/user-attachments/assets/5a75b044-f685-4b0d-8889-407f8d570002" />
</p>
</details>  
<p>
Once feature is finsihed installing, select "Close". On your Server Manager Dashboard, select  the notifications icon.
</p>
<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="1424" height="750" alt="image" src="https://github.com/user-attachments/assets/c2c3b961-6440-4854-9c44-99cd3dc3b9f4" />
</p>
</details>  
<p>
From here, select "Promote this server to a domain controller". In the Domain Configuration screen, select "Add a new forest" and in Root domain name field, type "mydomain.com".  (you may name the forest anything) Select "Next", in the Domain Controller Options, you will need to set the DSRM Password here. Select "Next" 5 more times from here, and lastly "Install". The VM will install the new forest and will sign out automatically.
</p>
<details>
<summary><i>See screenshots</i></summary>
<p>
<img width="1409" height="729" alt="image" src="https://github.com/user-attachments/assets/bfd708ee-f4e3-407a-9495-39a7ae186fdc" />
</p>
</details>  
<p>Once signed out, RDP will restart for the VM, select "More Options" and clear the username field, and enter mydomain.com\"yourcreatedcredentials" and password.</p>
<details>
<summary><i>See screenshots</i></summary><p>
<img width="406" height="489" alt="image" src="https://github.com/user-attachments/assets/fe139151-9e63-4422-a50d-592864edfb07" />
</p>
</details> 
<p>
Once logged back into the Domain Controller, we can review the Server Manager Dashboard and verify that the Active Directory Domain Services and DNS roles are installed and running! 
</p>
<details>
<summary><i>See screenshots</i></summary><p>
<img width="1416" height="742" alt="image" src="https://github.com/user-attachments/assets/729d55f7-7a97-43b6-b9c6-115d690927b3" />
</p>
</details> 
<br />
