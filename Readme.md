# Trading Cloud Server 🚀

Welcome to your Oracle Cloud Free Tier server, specially configured for trading applications, bots, and automation!

## 📋 Quick Overview

This is a **FREE** cloud server running on Oracle Cloud Infrastructure with the following specs:

- **Server Name**: Trading Cloud Server
- **Provider**: Oracle Cloud (Always Free Tier)
- **Location**: Mumbai, India (AP-MUMBAI-1)
- **IP Address**: 155.248.251.25
- **Operating System**: Ubuntu 24.04.3 LTS
- **CPU**: 1 OCPU (2 vCPUs) - AMD EPYC 7551
- **RAM**: 1 GB
- **Storage**: 45 GB SSD
- **Cost**: $0/month (FREE forever!)

## 📁 What's in This Folder?

This folder contains everything you need to access and manage your cloud server:

1. **Readme.md** (this file) - Start here!
2. **Hardware Details.md** - Complete hardware specifications
3. **Software Details.md** - Installed software and system configuration
4. **Access Details.md** - How to connect and manage the server
5. **trading_cloud_server_key** - Private SSH key (KEEP SECURE!)
6. **trading_cloud_server_key.pub** - Public SSH key

## 🚀 Quick Start (5 Minutes)

### Step 1: Setup SSH Key (One-time setup)

#### On Mac/Linux:
```bash
# Open Terminal and run:
cd ~/Desktop/Trading\ Cloud\ Server/
cp trading_cloud_server_key ~/.ssh/
chmod 600 ~/.ssh/trading_cloud_server_key
```

#### On Windows (PowerShell):
```powershell
# Open PowerShell and run:
cd ~\Desktop\"Trading Cloud Server"
Copy-Item trading_cloud_server_key ~\.ssh\
icacls ~\.ssh\trading_cloud_server_key /inheritance:r
icacls ~\.ssh\trading_cloud_server_key /grant:r "$env:USERNAME:R"
```

### Step 2: Connect to Your Server

```bash
ssh -i ~/.ssh/trading_cloud_server_key ubuntu@155.248.251.25
```

That's it! You're now connected to your cloud server.

### Step 3: First Time Setup (Recommended)

Once connected, run these commands:

```bash
# Update the system
sudo apt update && sudo apt upgrade -y

# Install essential tools
sudo apt install -y htop curl wget git vim python3-pip

# Create swap file (helps with low RAM)
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# Setup firewall
sudo ufw allow 22/tcp
sudo ufw enable

# Done!
echo "Server setup complete!"
```

## 💡 What Can You Do With This Server?

### Perfect For:
- **Trading Bots**: Run automated trading bots 24/7
- **Market Data Collection**: Scrape and store market data
- **APIs**: Host REST APIs for trading applications
- **Backtesting**: Run trading strategy backtests
- **Alerts & Notifications**: Send trading alerts via Telegram/Email
- **Web Scraping**: Collect data from financial websites
- **Lightweight Web Apps**: Host simple dashboards or tools

### Not Suitable For:
- Heavy machine learning (only 1GB RAM)
- High-frequency trading (network latency)
- Large databases (only 45GB storage)
- Video processing or rendering
- Game servers

## 📚 Detailed Documentation

For more information, check out these files:

- **[Hardware Details.md](Hardware%20Details.md)** - CPU, RAM, storage specs
- **[Software Details.md](Software%20Details.md)** - OS, installed packages, recommended software
- **[Access Details.md](Access%20Details.md)** - SSH setup, file transfer, troubleshooting

## 🛠️ Common Tasks

### Check Server Status
```bash
# System resources
htop

# Disk space
df -h

# Memory usage
free -h

# Running processes
ps aux
```

### Upload Files to Server
```bash
# Upload a single file
scp -i ~/.ssh/trading_cloud_server_key myfile.txt ubuntu@155.248.251.25:~/

# Upload a folder
scp -i ~/.ssh/trading_cloud_server_key -r myfolder/ ubuntu@155.248.251.25:~/
```

### Download Files from Server
```bash
# Download a file
scp -i ~/.ssh/trading_cloud_server_key ubuntu@155.248.251.25:~/remote_file.txt ./

# Download a folder
scp -i ~/.ssh/trading_cloud_server_key -r ubuntu@155.248.251.25:~/remote_folder/ ./
```

### Install Python Trading Libraries
```bash
# Connect to server first
ssh -i ~/.ssh/trading_cloud_server_key ubuntu@155.248.251.25

# Install trading libraries
pip3 install pandas numpy ccxt python-binance requests ta-lib-binary

# For Telegram bot
pip3 install python-telegram-bot
```

### Run a Trading Bot (Example)
```bash
# Upload your bot
scp -i ~/.ssh/trading_cloud_server_key trading_bot.py ubuntu@155.248.251.25:~/

# Connect to server
ssh -i ~/.ssh/trading_cloud_server_key ubuntu@155.248.251.25

# Run bot in background
nohup python3 trading_bot.py > bot.log 2>&1 &

# Check if running
ps aux | grep trading_bot

# View logs
tail -f bot.log
```

## 🔒 Security Best Practices

1. **NEVER share your private key** (`trading_cloud_server_key`)
2. **Always update your system** regularly: `sudo apt update && sudo apt upgrade`
3. **Use strong passwords** if you create new users
4. **Enable firewall**: Only open ports you actually need
5. **Monitor server logs**: `sudo journalctl -f`
6. **Backup important data**: Download critical files regularly
7. **Don't store API keys** in plain text - use environment variables

## 🆘 Troubleshooting

### Can't Connect to Server?
1. Check if your internet is working
2. Verify the IP address hasn't changed (check Oracle Cloud Console)
3. Make sure you're using the correct key: `trading_cloud_server_key`
4. Check key permissions: `chmod 600 ~/.ssh/trading_cloud_server_key`

### Server Running Slow?
1. Check RAM usage: `free -h`
2. Check CPU usage: `top` or `htop`
3. Consider adding swap space (see Step 3 in Quick Start)
4. Kill unnecessary processes

### Out of Disk Space?
```bash
# Check disk usage
df -h

# Find large files
du -h --max-depth=1 /home/ubuntu | sort -hr

# Clean package cache
sudo apt clean
sudo apt autoremove
```

## 📞 Support & Resources

### Oracle Cloud
- **Console**: https://cloud.oracle.com/
- **Documentation**: https://docs.oracle.com/en-us/iaas/Content/home.htm
- **Free Tier**: https://www.oracle.com/cloud/free/

### Ubuntu
- **Documentation**: https://ubuntu.com/server/docs
- **Community Help**: https://askubuntu.com/

### Python Trading
- **CCXT Library**: https://github.com/ccxt/ccxt
- **Python Binance**: https://github.com/sammchardy/python-binance
- **Pandas**: https://pandas.pydata.org/

## 🎯 Next Steps

1. **Connect to your server** using the Quick Start guide above
2. **Run the first-time setup** to update and secure your server
3. **Install your trading bot** or application
4. **Set up monitoring** to track your bot's performance
5. **Create backups** of important data regularly

## ⚠️ Important Notes

- This server is on Oracle Cloud's **Always Free Tier** - it will remain free forever
- The server has **1GB RAM** - be mindful of memory usage
- **Backup your data** regularly - free tier doesn't include automatic backups
- The **private SSH key is your only way to access** the server - keep it safe!
- Server may be rebooted for maintenance - use `systemd` services for auto-restart

## 📊 Server Monitoring

### Check if Server is Online
```bash
ping 155.248.251.25
```

### Monitor System Resources (once connected)
```bash
# Real-time monitoring
htop

# Disk I/O
sudo iotop

# Network usage
sudo nethogs

# System logs
sudo journalctl -f
```

## 🎉 You're All Set!

Your cloud server is ready to run 24/7 trading bots, APIs, and automation scripts - completely **FREE**!

If you have any questions, refer to the detailed documentation files in this folder.

Happy Trading! 📈

---
*Server Created: January 11, 2026*
*Provider: Oracle Cloud Infrastructure (OCI)*
*Region: AP-MUMBAI-1 (Mumbai, India)*
*Instance ID: ocid1.instance.oc1.ap-mumbai-1.anrg6ljrllerkbacaq6b2orkipd7jo2uxvaszxxza7hhs73pdffyxqwfzbja*
