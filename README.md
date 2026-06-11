# Home Lab Infrastructure

## Overview

This repository documents the design, deployment, troubleshooting and ongoing development of a personal enterprise-style IT infrastructure home lab.

The purpose of this lab is to develop practical skills in infrastructure support, networking, systems administration, security engineering and technical documentation.

This project demonstrates hands-on experience with:

- Active Directory
- Windows Server
- DNS
- Group Policy
- Proxmox VE
- OPNsense Firewall
- Cisco CBS350 Managed Switching
- VLANs and network segmentation
- Ubuntu Server
- PowerShell automation
- Nmap and Wireshark
- Technical documentation

---

## Lab Goals

- Build a realistic enterprise-style infrastructure environment
- Practise 2nd/3rd line troubleshooting
- Develop networking and infrastructure engineering skills
- Improve security awareness through segmentation, access control and firewall rules
- Create professional documentation suitable for an employer-facing technical portfolio

---

## Current Lab Components

| Component | Purpose |
|---|---|
| OPNsense Firewall | Routing, firewalling, DHCP and network segmentation |
| Cisco CBS350 Managed Switch | VLANs, trunking and access port configuration |
| Proxmox VE | Virtualisation platform for lab servers and clients |
| Windows Server | Active Directory, DNS and Group Policy |
| Windows Client | Domain-joined endpoint testing |
| Ubuntu Server | Linux administration and service testing |
| Kali Linux | Security testing and network analysis |

---

## Network Design

The lab uses segmented VLANs to separate management, user, server and test environments.

| VLAN | Purpose |
|---|---|
| VLAN 10 | Management |
| VLAN 20 | Users |
| VLAN 30 | Servers |
| VLAN 40 | Lab / Testing |

IP addressing has been intentionally redacted from public documentation.

---

## Skills Demonstrated

### Infrastructure

- Windows Server administration
- Active Directory Domain Services
- DNS configuration and troubleshooting
- Group Policy configuration
- Virtual machine deployment and management
- Snapshot and recovery planning

### Networking

- VLAN design and segmentation
- Trunk and access port configuration
- DHCP troubleshooting
- DNS and name resolution troubleshooting
- Inter-VLAN routing concepts
- Cisco managed switch administration
- Firewall rule design using OPNsense

### Security

- Network segmentation
- Role-based access control
- Firewall rule management
- Endpoint and identity security awareness
- Vulnerability discovery using Nmap
- Packet analysis using Wireshark
- Cyber Essentials-aligned security principles

### Automation & Documentation

- PowerShell scripting for administration and reporting
- GitHub-based technical documentation
- Structured troubleshooting notes
- Professional network diagrams using draw.io

---

## Repository Structure

```text
Automation/
Firewall/
Network-Design/
Troubleshooting/
active-directory/
docs/Diagrams/
projects/project-01-network-foundation/
screenshots/
