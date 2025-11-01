# Network Lab: Multi-Switch & VLAN Configuration with DHCP and EtherChannel

## Objective
This lab simulates a corporate HQ and a branch office network with multiple VLANs, a multi-switch setup, inter-VLAN routing, EtherChannel between switches, and DHCP for dynamic IP allocation. The purpose is to demonstrate my ability to configure Layer 2 and Layer 3 devices, VLANs, subinterfaces, EtherChannel, and DHCP, similar to real-world network scenarios.

## Topology

*HQ:*

- R1
  - G0/0 → SW1 G0/1
  - G0/1 → R2 G0/1
- SW1
  - G0/1 → R1 G0/0
  - G0/2 → DHCP Server
  - F0/1 → SW2 F0/1 (EtherChannel)
  - F0/2 → SW2 F0/2 (EtherChannel)
  - F0/3 → SW2 F0/3 (EtherChannel)
  - F0/4 → PC1 (VLAN10 HR)
  - F0/5 → PC2 (VLAN20 FIN)
  - F0/6 → PC3 (VLAN30 IT)
- SW2
  - F0/1 → SW1 F0/1 (EtherChannel)
  - F0/2 → SW1 F0/2 (EtherChannel)
  - F0/3 → SW1 F0/3 (EtherChannel)
  - F0/4 → PC4 (VLAN40 CLIENT)
  - F0/5 → PC5 (VLAN40 CLIENT)

*Branch Office:*

- R2
  - G0/0 → SW3 G0/1
  - G0/1 → R1 G0/1
- SW3
  - G0/1 → R2 G0/0
  - F0/1 → SW4 F0/1 (EtherChannel)
  - F0/2 → SW4 F0/2 (EtherChannel)
  - F0/3 → SW4 F0/3 (EtherChannel)
  - F0/4 → PC6 (VLAN10 HR Branch)
  - F0/5 → PC7 (VLAN20 FIN Branch)
  - F0/6 → PC8 (VLAN30 IT Branch)
- SW4
  - F0/1 → SW3 F0/1 (EtherChannel)
  - F0/2 → SW3 F0/2 (EtherChannel)
  - F0/3 → SW3 F0/3 (EtherChannel)
  - F0/4 → PC9 (VLAN40 CLIENT Branch)

## IP Addressing

### HQ
| VLAN | Subnet          | Default Gateway  |
|------|----------------|----------------|
| 10   | 192.168.10.0/28 | 192.168.10.1   |
| 20   | 192.168.10.16/28 | 192.168.10.17  |
| 30   | 192.168.10.32/28 | 192.168.10.33  |
| 40   | 192.168.10.48/28 | 192.168.10.49  |

### Branch
| VLAN | Subnet          | Default Gateway  |
|------|----------------|----------------|
| 10   | 192.168.20.0/28  | 192.168.20.1   |
| 20   | 192.168.20.16/28 | 192.168.20.17  |
| 30   | 192.168.20.32/28 | 192.168.20.33  |
| 40   | 192.168.20.48/28 | 192.168.20.49  |

## Lab Summary
- Configured VLANs on switches and assigned ports to access VLANs.
- Configured EtherChannel between SW1↔SW2 and SW3↔SW4.
- Configured subinterfaces on routers for inter-VLAN routing.
- Set up DHCP pools for each VLAN with proper default gateways.
- Verified connectivity between VLANs and ensured dynamic IP assignment.
- *Note:* No ACLs or SSH configurations were applied in this lab. Due to limitations in Cisco Packet Tracer, some DHCP or ARP behaviors may appear inconsistent. Despite this, all configurations reflect real-world practices.

## Files Included
- Cisco Packet Tracer file (.pkt)
- Lab topology screenshot (.png)
- Lab ReadMe (this file)