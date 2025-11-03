# Network Lab: Redundant Network with HSRP, STP & Layer 2 Security

## Objective
This lab simulates a *redundant multi-VLAN enterprise network* with synchronized HSRP (gateway redundancy) and Spanning Tree Protocol (STP) for path optimization and fault tolerance.  
It also implements Layer 2 security mechanisms including *DHCP Snooping, **Dynamic ARP Inspection (DAI), and **Port Security* to protect against spoofing and MAC-based attacks.

The goal is to design a network that maintains continuous availability even during device or link failures, while ensuring access-layer security.

---

## Topology

Core Routers:

- *R1 (Primary Gateway for VLAN10, Standby for VLAN20)*
  - G0/0 → SW1 G0/1  
  - G0/1 → R3 G0/1 (External Link)
- *R2 (Primary Gateway for VLAN20, Standby for VLAN10)*
  - G0/0 → SW2 G0/1  
  - G0/1 → R3 G0/0 (External Link)
- *R3 (Simulated Internet/External Network)*
  - G0/0 → R2 G0/1  
  - G0/1 → R1 G0/1

Distribution Layer:

- *SW1 (STP Root for VLAN10, Secondary for VLAN20)*
  - G0/1 → R1 (Trusted for DHCP/ARP)
  - F0/1, F0/2 → Uplinks to SW3 & SW4  
- *SW2 (STP Root for VLAN20, Secondary for VLAN10)*
  - G0/1 → R2 (Trusted for DHCP/ARP)
  - F0/1, F0/2 → Uplinks to SW3 & SW4  

Access Layer:

- *SW3 (Access for VLAN10)*
  - F0/1, F0/2 → Uplinks to SW1 & SW2 (Trusted)  
  - F0/3 → PC1 (Port Security enabled)
- *SW4 (Access for VLAN20)*
  - F0/1, F0/2 → Uplinks to SW1 & SW2 (Trusted)  
  - F0/3 → PC2 (Port Security enabled)

End Devices:
- *PC1:* VLAN10 → Subnet 10.0.1.0/28  
- *PC2:* VLAN20 → Subnet 10.0.1.16/28  

---

## IP Addressing

### VLAN Networks
| VLAN | Subnet | Gateway (HSRP Virtual IP) | Active Router | Standby Router |
|------|---------|---------------------------|----------------|----------------|
| 10 | 10.0.1.0/28 | 10.0.1.1 | R1 | R2 |
| 20 | 10.0.1.16/28 | 10.0.1.17 | R2 | R1 |

### WAN Network
| Link | IP Addresses | Subnet | Notes |
|------|---------------|---------|-------|
| R1 ↔ R3 | 203.0.113.1 / 203.0.113.2 | 203.0.113.0/30 | External link |
| R2 ↔ R3 | 203.0.113.5 / 203.0.113.6 | 203.0.113.4/30 | External link |

---

## Lab Summary
- Configured *VLAN10* and *VLAN20* across all switches.  
- Assigned *STP priorities* so that:
  - SW1 is Root Bridge for VLAN10.
  - SW2 is Root Bridge for VLAN20.
- Implemented *HSRP* redundancy:
  - R1 active for VLAN10 / standby for VLAN20.
  - R2 active for VLAN20 / standby for VLAN10.
- Synchronized STP roots with HSRP actives for traffic efficiency.
- Enabled *DHCP Snooping* globally:
  - Trusted ports: uplinks to routers and distribution switches.
  - Untrusted: access ports.
- Configured *Dynamic ARP Inspection (DAI)* to prevent spoofing.
- Implemented *Port Security*:
  - On access switches (SW3 & SW4):
    - Sticky MAC on end-user ports.
    - Violation mode: shutdown.
  - On distribution switches (SW1 & SW2):
    - Restrict mode on uplinks to access layer.
- Verified network recovery after link or device failure.

✅ Testing Results:
- HSRP failover works seamlessly between R1 and R2.  
- STP blocks redundant links properly and reconverges fast after failure.  
- PCs in VLAN10 and VLAN20 get IPs from DHCP and communicate via inter-VLAN routing.  
- DHCP Snooping, DAI, and Port Security prevent spoofed or rogue connections.  
- Network remains operational after router or switch failure.

---

## Notes
- This lab integrates *redundancy (HSRP + STP)* and *Layer 2 security* in a single topology.  
- Designed to simulate a *realistic enterprise network* using Cisco Packet Tracer.  
- Some commands (e.g., errdisable recovery) may not be supported in Packet Tracer.  
- The setup is suitable for *CCNA/CCNP portfolio demonstration* or advanced practice.

---

## Files Included
- lab-hsrp-stp-security.pkt – Cisco Packet Tracer project  
- topology.png – Network topology diagram  
- README.md – This documentation file  
- configs/ – Device configurations (R1, R2, R3, SW1–SW4)  
- verification/ – Output screenshots of key show commands