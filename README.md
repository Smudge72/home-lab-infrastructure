# Enterprise Infrastructure & Security Homelab

## Overview

This repository documents the design, deployment, administration and troubleshooting of a multi-platform enterprise-style homelab.

The environment has been built to develop and demonstrate practical skills in:

* Infrastructure Engineering
* Network Engineering
* Systems Administration
* Linux Administration
* Active Directory
* Virtualisation
* Cyber Security
* PowerShell Automation

The objective is to gain hands-on experience with technologies commonly found in enterprise environments while creating a professional portfolio of documented projects and troubleshooting activities.

---

## Core Technologies

### Infrastructure

* Proxmox VE
* Windows Server
* Windows 11
* Ubuntu Server

### Networking

* Cisco CBS350 Managed Switch
* VLAN Segmentation
* DHCP
* DNS
* Routing and Switching

### Security

* OPNsense Firewall
* Network Segmentation
* Access Control
* Security Hardening

### Administration

* Active Directory Domain Services
* Group Policy
* PowerShell
* Git & GitHub

---

## Current Lab Architecture

### Virtualisation Platform

**Proxmox VE**

Provides the core virtualisation platform hosting Windows and Linux workloads used throughout the lab.

### Network Infrastructure

**Cisco CBS350 Managed Switch**

Configured to support:

* Access Ports
* Trunk Ports
* VLAN Segmentation
* Inter-device Connectivity

### Firewall Platform

**OPNsense**

Configured to provide:

* Routing
* DHCP Services
* VLAN Interfaces
* DNS Forwarding
* Firewall Policy Management

### Active Directory Environment

**Domain Services**

* Active Directory Domain Services
* Microsoft DNS
* Organisational Units
* Security Groups
* Group Policy Management

### Linux Environment

**Ubuntu Server 24.04**

Configured for:

* User and Group Administration
* Linux File Permissions
* DNS Configuration
* Network Troubleshooting
* Package Management
* SSH Administration

---

## Skills Demonstrated

### Infrastructure

* Virtual Machine Deployment
* Hypervisor Administration
* System Configuration
* Backup and Snapshot Management

### Networking

* VLAN Design
* Switch Configuration
* Trunking
* DHCP Troubleshooting
* DNS Troubleshooting
* Network Connectivity Analysis

### Windows Administration

* Active Directory Deployment
* User Management
* Group Management
* OU Design
* Group Policy Configuration
* DNS Administration

### Linux Administration

* User and Group Management
* File Permissions
* Package Management
* Network Configuration
* DNS Configuration
* Command Line Administration

### Security

* Firewall Configuration
* Network Segmentation
* Access Control
* Principle of Least Privilege

### Automation

* PowerShell Scripting
* Active Directory Automation
* Administrative Task Automation

---

## Troubleshooting Methodology

A major focus of this lab is developing structured troubleshooting skills.

Typical workflow:

1. Identify the issue
2. Gather evidence
3. Isolate potential causes
4. Test assumptions
5. Implement a fix
6. Validate functionality
7. Document findings

---

## Example Troubleshooting Scenarios

### Active Directory DNS Resolution

Issue:

* Domain resources unavailable
* Name resolution failures

Investigation:

* DNS configuration review
* SRV record validation
* Forwarder verification
* Client DNS testing

Resolution:

* Corrected DNS configuration
* Validated AD-integrated DNS functionality
* Confirmed internal and external name resolution

### VLAN Connectivity Investigation

Issue:

* Virtual machine unable to obtain expected network connectivity

Investigation:

* Proxmox VLAN tagging
* Cisco switch VLAN membership
* Trunk configuration
* DHCP scope validation
* Firewall interface verification

Resolution:

* Corrected network configuration
* Validated VLAN operation
* Confirmed end-to-end connectivity

---

## Repository Structure

```text
active-directory/
Automation/
docs/
Firewall/
Network-Design/
Troubleshooting/
screenshots/
```

---

## Current Learning Focus

* Cisco CCNA
* Linux Administration
* Infrastructure Engineering
* Security Engineering
* PowerShell Automation
* Enterprise Troubleshooting

---

## Future Development

Planned additions include:

* Advanced VLAN Architecture
* Network Monitoring
* Centralised Logging
* Vulnerability Assessment
* Security Information and Event Management (SIEM)
* Wazuh Deployment
* Security Automation
* Infrastructure as Code

---

## Professional Objective

This homelab is maintained as a practical learning environment and technical portfolio to support progression into Infrastructure Engineering and Cyber Security Engineering roles.
