# Troubleshooting: Windows Server Remote Management

## Problem

PowerShell Remoting to the Windows Server initially failed.

The first tests showed that the host could not reach the server through the planned internal lab address.

## Investigation

The network architecture was reviewed and separated into three purposes:

1. NAT for outbound internet access
2. Internal Network for VM-to-VM lab traffic
3. Host-Only networking for host-to-VM management

The Host-Only network was configured as:

```text
Host: 192.168.56.1
DC01: 192.168.56.101
```

Connectivity was then tested independently from WinRM.

## WinRM

Once network connectivity was working, WinRM was configured on the server.

The client initially returned an authentication/trust error because the host and server were not yet members of an Active Directory domain.

For this isolated lab, the server was added to the WinRM client's TrustedHosts configuration.

This was treated as a lab-specific solution; in a production environment, authentication and trust would need to be designed appropriately.

## Result

PowerShell Remoting was successfully established:

```powershell
Enter-PSSession -ComputerName 192.168.56.101 -Credential (Get-Credential)
```

The resulting prompt showed:

```text
[192.168.56.101]: PS ...
```

confirming that commands were being executed remotely on DC01.

## Lessons Learned

The main lesson was to troubleshoot infrastructure layer by layer:

```text
Virtual network
        |
IP configuration
        |
Connectivity
        |
Port / service
        |
Firewall
        |
Authentication
        |
Remote management
```

This approach prevents changing multiple variables at the same time and makes it easier to identify the actual cause of a problem.
