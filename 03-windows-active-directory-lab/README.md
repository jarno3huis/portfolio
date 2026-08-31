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


## Overview

As part of my IT infrastructure home lab, I deployed a Windows Server 2025 Standard Evaluation virtual machine in VirtualBox.

The goal is to build a small enterprise-style Windows infrastructure environment while developing practical skills in system administration, networking, identity management, security and automation.

The environment is being built and documented step by step rather than following only theoretical exercises.

## Current Environment

### Server

- Hostname: `DC01`
- Operating system: Windows Server 2025 Standard Evaluation
- Installation type: Server Core
- Virtualization: VirtualBox
- Remote administration: PowerShell Remoting / WinRM

## Network Architecture

The server uses separate virtual network interfaces for different purposes.

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
                                      |
                                Host PC
                                192.168.56.1
```

### NAT

The NAT adapter provides outbound internet connectivity for the server, such as downloading updates and required components.

Current address observed during setup:

```text
10.0.2.15
```

### Internal Network - IT-LAB

The Internal Network is intended for communication between the virtual machines inside the isolated lab.

Planned network:

```text
192.168.50.0/24
```

The server's planned internal lab address is:

```text
192.168.50.10/24
```

### Host-Only Network

A separate Host-Only network was configured for management access between the physical host and the virtual server.

Host:

```text
192.168.56.1
```

DC01:

```text
192.168.56.101
```

This keeps management traffic separate from the physical home network.

## Remote Management

Because the Windows Server installation uses Server Core, remote administration was configured using Windows Remote Management (WinRM) and PowerShell Remoting.

The setup required troubleshooting several layers:

```text
Network connectivity
        |
        v
Host-Only networking
        |
        v
WinRM
        |
        v
Firewall / access configuration
        |
        v
Authentication
        |
        v
PowerShell Remoting
```

The final connection was successfully established from the host PC.

The remote session was opened using:

```powershell
Enter-PSSession -ComputerName 192.168.56.101 -Credential (Get-Credential)
```

The remote PowerShell prompt confirmed that commands were being executed on the Windows Server.

## Troubleshooting - WinRM

Initially, remote PowerShell access failed even though the server was running.

The investigation included:

- Checking the server's IP configuration
- Checking VirtualBox adapter configuration
- Separating NAT, Internal Network and Host-Only traffic
- Testing connectivity with `ping`
- Testing TCP port `5985`
- Configuring WinRM
- Configuring the WinRM client
- Adding the lab server to TrustedHosts for this isolated lab
- Retesting PowerShell Remoting

The final result was a working remote PowerShell session.

This was an important practical exercise because it demonstrated that a remote-access problem can involve multiple layers: networking, services, firewall configuration and authentication.

## Skills Practiced

- Windows Server 2025
- Server Core
- VirtualBox
- PowerShell
- IPv4 networking
- NAT
- Internal Network
- Host-Only networking
- Network segmentation
- WinRM
- PowerShell Remoting
- Basic firewall troubleshooting
- Remote server administration

## Current Status

| Component | Status |
|---|---|
| Windows Server 2025 | Complete |
| Server Core | Complete |
| NAT connectivity | Complete |
| Internal lab network | Configured |
| Host-Only management network | Complete |
| WinRM | Complete |
| PowerShell Remoting | Complete |
| Active Directory Domain Services | Next step |
| Domain Controller promotion | Planned |
| DNS | Planned |
| Users & Groups | Planned |
| Group Policy | Planned |
| Windows Client domain join | Planned |

## Next Steps

The next stage of the project is to install and configure Active Directory Domain Services and turn `DC01` into a Domain Controller.

Planned architecture:

```text
                 DC01
                  |
          Active Directory
                  |
          +-------+-------+
          |               |
        Users           Groups
          |
     Group Policy
          |
    Windows Client
```

The environment will then be expanded with DNS, organizational units, users, security groups, Group Policy and PowerShell automation.
