<div align="center">

# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice**

![Skill](https://img.shields.io/badge/Skill-Cybersecurity-red) ![VirtualBox](https://img.shields.io/badge/VirtualBox-7.x-blue) ![Kali](https://img.shields.io/badge/Kali_Linux-2026.x-black) ![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-teal) ![Wireshark](https://img.shields.io/badge/Wireshark-SOC_Labs-1679A7) ![NetworkWalks](https://img.shields.io/badge/NetworkWalks-Internship-darkred)

*Networkwalks Cybersecurity Internship · Batch B084 · Week 1 · Project Module 1 + Extras*

</div>

---

## 📌 Project Overview

This project sets up a virtual cybersecurity lab on my own laptop using VirtualBox and Kali Linux. It is a private, controlled environment where traffic analysis and other security-testing activities can be practiced safely and repeatably.

> ⚠️ **Ethics & legality:** Every machine in this lab is my own virtual machine on my own device. Nothing was tested against systems I do not own or have written permission to test.

## 🎯 Objectives

- [x] Install VirtualBox and import Kali Linux
- [x] Create a NAT Network in `10.0.0.0/24`
- [x] Enable shared clipboard, drag & drop and a shared `Downloads` folder
- [x] Static IP `10.0.0.2/24` for Kali with full Internet access
- [x] Take a clean snapshot
- [x] Extra: Android-x86 9.0 VM (`10.0.0.9/24`), ping tested both ways
- [x] Extra: 6 Wireshark SOC labs (Labs 3 to 8), all 100/100
- [ ] Extra: Windows 10 VM (not completed yet)

## 🧰 Environment

| Item | Detail |
|---|---|
| Host OS | Windows 11 |
| Laptop | Dell Latitude 7300 |
| CPU | Intel Core i7-8665U (4 cores, 8 threads), virtualization enabled |
| RAM | 16 GB DDR4 |
| Storage | 238 GB SSD (C: 119 GB, plus drive D:) |
| VirtualBox | 7.2.22 |
| Kali Linux | 2026.3 (4096 MB RAM, 4 CPU, 80 GB dynamic disk) |

| Machine | Role | IP Address | Network |
|---|---|---|---|
| Kali Linux | Attacker / analyst | `10.0.0.2/24` | NatNetwork |
| Android-x86 9.0 | Target (extra) | `10.0.0.9/24` | NatNetwork |
| Windows 10 | Target (planned) | `10.0.0.10/24` | NatNetwork |

Gateway `10.0.0.1` · DNS `8.8.8.8`

---

## 🛠️ Implementation

**1. VirtualBox 7.2.22** installed from the official site.

<img src="screenshots/kali%20linux/01-virtualbox-installed.png" width="480">

**2. NAT Network** `NatNetwork`, prefix `10.0.0.0/24`, DHCP enabled.

<img src="screenshots/kali%20linux/02-natnetwork.png" width="560">

**3. Kali Linux** imported and attached to `NatNetwork`, Promiscuous Mode: Allow All.

<img src="screenshots/kali%20linux/03-kali-imported.png" width="560">
<img src="screenshots/kali%20linux/04-kali-nat-network-adapter.png" width="560">

**4. Clipboard, drag & drop, shared folder** (Bidirectional; host `Downloads` shared with auto-mount).

<img src="screenshots/kali%20linux/05a-shared-clipboard.png" width="560">
<img src="screenshots/kali%20linux/05b-drag-and-drop.png" width="560">
<img src="screenshots/kali%20linux/06b-shared-folder-configured.png" width="560">
<img src="screenshots/kali%20linux/06c-shared-folder-mounted.png" width="560">

```bash
sudo usermod -aG vboxsf $USER
sudo reboot
ls /media/sf_Downloads
```

**5. Static IP** set from the terminal (see Troubleshooting):

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.method manual ipv4.addresses 10.0.0.2/24 ipv4.gateway 10.0.0.1 ipv4.dns 8.8.8.8 ipv4.dad-timeout 0
sudo nmcli connection up "Wired connection 1"
```

<img src="screenshots/kali%20linux/07a-kali-ip-address.png" width="480">
<img src="screenshots/kali%20linux/07b-kali-manual-ip-settings.png" width="480">

**6. Verify** Internet and DNS:

```
--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss
--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss
```

<img src="screenshots/kali%20linux/08a-internet-test-ping-ip.png" width="480">
<img src="screenshots/kali%20linux/08b-internet-test-ping-dns.png" width="480">

**7. Snapshot** `Kali-WK1-Clean-Setup` taken while the VM was powered off.

<img src="screenshots/kali%20linux/09-vm-snapshot-taken.png" width="480">

---

## ➕ Extra Tasks

### Android-x86 9.0 VM ✅
`Android9-Lab` (Linux, Other Linux 64-bit), 2048 MB RAM, about 10 GB VDI, NatNetwork, VBoxVGA with 3D acceleration off. Installed to disk with GRUB. DHCP gave `10.0.0.4`, then I set the static IP `10.0.0.9/24`. Snapshot: `Android-WK1-Clean-Setup`.

```
Android -> Kali     (10.0.0.2)   0% packet loss
Android -> Internet (8.8.8.8)    0% packet loss
Kali    -> Android  (10.0.0.9)   0% packet loss
```

<img src="screenshots/android/11-android-ip-after-static-10.0.0.9.png" width="300">
<img src="screenshots/android/12-android-ping-kali-and-internet.png" width="300">
<img src="screenshots/android/12b-kali-ping-android.png" width="300">

### Wireshark SOC Labs ✅

| Lab | Title | What I practiced | Score |
|---|---|---|---|
| 3 | Identify the Attacker's IP | Filtering TCP SYN packets, finding attacker and target | 100/100 |
| 4 | Follow TCP Stream | Reading a plain-text chat | 100/100 |
| 5 | Follow TCP Stream, Part 2 | Hidden HTML comment and a downloaded text file | 100/100 |
| 6 | HTTP Plain Text Credentials | Clear-text login in an HTTP POST form | 100/100 |
| 7 | Catch the Brute Force Attacker | Many failed FTP logins from one source | 100/100 |
| 8 | Catch the Call Scammer | Investigating a captured VoIP call | 100/100 |

Filters I used:

```
tcp.flags.syn == 1                              # packets with the SYN flag set
tcp && !(tcp.port == 80 || tcp.port == 443)     # hide normal web traffic
http.request.method == "POST"                   # form submissions
ftp.response.code == 530                        # failed FTP logins
```

| Lab 3 | Lab 4 | Lab 5 |
|:-:|:-:|:-:|
| <img src="screenshots/wireshark/Lab%203%20Result%20-%20Marliana.png" width="240"> | <img src="screenshots/wireshark/Lab%204%20Result%20-%20Marliana.png" width="240"> | <img src="screenshots/wireshark/Lab%205%20Result%20-%20Marliana.png" width="240"> |

| Lab 6 | Lab 7 | Lab 8 |
|:-:|:-:|:-:|
| <img src="screenshots/wireshark/Lab%206%20Result%20-%20Marliana.png" width="240"> | <img src="screenshots/wireshark/Lab%207%20Result%20-%20Marliana.png" width="240"> | <img src="screenshots/wireshark/Lab%208%20Result%20-%20Marliana.png" width="240"> |

### Windows 10 VM ⏳ (not completed yet)
This is where I was stuck the longest. Windows setup shows *"Windows cannot find the Microsoft Software License Terms"*. I downloaded a new ISO, checked that it was healthy and turned off Hyper-V related features, but the error stayed. I will update this repo when it works. Planned: `Windows10-Lab`, 4096 MB RAM, 40 GB VDI, NatNetwork, `10.0.0.10/24`.

---

## 🧯 Troubleshooting

**Kali had no IP.** `eth0` was stuck in "connecting (getting IP configuration)". I tried different settings several times. The fix was setting the static IP with `nmcli` and `ipv4.dad-timeout 0` (commands above). After that Internet and DNS worked.

<img src="screenshots/kali%20linux/10a-troubleshooting-connecting.png" width="480">
<img src="screenshots/kali%20linux/10b-troubleshooting-fix-nmcli.png" width="560">

**Kali froze on reboot.** After adding my user to `vboxsf` it stayed on a black screen. I used Machine > Reset and it booted normally.

**Drive C was full.** I kept VM files, downloads and snapshots on drive D.

**Promiscuous Mode was on "Deny".** I changed it to "Allow All" to match the task.

**Wireshark Lab 3.** One answer was wrong and I got 90%. I did it again, read the questions more carefully and got 100%.

---

## 📚 Lessons Learned

- I thought a lab like this needs a gaming laptop. In fact a modest laptop can run several virtual machines.
- This was my first time with Wireshark. I was surprised the labs run in the browser, and I enjoyed answering the questions. It was my favourite part.
- A snapshot gives me a clean state to go back to if something breaks.
- Plain-text protocols (HTTP, FTP, an old chat tool) show everything to anyone who captures the traffic, so encryption like HTTPS matters.
- My advice for anyone starting: just try it. If it feels hard, do not give up. Take a break, then continue.

---

<div align="center">

**Networkwalks Cybersecurity Internship · Instructor: Waqas Karim CCIE**
*All activity performed on my own virtual lab for educational purposes.*

</div>
