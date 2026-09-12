# Network Foundation — OPNsense, VLANs and Virtualisation

A segmented home-lab network supporting Windows infrastructure, virtual machines and administration exercises.

## Objective

Build a network that separates management, client, server and experimental workloads, with OPNsense as the intended control point for communication between network segments.

The project develops practical skills in VLAN configuration, switching, firewall administration and troubleshooting across physical and virtual infrastructure.

## Lab Platforms

| Component | Role in the lab design |
|---|---|
| OPNsense firewall | VLAN interfaces, routing and network access policy |
| Cisco CBS350 managed switch | Physical connectivity, access ports and VLAN trunks |
| Proxmox VE | Virtual-machine hosting and virtual networking |
| Windows Server and Microsoft DNS | Active Directory and internal name resolution |
| Windows and Ubuntu systems | Client workloads and administration exercises |

## Verified OPNsense Interface Mapping

**Configuration review: 12 September 2026**

The following mapping was checked against screenshots of:

- **Interfaces → Devices → VLAN**
- **Interfaces → Assignments**

### Physical Interface Assignments

| Assignment | Identifier | Device |
|---|---|---|
| WAN | `wan` | `igc0` |
| LAN | `lan` | `igc1` |

### VLAN Devices and Assignments

| VLAN tag | Purpose | OPNsense description | VLAN device | Assignment | Parent |
|---|---|---|---|---|---|
| 10 | Management | `VLAN10_Management` | `vlan03` | `opt3` | `igc1` |
| 20 | Clients | `VLAN20_CLIENT` | `vlan01` | `opt1` | `igc1` |
| 30 | Servers | `VLAN30_SERVERS` | `vlan02` | `opt2` | `igc1` |
| 40 | Lab | `VLAN40_LAB` | `vlan04` | `opt4` | `igc1` |

The VLAN device names are not the VLAN tags. For example, `vlan01` carries tag **20**, not tag 1.

The physical parent `igc1` is also assigned as LAN. Its separate addressing and the switch's untagged/native VLAN configuration are not established by these two screens.

**Guest VLAN 50:** mentioned in earlier documentation, but absent from the supplied OPNsense VLAN and assignment tables. It is not included as a configured OPNsense VLAN in this inventory.

## Design Intent

The network is organised around four purposes:

| Segment | Intended use |
|---|---|
| Management | Administration of infrastructure devices |
| Clients | User-facing systems and domain-client exercises |
| Servers | Directory services and infrastructure workloads |
| Lab | Experimental systems and test workloads |

The security objective is to permit required communication between segments while restricting unnecessary access.

That objective must be checked against the actual firewall rules and traffic tests; the existence of the VLAN interfaces alone is not evidence that the intended access restrictions are enforced.

## Documentation Reconciliation

Earlier repository documents disagreed about whether VLAN 20 or VLAN 30 contained clients and servers.

The OPNsense configuration screenshots establish the mapping used here:

**VLAN 20 = Clients**  
**VLAN 30 = Servers**

This table is the reference for correcting the remaining firewall guide, network-design notes and topology documentation.

The correction is to the documentation. It does not require changing VLAN numbers or interface assignments in the lab.

## Validation Record

The original project write-up records successful DHCP lease assignment, internal and external DNS resolution, Active Directory authentication, internet connectivity, inter-VLAN communication and administrative access.

Those are retained as historical build results. The configuration review above checks the visible VLAN definitions and assignments, rather than repeating those functional tests.

| Area | Evidence status |
|---|---|
| VLAN tags, descriptions and parent interface | Checked against OPNsense configuration screenshots |
| Physical and VLAN interface assignments | Checked against OPNsense configuration screenshots |
| Switch VLAN membership, access ports and trunks | Configuration evidence to capture |
| VLAN subnets, gateway addresses and DHCP settings | Configuration evidence to capture |
| DHCP, DNS, authentication and connectivity | Success recorded in the original project; dated retest evidence to capture |
| Firewall access restrictions | Rule review and permitted/blocked traffic tests to capture |

For each functional test, record the source, destination, protocol or service, expected result and observed result.

## Troubleshooting From the Original Build

### External DNS Resolution Failure

**Problem:** Internal systems could not resolve external DNS queries.

**Investigation:** Checked client DNS configuration, internal zone resolution and DNS forwarding.

**Recorded resolution:** Corrected the DNS forwarder configuration and restored external name resolution.

### VLAN Connectivity Failure

**Problem:** Systems on different VLANs could not communicate as expected.

**Investigation:** Reviewed switch VLAN assignments, trunk configuration and firewall routing policies.

**Recorded resolution:** Corrected VLAN and routing configuration, restoring the expected communication paths.

The original notes describe the investigation and outcomes but do not preserve the exact configuration changes or test output. Future case records will include those details.

## Next Documentation Tasks

- Align the remaining network and firewall documents with the reviewed interface mapping.
- Add reviewed screenshots as supporting evidence.
- Document the addressing plan, switch-port assignments and Proxmox network configuration.
- Capture dated service tests and both permitted and blocked inter-VLAN traffic tests.

Monitoring, centralised logging and configuration-backup automation remain future development work.

## Related Projects

[Active Directory deployment and administration](../project-02-active-directory/README.md)  
[Infrastructure troubleshooting case studies](../../Troubleshooting/Issues.md)  
[PowerShell and Windows administration reference](../../Automation/PowerShell.md)

[Return to the portfolio overview](../../README.md)
