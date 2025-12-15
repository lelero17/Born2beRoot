# Born2beRoot

_This project has been created as part of the 42 curriculum by lemmerli._

## Description

Born2beRoot is a system administration project that introduces virtualization, server setup, and security configuration. The goal is to create a virtual machine running Debian with strict security policies including encrypted partitions, password policies, sudo configuration, SSH hardening, and automated system monitoring.

## Instructions

### Requirements
- VirtualBox (or UTM)
- Debian 13 ISO (latest stable)

### Setup
1. Create VM with encrypted LVM partitions (see subject for structure)
2. Configure sudo with strict rules
3. Set up SSH on port 4242 (root login disabled)
4. Configure UFW firewall (only port 4242 open)
5. Implement strong password policy
6. Create monitoring script (`/usr/local/bin/monitoring.sh`)
7. Set up cron job (every 10 minutes)

### Evaluation
- Start VM and demonstrate configuration
- Signature file must match VM disk signature

## Project Description

### Operating System Choice: Debian
**Pros:**
- Beginner-friendly
- Extensive documentation and community support
- Stable and reliable (perfect for servers)
- Simple package management (apt)

**Cons:**
- Less enterprise-focused than Rocky
- Older packages (due to stability focus)

**vs Rocky Linux:**
- Rocky: Enterprise (RHEL-based), dnf/yum, SELinux
- Debian: Community-driven, apt/dpkg, AppArmor

### Design Choices

**Partitioning:**
- `/boot` (500M, unencrypted) - Required for GRUB
- Encrypted LVM with 7 logical volumes:
  - root (10G), swap (2.3G), home (5G)
  - var (3G), srv (3G), tmp (3G), var-log (4G)
- Encryption provides data protection if disk is stolen
- LVM allows flexible partition resizing

**Security Policies:**
- Password aging: 30 days max, 2 days min, 7 days warning
- Password quality: 10+ chars, uppercase, lowercase, digit, no username
- sudo: 3 attempts max, logging enabled, TTY required, secure_path

**User Management:**
- User `lemmerli` in groups: sudo, user42
- Separation of privileges (principle of least privilege)

**Services:**
- SSH on port 4242 (non-standard for security)
- UFW firewall (only 4242 open)
- AppArmor running (mandatory access control)

### Comparisons

**AppArmor vs SELinux:**
- AppArmor: Path-based, simpler, default on Debian
- SELinux: Label-based, more complex, default on RHEL/Rocky

**UFW vs firewalld:**
- UFW: Simple frontend for iptables (Debian/Ubuntu)
- firewalld: Zone-based, dynamic rules (RHEL/Rocky)

**VirtualBox vs UTM:**
- VirtualBox: Cross-platform, mature, x86/x64
- UTM: macOS focus, QEMU-based, ARM support (M1/M2)

## Resources

### Documentation
- [Debian Installation Guide](https://www.debian.org/releases/stable/installmanual)
- [sudo Manual](https://www.sudo.ws/docs/man/sudo.man/)
- [SSH Hardening Guide](https://www.ssh.com/academy/ssh/config)
- [LVM Tutorial](https://wiki.debian.org/LVM)

### AI Usage
AI (Claude) was used for:
- Understanding complex concepts (LVM, encryption, PAM)
- Debugging configuration issues (GRUB, SSH, cron)
- Learning bash scripting best practices
- Explaining security rationale for each requirement

---

**Author:** lemmerli  
**School:** 42 Heilbronn  
**Project:** Born2beRoot