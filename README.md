# Kali Linux VirtualBox Setup

## Project Overview

This project documents the installation and configuration of Kali Linux in Oracle VM VirtualBox as part of the **NetworkWalks Cybersecurity Internship 2026 – Batch B084, Week 1**.

The main objective of this project is to prepare a Kali Linux virtual machine for cybersecurity learning and practical lab activities. The setup includes VirtualBox configuration, network configuration, shared clipboard, drag and drop, shared folder integration, internet connectivity testing, and VM snapshot creation.

## Project Objectives

- Install and configure Kali Linux using Oracle VM VirtualBox.
- Configure a NAT Network to provide network connectivity.
- Set a static IP address for the Kali Linux virtual machine.
- Enable shared clipboard and drag and drop functionality.
- Configure a shared folder between Windows and Kali Linux.
- Verify internet and DNS connectivity.
- Create a virtual machine snapshot as a restore point.
- Understand basic virtual machine and network configuration.

## Environment and Specifications

### Host Machine

| Component | Specification |
|---|---|
| Operating System | Windows 11 |
| Device | Dell Latitude 7300 |
| Processor | Intel Core i7-8665U |
| CPU | 4 Cores / 8 Threads |
| RAM | 16 GB DDR4 |
| Storage | 238 GB SSD |

### Virtual Machine

| Component | Configuration |
|---|---|
| Virtualization Software | Oracle VM VirtualBox 7.2.22 |
| Operating System | Kali Linux 2026.3 |
| Base Memory | 4096 MB |
| Processors | 4 CPUs |
| Virtual Disk | 80 GB |
| Disk Type | Dynamically Allocated |
| Network Adapter | NAT Network |

## Implementation Steps

### 1. Install Oracle VM VirtualBox

Installed Oracle VM VirtualBox 7.2.22 on the Windows 11 host machine.

![VirtualBox Installed](01-virtualbox-installed.png)

### 2. Configure NAT Network

Created a NAT Network named `NatNetwork` with the following configuration:

| Configuration | Value |
|---|---|
| Network Name | NatNetwork |
| IPv4 Prefix | 10.0.0.0/24 |
| Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |

![NAT Network Configuration](02-natnetwork.png)

### 3. Import Kali Linux Virtual Machine

Imported Kali Linux 2026.3 into VirtualBox and configured the virtual machine resources according to the available host specifications.

![Kali Linux Imported](03-kali-imported.png)

### 4. Configure Network Adapter

Configured the Kali Linux network adapter to use the previously created `NatNetwork`.

![Kali Network Adapter](04-kali-nat-network-adapter.png)

### 5. Enable Shared Clipboard and Drag and Drop

Enabled the following VirtualBox integration features:

- Shared Clipboard: Bidirectional
- Drag and Drop: Bidirectional

These features allow easier data exchange between the Windows host and Kali Linux virtual machine.

![Shared Clipboard](05a-shared-clipboard.png)

![Drag and Drop](05b-drag-and-drop.png)

### 6. Configure Shared Folder

Configured a shared folder between the Windows host and Kali Linux.

The Windows Downloads folder was shared and mounted inside Kali Linux at:

`/media/sf_Downloads`

The Kali Linux user was also added to the `vboxsf` group to obtain access to the shared folder.

![Add Shared Folder](06a-shared-folder-add-share.png)

![Shared Folder Configuration](06b-shared-folder-configured.png)

![Shared Folder Mounted](06c-shared-folder-mounted.png)

### 7. Configure Static IP Address

Configured a static IP address for the Kali Linux virtual machine.

| Network Configuration | Value |
|---|---|
| IP Address | 10.0.0.2 |
| Subnet Mask | 255.255.255.0 |
| CIDR | /24 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |

The static IP configuration was applied using NetworkManager (`nmcli`).

![Kali IP Address](07a-kali-ip-address.png)

![Manual IP Configuration](07b-kali-manual-ip-settings.png)

### 8. Test Internet Connectivity

Performed connectivity tests to verify that Kali Linux could access the internet.

The tests included:

- Ping to `8.8.8.8` to verify IP connectivity.
- Ping to `google.com` to verify DNS resolution.

Both tests were successful with 0% packet loss.

![Ping IP Test](08a-internet-test-ping-ip.png)

![Ping DNS Test](08b-internet-test-ping-dns.png)

### 9. Create Virtual Machine Snapshot

Created a snapshot named `Kali-WK1-Clean-Setup` after completing the installation and configuration.

This snapshot serves as a restore point if the virtual machine needs to return to its initial configured state.

![Kali Snapshot](09-vm-snapshot-taken.png)

## Troubleshooting

### Network Connection Stuck on "Getting IP Configuration"

**Problem:**

During network configuration, Kali Linux remained stuck at:

`connecting (getting IP configuration)`

The virtual machine did not obtain an IP address automatically, even though the NAT Network configuration was already set.

**Solution:**

Resolved the issue by manually assigning a static IP address through NetworkManager using `nmcli`.

The following commands were executed:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.method manual ipv4.addresses 10.0.0.2/24 ipv4.gateway 10.0.0.1 ipv4.dns 8.8.8.8 ipv4.dad-timeout 0
```

Then restarted the network connection:

```bash
sudo nmcli connection up "Wired connection 1"
```

After applying the configuration, Kali Linux successfully obtained the static IP address and network connectivity was restored.

![Network Connection Issue](10a-troubleshooting-connecting.png)

![Network Configuration Fix](10b-troubleshooting-fix-nmcli.png)

## Lessons Learned

Throughout this project, I learned how to:

- Install and configure Kali Linux in a virtualized environment.
- Configure VirtualBox NAT Network settings.
- Assign and manage static IP addresses using NetworkManager.
- Enable integration features between the host and virtual machine.
- Configure shared folders in VirtualBox.
- Perform basic network connectivity and DNS tests.
- Troubleshoot network configuration issues.
- Create and manage virtual machine snapshots.

This project also helped me understand the importance of network configuration and troubleshooting when preparing a cybersecurity lab environment.

## Repository Structure

```text
NETWORKWALKS-MARLIANA-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP/
│
├── README.md
├── 01-virtualbox-installed.png
├── 02-natnetwork.png
├── 03-kali-imported.png
├── 04-kali-nat-network-adapter.png
├── 05a-shared-clipboard.png
├── 05b-drag-and-drop.png
├── 06a-shared-folder-add-share.png
├── 06b-shared-folder-configured.png
├── 06c-shared-folder-mounted.png
├── 07a-kali-ip-address.png
├── 07b-kali-manual-ip-settings.png
├── 08a-internet-test-ping-ip.png
├── 08b-internet-test-ping-dns.png
├── 09-vm-snapshot-taken.png
├── 10a-troubleshooting-connecting.png
└── 10b-troubleshooting-fix-nmcli.png
```

## Disclaimer

This repository is intended for educational purposes as part of the NetworkWalks Cybersecurity Internship 2026.

All configurations and activities were performed in a controlled virtual lab environment.

## Acknowledgements

Special thanks to **NetworkWalks** and **Waqas Karim (CCIE)** for providing the learning materials, guidance, and opportunity to participate in the Cybersecurity Internship 2026.

## Author

**Marliana**  
NetworkWalks Cybersecurity Internship 2026  
Batch B084 – Week 1

GitHub: [LilyMarliana](https://github.com/LilyMarliana)
