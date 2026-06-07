# Project 01 - Enterprise Network Foundation

## Objective

Design and implement a segmented enterprise-style network using OPNsense, Cisco switching and Proxmox virtualisation.

---

## Technologies Used

- OPNsense
- Cisco CBS350
- Proxmox VE
- VLANs
- DHCP
- DNS
- Active Directory

---

## Network Topology

[Diagram To Be Added]

---

## VLAN Design

| VLAN | Name | Network |
|--------|--------|--------|
| 10 | Management | 192.168.10.0/26 |
| 20 | Users | 192.168.10.64/26 |
| 30 | Servers | 192.168.10.128/26 |
| 40 | Lab | 192.168.10.192/26 |

---

## Infrastructure Components

### OPNsense

Responsibilities:

- Routing
- DHCP
- Firewalling
- Inter-VLAN communication

### Cisco CBS350

Responsibilities:

- VLAN segmentation
- Trunking
- Access ports

### Proxmox

Responsibilities:

- VM hosting
- Infrastructure services

---

## Validation Tests

- Client receives DHCP lease
- DNS resolution working
- Inter-VLAN routing operational
- Internet access available
- Management access verified

---

## Troubleshooting Performed

### DNS SERVFAIL Issue

Problem:

Description here.

Resolution:

Description here.

---

## Skills Demonstrated

- Network Design
- VLAN Configuration
- Cisco Switching
- OPNsense Administration
- DNS Troubleshooting
- Infrastructure Documentation

---

## Future Enhancements

- Syslog
- Wazuh
- Vulnerability Scanning
- SIEM Integration
