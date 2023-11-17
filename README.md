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
- Create a Windows 10 Client VM, "Client-1," in the same Resource Group and Vnet.

### Ensure Connectivity:
- Log in to Client-1 using Remote Desktop and ping DC-1's private IP address.
- Enable ICMPv4 on DC-1's local Windows Firewall.
- Verify successful ping from Client-1.

### Install Active Directory:
- Log in to DC-1 and install Active Directory Domain Services.
- Promote DC-1 as a DC, setting up a new forest (e.g., mydomain.com).
- Log in as "mydomain.com\labuser" after restart.

### Create AD User Accounts:
- In ADUC, create an OU called "_EMPLOYEES" and another named "_ADMINS."
- Create "Jane Doe" as "jane_admin" and add her to "Domain Admins."
- Log in as "mydomain.com\jane_admin" for admin tasks.

### Join Client-1 to Domain:
- Set Client-1's DNS settings to DC's Private IP address.
- Restart Client-1 from Azure Portal.
- Log in to Client-1 as the local admin (labuser) and join it to the domain.
- Verify Client-1 in ADUC under "Computers" on the root of the domain.
- Create an optional "_CLIENTS" OU and move Client-1 there.

### Configure Remote Desktop:
- Log into Client-1 as "mydomain.com\jane_admin" and open system properties.
- Enable Remote Desktop access for "domain users."
- Create Additional Users:

### Log in to DC-1 as "jane_admin."
- Run the provided PowerShell script to create additional users.
- Observe created accounts in ADUC in the appropriate OU.
- Attempt to log into Client-1 with one of the new accounts.

