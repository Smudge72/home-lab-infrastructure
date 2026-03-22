# OPNsense Setup

OPNsense is used as the primary firewall and inter-VLAN router for the home lab. It sits between the ISP router (operating in upstream/bridge mode) and the Cisco CBS350 managed switch.

---

## Hardware

- CWWK N97 Firewall Appliance
- WAN interface: connected to ISP Router (upstream/bridge mode)
- LAN interface: trunk link to Cisco CBS350 Switch (carries VLANs 10, 20, 30, 40 & 50)

---

## Initial Installation

1. Download the latest OPNsense AMD64 ISO from [opnsense.org](https://opnsense.org/download/)
2. Write the ISO to a USB drive using Balena Etcher or Rufus
3. Boot the appliance from USB and follow the installer
4. Set the root password during installation
5. After reboot, assign interfaces via the console menu:
   - WAN → physical interface connected to ISP router
   - LAN → physical interface connected to Cisco switch

---

## VLAN Configuration

Create VLAN sub-interfaces on the LAN interface for each VLAN:

| VLAN | Name     | Interface Tag (example) | LAN IP (gateway) |
|------|----------|-------------------------|------------------|
| 10   | MGMT     | `<iface>`.10            | 192.168.10.1/24  |
| 20   | SERVERS  | `<iface>`.20            | 192.168.20.1/24  |
| 30   | CLIENTS  | `<iface>`.30            | 192.168.30.1/24  |
| 40   | LAB      | `<iface>`.40            | 192.168.40.1/24  |
| 50   | GUEST    | `<iface>`.50            | 192.168.50.1/24  |

> **Note:** Replace `<iface>` with the actual LAN interface name detected during installation (e.g. `igb0`, `em0`, `vtnet0`). Check **Interfaces → Assignments** in the OPNsense UI to confirm the correct name.

**Steps (Interfaces → Other Types → VLAN):**
1. Select the parent LAN interface
2. Set the VLAN tag (10, 20, 30, 40, 50)
3. Assign each VLAN as a new interface and enable it
4. Set the gateway IP for each interface (e.g. 192.168.10.1/24 for VLAN 10)

---

## Firewall Rules (Inter-VLAN)

Inter-VLAN routing is enforced by OPNsense. Default policy: **deny all inter-VLAN traffic** unless explicitly permitted.

| Source VLAN | Destination     | Action | Notes                                  |
|-------------|-----------------|--------|----------------------------------------|
| MGMT (10)   | Any             | Allow  | Full management access                 |
| SERVERS (20)| CLIENTS (30)    | Allow  | Servers can reach clients              |
| CLIENTS (30)| SERVERS (20)    | Allow  | Clients can reach servers              |
| CLIENTS (30)| WAN             | Allow  | Internet access                        |
| LAB (40)    | LAB (40)        | Allow  | Isolated lab traffic only              |
| LAB (40)    | WAN             | Allow  | Internet access for lab                |
| GUEST (50)  | WAN             | Allow  | Internet access only                   |
| GUEST (50)  | Any VLAN        | Block  | No access to internal VLANs            |
| Any         | Any             | Block  | Default deny                           |

---

## DHCP

Enable DHCP server on each VLAN interface:

| VLAN | Subnet           | DHCP Range                      |
|------|------------------|---------------------------------|
| 10   | 192.168.10.0/24  | 192.168.10.100 – 192.168.10.200 |
| 20   | 192.168.20.0/24  | 192.168.20.100 – 192.168.20.200 |
| 30   | 192.168.30.0/24  | 192.168.30.100 – 192.168.30.200 |
| 40   | 192.168.40.0/24  | 192.168.40.100 – 192.168.40.200 |
| 50   | 192.168.50.0/24  | 192.168.50.100 – 192.168.50.200 |

---

## DNS

- OPNsense Unbound DNS resolver enabled
- DNS forwarding to upstream resolver (e.g. 1.1.1.1, 8.8.8.8)
- Local domain: `lab.local`

---

## Status

- [ ] Hardware received and OPNsense installed
- [ ] Interfaces assigned (WAN/LAN)
- [ ] VLAN sub-interfaces created
- [ ] Firewall rules configured
- [ ] DHCP enabled on all VLANs
- [ ] DNS resolver configured

## Interface Mapping

- igc0 → WAN (connected to ISP router)
- igc1 → LAN (trunk to Cisco switch)

---

## VLAN Configuration

- VLAN 10 – Management
- VLAN 20 – Servers
- VLAN 30 – Clients
- VLAN 40 – Lab
- VLAN 50 – Guest

---

## Design Approach

Inter-VLAN routing is handled by the firewall to enforce security policies between network segments.

Default deny rules are applied between VLANs, with explicit allow rules configured where required.
