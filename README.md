🏛️ **USIU Campus Network — Enterprise Network Simulation**

A full-scale, multi-layer enterprise campus network simulation built in Cisco Packet Tracer, modelled after a real private university environment (USIU-Africa, Nairobi). Designed to demonstrate production-grade network engineering across routing, switching, security, redundancy, and automation-readiness.


📌 **Project Overview**

This project simulates the complete network infrastructure of a university campus - from edge connectivity to end-user access — using a strict three-tier hierarchical design model. Every design decision mirrors real-world enterprise deployments, covering Layer 2 hardening, Layer 3 dynamic routing, gateway redundancy, DHCP relay, and network security enforcement across 12 VLANs serving multiple academic and administrative departments.

The topology spans four routing domains, multiple distribution zones, dual-stack redundancy via HSRP, inter-VLAN routing via SVIs, and an ISP uplink with static routing — making it one of the most comprehensive student-grade network simulations achievable in Packet Tracer.


📌**Key Features**

🔸**MD5 encryption** on all routers and switches for secure OSPF authentication.

🔸**Access ports** and **trunks** configured for VLAN segmentation.

🔸**Port‑security** with sticky MACs and violation modes.

🔸**DHCP pools** for 12 VLANs, with helper addresses inside SVIs.

🔸**DHCP Snooping** and **Dynamic ARP Inspection** for Layer 2 security.

🔸**EtherChannel** for link aggregation and redundancy.

🔸**ACLs** applied for traffic filtering and security policies.

🔸**HSRP** for gateway redundancy.

🔸**STP** with priority tuning to prevent loops.

🔸**Loopbacks** for router identification and OSPF stability.

🔸**Passive interfaces** in OSPF to reduce unnecessary hello traffic.

🔸**IP routing** enabled on Layer 3 switches for inter‑VLAN communication.

🔸**Serial connections** with clock rate and PPP encapsulation for WAN simulation.

🔸**Static route** to ISP for external connectivity.

🔸ISP provider cloud integrated to simulate internet access.


**🌐 Advanced Concepts Added**

To make the design more sophisticated:

➜**AAA authentication** using local database (future RADIUS/TACACS+ integration).

➜**Syslog and SNMP** for monitoring and logging.

➜**NTP** for time synchronization across all devices.

➜**QoS policies** for prioritizing voice/video traffic.

➜Cloud integration concepts (simulated ISP + external services).

➜**IPv6** readiness with dual‑stack addressing for future scalability.

➜**Security hardening**: disabling unused ports, service password encryption, and banner warnings.


📌**Objectives**

This project was built to simulate real-world enterprise networking operations and demonstrate practical skills in:

▪Enterprise campus design

▪Layer 2 and Layer 3 switching

▪VLAN segmentation

▪Routing and route advertisement

▪High availability and redundancy

▪Network hardening and access control

▪DHCP deployment and troubleshooting

▪Secure switch configurations

▪Scalability and fault tolerance

▪Structured network documentation


🏗️ **Architecture — Three-Tier Hierarchical Design**
✅**Core Layer**

**USI-CORE-R1 (Cisco 2911)** — Central routing hub, OSPF backbone (Area 0), connects all distribution zones via serial and GigabitEthernet uplinks

✅**Distribution Layer**

**4x Cisco 3560-24PS L3 switches** — Inter-VLAN routing via SVIs, HSRP active/standby gateway redundancy, EtherChannel uplinks to access layer, OSPF participation, DHCP relay via ip helper-address

✅**Access Layer**

**4x Cisco 2960-24TT L2 switches** — VLAN access port assignment, 802.1Q trunking, EtherChannel to distribution, port security, DHCP Snooping, and DAI enforcement


📌**Technologies & Protocols Implemented**

✅**VLAN Segmentation**

12 VLANs were created to isolate departments and reduce broadcast domains.

VLAN	Department

➔10	Hostels

➔20	CCTV & Security

➔30	CompLab & ICT Department

➔40	Library & Innovation Hub

➔50	Finance & Economics

➔60	Cafeteria

➔70	Conference Centre

➔80	Administration

➔90	Lecture Halls

➔100	Medical Labs & Scientific Research Dept

➔110	Court Room

➔120	Engineering & Robotics 


📌**Trunking**

802.1Q trunk links were configured between switches to allow multiple VLANs across uplinks.

Features implemented:

•Native VLAN configuration

•Allowed VLAN restrictions

•Multi-switch trunking architecture


📌**EtherChannel**

🔘EtherChannel was configured between switches to provide:

🔘Link aggregation

🔘Increased bandwidth

🔘Redundancy

🔘Loop prevention

🔘Protocols used:

🔘PAgP (desirable mode)

📌**Spanning Tree Protocol (STP)**

Rapid-PVST was implemented for loop prevention and optimized convergence.

Enhancements include:

Root bridge tuning
Priority adjustments
PortFast
BPDU Guard

📌**Port Security**

Access ports were hardened using:

Sticky MAC learning
MAC address limits
Restrict violation mode

This prevents:

Rogue devices
Unauthorized switch access
MAC flooding attacks


📌**Routing**

OSPFv2 Multi-Area — Area 0 (backbone), Area 2, Area 3, Area 4 with proper ABR configuration.
Static Routing — Default route to ISP (ip route 0.0.0.0 0.0.0.0) for internet connectivity.
Route Redistribution — Connected subnets redistributed into OSPF on L3 distribution switches.
Loopback Interfaces — Stable router IDs on all routers, used as OSPF router-ID anchors.
Passive Interfaces — Configured on all access-facing SVIs to suppress unnecessary OSPF hellos.

📌 **Switching**

VLANs — 12 VLANs, consistently provisioned across all switches.
802.1Q Trunking — All inter-switch and switch-to-router links, explicit VLAN allow lists.
EtherChannel (PAgP) — Port-channel bundles (Po1, Po3) on all distribution-to-access uplinks for redundancy and bandwidth aggregation.
STP (Rapid-PVST+) — Per-VLAN spanning tree with explicit root bridge priority assignments, PortFast and BPDUGuard on all access ports.
SVIs — Layer 3 virtual interfaces on all distribution switches for inter-VLAN routing and HSRP.

📌 **Redundancy & High Availability**

🔘HSRP (Hot Standby Router Protocol) — Active/standby gateway redundancy per VLAN, virtual IPs as default gateways, priority and preempt configured, group IDs matching VLAN IDs.

🔘EtherChannel — Link aggregation providing both redundancy and load balancing on uplinks.

DHCP

DHCP Server — Centralized per router (EDGE-R2, EDGE-R3), per-VLAN pools with domain names.
DHCP Excluded Addresses — First 10 addresses per subnet reserved for infrastructure.
ip helper-address — Configured on all SVIs to relay broadcasts across L3 boundaries to DHCP servers.
DHCP Snooping — Enabled per zone, trusted ports on EtherChannel uplinks and routed uplinks, no ip dhcp snooping information option to prevent option-82 relay issues in PT.

Security

MD5 Authentication — enable secret with MD5 hash on all routers and switches.
DHCP Snooping — Prevents rogue DHCP server attacks, binding table built per VLAN.
Dynamic ARP Inspection (DAI) — Validates ARP packets against DHCP snooping binding table, per-VLAN enforcement on all access and distribution switches.
Port Security — Sticky MAC learning on all access ports, violation restrict mode, maximum 2 MAC addresses per port.
BPDUGuard — Globally enabled via spanning-tree portfast bpduguard default, shuts rogue switch connections.
PortFast — Globally enabled on all access switches for immediate port state transition.
Access Control Lists (ACLs) — Applied for inter-zone traffic filtering and management plane protection.

WAN & Serial Connectivity

Serial Links — PPP encapsulation on all router-to-router WAN links.
Clock Rate — DCE-side clock rate configured on all serial connections.
ISP Uplink — Static default route toward ISP with cloud simulation.

Management & Infrastructure

ip routing — Enabled on all Layer 3 distribution switches.
MAC Address Assignment — Explicit MAC addresses on SVIs for stability in PT.
EtherChannel Channel-Groups — PAgP desirable mode, consistent across all bundles.


**Skills **Demonstrated**

**Networking**

Enterprise campus design
Dynamic routing
Layer 2 switching
Layer 3 switching
WAN technologies
Redundancy engineering
VLAN architecture

**Security**

DHCP Snooping
Dynamic ARP Inspection
Port Security
Segmentation
Network hardening

**Operations**
Troubleshooting
Configuration management
Network documentation
Infrastructure planning

**Tools Used**
Cisco Packet Tracer
Cisco IOS CLI
Wireshark
Gns3


Project Highlights

✔ Enterprise-style 3-tier campus architecture
✔ 12 departmental VLANs
✔ Redundant Layer 2 and Layer 3 paths
✔ Dynamic routing with OSPF
✔ Gateway redundancy using HSRP
✔ Secure switching implementation
✔ DHCP relay architecture
✔ WAN and ISP simulation
✔ Real-world troubleshooting scenarios
✔ Scalable and modular design

👤 Author

Bradley Giovanni

Network Engineer | Network Administrator | NOC Engineer


📄 License
This project is open for reference and educational use. If you use this topology or configs as a base for your own lab, a star on the repo is appreciated. ⭐


🚀 How to Run

1. Download and install Cisco Packet Tracer 8.x or later
2. Clone this repository: git clone https://github.com/Brxdl3y/USIU-Campus-Network
3. Open topology/USIU_Campus_Network.pkt in Packet Tracer
4. Wait approximately 60 seconds for OSPF to converge and HSRP elections to complete
5. Test connectivity using the simulation panel or CLI ping tests
