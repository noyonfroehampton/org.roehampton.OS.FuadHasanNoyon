# 🗓️ Week 3: Application Selection for Performance Testing

This week, I am planning the applications I will use for performance testing in Phase 6. This journal entry documents the Application Selection Matrix, the installation commands, expected resource profiles, and the monitoring strategy for each application, as required by the Phase 3 deliverables.

---

## 1. 📊 Application Selection Matrix

I have selected the following applications to represent different workload types on my server. This will allow me to conduct a well-rounded performance evaluation.

| Workload Type | Application Selected | Justification for Selection |
| :--- | :--- | :--- |
| **CPU-intensive** | `sysbench` (CPU test) | A standard and reliable benchmarking tool. I will use its CPU test to run complex calculations and push the processor to 100% capacity. |
| **RAM-intensive** | `stress-ng` (memory test) | A powerful tool designed to stress-test system components. I will use its memory stressors to allocate and use large amounts of RAM, testing memory capacity and speed. |
| **I/O-intensive** | `sysbench` (fileio test) | I will use `sysbench` again, but this time its file I/O test. This allows me to create large test files and measure disk read/write throughput and latency. |
| **Network-intensive**| `iperf3` | As planned in Week 2, this is the standard tool for measuring maximum network bandwidth (throughput) between my workstation and the server. |
| **Server Application**| `nginx` | A lightweight, high-performance web server. This represents a real-world server application. I will measure its service response time and network performance. |

---

## 2. 🛠️ Installation Documentation

All installations will be performed remotely from my Fedora workstation via SSH. Here are the exact commands I will use to install each application on the Ubuntu server.

```bash
# Update package lists
sudo apt update
```
```bash
# Install sysbench (for CPU and I/O)
sudo apt install sysbench
```
```bash
# Install stress-ng (for RAM)
sudo apt install stress-ng
```
```bash
# Install iperf3 (for Network)
sudo apt install iperf3
```
```bash
# Install nginx (for Server Application)
sudo apt install nginx
```
## 3. 📈 Expected Resource Profiles

Here is what I anticipate seeing in my monitoring tools when I run each test.

### sysbench (CPU)
* **htop:** I expect to see 100% usage on one or more CPU cores.
* **free -h:** Memory usage should remain low and stable.
* **iostat:** Disk I/O should be minimal.

### stress-ng (RAM)
* **free -h:** I expect "available" memory to drop significantly as the tool allocates RAM.
* **htop:** I will see the stress-ng processes using large amounts of memory (RES column). CPU usage may be moderate.

### sysbench (I/O)
* **iostat:** I expect to see very high read/write numbers (kB_rd/s, kB_wrtn/s).
* **htop:** I expect the sysbench process to have a high 'D' (Disk Sleep) state, indicating it's waiting for the disk.

### iperf3 (Network)
* **iperf3 client:** The tool itself will report the network throughput in Mbits/sec.
* **htop:** I expect to see moderate CPU usage from the iperf3 process.

### nginx (Server)
* **Baseline:** With no traffic, I expect nginx to use very low CPU and RAM.
* **Under Load:** When I test it (e.g., with a tool like `ab` - Apache Benchmark), I expect to see CPU usage increase as it handles connections.



## 4. 🔬 Monitoring Strategy

This is my specific plan to measure each application, based on my Week 2 testing plan3.

| Application | Test Command (Example) | How I Will Monitor It (in a separate SSH terminal) |
|---|---|---|
| **sysbench (CPU)** | `sysbench cpu --threads=2 run` | I will have `htop` running to watch the CPU cores spike to 100%. |
| **stress-ng (RAM)** | `stress-ng --vm 1 --vm-bytes 1G` | I will run `free -h` before and during the test to document the drop in available memory. |
| **sysbench (I/O)** | `sysbench fileio --file-test-mode=rndrw run` | I will have `iostat -d 2` running to get live updates on disk read/write speeds every 2 seconds. |
| **iperf3 (Network)** | `iperf3 -s` (on server), `iperf3 -c [server_ip]` (on workstation) | The `iperf3` client on my workstation will provide the final performance report. |
| **nginx (Server)** | `systemctl status nginx` (check service) | I will use `ping` to measure latency 4 and a tool like `curl` to measure the time to get a response. |

[Back to Home](README.md)
