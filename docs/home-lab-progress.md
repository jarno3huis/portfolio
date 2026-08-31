# Home Lab Progress Update

This update documents the current progress of my IT infrastructure home lab.

## Current Progress

### Linux

Ubuntu Server has been deployed and remotely managed using SSH.

I have practiced Linux users and groups, file permissions, Bash scripting, processes, services and networking.

### Windows Infrastructure

Windows Server 2025 has been deployed as `DC01` using Server Core.

The server has been configured with separate virtual networks for:

- Internet access through NAT
- Internal VM communication through an Internal Network
- Host-to-server management through a Host-Only network

PowerShell Remoting over WinRM has been successfully configured and tested.

## Current Architecture

```text
                         Host PC
                            |
                     Host-Only Network
                      192.168.56.0/24
                            |
                         DC01
                  Windows Server 2025
                     /            \
                   NAT           IT-LAB
                10.0.2.x       192.168.50.0/24
                                  |
                            Linux / Clients
```

## Next Milestone

The next major milestone is Active Directory:

```text
Windows Server
      |
      v
AD DS
      |
      v
Domain Controller
      |
      v
DNS
      |
      v
Users / Groups / OUs
      |
      v
Group Policy
      |
      v
Windows Client
```
