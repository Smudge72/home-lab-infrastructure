# Network Design

## VLANs

| VLAN | Name     | Subnet           | Purpose              |
|------|----------|------------------|----------------------|
| 10   | MGMT     | 192.168.10.0/24  | Network management   |
| 20   | SERVERS  | 192.168.20.0/24  | AD, services         |
| 30   | CLIENTS  | 192.168.30.0/24  | User machines        |
| 40   | LAB      | 192.168.40.0/24  | Testing environment  |
| 50   | GUEST    | 192.168.50.0/24  | Isolated internet    |
| 60   | IOT      | 192.168.60.0/24  | Devices              |

---

## Core Components

- Firewall (OPNsense)
- Cisco CBS350 Switch
- Proxmox Host
- Windows Server (Domain Controller)

---

## Design Goals

- Segmented network using VLANs
- Controlled inter-VLAN routing via firewall
- Secure separation of lab, client, and guest traffic