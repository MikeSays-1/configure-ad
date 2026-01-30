<p align="center">
<img width="600" alt="Microsoft Active Directory Logo" src="images/active-directory-seeklogo.png" />

</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This project demonstrates the deployment of a traditional on-premises Active Directory Domain Services (AD DS) environment using Microsoft Azure virtual machines. A Windows Server VM was configured and promoted to a domain controller with integrated DNS, and a Windows client VM was provisioned and joined to the new domain within the same virtual network. The lab successfully validates domain join, DNS resolution, and authentication using RDP and PowerShell, replicating a real-world enterprise Active Directory infrastructure scenario hosted in the cloud.<br />


<!--
<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)
-->

<h2>Environments and Technologies Used</h2>

<img src="https://skillicons.dev/icons?i=azure,windows,powershell" />

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

<img src="images/Configure Azure and AD flow chart.gif" width="400" alt="Deployment Diagram">


- Step 1. Create VM Client 1
- Step 2. Create VM Server Domain Controller
- Step 3. Install Active Directory

> [!IMPORTANT]
> Each step includes written instructions followed by a corresponding screenshot.
<br>Expand the **See screenshots** section to view the images.

<h2>Deployment and Configuration</h2> 

<b>1. CREATE RESOURCE GROUP. </b>
<p>Log into Azure Portal, and in the search bar type "Resource Groups", select Resource Groups and press "+ Create" to create a resouce group. Name your resource group "rg-ad-lab" and select "Review + Create", finally "Create". </p>

<details><summary>See screenshots</summary>
<img src="images/Step 1a.png" width="48%" > <img src="images/Step 1b.png" width="48%" >
</details>


<b>2. CREATE VIRTUAL NETWORK. </b>
<p>In the search bar, type "Virtual Networks", select Virtual Networks and press "+ Create" to start creation of your Virtual Network. Select the resource group we just made and name your virtual network "vnet-ad-lab", select "Review + Create" and finally "Create". </p>

<details><summary>See screenshots</summary>

<img src="images/Step 2.JPG" width="60%">
</details> 


<b>3. CREATE VM DOMAIN CONTROLLER </b>
<p>In the search bar, type "VM", select Virtual Machines and press "+ Create" and select "Virtual Machines" to start creation of your Virtual Machine. Select the "rg-ad-lab" as the resource group, name your vm "vm-dc-1". For Image, select "Windows Server 2022, Datacenter: Azure Edition - x64 Gen2" For Size, select any with 2 VCPUs and at least 16 GB Ram. Set your username and password in the Admin Account section. Near the bottom, select "Next : Disk >" continue on to "Next : Networking >". </p>

<details><summary>See screenshots</summary>

<img src="images/Step 3.JPG" width="60%">
</details> 

<p>In the Nerwoking screen, for Virtual Network, select our created vnet from Step 2. "vnet-ad-lab". for Subnet, select default. We're finished with Networking settings, select "Review + Create" and finally "Create". </p>

<details><summary>See screenshots</summary>

<img src="images/Step 3 Networking.JPG" width="60%">
</details>

<p>Now we will set the NIC Private IP Address to Static. Once your Domain Controller VM is deployed, view the VM by typing "vm" in the search bar > select "Virtual Machines" > select "vm-dc-1". On the left pane, find "Network" > "Network Settings". Here, select your "Network Interface" under "Essentials" > On the left pane, in drop down "Settings" select "IP Configurations" > Select "ipconfig1" and set Private IP Allocation settings to Static. And now "Save". Go back to your listed VMs, and note/copy the Public IP of the Domain Controller. </p>

<details><summary>See screenshots</summary>

<img src="images/Step 3c.JPG" width="60%">
</details>

<p>On your local computer (Windows or macOS), open a Remote Desktop client and connect to the VM using public IP address, you'll be prompted to enter your credentials you created when creating this VM. Next prompt, select yes, and your Domain Controller will now boot. Once booted, open "Windows Defender Firewall with Advanced Security", go to "Windows Defender Firewall Properties", and for Firewall State: Select "Off" for Domain, Public and Private Profiles and select Apply. (We will be testing connectivity.) Leave your RDP connection on, we will return in Step 5. </p>

<details><summary>See screenshots</summary>

<img src="images/Step 3d.PNG" width="60%">
</details>

<b>4. CREATE VM CLIENT </b>
<p>In the search bar, type "VM", select Virtual Machines and press "+ Create" and select "Virtual Machines" to start creation of your Virtual Machine. Select the "rg-ad-lab" as the resource group, name your vm "vm-client-1". For Image, select "Windows 10 Enterprise, version 22H2 - x64 Gen 2" For Size, select any with 2 VCPUs and at least 16 GB Ram. Set your username and password in the Admin Account section. Near the bottom, mark the checkbox in the Licensing section and select "Next : Disk >" continue on to "Next : Networking >". </p>

<details><summary>See screenshots</summary>

<img src="images/step 4a.JPG" width="60%">
</details> 

<p>In the Nerwoking screen, for Virtual Network, select our created vnet from Step 2. "vnet-ad-lab". for Subnet, select default. We're finished with Networking, now select "Review + Create" and finally "Create". Once deployed, back out to your list of VMs, and select "vm-dc-1" > Select "Network Settings" on the left pane. Copy/Note the Private IP Addess of vm-dc-1. Back out to list of VMs, select vm-client-1 > On the left pane, find "Network" > "Network Settings". Here, select your "Network Interface" under "Essentials" > On the left pane, in drop down "Settings" select "DNS Servers". Under DNS Servers, select "custom", here in the blank field paste the "vm-dc-1" Private IP Address, select "Save" near the top. 

<details><summary>See screenshots</summary>

<img src="images/Step 4b DNS.JPG" width="60%">
</details> 

Restart "vm-client-1" within the Azure Portal by going to your vm list. Mark the checkbox for "vm-client-1" and select "Restart" near the top.While on this screen, copy/note "vm-client'1" Public IP Address, we'll need it to Login. </p>

<details><summary>See screenshots</summary>

<img src="images/Step 4c restart client 1.JPG" width="60%">
</details> 

<p>On your local computer (Windows or macOS), open another instance of  Remote Desktop client and connect to the VM Client 1 using public IP address, you'll be prompted to enter your credentials you created when creating this VM. Next prompt, select yes, and your VM Client 1 will now boot. Open PowerShell and attempt to ping your Domain Controller's Private IP Address. Ensure the ping the succeded, run ipconfig /all. The output for DNS Settings should now show "vm-dc-1"'s Private IP Address. </p>

<details><summary>See screenshots</summary>

<img src="images/Step 4d.PNG" width="50%">
</details>

<b>5. INSTALL ACTIVE DIRECTORY </b>
<p>Return to our Domain Controller from Step 3. View or Open "Server Manager > Dashboard". Select option 2. Add roles and features. Select "Next" 3 times, until we arrive at "Server Roles". Here select "Active Directory Domain Services". Select "Next" 3 times again. On the Confirmation screen, mark the checkbox "Restart the destination server automatically..." , and select "Install". </p>

<details><summary>See screenshots</summary>

<img src="images/Step 5a.PNG" width="60%">
</details>

<p>Once feature is finsihed installing, select "Close". On your Server Manager Dashboard, select the notifications icon. </p>

<details><summary>See screenshots</summary>

<img src="images/Step 5b.PNG" width="60%">
</details> <br>

<p>From here, select "Promote this server to a domain controller". In the Domain Configuration screen, select "Add a new forest" and in Root domain name field, type "mydomain.com". (you may name the forest anything) Select "Next", in the Domain Controller Options, you will need to set the DSRM Password here. Select "Next", be sure to unmark the DNS Delegation checkbox here, select 4 more times from here, and lastly "Install". The VM will install the new forest and will sign out automatically. </p>

<details><summary>See screenshots</summary>

<img src="images/Step 5c.PNG" width="60%">
</details>

<p>Once signed out, RDP will restart for the VM, select "More Options" and clear the username field, and enter mydomain.com\&lt;yourcreatedcredentials&gt; and password. </p>

<details><summary>See screenshots</summary>

<img src="images/Step 5d.JPG" width="40%">
</details>

<p>Once logged back into the Domain Controller, we can review the Server Manager Dashboard and verify that the Active Directory Domain Services and DNS roles are installed and running! </p>

<details><summary>See screenshots</summary>

<img src="images/Step 5e.PNG" width="60%">
</details>
