# 02 - Linux Server Lab

## Goal

Build and administer a Linux server in a virtual lab.

## Topics

- Users and groups
- File permissions
- SSH
- Services
- Processes
- Package management
- Networking
- Logs
- Bash

## Evidence to add

- [ ] Server setup documentation
- [ ] SSH configuration
- [ ] User/group configuration
- [ ] Service management examples
- [ ] Troubleshooting notes

## What I learned

# Linux Server Lab

## Overview

As part of my IT infrastructure home lab, I deployed an Ubuntu Server virtual machine to build practical Linux system administration skills.

The objective is to move beyond theoretical knowledge by configuring, testing and troubleshooting a working server environment and documenting the process.

## Current Environment

The Ubuntu Server is running as a virtual machine in VirtualBox.

### Remote administration

SSH was configured so the server can be managed remotely instead of relying on the VM console.

The connection was successfully tested from the host machine.

```text
Host PC
   |
   | SSH
   v
Ubuntu Server
```

## Skills Practiced

- Ubuntu Server
- Linux command line
- SSH
- Users and groups
- File and directory permissions
- `chmod`
- `chown`
- Bash scripting
- Processes
- Services
- `systemctl`
- `journalctl`
- IPv4 networking
- Basic network troubleshooting

## File Permissions

I practiced Linux permissions using the `rwx` model.

For example:

```text
-rwxr-x---
```

This means:

- Owner: read, write and execute
- Group: read and execute
- Others: no permissions

I also practiced translating numeric permissions such as `750` into their corresponding `rwx` values.

## Troubleshooting

The SSH setup required troubleshooting a connection timeout before the server could be accessed remotely.

The troubleshooting process involved checking the server, network connectivity and SSH service configuration.

This reinforced an important infrastructure principle: troubleshoot from the lower layers upward instead of changing multiple things at once.

## Current Status

| Component | Status |
|---|---|
| Ubuntu Server | Complete |
| SSH remote access | Complete |
| Users & groups | Practiced |
| File permissions | Practiced |
| Bash scripting | Practiced |
| Processes & services | Practiced |
| Networking | Practiced |

## Next Steps

The Linux environment will later be expanded with additional services, security hardening and automation as the wider home lab develops.

