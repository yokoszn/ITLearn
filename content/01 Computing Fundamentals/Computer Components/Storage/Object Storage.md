---
title: Object Storage
tags:
  - storage
  - fundamentals
  - object-storage
---

# Object Storage

Object storage is a data architecture that manages data as **objects** rather than as files in a hierarchy (file storage) or blocks on a disk (block storage). Each object contains the data itself, metadata, and a unique identifier.

## Key Characteristics

- **Flat namespace** - Objects are accessed by key, not by navigating directory trees
- **Rich metadata** - Arbitrary key-value pairs attached to each object
- **HTTP access** - Typically accessed via REST APIs rather than filesystem mounts
- **Massive scalability** - Designed to store billions of objects across distributed systems
- **Durability** - Built-in replication and erasure coding for data protection

## Common Use Cases

- Backup and archival storage
- Static website and media hosting
- Data lake and analytics storage
- Application asset storage (images, documents, videos)
- Log aggregation and retention

## The S3 Protocol

The most widely adopted object storage interface is the **S3 API**, originally created by Amazon but now a de facto industry standard. Dozens of implementations exist, from self-hosted servers to competing cloud platforms.

See [[S3 as a Protocol]] for a deep dive into S3-compatible implementations including RustFS, Cloudflare R2, and Garage.

## Object Storage vs. Other Storage Types

| | Object Storage | Block Storage | File Storage |
|---|---|---|---|
| **Access** | HTTP REST API | Raw device (iSCSI, FC) | Network mount (NFS, SMB) |
| **Structure** | Flat key-value | Fixed-size blocks | Hierarchical directories |
| **Best for** | Unstructured data at scale | Databases, VMs | Shared files, home dirs |
| **Scalability** | Horizontal, massive | Vertical, limited | Moderate |
| **Latency** | Higher (HTTP overhead) | Lowest | Low to moderate |

> [!TIP] Choosing Storage Types
> Most infrastructure uses a mix: **block storage** for databases and boot volumes, **file storage** for shared application data, and **object storage** for everything else (backups, media, logs, archives).
