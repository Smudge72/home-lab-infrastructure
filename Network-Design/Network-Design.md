m# Network Design

See [Diagram.md](Diagram.md) for the full network topology diagram.

---

## VLANs

| VLAN | Name     | Subnet           | Purpose                        | Key Devices        |
|------|----------|------------------|--------------------------------|--------------------|
| 10   | MGMT     | Redacted         | Network management             |                    |
| 20   | SERVERS  | Redacted         | Virtualisation & services      | Proxmox            |
| 30   | CLIENTS  | Redacted         | User machines                  | Main PC            |
| 40   | LAB      | Redacted         | Testing environment            |                    |
| 50   | GUEST    | Redacted         | Isolated internet access       |                    |

---

## Core Components

- Firewall (OPNsense) — inter-VLAN routing & firewall rules enforced here
- Cisco CBS350 Switch — trunk ports carrying VLANs 10, 20, 30, 40 & 50
- ISP Router (Upstream/Bridge)
- Proxmox Host
- Windows Server (Domain Controller)

---

## Design Goals

- Segmented network using VLANs
- Controlled inter-VLAN routing via firewall
- Secure separation of lab, client, and guest traffic

---

## IP Addressing Scheme

| Device        | IP Address        |
|---------------|-------------------|
| Firewall      | Redacted          |
| Proxmox Host  | Redacted          |
| Domain Ctrl   | Redacted          |

---

## Design Decisions

- VLAN segmentation implemented to isolate traffic between user, server, and guest networks
- Firewall used for all inter-VLAN routing to enforce security policies
- Dedicated management VLAN for infrastructure devices
- ISP router operates in upstream/bridge mode; all routing handled by OPNSense

## Design Decisions

- Firewall used as central routing point to maintain visibility and control
- VLAN segmentation implemented to reduce risk of lateral movement
- Separate client and server networks to enforce access control
