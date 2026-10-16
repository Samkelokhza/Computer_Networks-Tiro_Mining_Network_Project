# CMPG325 – Computer Networks: Final Project
## Tiro Mining Engineering Services (Vryburg)

**Student:** Samkelo Mbongela
**Student Number:** 43520286
**Module:** CMPG325 – Computer Networks
**Project ID:** CMPG325-20209-067
**Client ID:** CLI-067

---

##Project Overview

This repository contains the complete implementation, documentation, and testing evidence for the CMPG325 Computer Networks final project. The project simulates a real-world client environment for **Tiro Mining Engineering Services**, requiring secure, resilient, and scalable network connectivity using Cisco Packet Tracer.

### Client Requirements Addressed:
- **Internal HTTP Web Server** hosting a custom company webpage (Assigned Feature).
- **VLAN Segmentation** for Management, Servers, and Clients.
- **Inter-VLAN Routing** on a Layer-3 core switch.
- **Firewall** with NAT and Access Control Lists (ACLs).
- **Dual-ISP Connectivity** with automatic failover for resilience (CR15).
- **DHCP** for automatic client addressing.

---

## Network Topology and Device Roles

The network consists of the following devices:

| Device | Role |
| :--- | :--- |
| **ISP1** | Primary Internet Service Provider connection. |
| **ISP2** | Backup Internet Service Provider connection (CR15). |
| **R1** | Edge router with dual WAN links and floating static route. |
| **FW1** | Cisco ASA firewall providing NAT and ACL security. |
| **SW1** | Layer-3 core switch providing VLAN gateways and inter-VLAN routing. |
| **SW2** | Access switch connecting client workstations. |
| **SRV1** | Internal HTTP server hosting the company webpage. |
| **PC1–PC3** | Client workstations obtaining IP addresses via DHCP. |

The topology diagram is included in the technical report (`Figure 1`).

---

## IP Addressing and VLAN Design

The internal network uses the `192.168.36.0/24` address block, divided into three VLANs:

| VLAN | Purpose | Subnet | Gateway |
| :--- | :--- | :--- | :--- |
| VLAN 10 | Management | 192.168.36.0/28 | 192.168.36.1 |
| VLAN 20 | Servers | 192.168.36.16/28 | 192.168.36.17 |
| VLAN 30 | Clients | 192.168.36.32/27 | 192.168.36.33 |

**Transit Networks:**
- **R1–FW1:** `172.16.0.0/30` (R1: `.1`, FW1: `.2`)
- **FW1–SW1:** `192.168.36.64/30` (FW1: `.65`, SW1: `.66`)

**WAN Links:**
- **ISP1:** `10.0.0.0/30` (R1: `.2`, ISP1: `.1`)
- **ISP2:** `10.0.0.4/30` (R1: `.6`, ISP2: `.5`)

**Server:** SRV1 uses the static IP `192.168.36.18/28` with gateway `192.168.36.17`.

---

## Implementation Summary

### Milestone 1 – Design and Base Configuration
- Designed the physical and logical topology.
- Configured VLANs 10, 20, and 30 on SW1 and SW2.
- Configured DHCP pools on SW1 for client addressing.
- Configured interface IP addressing on R1, FW1, and SW1.
- Configured default routes on R1 and SW1.
- Configured NAT and ACLs on FW1.

### Milestone 2 – Assigned Feature and Testing
- **Assigned Feature:** Internal HTTP Web Server.
  - SRV1 configured with static IP `192.168.36.18`, gateway `192.168.36.17`, VLAN 20.
  - HTTP service enabled with a custom webpage: *"Tiro Mining Engineering Services"*.
  - Webpage verified from PC1, PC2, and PC3 using `http://192.168.36.18`.
- **Testing Evidence Collected:**
  - Successful pings from PC1–PC3 to gateways and SRV1.
  - Browser access to the internal webpage from all three clients.
  - NAT translations and ACL hit counts confirmed on FW1.
  - Failover test showing ISP2 takeover when ISP1 fails.

### Milestone 3 – Final Evaluation
- Completed the final technical report with all required sections.
- Verified end-to-end connectivity (internal, external, and failover).
- Documented troubleshooting and resolutions.
- Recorded the 15–20 minute inset video demonstration.
- Finalized the GitHub portfolio of evidence.

---

##  Testing and Verification

All tests were performed in Cisco Packet Tracer and documented with screenshots in the technical report.

| Test | Description | Evidence |
| :--- | :--- | :--- |
| **Internal Connectivity** | PC1–PC3 pinging gateway (`192.168.36.33`) and SRV1 (`192.168.36.18`). | Figures 14–19 in the report. |
| **HTTP Server Access** | PC1–PC3 accessing `http://192.168.36.18`. | Figure 5 in the report. |
| **Firewall/NAT** | `show nat` and `show access-list` on FW1. | Figure 3 in the report. |
| **Internet Connectivity** | PC1 pinging `8.8.8.8` with 0% loss. | Included in the report. |
| **CR15 Failover** | Continuous ping recovering after ISP1 shutdown on R1. | Included in the report. |

---

## Troubleshooting and Resolutions

### 1. Firewall Blocking ICMP Traffic
- **Problem:** Clients could not ping external addresses despite correct routing.
- **Diagnosis:** Used Packet Tracer Simulation Mode to trace the packet; found it was dropped at FW1.
- **Resolution:** Applied `inspect icmp` to the global policy map on FW1. Re-tested and confirmed connectivity.

### 2. Router Switch-Module Interface Issue
- **Problem:** A Layer-2 switchport on R1 could not be configured as a routed interface.
- **Resolution:** Used SW1 as the Layer-3 core for inter-VLAN routing while retaining R1 for WAN routing.

### 3. Systematic Troubleshooting Approach
- Verified interfaces, inspected routing tables, checked firewall and NAT behaviour, and tested the complete path before concluding that a service was working.

