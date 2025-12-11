# 🗓️ Week 1: System Planning and Distribution Selection

This week focuses on planning the system architecture, selecting the server distribution, and documenting the initial setup.

---

## 1. 🧩 System Architecture Diagram

Below is the system architecture diagram showing the two-system setup, network connection, and planned IP addresses.

![System Architecture Diagram](architecture.png)

> **⚠️ Note on Infrastructure & Network Environment**
> Because I am working on this project across multiple physical locations (e.g., University Lab and Home), my network environment changes. You will notice that:
> * **IP Addresses** vary throughout the weeks (e.g., `10.208.115.17` vs `10.208.115.132`) as they are assigned dynamically by different DHCP servers.
> * **Workstation Terminals** may show different prompts (e.g., `vboxuser@Ubuntu` or `sakibbaa@fedora`) depending on which machine I was physically using to connect via SSH at the time.
>
> Regardless of the location, the architecture remains a **Dual-System setup**, and all server administration is performed strictly via SSH.

---

## 2. 💿 Distribution Selection Justification

For my server system, I utilized **Ubuntu Desktop 24.04 LTS**, but I have configured it to function as a **headless server**.

### Justification & Configuration

- **Resource Availability:** I leveraged the Ubuntu Desktop ISO to ensure broad driver compatibility with the physical hardware I am using for this node.

- **Server Transformation:** Although the installation includes a GUI, I am strictly enforcing a "headless" workflow:
  * All administration is performed remotely via SSH.
  * I have configured the system to boot to `multi-user.target` (CLI only) to prevent the GUI from loading, strictly enforcing a headless environment.
  * I have disabled unnecessary background services (like `snapd` in Week 6) to optimize resources.

- **Security Module:** Like the Server edition, Ubuntu Desktop uses **AppArmor** by default, allowing me to fulfill the Mandatory Access Control requirements of Phase 5.

---

## 3. 🖥️ Workstation Configuration Decision

I am using a **Fedora Desktop VM** as my administrative workstation, which runs on a separate physical machine from my **Ubuntu Server VM**.

This approach fully meets the *dual-system architecture* requirement.  
It provides a dedicated, isolated Linux environment to perform all remote administration tasks via SSH.  
This setup mirrors a professional environment where administrators use their own machines to manage remote servers — helping to develop essential command-line and remote management skills.

---

## 4. 🌐 Network Configuration Documentation

Since my server and workstation VMs are on two different physical host machines, a "Host-Only Network" (like the one in my initial diagram) is not possible.

Instead, both VMs use a **"Bridged Adapter"** setting in VirtualBox. This connects both VMs directly to my physical home network, allowing them to communicate. My documentation and diagram will be updated to reflect this correct "Bridged" setup.

| Configuration Item | Setting / Value |
|---------------------|-----------------|
| **VirtualBox Network Type (Both VMs)** | **Bridged Adapter** |
| **Physical Network** | Home LAN (`10.208.115.0/24`) |
| **Server IP (Ubuntu)** | `10.208.115.17` (Dynamic) |
| **Workstation IP (Fedora)** | (Will be assigned by DHCP) |

> **Note:** My `ip addr` output confirms this bridged setup. I will later configure a *static* IP for the server (e.g., `10.208.115.50`) as required.

---

## 5. ⚙️ System Specifications

Here are the initial specifications for the headless Ubuntu server, captured from the direct console.

### 🧠 `uname -a`
```bash
Linux Ubuntu 6.14.0-35-generic #3524.04.1-Ubuntu SMP PREEMPT_DYNAMIC Tue Oct 14 13:55:17 UTC 2 x86_64 x86_64 x86_64 GNU/Linux;
```
---

### Memory `free -h`
```bash
              total         used         free      shared   buff/cache   available
Mem:          7.8Gi        1.0Gi        6.0Gi        32Mi        1.1Gi       6.8Gi
Swap:            0B           0B           0B;
```

### 📁 `df -h`
```bash
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           795M  1.7M  793M   1% /run
/dev/sda2       251G  5.3G  233G   3% /
tmpfs           3.9G     0  3.9G   0% /dev/shm
tmpfs           5.0M  8.0K  5.0M   1% /run/lock
tmpfs           795M   152K  795M   1% /run/user/1000
```

### 🌍 `ip addr`
```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever

2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e9:b8:6d brd ff:ff:ff:ff:ff:ff
    inet 10.208.115.17/24 brd 10.208.115.255 scope global dynamic noprefixroute enp0s3
       valid_lft 431737sec preferred_lft 431737sec
    inet6 fe80::a00:27ff:fee9:b86d/64 scope link
       valid_lft forever preferred_lft forever
```

### 🧾 `lsb_release -a`
```bash
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 24.04.3 LTS
Release:        24.04
Codename:       noble
```

---
## References

[1] Canonical Ltd., “Ubuntu 24.04 LTS (Noble Numbat),” *Ubuntu Releases*, 2024. [Online]. Available: https://releases.ubuntu.com/24.04/

[2] Oracle, “Oracle VM VirtualBox User Manual,” *VirtualBox.org*, 2024. [Online]. Available: https://www.virtualbox.org/manual/

---

[Back to Home](README.md)


