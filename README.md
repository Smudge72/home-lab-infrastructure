# Home Lab Infrastructure Project

## Overview

This repository documents the design, build, and configuration of a fully functional home lab environment that simulates a small enterprise IT infrastructure.

The lab is built to replicate real-world system administration responsibilities, including virtualisation, Active Directory, networking, firewall configuration, and troubleshooting.

This project serves as both a technical learning platform and a professional portfolio demonstrating hands-on infrastructure experience.

---

## High-Level Architecture

```
                [ ISP Router ]
                      │
              [ OPNsense Firewall ]
                      │
                   [ Switch ]
                      │
              ┌────────────────────┐
              │   Proxmox Host     │
              │                    │
              │  DC01 (Server)     │
              │  CLIENT01 (Win11)  │
              │  Future VMs        │
              └────────────────────┘
```

---

## Core Technologies

* Virtualisation: Proxmox VE
* Operating Systems:

  * Windows Server 2022
  * Windows 11 Pro
* Directory Services: Active Directory Domain Services (AD DS)
* Networking: Internal virtual networks, DNS, DHCP concepts
* Firewall: OPNsense
* Automation: PowerShell (in progress)

---

## Repository Structure

```
/Active-Directory-Lab      → Domain setup, GPOs, users, permissions
/Firewall-OPNsense         → Firewall configuration and rules
/Network-Design            → IP scheme, topology, design decisions
/Troubleshooting           → Real issues encountered and fixes
/Automation-PowerShell     → Scripts and automation work
/docs                      → Detailed build documentation
/screenshots               → Visual proof of configuration
README.md                  → Project overview (this file)
```

---

## Key Features

* Deployment of Active Directory Domain Controller (DC01)
* Domain-joined Windows 11 client (CLIENT01)
* Organisational Unit (OU) design and user management
* Group Policy configuration (security and system control)
* File share with NTFS and share permissions
* OPNsense firewall setup and traffic control
* Virtual machine provisioning and management via Proxmox
* Structured troubleshooting and issue resolution logging

---

## Troubleshooting and Real-World Issues

This lab includes documented troubleshooting scenarios to reflect real IT support and infrastructure work:

* VM network connectivity failures (APIPA addressing, ARP issues)
* Hypervisor virtual switch misconfiguration
* Windows Firewall blocking traffic (ICMP issues)
* Domain join and DNS dependency problems

Each issue is documented with:

* Problem description
* Root cause analysis
* Resolution steps

---

## Skills Demonstrated

* Virtualisation (Proxmox)
* Active Directory administration
* DNS and network configuration
* Firewall configuration (OPNsense)
* Group Policy management
* File permissions and access control
* PowerShell (automation in progress)
* Structured troubleshooting methodology

---

## Screenshots

Screenshots are included in the `/screenshots` directory to demonstrate:

* Running virtual machines
* Active Directory configuration
* Group Policy settings
* Firewall interface and rules
* Successful domain joins and file access

---

## Detailed Documentation

* Active Directory build: `/Active-Directory-Lab`
* Firewall configuration: `/Firewall-OPNsense`
* Network design: `/Network-Design`
* Troubleshooting logs: `/Troubleshooting`
* Additional notes: `/docs`

---

## Project Roadmap

Planned improvements to extend the lab:

* VLAN implementation and network segmentation
* Advanced firewall rules and monitoring
* PowerShell automation for user and system management
* Additional servers (e.g. file server, monitoring tools)
* Simulated enterprise scenarios and helpdesk tickets
* Backup and disaster recovery configuration

---

## Purpose

This project is designed to:

* Reinforce hands-on infrastructure skills
* Simulate real-world IT environments
* Demonstrate practical knowledge to employers
* Support progression into system administration and infrastructure roles

---

## Author

Built and maintained as part of continuous professional development in IT infrastructure and system administration.

