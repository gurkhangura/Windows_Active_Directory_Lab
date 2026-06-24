# Windows_Active_Directory_Lab
Windows Server 2025 Active Directory homelab built with Hyper-V to practice helpdesk and junior system administration tasks including AD DS, DNS, users, groups, OUs, Group Policy, file shares, and domain-joined Windows clients.

## Skills Demonstrated

- Hyper-V virtual machine deployment
- Windows Server 2025 administration
- Active Directory Domain Services
- DNS configuration
- Domain controller setup
- Internal virtual networking
- Static IP addressing
- Organizational Unit management
- Active Directory user creation
- Security group creation
- Windows 11 domain joining
- Domain user authentication
- Basic network troubleshooting
- Technical documentation

## Lab Environment

| Machine | Operating System | Role |
|---|---|---|
| DC01 | Windows Server 2025 Evaluation | Domain Controller, DNS Server |
| CLIENT01 | Windows 11 Enterprise Evaluation | Domain-Joined Workstation |

## Network Configuration

| Item | Configuration |
|---|---|
| Virtualization Platform | Hyper-V |
| Virtual Switch | AD-Lab-Internal |
| Switch Type | Internal |
| Domain | khanguralab.local |
| DC01 IP Address | 192.168.50.10 |
| CLIENT01 IP Address | 192.168.50.20 |
| DNS Server | 192.168.50.10 |

## Hyper-V Virtual Machines

![Hyper-V VMs Running](screenshots/01_HyperV_VMs_Running)

I created two virtual machines in Hyper-V to simulate a small Windows business environment. DC01 was configured as the domain controller and DNS server. CLIENT01 was used as a Windows 11 workstation to test domain joining and domain user login.

## Internal Virtual Switch

![Virtual Switch Internal Network](screenshots/02_Virtual_Switch_Internal_Network.png)

I created an internal Hyper-V switch named `AD-Lab-Internal` so the virtual machines could communicate with each other on an isolated lab network.

## Domain Controller Server Roles

![DC01 Server Manager Roles](screenshots/03_DC01_Server_Manager_Roles.png)

I installed Active Directory Domain Services and DNS on DC01. These roles allow DC01 to manage domain authentication and internal name resolution for `khanguralab.local`.

## DC01 Static IP Configuration

![DC01 Static IP](screenshots/04_DC01_Static_IP.png)

I assigned DC01 a static IP address of `192.168.50.10`. Since DC01 is the domain controller and DNS server, it needs a consistent IP address for client machines to find it.

## Active Directory OU Structure

![AD OU Structure](screenshots/05_AD_OU_Structure.png)

I created a custom Active Directory OU structure to organize users, computers, groups, servers, and disabled accounts.

OU structure:

- khanguralab.local
  - KhanguraLab
    - Computers
    - Disabled Users
    - Groups
    - Servers
    - Users
      - Finance
      - HR
      - IT
      - Sales

## Department Users

![AD Department Users](screenshots/06_AD_Department_Users.png)

I created sample users and placed them into department-based OUs.

| User | Department |
|---|---|
| Peyton Manning | Finance |
| Bruce Wayne | HR |
| James Bond | IT |
| Master Chief | Sales |

## Security Groups

![AD Security Groups](screenshots/07_AD_Security_Groups.png)

I created department-based security groups and file share access groups to simulate role-based access control.

| Group | Purpose |
|---|---|
| Finance_Users | Finance department users |
| HR_Users | HR department users |
| IT_Admins | IT administrative users |
| Sales_Users | Sales department users |
| FileShare_Finance_Read | Read access to Finance share |
| FileShare_Finance_Modify | Modify access to Finance share |
| FileShare_HR_Read | Read access to HR share |
| FileShare_HR_Modify | Modify access to HR share |
| FileShare_IT_Read | Read access to IT share |
| FileShare_IT_Modify | Modify access to IT share |
| FileShare_Sales_Read | Read access to Sales share |
| FileShare_Sales_Modify | Modify access to Sales share |

## User Group Membership

![User Group Membership](screenshots/08_User_Group_Membership.png)

I assigned the Sales user to the `Sales_Users` group and the `FileShare_Sales_Modify` group. This demonstrates how access can be controlled through Active Directory group membership instead of assigning permissions directly to individual users.

## Domain-Joined Computer Object

![CLIENT01 Computer Object](screenshots/09_CLIENT01_Computer_Object.png)

After joining CLIENT01 to the domain, the computer object appeared in Active Directory. This confirms that the Windows 11 workstation successfully joined `khanguralab.local`.

## CLIENT01 Domain Join Verification

![CLIENT01 Domain Joined](screenshots/10_CLIENT01_Domain_Joined.png)

I verified the domain join from CLIENT01 by checking the system information page. The full device name shows `CLIENT01.khanguralab.local`.

## Domain User Authentication

![Domain User Whoami](screenshots/11_Domain_User_Whoami.png)

I logged into CLIENT01 using a domain account and ran the `whoami` command to verify the active user session.

Command used:

`whoami`

Example result:

`khanguralab\mchief`

This confirms that domain authentication is working.

## CLIENT01 to DC01 Connectivity Test

![CLIENT01 Ping DC01](screenshots/12_CLIENT01_Ping_DC01.png)

I tested network connectivity from CLIENT01 to DC01 using the `ping` command.

Command used:

`ping 192.168.50.10`

The successful replies confirm that CLIENT01 can communicate with the domain controller over the internal virtual network.

## Troubleshooting Commands Used

During the lab, I used these commands to verify network and domain functionality:

- `ipconfig`
- `ping 192.168.50.10`
- `nslookup khanguralab.local`
- `whoami`

These commands helped confirm IP configuration, domain controller connectivity, DNS resolution, and domain user authentication.

## Summary

This lab demonstrates a basic Windows Active Directory environment built from scratch. I configured a domain controller, DNS, an internal Hyper-V network, department-based OUs, Active Directory users, security groups, and a Windows 11 domain-joined client.

This project helped me practice real help desk and junior system administrator skills, including user management, domain troubleshooting, network testing, and documentation.

## Next Steps

Planned improvements for this lab include:

- Configure Group Policy Objects
- Create mapped network drives
- Configure department file shares
- Apply NTFS permissions using security groups
- Simulate password reset and account lockout tickets
- Automate user creation with PowerShell
- Add a dedicated file server named FS01
- Document additional help desk troubleshooting scenarios
