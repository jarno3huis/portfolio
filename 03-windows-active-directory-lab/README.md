# 03 - Windows active directory lab

## Goal

Build a small Windows domain environment for a fictional company.

## Topics

- Windows Server
- Active Directory Domain Services
- DNS
- Users and groups
- Organizational Units
- Group Policy
- Permissions
- Windows administration

## Evidence to add

- [ ] Architecture diagram
- [ ] Domain / OU design
- [ ] User and group strategy
- [ ] GPO documentation
- [ ] DNS configuration
- [ ] Screenshots

## What I learned


# Windows Server & Active Directory Lab

## Overview

As part of my IT infrastructure home lab, I deployed Windows Server 2025 in VirtualBox and built the first part of a small enterprise-style Windows environment.

The goal is to develop practical skills in Windows Server administration, networking, identity management, Group Policy and troubleshooting.

## Environment

- Domain Controller: `DC01`
- Operating system: Windows Server 2025 Standard Evaluation
- Domain: `lab.home`
- Virtualization: VirtualBox
- Server interface: Server Core
- Remote administration: PowerShell Remoting / WinRM

## Network Architecture

The server uses separate virtual networks for different purposes:

```text
                         Internet
                            |
                           NAT
                            |
                         DC01
                    Windows Server 2025
                    /        |        \
                   /         |         \
                NAT        IT-LAB    Host-Only
                            |         |
                     192.168.50.x   192.168.56.x
                                      |
                                    Host PC
```

**NAT** provides outbound internet access.

**IT-LAB** is used for communication between lab VMs:

```text
Network: 192.168.50.0/24
DC01:    192.168.50.10
```

**Host-Only** is used for management access:

```text
Host: 192.168.56.1
DC01: 192.168.56.101
```

## Remote Management

Because Server Core does not provide the normal graphical management experience, PowerShell Remoting was configured through WinRM.

The connection was successfully established from the host computer:

```powershell
Enter-PSSession -ComputerName 192.168.56.101 -Credential (Get-Credential)
```

## Active Directory

Active Directory Domain Services was installed and `DC01` was promoted to a Domain Controller.

The lab domain is:

```text
lab.home
```

DNS was configured as part of the Active Directory deployment.

During setup, DNS initially registered multiple network interfaces on the multi-homed server. DNS registration was adjusted so the IT-LAB interface is the intended DNS-registered address:

```text
DC01 → 192.168.50.10
```

## Active Directory Structure

```text
lab.home
│
├── IT
│   ├── Users
│   ├── Admins
│   └── Computers
│       └── WD-SERVER
│
└── Groups
    ├── IT-Users
    └── IT-Admins
```

Users and security groups were created to begin separating normal usage from administrative responsibilities.

## Windows Client

A Windows 11 Pro virtual machine named `WD-SERVER` was successfully joined to the `lab.home` domain.

The computer object was moved into:

```text
OU=Computers,OU=IT,DC=lab,DC=home
```

A domain user was successfully used to log in to the Windows client.

## Group Policy

The first Group Policy Object was created:

```text
IT-Workstations
```

The GPO was linked to:

```text
OU=Computers,OU=IT,DC=lab,DC=home
```

A `gpupdate /force` was successfully executed on the client.

The next stage is to verify and configure the policy so its effective settings can be tested.

## Troubleshooting

### WinRM

Remote management initially failed. The investigation covered IP configuration, VirtualBox adapters, Host-Only networking, connectivity, WinRM, TrustedHosts and authentication. The result was a successful remote PowerShell session.

### DNS

The multi-homed Domain Controller initially registered all three interface addresses in DNS. The interfaces were reviewed and DNS registration was adjusted so the IT-LAB address is the intended DNS-registered address.

### Windows Domain Join

The first domain join attempt failed. DNS was investigated and corrected, but the client still could not join the domain. The root cause was then identified: the client was running Windows 11 Home, which does not support joining an Active Directory domain. The client was moved to Windows 11 Pro and the domain join then succeeded.

### Active Directory object placement

After joining the domain, `WD-SERVER` initially appeared in the default `Computers` container. It was moved into the custom `IT → Computers` OU.

While experimenting with PowerShell, an accidental `IT-Workstations` OU was created. Active Directory's `ProtectedFromAccidentalDeletion` setting prevented its deletion until the protection was explicitly disabled.

## Current Status

| Component | Status |
|---|---|
| Windows Server 2025 | Complete |
| Server Core | Complete |
| VirtualBox networking | Complete |
| NAT | Complete |
| IT-LAB network | Complete |
| Host-Only management | Complete |
| WinRM | Complete |
| PowerShell Remoting | Complete |
| AD DS | Complete |
| Domain Controller | Complete |
| DNS | Complete |
| `lab.home` domain | Complete |
| AD Users | Complete |
| AD Groups | Complete |
| OU structure | Complete |
| Windows 11 Pro client | Complete |
| Domain Join | Complete |
| Client computer OU | Complete |
| First GPO | Complete |
| GPO effective-policy testing | Next |

## Next Steps

1. Verify the effective `IT-Workstations` policy
2. Configure a simple test policy
3. Test policy application on `WD-SERVER`
4. Review administrative privileges and least privilege
5. Create additional security groups
6. Configure useful workstation policies
7. Continue toward a more complete enterprise-style environment

## Lessons Learned

A major lesson from this project has been the importance of troubleshooting one layer at a time:

```text
Network
   ↓
IP configuration
   ↓
DNS
   ↓
Service
   ↓
Firewall
   ↓
Authentication
   ↓
Application / management
```

The lab has demonstrated how DNS, network adapter configuration, Windows editions, Active Directory structure and permissions interact in an infrastructure environment.

The environment will then be expanded with DNS, organizational units, users, security groups, Group Policy and PowerShell automation.
