# Trading Cloud Server - Hardware Details

## Server Information
- **Provider**: Oracle Cloud Infrastructure (OCI)
- **Region**: AP-MUMBAI-1 (Asia Pacific - Mumbai)
- **Availability Domain**: wmMi:AP-MUMBAI-1-AD-1
- **Fault Domain**: FAULT-DOMAIN-1
- **Shape**: VM.Standard.E2.1.Micro (Always Free Tier)
- **Hostname**: trading-cloud-server

## Instance Details
- **Instance ID**: `ocid1.instance.oc1.ap-mumbai-1.anrg6ljrllerkbacaq6b2orkipd7jo2uxvaszxxza7hhs73pdffyxqwfzbja`
- **Created**: January 11, 2026
- **Status**: RUNNING ✅
- **Launch Mode**: PARAVIRTUALIZED
- **Firmware**: UEFI 64-bit

## CPU Specifications
- **Processor**: AMD EPYC 7551 32-Core Processor
- **Clock Speed**: 2.0 GHz (Naples Architecture)
- **vCPUs**: 2 (Virtual CPUs)
- **Physical Cores**: 1 core
- **Threads per Core**: 2 (Hyperthreading enabled)
- **OCPUs**: 1.0 (Oracle CPU Unit)

## Memory Specifications
- **Total RAM**: 1.0 GB (956 MiB)
- **Memory Type**: DDR4 ECC (Enterprise-grade)
- **Available Memory**: ~582 MiB (typical)
- **Swap**: Not configured (0 GB)

## Storage Configuration
- **Boot Volume Size**: 45 GB (44.07 GB usable)
- **Boot Volume Type**: PARAVIRTUALIZED
- **Filesystem**: ext4
- **Used Space**: ~2.0 GB (5%)
- **Available Space**: ~43 GB
- **Storage Type**: Block Volume (SSD-backed)
- **IOPS**: Baseline performance tier

## Network Configuration
- **Primary NIC**: ens3
- **Network Type**: PARAVIRTUALIZED
- **Network Bandwidth**: 0.48 Gbps
- **Max VNIC Attachments**: 1
- **Public IP**: 155.248.251.25
- **Private IP**: 10.0.0.113
- **Subnet**: Oracle Cloud VCN

## Security Features
- **Secure Boot**: UEFI Secure Boot capable
- **PV Encryption**: Not enabled (standard tier)
- **Management Services**: Enabled
  - Oracle Cloud Agent: Enabled
  - Monitoring: Enabled
  - OS Management: Available

## Availability Configuration
- **Live Migration**: Supported
- **Recovery Action**: RESTORE_INSTANCE (Auto-recovery enabled)
- **Maintenance**: Automated by Oracle Cloud

## Free Tier Benefits
- **Cost**: $0/month (Always Free)
- **Guaranteed Uptime**: Yes
- **Included in Free Tier**: Yes
- **System Tag**: `free-tier-retained: true`

## Performance Characteristics
- **Baseline CPU Utilization**: No throttling on this shape
- **Local Disks**: 0 (Uses block storage)
- **GPUs**: 0
- **Best For**:
  - Small web applications
  - Development/testing environments
  - Microservices
  - Trading bots and automation scripts
  - API servers

## Hardware Limitations
- Single vCPU with hyperthreading (2 threads)
- Limited to 1 GB RAM
- No GPU acceleration
- Standard network performance (0.48 Gbps)
- Cannot be upgraded (free tier fixed specs)

---
*Last Updated: January 11, 2026*
*Server uptime and health can be monitored via Oracle Cloud Console*
