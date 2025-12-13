# Linux Hardening Project (Parrot OS)

## Project Overview
This project demonstrates hands-on Linux system hardening techniques performed on **Parrot OS**, a Debian-based security-focused
sed Linux distribution. The goal was to reduce the system's attack surface by applying industry standard security best practices commonly
ces commonly used in enterprise and SOC environments.

This project highlights practical skills in Linux administration, system security, and documentation.

---

##Objectives
- Secure remote access to the system
- Reduce exposure to common attack vectors
- configue host-based firewall protections
- Audit system permissions and priviledged files
- Document changes clearly and professionally
- Troubleshoot SSH configuration

---

## Tools & Technology Used
- **Operating System:** Parrot OS (Linux)
- **Firewall:** UFW (Uncomplicated Firewall)
- **Services:** systemd
- **Shell:** Bash
- **Utilities:** ssh, chmod, find, sha256sum
- **Version Control:** Git & Github

---

## Hardening Tasks Performed

### System Update & Cleanup
-Updated all installed packages to the latest versions
-Removed unused and obsolete packages to minimize vulnerabilites

Commands used:
```bash
sudo apt update && sudo apt upgrade -y
sudo apt autoremove -y 
sudo apt autoclean

### SSH Hardening
- Secured remote access to prevent unauthorized login attempts
- changed default SSH port
- Disabled root login 
- Disabled password-based authentication
- Enabled idle session timeouts

Key configuration changes:
port 2222
PermitRootLogin no
PasswordAuthentication no
ClientAliveInterval 300
ClientAliveCountMax 0

###Firewall Configuration (UFW)
- Implemented a host-based firewall to control network traffic
- Enabled UFW
- Allowed SSH on a non-default port
- Denied all other incoming connections by default
- Allowed all outgoing traffic

Commands used:
sudo ufw enable
sudo ufw allow 2222/tcp
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw status verbose

---

###File & Permission Hardening
- Restricted access to sensitive directories
- Performed an audit of files with elevated privileges to identify potential exploitation risks
- Restricted user home directory access
- Generated SHA-256 hashes for critical configuration files to detect unauthorized changes

Commands used:
sudo chmod 700 /boot
sudo find / -type f \(-perm -4000 -o -perm -2000 \) -exec ls -l {} \; 2>/dev/null
chmod /home/$USER
sha256sum /etc/ssh/sshd_config
