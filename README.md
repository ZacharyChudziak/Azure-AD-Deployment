<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This guide demonstrates the implementation of on-premises Active Directory within Azure Virtual Machines, as well as showcasing setting up new users to connect to the client PC.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Creating the Virtual Machines</h2>
<p>
  Create a new Virtual Machine in azure choosing Windows Server 2022. For the purpose of this example I used 2 Virtual CPUs, and 16 gig memory as seen below. Make sure to create a resource group at time of making the Virtual Machine for this purpose mine is named "AD-Practical".
</p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/6480663b-7c38-4711-b238-e43d79c46164"
 height="80%" width="80%"/> </p>
 <p>
  Next create a new Virtual Machine but this time choosing Windows 10. Make sure to choose the resource group that was created in the previous step, except now with this Virtual Machine go to network settings and make sure the new VM is connected to the same Virtual Network (VNET) as the Server VM.
</p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/73e77eeb-2ced-46a4-baf3-01c6b17d52ca"
 height="80%" width="80%"/> </p>
 <p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/0ae50245-cbaa-4b39-b643-2b37ffc69939"
 height="80%" width="80%"/> </p>
  <p>
  Next we are going to change the Windows Server IP address from Dynamic to Static so that the IP never changes and the client can always stay connected. For this we are going to go to the Virtual Machine in Azure choose the Windows Server VM and go to networking settings. Click the Network Interface and then in the left side menu choose IP Configurations. Here is where we will set the Server to Static.
</p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/d69c8e38-b53a-4ce5-8e84-b8c3502b8a7a"
 height="80%" width="80%"/> </p>



<h2>Installing Active Directory on the Windows Server VM</h2>
<p>
  Now we are going to install Active Directory, In Windows Server 2022 click "Manage" then choose "Add Roles and Features". Continue through the Wizard with default settings until we reach "Server Roles", Select "Active Directory Domain Services" and continue with default settings and install.
</p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/1e0f9f2e-06a5-4eda-a74c-c002574765b8"
 height="80%" width="80%"/> </p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/42804719-5df4-4b06-a189-c71f09bfc883"
 height="80%" width="80%"/> </p>
<p>
  Next we need to finish promoting the Windows Server VM to a "Domain Controller". In Server Manager a notification will have popped up where the "Flag" is click that and continue finishing the post deployment.
</p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/7d826f54-07f2-4d9d-9047-dedc634dd902"
 height="80%" width="80%"/> </p>
 <p>
  Go through the Wizard and Configure the Domain in a "NEW FOREST", choose your domain name it can be anything, for this example I used "CCPractical.com". Continue through with default settings and install.
</p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/4d4aaf25-d573-4629-871e-3c95fb295de3"
 height="80%" width="80%"/> </p>
 
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
