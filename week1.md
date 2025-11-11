# Week 1: System Planning and Distribution Selection

This week focuses on planning the system architecture, selecting the server distribution, and documenting the initial setup.

## 1. System Architecture Diagram

Below is the system architecture diagram showing the two-system setup, network connection, and planned IP addresses.

![System Architecture Diagram](architecture.png)
*(Note: You must upload your diagram image file as `architecture.png` to your GitHub repository for this to appear.)*

## 2. Distribution Selection Justification

For my server system, I selected **Ubuntu Server 22.04 LTS**. The primary alternative I considered was **Fedora Server**.

My justification for this choice is as follows:

* **Stability vs. Bleeding-Edge:** I chose Ubuntu Server because its Long-Term Support (LTS) version provides a stable, reliable platform with security updates for 5 years. This is a critical feature for a server environment, and I value this stability over Fedora Server's more frequent, bleeding-edge release cycle.
* **Security Module:** Ubuntu uses **AppArmor** by default, while Fedora uses **SELinux**. As implementing Mandatory Access Control is a requirement for Phase 5, I will be focusing on learning and configuring AppArmor for this project.
* **Package Management:** I am more familiar with the `apt` package manager and `.deb` packages used by Ubuntu, which will allow me to configure the system more efficiently.
* **Community and Documentation:** Ubuntu has an exceptionally large user community and a vast amount of online documentation. As a student, this extensive support network is a significant advantage for troubleshooting and learning.

## 3. Workstation Configuration Decision

*[This is our next task. Here you will justify your workstation choice.]*

## 4. Network Configuration Documentation

*[We will fill this in after Task 3. Here you will document your VirtualBox network settings and IP addresses.]*

## 5. System Specifications

*[We will fill this in last. Here you will add the CLI output from your server: `uname`, `free`, `df -h`, `ip addr`, and `lsb_release`.]*

---
[Back to Home](README.md)
