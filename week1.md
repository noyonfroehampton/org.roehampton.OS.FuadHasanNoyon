# Week 1: System Planning and Distribution Selection

This week focuses on planning the system architecture, selecting the server distribution, and documenting the initial setup.

## 1. System Architecture Diagram

Below is the system architecture diagram showing the two-system setup, network connection, and planned IP addresses.

![System Architecture Diagram](architecture.png)

## 2. Distribution Selection Justification

For my server system, I selected **Ubuntu Server 22.04 LTS**. The primary alternative I considered was **Fedora Server**.

My justification for this choice is as follows:

* **Stability vs. Bleeding-Edge:** I chose Ubuntu Server because its Long-Term Support (LTS) version provides a stable, reliable platform with security updates for 5 years. This is a critical feature for a server environment, and I value this stability over Fedora Server's more frequent, bleeding-edge release cycle.
* **Security Module:** Ubuntu uses **AppArmor** by default, while Fedora uses **SELinux**. As implementing Mandatory Access Control is a requirement for Phase 5, I will be focusing on learning and configuring AppArmor for this project.
* **Package Management:** I am more familiar with the `apt` package manager and `.deb` packages used by Ubuntu, which will allow me to configure the system more efficiently.
* **Community and Documentation:** Ubuntu has an exceptionally large user community and a vast amount of online documentation. As a student, this extensive support network is a significant advantage for troubleshooting and learning.

## 3. Workstation Configuration Decision

I am using a Fedora Desktop VM as my administrative workstation, which runs on a separate physical machine from my Ubuntu Server VM.

This approach is fully compliant with the "dual-system architecture" requirement. It provides a dedicated, isolated Linux environment to perform all remote administration tasks via SSH. This setup mirrors a professional environment where administrators use their own machines to manage remote servers, thus developing key command-line and remote management skills.

## 4. Network Configuration Documentation

## 4. Network Configuration Documentation

Since my server and workstation VMs are on two different physical host machines, a standard VirtualBox internal network will not work.

To enable communication, both VMs will use a **"Bridged Adapter"** setting in VirtualBox. This connects both VMs directly to my physical home network, where they will each get an IP address from my router, allowing them to communicate.

* **VirtualBox Network Type (Both VMs):** Bridged Adapter.
* **Physical Network:** My home LAN (e.g., 192.168.1.0/24).
* **Server IP (Ubuntu):** I will configure a static IP *inside* the Ubuntu OS (e.g., **192.168.1.10**) to ensure it's always reachable at the same address.
* **Workstation IP (Fedora):** This can be assigned by DHCP from my router (e.g., **192.168.1.11**).

## 5. System Specifications

*[We will fill this in last. Here you will add the CLI output from your server: `uname`, `free`, `df -h`, `ip addr`, and `lsb_release`.]*

---
[Back to Home](README.md)
