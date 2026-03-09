---
title: Common Internet File System (CIFS)
tags:
  - networking
  - file-sharing
  - protocols
---

# Common Internet File System (CIFS)

CIFS (Common Internet File System) is Microsoft's renamed and extended version of [[Server Message Block (SMB)|SMB 1.0]], introduced in 1996. The name "CIFS" was an attempt to position the protocol as an internet standard alongside protocols like HTTP and FTP.

## CIFS vs SMB

While the terms are sometimes used interchangeably, there is an important distinction:

| Aspect | CIFS | SMB |
|--------|------|-----|
| Protocol version | SMB 1.0 only | SMB 1.0, 2.0, 2.1, 3.0, 3.1.1 |
| Status | **Deprecated** | Actively developed |
| Performance | Chatty, high latency | Efficient (SMB 2.0+) |
| Security | Weak (no encryption) | Strong (SMB 3.0+ encryption) |
| Modern usage | Legacy only | Current standard |

> [!WARNING] CIFS is deprecated
> CIFS refers specifically to SMB 1.0, which is deprecated and carries serious security vulnerabilities (including the EternalBlue exploit). Always use SMB 3.x in modern environments. See [[Server Message Block (SMB)]] for details on modern SMB versions.

## The Linux `cifs` Mount Type

On Linux, the `mount -t cifs` command and the `cifs-utils` package support modern SMB versions despite the legacy name. The `vers=` mount option controls which SMB version is negotiated:

```bash
# This uses SMB 3.1.1 despite the "cifs" type name
sudo mount -t cifs //server/share /mnt/share -o vers=3.1.1,username=user
```

The naming is a historical artifact — the Linux kernel module was written when "CIFS" was the common term for the protocol.

## Further Reading

See [[Server Message Block (SMB)]] for comprehensive coverage of:
- SMB protocol versions 1.0 through 3.1.1
- Samba configuration and Active Directory integration
- Security hardening and best practices
- Troubleshooting common issues
