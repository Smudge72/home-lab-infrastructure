# Project 01 - Enterprise Network Foundation

## Objective

Design and implement a segmented enterprise-style network using OPNsense, Cisco switching and Proxmox virtualisation.

---

## Technologies Used

- OPNsense Firewall
- Cisco CBS350 Managed Switch
- Proxmox VE
- Microsoft Active Directory
- Microsoft DNS
- Ubuntu Server
- Windows 11
- VLAN Segmentation

---

## Network Topology

[Network Diagram To Be Added]

---

## Network Design

The environment is segmented using dedicated VLANs to separate management, user, server and lab traffic.

| VLAN | Purpose |
|--------|--------|
| VLAN 10 | Management |
| VLAN 20 | User Devices |
| VLAN 30 | Server Infrastructure |
| VLAN 40 | Testing and Lab Systems |

---

## Infrastructure Components

### OPNsense Firewall

Responsibilities:

- Default gateway services
- DHCP services
- Inter-VLAN routing
- Firewall policy enforcement
- Internet access control

### Cisco CBS350 Switch

Responsibilities:

- VLAN segmentation
- Trunk configuration
- Access port assignment
- Layer 2 switching

### Proxmox VE

Responsibilities:

- Virtual machine hosting
- Resource management
- Infrastructure platform services

### Active Directory

Responsibilities:

- Centralised authentication
- User management
- Group management
- Policy enforcement

### Microsoft DNS

Responsibilities:

- Internal name resolution
- Active Directory service discovery
- Forwarding external DNS requests

### Ubuntu Administration Server

Responsibilities:

- Linux administration practice
- User and group management
- Permission management
- System administration exercises

---

## Validation Testing

The following tests were successfully completed:

- DHCP lease assignment
- Internal DNS resolution
- External DNS resolution
- Active Directory authentication
- Internet connectivity
- Inter-VLAN communication
- Administrative access to infrastructure devices

---

## Troubleshooting Performed

### DNS Resolution Failure

Problem:

Internal systems were unable to resolve external DNS queries.

Investigation:

- Verified DNS client configuration
- Tested internal zone resolution
- Reviewed DNS forwarding configuration

Resolution:

DNS forwarder configuration was corrected and successful external name resolution was restored.

---

### VLAN Connectivity Issue

Problem:

Systems connected to different VLANs could not communicate as expected.

Investigation:

- Reviewed switch VLAN assignments
- Verified trunk configuration
- Checked firewall routing policies

Resolution:

VLAN and routing configuration were corrected, restoring expected communication paths.

---

## Skills Demonstrated

### Infrastructure Engineering

- Network design
- Virtualisation
- Active Directory administration
- DNS administration
- DHCP administration

### Networking

- VLAN configuration
- Trunking
- Layer 2 switching
- Routing concepts
- Network troubleshooting

### Security

- Network segmentation
- Firewall administration
- Access control
- Least privilege principles

### Documentation

- Technical documentation
- Change tracking
- Troubleshooting records
- Infrastructure diagrams

---

## Future Enhancements

Planned improvements include:

- Centralised logging
- Security monitoring
- Vulnerability scanning
- SIEM integration
- Configuration backup automation
- Infrastructure monitoring
- PowerShell automation
- Linux automation

---

## Repository References

Related documentation can be found within:

- Networking Documentation
- Active Directory Documentation
- Firewall Documentation
- Automation Documentation
- Troubleshooting Documentation
