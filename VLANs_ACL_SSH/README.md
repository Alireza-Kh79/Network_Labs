# Network Labs - Cisco Packet Tracer Exercises

## Overview
This repository contains lab exercises for network configuration using Cisco Packet Tracer.  
The goal of these exercises is to demonstrate fundamental network skills including VLAN configuration, SVI, ACL, IP routing, and SSH access on multi-layer switches.

---

## Lab 1: VLAN, SVI, ACL, and SSH Configuration

### Objective
- Configure VLANs for different departments: Sales (VLAN 10) and Server Room (VLAN 20).  
- Assign IP addresses to SVI interfaces.  
- Configure ACL to allow only the manager PC to access the server via SSH.  
- Enable SSH on the multi-layer switch for secure remote management.  

### Devices Used
- *SW1* - Multi-layer switch for Sales and Server VLANs  
- *SW2* - Additional switch for lab expansion (optional)  
- PCs assigned to each VLAN for testing connectivity  

### IP Addressing
| VLAN | Device / Role          | IP Address       | Subnet Mask     |
|------|-----------------------|-----------------|----------------|
| 10   | Sales PC (Manager)     | 192.168.10.5    | 255.255.255.0  |
| 10   | SVI VLAN 10            | 192.168.10.1    | 255.255.255.0  |
| 20   | Staff PC               | 192.168.20.10   | 255.255.255.0  |
| 20   | SVI VLAN 20            | 192.168.20.1    | 255.255.255.0  |

### Key Configurations
1. *VLAN and SVI Setup*
   - VLAN 10 for Sales
   - VLAN 20 for Server Room
   - IP addresses assigned to SVIs
   - Trunk port between switches configured

2. *Access Control List (ACL)*
   - Only manager PC (192.168.10.5) allowed to SSH to the SVI of VLAN 10  
   - All other traffic from sales to server restricted (HTTP/HTTPS blocked)

3. *SSH Configuration*
   - Local user management with password cisco
   - Domain name set (net.lab)
   - RSA key generated
   - SSH enabled for VTY lines

4. *IP Routing*
   - ip routing enabled globally for inter-VLAN routing

### Verification
- Connectivity between PCs verified using *ping*.  
- SSH access tested from manager PC to multi-layer switch.  
- ACL verified by attempting blocked traffic from non-manager PCs.

---

## Files in this Repository
- SW1_running-config.txt – Running configuration of SW1  
- SW2_running-config.txt – Running configuration of SW2 (if applicable)  
- Network_Topology.png – Visual diagram of the lab topology  
- README.md – This file  

---

## Notes
- Packet Tracer is used for lab simulation.  
- This lab is designed for educational purposes and demonstrates core networking skills relevant to CCNA-level knowledge.