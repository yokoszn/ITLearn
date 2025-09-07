Potential projects

Deploy LibreNMS or Zabbix in your homelab to collect interface and device metrics over time.

Python Forecasting Script: Pull SNMP data every hour, store in a CSV, then run a script to forecast when each link will cross 80% utilization.

Capacity Roadmap Presentation: Create a PowerPoint that maps projected growth to planned hardware refresh cycles for an IRIS client.



---

Capacity Analysis & Strategic Technical Planning
How it works

Metric Collection

Pull SNMP (interface counters, CPU/memory) and flow data (NetFlow/sFlow/IPFIX).

Track historical trends (daily/weekly/monthly).

Trend Analysis & Forecasting

Use statistical models (linear or seasonal) to project growth over 12–36 months.

Identify when links or devices will hit thresholds (e.g., 70–80% utilization).

Sizing & Headroom

Apply safety margins (30–50%) to account for traffic spikes or future services.

Map business projects (new datacentre build, IoT rollout) to capacity requirements.

Strategic Planning

Feed forecasts into budget cycles and roadmap sessions.

Work with solution architects to align new chassis/module purchases with projected needs.


---

Layer-2 Redundancy Protocols & Topologies
How it works

STP Family

RSTP (802.1w) for sub-second convergence.

MSTP (802.1s) to group VLANs into instances and optimize port roles.

Link Aggregation

LACP (802.3ad) active/passive negotiation.

PAGP on Cisco platforms.

Modern Fabric

EVPN-VXLAN multihoming (IRB) for active/active uplinks and loop prevention at scale.

Key Tradeoffs

STP blocks redundant links—slower convergence vs. loop risk.

LACP bundles links into a single logical port—higher throughput and faster failover.

Potential projects

MSTP Tuning Lab: Build a three-switch ring, configure MST regions to carry different VLAN groups, measure convergence time when you pull one link.

LACP with Proxmox: Connect your Proxmox management bridge to two physical uplinks in active/active LACP, test failover by unplugging one cable.

EVPN-VXLAN Mini-Fabric: Spin up two Cumulus Linux VMs in EVE-NG, configure BGP EVPN underlay, VXLAN overlay with multi-homed hosts.


North-South Routing
How it works

Definition: Traffic flowing between “inside” (LAN) and “outside” (WAN/Internet/DMZ).

Edge Devices: Routers/Firewalls perform NAT, ACL enforcement, VPN termination.

DMZ/Zoning: Place public-facing servers in a DMZ, route north-south via ACLs or zone-based firewalls.

High Availability: Use VRRP/HSRP/GLBP on routers; clustering on firewalls.

Performance: Ensure enough throughput and SSL/TLS decryption capacity.

Potential projects

pfSense Border Router: Deploy pfSense in your homelab as the edge, implement 1:1 NAT for a DMZ web VM, write ACLs to restrict inbound traffic.

VRRP Cluster: Configure two VyOS VMs with VRRP to share a virtual gateway IP, test failover by shutting down one VM.

BGP to the Cloud: Spin up an AWS VPC with a virtual router (e.g., FRR), establish an eBGP session with your on-prem VyOS lab, advertise private prefixes.



---



Building the HLD: Key Components
How it works

Logical Topologies: Abstract diagrams showing how sites, VLANs, and services connect (no physical racks).

Service Requirements: SLAs—latency, jitter, availability targets per application (VoIP needs <30 ms, <1 ms jitter, 99.99% uptime).

IP Addressing Plan: Hierarchical addressing (e.g., 10.1.X.0/24 per site), include VLAN→subnet mapping, summarization boundaries.

Chassis/Platform Selection: Match expected throughput, port density, redundancy features (dual supervisors, hot-swap fans).

Redundancy Model: Active/active vs. active/standby, link aggregation choices.

High-Level QoS Approach: Define traffic classes and DSCP markings, outline priority queuing without detailing per-device CLI.

Potential projects

HLD for Homelab Expansion: Document a plan to add a new VLAN (IoT-VLAN) with its own IP pool, map to a redundant leaf-spine design.

IP Plan Spreadsheet: Create an Excel or Google Sheets workbook listing VLAN IDs, subnets, DNS scopes, DHCP exclusions.

Vendor Eval Matrix: Compare two switch platforms on throughput, PoE budget, feature set, and price per port.

---

IP-Based Network Solutions Across Telecom Environments
Access Layer
How it works

GPON/DSL Aggregation: OLT terminates multiple ONTs; uses VLAN tagging to separate subscriber traffic.

Ethernet Access Rings: Deploy dual-homed switches in a ring with RSTP or short-path forwarding for resiliency.

Edge AAA: RADIUS/TACACS+ authenticates devices/users; enforces policy via dynamic VLAN assignment or downloadable ACLs.

Potential projects

FreeRADIUS Lab: Stand up a FreeRADIUS VM, configure a DSL modem (or Cisco router) to authenticate PPPoE sessions against it.

GPON Simulation: Use ONT/OLT simulators in GNS3 to practice service-specific VLAN assignments.

Ring Topology Test: Build a three-switch ring in your homelab, test RSTP vs. MSTP convergence.

Transport Layer
How it works

WDM/OTN/DWDM: Carries multiple wavelengths over a single fiber; provisioning uses an optical management system.

Carrier Ethernet / Pseudowire: MPLS PWE3 encapsulates Ethernet frames over an MPLS backbone, emulating point-to-point circuits.

MPLS-TE & SR-TE: RSVP-TE signals LSPs with explicit paths and resource reservations; SR-TE uses segment lists in BGP to steer traffic.

BGP/MPLS VPN (RFC 4364): Uses MP-BGP to distribute VPN routes, VRF tables isolate customer traffic.

IGP Scaling: OSPF multi-area or IS-IS levels to limit LSDB size and control LSA flooding.

Potential projects

GNS3 MPLS Backbone: Build three routers, enable LDP and RSVP-TE, configure an RSVP-TE LSP with FRR on link failure.

BGP VPNs: Spin up two PE routers in GNS3, configure MP-BGP, define two VRFs, and validate isolation between customer sites.

SR-TE Demo: Use FRRouting’s SR-TE feature to carve an explicit path across your lab routers, forcing traffic to avoid a “bad” link.


