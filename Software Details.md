# Trading Cloud Server - Software Details

## Operating System
- **Distribution**: Ubuntu 24.04.3 LTS (Noble Numbat)
- **Kernel Version**: 6.14.0-1016-oracle
- **Architecture**: x86_64 (64-bit)
- **Image ID**: `ocid1.image.oc1.ap-mumbai-1.aaaaaaaa3k2zgro5ew3653n5ua26xbql7zh3izfthat4in7lfjjpelezbfwa`
- **Boot Mode**: UEFI
- **Init System**: systemd

## Kernel Details
- **Type**: Oracle Linux Kernel
- **Version**: 6.14.0-1016-oracle
- **Build**: Custom Oracle Cloud optimized kernel
- **Features**:
  - KVM virtualization support
  - Paravirtualized drivers
  - Oracle Cloud Agent integration

## Pre-installed Software

### Programming Languages & Runtimes
- **Python 3**: v3.12.3
  - Location: `/usr/bin/python3`
  - pip3: Included
  - Standard library: Complete

### Development Tools
- **Git**: v2.43.0
  - Location: `/usr/bin/git`
  - Ready for version control

### System Utilities
- **Package Manager**: apt (Advanced Package Tool)
- **Shell**: bash 5.2+
- **Text Editors**: nano, vim (basic)
- **Network Tools**: curl, wget, netstat, ss

## Services & Daemons

### Active Services
- **SSH Server**: OpenSSH Server
  - Port: 22
  - Status: Running
  - Root login: Disabled
  - Password auth: Enabled

- **Oracle Cloud Agent**
  - Auto-updates enabled
  - Monitoring enabled
  - Management enabled

- **systemd-resolved**: DNS resolution
- **systemd-networkd**: Network management
- **cron**: Task scheduler

### Security Services
- **UFW (Uncomplicated Firewall)**: Available (not configured)
- **fail2ban**: Not installed
- **AppArmor**: Active (Linux security module)

## System Status (as of deployment)
- **System Load**: Low (0.38)
- **Processes**: 122
- **Memory Usage**: 25% (~240 MB used)
- **Disk Usage**: 4.3% (~2 GB used)
- **Swap Usage**: 0% (no swap configured)

## Available Package Repositories
- Ubuntu 24.04 Noble main repository
- Ubuntu 24.04 Noble universe repository
- Ubuntu 24.04 Noble security updates
- Oracle Cloud Infrastructure repository

## Security & Updates
- **ESM (Extended Security Maintenance)**: Not enabled (available for activation)
- **Automatic Updates**: Not configured
- **Security Patches**: Available via apt
- **Last Update Check**: More than a week old (needs update)

## Recommended Software to Install

### For Trading Applications
```bash
# Python trading libraries
sudo apt update
sudo apt install python3-pip python3-venv
pip3 install pandas numpy ccxt ta-lib

# Database (for storing trading data)
sudo apt install postgresql postgresql-contrib
# OR
sudo apt install redis-server

# Monitoring tools
sudo apt install htop iotop nethogs
```

### For Containerization
```bash
# Docker (recommended for isolated environments)
sudo apt install docker.io
sudo systemctl enable docker
sudo usermod -aG docker ubuntu
```

### For Security
```bash
# Firewall configuration
sudo apt install ufw
sudo ufw allow 22/tcp
sudo ufw enable

# Intrusion prevention
sudo apt install fail2ban
```

### For Web Services
```bash
# Nginx (if running web interface)
sudo apt install nginx

# Node.js (for JavaScript trading bots)
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install nodejs
```

## Network Configuration
- **Hostname**: trading-cloud-server
- **DNS**: Managed by systemd-resolved
- **IPv4**: Enabled (10.0.0.113 private, 155.248.251.25 public)
- **IPv6**: Not configured

## Disk & Filesystem
- **Root Filesystem**: ext4
- **Mount Options**: defaults, relatime
- **Reserved Blocks**: 5% (for root)
- **Inode Usage**: Low

## User Accounts
- **Default User**: ubuntu (sudo privileges)
- **Home Directory**: /home/ubuntu
- **Shell**: /bin/bash
- **Groups**: ubuntu, sudo, adm, dialout, cdrom, floppy, audio, dip, video, plugdev, netdev, lxd

## Boot Configuration
- **Boot Loader**: GRUB (managed by cloud-init)
- **Boot Time**: Fast (cloud-optimized)
- **Console**: Serial console available via Oracle Cloud Console

## Cloud Integration
- **cloud-init**: Installed and active
  - Handles initial setup
  - Configures networking
  - Injects SSH keys
  - Sets hostname

## Limitations & Notes
- No Docker installed by default
- No database installed
- No web server installed
- Minimal package set (cloud image)
- ESM Apps not enabled (requires Ubuntu Pro)

## System Optimization Tips
1. **Memory**: With only 1GB RAM, avoid memory-intensive applications
2. **Swap**: Consider adding swap for stability
3. **Updates**: Run `sudo apt update && sudo apt upgrade` regularly
4. **Monitoring**: Install monitoring tools to track resource usage
5. **Cleanup**: Use `sudo apt autoremove` to clean unused packages

## Recommended First Steps
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install essential tools
sudo apt install -y htop curl wget git vim

# Create swap (recommended for 1GB RAM)
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# Configure firewall
sudo ufw allow 22/tcp
sudo ufw enable
```

---
*Last Updated: January 11, 2026*
*Software inventory subject to user installations*
