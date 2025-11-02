# Network Lab: Multi-VLAN Network with DHCP, SSH, ACL & NAT

## Objective
This lab simulates a small enterprise network that connects two VLANs (Management and Employees) to the Internet through an ISP router.  
It demonstrates configuration of *Router-on-a-Stick, **DHCP services, **SSH remote access, **Access Control Lists (ACLs)* for security, and *Network Address Translation (NAT/PAT)* to provide Internet connectivity to internal hosts.

The goal is to replicate a realistic small-office setup where VLAN segmentation, secure remote management, and external access coexist efficiently.

---

## Topology

*HQ Site:*

- *R1 (HQ Router)*
  - G0/0 → R2 G0/0 (WAN link)
  - G0/1 → SW1 G0/1 (Trunk)
- *SW1 (Access Switch)*
  - G0/1 → R1 G0/1 (Trunk)
  - F0/1 → PC1 (VLAN10 – Management)
  - F0/2 → PC2 (VLAN20 – Employees)
- *PC1*
  - VLAN10 (Management)
  - Gets IP via DHCP
- *PC2*
  - VLAN20 (Employees)
  - Gets IP via DHCP

*ISP Site:*

- *R2 (ISP Router)*
  - G0/0 → R1 G0/0 (WAN)
  - G0/1 → “Google Server” (8.8.8.8)
  - G0/2 → “DNS Server” (1.1.1.1)

---

## IP Addressing

### HQ Network
| VLAN | Subnet | Default Gateway |
|------|---------|----------------|
| 10 (Management) | 192.168.1.0/28 | 192.168.1.1 |
| 20 (Employees) | 192.168.1.16/28 | 192.168.1.17 |

### WAN & ISP
| Link / Device | IP Address | Subnet Mask | Notes |
|----------------|-------------|--------------|--------|
| R1 G0/0 | 200.1.1.1 | 255.255.255.252 | WAN interface |
| R2 G0/0 | 200.1.1.2 | 255.255.255.252 | WAN interface |
| DNS Server | 1.1.1.1 | 255.255.255.0 | Local DNS |
| Google Server | 8.8.8.8 | 255.255.255.0 | Simulated Internet |

---

## Lab Summary
- Configured *VLAN10* (Management) and *VLAN20* (Employees) on SW1.  
- Configured *Trunk link* between SW1 and R1 for inter-VLAN routing.  
- Implemented *Router-on-a-Stick* on R1 with subinterfaces for each VLAN.  
- Set up *DHCP pools* on R1 to dynamically assign IPs, gateways, and DNS servers.  
- Enabled *SSH* on R1 for secure management (only VLAN10 permitted).  
- Applied an *ACL* to restrict SSH access to Management VLAN only.  
- Configured *PAT (NAT Overload)* on R1 so both VLANs can reach external networks.  
- Configured *Default route* on R1 pointing to R2 (ISP).  
- R2 simulates *Internet and DNS services*, allowing hostnames like google.com to resolve.  

✅ *Testing Results:*
- PCs in VLAN10 and VLAN20 receive IPs automatically via DHCP.  
- Only VLAN10 can SSH into R1.  
- Both VLANs can ping 8.8.8.8 and access Internet via NAT.  
- DNS resolution (e.g. ping google.com) works through R2’s DNS server.  

⚠ Note: Cisco Packet Tracer sometimes fails to simulate DNS correctly even if configuration is valid. If name resolution fails but ping to IPs succeeds, assume it’s a simulation limitation.

---

## Files Included
- Cisco Packet Tracer file (.pkt)  
- Lab topology screenshot (.png)  
- Lab ReadMe (this file)