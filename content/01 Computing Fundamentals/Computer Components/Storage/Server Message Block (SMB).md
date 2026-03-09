---
title: Server Message Block (SMB)
tags:
  - networking
  - file-sharing
  - protocols
  - windows
  - samba
---

# Server Message Block (SMB)

Server Message Block (SMB) is a network file sharing protocol that allows applications and users to read, write, and request services from network resources. Originally developed by IBM in the 1980s and later extended significantly by Microsoft, SMB is the foundation of file and printer sharing in Windows environments and plays a critical role in enterprise networks worldwide.

```
SMB File Sharing - How It Works

  Client                              Server
┌──────────┐    SMB Negotiate    ┌──────────────┐
│          │ ──────────────────► │              │
│ Windows  │    Session Setup    │  File Server │
│ Linux    │ ◄──────────────────►│  (Windows /  │
│ macOS    │    Tree Connect     │   Samba)     │
│          │ ──────────────────► │              │
│          │    Read/Write       │  ┌────────┐  │
│          │ ◄──────────────────►│  │ Shares │  │
└──────────┘                     │  └────────┘  │
                                 └──────────────┘
     Port 445 (Direct SMB over TCP)
     Port 139 (SMB over NetBIOS - Legacy)
```

## SMB Protocol Versions

### SMB 1.0 / CIFS (1996)

The original widely-deployed version, also known as [[CIFS]] (Common Internet File System). Microsoft introduced SMB 1.0 with Windows NT 4.0.

**Key characteristics:**
- Chatty protocol with many round-trips per operation
- Opportunistic locking (oplocks) for caching
- NetBIOS over TCP/IP for name resolution and transport
- Uses ports 137-139 (NetBIOS) and port 445 (direct hosting)
- Maximum file size: theoretically unlimited but practically limited by implementation

**Security concerns:**
- No encryption of data in transit
- Vulnerable to man-in-the-middle attacks
- The **EternalBlue** exploit (CVE-2017-0144) targeted SMB 1.0 and enabled the WannaCry and NotPetya ransomware outbreaks
- NTLM relay attacks are possible
- Null session enumeration allows unauthenticated information gathering

> [!WARNING] SMB 1.0 is deprecated
> Microsoft deprecated SMB 1.0 in 2014 and began disabling it by default starting with Windows 10 Fall Creators Update (1709). **Do not use SMB 1.0 in production environments.** If you must support legacy devices, isolate them on a separate network segment.

**Disabling SMB 1.0:**

Windows (PowerShell):
```powershell
# Check SMB1 status
Get-SmbServerConfiguration | Select EnableSMB1Protocol

# Disable SMB1
Set-SmbServerConfiguration -EnableSMB1Protocol $false -Force

# Remove SMB1 feature entirely (Windows 10/11)
Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
```

Linux (Samba):
```ini
# /etc/samba/smb.conf
[global]
    min protocol = SMB2
    # Or more restrictively:
    # min protocol = SMB3
```

### SMB 2.0 (2006)

Introduced with Windows Vista and Windows Server 2008, SMB 2.0 was a major overhaul that addressed the performance and security shortcomings of SMB 1.0.

**Improvements over SMB 1.0:**
- **Reduced chattiness** - Compound commands combine multiple operations into a single request
- **Pipelining** - Send multiple requests without waiting for responses
- **Larger reads/writes** - Buffer sizes increased from 64 KB to 1 MB
- **Durable file handles** - Survive brief network disconnections
- **Symbolic link support** - Server-side symlink resolution
- **Message signing with HMAC-SHA256** - Stronger integrity protection

### SMB 2.1 (2010)

Released with Windows 7 and Windows Server 2008 R2.

**Additions:**
- **BranchCache support** - Content caching for branch office scenarios
- **Larger MTU support** - Improved performance on high-speed networks
- **Lease oplocks** - More efficient client caching mechanism

### SMB 3.0 (2012)

Introduced with Windows 8 and Windows Server 2012. This was a transformative release focused on datacenter and cloud workloads.

**Major features:**
- **SMB Encryption** - AES-128-CCM end-to-end encryption without requiring IPsec
- **SMB Direct (RDMA)** - Remote Direct Memory Access support for high-throughput, low-latency access
- **SMB Multichannel** - Aggregate multiple network connections for bandwidth and failover
- **SMB Transparent Failover** - Seamless failover for clustered file servers
- **VSS Remote File Snapshots** - Access Volume Shadow Copy snapshots remotely
- **SMB Scale-Out** - Concurrent access from multiple cluster nodes

```
SMB 3.0 Multichannel - Bandwidth Aggregation

  Client                              Server
┌──────────┐                     ┌──────────────┐
│          │── NIC 1 (10 Gbps) ──│              │
│          │── NIC 2 (10 Gbps) ──│  File Server │
│          │── NIC 3 (10 Gbps) ──│              │
└──────────┘                     └──────────────┘
         Total: Up to 30 Gbps aggregate
         + Automatic failover if a NIC fails
```

### SMB 3.0.2 (2014)

Released with Windows 8.1 and Windows Server 2012 R2.

**Additions:**
- Ability to disable SMB 1.0 without removing the feature
- Improved performance for clustered shared volumes

### SMB 3.1.1 (2015)

Released with Windows 10 and Windows Server 2016. The current and most secure version.

**Security enhancements:**
- **AES-128-GCM encryption** - More efficient authenticated encryption (in addition to AES-128-CCM)
- **Pre-authentication integrity** - SHA-512 hash protects the negotiate and session setup exchange from tampering
- **Cluster dialect fencing** - Prevents downgrade attacks in failover clusters
- **Encryption negotiation** - Mandatory encryption can be required per-share

**Added in later updates (Windows Server 2022 / Windows 11):**
- **AES-256-GCM and AES-256-CCM** encryption
- **SMB over QUIC** - Access file shares over the internet without VPN (port 443)
- **SMB compression** - Compress data in transit for better WAN performance

```
SMB Version Summary

Version │ Year │ Windows Version         │ Key Feature
────────┼──────┼─────────────────────────┼──────────────────────────
1.0     │ 1996 │ NT 4.0                  │ Original (DEPRECATED)
2.0     │ 2006 │ Vista / Server 2008     │ Reduced chattiness
2.1     │ 2010 │ 7 / Server 2008 R2     │ BranchCache, leases
3.0     │ 2012 │ 8 / Server 2012        │ Encryption, Multichannel
3.0.2   │ 2014 │ 8.1 / Server 2012 R2   │ Disable SMB1
3.1.1   │ 2015 │ 10 / Server 2016+      │ Pre-auth integrity, GCM
```

## Samba

Samba is the open-source implementation of SMB/CIFS for Unix/Linux systems. It enables Linux and macOS machines to participate in Windows-based file sharing networks as both clients and servers.

### Samba as a File Server

Samba allows Linux servers to share files and printers with Windows, macOS, and Linux clients.

**Installation:**
```bash
# Debian/Ubuntu
sudo apt install samba samba-common-bin

# RHEL/Fedora/Rocky
sudo dnf install samba samba-common samba-client

# Arch Linux
sudo pacman -S samba
```

**Basic configuration (`/etc/samba/smb.conf`):**
```ini
[global]
    workgroup = WORKGROUP
    server string = Samba File Server
    security = user
    map to guest = never
    min protocol = SMB3

    # Logging
    log file = /var/log/samba/log.%m
    max log size = 1000

    # Performance tuning
    socket options = TCP_NODELAY IPTOS_LOWDELAY
    read raw = yes
    write raw = yes

    # Security hardening
    server signing = mandatory
    smb encrypt = required    # Enforce SMB 3.x encryption

[shared]
    path = /srv/samba/shared
    browseable = yes
    read only = no
    valid users = @smbgroup
    create mask = 0660
    directory mask = 0770
    force group = smbgroup

[projects]
    path = /srv/samba/projects
    browseable = yes
    read only = no
    valid users = @developers
    write list = @developers
    create mask = 0664
    directory mask = 0775
    vfs objects = recycle
    recycle:repository = .recycle
    recycle:keeptree = yes
```

**User management:**
```bash
# Add a system user (if not existing)
sudo useradd -M -s /usr/sbin/nologin smbuser

# Set Samba password (separate from system password)
sudo smbpasswd -a smbuser

# Enable the user
sudo smbpasswd -e smbuser

# Create group and add user
sudo groupadd smbgroup
sudo usermod -aG smbgroup smbuser

# Prepare the share directory
sudo mkdir -p /srv/samba/shared
sudo chown root:smbgroup /srv/samba/shared
sudo chmod 2770 /srv/samba/shared
```

**Service management:**
```bash
# Start and enable Samba
sudo systemctl enable --now smbd nmbd

# Test configuration
testparm

# List shares
smbclient -L //localhost -U smbuser
```

### Samba as an Active Directory Domain Controller

Samba 4 can function as a full Active Directory Domain Controller, providing:
- Kerberos authentication (KDC)
- LDAP directory services
- DNS server
- Group Policy support
- Domain join for Windows clients

**Provisioning a new AD domain:**
```bash
# Install Samba with AD support
sudo apt install samba krb5-user smbclient winbind

# Stop existing services
sudo systemctl stop smbd nmbd winbind
sudo systemctl disable smbd nmbd winbind

# Back up existing config
sudo mv /etc/samba/smb.conf /etc/samba/smb.conf.bak

# Provision the domain
sudo samba-tool domain provision \
    --use-rfc2307 \
    --realm=CORP.EXAMPLE.COM \
    --domain=CORP \
    --server-role=dc \
    --dns-backend=SAMBA_INTERNAL \
    --adminpass='SecureP@ssw0rd!'

# Configure Kerberos
sudo cp /var/lib/samba/private/krb5.conf /etc/krb5.conf

# Start Samba AD DC
sudo systemctl unmask samba-ad-dc
sudo systemctl enable --now samba-ad-dc
```

**Verify the domain controller:**
```bash
# Test DNS
host -t SRV _ldap._tcp.corp.example.com localhost
host -t SRV _kerberos._tcp.corp.example.com localhost

# Test Kerberos
kinit administrator@CORP.EXAMPLE.COM

# List domain users
samba-tool user list

# Test SMB access
smbclient //localhost/netlogon -U administrator -c 'ls'
```

> [!TIP] Samba AD vs Microsoft AD
> Samba's AD implementation is compatible with Windows AD but has some limitations around advanced Group Policy features and certain newer AD schema extensions. For environments that need full AD feature parity, consider running Windows Server AD DCs alongside Samba for specific services. Samba AD is excellent for smaller environments or as a sovereignty-preserving alternative.

## Active Directory File Sharing

In Active Directory environments, file sharing integrates tightly with domain services to provide centralized access control, auditing, and management.

### How AD File Sharing Works

```
Active Directory File Sharing Architecture

┌─────────────────────────────────────────────────────┐
│                Active Directory                      │
│  ┌──────────┐  ┌──────────┐  ┌───────────────────┐ │
│  │ Kerberos │  │   LDAP   │  │   Group Policy    │ │
│  │   KDC    │  │ Directory│  │   (GPO for shares)│ │
│  └────┬─────┘  └────┬─────┘  └────────┬──────────┘ │
└───────┼──────────────┼─────────────────┼────────────┘
        │              │                 │
   ┌────▼──────────────▼─────────────────▼────┐
   │            File Server                    │
   │  ┌─────────────────────────────────────┐  │
   │  │  Share: \\server\finance$           │  │
   │  │  NTFS Permissions + Share Perms     │  │
   │  │  Access Based Enumeration: ON       │  │
   │  │  DFS Namespace: \\corp\shares\fin   │  │
   │  └─────────────────────────────────────┘  │
   └──────────────────────────────────────────-┘
        ▲                           ▲
   Kerberos ticket             Kerberos ticket
        │                           │
   ┌────┴─────┐              ┌──────┴───┐
   │  Domain   │              │  Domain  │
   │  User A   │              │  User B  │
   │ (Finance) │              │ (IT Ops) │
   └──────────┘              └──────────┘
   ✅ Can access                ❌ Access denied
```

### Authentication Flow

1. **User logs into domain workstation** - Receives a Kerberos Ticket Granting Ticket (TGT) from the Domain Controller
2. **User accesses a file share** (e.g., `\\fileserver\projects`) - The client requests a Service Ticket from the KDC for the file server's SPN
3. **Client presents Service Ticket to file server** - Server validates the ticket and checks group membership
4. **Access is evaluated** - Both share-level and NTFS permissions are checked; the most restrictive combination applies
5. **Session established** - SMB session is created with the user's security context

### Share and NTFS Permissions

File access in Windows/AD environments uses two layers of permissions:

**Share Permissions** (apply only to network access):
- Full Control, Change, Read
- Apply at the share level
- Best practice: Set to "Authenticated Users: Full Control" and control access via NTFS permissions

**NTFS Permissions** (apply to both local and network access):
- Full Control, Modify, Read & Execute, List Folder Contents, Read, Write
- Support inheritance from parent folders
- Allow granular per-user and per-group control
- Support explicit Deny entries (override Allow)

```powershell
# Create a new SMB share with AD security group
New-SmbShare -Name "Projects" `
    -Path "D:\Shares\Projects" `
    -FullAccess "CORP\Domain Admins" `
    -ChangeAccess "CORP\Project-Managers" `
    -ReadAccess "CORP\All-Staff"

# Set NTFS permissions
$acl = Get-Acl "D:\Shares\Projects"
$rule = New-Object System.Security.AccessControl.FileSystemAccessRule(
    "CORP\Project-Managers", "Modify", "ContainerInherit,ObjectInherit", "None", "Allow"
)
$acl.AddAccessRule($rule)
Set-Acl "D:\Shares\Projects" $acl

# Enable Access Based Enumeration (users only see folders they can access)
Set-SmbShare -Name "Projects" -FolderEnumerationMode AccessBased
```

### DFS Namespaces

Distributed File System (DFS) Namespaces provide a unified namespace that abstracts the physical location of shared folders:

```
Without DFS:                      With DFS:
\\server1\finance                 \\corp.example.com\shares\finance
\\server2\engineering             \\corp.example.com\shares\engineering
\\server3\hr                      \\corp.example.com\shares\hr

Users don't need to know          One namespace, multiple
which server hosts what           underlying servers
```

**Benefits:**
- Server migration is transparent to users
- Load balancing across multiple servers via DFS Replication
- Simplified access paths for end users
- Referral-based redirection

### Group Policy for File Shares

Map network drives automatically using Group Policy:
- **Group Policy Preferences > Drive Maps** - Map drives based on group membership
- **Folder Redirection** - Redirect Desktop, Documents, etc. to network shares
- **Offline Files** - Cache network files for disconnected use

## Connecting to SMB Shares

### From Windows

```powershell
# Map a network drive
net use Z: \\fileserver\shared /user:CORP\username

# Using PowerShell
New-PSDrive -Name "Z" -PSProvider FileSystem -Root "\\fileserver\shared" -Persist

# List current connections
net use

# Browse available shares
net view \\fileserver
```

### From Linux

```bash
# One-time mount
sudo mount -t cifs //fileserver/shared /mnt/shared \
    -o username=user,domain=CORP,vers=3.1.1,sec=krb5

# Using credentials file (more secure)
# Create /root/.smbcredentials:
#   username=user
#   password=secret
#   domain=CORP
sudo mount -t cifs //fileserver/shared /mnt/shared \
    -o credentials=/root/.smbcredentials,vers=3.1.1

# Persistent mount via /etc/fstab
# //fileserver/shared  /mnt/shared  cifs  credentials=/root/.smbcredentials,vers=3.1.1,_netdev  0  0

# Browse shares with smbclient
smbclient -L //fileserver -U user

# Interactive smbclient session
smbclient //fileserver/shared -U CORP\\user
```

### From macOS

```bash
# Mount via command line
mount_smbfs //user@fileserver/shared /Volumes/shared

# Or use Finder: Go > Connect to Server > smb://fileserver/shared
```

## Security Best Practices

### Protocol Hardening

```ini
# Samba: /etc/samba/smb.conf
[global]
    # Enforce modern protocol versions
    min protocol = SMB3
    max protocol = SMB3

    # Require signing
    server signing = mandatory

    # Require encryption
    smb encrypt = required

    # Disable guest access
    map to guest = never
    restrict anonymous = 2

    # Disable unused features
    ntlm auth = ntlmv2-only
    lanman auth = no
    client NTLMv2 auth = yes
```

```powershell
# Windows: Enforce SMB encryption and signing
Set-SmbServerConfiguration -EncryptData $true -Force
Set-SmbServerConfiguration -RequireSecuritySignature $true -Force

# Disable SMB 1.0
Set-SmbServerConfiguration -EnableSMB1Protocol $false -Force

# Audit SMB access
Set-SmbServerConfiguration -AuditSmb1Access $true -Force
```

### Network Security

- **Firewall rules** - Only allow SMB traffic (port 445) from trusted networks. Never expose SMB directly to the internet.
- **Network segmentation** - Place file servers in dedicated VLANs with controlled access
- **VPN for remote access** - Use SMB over QUIC (Windows Server 2022+) or VPN tunnels for remote file access
- **Disable NetBIOS** - Block ports 137-139 if not needed for legacy compatibility

### Monitoring and Auditing

```powershell
# Windows: Enable file access auditing
auditpol /set /subcategory:"File Share" /success:enable /failure:enable
auditpol /set /subcategory:"File System" /success:enable /failure:enable

# Check active SMB sessions
Get-SmbSession

# View open files
Get-SmbOpenFile

# Check SMB connection details (encryption, dialect)
Get-SmbConnection
```

```bash
# Linux/Samba: View active connections
sudo smbstatus

# View connected users
sudo smbstatus -b

# View locked files
sudo smbstatus -L
```

## Troubleshooting

| Symptom | Possible Cause | Solution |
|---------|---------------|----------|
| "Access Denied" | Permission mismatch | Check both share and NTFS permissions; verify group membership |
| Cannot browse shares | NetBIOS disabled or firewall | Ensure port 445 is open; check `Computer Browser` service |
| Slow file transfers | SMB 1.0 in use or no multichannel | Verify negotiated dialect with `Get-SmbConnection`; check NIC config |
| "The specified network name is no longer available" | Signing/encryption mismatch | Ensure both sides agree on signing and encryption requirements |
| Linux mount fails | Missing `cifs-utils` package | Install `cifs-utils`; check `vers=` mount option |
| Intermittent disconnects | Durable handles not supported | Upgrade to SMB 3.x; check for network instability |

## SMB vs NFS Comparison

| Feature | SMB | [[Network File System (NFS)\|NFS]] |
|---------|-----|-----|
| Primary OS | Windows | Linux/Unix |
| Authentication | NTLM / Kerberos / AD | Kerberos / AUTH_SYS (IP-based) |
| Encryption | Built-in (SMB 3.0+) | Kerberos or TLS (NFSv4) |
| Port | 445 | 2049 |
| Lock management | Built-in | NLM (v3) / built-in (v4) |
| Performance | Good; Multichannel in 3.0+ | Generally faster on Linux |
| Windows support | Native | Requires NFS client feature |
| Linux support | Via CIFS/Samba | Native |
| Best for | Mixed OS, AD environments | Linux-only environments |

> [!TIP] Need guidance?
> Join the [TWN Commons on Discord](https://discord.gg/kgaMm6WJya) to ask questions about file sharing, Samba configuration, or Active Directory setup.

> [!NOTE] Bridge to TWN
> Understanding SMB and file sharing gives you the power to build your own sovereign file infrastructure. Instead of relying on cloud storage providers, deploy self-hosted file servers with Samba and maintain full control over your data. Explore sovereignty-focused hosting options at [TWN Systems](https://twn.systems).
