# Week 2 – Security Planning and Testing Methodology

## 1. Performance Testing Plan

The performance testing plan focuses on monitoring the Ubuntu Server remotely while it is being administered via SSH from the Windows workstation. As the server is deployed as a headless system, all monitoring and testing is conducted using command-line tools to reflect real-world server administration practices.

### Remote Monitoring Methodology

Performance monitoring is carried out remotely over SSH using standard Linux command-line utilities. This approach ensures that system performance is observed under realistic operating conditions, without the overhead of a graphical interface.

The following metrics are monitored:
- CPU usage
- Memory usage
- Disk usage
- Network activity
- System load

Monitoring is performed while the server is idle and while administrative tasks are being executed to compare baseline and active system performance.

### Testing Approach

Performance testing is conducted in the following stages:

1. **Baseline Measurement**
   - System performance is measured immediately after boot with minimal background activity.
   - Commands such as `top`, `free -h`, and `df -h` are used to establish baseline values.

2. **Active Load Testing**
   - Administrative tasks such as package updates and file operations are performed.
   - System resource usage is observed during these tasks to identify performance changes.

3. **Observation and Analysis**
   - Differences between baseline and active states are recorded.
   - Any unusual resource spikes or bottlenecks are noted for further investigation.

This structured approach ensures consistent and repeatable performance evaluation.

---

## 2. Security Configuration Checklist

A security baseline was designed to protect the headless Ubuntu Server from unauthorised access and misconfiguration. The following checklist outlines the implemented and planned security controls.

### SSH Hardening
- SSH access restricted to authenticated users only
- Password authentication disabled in favour of key-based authentication
- Root login over SSH disabled
- SSH service configured to use a non-default port

### Firewall Configuration
- Uncomplicated Firewall (UFW) enabled
- Default policy set to deny all incoming connections
- SSH traffic explicitly allowed
- Unused ports blocked

### Mandatory Access Control
- AppArmor enabled to enforce application-level access controls
- Default security profiles applied to system services
- Ensures processes operate with the least privileges required

### Automatic Updates
- Automatic security updates enabled
- Ensures timely patching of known vulnerabilities
- Reduces risk of exploitation from outdated software

### User Privilege Management
- Principle of least privilege applied
- Administrative access restricted to authorised users only
- Use of `sudo` for elevated privileges instead of direct root access

### Network Security
- Host-only network used for SSH communication
- Server isolated from public networks
- NAT used solely for controlled outbound internet access

---

## 3. Threat Model and Mitigation Strategies

A threat model was developed to identify potential security risks to the system and define mitigation strategies.

### Threat 1: Brute-Force SSH Attacks
**Description:**  
Attackers may attempt to gain unauthorised access by repeatedly guessing SSH credentials.

**Mitigation:**
- Disable password-based SSH authentication
- Use key-based authentication
- Change default SSH port
- Implement firewall rules to limit access

---

### Threat 2: Privilege Escalation
**Description:**  
A compromised user account could be used to gain elevated privileges and control the system.

**Mitigation:**
- Restrict administrative privileges
- Use `sudo` with logging enabled
- Disable direct root login
- Apply mandatory access control using AppArmor

---

### Threat 3: Unpatched System Vulnerabilities
**Description:**  
Outdated software may contain known vulnerabilities that attackers can exploit.

**Mitigation:**
- Enable automatic security updates
- Regularly update system packages
- Monitor update logs to ensure patches are applied successfully

---

## Week 2 Summary

This phase focused on planning a secure and reliable operating environment for the headless Ubuntu Server. A structured performance testing methodology was designed to monitor system behaviour under different conditions. A comprehensive security baseline was established, addressing authentication, access control, network security, and system maintenance. Additionally, a threat model was developed to identify key risks and appropriate mitigation strategies, providing a strong foundation for secure system operation in subsequent phases.
