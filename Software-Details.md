# Oracle Cloud Server - Software Details

## Operating System

### vibhav-cloud-server (AMD)

| Property | Value |
|----------|-------|
| **OS** | Ubuntu 24.04 LTS (Noble Numbat) |
| **Kernel** | 6.14.0-1016-oracle |
| **Architecture** | x86_64 |
| **Image ID** | `ocid1.image.oc1.ap-mumbai-1.aaaaaaaa3k2zgro5ew3653n5ua26xbql7zh3izfthat4in7lfjjpelezbfwa` |

### vibhav-arm-server (ARM) - Planned

| Property | Value |
|----------|-------|
| **OS** | Ubuntu 22.04 LTS (Jammy Jellyfish) |
| **Architecture** | ARM64 |
| **Image ID** | `ocid1.image.oc1.ap-mumbai-1.aaaaaaaahzcec4tjbvlvkptojwrc5zo4zazgdnwwyg5f5ayjpkreigtzwpxa` |

---

## Pre-installed Software (Ubuntu 24.04)

### System Utilities

| Package | Purpose |
|---------|---------|
| systemd | Init system & service manager |
| apt | Package manager |
| snap | Snap package manager |
| cloud-init | Cloud instance initialization |
| iptables-persistent | Firewall rules persistence |
| unattended-upgrades | Automatic security updates |

### Network Tools

| Package | Purpose |
|---------|---------|
| openssh-server | SSH daemon |
| netplan | Network configuration |
| curl, wget | HTTP clients |
| iptables, nftables | Firewall |

### Oracle Cloud Agent

| Service | Purpose |
|---------|---------|
| oracle-cloud-agent | OCI monitoring & management |
| Compute Instance Run Command | Remote command execution |
| Compute Instance Monitoring | Metrics collection |
| OS Management Service Agent | Patch management |

---

## Recommended Software Installation

### Essential Tools

```bash
# Connect to server
ssh oracle-cloud

# Update system
sudo apt update && sudo apt upgrade -y

# Install essential tools
sudo apt install -y \
  htop \
  tmux \
  vim \
  git \
  curl \
  wget \
  unzip \
  jq \
  tree \
  ncdu \
  net-tools \
  dnsutils
```

### Docker

```bash
# Install Docker
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker ubuntu
sudo systemctl enable docker

# Install Docker Compose
sudo apt install docker-compose-plugin
```

### Tailscale (Mesh VPN)

```bash
# Install Tailscale
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up

# Optional: Advertise as exit node
sudo tailscale up --advertise-exit-node
```

### Cloudflared (Tunnel)

```bash
# Install cloudflared
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
sudo dpkg -i cloudflared-linux-amd64.deb

# Login and create tunnel
cloudflared tunnel login
cloudflared tunnel create oracle-cloud
```

### Node.js

```bash
# Install Node.js via nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install --lts
```

### Python

```bash
# Python 3 with pip
sudo apt install python3-pip python3-venv
```

---

## Service Ideas

### 1. Nginx Reverse Proxy

```bash
sudo apt install nginx
sudo systemctl enable nginx
```

### 2. Pi-hole (DNS Ad Blocker)

```bash
curl -sSL https://install.pi-hole.net | bash
```

### 3. Code Server (VS Code in Browser)

```bash
curl -fsSL https://code-server.dev/install.sh | sh
sudo systemctl enable --now code-server@ubuntu
```

### 4. GitHub Actions Runner

```bash
# Download runner
mkdir actions-runner && cd actions-runner
curl -o actions-runner-linux-x64.tar.gz -L https://github.com/actions/runner/releases/download/v2.320.0/actions-runner-linux-x64-2.320.0.tar.gz
tar xzf actions-runner-linux-x64.tar.gz

# Configure
./config.sh --url https://github.com/YOUR_REPO --token YOUR_TOKEN
./run.sh
```

### 5. Monitoring Stack

```bash
# Prometheus + Grafana via Docker
docker run -d --name prometheus -p 9090:9090 prom/prometheus
docker run -d --name grafana -p 3000:3000 grafana/grafana
```

---

## Firewall Configuration

### Ubuntu UFW (Application Level)

```bash
# Enable UFW
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
```

### Oracle Cloud Security List (Network Level)

Already configured in OCI console:
- Port 22 (SSH)
- Port 80 (HTTP)
- Port 443 (HTTPS)
- ICMP (Ping)

**Note**: Both UFW and OCI Security List must allow traffic.

---

## System Optimization

### Swap (for 1GB RAM instance)

```bash
# Create 2GB swap
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# Optimize swappiness
echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### Performance Tuning

```bash
# Add to /etc/sysctl.conf
net.core.default_qdisc = fq
net.ipv4.tcp_congestion_control = bbr
vm.swappiness = 10
```

---

## Backup Strategy

### Using rclone to Object Storage

```bash
# Install rclone
sudo apt install rclone

# Configure OCI Object Storage
rclone config
# Type: oracle
# Namespace: bmidfwjenpmb
# Compartment: ocid1.tenancy.oc1..aaaaaaaaf5453txsqxwvjht7iyhogdjmbgiebuar3mtohym6dgksocn67eua

# Backup command
rclone sync /important/data oci:backup-bucket/
```

---

**Last Updated**: December 23, 2025
