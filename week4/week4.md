# Week 4 – Initial System Configuration and Security Implementation

## Administrative Constraint

All server configuration tasks in this phase were performed remotely via SSH from the workstation. No direct console or local access to the server was used at any stage. This reflects real-world server administration practices and complies with the module’s administrative constraint.

---

## 1. SSH Configuration with Key-Based Authentication

SSH was configured to use key-based authentication to improve security and prevent password-based login attacks.

### SSH Key Generation (Workstation)

An SSH key pair was generated on the workstation using the following command:

```bash
ssh-keygen -t ed25519
```

![ssh key generation](../images/week4/ssh_key_generation.png)
*Figure 1: SSH key pair generation on the workstation to enable key-based authentication.*


![ssh key login](../images/week4/ssh_key_login.png)
*Figure 2: Successful SSH login to the server without a password, confirming key-based authentication.*

---

## SSH Hardening Configuration

The SSH service was hardened to reduce the risk of unauthorised access and brute-force attacks. Password-based authentication was disabled, and direct root login was prevented to enforce secure access control.

The SSH daemon configuration file was edited remotely via SSH using the following command:

```bash
sudo nano /etc/ssh/sshd_config
```

The following configuration options were applied:
PasswordAuthentication no
PermitRootLogin no
PubkeyAuthentication yes

After making the changes, the configuration was validated to ensure there were no syntax errors:

```bash
sudo sshd -t
```

The SSH service was then restarted to apply the new settings:

```bash
sudo systemctl restart ssh
```

![sshd hardening](../images/week4/sshd_hardening_config.png)
*Figure 3: SSH daemon configuration showing password authentication disabled and root login prevented.*

Successful passwordless SSH login confirmed that key-based authentication was correctly enforced.
---

## Firewall Configuration Evidence

![ufw rules](../images/week4/ufw_firewall_rules.png)
*Figure 4: UFW firewall ruleset showing SSH access restricted to a single trusted workstation IP address.*

---

## User and Privilege Management Evidence

![user management](../images/week4/user_management.png)
*Figure 5: Creation of a non-root administrative user and assignment of sudo privileges.*

![admin sudo privileges](../images/week4/adminuser_sudo_privileges.png)
*Figure 6: Demonstration of privilege escalation using sudo by a non-root administrative user.*
