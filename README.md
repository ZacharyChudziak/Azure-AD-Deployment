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
  Go through the Wizard and Configure the Domain in a "NEW FOREST", choose your domain name it can be anything, for this example I used "CCPractical.com". Continue through with default settings and install. The Server will need to restart after completion. After restarting you will need to use the new domain created to log back in through Remote Desktop "RDP" in this case it would be CCPractical.com\labuser.
</p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/4d4aaf25-d573-4629-871e-3c95fb295de3"
 height="80%" width="80%"/> </p>
 <p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/5ed1c2e4-72bd-4775-84b1-9f5e70d3f6dd"
 height="80%" width="80%"/> </p>
 <h2>Creating an Admin User to connect to the Client PC</h2>
 <p>
  Open up Active Directory Users and Computers by clikcing start menu and searching for it. After opening up ADUC click on the domain that was created previously in this case it will be "CCPractical.com". From there we are going to create a new organizational unit right click and create new and choose "Organizational Unit" and name it "_ACTIVEADMINS".
</p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/313b2eec-c5f1-4018-9c5a-2e85d83e1fd3"
 height="80%" width="80%"/> </p>
 <p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/be7e43a8-077a-405c-ae8f-2f3148160040"
 height="80%" width="80%"/> </p>
 <p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/4e337a36-a4f0-4320-8b69-cfc60649d8be"
 height="80%" width="80%"/> </p>
 
 <h2>Setting up the Client PC on the Domain</h2>
  <p>
  Next we need to setup the Client PC to be on the Domain of the Server VM. In Azure, go to "Virtual Machines", Click on the "Client VM" and go to "Networking Settings". Click on the "Network Interface" and in the left side menu choose "DNS Servers" click Custom and using the "Windows Server" private IP add it. Restart the VM so it can obtain its new "DNS".
</p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/65544521-721c-438b-909e-5a2c6e3c1917"
 height="80%" width="80%"/> </p>
   <p>
  Next we need to add the Client PC to the "Domain". For this right click the start menu and choose "System". In the "System" page click "Rename this PC Advanced", next choose "Rename this Computer or change its Domain". Next add it to the "Domain" we created "CCPractical.com". The computer will need to restart and we will need to reconnect using "CCPractical.com\username" however in the next steps we are going to create an "Admin User" for this case.
</p>
<p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/d269516f-4a1d-4db8-8252-f7cf8fc3ab88"
 height="80%" width="80%"/> </p>
 <p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/df8dfeb0-2031-47da-a935-e70d4e13aae0"
height="80%" width="80%"/> </p>
 <p align="center">
  <img src="https://github.com/ZacharyChudziak/Azure-AD-Deployment/assets/154548436/88b60d11-0a88-4968-8847-9f849a547c21"
height="80%" width="80%"/> </p>
<h2>Creating Users and an Admin User to connect to the Client VM</h2>

<br />
