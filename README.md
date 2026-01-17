# Cloud Server - Oracle Cloud Infrastructure

## Overview

Oracle Cloud Free Tier server running in Mumbai (ap-mumbai-1) region. Part of Vibhav's distributed infrastructure.

| Property | Value |
|----------|-------|
| **Provider** | Oracle Cloud Infrastructure |
| **Account** | vibhavaggarwal2 |
| **Region** | ap-mumbai-1 (Mumbai, India) |
| **Tier** | Always Free |
| **Created** | December 23, 2025 |

---

## Active Instances

### 1. vibhav-cloud-server (AMD)

| Property | Value |
|----------|-------|
| **Status** | ✅ RUNNING |
| **Public IP** | 92.4.88.143 |
| **Tailscale IP** | 100.102.27.25 |
| **Shape** | VM.Standard.E2.1.Micro |
| **CPU** | 2 vCPU (AMD EPYC) |
| **RAM** | 1 GB |
| **Storage** | 47 GB |
| **OS** | Ubuntu 24.04 LTS |

**Quick Access:**
```bash
ssh cloud-server
```

### 2. vibhav-cloud-backup-server (AMD)

| Property | Value |
|----------|-------|
| **Status** | ✅ RUNNING |
| **Public IP** | 161.118.167.96 |
| **Tailscale IP** | 100.85.233.36 |
| **Shape** | VM.Standard.E2.1.Micro |
| **CPU** | 2 vCPU (AMD EPYC) |
| **RAM** | 1 GB |
| **Storage** | 50 GB |
| **OS** | Ubuntu 24.04 LTS |

**Quick Access:**
```bash
ssh cloud-backup-server
```

---

## Documentation

| File | Description |
|------|-------------|
| [Hardware-Details.md](Hardware-Details.md) | CPU, RAM, storage, network specs |
| [Software-Details.md](Software-Details.md) | OS, packages, installation guides |
| [Access-Details.md](Access-Details.md) | SSH, API, CLI, web console access |

---

## Free Tier Resources

| Resource | Limit | Used |
|----------|-------|------|
| AMD Micro VMs | 2 | **2 (MAX)** |
| ARM A1 OCPUs | 4 | 0 (unavailable) |
| ARM A1 Memory | 24 GB | 0 (unavailable) |
| Block Storage | 200 GB | 97 GB |
| Object Storage | 20 GB | 0 |
| Outbound Data | 10 TB/mo | ~0 |

---

## Network Architecture

```
Internet
    │
    ▼
┌───────────────────────────────────┐
│  Oracle Cloud (ap-mumbai-1)       │
│  ┌─────────────────────────────┐  │
│  │  vibhav-vcn (10.0.0.0/16)   │  │
│  │  ┌───────────────────────┐  │  │
│  │  │ vibhav-public-subnet  │  │  │
│  │  │    10.0.0.0/24        │  │  │
│  │  │  ┌─────────────────┐  │  │  │
│  │  │  │ vibhav-cloud-   │  │  │  │
│  │  │  │ server          │  │  │  │
│  │  │  │ 10.0.0.14       │  │  │  │
│  │  │  │ 92.4.88.143     │  │  │  │
│  │  │  └─────────────────┘  │  │  │
│  │  └───────────────────────┘  │  │
│  └─────────────────────────────┘  │
└───────────────────────────────────┘
```

---

## Quick Commands

```bash
# SSH to server
ssh oracle-cloud

# Check status via CLI
oci compute instance get \
  --instance-id ocid1.instance.oc1.ap-mumbai-1.anrg6ljrllerkbacghbwewkj6r3lst3s5s5jf26kpgvqfcbm7xb2cpeiryfq \
  --query "data.\"lifecycle-state\"" --raw-output

# Use helper script
"/Users/vibhavaggarwal/Desktop/Oracle Cloud/oci-commands.sh" help

# Monitor ARM retry
tail -f "/Users/vibhavaggarwal/Desktop/Oracle Cloud/arm-retry.log"
```

---

## Integration Points

| Service | Status | Purpose |
|---------|--------|---------|
| Cloudflare Tunnel | Planned | Remote access via oracle.vibhavaggarwal.com |
| Tailscale | Planned | Mesh VPN integration |
| MCP Server | Planned | Filesystem access for Claude |

---

## Related Documentation

- **Full Documentation**: `~/Desktop/Oracle Cloud/`
  - `README.md` - Complete setup guide
  - `ANALYSIS.md` - API analysis & workflow ideas
  - `oci-commands.sh` - Quick command helper
  - `retry-arm-instance.sh` - ARM retry script
  - `arm-retry.log` - Retry attempt logs

---

## Use Cases

1. **CI/CD Runner** - GitHub Actions self-hosted runner
2. **Monitoring Hub** - Prometheus + Grafana for all servers
3. **Backup Destination** - Off-site backup via Object Storage
4. **Exit Node** - Tailscale VPN exit in India
5. **Public Gateway** - Nginx reverse proxy for services

---

**Last Updated**: December 23, 2025
