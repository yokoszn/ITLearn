---
title: SNMP and Syslog - Network Monitoring Fundamentals
tags:
  - networking
  - monitoring
  - snmp
  - syslog
  - protocols
---

# SNMP and Syslog - Network Monitoring Fundamentals

Understanding how to monitor and manage network devices is a critical skill for any IT professional. Two foundational protocols make this possible: **SNMP** (Simple Network Management Protocol) for querying and managing devices, and **Syslog** for centralized log collection. Together, they form the backbone of network observability.

```
📊 Network Monitoring Architecture

                    ┌─────────────────────┐
                    │   NMS / Monitoring   │
                    │   (Nagios, Zabbix,   │
                    │    LibreNMS, PRTG)   │
                    └────────┬────────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
         SNMP Polls    SNMP Traps     Syslog Messages
         (UDP 161)     (UDP 162)      (UDP 514)
              │              │              │
       ┌──────┴──────┐  ┌───┴───┐   ┌──────┴──────┐
       │   Routers   │  │ Traps │   │  All Network │
       │  Switches   │  │ from  │   │   Devices    │
       │  Firewalls  │  │ any   │   │  Servers     │
       │  Servers    │  │ device │   │  Firewalls   │
       └─────────────┘  └───────┘   └──────────────┘
```

---

## SNMP - Simple Network Management Protocol

SNMP is a protocol used to **query, monitor, and configure** network devices remotely. It operates on a manager-agent model where a central management station communicates with agents running on network devices.

### How SNMP Works

SNMP uses a simple request-response model:

1. **SNMP Manager (NMS)** - The central monitoring system that sends queries and receives data
2. **SNMP Agent** - Software running on managed devices (routers, switches, servers, printers)
3. **Management Information Base (MIB)** - A structured database of objects that can be queried on a device

```
🔄 SNMP Communication Flow

  SNMP Manager                          SNMP Agent
  (NMS)                                 (Network Device)
       │                                      │
       │── GET Request (OID) ────────────────>│
       │<──── GET Response (Value) ───────────│
       │                                      │
       │── SET Request (OID + Value) ────────>│
       │<──── SET Response (Confirmation) ────│
       │                                      │
       │── GETNEXT (Walk the MIB) ──────────>│
       │<──── Response (Next OID + Value) ────│
       │                                      │
       │<──── TRAP (Unsolicited Alert) ───────│  ← Agent-initiated!
       │                                      │
```

### SNMP Operations

| Operation   | Direction        | Purpose                                   |
|-------------|------------------|-------------------------------------------|
| `GET`       | Manager → Agent  | Retrieve a specific OID value              |
| `GETNEXT`   | Manager → Agent  | Retrieve the next OID in the MIB tree      |
| `GETBULK`   | Manager → Agent  | Retrieve large sections of a MIB (v2c/v3)  |
| `SET`        | Manager → Agent  | Modify a value on the device               |
| `TRAP`       | Agent → Manager  | Unsolicited alert sent by the agent        |
| `INFORM`     | Agent → Manager  | Acknowledged trap (v2c/v3)                 |

### The MIB and OIDs

Every piece of data an SNMP agent can report is identified by an **Object Identifier (OID)** — a unique numerical address in a hierarchical tree structure.

```
🌳 OID Tree Structure (Simplified)

iso(1)
 └── org(3)
      └── dod(6)
           └── internet(1)
                └── mgmt(2)
                     └── mib-2(1)
                          ├── system(1)
                          │    ├── sysDescr(1)     → 1.3.6.1.2.1.1.1
                          │    ├── sysUpTime(3)    → 1.3.6.1.2.1.1.3
                          │    ├── sysContact(4)   → 1.3.6.1.2.1.1.4
                          │    └── sysName(5)      → 1.3.6.1.2.1.1.5
                          ├── interfaces(2)
                          │    ├── ifNumber(1)     → 1.3.6.1.2.1.2.1
                          │    └── ifTable(2)      → 1.3.6.1.2.1.2.2
                          └── ip(4)
                               └── ...
```

**Common OIDs you'll use regularly:**

| OID                    | Name           | Returns                            |
|------------------------|----------------|------------------------------------|
| `1.3.6.1.2.1.1.1`     | sysDescr       | Device description                 |
| `1.3.6.1.2.1.1.3`     | sysUpTime      | Time since last reboot             |
| `1.3.6.1.2.1.1.5`     | sysName        | Hostname of the device             |
| `1.3.6.1.2.1.2.2.1.10`| ifInOctets     | Bytes received on an interface     |
| `1.3.6.1.2.1.2.2.1.16`| ifOutOctets    | Bytes transmitted on an interface  |
| `1.3.6.1.2.1.25.1.1`  | hrSystemUptime | Host uptime (HOST-RESOURCES-MIB)   |

---

## SNMP Versions Compared

### SNMPv1 - The Original (RFC 1157, 1990)

The first version of SNMP, still widely supported but considered **insecure**.

**How it works:**
- Uses **community strings** for authentication — essentially a plaintext password sent with every request
- Default community strings: `public` (read-only) and `private` (read-write)
- No encryption — all data including the community string travels in cleartext

**Key characteristics:**
- Simple 32-bit counters (wrap around at ~4.3 billion — problematic on high-speed interfaces)
- Basic error handling
- Only supports TRAP for agent-initiated messages (no acknowledgment)

**Example — querying with SNMPv1:**
```bash
# Get system description using SNMPv1
snmpget -v1 -c public 192.168.1.1 1.3.6.1.2.1.1.1.0

# Walk the entire system MIB subtree
snmpwalk -v1 -c public 192.168.1.1 1.3.6.1.2.1.1
```

> [!WARNING] Security Risk
> SNMPv1 transmits community strings in **plaintext**. Anyone with a packet capture tool on the network can read them. Never use SNMPv1 on untrusted networks, and always change default community strings.

### SNMPv2c - Improved Performance, Same Security Model (RFC 3416, 2002)

SNMPv2c added performance improvements while keeping the community-string authentication model (the "c" stands for "community").

**Improvements over v1:**
- **GETBULK operation** — retrieve large tables efficiently in a single request instead of walking one OID at a time
- **INFORM operation** — like TRAP but with acknowledgment, so the manager confirms receipt
- **64-bit counters** (Counter64) — solves the counter wrap problem on high-speed interfaces (10 Gbps+)
- Better error handling with more detailed error codes

**Example — querying with SNMPv2c:**
```bash
# Get system uptime using SNMPv2c
snmpget -v2c -c public 192.168.1.1 1.3.6.1.2.1.1.3.0

# Bulk retrieve interface table (much faster than walk for large tables)
snmpbulkget -v2c -c public -Cr10 192.168.1.1 1.3.6.1.2.1.2.2

# Walk with v2c (uses GETBULK internally for efficiency)
snmpbulkwalk -v2c -c public 192.168.1.1 1.3.6.1.2.1.2.2
```

**Still insecure:** Community strings are still sent in cleartext. The "v2c" compromise kept the simple auth model because the original SNMPv2 security features were too complex to implement.

### SNMPv3 - Security Finally Done Right (RFC 3414, 2004)

SNMPv3 is the current standard and adds proper **authentication, encryption, and access control**. It replaces community strings with a user-based security model.

**Security features:**

| Feature          | Description                                              |
|------------------|----------------------------------------------------------|
| Authentication   | Verify message sender identity (MD5, SHA, SHA-256, SHA-512) |
| Encryption       | Encrypt message contents (DES, 3DES, AES-128/192/256)    |
| Message Integrity| Detect message tampering in transit                      |
| Access Control   | Fine-grained control over who can access what            |

**SNMPv3 Security Levels:**

| Level            | Auth | Encryption | Use Case                              |
|------------------|------|------------|---------------------------------------|
| `noAuthNoPriv`   | No   | No         | Similar to v1/v2c (not recommended)   |
| `authNoPriv`     | Yes  | No         | Verified sender, readable data        |
| `authPriv`       | Yes  | Yes        | Full security (recommended)           |

**Example — querying with SNMPv3:**
```bash
# SNMPv3 with authentication only (authNoPriv)
snmpget -v3 -u monitorUser -l authNoPriv \
  -a SHA -A 'MyAuthPass123' \
  192.168.1.1 1.3.6.1.2.1.1.1.0

# SNMPv3 with authentication AND encryption (authPriv) — recommended
snmpget -v3 -u monitorUser -l authPriv \
  -a SHA -A 'MyAuthPass123' \
  -x AES -X 'MyPrivPass456' \
  192.168.1.1 1.3.6.1.2.1.1.1.0

# Walk with full SNMPv3 security
snmpwalk -v3 -u monitorUser -l authPriv \
  -a SHA-256 -A 'MyAuthPass123' \
  -x AES -X 'MyPrivPass456' \
  192.168.1.1 1.3.6.1.2.1.2.2
```

**Configuring SNMPv3 on a Cisco device:**
```
! Create an SNMPv3 group with read-only access and full security
snmp-server group MONITORS v3 priv read MONITOR-VIEW

! Create a view limiting what the group can see
snmp-server view MONITOR-VIEW iso included

! Create a user in the group with SHA auth and AES encryption
snmp-server user monitorUser MONITORS v3 auth sha AuthPass123 priv aes 128 PrivPass456
```

### Version Comparison Summary

```
┌────────────────┬──────────┬──────────┬──────────┐
│ Feature        │  SNMPv1  │ SNMPv2c  │  SNMPv3  │
├────────────────┼──────────┼──────────┼──────────┤
│ Authentication │Community │Community │ Username │
│                │(plaintext)│(plaintext)│ + Password│
│ Encryption     │   None   │   None   │ AES/DES  │
│ Counter Size   │  32-bit  │  64-bit  │  64-bit  │
│ GETBULK        │    No    │   Yes    │   Yes    │
│ INFORM         │    No    │   Yes    │   Yes    │
│ Access Control │  Basic   │  Basic   │ VACM     │
│ Still Used?    │  Legacy  │  Common  │ Required │
│                │  only    │          │ for security│
└────────────────┴──────────┴──────────┴──────────┘
```

> [!TIP] Which version should you use?
> **Always use SNMPv3 with `authPriv`** for production environments. Use v2c only in isolated lab networks where security is not a concern. Avoid v1 entirely on modern networks.

---

## SNMP in Practice - Monitoring Use Cases

### Interface Monitoring

The most common SNMP use case is tracking interface bandwidth, errors, and status:

```bash
# Check interface status (up/down)
snmpwalk -v2c -c public 192.168.1.1 IF-MIB::ifOperStatus

# Monitor bandwidth usage (poll every 5 minutes, calculate delta)
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifHCInOctets.1
snmpget -v2c -c public 192.168.1.1 IF-MIB::ifHCOutOctets.1

# Check for interface errors
snmpwalk -v2c -c public 192.168.1.1 IF-MIB::ifInErrors
snmpwalk -v2c -c public 192.168.1.1 IF-MIB::ifOutErrors
```

### CPU and Memory Monitoring

```bash
# Cisco CPU utilization (1 min, 5 min averages)
snmpget -v2c -c public 192.168.1.1 \
  1.3.6.1.4.1.9.9.109.1.1.1.1.7.1 \
  1.3.6.1.4.1.9.9.109.1.1.1.1.8.1

# Linux host memory (via HOST-RESOURCES-MIB)
snmpwalk -v2c -c public 192.168.1.100 HOST-RESOURCES-MIB::hrStorageTable
```

### SNMP Traps - Event-Driven Monitoring

Instead of polling, devices can push alerts to the manager when something happens:

```
Common SNMP Traps:
├── linkDown        → An interface went down
├── linkUp          → An interface came back up
├── coldStart       → Device rebooted
├── warmStart       → Agent restarted
├── authFailure     → Someone used the wrong community string
└── Vendor-specific → Fan failure, high temperature, PSU alert, etc.
```

**Configuring trap destinations on a Cisco device:**
```
! Send traps to the NMS at 10.0.0.50 using SNMPv3
snmp-server host 10.0.0.50 version 3 priv monitorUser

! Enable specific trap types
snmp-server enable traps snmp linkdown linkup coldstart
snmp-server enable traps config
snmp-server enable traps envmon fan shutdown supply temperature
```

---

## Syslog - Centralized Log Management

While SNMP is built for querying metrics and status, **Syslog** is designed for streaming log messages from devices to a central collector. It captures everything from informational messages to critical errors.

### How Syslog Works

Syslog follows a simple model: devices generate log messages and send them to one or more **syslog servers** (collectors).

```
📨 Syslog Message Flow

  Network Devices                    Syslog Server
  ┌──────────┐                    ┌──────────────────┐
  │  Router   │───UDP 514────────>│                  │
  │  Switch   │───UDP 514────────>│  rsyslog /       │
  │  Firewall │───TCP 514────────>│  syslog-ng /     │
  │  Server   │───TLS 6514──────>│  Graylog /       │
  │  AP       │───UDP 514────────>│  ELK Stack       │
  └──────────┘                    │                  │
                                  │  → Parse         │
                                  │  → Store         │
                                  │  → Alert         │
                                  │  → Dashboard     │
                                  └──────────────────┘
```

### Syslog Message Format

Every syslog message contains a **facility** (what generated it) and a **severity** (how important it is).

**Syslog Severity Levels (RFC 5424):**

| Level | Keyword       | Description                              | Example                        |
|-------|---------------|------------------------------------------|--------------------------------|
| 0     | Emergency     | System is unusable                       | Kernel panic                   |
| 1     | Alert         | Immediate action required                | Database corruption detected   |
| 2     | Critical      | Critical conditions                      | Hardware failure               |
| 3     | Error         | Error conditions                         | Disk write failure             |
| 4     | Warning       | Warning conditions                       | Filesystem 90% full            |
| 5     | Notice        | Normal but significant                   | User login from new IP         |
| 6     | Informational | General information                      | Interface up/down              |
| 7     | Debug         | Debug-level messages                     | Packet processing details      |

> [!TIP] Remember the severity levels
> A common mnemonic: **"Every Alley Cat Eats Watery Noodle In Dishes"** (Emergency, Alert, Critical, Error, Warning, Notice, Informational, Debug). Lower number = higher severity.

**Syslog Facilities:**

| Code | Facility         | Description                    |
|------|------------------|--------------------------------|
| 0    | kern             | Kernel messages                |
| 1    | user             | User-level messages            |
| 3    | daemon           | System daemons                 |
| 4    | auth             | Authentication/security        |
| 10   | authpriv         | Private authentication         |
| 16-23| local0-local7    | Custom/locally defined use     |

**Priority value** is calculated as: `Priority = (Facility × 8) + Severity`

For example, a kernel (0) emergency (0) = priority 0, while a local0 (16) warning (4) = priority 132.

### Syslog Message Structure

```
RFC 5424 Format:
<priority>version timestamp hostname app-name procid msgid structured-data msg

Example:
<134>1 2026-03-09T14:22:01.123Z fw01.lab.local firewalld - - - DROP IN=eth0 SRC=10.0.0.5 DST=192.168.1.1 PROTO=TCP DPT=22
  │   │          │                │          │             └── Message body
  │   │          │                │          └── Structured data (optional)
  │   │          │                └── Application name
  │   │          └── Hostname
  │   └── Syslog version
  └── Priority 134 = Facility 16 (local0) × 8 + Severity 6 (info)
```

### Configuring Syslog

**On a Cisco device:**
```
! Send logs to syslog server
logging host 10.0.0.50

! Set the severity level to capture (and everything more severe)
logging trap informational

! Use a specific facility for identification
logging facility local6

! Add timestamps to messages
service timestamps log datetime msec localtime show-timezone

! Set source interface for syslog packets
logging source-interface Loopback0
```

**On a Linux server (rsyslog):**
```bash
# /etc/rsyslog.conf — accept remote syslog via UDP
module(load="imudp")
input(type="imudp" port="514")

# Accept remote syslog via TCP (more reliable)
module(load="imtcp")
input(type="imtcp" port="514")

# Sort incoming logs by hostname into separate files
template(name="RemoteLogs" type="string"
  string="/var/log/remote/%HOSTNAME%/%PROGRAMNAME%.log")

*.* ?RemoteLogs
```

**On a Linux server (syslog-ng):**
```
source s_network {
    udp(port(514));
    tcp(port(514));
};

destination d_remote {
    file("/var/log/remote/${HOST}/${PROGRAM}.log");
};

log {
    source(s_network);
    destination(d_remote);
};
```

### Syslog Transport Protocols

| Transport | Port | Reliability | Security | Use Case                      |
|-----------|------|-------------|----------|-------------------------------|
| UDP       | 514  | Unreliable  | None     | Traditional, most common      |
| TCP       | 514  | Reliable    | None     | When you can't afford lost logs|
| TLS       | 6514 | Reliable    | Encrypted| Compliance, sensitive environments |

> [!WARNING] UDP syslog can lose messages
> Traditional syslog over UDP is fire-and-forget — messages can be lost due to network congestion, buffer overflows, or packet drops. For production environments, use **TCP or TLS** transport to ensure log delivery. This matters for compliance and forensic analysis.

---

## SNMP + Syslog Together - A Complete Monitoring Strategy

In practice, you use both protocols together for comprehensive network monitoring:

| Aspect           | SNMP                                    | Syslog                               |
|------------------|-----------------------------------------|--------------------------------------|
| **Purpose**      | Metrics, status, configuration          | Event logs, audit trails             |
| **Model**        | Poll (request/response) + Traps        | Push (device sends logs)             |
| **Data Type**    | Structured (OID/value pairs)            | Unstructured text messages           |
| **Transport**    | UDP 161 (queries), UDP 162 (traps)      | UDP/TCP 514, TLS 6514               |
| **Best For**     | Bandwidth, CPU, uptime, interface stats | Login events, config changes, errors |
| **Alerting**     | Threshold-based (poll and compare)      | Pattern matching on log messages     |

**Example monitoring stack:**

```
Comprehensive Monitoring Architecture

┌─────────────────────────────────────────────────────────┐
│                    Grafana Dashboard                     │
│  [CPU Graph] [Bandwidth] [Uptime] [Error Log] [Alerts] │
└──────────┬──────────────────────────────┬───────────────┘
           │                              │
    ┌──────┴──────┐               ┌───────┴───────┐
    │ Prometheus / │               │  Graylog /    │
    │ LibreNMS /   │               │  ELK Stack /  │
    │ Zabbix       │               │  Loki         │
    │ (SNMP Polls) │               │ (Syslog Rx)   │
    └──────┬──────┘               └───────┬───────┘
           │                              │
     SNMP GET/WALK                  Syslog Messages
     (every 5 min)                (real-time stream)
           │                              │
    ┌──────┴──────────────────────────────┴──────┐
    │          Network Infrastructure             │
    │  Routers  Switches  Firewalls  Servers      │
    └─────────────────────────────────────────────┘
```

---

## 🛠️ Hands-on Practice

- [ ] Install `net-snmp` tools on a Linux system (`snmpget`, `snmpwalk`, `snmptrap`)
- [ ] Query a device or virtual router using SNMPv2c and examine the output
- [ ] Configure SNMPv3 with `authPriv` on a lab device and verify encrypted communication with Wireshark
- [ ] Set up `rsyslog` to receive remote syslog messages and organize them by hostname
- [ ] Configure a network device to send both SNMP traps and syslog messages to your monitoring server
- [ ] Deploy a monitoring tool (LibreNMS, Zabbix, or Prometheus with SNMP exporter) and add devices
- [ ] Create a Grafana dashboard showing interface bandwidth from SNMP data alongside syslog events

> [!TIP] Lab Environment
> Use **GNS3** or **EVE-NG** with virtual Cisco routers to practice SNMP and syslog configuration without needing physical hardware. Pair it with a Linux VM running rsyslog and a monitoring tool for a complete lab.

## 📚 Essential Resources

- [RFC 3411-3418](https://www.rfc-editor.org/rfc/rfc3411) — SNMPv3 framework specifications
- [RFC 5424](https://www.rfc-editor.org/rfc/rfc5424) — The Syslog Protocol
- [Net-SNMP Documentation](http://www.net-snmp.org/docs/) — Tools and library reference
- [OID Repository](http://www.oid-info.com/) — Browse and search the global OID tree
- [Cisco SNMP Configuration Guide](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/snmp/configuration/xe-16/snmp-xe-16-book.html) — Vendor-specific setup

## 🤝 Community Support

> [!TIP] Need guidance?
> Join the [TWN Commons on Discord](https://discord.gg/kgaMm6WJya) to ask questions and connect with other learners.

**Relevant channels:**
- **#networking** — SNMP and syslog configuration questions
- **#sre** — Monitoring architecture and tool selection
- **#lab-help** — Troubleshooting your monitoring lab setup

## 🌉 Bridge to TWN

> [!NOTE] Bridge to TWN
> Self-hosted monitoring is a cornerstone of digital sovereignty. By running your own SNMP polling and syslog collection, you keep full visibility into your infrastructure without sending telemetry data to third-party cloud services. Explore sovereign monitoring solutions and hosting providers at [TWN Systems](https://twn.systems).

---

**Related topics:** [[Common Network Protocols and their Uses]] | [[Common Ports and their Uses]] | [[Network Troubleshooting Tools]]

*Last updated: March 2026*
