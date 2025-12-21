# Week 1 – System Planning and Distribution Selection

## 1. System Architecture Overview

This system consists of a Windows host machine acting as the workstation and an Ubuntu Server LTS virtual machine deployed as a headless server. Oracle VirtualBox is used as the virtualization platform. The server does not use a graphical interface and is administered remotely using Secure Shell (SSH) from the Windows workstation via PowerShell.

Two virtual network interfaces are configured to separate internal communication from external connectivity. A host-only network is used to enable secure local communication between the workstation and the server, while Network Address Translation (NAT) provides controlled internet access for software updates and package management.

---

## 2. System Architecture Diagram

```mermaid
flowchart LR
    W[Windows Host PC\nWorkstation\nPowerShell SSH Client\nIP 192.168.56.1]

    S[Ubuntu Server LTS\nHeadless Server VM\nSSH Enabled\nenp0s8 192.168.56.x\nenp0s3 10.0.2.x]

    H[Host-only Network\nvboxnet0\n192.168.56.0/24]
    N[NAT Network\n10.0.2.0/24]
    I[Internet]

    W -->|SSH| H
    H --> S
    S -->|NAT| N
    N --> I
