# Trading Cloud Server - Access Details

## 🔐 SSH Access

### Primary Access Method
```bash
ssh -i trading_cloud_server_key ubuntu@155.248.251.25
```

### Server Details
- **Public IP**: 155.248.251.25
- **Private IP**: 10.0.0.113
- **SSH Port**: 22 (default)
- **Username**: ubuntu
- **Authentication**: SSH Key (Ed25519)

### SSH Key Information
- **Private Key**: `trading_cloud_server_key` (in this folder)
- **Public Key**: `trading_cloud_server_key.pub` (in this folder)
- **Key Type**: Ed25519 (modern, secure, fast)
- **Key Fingerprint**: SHA256:/zZwxj3Vlzu1K8ox3WBHyu8WAV4PS6ppbHu2UAjLNOc
- **Key Comment**: trading-cloud-server-access

### 🚨 IMPORTANT SECURITY NOTES
1. **NEVER share the private key** (`trading_cloud_server_key`) publicly
2. **Keep the private key secure** - store it in `~/.ssh/` with permissions 600
3. **Backup the key** - if lost, you'll need to recreate the instance
4. **Use a passphrase** (optional but recommended) for extra security

## 📁 SSH Key Setup Instructions

### For Linux/macOS Users
```bash
# 1. Copy the private key to your SSH directory
cp trading_cloud_server_key ~/.ssh/
chmod 600 ~/.ssh/trading_cloud_server_key

# 2. Connect to the server
ssh -i ~/.ssh/trading_cloud_server_key ubuntu@155.248.251.25

# 3. (Optional) Add to SSH config for easier access
cat >> ~/.ssh/config << EOF
Host trading-cloud
    HostName 155.248.251.25
    User ubuntu
    IdentityFile ~/.ssh/trading_cloud_server_key
    StrictHostKeyChecking no
EOF

# 4. Now you can connect with just:
ssh trading-cloud
```

### For Windows Users (PowerShell)
```powershell
# 1. Copy the private key to your SSH directory
Copy-Item trading_cloud_server_key ~\.ssh\
icacls ~\.ssh\trading_cloud_server_key /inheritance:r
icacls ~\.ssh\trading_cloud_server_key /grant:r "$env:USERNAME:R"

# 2. Connect to the server
ssh -i ~\.ssh\trading_cloud_server_key ubuntu@155.248.251.25
```

### For Windows Users (PuTTY)
1. Download PuTTYgen from https://www.putty.org/
2. Load the `trading_cloud_server_key` file
3. Save it as a `.ppk` file
4. In PuTTY:
   - Host: 155.248.251.25
   - Port: 22
   - Connection → SSH → Auth → Browse and select the `.ppk` file
   - Session → Save for future use

## 🌐 Oracle Cloud Console Access

### Instance Management
- **Console URL**: https://cloud.oracle.com/
- **Region**: AP-MUMBAI-1
- **Compartment**: Root compartment (tenancy)
- **Instance OCID**: `ocid1.instance.oc1.ap-mumbai-1.anrg6ljrllerkbacaq6b2orkipd7jo2uxvaszxxza7hhs73pdffyxqwfzbja`

### Console Features Available
- **Instance Actions**:
  - Start/Stop/Reboot/Terminate
  - Console Connection (VNC)
  - Metrics and Monitoring
  - Audit Logs

- **Network Configuration**:
  - Security Lists
  - Route Tables
  - Internet Gateway settings

- **Storage Management**:
  - Boot Volume snapshots
  - Volume backups
  - Block volume attachments

## 🔥 Emergency Access (If SSH Fails)

### Via Oracle Cloud Console
1. Go to https://cloud.oracle.com/
2. Navigate to: Compute → Instances → trading-cloud-server
3. Click "Console Connection" → Create Console Connection
4. Use the generated connection command

### Via Instance Metadata
- Access via Serial Console through OCI Console
- Useful if network or SSH is broken

## 🛡️ Security Configuration

### Firewall Rules (Oracle Cloud Security List)
Currently, only SSH (port 22) is allowed by default:
- **SSH**: 0.0.0.0/0 → Port 22 (TCP)

### Adding New Firewall Rules (Examples)
If you need to open more ports (e.g., for web server, API):

```bash
# For HTTP (port 80)
# Go to: VCN → Security Lists → Default Security List → Add Ingress Rule
# Source: 0.0.0.0/0
# Protocol: TCP
# Destination Port: 80

# For HTTPS (port 443)
# Source: 0.0.0.0/0
# Protocol: TCP
# Destination Port: 443

# For Custom Application (e.g., 8080)
# Source: 0.0.0.0/0
# Protocol: TCP
# Destination Port: 8080
```

### UFW (Ubuntu Firewall) - Not Configured
Once inside the server, you can also configure UFW:
```bash
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
```

## 📊 Monitoring & Management

### SSH into Server and Check Status
```bash
# System resource usage
htop

# Disk usage
df -h

# Memory usage
free -h

# Network connections
sudo netstat -tulpn

# System logs
sudo journalctl -f
```

### Oracle Cloud Monitoring (via Console)
- CPU utilization graphs
- Memory utilization
- Network I/O
- Disk I/O

## 🔄 Server Management Commands

### Restart Services
```bash
# Restart SSH service
sudo systemctl restart sshd

# Restart server
sudo reboot
```

### Update System
```bash
sudo apt update
sudo apt upgrade -y
```

### Check Server Uptime
```bash
uptime
```

## 💾 File Transfer

### Using SCP (Secure Copy)
```bash
# Upload file to server
scp -i ~/.ssh/trading_cloud_server_key local_file.txt ubuntu@155.248.251.25:~/

# Download file from server
scp -i ~/.ssh/trading_cloud_server_key ubuntu@155.248.251.25:~/remote_file.txt ./

# Upload entire directory
scp -i ~/.ssh/trading_cloud_server_key -r local_folder/ ubuntu@155.248.251.25:~/
```

### Using SFTP
```bash
sftp -i ~/.ssh/trading_cloud_server_key ubuntu@155.248.251.25
# Then use: put, get, ls, cd commands
```

### Using rsync (Efficient for large transfers)
```bash
rsync -avz -e "ssh -i ~/.ssh/trading_cloud_server_key" local_folder/ ubuntu@155.248.251.25:~/remote_folder/
```

## 🚀 Quick Start Guide

### First Login
```bash
# 1. Connect to server
ssh -i trading_cloud_server_key ubuntu@155.248.251.25

# 2. Update system
sudo apt update && sudo apt upgrade -y

# 3. Install essential tools
sudo apt install -y htop curl wget git vim

# 4. Check system info
uname -a
free -h
df -h
```

## 🆘 Troubleshooting

### SSH Connection Refused
- Check if server is running in Oracle Cloud Console
- Verify security list allows port 22 from your IP
- Check if SSH service is running (via Console Connection)

### Permission Denied (publickey)
- Verify you're using the correct private key
- Check key permissions: `chmod 600 trading_cloud_server_key`
- Verify username is `ubuntu` not `root`

### Timeout Connecting
- Check your internet connection
- Verify the public IP hasn't changed
- Check Oracle Cloud security lists

## 📞 Support & Resources

### Oracle Cloud Documentation
- [OCI Documentation](https://docs.oracle.com/en-us/iaas/Content/home.htm)
- [Compute Instance Guide](https://docs.oracle.com/en-us/iaas/Content/Compute/home.htm)

### Ubuntu Documentation
- [Ubuntu Server Guide](https://ubuntu.com/server/docs)
- [Ubuntu Security](https://ubuntu.com/security)

---
*Last Updated: January 11, 2026*
*Keep this document secure - it contains sensitive access information*
