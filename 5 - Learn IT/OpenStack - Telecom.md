[[hyperscaler]]
[[To be published - WizardryAtWork]]

---

## 🧱 1. **Do Telcos Virtualise All Their Network Infrastructure?**

Not *all*, but they're aggressively moving in that direction. This shift is known as **NFV (Network Functions Virtualisation)**.

### Key Concept:

Instead of relying on dedicated hardware appliances (firewalls, routers, BNGs, etc.), telcos now **run network functions as VMs or containers** on COTS (commodity off-the-shelf) hardware using OpenStack.

> Think: Instead of a \$100K hardware box from Cisco/Nokia, you spin up a VM running vRouter, vFirewall, vIMS, etc.

---

## 🔧 2. **What Hardware Do They Use with OpenStack?**

While there's no single standard, here's the typical layout:

### a) **Compute Nodes**:

* High-core count x86 CPUs (often AMD EPYC or Intel Xeon)
* 256–1024 GB RAM
* Dual 25/40/100 GbE NICs (Mellanox, Intel)
* Optional GPU or FPGA for network offload (SmartNICs like NVIDIA BlueField)

### b) **Storage Nodes** (Ceph cluster):

* SAS/SATA SSDs for journals/cache
* HDDs for capacity
* NVMe tiers for performance
* 10/25/40GbE NICs
* Sometimes hyper-converged with compute

### c) **Networking**:

* TOR (Top-of-Rack) switches with high-throughput L2/L3 support
* Spine-leaf architecture
* SDN controllers like OpenDaylight or Tungsten Fabric
* SR-IOV and DPDK-enabled NICs for low-latency VNF performance

### d) **Out-of-Band (OOB) Management**:

* IPMI/iDRAC/iLO access via separate VLAN
* Often a dedicated management switch for BMC traffic

---

## 🧠 3. **What Does OpenStack Actually Run in Telco Context?**

* **Nova**: VMs for VNFs
* **Neutron**: SDN-backed networks for isolation & traffic shaping
* **Cinder**: Block storage for stateful network functions
* **Glance**: VNF image management
* **Ironic**: Bare-metal provisioning for high-throughput NFV workloads
* **Magnum/Kolla** (optional): Container orchestration (K8s) on top of OpenStack
* **Tacker**: VNF manager supporting ETSI MANO (Management & Orchestration) standards

---

## 🛰️ 4. **Common Telco Network Functions Virtualised**

| Legacy Function                 | Virtualised Equivalent                                         |
| ------------------------------- | -------------------------------------------------------------- |
| BNG (Broadband Network Gateway) | vBNG                                                           |
| Firewall                        | vFirewall                                                      |
| IMS (IP Multimedia Subsystem)   | vIMS                                                           |
| DPI (Deep Packet Inspection)    | vDPI                                                           |
| CG-NAT                          | vCGN                                                           |
| Load Balancer                   | vLB                                                            |
| EPC (Evolved Packet Core)       | vEPC                                                           |
| RAN (Radio Access Network)      | vRAN (typically uses OpenShift, K8s more often than OpenStack) |

---

## 🌍 Real-World Examples

* **AT\&T**: Runs OpenStack at scale via their *AT\&T Integrated Cloud (AIC)* with millions of vCPUs.
* **Verizon**: Built a massive OpenStack deployment to support NFV.
* **Deutsche Telekom**: Runs OpenStack and Kubernetes in their *Pan-Net* architecture.

---

## 🧰 Bonus: Why Not Just Use VMware?

They did. But:

* OpenStack is open-source, customizable, and avoids vendor lock-in.
* Works better for **multi-tenant edge + core** cloud deployments.
* Often deployed with **Ceph** as a native storage backend to reduce SAN reliance.

---

If you're coming from a Proxmox background: imagine running VyOS, OPNsense, FreeRADIUS, etc. as Proxmox VMs — but now at national scale, with programmable API-driven deployment across data centers, PoPs, and even MEC (Mobile Edge Compute) locations.

Want a sample architecture diagram or a breakdown of how this would scale from a single site to regional clusters?

Perfect. Let’s break down **OpenStack networking (Neutron)** in a way that makes sense for someone familiar with **Proxmox VE**, especially if you’ve done some VLAN tagging, bridges, and maybe played with SDN plugins like Open vSwitch (OVS).

---

## 🧠 Core Concept: OpenStack ≠ Hypervisor

OpenStack is a **cloud controller platform**, not a hypervisor. Under the hood, it usually runs **KVM/QEMU**, same as Proxmox. But the big shift is:

- **Proxmox**: You define networking manually per VM/host.
    
- **OpenStack**: You **define networks via API/UI**, and OpenStack wires up the plumbing underneath using **Neutron**.
    

So let’s translate Neutron concepts to something a Proxmox user can digest.

---

## 🕸️ Basic Networking Modes in OpenStack (as a Proxmox User)

|OpenStack|What it means in Proxmox terms|
|---|---|
|**Provider network**|A VM bridged directly to a physical NIC or VLAN, just like `vmbr0.20` on `enp1s0` in Proxmox|
|**Self-service network**|A virtual, internal-only network like a `vmbr1` bridge with no uplink, but with NAT + DHCP|
|**Tenant network (VXLAN)**|A fully virtual L2 overlay via VXLAN, routed over the underlay—nothing like this exists natively in Proxmox|
|**Router (Neutron L3 agent)**|Like setting up a VM as a pfSense box or Linux router to connect two Proxmox bridges|
|**Floating IP**|A 1:1 NAT from public IP to internal VM IP—think of `iptables DNAT` but via API|

---

## 🔌 Networking Stack Breakdown (OpenStack vs Proxmox)

### 1. **Underlay (Physical) Network**

- **Proxmox**: You tag traffic manually using `vmbrX` and bridge interfaces to VLAN trunks.
    
- **OpenStack**: You predefine **"provider networks"** that map to VLANs or flat networks. These are often used for:
    
    - Public internet
        
    - Storage
        
    - Management interfaces
        

```yaml
Example:
Provider Network "public" = VLAN 100 on bond0 = mapped to br-ex (external bridge)
```

---

### 2. **Overlay (Tenant) Networks with VXLAN**

- **Proxmox** doesn’t do this natively unless you bring in Open vSwitch or Tinc/WireGuard tunnels.
    
- **OpenStack** automates VXLAN overlays using Neutron and agents.
    

**How it works**:

- Each tenant network gets a unique **VXLAN ID (VNI)**
    
- VMs on the same VNI can talk L2 even across different hypervisors
    
- The traffic is encapsulated and sent over the **underlay IP network**
    
- You need a bigger MTU (usually 1600–1650)
    

This is like **creating a private bridge per customer** and letting them use the same 192.168.0.0/24 space over and over.

---

### 3. **Neutron Router**

Used to **connect overlay networks (VXLAN) to provider networks (VLAN/public)**

Think:

- A **virtual Linux router** running on a “network node”
    
- Handles NAT, DHCP relay, static routing
    
- Gives tenants a virtual gateway and enables floating IPs (public IPs → internal IPs)
    

---

## 🔧 In Practice (Simplified Stack)

### 🔽 Underlay Setup

- All nodes connected via a **L3 routed network**, typically on a bond or trunked interface.
    
- Bridges:
    
    - `br-ex` → external public VLAN (for floating IPs)
        
    - `br-mgmt` → OpenStack control plane (API/SSH/etc)
        
    - `br-vxlan` → Overlay transport
        

### 🔼 Overlay and VM Networking

- Tenant creates a new **Neutron Network** (VXLAN-backed)
    
- Neutron dynamically builds **Linux bridges / OVS bridges** and configures tunnels
    
- VM gets connected to these networks with a virtual NIC (tap interface)
    

---

## 💡 For You as a Proxmox User

You’re used to doing this manually:

- `vmbr0` → physical NIC → tagged VLAN
    
- `vmbr1` → internal no uplink
    
- pfSense VM as router/NAT
    
- Manual floating IP NAT
    

OpenStack automates **all of this**:

- Neutron wires tap interfaces to bridges
    
- VXLAN replaces the need for VLAN gymnastics
    
- Routers and NAT are deployed via API
    
- IPAM/DHCP happens per network
    

---

## 🛠️ Tools That Power This

- **Open vSwitch**: Acts as the bridge/VXLAN tunnel engine (replaces Linux bridges)
    
- **Linuxbridge**: Simpler alternative to OVS (no VXLAN)
    
- **OVN (OVS + Northbound DB)**: Full SDN engine for OpenStack
    
- **Neutron agents**: Do the actual wiring on compute/network nodes
    

---

## 🤔 Should I Use VLAN or VXLAN?

|Use Case|Use VLAN|Use VXLAN|
|---|---|---|
|Simple, on-prem only|✅|❌|
|Need public IP per VM|✅|❌ (use router + NAT)|
|Multi-tenant isolation|❌ (limited VLANs)|✅|
|SDN scaling (cloud-scale)|❌|✅|
|Want dynamic network creation via API|❌|✅|

---

## 📦 Recap for a Proxmox User Building OpenStack

|Element|Proxmox Term|OpenStack Equivalent|
|---|---|---|
|vmbrX|Linux bridge|br-int / br-ex|
|VLAN subinterface|`enp1s0.100`|Provider network with VLAN 100|
|NAT router VM|pfSense/iptables|Neutron L3 agent|
|Manual NAT|`iptables -t nat`|Floating IP via Neutron|
|Internal-only bridge|`vmbr1`|Tenant network (VXLAN)|
|Cloud-init image|Proxmox template|Glance image + metadata service|
|DHCP/static IP|/etc/network/interfaces|Fully automated with Neutron|

---

If you want, I can map **your current Proxmox setup into an OpenStack design**, or help mock up a **sample Neutron config** using OVS or OVN.