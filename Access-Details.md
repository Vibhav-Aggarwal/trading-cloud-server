# Oracle Cloud Server - Access Details

## Quick Access

### SSH Access

```bash
# Primary method (using SSH config alias)
ssh oracle-cloud

# Direct SSH
ssh ubuntu@92.4.88.143

# With explicit key
ssh -i ~/.ssh/id_ed25519_vibhav ubuntu@92.4.88.143
```

### Web Console

| Resource | URL |
|----------|-----|
| **Cloud Console** | https://cloud.oracle.com/?region=ap-mumbai-1 |
| **Compute Instances** | https://cloud.oracle.com/compute/instances?region=ap-mumbai-1 |
| **Networking** | https://cloud.oracle.com/networking/vcns?region=ap-mumbai-1 |

---

## SSH Configuration

### ~/.ssh/config Entry

```
# Oracle Cloud Server (Mumbai) - AMD Micro
Host oracle-cloud cloud-server
    HostName 92.4.88.143
    User ubuntu
    IdentityFile ~/.ssh/id_ed25519_vibhav
    StrictHostKeyChecking no

# Oracle Cloud ARM Server (when created)
Host oracle-arm arm-server
    HostName <ARM_PUBLIC_IP>
    User ubuntu
    IdentityFile ~/.ssh/id_ed25519_vibhav
    StrictHostKeyChecking no
```

### SSH Key

| Property | Value |
|----------|-------|
| **Key Type** | Ed25519 |
| **Key Name** | vibhav-universal-key |
| **Key File** | `~/.ssh/id_ed25519_vibhav` |
| **Public Key** | `ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILibL1rCreAT/aa+dOLhiI+9KxnDczuOdMh3Qcs9wfMu` |

---

## OCI Account Details

### Tenancy

| Property | Value |
|----------|-------|
| **Tenancy Name** | vibhavaggarwal2 |
| **Home Region** | ap-mumbai-1 (Mumbai) |
| **Tenancy OCID** | `ocid1.tenancy.oc1..aaaaaaaaf5453txsqxwvjht7iyhogdjmbgiebuar3mtohym6dgksocn67eua` |

### User

| Property | Value |
|----------|-------|
| **Email** | vibhav.aggarwal2@gmail.com |
| **User OCID** | `ocid1.user.oc1..aaaaaaaabs6mokt2qcaie3uvabtosaoi4xjfjk3y32gwvhxsbscz5bwvx2ca` |

### API Key

| Property | Value |
|----------|-------|
| **Fingerprint** | `a2:e5:c4:32:55:8c:f1:22:6a:05:f1:a1:ff:d5:dd:ef` |
| **Config File** | `~/.oci/config` |
| **Private Key** | `~/.oci/oci_api_key.pem` |

---

## Network Details

### Instance Network

| Property | Value |
|----------|-------|
| **Hostname** | vibhav-cloud-server |
| **FQDN** | vibhavcloudserver.public.vibhavvcn.oraclevcn.com |
| **Private IP** | 10.0.0.14 |
| **Public IP** | 92.4.88.143 |
| **MAC Address** | 02:00:17:02:FD:3C |

### VCN & Subnet

| Resource | Name | CIDR |
|----------|------|------|
| VCN | vibhav-vcn | 10.0.0.0/16 |
| Subnet | vibhav-public-subnet | 10.0.0.0/24 |
| Gateway | 10.0.0.1 | - |

### Open Ports

| Port | Protocol | Service |
|------|----------|---------|
| 22 | TCP | SSH |
| 80 | TCP | HTTP |
| 443 | TCP | HTTPS |
| ICMP | - | Ping |

---

## OCI CLI Access

### Configuration File (~/.oci/config)

```ini
[DEFAULT]
user=ocid1.user.oc1..aaaaaaaabs6mokt2qcaie3uvabtosaoi4xjfjk3y32gwvhxsbscz5bwvx2ca
fingerprint=a2:e5:c4:32:55:8c:f1:22:6a:05:f1:a1:ff:d5:dd:ef
tenancy=ocid1.tenancy.oc1..aaaaaaaaf5453txsqxwvjht7iyhogdjmbgiebuar3mtohym6dgksocn67eua
region=ap-mumbai-1
key_file=~/.oci/oci_api_key.pem
```

### Test CLI Connection

```bash
# Verify CLI is working
oci iam user get --user-id ocid1.user.oc1..aaaaaaaabs6mokt2qcaie3uvabtosaoi4xjfjk3y32gwvhxsbscz5bwvx2ca

# List instances
oci compute instance list \
  --compartment-id ocid1.tenancy.oc1..aaaaaaaaf5453txsqxwvjht7iyhogdjmbgiebuar3mtohym6dgksocn67eua \
  --output table
```

---

## Instance Management Commands

### Quick Commands Script

```bash
# Use the helper script
"/Users/vibhavaggarwal/Desktop/Oracle Cloud/oci-commands.sh" help
```

### Manual Commands

```bash
# Get instance status
oci compute instance get \
  --instance-id ocid1.instance.oc1.ap-mumbai-1.anrg6ljrllerkbacghbwewkj6r3lst3s5s5jf26kpgvqfcbm7xb2cpeiryfq \
  --query "data.\"lifecycle-state\"" --raw-output

# Start instance
oci compute instance action \
  --instance-id ocid1.instance.oc1.ap-mumbai-1.anrg6ljrllerkbacghbwewkj6r3lst3s5s5jf26kpgvqfcbm7xb2cpeiryfq \
  --action START

# Stop instance
oci compute instance action \
  --instance-id ocid1.instance.oc1.ap-mumbai-1.anrg6ljrllerkbacghbwewkj6r3lst3s5s5jf26kpgvqfcbm7xb2cpeiryfq \
  --action STOP

# Reboot instance
oci compute instance action \
  --instance-id ocid1.instance.oc1.ap-mumbai-1.anrg6ljrllerkbacghbwewkj6r3lst3s5s5jf26kpgvqfcbm7xb2cpeiryfq \
  --action SOFTRESET

# Get public IP
oci compute instance list-vnics \
  --instance-id ocid1.instance.oc1.ap-mumbai-1.anrg6ljrllerkbacghbwewkj6r3lst3s5s5jf26kpgvqfcbm7xb2cpeiryfq \
  --query "data[0].\"public-ip\"" --raw-output
```

---

## Object Storage Access

### Namespace & Bucket

| Property | Value |
|----------|-------|
| **Namespace** | bmidfwjenpmb |
| **Compartment** | ocid1.tenancy.oc1..aaaaaaaaf5453txsqxwvjht7iyhogdjmbgiebuar3mtohym6dgksocn67eua |

### Access Commands

```bash
# List buckets
oci os bucket list \
  --compartment-id ocid1.tenancy.oc1..aaaaaaaaf5453txsqxwvjht7iyhogdjmbgiebuar3mtohym6dgksocn67eua

# Create bucket
oci os bucket create \
  --compartment-id ocid1.tenancy.oc1..aaaaaaaaf5453txsqxwvjht7iyhogdjmbgiebuar3mtohym6dgksocn67eua \
  --name my-bucket

# Upload file
oci os object put --bucket-name my-bucket --file /path/to/file

# Download file
oci os object get --bucket-name my-bucket --name filename --file /local/path
```

---

## Integration with Infrastructure

### Future Cloudflare Tunnel Setup

```bash
# On Oracle Cloud instance
CLOUDFLARE_API_TOKEN=ZAObC6_gFbJdwgAyEYHJw-XqSWuiOjbIiXa3nBwc \
cloudflared tunnel create oracle-cloud

# Route DNS
CLOUDFLARE_API_TOKEN=ZAObC6_gFbJdwgAyEYHJw-XqSWuiOjbIiXa3nBwc \
cloudflared tunnel route dns <TUNNEL_ID> oracle.vibhavaggarwal.com
```

### Tailscale Integration

```bash
# On Oracle Cloud instance
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up

# Get Tailscale IP
tailscale ip
```

---

## Resource OCIDs Reference

| Resource | OCID |
|----------|------|
| **Tenancy** | `ocid1.tenancy.oc1..aaaaaaaaf5453txsqxwvjht7iyhogdjmbgiebuar3mtohym6dgksocn67eua` |
| **User** | `ocid1.user.oc1..aaaaaaaabs6mokt2qcaie3uvabtosaoi4xjfjk3y32gwvhxsbscz5bwvx2ca` |
| **AMD Instance** | `ocid1.instance.oc1.ap-mumbai-1.anrg6ljrllerkbacghbwewkj6r3lst3s5s5jf26kpgvqfcbm7xb2cpeiryfq` |
| **VCN** | `ocid1.vcn.oc1.ap-mumbai-1.amaaaaaallerkbaavglktbs2icdhxg5qu4elo7ar3fsspqws527dql6qaxta` |
| **Subnet** | `ocid1.subnet.oc1.ap-mumbai-1.aaaaaaaackut2v6ls3slvemm4ci5txp3pvvxkdebsvun4ctvfoa3ql7ds6vq` |
| **Boot Volume** | `ocid1.bootvolume.oc1.ap-mumbai-1.abrg6ljr3g7tdswpecseql6yaznhxlt4z5hcah7tychtrh7bpubht7vwcu7a` |
| **Internet Gateway** | `ocid1.internetgateway.oc1.ap-mumbai-1.aaaaaaaahovvhslesdcldxxgen3t5hhchbsirnldinskvhlnp2ewjjz5sbxa` |

---

**Last Updated**: December 23, 2025
