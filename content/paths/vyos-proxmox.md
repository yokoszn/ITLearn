---
title: VyOS and Proxmox Network Infrastructure
tags:
  - vyos
  - proxmox
  - networking
  - dns
  - virtualization
  - learning-path
---

# VyOS and Proxmox Network Infrastructure Learning Path

Master the deployment and management of production-grade network infrastructure using VyOS as a software router/firewall and Proxmox VE as a virtualization platform. This path takes you from basic VyOS configuration through advanced multi-cluster DNS architectures with PowerDNS, Unbound, and split-horizon DNS.

## 📋 Overview

**Duration:** 12-16 weeks (self-paced)
**Level:** Intermediate to Advanced
**Prerequisites:** Solid networking fundamentals, basic Linux administration, familiarity with virtualization concepts

**Why this matters:** Running VyOS on Proxmox gives you a fully open-source, sovereign network stack. You control your routing, firewalling, VPNs, and DNS — no vendor lock-in, no licensing fees, no phoning home. Combined with Proxmox SDN and PowerDNS, you can build infrastructure that rivals enterprise solutions while maintaining complete ownership.

```
🏗️ Architecture You'll Build

                    ┌─────────────────────────────────────┐
                    │     Root PowerDNS Supermaster        │
                    │   (Zone Authority & Sync Source)     │
                    └──────────┬──────────┬───────────────┘
                               │          │
                 ┌─────────────┘          └──────────────┐
                 ▼                                       ▼
    ┌────────────────────────┐          ┌────────────────────────┐
    │   Proxmox Cluster A    │          │   Proxmox Cluster B    │
    │  ┌──────────────────┐  │          │  ┌──────────────────┐  │
    │  │  VyOS Router VM  │  │          │  │  VyOS Router VM  │  │
    │  │  ├─ OSPF/BGP     │  │          │  │  ├─ OSPF/BGP     │  │
    │  │  ├─ Firewall     │  │          │  │  ├─ Firewall     │  │
    │  │  ├─ VPN (WG/IPsec│  │          │  │  ├─ VPN (WG/IPsec│  │
    │  │  └─ NAT/DHCP     │  │          │  │  └─ NAT/DHCP     │  │
    │  └──────────────────┘  │          │  └──────────────────┘  │
    │  ┌──────────────────┐  │          │  ┌──────────────────┐  │
    │  │ PowerDNS (slave) │  │          │  │ PowerDNS (slave) │  │
    │  │ Unbound Resolver │  │          │  │ Unbound Resolver │  │
    │  │ Split-Horizon DNS│  │          │  │ Split-Horizon DNS│  │
    │  └──────────────────┘  │          │  └──────────────────┘  │
    │  ┌──────────────────┐  │          │  ┌──────────────────┐  │
    │  │   Proxmox SDN    │  │          │  │   Proxmox SDN    │  │
    │  │  VLANs / VXLANs  │  │          │  │  VLANs / VXLANs  │  │
    │  │  EVPN Fabric     │  │          │  │  EVPN Fabric     │  │
    │  └──────────────────┘  │          │  └──────────────────┘  │
    └────────────────────────┘          └────────────────────────┘
```

## ✅ Prerequisites

Before starting this path, you should:
- [ ] Complete or be comfortable with [[paths/networking|Networking Fundamentals]] (especially routing, VLANs, subnetting)
- [ ] Have working knowledge of Linux command line and system administration
- [ ] Understand virtualization concepts ([[03 Information Technology/Virtualization/Hypervisors|Hypervisors]], VMs, virtual networking)
- [ ] Have access to at least one Proxmox VE host (bare metal recommended, nested virtualization possible)
- [ ] **Recommended:** Familiarity with DNS concepts (A/AAAA/CNAME/NS records, zones, resolution flow)
- [ ] **Recommended:** Basic understanding of firewall rules and NAT

## 🎯 Learning Milestones

### 🏗️ Milestone 1: VyOS Fundamentals on Proxmox (Weeks 1-3)
**Goal:** Deploy VyOS as a virtual router on Proxmox and master its configuration model

**Core Concepts:**
- VyOS architecture: Debian-based, configuration tree model, commit/save workflow
- VyOS image types: rolling vs. LTS (Circinus, Sagitta), building from source
- Deploying VyOS as a Proxmox VM: CPU, memory, disk, and NIC sizing
- VyOS interface types: ethernet, bonding, bridge, VLAN sub-interfaces, WireGuard, tunnel
- The VyOS configuration system: `configure`, `set`, `delete`, `commit`, `save`, `compare`, `rollback`

```
📦 VyOS on Proxmox VM Setup

  Proxmox Host
  ├─ vmbr0 (Management Bridge) ──── Physical NIC (em0)
  ├─ vmbr1 (WAN Bridge) ─────────── Physical NIC (em1)
  └─ vmbr2 (Internal Bridge) ────── Physical NIC (em2) [or VLAN trunk]
       │
       └─── VyOS VM
            ├─ eth0 → vmbr0 (management)
            ├─ eth1 → vmbr1 (WAN / upstream)
            └─ eth2 → vmbr2 (LAN / internal networks)
```

**🛠️ Hands-on Practice:**
- [ ] Download or build a VyOS ISO and create a Proxmox VM with multiple NICs
- [ ] Install VyOS from ISO, configure initial interfaces, set hostname and credentials
- [ ] Configure basic routing: static routes, default gateway, source NAT (masquerade)
- [ ] Set up DHCP server and DNS forwarding on VyOS for a LAN segment
- [ ] Practice the commit/rollback workflow — intentionally break and recover configuration
- [ ] Enable SSH and configure key-based authentication on VyOS
- [ ] Set up VyOS firewall zones and basic rulesets (WAN, LAN, DMZ)

**Key Configuration Examples:**
```bash
# Basic VyOS interface and NAT setup
configure
set interfaces ethernet eth0 address '10.0.0.1/24'
set interfaces ethernet eth1 address 'dhcp'
set nat source rule 100 outbound-interface name 'eth1'
set nat source rule 100 source address '10.0.0.0/24'
set nat source rule 100 translation address 'masquerade'
set service dhcp-server shared-network-name LAN subnet 10.0.0.0/24 range 0 start '10.0.0.100'
set service dhcp-server shared-network-name LAN subnet 10.0.0.0/24 range 0 stop '10.0.0.200'
set service dhcp-server shared-network-name LAN subnet 10.0.0.0/24 default-router '10.0.0.1'
set service dhcp-server shared-network-name LAN subnet 10.0.0.0/24 name-server '10.0.0.1'
set service dns forwarding listen-address '10.0.0.1'
set service dns forwarding allow-from '10.0.0.0/24'
commit
save
```

**Checkpoint:** Can you deploy a VyOS VM that provides routing, NAT, DHCP, and DNS forwarding for a Proxmox internal network?

> [!TIP] Need guidance?
> Join [TWN Commons #networking](https://discord.gg/kgaMm6WJya) to ask questions and discuss VyOS deployments with other learners.

**💬 Share Your Progress:** Post your VyOS interface diagram and firewall zone layout in Discord!

---

### 🌐 Milestone 2: Proxmox SDN and VyOS Integration (Weeks 4-6)
**Goal:** Use Proxmox SDN to build software-defined network fabrics and integrate VyOS as the routing gateway

**Core Concepts:**
- Proxmox SDN architecture: zones, VNets, subnets, controllers
- SDN zone types: Simple, VLAN, QinQ, VXLAN, EVPN
- How Proxmox SDN interacts with Linux bridges and Open vSwitch (OVS)
- VXLAN overlays: why they exist, how they encapsulate L2 over L3
- EVPN fabric: BGP-based control plane for VXLAN, automatic MAC/IP learning
- VyOS as the SDN gateway: routing between VNets and external networks
- VLAN trunking from Proxmox bridges into VyOS sub-interfaces

```
🌐 Proxmox SDN with VyOS Gateway

  Proxmox SDN Controller (EVPN)
  │
  ├── Zone: "production" (EVPN/VXLAN)
  │   ├── VNet: vnet-web    (10.10.1.0/24, VLAN 101)
  │   ├── VNet: vnet-app    (10.10.2.0/24, VLAN 102)
  │   └── VNet: vnet-db     (10.10.3.0/24, VLAN 103)
  │
  ├── Zone: "management" (VLAN)
  │   └── VNet: vnet-mgmt   (10.0.0.0/24, VLAN 1)
  │
  └── VyOS Router VM
      ├── eth0          → vnet-mgmt (management)
      ├── eth1          → WAN (upstream)
      ├── eth2.101      → vnet-web  (VLAN sub-interface)
      ├── eth2.102      → vnet-app  (VLAN sub-interface)
      └── eth2.103      → vnet-db   (VLAN sub-interface)

  VyOS provides:
  - Inter-VLAN routing between web/app/db tiers
  - Firewall rules between zones
  - NAT to WAN for outbound traffic
  - VPN endpoints for remote access
```

**🛠️ Hands-on Practice:**
- [ ] Enable Proxmox SDN in the datacenter configuration
- [ ] Create a VLAN zone with multiple VNets and subnets
- [ ] Attach VMs to different VNets and verify L2 isolation
- [ ] Configure VyOS with VLAN sub-interfaces to route between VNets
- [ ] Set up firewall rules on VyOS to control inter-VLAN traffic (e.g., web can reach app, but not db directly)
- [ ] Deploy a VXLAN zone across multiple Proxmox nodes and verify overlay connectivity
- [ ] Set up an EVPN zone with a BGP controller and verify automatic MAC learning
- [ ] Configure VyOS as the default gateway for SDN subnets

**Key VyOS VLAN Configuration:**
```bash
# VLAN sub-interfaces on VyOS for Proxmox SDN VNets
configure
set interfaces ethernet eth2 vif 101 address '10.10.1.1/24'
set interfaces ethernet eth2 vif 101 description 'web-tier'
set interfaces ethernet eth2 vif 102 address '10.10.2.1/24'
set interfaces ethernet eth2 vif 102 description 'app-tier'
set interfaces ethernet eth2 vif 103 address '10.10.3.1/24'
set interfaces ethernet eth2 vif 103 description 'db-tier'

# Firewall zone policy
set firewall group network-group WEB network '10.10.1.0/24'
set firewall group network-group APP network '10.10.2.0/24'
set firewall group network-group DB network '10.10.3.0/24'

set firewall ipv4 forward filter rule 10 action 'accept'
set firewall ipv4 forward filter rule 10 source group network-group 'WEB'
set firewall ipv4 forward filter rule 10 destination group network-group 'APP'

set firewall ipv4 forward filter rule 20 action 'accept'
set firewall ipv4 forward filter rule 20 source group network-group 'APP'
set firewall ipv4 forward filter rule 20 destination group network-group 'DB'

set firewall ipv4 forward filter rule 99 action 'drop'
set firewall ipv4 forward filter rule 99 description 'drop all other inter-zone'
commit
save
```

**Checkpoint:** Can you build a multi-tier application network using Proxmox SDN VNets with VyOS providing inter-VLAN routing and zone-based firewalling?

**💬 Share Your Progress:** Post your SDN topology diagram and VyOS firewall rules in [TWN Commons #networking](https://discord.gg/kgaMm6WJya)!

---

### 🔒 Milestone 3: VyOS VPN and Dynamic Routing (Weeks 7-8)
**Goal:** Connect Proxmox sites with VPN tunnels and dynamic routing protocols

**Core Concepts:**
- WireGuard on VyOS: lightweight, modern, kernel-level VPN
- IPsec on VyOS: site-to-site IKEv2 tunnels for legacy and standards compliance
- OSPF on VyOS: link-state routing for internal networks, areas, cost tuning
- BGP on VyOS: peering with upstream providers, route filtering, communities
- Combining VPN + dynamic routing: running OSPF/BGP over WireGuard tunnels
- Policy-based routing and traffic engineering on VyOS

```
🔒 Multi-Site VPN with Dynamic Routing

  Site A (Proxmox Cluster)              Site B (Proxmox Cluster)
  ┌─────────────────────┐              ┌─────────────────────┐
  │  VyOS-A              │              │  VyOS-B              │
  │  ├─ WAN: 203.0.113.1│◄── WireGuard ──►│  ├─ WAN: 198.51.100.1│
  │  ├─ wg0: 10.255.0.1 │    Tunnel     │  ├─ wg0: 10.255.0.2 │
  │  ├─ LAN: 10.10.0.0/16              │  ├─ LAN: 10.20.0.0/16
  │  └─ OSPF Area 0     │◄── OSPF ────►│  └─ OSPF Area 0     │
  └─────────────────────┘   over wg0    └─────────────────────┘

  Result: Full mesh routing between sites, automatic failover,
          encrypted transport, dynamic route learning
```

**🛠️ Hands-on Practice:**
- [ ] Configure a WireGuard tunnel between two VyOS instances
- [ ] Run OSPF over the WireGuard tunnel to exchange routes dynamically
- [ ] Set up an IPsec IKEv2 tunnel as an alternative/backup path
- [ ] Configure BGP peering between VyOS routers with route filtering
- [ ] Implement redundant WAN with failover using VyOS connection tracking
- [ ] Test failover scenarios: bring down primary links and verify convergence
- [ ] Configure policy-based routing to steer specific traffic over specific tunnels

**Key WireGuard + OSPF Configuration:**
```bash
# VyOS-A: WireGuard tunnel
configure
set interfaces wireguard wg0 address '10.255.0.1/30'
set interfaces wireguard wg0 private-key '<GENERATED_PRIVATE_KEY>'
set interfaces wireguard wg0 peer site-b allowed-ips '0.0.0.0/0'
set interfaces wireguard wg0 peer site-b address '198.51.100.1'
set interfaces wireguard wg0 peer site-b port '51820'
set interfaces wireguard wg0 peer site-b public-key '<SITE_B_PUBLIC_KEY>'
set interfaces wireguard wg0 port '51820'

# OSPF over WireGuard
set protocols ospf area 0 network '10.10.0.0/16'
set protocols ospf area 0 network '10.255.0.0/30'
set protocols ospf parameters router-id '10.255.0.1'
set protocols ospf passive-interface 'eth0'
set protocols ospf passive-interface 'eth2'
commit
save
```

**Checkpoint:** Can you establish an encrypted multi-site network where routes propagate automatically and traffic fails over when links go down?

> [!TIP] Testing failover?
> Use `monitor protocol ospf` and `show ip route` on VyOS to watch route convergence in real time. Pull cables (or disconnect VM NICs) to simulate failures.

**💬 Share Your Lab:** Post your multi-site topology and OSPF neighbor output in [TWN Commons #lab-help](https://discord.gg/kgaMm6WJya)!

---

### 🔍 Milestone 4: Unbound DNS and Split-Horizon DNS (Weeks 9-10)
**Goal:** Deploy Unbound as a recursive resolver with split-horizon views for internal vs. external DNS resolution

**Core Concepts:**
- Unbound as a validating, recursive, caching DNS resolver
- Why Unbound over forwarding to public resolvers (privacy, control, DNSSEC validation)
- Split-horizon DNS: returning different answers based on the client's source network
- Use cases: internal services resolve to private IPs, external clients get public IPs
- Unbound `access-control`, `local-zone`, `local-data`, and `views` for split-horizon
- VyOS DNS forwarding integration: pointing VyOS DHCP clients at your Unbound resolver
- DNSSEC validation in Unbound and troubleshooting

```
🔍 Split-Horizon DNS Architecture

  External Client                  Internal Client (10.10.0.0/16)
       │                                    │
       ▼                                    ▼
  ┌──────────┐                     ┌──────────────────┐
  │ Public   │                     │ Unbound Resolver │
  │ DNS      │                     │ (on Proxmox VM)  │
  │ (normal) │                     │                  │
  └──────────┘                     │ Query: app.example.com
                                   │                  │
                                   │ View: "internal" │
                                   │ → 10.10.2.50     │
                                   │                  │
                                   │ View: "external" │
                                   │ → 203.0.113.50   │
                                   └──────────────────┘
                                          │
                        ┌─────────────────┴────────────────┐
                        ▼                                  ▼
                Internal answer:                   External/fallback:
                10.10.2.50 (private)              Recurse to root servers
                                                  or forward to PowerDNS
```

**🛠️ Hands-on Practice:**
- [ ] Deploy Unbound on a Proxmox VM (or LXC container)
- [ ] Configure Unbound as a full recursive resolver (no forwarding, resolves from root)
- [ ] Enable DNSSEC validation and test with `dig +dnssec`
- [ ] Configure Unbound `local-zone` and `local-data` for internal domain resolution
- [ ] Set up split-horizon views: internal clients get private IPs, external get public
- [ ] Integrate with VyOS: configure VyOS DHCP to hand out Unbound's IP as the DNS server
- [ ] Configure VyOS `dns forwarding` to use Unbound as the upstream resolver
- [ ] Test resolution from different source networks and verify correct view selection
- [ ] Set up Unbound logging and monitoring for DNS query analytics

**Key Unbound Split-Horizon Configuration:**
```yaml
# /etc/unbound/unbound.conf

server:
    interface: 0.0.0.0
    access-control: 10.10.0.0/16 allow
    access-control: 10.20.0.0/16 allow
    access-control: 127.0.0.0/8 allow
    access-control: 0.0.0.0/0 refuse

    # DNSSEC
    auto-trust-anchor-file: "/var/lib/unbound/root.key"
    val-clean-additional: yes

    # Performance
    num-threads: 4
    msg-cache-size: 50m
    rrset-cache-size: 100m
    cache-min-ttl: 300
    prefetch: yes

    # Internal zone overrides (split-horizon)
    local-zone: "infra.example.com." static
    local-data: "app.infra.example.com. IN A 10.10.2.50"
    local-data: "db.infra.example.com.  IN A 10.10.3.10"
    local-data: "mon.infra.example.com. IN A 10.10.1.20"

    # PTR records for reverse lookups
    local-data-ptr: "10.10.2.50 app.infra.example.com."
    local-data-ptr: "10.10.3.10 db.infra.example.com."
    local-data-ptr: "10.10.1.20 mon.infra.example.com."

# Forward specific zones to PowerDNS authoritative server
forward-zone:
    name: "example.com"
    forward-addr: 10.10.1.53    # PowerDNS authoritative

# Forward reverse zones
forward-zone:
    name: "10.in-addr.arpa."
    forward-addr: 10.10.1.53
```

**VyOS DNS Forwarding Integration:**
```bash
# Point VyOS DNS forwarding to Unbound
configure
set service dns forwarding listen-address '10.10.1.1'
set service dns forwarding listen-address '10.10.2.1'
set service dns forwarding listen-address '10.10.3.1'
set service dns forwarding allow-from '10.10.0.0/16'
set service dns forwarding name-server '10.10.1.53'
set service dns forwarding name-server '10.10.1.54'

# Or use Unbound directly
set service dhcp-server shared-network-name LAN subnet 10.10.1.0/24 name-server '10.10.1.53'
commit
save
```

**Checkpoint:** Can you set up an Unbound resolver that returns different DNS answers based on whether the query comes from an internal or external network?

**💬 Share Your Setup:** Post your split-horizon DNS test results (`dig` outputs from different source IPs) in [TWN Commons #networking](https://discord.gg/kgaMm6WJya)!

---

### 🗄️ Milestone 5: PowerDNS Authoritative Server and Supermaster (Weeks 11-13)
**Goal:** Deploy PowerDNS as your authoritative DNS server with supermaster/superslave replication for automatic zone synchronization across clusters

**Core Concepts:**
- PowerDNS Authoritative Server vs. PowerDNS Recursor vs. dnsdist (the PowerDNS ecosystem)
- PowerDNS backends: MySQL/MariaDB, PostgreSQL, SQLite, LMDB, BIND-format files
- Zone management: primary (master) zones, secondary (slave) zones, AXFR/IXFR transfers
- Supermaster: automatic provisioning of slave zones — when a master NOTIFYs a slave that doesn't know about a zone, the slave automatically creates it
- Why supermasters matter: add a zone once on the master, all slaves pick it up automatically
- DNS NOTIFY mechanism and how it triggers zone transfers
- PowerDNS API for programmatic zone and record management
- Combining PowerDNS (authoritative) with Unbound (recursive) — the recommended architecture

```
🗄️ PowerDNS Supermaster Architecture

                 ┌──────────────────────────────┐
                 │   Root Supermaster (pdns-root)│
                 │   IP: 10.0.0.53              │
                 │   Backend: PostgreSQL         │
                 │   Role: Primary / Supermaster │
                 │   Zones: *.example.com        │
                 │          *.infra.local         │
                 │          reverse zones         │
                 └──────────┬───────┬────────────┘
                    NOTIFY  │       │  NOTIFY
                    + AXFR  │       │  + AXFR
                 ┌──────────┘       └──────────┐
                 ▼                              ▼
   ┌─────────────────────────┐   ┌─────────────────────────┐
   │ Cluster A Slave (pdns-a)│   │ Cluster B Slave (pdns-b)│
   │ IP: 10.10.1.53         │   │ IP: 10.20.1.53         │
   │ Backend: PostgreSQL     │   │ Backend: PostgreSQL     │
   │ Role: Superslave        │   │ Role: Superslave        │
   │ Auto-creates zones from │   │ Auto-creates zones from │
   │ supermaster NOTIFYs     │   │ supermaster NOTIFYs     │
   └─────────────────────────┘   └─────────────────────────┘

   Flow:
   1. Admin creates zone on pdns-root
   2. pdns-root sends NOTIFY to slaves
   3. Slaves check supermasters table → pdns-root is listed
   4. Slaves auto-create the zone and AXFR all records
   5. Future changes: pdns-root increments SOA serial → NOTIFY → IXFR
```

**🛠️ Hands-on Practice:**
- [ ] Deploy PowerDNS Authoritative Server on a Proxmox VM with a PostgreSQL backend
- [ ] Create zones and records using `pdnsutil` and the PowerDNS REST API
- [ ] Set up a second PowerDNS instance as a slave and configure zone transfers (AXFR)
- [ ] Configure the supermaster relationship: add the master to the slave's `supermasters` table
- [ ] Test automatic zone provisioning: create a new zone on master, verify it appears on slave
- [ ] Set up DNSSEC signing on PowerDNS with `pdnsutil secure-zone`
- [ ] Configure the PowerDNS API and manage records programmatically (curl / scripts)
- [ ] Integrate Unbound to forward authoritative queries to your PowerDNS servers

**Key PowerDNS Supermaster Configuration:**

Master (pdns-root) — `pdns.conf`:
```ini
# /etc/powerdns/pdns.conf on supermaster
launch=gpgsql
gpgsql-host=127.0.0.1
gpgsql-dbname=pdns
gpgsql-user=pdns
gpgsql-password=<secure_password>

# Enable master mode and the API
master=yes
api=yes
api-key=<secure_api_key>
webserver=yes
webserver-address=0.0.0.0
webserver-port=8081
webserver-allow-from=10.0.0.0/8

# NOTIFY slaves on zone changes
also-notify=10.10.1.53,10.20.1.53
allow-axfr-ips=10.10.1.53/32,10.20.1.53/32

# SOA defaults
default-soa-content=ns1.example.com hostmaster.example.com 0 10800 3600 604800 3600
```

Slave (pdns-a) — `pdns.conf`:
```ini
# /etc/powerdns/pdns.conf on superslave
launch=gpgsql
gpgsql-host=127.0.0.1
gpgsql-dbname=pdns
gpgsql-user=pdns
gpgsql-password=<secure_password>

# Enable slave and superslave mode
slave=yes
superslave=yes
autosecondary=yes

# Allow NOTIFY from master
allow-notify-from=10.0.0.53/32
```

Superslave database setup:
```sql
-- On each slave, register the supermaster
INSERT INTO supermasters (ip, nameserver, account)
VALUES ('10.0.0.53', 'ns1.example.com', 'root-master');
```

Zone creation on master:
```bash
# Create a new zone on the supermaster
pdnsutil create-zone infra.example.com ns1.example.com

# Add records
pdnsutil add-record infra.example.com app A 10.10.2.50
pdnsutil add-record infra.example.com db  A 10.10.3.10
pdnsutil add-record infra.example.com mon A 10.10.1.20

# Increase SOA serial and notify slaves
pdnsutil increase-serial infra.example.com
pdns_control notify infra.example.com

# Verify on slave
dig @10.10.1.53 app.infra.example.com A
```

**Checkpoint:** Can you create a new zone on your supermaster and have it automatically appear on all slave servers without manual intervention?

> [!WARNING] SOA Serial Discipline
> Always increment the SOA serial when making changes. PowerDNS can auto-increment for API changes, but manual `pdnsutil` edits need explicit `increase-serial` calls. Slaves only transfer when they see a higher serial number.

**💬 Share Your Architecture:** Post your PowerDNS supermaster/slave topology and test results in [TWN Commons #networking](https://discord.gg/kgaMm6WJya)!

---

### 🏢 Milestone 6: Cluster-Specific PowerDNS with Root Supermaster Sync (Weeks 14-16)
**Goal:** Build a production architecture where each Proxmox cluster runs its own PowerDNS instance, all synchronized from a root supermaster, with Unbound providing recursive resolution and split-horizon views

**Core Concepts:**
- Multi-cluster DNS architecture: why each cluster needs local DNS authority
- Root supermaster as single source of truth for zone data
- Cluster-local PowerDNS slaves for low-latency, resilient name resolution
- Combining PowerDNS + Unbound per cluster: authoritative + recursive separation
- Split-horizon at the Unbound layer: internal views for cluster-local services
- DNS failover and high availability: what happens when the supermaster is down
- Automating DNS record management: Proxmox hooks, Ansible, Terraform integration
- VyOS as the DNS gateway: DHCP → Unbound → PowerDNS resolution chain

```
🏢 Full Production DNS Architecture

                         ┌─────────────────────┐
                         │   Root Supermaster   │
                         │   pdns-root          │
                         │   (PostgreSQL)       │
                         │                     │
                         │ Zones:              │
                         │  example.com        │
                         │  infra.example.com  │
                         │  10.in-addr.arpa    │
                         │  20.in-addr.arpa    │
                         └──────┬────┬─────────┘
                     NOTIFY/AXFR│    │NOTIFY/AXFR
                 ┌──────────────┘    └──────────────┐
                 ▼                                  ▼
  ┌──────────────────────────┐    ┌──────────────────────────┐
  │   Cluster A              │    │   Cluster B              │
  │                          │    │                          │
  │ ┌──────────────────────┐ │    │ ┌──────────────────────┐ │
  │ │ PowerDNS Slave       │ │    │ │ PowerDNS Slave       │ │
  │ │ (auth for all zones) │ │    │ │ (auth for all zones) │ │
  │ └──────────┬───────────┘ │    │ └──────────┬───────────┘ │
  │            │ forward      │    │            │ forward      │
  │ ┌──────────▼───────────┐ │    │ ┌──────────▼───────────┐ │
  │ │ Unbound Resolver     │ │    │ │ Unbound Resolver     │ │
  │ │ - recurse external   │ │    │ │ - recurse external   │ │
  │ │ - forward internal → │ │    │ │ - forward internal → │ │
  │ │   PowerDNS slave     │ │    │ │   PowerDNS slave     │ │
  │ │ - split-horizon views│ │    │ │ - split-horizon views│ │
  │ └──────────┬───────────┘ │    │ └──────────┬───────────┘ │
  │            │              │    │            │              │
  │ ┌──────────▼───────────┐ │    │ ┌──────────▼───────────┐ │
  │ │ VyOS Router          │ │    │ │ VyOS Router          │ │
  │ │ DHCP → clients get   │ │    │ │ DHCP → clients get   │ │
  │ │ Unbound as DNS       │ │    │ │ Unbound as DNS       │ │
  │ └──────────────────────┘ │    │ └──────────────────────┘ │
  │                          │    │                          │
  │ VMs query:               │    │ VMs query:               │
  │  VyOS → Unbound          │    │  VyOS → Unbound          │
  │  Unbound → PowerDNS      │    │  Unbound → PowerDNS      │
  │  (internal zones)        │    │  (internal zones)        │
  │  Unbound → root servers  │    │  Unbound → root servers  │
  │  (external zones)        │    │  (external zones)        │
  └──────────────────────────┘    └──────────────────────────┘
```

**🛠️ Hands-on Practice:**
- [ ] Deploy the full stack: root supermaster + per-cluster PowerDNS slaves + per-cluster Unbound resolvers
- [ ] Configure Unbound to forward internal zones to the local PowerDNS slave
- [ ] Set up VyOS DHCP to hand out the local Unbound resolver to all VMs
- [ ] Create a new zone on the root supermaster and verify it propagates to all clusters
- [ ] Test split-horizon: internal VMs resolve `app.infra.example.com` to private IPs; external resolvers see public IPs or NXDOMAIN
- [ ] Simulate supermaster failure: verify slaves continue serving cached zones
- [ ] Simulate cluster PowerDNS failure: verify Unbound falls back or returns cached answers
- [ ] Set up monitoring: track zone transfer status, query latency, DNSSEC validation
- [ ] Automate record creation when new VMs are provisioned in Proxmox (using hooks or the PowerDNS API)
- [ ] Configure zone-specific DNSSEC policies and key rotation schedules

**Automation Example — Proxmox VM Hook for DNS Registration:**
```bash
#!/bin/bash
# /var/lib/vz/snippets/dns-register.sh
# Called as a Proxmox hookscript on VM start

PHASE=$1    # pre-start, post-start, pre-stop, post-stop
VMID=$2

if [ "$PHASE" == "post-start" ]; then
    VM_NAME=$(qm config "$VMID" | grep '^name:' | awk '{print $2}')
    VM_IP=$(qm guest cmd "$VMID" network-get-interfaces | \
            jq -r '.[] | select(.name != "lo") | .["ip-addresses"][] | select(.["ip-address-type"] == "ipv4") | .["ip-address"]' | head -1)

    if [ -n "$VM_NAME" ] && [ -n "$VM_IP" ]; then
        PDNS_API="http://10.0.0.53:8081"
        PDNS_KEY="your-api-key"
        ZONE="infra.example.com."

        curl -s -X PATCH "${PDNS_API}/api/v1/servers/localhost/zones/${ZONE}" \
            -H "X-API-Key: ${PDNS_KEY}" \
            -H "Content-Type: application/json" \
            -d "{\"rrsets\": [{\"name\": \"${VM_NAME}.${ZONE}\", \"type\": \"A\", \"ttl\": 300, \"changetype\": \"REPLACE\", \"records\": [{\"content\": \"${VM_IP}\", \"disabled\": false}]}]}"

        echo "Registered ${VM_NAME}.infra.example.com → ${VM_IP}"
    fi
fi
```

**Full Unbound + PowerDNS Integration:**
```yaml
# /etc/unbound/unbound.conf (per-cluster resolver)

server:
    interface: 0.0.0.0
    port: 53
    access-control: 10.0.0.0/8 allow
    access-control: 127.0.0.0/8 allow
    access-control: 0.0.0.0/0 refuse

    # Performance tuning
    num-threads: 4
    msg-cache-size: 64m
    rrset-cache-size: 128m
    prefetch: yes
    prefetch-key: yes

    # DNSSEC
    auto-trust-anchor-file: "/var/lib/unbound/root.key"

    # Split-horizon: override specific names for internal use
    # These take priority over forwarded zones
    local-zone: "cluster-a.infra.example.com." transparent
    local-data: "gateway.cluster-a.infra.example.com. IN A 10.10.1.1"
    local-data: "dns.cluster-a.infra.example.com.     IN A 10.10.1.53"
    local-data: "pve1.cluster-a.infra.example.com.    IN A 10.10.1.10"
    local-data: "pve2.cluster-a.infra.example.com.    IN A 10.10.1.11"
    local-data: "pve3.cluster-a.infra.example.com.    IN A 10.10.1.12"

# Forward authoritative internal zones to local PowerDNS slave
forward-zone:
    name: "example.com."
    forward-addr: 10.10.1.53

forward-zone:
    name: "infra.example.com."
    forward-addr: 10.10.1.53

forward-zone:
    name: "10.in-addr.arpa."
    forward-addr: 10.10.1.53

forward-zone:
    name: "20.in-addr.arpa."
    forward-addr: 10.10.1.53

# Everything else: recurse from root (no forwarding to public DNS)
```

**Checkpoint:** Can you deploy the full multi-cluster DNS stack where a single zone change on the root supermaster propagates to all clusters, and VMs in each cluster resolve names through VyOS → Unbound → PowerDNS?

> [!WARNING] Production Considerations
> - Always run at least 2 PowerDNS slaves per cluster for HA
> - Monitor AXFR transfer status — a stuck transfer means stale records
> - Keep SOA refresh/retry timers reasonable (refresh: 3600, retry: 900)
> - Test DNSSEC key rollovers in staging before production
> - Back up PowerDNS databases — they hold all your zone data

**💬 Share Your Architecture:** Post your full multi-cluster DNS diagram in [TWN Commons #networking](https://discord.gg/kgaMm6WJya)!

---

## 📚 Essential Resources

### Documentation
- [VyOS Documentation](https://docs.vyos.io/) — Official VyOS configuration reference
- [Proxmox VE Admin Guide](https://pve.proxmox.com/pve-docs/) — Proxmox administration and SDN documentation
- [PowerDNS Authoritative Documentation](https://doc.powerdns.com/authoritative/) — PowerDNS server configuration
- [Unbound Documentation](https://unbound.docs.nlnetlabs.nl/) — Unbound resolver configuration
- [RFC 1996](https://www.rfc-editor.org/rfc/rfc1996) — DNS NOTIFY mechanism
- [RFC 5936](https://www.rfc-editor.org/rfc/rfc5936) — DNS Zone Transfer Protocol (AXFR)

### Tools and Software
- **VyOS** — Open-source network OS (rolling images free, LTS requires subscription or build from source)
- **Proxmox VE** — Open-source virtualization platform
- **PowerDNS** — Authoritative DNS server with database backends
- **Unbound** — Validating, recursive, caching DNS resolver
- **pdnsutil** — PowerDNS zone management CLI
- **dnsdist** — DNS load balancer (PowerDNS ecosystem)
- **dig / drill** — DNS query tools for testing and debugging
- **Ansible** — Automation for deploying and configuring all components

### Practice Labs
- **Home Lab Setup** — A single Proxmox host with 32GB+ RAM can run this entire architecture as nested VMs
- **Nested Virtualization** — Run Proxmox inside Proxmox for multi-cluster testing without extra hardware
- **VyOS Rolling Images** — Free nightly builds for lab use at [VyOS rolling releases](https://vyos.net/get/nightly-builds/)

## 🤝 Community and Support

**[Join TWN Commons](https://discord.gg/kgaMm6WJya)** for help with:
- **#networking** — VyOS configuration, routing, VPN, and firewall questions
- **#lab-help** — Proxmox setup, SDN configuration, and DNS deployment assistance
- **#infrastructure** — Production architecture design discussions
- **#study-groups** — Find lab partners to build multi-site topologies together

**🎯 Community Challenges:**
- **Weekly Lab Share** — Post your VyOS + Proxmox topology diagrams every Friday
- **DNS Architecture Review** — Monthly challenge to design DNS for specific scenarios
- **Break and Fix** — Intentionally misconfigure DNS/routing, share symptoms, and let others diagnose

**💬 Share Your Journey:**
- Post **network diagrams** and **VyOS configs** in #networking
- Share **PowerDNS automation scripts** and **Unbound configurations**
- Help others troubleshoot — debugging DNS is one of the best ways to learn
- Share your **production deployment stories** — successes and failures both teach

## 🌉 Bridge to TWN Systems

This learning path directly enables sovereign infrastructure:

> [!NOTE] Digital Infrastructure Independence
> Mastering VyOS + Proxmox + PowerDNS gives you:
> - **Complete network sovereignty** — your routing, firewalling, and DNS run on hardware you control
> - **No vendor DNS lock-in** — PowerDNS replaces managed DNS services with full control over your zones
> - **Privacy-preserving resolution** — Unbound resolves from root servers without leaking queries to third parties
> - **Multi-site resilience** — your infrastructure works even when cloud providers have outages

**🛠️ Apply Your Skills with TWN:**
- **Self-hosted DNS** — Run authoritative DNS for your domains without third-party nameservers
- **Sovereign routing** — VyOS replaces expensive commercial routers with full feature parity
- **Encrypted interconnects** — WireGuard tunnels between sites without trusting transit networks
- **Community-verified providers** — Deploy on [TWN-listed infrastructure](https://twn.systems) that respects your network choices

## 🚀 What's Next?

After completing this path, you'll be ready for:
- **[[paths/sre|Site Reliability Engineering]]** — Apply this infrastructure at scale with monitoring and automation
- **[[paths/linux|Linux Systems]]** — Deepen the OS skills that underpin VyOS, PowerDNS, and Unbound
- **Advanced BGP** — Internet routing, peering, and running your own ASN
- **Infrastructure as Code** — Terraform/OpenTofu + Ansible for full deployment automation
- **Container Networking** — Kubernetes CNI, service mesh, and DNS integration with CoreDNS

## 🏆 Certification Alignment

This learning path provides strong preparation for:
- **CompTIA Network+** — Networking fundamentals covered extensively in Milestones 1-3
- **Cisco CCNA** — Routing, switching, VPN, and ACL concepts map directly
- **Linux Foundation Certified System Administrator (LFCS)** — DNS and network service administration
- **Proxmox Certified Administrator** — If/when Proxmox formalizes certification

> [!TIP] Focus on Understanding, Not Certs
> The skills in this path — running your own routers, DNS infrastructure, and overlay networks — are deeply practical. Employers value engineers who can build and troubleshoot this stack far more than cert holders who memorized theory.

---

## 🔍 Path Quality Assurance

**✅ Community Validated:** Architecture patterns tested in production TWN community deployments.

**🧪 Lab Tested:** All configurations verified on VyOS rolling/1.4.x and Proxmox VE 8.x with PowerDNS 4.x and Unbound 1.x.

**📈 Actively Maintained:** Updated as VyOS, Proxmox SDN, and PowerDNS release new features.

**👥 Peer Reviewed:** Reviewed by infrastructure engineers running these stacks in production.

*Last updated: March 2026 | Version 1.0*

---

**Ready to start?** Begin with Milestone 1 and join the [TWN Commons networking channel](https://discord.gg/kgaMm6WJya) for support and community.
