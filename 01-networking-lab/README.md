# 01 - Networking Lab

## Goal

Build a small network environment and document how hosts communicate.

## Topics

- IPv4
- Subnetting / CIDR
- DNS
- DHCP
- TCP / UDP
- NAT
- Routing
- Firewall
- SSH
- Troubleshooting

## Evidence to add

- [ ] Network diagram
- [ ] IP addressing plan
- [ ] Packet Tracer or lab files
- [ ] Test results
- [ ] Troubleshooting notes

## What I learned

# Networking Lab

## Overview

As the first technical stage of my IT infrastructure home lab, I worked through the fundamentals of computer networking.

The goal was to strengthen my existing networking knowledge and connect the theory to practical troubleshooting and server administration.

Rather than focusing only on definitions, I practiced understanding how devices communicate, how IP addressing works, how DNS and DHCP fit into a network, and how to approach connectivity problems systematically.

---

## Networking Fundamentals

### IP addressing

An IP address identifies a device/interface on a network and allows network traffic to be directed to the correct destination.

I practiced working with IPv4 addresses and subnet masks and learned how the subnet determines which addresses belong to the same network.

Example:

```text
192.168.1.10/24

Network: 192.168.1.0
Host:    192.168.1.10
Mask:    255.255.255.0
```

### DHCP

DHCP (Dynamic Host Configuration Protocol) can automatically provide network configuration to clients.

This can include:

- IP address
- Subnet mask
- Default gateway
- DNS server

This removes the need to manually configure every client.

### DNS

DNS (Domain Name System) translates human-readable hostnames into IP addresses.

For example:

```text
google.com
    |
    v
DNS
    |
    v
IP address
```

This allows users and applications to use names instead of having to remember IP addresses.

### Default gateway

The default gateway is used when a device needs to communicate with a destination outside its local subnet.

A simplified example:

```text
Client
192.168.1.20
     |
     v
Gateway
192.168.1.1
     |
     v
Other networks / Internet
```

---

## Connectivity Testing

I practiced using `ping` to test basic network connectivity.

Examples:

```bash
ping 192.168.1.1
```

```bash
ping 8.8.8.8
```

```bash
ping google.com
```

These tests can help separate different types of problems.

For example:

```text
Ping gateway
      |
      +-- fails → local network / configuration problem
      |
      +-- works
            |
        Ping public IP
            |
            +-- fails → routing / internet connectivity problem
            |
            +-- works
                  |
              Ping hostname
                  |
                  +-- fails → DNS may be the problem
```

This introduced a structured approach to troubleshooting instead of immediately changing configuration.

---

## DNS vs DHCP

One of the key concepts practiced in this lab was understanding the difference between DNS and DHCP.

### DHCP

Answers the question:

> "What network configuration should this device use?"

### DNS

Answers the question:

> "What IP address belongs to this hostname?"

Simplified:

```text
DHCP
  ↓
Gives a client network configuration

DNS
  ↓
Resolves names to IP addresses
```

---

## Troubleshooting Methodology

A major lesson from the networking lab was to troubleshoot connectivity layer by layer.

A simplified approach used throughout the lab was:

```text
1. Check the local interface
        ↓
2. Check IP configuration
        ↓
3. Check subnet
        ↓
4. Check default gateway
        ↓
5. Test local network connectivity
        ↓
6. Test external IP connectivity
        ↓
7. Test DNS resolution
        ↓
8. Check services / firewall if required
```

This methodology was later useful when setting up SSH on Ubuntu and remote PowerShell management on Windows Server.

---

## Networking in the Home Lab

The networking knowledge from this lab was applied directly to the later virtual infrastructure.

The lab now uses multiple virtual network types in VirtualBox:

```text
NAT
 ↓
Internet access

Internal Network
 ↓
VM-to-VM lab communication

Host-Only
 ↓
Host-to-VM management
```

This provided practical experience with network separation and helped me understand why different interfaces can have different purposes.

---

## Skills Practiced

- IPv4 addressing
- Subnet masks
- CIDR notation
- DHCP
- DNS
- Default gateways
- Ping / ICMP
- Basic connectivity testing
- Network troubleshooting
- Virtual networking
- NAT
- Internal networks
- Host-Only networking
- Basic network segmentation

---

## Practical Application

The concepts from this lab were applied directly to later projects:

### Ubuntu Server

Networking knowledge was used while configuring and troubleshooting SSH connectivity.

### Windows Server

Networking concepts were applied when building the Windows Server environment with:

- NAT
- Internal Network
- Host-Only networking
- Static IPv4 configuration
- Remote PowerShell management

The Windows Server lab currently uses:

```text
IT-LAB
192.168.50.0/24

Host-Only
192.168.56.0/24
```

---

## What I Learned

The most important lesson was that networking is not just about memorizing protocols and commands.

When something does not work, I need to determine **where** the communication stops.

For example:

```text
Application
    ↓
Service
    ↓
Port
    ↓
Firewall
    ↓
IP
    ↓
Routing
    ↓
Network interface
```

This way of thinking is becoming the foundation for the system administration and cybersecurity projects that follow.

---

## Current Status

| Topic | Status |
|---|---|
| IPv4 | Practiced |
| Subnetting | Practiced |
| DHCP | Practiced |
| DNS | Practiced |
| Default gateway | Practiced |
| ICMP / ping | Practiced |
| Basic troubleshooting | Practiced |
| VirtualBox networking | Applied |
| NAT | Applied |
| Internal Network | Applied |
| Host-Only networking | Applied |

## Next Steps

The networking fundamentals from this lab will be applied throughout the rest of the home lab.

The next infrastructure stages build on these concepts:

```text
Networking
    ↓
Linux Server
    ↓
Windows Server
    ↓
Active Directory
    ↓
PowerShell Automation
    ↓
Security
    ↓
Cloud / Azure
    ↓
Terraform
    ↓
Docker
    ↓
CI/CD
```

