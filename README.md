<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines deploying on-premises Active Directory in Azure VMs. Using Windows Server 2022 and Windows 10 (21H2), it covers resource setup, creating a Domain Controller VM, and configuring a Windows 10 Client VM. The guide progresses through Active Directory installation, user account creation, and domain joining. Leveraging Azure services, Remote Desktop, and PowerShell, the tutorial offers a concise yet comprehensive deployment process. For visual guidance, refer to the YouTube video titled "How to Deploy on-premises Active Directory within Azure Compute".<br />


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

### Resources Configuration:

- Set up resources in Azure.
- Create a Domain Controller VM, "DC-1," using Windows Server 2022.
- Note the Resource Group and Virtual Network (Vnet) details.
- Set DC-1's NIC Private IP address to be static.


![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/df45aaf7-2c84-4a3f-962f-10ec8099771b)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/7c0bcb86-5389-43ad-9bc5-1dfc7b1ca67f)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/75676160-5ba6-46e5-8b00-ed2d2b3d3578)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/7fd7779b-613b-4c50-a8e3-17fc260ce6a7)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/5fb47c66-4145-4bbf-91bf-37b376e82795)

- Create a Windows 10 Client VM, "Client-1," in the same Resource Group and Vnet.

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/0512b8b0-b9ab-4320-bfef-753c803ed376)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/ec263d9b-717b-4c6a-a66b-d7c95895f20c)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/1fa3d72d-f650-4d27-8212-d7600f6b1533)

### Ensure Connectivity:
- Log in to Client-1 using Remote Desktop and ping DC-1's private IP address.
- Enable ICMPv4 on DC-1's local Windows Firewall.
- Verify successful ping from Client-1.

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/739def6d-7640-4e81-a4df-981cd3e51093)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/b8fd87be-8d19-424d-9348-14e8f2d49a99)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/57d2b640-b9a0-42e5-b5c9-5d8fd41b6620)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/4a3b1c69-e7dc-4012-b5c2-639e8f08755f)


### Install Active Directory:
- Log in to DC-1 and install Active Directory Domain Services.
- Promote DC-1 as a DC, setting up a new forest (e.g., mydomain.com).
- Log in as "mydomain.com\labuser" after restart.

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/32af4702-923d-4f73-9b94-b4d996fc7e09)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/ce81b8d2-dd64-45b3-89a8-55fe714eb770)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/272f2867-b79c-4948-a145-ae777006c1d8)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/9a770fd0-8ddc-44dd-9701-f89334b553d6)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/b5e1823d-a86b-487e-9993-4c18bfd9b320)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/90b44eab-aaae-4a3b-aaa7-cf55d1032ef6)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/6d27e2d0-43fc-436a-a0cb-95a8d50b8de8)

### Create AD User Accounts:
- In ADUC, create an OU called "_EMPLOYEES" and another named "_ADMINS."
- Create "Jane Doe" as "jane_admin" and add her to "Domain Admins."
- Log in as "mydomain.com\jane_admin" for admin tasks.

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/aa0be3e2-4a9a-485a-841a-1bb46020aab1)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/8082838e-35a9-482a-905e-1ec8a0831524)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/f3ef762d-a185-47fb-8f4d-71afb368cd1f)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/58836d3a-d85d-41bf-9097-d7378b2d6108)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/b5f9d72b-98e2-49ff-9595-7bdb07b338da)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/3b87d655-3489-48e2-8328-88745afe2071)

### Join Client-1 to Domain:
- Set Client-1's DNS settings to DC's Private IP address.
- Restart Client-1 from Azure Portal.
- Log in to Client-1 as the local admin (labuser) and join it to the domain.
- Verify Client-1 in ADUC under "Computers" on the root of the domain.
- Create an optional "_CLIENTS" OU and move Client-1 there.

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/0d41a2c4-3e44-4a4d-96e2-dbe8c9b359f9)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/bf9d0014-ce10-4e46-b501-fc5327b00ed6)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/44e794f2-f333-4aaa-bb5a-ca6df15b7250)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/20c85022-ceea-4425-ab98-1c70913dbcc5)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/c9e3e482-139b-4c99-9b06-c79881e5ee43)

### Configure Remote Desktop:
- Log into Client-1 as "mydomain.com\jane_admin" and open system properties.
- Enable Remote Desktop access for "domain users."
- Create Additional Users:

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/3a99600e-eb6f-4213-9215-d3f59d183f01)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/5b93849d-56af-457d-97a0-d6517ac853e7)

### Log in to DC-1 as "jane_admin."
- Run the provided [PowerShell script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) to create additional users.
- Observe created accounts in ADUC in the appropriate OU.
- Attempt to log into Client-1 with one of the new accounts.

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/3ba156ab-c3bb-45fa-bf08-35c2c10bbec0)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/4b7ccd82-73b4-446a-8ae8-3f55cc2cef53)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/b102de67-05bc-4252-810c-291a6226c010)

![image](https://github.com/CaseyHrt/configure-ad/assets/146404028/9c61b77a-f871-4c60-ada4-047767f93291)

## Conclusion
Understanding the ticket lifecycle in osTicket is essential for effective ticket management and resolution. By following the guidance provided in this repository, users can streamline their support processes and ensure timely resolution of issues. This concludes the lab, providing a comprehensive overview of ticket management in osTicket.


