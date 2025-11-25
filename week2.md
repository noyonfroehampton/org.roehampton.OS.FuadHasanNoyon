# 🗓️ Week 2: Security Planning and Testing Methodology

This journal entry outlines the complete planning phase for my server, as required by the Phase 2 deliverables. It includes the performance testing plan, a comprehensive security configuration checklist, and a threat model.

---

## 1. Performance Testing Plan

This plan describes the remote monitoring methodology and testing approach I will use to evaluate the server's performance in Phase 6. All tests will be conducted from my Fedora workstation via SSH to the Ubuntu server.

| Metric to Measure (from Phase 6) | Command-Line Tool | My Planned Methodology & Justification |
| :--- | :--- | :--- |
| **CPU Usage** | `htop` | I will run `ssh user@server_ip "htop"` to get a real-time, per-process view of CPU load. |
| **Memory Usage** | `free -h` | I will run `ssh user@server_ip "free -h"` before and after tests to check "used" vs. "available" memory. |
| **Disk I/O** | `iostat` | I will use `ssh user@server_ip "iostat"` to measure disk read/write statistics and identify bottlenecks. |
| **Network Performance** | `ping` | I will use `ping server_ip` from my workstation to measure packet latency. |
| **Network Throughput** | `iperf3` | I plan to install `iperf3` on both VMs to run a test and measure the maximum network bandwidth. |

---

## 2. 🛡️ Security Configuration Checklist

This is my detailed checklist for implementing the server's security configuration, as required by the brief. I will use this as my guide for Phase 4 and Phase 5.

### SSH Hardening
- [ ] Create a new non-root administrative user with `sudo` privileges.
- [ ] Generate SSH key pairs on my workstation.
- [ ] Copy the public key to the new user on the server.
- [ ] Edit `/etc/ssh/sshd_config` on the server to:
  - [ ] Set `PermitRootLogin no`.
  - [ ] Set `PasswordAuthentication no`.
- [ ] Restart the SSH service.

### Firewall Configuration
- [ ] Install `ufw` (Uncomplicated Firewall).
- [ ] Set `ufw` default to `deny incoming` and `allow outgoing`.
- [ ] Create a `ufw` rule to allow SSH (on the correct port) *only* from my Fedora workstation's IP.
- [ ] Enable `ufw`.

### Mandatory Access Control (MAC)
- [ ] As per my `week1.md` file, my server is Ubuntu, so I will use **AppArmor**.
- [ ] Verify AppArmor is active using `aa-status`.
- [ ] Document the AppArmor profiles currently in "enforce" mode.
- [ ] Investigate and document the profile for `sshd`.

### Automatic Updates
- [ ] Verify the `unattended-upgrades` package is installed.
- [ ] Check the configuration in `/etc/apt/apt.conf.d/` to ensure security updates are enabled.
- [ ] Document how to check the logs for automatic updates.

### User Privilege Management
- [ ] Confirm my new administrative user is in the `sudo` group.
- [ ] Document the `sudo` configuration (`/etc/sudoers`) and how it grants privileges.

### Network Security
- [ ] Run `ss -tulpn` (or `netstat -tulpn`) to list all listening services.
- [S] Justify every open port (e.g., port 22 for SSH).
- [ ] Ensure no unnecessary services are running and listening.

---

## 3. ☣️ Threat Model

This model identifies at least 3 specific security threats and the mitigation strategies I plan to implement, as required by the brief.

| Threat ID | Specific Security Threat | Potential Impact | Planned Mitigation Strategy (from my checklist) |
| :--- | :--- | :--- | :--- |
| **T-001** | **Brute-Force Attack** | An attacker guesses my user's password via SSH and gains unauthorized access. | **SSH Hardening:** I will disable `PasswordAuthentication` and enforce SSH key-only login. This makes a brute-force *password* attack impossible. |
| **T-002** | **Network Port Scanning & Exploitation** | An attacker scans my server's IP, finds an open port for an unpatched service, and exploits it. | **Firewall Configuration:** I will use `ufw` to `deny incoming` traffic by default. Only the SSH port will be open, and *only* to my workstation's IP. |
| **T-003** | **Privilege Escalation** | An attacker gains entry as a standard user (or via a compromised service) and manages to get `root` access. | **User Privilege Management:** I will disable root login via SSH (`PermitRootLogin no`) and use a non-root admin account. |
| **T-004** | **Known Vulnerability Exploit** | A new critical vulnerability is discovered in the OS, and an attacker exploits it before I can patch. | **Automatic Updates:** I will configure `unattended-upgrades` to automatically apply critical security patches. |

[Back to Home](README.md)
