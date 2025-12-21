# Week 3 – Application Selection and Performance Evaluation Planning

## 1. Application Selection Matrix

To evaluate system performance under different workload conditions, a range of applications representing distinct workload types were selected. Each application was chosen based on its ability to stress specific system resources in a controlled and measurable way.

| Workload Type        | Application        | Justification |
|----------------------|--------------------|---------------|
| CPU-intensive        | stress-ng          | Designed to generate high CPU load and simulate real-world computational stress scenarios. |
| RAM-intensive        | stress-ng (vm)     | Allows controlled memory allocation and pressure testing of system RAM. |
| I/O-intensive        | fio                | Commonly used benchmarking tool for testing disk read/write performance and I/O throughput. |
| Network-intensive    | iperf3             | Widely used for measuring network bandwidth, latency, and throughput between systems. |
| Server Application   | Apache Web Server  | Represents a real-world server workload handling client requests and background services. |

These applications collectively provide a comprehensive overview of system performance across different resource domains.

---

## 2. Installation Documentation (SSH-Based)

All applications were installed remotely on the Ubuntu Server using SSH from the Windows workstation. The following commands were executed on the server.

### System Update
```bash
sudo apt update && sudo apt upgrade -y
```

![update](../images/week3/update.png)
*Figure 1: System update performed using the APT package manager prior to application installation.*

```bash
ssudo apt install stress-ng -y
```
![stress](../images/week3/stress.png)
*Figure 2: Output from the `stress-ng` tool demonstrating CPU and memory intensive workload execution.*

```bash
sudo apt install fio -y
```
![fio](../images/week3/fio.png)
*Figure 3: Disk I/O performance testing using the `fio` benchmarking tool.*

```bash
sudo apt install iperf3 -y
```
![iperf3](../images/week3/iperf3.png)
*Figure 4: Network performance testing conducted using `iperf3` to measure throughput.*

```bash
sudo apt install apache2 -y
```
![apache](../images/week3/apache.png)
*Figure 5: Apache web server installation and service status confirming server application deployment.*

Each installation was performed using the APT package manager to ensure software integrity and compatibility.

---

## 3. Expected Resource Profiles

The expected resource profiles describe the anticipated impact of each selected application on system resources. These profiles provide a baseline for comparing observed performance during testing.

| Application            | CPU Usage      | Memory Usage   | Disk I/O Usage | Network Usage |
|------------------------|----------------|----------------|----------------|----------------|
| stress-ng (CPU test)   | High           | Low            | Minimal        | None           |
| stress-ng (RAM test)   | Moderate       | High           | Minimal        | None           |
| fio                    | Low            | Low            | High           | None           |
| iperf3                 | Low            | Low            | Minimal        | High           |
| Apache Web Server      | Low–Moderate   | Low–Moderate   | Moderate       | Moderate       |

CPU-intensive workloads are expected to place sustained load on the processor, while memory-intensive workloads increase RAM usage. Disk I/O tests generate frequent read and write operations, and network-intensive workloads consume available bandwidth. Server applications such as Apache are expected to use a combination of resources depending on request load.

---

## 4. Monitoring Strategy

System performance is monitored remotely via SSH using standard Linux command-line tools. Monitoring is performed during idle states and while each application is actively running to identify changes in resource usage.

### Monitoring Tools and Metrics

- **CPU and Memory Monitoring**
  - `top` is used to observe real-time CPU utilisation, running processes, and memory usage.
  - `free -h` is used to verify memory consumption during RAM-intensive workloads.

- **Disk I/O Monitoring**
  - `df -h` is used to monitor disk space usage.
  - Disk activity is observed during `fio` execution to identify I/O pressure.

- **Network Monitoring**
  - `ip addr` is used to confirm active network interfaces.
  - `iperf3` output is used to measure bandwidth and network throughput.

- **Service Monitoring**
  - `systemctl status apache2` is used to confirm that the Apache web server is running correctly during testing.

### Measurement Approach

Each workload is executed individually to isolate its impact on system performance. Baseline measurements are taken before execution, followed by continuous observation while the application is running. Results are recorded and compared against the expected resource profiles to evaluate system behaviour under different workload conditions.

---

## Week 3 Reflection

During Week 3, I developed a deeper understanding of how different workload types impact system performance by selecting and preparing applications that stress specific system resources. Choosing tools such as `stress-ng`, `fio`, `iperf3`, and Apache helped me recognise how CPU, memory, disk I/O, network, and server-based workloads behave differently and why it is important to test each resource independently.

One key learning outcome from this phase was the importance of defining expected resource profiles before conducting performance tests. By anticipating how each application should affect CPU usage, memory consumption, disk activity, and network throughput, I was able to create a clear baseline against which real performance results can later be compared. This improved my understanding of performance evaluation as a structured and methodical process rather than simple observation.

The monitoring strategy reinforced my confidence in using command-line tools such as `top`, `free`, `df`, and `ip addr` to observe system behaviour in real time. Monitoring the system remotely via SSH highlighted how performance analysis is commonly carried out in real-world server environments without relying on graphical interfaces.

Overall, this phase strengthened my ability to plan performance testing logically and professionally. The skills developed in application selection, expected resource analysis, and monitoring preparation provide a strong foundation for conducting and interpreting practical performance tests in the following weeks.

---