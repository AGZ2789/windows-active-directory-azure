# Active Directory Administration in Microsoft Azure

This project demonstrates the deployment and administration of an Active Directory domain environment using Microsoft Azure Virtual Machines. A Windows Server virtual machine was configured as a Domain Controller, while a Windows client was configured for domain-based authentication and centralized administration.

The project focused on Active Directory Domain Services, DNS configuration, user and group administration, domain authentication, Remote Desktop access, and PowerShell-based user provisioning.

<br>

## Environments and Technologies Used

- Microsoft Azure
- Windows Server 2022
- Windows 10
- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)
- PowerShell
- DNS
- Remote Desktop Protocol (RDP)

<br>

## Active Directory Environment

Two Azure Virtual Machines were used within the same virtual network:

- **DC-1** — Windows Server 2022 Domain Controller
- **Client-1** — Windows 10 domain client

The systems were configured on the same private network to support communication between the Windows client and server.

<img width="1616" height="1281" alt="Snipaste_2024-05-18_17-40-15" src="https://github.com/user-attachments/assets/858a0023-ea36-43ec-afac-2f072adbbef8" />

<br><br>

## Connectivity Verification

Connectivity between Client-1 and DC-1 was tested using ICMP.

Initial ping attempts from Client-1 to DC-1 timed out. After the appropriate Windows Firewall ICMP rule was enabled on DC-1, Client-1 successfully received replies from **10.0.0.4**.

<img width="2772" height="1391" alt="Snipaste_2024-05-18_18-27-51" src="https://github.com/user-attachments/assets/9faebada-4a33-4504-bc3a-d9f13a5f38b2" />

<br><br>

## Active Directory Domain Services Deployment

Active Directory Domain Services was installed on DC-1.

After the AD DS role was installed, Server Manager provided the option to promote the server to a Domain Controller.

<img width="1718" height="1360" alt="Snipaste_2024-05-18_18-53-40" src="https://github.com/user-attachments/assets/5b7faf03-618d-47f9-bd93-accf68bfed8a" />

This established the foundation for centralized authentication and administration within the domain environment.

<br><br>

## Organizational Units, Users, and Groups

Active Directory Users and Computers was used to organize domain resources.

Separate Organizational Units were created for administrative and employee accounts.

<img width="1117" height="322" alt="Snipaste_2024-05-18_19-19-21" src="https://github.com/user-attachments/assets/ee6808d5-5e7d-48c6-99b1-907ce89c9192" />

An administrative account was also assigned to the **Domain Admins** security group.

<img width="1718" height="1391" alt="Snipaste_2024-05-18_21-01-05" src="https://github.com/user-attachments/assets/8ae87d29-0ffe-44ea-beeb-7a7bbf09f02f" />

<br><br>

## Client DNS and Domain Configuration

DC-1 used the private IP address **10.0.0.4**.

Client-1 was configured to use **10.0.0.4** as its DNS server so that it could locate Active Directory services through the Domain Controller.

<img width="1678" height="1232" alt="Snipaste_2024-05-18_21-43-40" src="https://github.com/user-attachments/assets/1e743b4d-f3da-4ca6-b7b3-67d988853389" />

<br><br>

## Joining Client-1 to the Domain

Client-1 was configured to join the **mydomain.com** Active Directory domain.

The successful domain join was confirmed by Windows.

<img width="298" height="149" alt="Snipaste_2024-05-18_21-54-44" src="https://github.com/user-attachments/assets/9f9049a3-4471-4186-8cb3-e14cf98b7e5a" />

<br><br>

## Domain Authentication

Domain credentials were used to connect to Client-1 through Remote Desktop.

<img width="1526" height="1231" alt="Snipaste_2024-05-18_21-59-45" src="https://github.com/user-attachments/assets/fe8ff88f-838e-4746-b1cb-d395c9eac59a" />

This demonstrated domain-based authentication on the Windows client.

<br><br>

## User Provisioning with PowerShell

An instructor-provided PowerShell script was used to automate the creation of multiple Active Directory user accounts rather than creating each account manually.

The script generates usernames and uses `New-ADUser` to provision the accounts in the `_EMPLOYEES` Organizational Unit.

**PowerShell Script:** [Generate-Names-Create-Users.ps1](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

<img width="1718" height="1360" alt="Snipaste_2024-05-18_22-32-17" src="https://github.com/user-attachments/assets/4b3e54f0-4e0a-4d4a-b9a7-2805877ea68a" />

The generated accounts were then verified in Active Directory Users and Computers.

This demonstrated how PowerShell can automate repetitive identity-management tasks and improve consistency when provisioning users.

<br>

## Challenges and Troubleshooting

One of the main configuration issues involved communication between Client-1 and the Domain Controller.

Initial ping attempts timed out until the appropriate ICMP firewall rule was enabled on DC-1.

The project also reinforced the importance of configuring the client to use the Domain Controller for DNS and distinguishing between local accounts, standard domain users, and privileged administrative accounts.

<br>

## Key Takeaways

- Deployed a Windows Server system for Active Directory in Microsoft Azure
- Configured private networking and DNS for domain communication
- Installed Active Directory Domain Services
- Created Organizational Units and managed domain users and groups
- Configured a Windows workstation to join the Active Directory domain
- Verified successful domain membership
- Verified domain-based authentication through Remote Desktop
- Automated bulk user creation with PowerShell
- Troubleshot client-to-domain-controller connectivity and Windows Firewall behavior
