___
**Tags:** 

**Links:** 

---
#networking #Learning #study-notes #switching #VPN #virtualization #network-security #cyber-security 

[[Personal Learning]]
[[Source Material]]
[[]]
[[Cisco Networking Basics - Notes]]

[[Cisco Networking Basics]][[cisco packet tracer activity]][[Cisco Networking Basics - Notes]] [[Cisco Network Addressing and Basic Troubleshooting]]

---

### **1. How Ethernet Frames Carry Data, How MAC Addresses Work, and Layer 2 Switching Concepts**

#### **Ethernet Frames:**

Ethernet is the most common technology used for local area networks (LANs). Ethernet frames are data packets transmitted over the network at Layer 2 (the Data Link layer of the OSI model). The frame contains:

- **Preamble:** A sequence of bits for synchronization.
- **Destination MAC Address:** The address of the device intended to receive the data.
- **Source MAC Address:** The address of the device sending the data.
- **EtherType:** Identifies the protocol in the payload (e.g., IPv4).
- **Payload:** The actual data being transmitted (usually an IP packet).
- **Frame Check Sequence (FCS):** Used to detect errors in the frame.

#### **MAC Addresses:**

A **Media Access Control (MAC) address** is a unique identifier assigned to network interfaces for communication at the data link layer. It's a 48-bit hexadecimal address (e.g., `00:1A:2B:3C:4D:5E`), permanently assigned to a network device.

- **Unicast:** A frame sent to a specific MAC address.
- **Broadcast:** A frame sent to all devices in a network segment (FF:FF:FF:FF:FF
    
    ).
- **Multicast:** A frame sent to a group of devices.

#### **Layer 2 Switching:**

A **Layer 2 switch** uses MAC addresses to forward data between devices within the same LAN. It maintains a **MAC address table** that maps MAC addresses to specific switch ports.

- When a switch receives a frame, it checks the destination MAC address and forwards the frame to the correct port based on its MAC table.
- If the destination MAC address isn’t in the table, the switch floods the frame to all ports except the one it received it from (this is called **flooding**).

---

### **2. How Routing Works, and Differences Between RIP, OSPF, and EIGRP Protocols**

#### **Routing Basics:**

Routers operate at Layer 3 (Network layer) and direct data between different networks by selecting the best path for packet transmission based on routing tables. When a router receives a packet, it looks at the **destination IP address** and forwards it to the next hop based on its routing table.

#### **Routing Protocols:**

- **RIP (Routing Information Protocol):**
    
    - Type: Distance-vector protocol.
    - Metric: Uses hop count (max 15 hops, 16 is considered unreachable).
    - Characteristics: Easy to configure but not scalable for large networks.
    - Routing Updates: Every 30 seconds, leading to slower convergence.
- **OSPF (Open Shortest Path First):**
    
    - Type: Link-state protocol.
    - Metric: Based on **cost**, which typically reflects bandwidth.
    - Characteristics: Scalable, used in large networks, faster convergence, supports **hierarchical design**.
    - Routing Updates: Sent only when network changes occur (rather than periodic updates).
- **EIGRP (Enhanced Interior Gateway Routing Protocol):**
    
    - Type: Hybrid protocol (combines characteristics of distance-vector and link-state protocols).
    - Metric: Uses a composite of bandwidth, delay, load, and reliability.
    - Characteristics: Faster convergence than RIP, uses **DUAL** (Diffusing Update Algorithm) for loop-free routing.
    - Routing Updates: Only sent when a topology change occurs.

---

### **3. Wi-Fi Standards (802.11 a/b/g/n/ac)**

#### **Wi-Fi Standards:**

Wi-Fi standards are developed by the **IEEE** and fall under the 802.11 family. Here’s a breakdown of key standards:

- **802.11a:**
    
    - Frequency: 5 GHz
    - Speed: Up to 54 Mbps
    - Range: Shorter range, higher interference resistance
    - Use: Often used in enterprise environments.
- **802.11b:**
    
    - Frequency: 2.4 GHz
    - Speed: Up to 11 Mbps
    - Range: Longer range, more interference (from devices like microwaves, Bluetooth).
- **802.11g:**
    
    - Frequency: 2.4 GHz
    - Speed: Up to 54 Mbps
    - Range: Similar to 802.11b, backward-compatible with 802.11b.
- **802.11n:**
    
    - Frequency: 2.4 GHz and 5 GHz (dual-band)
    - Speed: Up to 600 Mbps (with MIMO – multiple input, multiple output antennas)
    - Range: Greater than previous standards.
- **802.11ac:**
    
    - Frequency: 5 GHz
    - Speed: Up to 1.3 Gbps
    - Features: Wider channels, better MIMO, beamforming for improved performance.

---

### **4. NAT (Network Address Translation), ARP (Address Resolution Protocol), and Broadcast Domains**

#### **NAT (Network Address Translation):**

NAT translates private IP addresses used inside a network to a public IP address used on the internet. It conserves public IP addresses and adds a layer of security by hiding internal IPs.

- **Types of NAT:**
    - **Static NAT:** One-to-one mapping of private to public IP.
    - **Dynamic NAT:** Maps a private IP to a pool of public IPs.
    - **PAT (Port Address Translation):** Many-to-one mapping (multiple devices share one public IP, differentiated by port numbers).

#### **ARP (Address Resolution Protocol):**

ARP resolves IP addresses to MAC addresses. When a device knows the IP address but not the MAC address, it sends out an ARP request. The device with the matching IP responds with its MAC address.

- **Example:** If a computer wants to send data to another within the same network, it uses ARP to find the destination MAC address.

#### **Broadcast Domains:**

A broadcast domain is a network segment where a broadcast sent by one device is received by all devices within that segment. Devices in different broadcast domains require routers to communicate.

- **Switches** create multiple collision domains but operate within the same broadcast domain.
- **Routers** separate broadcast domains and prevent broadcast traffic from propagating to other networks.

---

### **5. The 7 Layers of the OSI Model and the 4 Layers of the TCP/IP Model**

#### **OSI Model (7 Layers):**

1. **Physical Layer** – Hardware, cables, and signal transmission.
2. **Data Link Layer** – MAC addresses, Ethernet, frames, and switches.
3. **Network Layer** – IP addresses, routers, and routing.
4. **Transport Layer** – End-to-end communication, TCP/UDP.
5. **Session Layer** – Session management, opening and closing connections.
6. **Presentation Layer** – Data formatting, encryption, and decryption.
7. **Application Layer** – User interface, protocols like HTTP, FTP, DNS.

#### **TCP/IP Model (4 Layers):**

1. **Network Access (Link) Layer** – Combines OSI's Physical and Data Link layers.
2. **Internet Layer** – Same as OSI's Network layer (IP routing).
3. **Transport Layer** – Same as OSI's Transport layer (TCP/UDP).
4. **Application Layer** – Combines OSI's Application, Presentation, and Session layers.

#### **Comparison:**

- **TCP/IP model** is more streamlined with fewer layers and focuses on real-world implementation.
- **OSI model** is conceptual and breaks down networking into more granular functions.

---

### **6. Key Protocols: TCP, UDP, IP**

#### **TCP (Transmission Control Protocol):**

- **Connection-oriented**: Establishes a reliable connection before data transfer.
- **Features:** Acknowledgments, error-checking, flow control.
- **Use Cases:** Web browsing (HTTP), email (SMTP), file transfer (FTP).

#### **UDP (User Datagram Protocol):**

- **Connectionless**: Sends data without establishing a connection, faster but less reliable.
- **Features:** No error-checking or acknowledgment.
- **Use Cases:** Streaming (video/audio), DNS queries, online gaming.

#### **IP (Internet Protocol):**

- **Connectionless protocol** used to deliver packets from one host to another based on their IP addresses.
- **IPv4 vs. IPv6:** IPv4 uses 32-bit addresses, while IPv6 uses 128-bit addresses to solve address exhaustion.

---
![[Pasted image 20240920155427.png]]

![[Pasted image 20240920160420.png]]
---

Before any network communications can occur, a physical connection to a local network must be established. A physical connection can be a wired connection using a cable or a wireless connection using radio waves. Network Interface Cards (NICs) connect a device to the network. Ethernet NICs are used for a wired connection, whereas WLAN (Wireless Local Area Network) NICs are used for wireless connections. The OSI physical layer provides the means to transport the bits that make up a data link layer frame across the network media. This layer accepts a complete frame from the data link layer and encodes it as a series of signals that are transmitted onto the local media. The encoded bits that comprise a frame are received by either an end device or an intermediary device.

The physical layer consists of electronic circuitry, media, and connectors developed by engineers. The physical layer standards address three functional areas: physical components, encoding, and signaling. Bandwidth is the capacity at which a medium can carry data. Digital bandwidth measures the amount of data that can flow from one place to another in a given amount of time. Throughput is the measure of the transfer of bits across the media over a given period of time and is usually lower than bandwidth. Latency refers to the amount of time, including delays, for data to travel from one given point to another. Goodput is the measure of usable data transferred over a given period of time. The physical layer produces the representation and groupings of bits for each type of media as follows:

- **Copper cable** - The signals are patterns of electrical pulses.
- **Fiber-optic cable** - The signals are patterns of light.
- **Wireless** - The signals are patterns of microwave transmissions.

Networks use copper media because it is inexpensive, easy to install, and has low resistance to electrical current. However, copper media is limited by distance and signal interference. The timing and voltage values of the electrical pulses are also susceptible to interference from two sources: EMI and crosstalk. Three types of copper cabling are: UTP, STP, and coaxial cable (coax). UTP has an outer jacket to protect the copper wires from physical damage, twisted pairs to protect the signal from interference, and color-coded plastic insulation that electrically isolates wires from each other and identifies each pair. The STP cable uses four pairs of wires, each wrapped in a foil shield, which are then wrapped in an overall metallic braid or foil. Coaxial cable gets its name from the fact that there are two conductors that share the same axis. Coax is used to attach antennas to wireless devices. Cable internet providers use coax inside their customers’ premises.

UTP cabling consists of four pairs of color-coded copper wires that have been twisted together and then encased in a flexible plastic sheath. UTP cable does not use shielding to counter the effects of EMI and RFI. Instead, cable designers have discovered other ways that they can limit the negative effect of crosstalk: cancellation and varying the number of twists per wire pair. UTP cabling conforms to the standards established jointly by the ANSI/TIA. The electrical characteristics of copper cabling are defined by the Institute of Electrical and Electronics Engineers (IEEE). UTP cable is usually terminated with an RJ-45 connector. The main cable types that are obtained by using specific wiring conventions are Ethernet Straight-through and Ethernet Crossover. Cisco has a proprietary UTP cable called a rollover that connects a workstation to a router console port.

Optical fiber cable transmits data over longer distances and at higher bandwidths than any other networking media. Fiber-optic cable can transmit signals with less attenuation than copper wire and is completely immune to EMI and RFI. Optical fiber is a flexible, but extremely thin, transparent strand of very pure glass, not much bigger than a human hair. Bits are encoded on the fiber as light impulses. Fiber-optic cabling is now being used in four types of industry: enterprise networks, FTTH, long-haul networks, and submarine cable networks. There are four types of fiber-optic connectors: ST, SC, LC, and duplex multimode LC. Fiber-optic patch cords include SC-SC multimode, LC-LC single-mode, ST-LC multimode, and SC-ST single-mode. In most enterprise environments, optical fiber is primarily used as backbone cabling for high-traffic point-to-point connections between data distribution facilities and for the interconnection of buildings in multi-building campuses.



---

# Data Link Layer - Module 2 


 Physical and Logical Topologies

As you learned in the previous topic, the data link layer prepares network data for the physical network. It must know the logical topology of a network in order to be able to determine what is needed to transfer frames from one device to another. This topic explains the ways in which the data link layer works with different logical network topologies.

The topology of a network is the arrangement, or the relationship, of the network devices and the interconnections between them.

There are two types of topologies used when describing LAN and WAN networks:

- **Physical topology** – Identifies the physical connections and how end devices and intermediary devices (i.e, routers, switches, and wireless access points) are interconnected. The topology may also include specific device location such as room number and location on the equipment rack. Physical topologies are usually point-to-point or star.
- **Logical topology** - Refers to the way a network transfers frames from one node to the next. This topology identifies virtual connections using device interfaces and Layer 3 IP addressing schemes.

The data link layer "sees" the logical topology of a network when controlling data access to the media. It is the logical topology that influences the type of network framing and media access control used.

The figure displays a sample **physical** topology for a small sample network.
![[Pasted image 20240920161909.png]]
![[Pasted image 20240920161918.png]]

---

**Topologies**

The two types of topologies used in LAN and WAN networks are physical and logical. The data link layer "sees" the logical topology of a network when controlling data access to the media. The logical topology influences the type of network framing and media access control used. Three common types of physical WAN topologies are: point-to-point, hub and spoke, and mesh. Physical point-to-point topologies directly connect two end devices (nodes). Adding intermediate physical connections may not change the logical topology. In multiaccess LANs, nodes are interconnected using star or extended star topologies. In this type of topology, nodes are connected to a central intermediary device.

Physical LAN topologies include: star, extended star, bus, and ring. Half-duplex communications exchange data in one direction at a time. Full-duplex sends and receives data simultaneously. Two interconnected interfaces must use the same duplex mode or there will be a duplex mismatch creating inefficiency and latency on the link. Ethernet LANs and WLANs are examples of multiaccess networks. A multiaccess network is a network that can have multiple nodes accessing the network simultaneously.

Some multiaccess networks require rules to govern how devices share the physical media. There are two basic access control methods for shared media: contention-based access and controlled access. In contention-based multiaccess networks, all nodes are operating in half-duplex. There is a process if more than one device transmits at the same time. Examples of contention-based access methods include: CSMA/CD for bus-topology Ethernet LANs and CSMA/CA for WLANs.


### **Key Differences at a Glance:**

|**Feature**|**CSMA/CD**|**CSMA/CA**|
|---|---|---|
|**Main Approach**|Detect collisions after they happen and retransmit.|Avoid collisions before they happen.|
|**Used in**|Wired networks (Ethernet).|Wireless networks (Wi-Fi, 802.11).|
|**Collision Handling**|Detects collisions and stops transmission; uses a jamming signal to notify all devices.|Avoids collisions by sending RTS/CTS signals (optional) and waiting for a clear channel.|
|**Backoff Mechanism**|Backoff occurs **after** a collision.|Backoff occurs **before** transmitting, based on a random waiting period.|
|**Efficiency**|More efficient with low traffic; performance degrades with high traffic.|Works well with high contention but introduces some delay due to collision avoidance mechanisms.|
|**Example**|Ethernet networks (especially half-duplex, legacy).|Wi-Fi networks (IEEE 802.11).|

### Summary:

- **CSMA/CD** (used in Ethernet) focuses on **collision detection**. Devices send data, detect collisions, and retransmit after waiting a random backoff time.
- **CSMA/CA** (used in Wi-Fi) focuses on **collision avoidance**. Devices check if the channel is clear, possibly exchange RTS/CTS signals, and back off **before** transmitting to reduce the likelihood of collisions.

In short, **CSMA/CD** deals with collisions after they happen (common in wired Ethernet), while **CSMA/CA** tries to prevent collisions from occurring in the first place (essential for wireless communication where collisions are harder to detect).


---

### **CSMA/CD (Carrier Sense Multiple Access with Collision Detection)**

- **Used in**: **Wired networks**, specifically **Ethernet** (originally in half-duplex Ethernet).
    
- **Collision Detection**: In CSMA/CD, devices first "listen" to the network medium (usually a shared Ethernet cable) to check if it's free before transmitting. If two devices transmit at the same time, a **collision** occurs. The devices detect the collision by sensing abnormal voltage levels on the wire.
    
    - **Post-Collision Process**: Once a collision is detected, devices stop transmitting, send a jamming signal to ensure all parties are aware of the collision, and then wait for a random period (using a **backoff algorithm**) before attempting to retransmit.
- **Efficiency**: CSMA/CD is efficient in environments with **low network traffic**. However, as network traffic increases and more collisions occur, the performance degrades because devices spend more time retransmitting after collisions.
    
- **Example of Use**: **Ethernet LANs** using **half-duplex** communication, especially legacy systems.
    

---

### **CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)**

- **Used in**: **Wireless networks**, specifically **Wi-Fi (IEEE 802.11)**.
    
- **Collision Avoidance**: In CSMA/CA, devices also "listen" to the network medium before transmitting, but instead of dealing with collisions after they occur, CSMA/CA tries to **avoid collisions** in the first place.
    
    - **How It Works**: A device checks if the channel is free. If it is, the device waits for a random backoff period before sending its data. Optionally, the device can send a **Request to Send (RTS)** signal to the receiver, which responds with a **Clear to Send (CTS)** signal if it's ready. This process reduces the chances of collisions because other devices in the vicinity are aware that communication is taking place.
        
    - **Why It’s Needed**: Wireless networks use CSMA/CA because detecting collisions in a wireless environment is much more difficult than in wired networks (due to the **hidden node problem** where two devices cannot hear each other but still transmit to the same access point).
        
- **Efficiency**: CSMA/CA has better performance in environments with **high contention** for the medium, such as Wi-Fi networks, but introduces additional overhead due to the RTS/CTS process, making it slightly slower than CSMA/CD.
    
- **Example of Use**: **Wi-Fi (IEEE 802.11)** networks, where physical collision detection is not feasible.
