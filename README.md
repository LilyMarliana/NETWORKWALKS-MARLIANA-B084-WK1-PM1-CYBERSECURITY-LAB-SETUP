
# Kali Linux VirtualBox Setup

**Building and Configuring an Isolated Cybersecurity Lab Environment**

![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-red)
![VirtualBox](https://img.shields.io/badge/VirtualBox-7.2.22-blue)
![Kali Linux](https://img.shields.io/badge/Kali_Linux-2026.3-blue)
![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-green)
![Internship](https://img.shields.io/badge/NetworkWalks-Week_1-orange)

## 1. Project Overview

This repository documents the installation, configuration, and setup of Kali Linux in Oracle VirtualBox as part of the **NetworkWalks Cybersecurity Internship 2026 — Batch B084, Week 1**.

The main objective of this project is to build an isolated virtual lab environment for learning cybersecurity fundamentals, Linux administration, networking, and penetration testing concepts.

The project focuses on configuring a Kali Linux virtual machine, establishing network connectivity, enabling integration between the host and guest operating systems, and preparing a clean virtual environment for future cybersecurity exercises.

All activities were performed in a controlled virtual lab environment for educational purposes.

## 2. Project Objectives

The main objectives of this project are:

- [x] Install and configure Oracle VirtualBox.
- [x] Set up Kali Linux 2026.3 in a virtual machine.
- [x] Configure virtual machine resources (RAM, CPU, and storage).
- [x] Create a NAT Network using the `10.0.0.0/24` subnet.
- [x] Configure Kali Linux with a static IP address.
- [x] Configure shared clipboard and drag-and-drop.
- [x] Configure a shared folder between Windows and Kali Linux.
- [x] Verify internet and DNS connectivity.
- [x] Troubleshoot network configuration issues.
- [x] Create a clean VM snapshot.

## 3. Lab Environment

### 3.1 Host Machine Specifications

| Component | Specification |
|---|---|
| Operating System | Windows 11 |
| Laptop | Dell Latitude 7300 |
| Processor | Intel Core i7-8665U |
| CPU | 4 Cores / 8 Threads |
| RAM | 16 GB DDR4 |
| Storage | 238 GB SSD |

### 3.2 Virtual Machine Configuration

| Component | Configuration |
|---|---|
| Virtualization Software | Oracle VirtualBox 7.2.22 |
| Operating System | Kali Linux 2026.3 |
| Memory (RAM) | 4096 MB |
| CPU | 4 Cores |
| Virtual Disk | 80 GB |
| Disk Allocation | Dynamically Allocated |
| Network Adapter | NAT Network |
| VM Snapshot | Kali-WK1-Clean-Setup |

### 3.3 Network Configuration

A NAT Network named `NatNetwork` was created in VirtualBox to provide network connectivity for the Kali Linux virtual machine.

| Setting | Value |
|---|---|
| Network Name | NatNetwork |
| Network Type | NAT Network |
| Network Prefix | 10.0.0.0/24 |
| IP Address | 10.0.0.2 |
| Subnet Mask | 255.255.255.0 |
| Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |

## 4. Kali Linux Installation and Configuration

### 4.1 VirtualBox Installation and NAT Network Setup

Oracle VirtualBox 7.2.22 was installed on the Windows 11 host machine.

After installation, a NAT Network named `NatNetwork` was created with the following network prefix:

```text
10.0.0.0/24
```

This network configuration was used to provide network connectivity to the Kali Linux virtual machine.

### 4.2 Kali Linux Virtual Machine Setup

Kali Linux 2026.3 was configured in Oracle VirtualBox with the following specifications:

- Memory: 4096 MB RAM
- Processors: 4 CPU cores
- Storage: 80 GB dynamically allocated virtual disk
- Network Adapter: NAT Network

The virtual machine was connected to the previously created `NatNetwork`.

### 4.3 Shared Clipboard, Drag-and-Drop, and Shared Folder

To improve integration between Windows and Kali Linux, the following VirtualBox features were configured:

| Feature | Configuration |
|---|---|
| Shared Clipboard | Bidirectional |
| Drag-and-Drop | Bidirectional |
| Shared Folder | Windows Downloads directory |

The shared folder was successfully mounted in Kali Linux and made accessible through:

```bash
/media/sf_Downloads
```

The Kali Linux user was also configured with the necessary `vboxsf` group access to use the shared folder.

### 4.4 Static IP Address Configuration

Kali Linux was configured with a static IP address to establish a consistent network configuration.

The following network settings were applied:

```text
IP Address : 10.0.0.2
Subnet Mask: 255.255.255.0
Gateway    : 10.0.0.1
DNS        : 8.8.8.8
```

### 4.5 Internet and DNS Connectivity Testing

Network connectivity was verified using the following commands:

**Test connectivity to an external IP address:**

```bash
ping 8.8.8.8
```

**Test DNS resolution and connectivity:**

```bash
ping google.com
```

Both tests completed successfully with **0% packet loss**, confirming that Kali Linux could access the internet and resolve domain names.

### 4.6 Virtual Machine Snapshot

After completing the installation and configuration process, a clean virtual machine snapshot was created.

Snapshot name:

```text
Kali-WK1-Clean-Setup
```

This snapshot provides a restore point for returning to the configured Kali Linux environment before performing future lab activities.

## 5. Screenshots and Documentation

The following screenshots document the installation and configuration process.

### 5.1 VirtualBox and NAT Network Configuration

1. `01-virtualbox-installed.png`
2. `02-natnetwork.png`
3. `03-kali-imported.png`
4. `04-kali-nat-network-adapter.png`

### 5.2 Shared Clipboard and Shared Folder Configuration

5. `05a-shared-clipboard.png`
6. `05b-drag-and-drop.png`
7. `06a-shared-folder-add-share.png`
8. `06b-shared-folder-configured.png`
9. `06c-shared-folder-mounted.png`

### 5.3 Network Configuration and Connectivity Testing

10. `07a-kali-ip-address.png`
11. `07b-kali-manual-ip-settings.png`
12. `08a-internet-test-ping-ip.png`
13. `08b-internet-test-ping-dns.png`

### 5.4 Snapshot and Troubleshooting

14. `09-vm-snapshot-taken.png`
15. `10a-troubleshooting-connecting.png`
16. `10b-troubleshooting-fix-nmcli.png`

All screenshots are available in:

```text
screenshots/kali linux/
```

## 6. Troubleshooting and Problem Solving

### 6.1 Network Configuration Issue

During the initial Kali Linux setup, the network interface remained in the following state:

```text
connecting (getting IP configuration)
```

Although the NAT Network configuration had been created, Kali Linux did not obtain the expected IP address.

### 6.2 Solution

The issue was resolved by manually configuring the static IP address through NetworkManager using `nmcli`.

The following command was executed:

```bash
sudo nmcli connection modify "Wired connection 1" \
ipv4.method manual \
ipv4.addresses 10.0.0.2/24 \
ipv4.gateway 10.0.0.1 \
ipv4.dns 8.8.8.8 \
ipv4.dad-timeout 0
```

After applying the configuration, the network connection was restarted:

```bash
sudo nmcli connection up "Wired connection 1"
```

The network configuration was then successfully applied, allowing Kali Linux to connect to the NAT Network and access the internet.

### 6.3 Key Lessons Learned

Through this troubleshooting process, I gained a better understanding of:

- Configuring network interfaces in Kali Linux.
- Using NetworkManager and `nmcli` commands.
- Assigning static IP addresses.
- Configuring gateways and DNS servers.
- Troubleshooting network connectivity issues.
- Verifying network connectivity using `ping`.

## 7. Key Takeaways

By completing this project, I gained practical experience in:

- Installing and configuring Kali Linux in VirtualBox.
- Understanding virtualization and virtual machine resources.
- Creating and configuring a NAT Network.
- Managing IP addresses, gateways, and DNS settings.
- Configuring shared folders and clipboard integration.
- Testing internet and DNS connectivity.
- Troubleshooting Linux network configuration issues.
- Creating and managing virtual machine snapshots.
- Preparing an isolated environment for cybersecurity practice.

This project provided a foundation for continuing to learn Linux, networking, and cybersecurity in a controlled virtual lab environment.

## 8. Repository Structure

```text
NETWORKWALKS-MARLIANA-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP/
│
├── README.md
│
└── screenshots/
    └── kali linux/
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

## 9. Disclaimer

All activities documented in this repository were performed for educational purposes in a controlled virtual lab environment.

This project is intended for learning cybersecurity fundamentals, Linux administration, networking, and penetration testing concepts.

Do not perform security testing against systems or networks without proper authorization.

## 10. Acknowledgment

This project was completed as part of the **NetworkWalks Cybersecurity Internship 2026 — Batch B084, Week 1**.

Special thanks to **NetworkWalks** and **Waqas Karim (CCIE)** for providing the learning materials, guidance, and practical lab exercises.

---

**Author:** Marliana  
**Program:** NetworkWalks Cybersecurity Internship 2026  
**Batch:** B084  
**Week:** 1  
**Project:** Kali Linux VirtualBox Setup

**Repository:** [GitHub - Kali Linux VirtualBox Setup](https://github.com/LilyMarliana/NETWORKWALKS-MARLIANA-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP)
