# Home NAS Infrastructure

**Status:** In progress
**Type:** Personal Home Lab
**Focus:** Storage · Networking · Access Management

## Overview

For my personal home lab, I independently set up and configured a NAS to create a centralized and reliable storage environment for my files.

The goal was to move away from storing everything locally on individual devices and instead create a central storage location that could be accessed over the home network. During the setup, I configured the NAS, network connectivity, storage structure and user access myself.

Although this is a personal environment rather than a production business environment, the project gave me practical experience with several concepts that are also relevant to IT infrastructure and system administration.

## Hardware

The NAS was configured with multiple drives and dedicated storage capacity for centralized file storage.

* **NAS:** DS224+
* **Drives:** 2
* **Total capacity:**  8 TB
* **Storage configuration:** Raid 1 

## Network Configuration

I connected the NAS to my home network and configured its network connectivity so that it could be reliably accessed by the devices in the network.

The NAS was configured with a consistent network address, allowing connected devices to find and access the storage without having to manually locate it each time.

This gave me practical experience with concepts such as:

* IP addressing
* DHCP / static IP configuration
* Network connectivity
* DNS and hostname resolution
* Accessing network resources from different devices

## Storage

I configured the available disks as centralized storage and organized the storage into separate volumes and network shares.

The storage configuration included:

* RAID configuration
* Storage volumes
* Shared folders
* Access permissions

The goal was to keep the storage organized and make sure that different types of data could be stored in appropriate locations.

I also considered the importance of redundancy when configuring the storage. The RAID configuration provides protection against certain types of disk failure, although I understand that **RAID itself is not a backup**.

## User Access & Permissions

I configured user accounts and access permissions for the NAS.

Different users could be given access to the appropriate shared folders rather than giving every account unrestricted access to all stored data.

The NAS was primarily accessed using network file-sharing protocols such as **SMB**.

This gave me practical experience with:

* User accounts
* Groups
* File and folder permissions
* Shared folders
* Network file access
* SMB

## Backup

I also considered the importance of separating storage redundancy from backups.

The NAS serves primarily as centralized storage. A proper backup strategy should provide an additional copy of important data outside the primary storage environment.

This is an area I want to develop further as part of my IT infrastructure learning.

## Security & Services

The NAS currently has limited additional services and security configuration beyond the basic setup and access controls described above.

I have intentionally left this area as a future learning opportunity rather than presenting it as completed experience.

Future improvements could include:

* stronger access controls
* MFA where supported
* secure remote access through VPN
* monitoring and logging
* automated backups
* vulnerability/update management
* containerized services
* network segmentation

## What I Learned

Setting up the NAS gave me practical experience with concepts that are directly relevant to system administration:

* configuring hardware and storage
* networking a device
* IP addressing
* centralized file storage
* RAID and storage redundancy
* network shares
* user and group management
* permissions
* SMB
* basic backup considerations

The project also made me interested in developing these skills further in a more structured lab environment.

## Next Steps

I plan to expand this personal home lab by learning and implementing:

1. Linux server administration
2. Windows Server and Active Directory
3. PowerShell automation
4. Network segmentation
5. Security hardening
6. Monitoring and logging
7. Cloud infrastructure with Azure
8. Infrastructure as Code with Terraform

This NAS is therefore the starting point of my broader IT infrastructure and cloud/security learning journey.
