# Computer_Networks-Tiro_Mining_Network_Project


## Project Overview
This repository contains the implementation and documentation for Milestone 1 and Milestone 2 of the CMPG 325 Computer Networks project. The project simulates a client environment requiring secure, resilient, and scalable connectivity using Cisco Packet Tracer.  

Key requirements addressed:
- Dual ISP connectivity with failover (R1).
- Firewall with NAT and ACLs (FW1).
- Layer‑3 core switch providing inter‑VLAN routing and DHCP (SW1).
- Access switch with VLAN assignments and trunking (SW2).
- Internal HTTP web server hosting a custom webpage (SRV1).
- Testing evidence for connectivity, feature functionality, firewall/NAT, and ISP failover.

---

## Implementation Summary

### Milestone 1
- **Topology Design:**  
  - Edge router (R1) with dual ISP links.  
  - Firewall (FW1) securing inside/outside traffic.  
  - Layer‑3 core switch (SW1) for VLAN routing.  
  - Access switch (SW2) for client connectivity.  
  - Internal HTTP server (SRV1).  
  - Three client PCs (PC1–PC3).  

- **Configuration Highlights:**  
  - VLANs: 10 (Management), 20 (Servers), 30 (Clients).  
  - DHCP pools defined on SW1 for dynamic IP allocation.  
  - NAT and ACLs configured on FW1.  
  - Default routes set on R1 and SW1.  

### Milestone 2
- **Assigned Feature:** Internal HTTP Web Server.  
  - SRV1 configured with IP `192.168.36.18`, gateway `192.168.36.17`, VLAN 20.  
  - HTTP service enabled with custom webpage: *“Tiro Mining Engineering Services”*.  

- **Testing Evidence:**  
  - Successful pings from PCs to gateways and SRV1.  
  - Browser access to SRV1 webpage.  
  - NAT translations and ACL hit counts on FW1.  
  - Failover test showing ISP2 takeover when ISP1 fails.  

---

##Evidence of Testing
Screenshots included in the documentation file show:
- **Internal Connectivity:** PC1–PC3 pinging gateways and SRV1.  
- **HTTP Server Testing:** Browser access to SRV1 webpage.  
- **Firewall/NAT Testing:** NAT hits and ACL counters.  
- **Failover Testing:** Routing table before/after ISP1 shutdown.  


## 📂 Repository Structure
