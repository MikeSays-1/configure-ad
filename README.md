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

<p>
<b>2. CREATE VIRTUAL NETWORK. </b> 
<br />In the search bar, type "Virtual Networks", select Virtual Networks and press "+ Create" to start creation of your Virtual Network. Select the resource group we just made and name your virtual network "vnet-ad-lab", select "Review + Create" and finally "Create".
</p>
> **Screenshot:** Creating a Resource Group in Azure
<p>
<img width="1124" height="917" alt="image" src="https://github.com/user-attachments/assets/334aad79-f8c4-4397-8ad0-2dc2176f0359" />

</p>

<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
