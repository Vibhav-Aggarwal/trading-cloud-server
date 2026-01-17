# Oracle Cloud Server - Hardware Details

## Instance 1: vibhav-cloud-server (AMD Micro)

### Compute Specifications

| Property | Value |
|----------|-------|
| **Shape** | VM.Standard.E2.1.Micro |
| **Architecture** | x86_64 (AMD64) |
| **Processor** | AMD EPYC 7551 @ 2.0 GHz (Naples) |
| **vCPUs** | 2 |
| **OCPUs** | 1/8 (burstable) |
| **RAM** | 1 GB |
| **Network Bandwidth** | 480 Mbps |
| **Max VNICs** | 1 |

### Storage

| Property | Value |
|----------|-------|
| **Boot Volume** | 47 GB |
| **Volume Type** | Block Storage (Paravirtualized) |
| **IOPS** | 10 VPUs/GB (default) |
| **Boot Mode** | UEFI 64-bit |

### Network Interface

| Property | Value |
|----------|-------|
| **MAC Address** | 02:00:17:02:FD:3C |
| **Private IP** | 10.0.0.14 |
| **Public IP** | 92.4.88.143 |
| **VNIC Type** | Paravirtualized |

### Location

| Property | Value |
|----------|-------|
| **Region** | ap-mumbai-1 (India West - Mumbai) |
| **Availability Domain** | wmMi:AP-MUMBAI-1-AD-1 |
| **Fault Domain** | FAULT-DOMAIN-3 |
| **Data Center** | Oracle Mumbai DC |

---

## Instance 2: vibhav-arm-server (ARM Ampere) - PENDING

### Compute Specifications (Planned)

| Property | Value |
|----------|-------|
| **Shape** | VM.Standard.A1.Flex |
| **Architecture** | ARM64 (AArch64) |
| **Processor** | Ampere Altra @ 3.0 GHz |
| **OCPUs** | 4 |
| **RAM** | 24 GB |
| **Network Bandwidth** | ~4 Gbps (1 Gbps per OCPU) |
| **Max VNICs** | 4 |

### Storage (Planned)

| Property | Value |
|----------|-------|
| **Boot Volume** | 100 GB |
| **Volume Type** | Block Storage (Paravirtualized) |

### Status

| Property | Value |
|----------|-------|
| **Current Status** | ⏳ Waiting for capacity |
| **Auto-Retry** | Running (every ~2 min) |
| **Region** | ap-mumbai-1 |

---

## Free Tier Limits

### Compute

| Resource | Limit | Used | Available |
|----------|-------|------|-----------|
| AMD E2.1.Micro | 2 instances | 1 | 1 |
| ARM A1 OCPUs | 4 cores | 0 | 4 |
| ARM A1 Memory | 24 GB | 0 | 24 GB |

### Storage

| Resource | Limit | Used | Available |
|----------|-------|------|-----------|
| Block Volume | 200 GB | 47 GB | 153 GB |
| Object Storage | 20 GB | 0 | 20 GB |
| Archive Storage | 20 GB | 0 | 20 GB |

### Network

| Resource | Limit |
|----------|-------|
| Outbound Data | 10 TB/month |
| Load Balancer | 1 (10 Mbps) |
| VCNs | 2 |

---

## Comparison with Home Infrastructure

| Server | CPU | RAM | Storage | Location |
|--------|-----|-----|---------|----------|
| **Oracle AMD** | 2 vCPU | 1 GB | 47 GB | Mumbai DC |
| **Oracle ARM** | 4 OCPU | 24 GB | 100 GB | Mumbai DC (pending) |
| Home Server | 4 cores | 8 GB | 2 TB | Home |
| Office Server | 8 cores | 32 GB | 1 TB | Office |
| Lab Server (IBM x3650) | 8 cores | 3 GB | 273 GB | Office |
| Admin Server (Alienware) | 4 cores | 16 GB | 500 GB | Office |
| GPU Server | 2 cores | 4 GB | 457 GB | Office |

---

**Last Updated**: December 23, 2025
