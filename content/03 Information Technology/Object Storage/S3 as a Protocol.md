---
title: "S3 as a Protocol: Beyond Amazon's Object Storage"
tags:
  - object-storage
  - s3
  - infrastructure
  - digital-sovereignty
  - self-hosting
---

# S3 as a Protocol

Amazon's Simple Storage Service (S3) launched in 2006 as a proprietary cloud storage product. Two decades later, the S3 API has become something far more significant: a **de facto standard protocol** for object storage. Dozens of implementations exist, from self-hosted servers to competing cloud platforms, all speaking the same language. Understanding S3 as a protocol rather than a product is key to building sovereign, vendor-independent infrastructure.

## How S3 Became a Protocol

S3's dominance isn't accidental. Its API is simple, well-documented, and solves a universal problem: storing and retrieving arbitrary data (objects) by key. Over time, an entire ecosystem of tools, libraries, and applications adopted the S3 API as their storage backend. This created a powerful network effect: any storage system that speaks S3 instantly gains compatibility with thousands of existing tools.

```
S3 API: A Universal Storage Interface

┌─────────────────────────────────────────┐
│            Applications & Tools          │
│  (backup agents, databases, CI/CD,      │
│   media platforms, data pipelines...)    │
└────────────────┬────────────────────────┘
                 │ S3 API (HTTP REST)
                 ▼
┌─────────────────────────────────────────┐
│        Any S3-Compatible Backend         │
│                                          │
│  AWS S3 │ Cloudflare R2 │ RustFS        │
│  Garage │ Ceph RGW      │ SeaweedFS     │
└─────────────────────────────────────────┘
```

### What Makes S3 a Protocol

The S3 API is built on standard HTTP REST conventions:

- **Buckets** - Named containers that group objects (similar to top-level directories)
- **Objects** - Files identified by a key (path), stored with metadata
- **Operations** - Standard HTTP verbs: `PUT` to upload, `GET` to retrieve, `DELETE` to remove, `HEAD` for metadata
- **Authentication** - AWS Signature Version 4 (SigV4) for request signing
- **Multipart Upload** - Chunked uploads for large files
- **Presigned URLs** - Time-limited access links without requiring credentials

A typical S3 interaction looks like this:

```bash
# Upload a file
PUT /my-bucket/backups/2026-03-09.tar.gz HTTP/1.1
Host: s3.example.com
Authorization: AWS4-HMAC-SHA256 Credential=...

# Retrieve it
GET /my-bucket/backups/2026-03-09.tar.gz HTTP/1.1
Host: s3.example.com
Authorization: AWS4-HMAC-SHA256 Credential=...
```

Any client that can sign requests and speak HTTP can talk to any S3-compatible server. This simplicity is what enabled S3 to transcend its origins.

### S3 vs. Traditional Filesystems

| Feature | Traditional Filesystem | S3 Object Storage |
|---------|----------------------|-------------------|
| Access method | POSIX file paths, mount points | HTTP REST API |
| Structure | Hierarchical directories | Flat namespace with key prefixes |
| Metadata | Limited (permissions, timestamps) | Arbitrary key-value headers |
| Scaling | Vertical (bigger disks) | Horizontal (add more nodes) |
| Access scope | Local or network mount | Anywhere with HTTP access |
| Consistency | Immediate | Eventually consistent (historically), now strong consistency |

> [!NOTE] When to Use Object Storage
> Object storage excels at storing **unstructured data at scale**: backups, media files, static assets, log archives, and data lake contents. It is **not** a replacement for block storage (databases) or traditional filesystems (application code, OS files).

## S3-Compatible Implementations

The real power of S3-as-protocol is **choice**. You are not locked into Amazon. Here are strong options for sovereign infrastructure.

---

### RustFS

[RustFS](https://github.com/rustfs/rustfs) is a high-performance, S3-compatible object storage server written in Rust. It emerged as a community response to MinIO's licensing changes, offering a modern, permissively licensed alternative.

**Key Features:**
- Written in Rust for memory safety and performance
- S3-compatible API
- Designed as a drop-in replacement for MinIO use cases
- Active open-source development
- Lightweight single-binary deployment

**Quick Start:**

```bash
# Download and run RustFS
curl -LO https://github.com/rustfs/rustfs/releases/latest/download/rustfs-linux-amd64
chmod +x rustfs-linux-amd64

# Start the server
./rustfs-linux-amd64 server /data --console-address ":9001"
```

**When to choose RustFS:** You want a performant, self-hosted S3 server with a familiar MinIO-like experience but without the AGPL licensing concerns. Good for single-node or small-cluster deployments.

---

### Cloudflare R2

[Cloudflare R2](https://developers.cloudflare.com/r2/) is a managed S3-compatible object storage service with a game-changing pricing model: **zero egress fees**.

**Key Features:**
- Full S3 API compatibility (use existing S3 tools and SDKs)
- **No egress fees** - download your data without penalty
- Automatic global distribution via Cloudflare's network
- Workers integration for edge compute alongside storage
- Free tier: 10 GB storage, 10 million Class B operations/month

**Configuration with standard S3 tools:**

```bash
# Configure AWS CLI to use R2
aws configure set default.s3.endpoint_url https://<ACCOUNT_ID>.r2.cloudflarestorage.com
aws configure set default.region auto

# Use normally
aws s3 cp backup.tar.gz s3://my-bucket/backups/
aws s3 ls s3://my-bucket/
```

**When to choose R2:** You want managed storage without egress cost surprises. Excellent for public content delivery, backup storage you need to restore from, or any workload where data retrieval costs are a concern. Pairs well with Cloudflare Workers for serverless applications.

> [!TIP] Egress Fees Matter
> AWS S3 charges ~$0.09/GB for data transfer out. Serving 1 TB of content costs ~$90/month in egress alone. R2 charges $0 for this. For content-heavy workloads, this difference is enormous.

---

### Garage

[Garage](https://garagehq.deuxfleurs.fr/) is a lightweight, self-hosted, S3-compatible distributed object storage system built by [Deuxfleurs](https://deuxfleurs.fr/), a French libre hosting collective. It is purpose-built for **geo-distributed clusters on modest hardware**.

**Key Features:**
- Designed for **homelab and small-scale infrastructure**
- Runs on low-resource machines (Raspberry Pi, small VPS instances)
- Geo-distributed by design - replicate across locations
- S3-compatible API for standard tooling
- Written in Rust for efficiency
- AGPL v3 licensed (copyleft, but maintained by a community collective)
- Simple operational model - no complex dependencies

**Architecture:**

```
Garage Cluster: Geo-Distributed Object Storage

  Location A          Location B         Location C
┌────────────┐    ┌────────────┐    ┌────────────┐
│  Garage     │◄──►│  Garage     │◄──►│  Garage     │
│  Node       │    │  Node       │    │  Node       │
│  (RPi/VPS)  │    │  (RPi/VPS)  │    │  (RPi/VPS)  │
└────────────┘    └────────────┘    └────────────┘
       ▲                ▲                 ▲
       └────── Automatic replication ─────┘

Data is distributed and replicated across all zones.
```

**Quick Start:**

```bash
# Download Garage
curl -LO https://garagehq.deuxfleurs.fr/download/latest/x86_64-unknown-linux-musl/garage
chmod +x garage

# Generate initial configuration
garage server  # First run generates config template

# After configuring, start the node
garage -c /etc/garage.toml server
```

**Example `garage.toml` configuration:**

```toml
metadata_dir = "/var/lib/garage/meta"
data_dir = "/var/lib/garage/data"
db_engine = "lmdb"

replication_factor = 3

[s3_api]
s3_region = "garage"
api_bind_addr = "[::]:3900"
root_domain = ".s3.garage.localhost"

[rpc_secret_file]
path = "/etc/garage/rpc_secret"

[admin]
api_bind_addr = "[::]:3903"
```

**When to choose Garage:** You want to run object storage across multiple low-powered machines or locations. Ideal for homelab setups, community infrastructure, or when you want true geographic distribution without enterprise hardware. The Deuxfleurs collective's values align well with digital sovereignty principles.

---

### A Note on MinIO

> [!WARNING] MinIO Licensing Changes
> MinIO was long the default recommendation for self-hosted S3 storage. However, its licensing trajectory raises concerns for sovereign infrastructure:
>
> - **2018:** Changed from Apache 2.0 to **GNU AGPL v3** - any network-accessible deployment must share source code of modifications
> - **2024:** Introduced the **MinIO Enterprise License**, further restricting commercial and large-scale self-hosted use
> - **Telemetry concerns:** Subnet registration and call-home features added in recent versions
>
> While MinIO remains technically capable, the licensing direction signals a move away from community-first development. For new deployments focused on long-term sovereignty, consider **RustFS** or **Garage** instead.

## Working with S3: Universal Client Tools

Because S3 is a protocol, the same tools work across all implementations. Configure the endpoint URL and credentials, and you're connected to whichever backend you choose.

### AWS CLI

```bash
# Point at any S3-compatible endpoint
export AWS_ENDPOINT_URL=http://localhost:9000
export AWS_ACCESS_KEY_ID=minioadmin
export AWS_SECRET_ACCESS_KEY=minioadmin

aws s3 mb s3://my-bucket
aws s3 cp myfile.txt s3://my-bucket/
aws s3 ls s3://my-bucket/
```

### rclone

[rclone](https://rclone.org/) is a powerful tool for syncing data between storage backends, including any S3-compatible service.

```bash
# Configure an S3-compatible remote
rclone config create mystore s3 \
  provider=Other \
  endpoint=http://localhost:3900 \
  access_key_id=GKxxxx \
  secret_access_key=xxxx

# Sync a directory
rclone sync /local/backups mystore:backup-bucket
```

### Programming Libraries

Every major language has S3 client libraries. Here's Python with `boto3`:

```python
import boto3

s3 = boto3.client(
    "s3",
    endpoint_url="http://localhost:3900",
    aws_access_key_id="GKxxxx",
    aws_secret_access_key="xxxx",
    region_name="garage",
)

# Works identically regardless of backend
s3.upload_file("report.pdf", "documents", "reports/2026/march.pdf")
```

## Choosing an Implementation

| | RustFS | Cloudflare R2 | Garage |
|---|---|---|---|
| **Hosting** | Self-hosted | Managed (Cloudflare) | Self-hosted |
| **Language** | Rust | N/A (SaaS) | Rust |
| **Best for** | Single/small cluster | Public content, backups | Geo-distributed, homelab |
| **Min. hardware** | Moderate | None (cloud) | Very low (RPi capable) |
| **Replication** | Erasure coding | Automatic (managed) | Configurable (1-3+) |
| **Egress cost** | None (self-hosted) | Free | None (self-hosted) |
| **License** | Permissive | Proprietary (SaaS) | AGPL v3 |
| **Sovereignty** | Full control | Cloudflare dependency | Full control |

> [!TIP] Mix and Match
> Because S3 is a protocol, you can use **multiple backends** simultaneously. Store hot data on Cloudflare R2 for fast global delivery, replicate critical backups to a Garage cluster you control, and use rclone to keep them in sync. Protocol compatibility means no vendor lock-in.

## Digital Sovereignty and Object Storage

S3 compatibility is one of the clearest examples of how protocol standardization enables sovereignty:

1. **No lock-in** - Switch backends without changing applications
2. **Self-host option** - Run your own storage on hardware you control
3. **Data locality** - Choose where your data physically lives
4. **Cost control** - Avoid egress fees and unpredictable pricing
5. **Resilience** - Replicate across providers and geographies

> [!NOTE] Bridge to TWN
> Object storage is foundational infrastructure for digital sovereignty. Whether you're hosting a static site, running backups, or building a data platform, controlling your storage layer means controlling your data. Explore sovereign hosting providers at [TWN Systems](https://twn.systems) and discuss storage strategies in the [TWN Commons](https://discord.gg/kgaMm6WJya).

## Further Reading

- [[Object Storage]] - Object storage fundamentals
- [S3 API Reference (AWS)](https://docs.aws.amazon.com/AmazonS3/latest/API/Welcome.html) - The canonical API specification
- [Garage Documentation](https://garagehq.deuxfleurs.fr/documentation/quick-start/) - Getting started with Garage
- [RustFS GitHub](https://github.com/rustfs/rustfs) - Source code and documentation
- [Cloudflare R2 Docs](https://developers.cloudflare.com/r2/) - R2 developer documentation
- [rclone S3 Guide](https://rclone.org/s3/) - Using rclone with S3-compatible storage
