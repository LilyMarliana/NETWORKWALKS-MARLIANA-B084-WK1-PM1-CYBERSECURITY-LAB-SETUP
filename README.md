# Cybersecurity Lab Environment Setup

**Building an Isolated Virtual Lab for Penetration Testing and Ethical Hacking Practice**

![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-red)
![VirtualBox](https://img.shields.io/badge/VirtualBox-7.x-blue)
![Kali Linux](https://img.shields.io/badge/Kali_Linux-2026.x-blue)
![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-green)
![Wireshark](https://img.shields.io/badge/Wireshark-SOC_Labs-blue)
![Internship](https://img.shields.io/badge/Program-NetworkWalks_Internship-orange)

## 1. Project Overview

This project documents the setup and configuration of an isolated cybersecurity lab environment using Oracle VirtualBox and Kali Linux.

The main objective is to build a controlled virtual environment for practicing networking fundamentals, penetration testing concepts, and cybersecurity activities.

In addition to the main Kali Linux setup, I also completed several additional learning activities, including an Android-x86 virtual machine and Wireshark SOC labs.

All activities were performed in a controlled lab environment for educational purposes.

## 2. Project Objectives

### Main Week 1 Requirements

- [x] Install and configure Oracle VirtualBox.
- [x] Set up Kali Linux in a virtual machine.
- [x] Create a NAT Network using the `10.0.0.0/24` subnet.
- [x] Configure Kali Linux with a static IP address.
- [x] Configure shared clipboard and drag-and-drop.
- [x] Configure a shared folder between Windows and Kali Linux.
- [x] Verify internet and DNS connectivity.
- [x] Create a clean VM snapshot.

### Additional Learning Activities

- [x] Install and configure Android-x86 9.0 in VirtualBox.
- [x] Connect Android-x86 to the same NAT Network.
- [x] Configure Android with a static IP address.
- [x] Test connectivity between Android and Kali Linux.
- [x] Complete six Wireshark SOC labs.
- [ ] Complete Windows 10 virtual machine setup (installation issue remains unresolved).

## 3. Lab Environment

### Host Machine

| Component | Specification |
|---|---|
| Operating System | Windows 11 |
| Laptop | Dell Latitude 7300 |
| Processor | Intel Core i7-8665U |
| CPU | 4 Cores / 8 Threads |
| RAM | 16 GB DDR4 |
| Storage | 238 GB SSD |

### Virtual Machine Configuration

| Component | Kali Linux | Android-x86 |
|---|---|---|
| Virtualization | VirtualBox 7.2.22 | VirtualBox 7.2.22 |
| Operating System | Kali Linux 2026.3 | Android-x86 9.0 |
| RAM | 4096 MB | 2048 MB |
| CPU | 4 Cores | Default configuration |
| Disk | 80 GB (Dynamic) | 10 GB (Dynamic) |
| Network | NAT Network | NAT Network |
| IP Address | 10.0.0.2/24 | 10.0.0.9/24 |

### Network Configuration

All configured virtual machines use the same VirtualBox NAT Network.

| Setting | Value |
|---|---|
| Network Name | NatNetwork |
| Network Type | NAT Network |
| Network Prefix | 10.0.0.0/24 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |
| Kali Linux IP | 10.0.0.2/24 |
| Android-x86 IP | 10.0.0.9/24 |
| Windows 10 Planned IP | 10.0.0.10/24 |

## 4. Main Project: Kali Linux Lab Setup

### 4.1 VirtualBox Installation and NAT Network Configuration

Oracle VirtualBox 7.2.22 was installed on the Windows 11 host machine. A NAT Network named `NatNetwork` was created with the network prefix `10.0.0.0/24`.

### 4.2 Kali Linux VM Configuration

Kali Linux 2026.3 was configured with:

- 4096 MB RAM
- 4 CPU cores
- 80 GB dynamically allocated virtual disk
- NAT Network adapter

### 4.3 Shared Clipboard, Drag-and-Drop, and Shared Folder

The following integration features were configured:

- Shared Clipboard: Bidirectional
- Drag-and-Drop: Bidirectional
- Shared Folder: Windows Downloads directory

The shared folder was mounted successfully in Kali Linux and made accessible through the `/media/sf_Downloads` directory.

### 4.4 Static IP Configuration

Kali Linux was configured with the following static network settings:

```text
IP Address : 10.0.0.2
Subnet Mask: 255.255.255.0
Gateway    : 10.0.0.1
DNS        : 8.8.8.8
```

### 4.5 Internet and DNS Connectivity

Connectivity was verified using:

```bash
ping 8.8.8.8
ping google.com
```

Both tests completed successfully with 0% packet loss.

### 4.6 VM Snapshot

A clean snapshot was created after completing the Kali Linux configuration.

Snapshot Name:

```text
Kali-WK1-Clean-Setup
```

### 4.7 Kali Linux Screenshots

The following screenshots document the main lab setup process.

**VirtualBox and NAT Network**

1. `01-virtualbox-installed.png`
2. `02-natnetwork.png`
3. `03-kali-imported.png`
4. `04-kali-nat-network-adapter.png`

**Shared Clipboard and Folder Configuration**

5. `05a-shared-clipboard.png`
6. `05b-drag-and-drop.png`
7. `06a-shared-folder-add-share.png`
8. `06b-shared-folder-configured.png`
9. `06c-shared-folder-mounted.png`

**Network Configuration and Connectivity**

10. `07a-kali-ip-address.png`
11. `07b-kali-manual-ip-settings.png`
12. `08a-internet-test-ping-ip.png`
13. `08b-internet-test-ping-dns.png`

**Snapshot and Troubleshooting**

14. `09-vm-snapshot-taken.png`
15. `10a-troubleshooting-connecting.png`
16. `10b-troubleshooting-fix-nmcli.png`

All screenshots are available in:

```text
screenshots/kali linux/
```

## 5. Additional Project: Android-x86 Lab Setup

As an additional learning activity, I installed Android-x86 9.0 in VirtualBox and connected it to the same NAT Network used by Kali Linux.

### 5.1 Android VM Configuration

| Setting | Value |
|---|---|
| VM Name | Android9-Lab |
| Operating System | Android-x86 9.0 |
| System Type | Linux / Other Linux (64-bit) |
| RAM | 2048 MB |
| Virtual Disk | 10 GB |
| Disk Format | VDI, Dynamically Allocated |
| Network | NatNetwork |

### 5.2 Android Network Configuration

Android-x86 was configured with a static IP address.

```text
IP Address : 10.0.0.9
Subnet Mask: 255.255.255.0
Gateway    : 10.0.0.1
DNS        : 8.8.8.8
```

### 5.3 Connectivity Testing

The following connectivity tests were performed successfully:

**Android to Kali Linux**

```bash
ping 10.0.0.2
```

**Android to Internet**

```bash
ping 8.8.8.8
```

**Kali Linux to Android**

```bash
ping 10.0.0.9
```

All connectivity tests were successful with 0% packet loss.

### 5.4 Android VM Snapshot

A clean snapshot was created after completing the Android-x86 configuration.

Snapshot Name:

```text
Android-WK1-Clean-Setup
```

### 5.5 Android Screenshots

The following screenshots document the Android-x86 installation and configuration process.

| No. | Screenshot | Description |
|---|---|---|
| 1 | `01-android-general-os-memory.png` | Android VM operating system and memory configuration |
| 2 | `02-android-storage-iso-vdi.png` | ISO and virtual disk configuration |
| 3 | `03-android-network-natnetwork.png` | NAT Network adapter configuration |
| 4 | `04-android-display-settings.png` | Display settings |
| 5 | `05-android-installer-boot-menu.png` | Android-x86 installer boot menu |
| 6 | `06-android-partition-sda1-written.png` | Partition creation and installation |
| 7 | `07-android-grub-installed.png` | GRUB bootloader installation |
| 8 | `08-android-first-boot.png` | Android-x86 first boot |
| 9 | `09-android-ip-before-dhcp.png` | Network IP before static configuration |
| 10 | `10-android-static-ip-form.png` | Static IP configuration |
| 11 | `11-android-ip-after-static-10.0.0.9.png` | Static IP verification |
| 12 | `12-android-ping-kali-and-internet.png` | Android connectivity to Kali and the internet |
| 13 | `12b-kali-ping-android.png` | Kali connectivity to Android |
| 14 | `13-android-vm-snapshot.png` | Android VM snapshot |

All screenshots are available in:

```text
screenshots/android/
```

## 6. Additional Learning: Wireshark SOC Labs

As another additional learning activity, I completed six Wireshark SOC labs to practice network traffic analysis and identify suspicious network activities.

### 6.1 Completed Labs

| Lab | Title | Result |
|---|---|---|
| Lab 3 | Identify the Attacker's IP | 100/100 |
| Lab 4 | Follow TCP Stream 1 | 100/100 |
| Lab 5 | Follow TCP Stream, Part 2 | 100/100 |
| Lab 6 | HTTP Plain Text Credentials | 100/100 |
| Lab 7 | Catch the Brute Force Attacker | 100/100 |
| Lab 8 | Catch the Call Scammer | 100/100 |

**Total Score: 600/600**

### 6.2 Wireshark Display Filters

The following display filters were used during the exercises:

**Identify TCP SYN Packets**

```wireshark
tcp.flags.syn == 1
```

**Filter TCP Traffic Except HTTP and HTTPS**

```wireshark
tcp && !(tcp.port == 80 || tcp.port == 443)
```

**Identify HTTP POST Requests**

```wireshark
http.request.method == "POST"
```

**Identify Failed FTP Login Responses**

```wireshark
ftp.response.code == 530
```

### 6.3 Wireshark Lab Screenshots

The results of the six completed labs are documented below:

1. `Lab 3 Result - Marliana.png`
2. `Lab 4 Result - Marliana.png`
3. `Lab 5 Result - Marliana.png`
4. `Lab 6 Result - Marliana.png`
5. `Lab 7 Result - Marliana.png`
6. `Lab 8 Result - Marliana.png`

All screenshots are available in:

```text
screenshots/wireshark/
```

## 7. Additional Project: Windows 10 Lab (In Progress)

I also attempted to create a Windows 10 virtual machine as an additional lab environment.

### Planned Configuration

| Setting | Value |
|---|---|
| VM Name | Windows10-Lab |
| Operating System | Windows 10 (64-bit) |
| RAM | 4096 MB |
| Virtual Disk | 40 GB |
| Network | NatNetwork |
| Planned IP | 10.0.0.10/24 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |

### Installation Issue

During the Windows 10 installation process, VirtualBox displayed the following error:

```text
Windows cannot find the Microsoft Software License Terms.
Make sure the installation sources are valid and restart the installation.
```

I attempted several troubleshooting steps, including:

- Trying a different Windows 10 ISO.
- Checking the ISO file integrity.
- Disabling Hyper-V-related Windows features.

However, the installation issue remains unresolved.

**Current Status:** In Progress — Windows 10 installation and network connectivity tests have not yet been completed.

This task is documented as unfinished rather than reported as successfully completed.

## 8. Troubleshooting and Lessons Learned

### 8.1 Kali Linux Network Configuration Issue

During the initial Kali Linux setup, the network interface remained in the `connecting (getting IP configuration)` state.

The issue was resolved by manually configuring the static IP address and setting the Duplicate Address Detection timeout to zero.

Commands used:

```bash
sudo nmcli connection modify "Wired connection 1" \
ipv4.method manual \
ipv4.addresses 10.0.0.2/24 \
ipv4.gateway 10.0.0.1 \
ipv4.dns 8.8.8.8 \
ipv4.dad-timeout 0
```

Then, the connection was restarted:

```bash
sudo nmcli connection up "Wired connection 1"
```

After applying the configuration, Kali Linux successfully connected to the NAT Network and the internet.

### 8.2 Android-x86 Network Configuration

Android-x86 was initially configured using DHCP before switching to a static IP address.

After applying the static network configuration, communication between Android-x86 and Kali Linux was successfully verified.

### 8.3 Windows 10 Installation Issue

The Windows 10 installation encountered a license terms error. Several troubleshooting attempts were performed, but the issue has not yet been resolved.

### 8.4 Key Takeaways

Through this project, I gained practical experience in:

- Virtual machine creation and configuration.
- VirtualBox NAT Network setup.
- Static IP address configuration.
- Network connectivity testing using ping.
- Shared folder and clipboard integration.
- Basic network troubleshooting.
- Creating and managing VM snapshots.
- Analyzing network traffic using Wireshark.
- Understanding suspicious network activities and potential security indicators.

## 9. Repository Structure

```text
NETWORKWALKS-MARLIANA-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP/
│
├── README.md
│
└── screenshots/
    ├── kali linux/
    │   ├── 01-virtualbox-installed.png
    │   ├── 02-natnetwork.png
    │   ├── ...
    │   └── 10b-troubleshooting-fix-nmcli.png
    │
    ├── android/
    │   ├── 01-android-general-os-memory.png
    │   ├── 02-android-storage-iso-vdi.png
    │   ├── ...
    │   └── 13-android-vm-snapshot.png
    │
    └── wireshark/
        ├── Lab 3 Result - Marliana.png
        ├── Lab 4 Result - Marliana.png
        ├── Lab 5 Result - Marliana.png
        ├── Lab 6 Result - Marliana.png
        ├── Lab 7 Result - Marliana.png
        └── Lab 8 Result - Marliana.png
```

## 10. Disclaimer

All activities documented in this repository were performed for educational purposes in a controlled virtual lab environment.

The lab is intended for learning cybersecurity fundamentals, networking, penetration testing concepts, and network traffic analysis.

Do not perform security testing against systems or networks without proper authorization.

## 11. Acknowledgment

This project was completed as part of the **NetworkWalks Cybersecurity Internship — Batch B084, Week 1**.

Special thanks to **NetworkWalks** and **Waqas Karim CCIE** for providing the learning materials and practical lab exercises.

---

**Author:** Marliana  
**Program:** NetworkWalks Cybersecurity Internship  
**Batch:** B084  
**Week:** 1  
**Project:** Cybersecurity Lab Environment Setup

**Repository:** [GitHub - Cybersecurity Lab Setup](https://github.com/LilyMarliana/NETWORKWALKS-MARLIANA-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP)
