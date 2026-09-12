# OPNsense — Interface Configuration and Firewall Policy

Configuration notes for the home-lab firewall, covering interface assignments, VLANs and the visible access rules.

## Review Summary

**Configuration review: 12 September 2026**

Reviewed the following OPNsense screens:

- Interfaces → Devices → VLAN
- Interfaces → Assignments
- Firewall → Rules, with All rules selected

The interface mapping is documented below. The visible client, server and lab rules provide broad IPv4 access; restrictive inter-VLAN policy remains a hardening task.

This review records configuration rather than end-to-end traffic-test results. No firewall settings were changed during this documentation update.

## Interface Configuration

### Physical Interfaces

| Assignment | Device |
|---|---|
| WAN | `igc0` |
| LAN | `igc1` |

### VLAN Interfaces

All four VLAN devices use `igc1` as their parent.

| VLAN | Purpose | Description | Device | Assignment |
|---|---|---|---|---|
| 10 | Management | `VLAN10_Management` | `vlan03` | `opt3` |
| 20 | Clients | `VLAN20_CLIENT` | `vlan01` | `opt1` |
| 30 | Servers | `VLAN30_SERVERS` | `vlan02` | `opt2` |
| 40 | Lab | `VLAN40_LAB` | `vlan04` | `opt4` |

The parent interface `igc1` also has a separate LAN assignment. Its addressing and the switch's untagged/native VLAN configuration require a separate check.

VLAN 50 appeared in earlier planning notes but is not present in the reviewed VLAN or assignment tables.

The [network foundation project](../projects/project-01-network-foundation/README.md) contains the wider network design and validation record.

## Visible Firewall Rules

The expanded Interface rules section shows six entries.

All six display the Pass action. Protocol, source port, destination and destination port are shown as `*`, meaning no restriction in those displayed fields.

| Interface | IP version | Source | Destination | Protocol / ports | Visible entries |
|---|---|---|---|---|---|
| LAN | IPv4 | LAN network | Any | Any | 1 |
| LAN | IPv6 | LAN network | Any | Any | 1 |
| VLAN20_CLIENT | IPv4 | VLAN20_CLIENT network | Any | Any | 1 |
| VLAN30_SERVERS | IPv4 | VLAN30_SERVERS network | Any | Any | 1 |
| VLAN40_LAB | IPv4 | VLAN40_LAB network | Any | Any | 2 |

The LAN entries have default allow-rule descriptions. The visible client, server and lab entries do not have descriptions.

### What This Policy Means

The visible VLAN rules are broad source-network-to-any permissions. They do not limit access to specific infrastructure services or to internet destinations.

An Any destination can include internal networks. OPNsense's default-deny behaviour applies when no permitting rule applies; it does not override a matching pass rule.

Actual connectivity also depends on the complete ruleset, routing and destination systems.

**Current position: VLAN interfaces are configured, but the reviewed rules do not demonstrate least-privilege inter-VLAN isolation.**

Reference: [OPNsense firewall rules documentation](https://docs.opnsense.org/manual/firewall.html).

## Findings to Carry Forward

| Finding | Follow-up |
|---|---|
| Broad IPv4 permissions on Clients, Servers and Lab | Define required traffic flows before replacing broad access with narrower rules |
| Two VLAN40 entries with identical displayed fields | Compare full rule settings and purpose before deciding whether one is redundant |
| Missing descriptions on the visible VLAN rules | Add meaningful purpose statements during a controlled rule-maintenance change |
| No VLAN10-specific entry visible in the expanded interface section | Review the complete applicable rules and confirm the management access path |
| A separate LAN IPv6 allow rule is visible | Include IPv6 addressing and policy in the review rather than assuming an IPv4 review covers it |

The automatically generated rules were collapsed in the supplied screenshot. Their contents were not reviewed.

The absence of a visible VLAN10 entry is not proof that management traffic is blocked. Likewise, this screenshot alone does not establish whether services are exposed through WAN.

## Planned Hardening and Validation

The next engineering task is to turn the required communication paths into a documented access policy.

Before changing rules, preserve a private configuration backup and confirm a recovery path that does not depend solely on the connection being changed.

Document which systems need access to directory services, DNS, administration interfaces and other lab services. Use those requirements to plan narrower permissions.

Apply changes in small, reversible steps. Check required services still work and verify that traffic intended to be blocked actually fails.

| Test record | Information to capture |
|---|---|
| Source | Device and network initiating the connection |
| Destination | Target device or service |
| Traffic | Protocol and destination port, where applicable |
| Expected result | Allow or deny |
| Observed result | Actual test outcome |
| Supporting evidence | Relevant rule, log entry or diagnostic output |
| Change record | Date, configuration change and rollback approach |

These are planned tasks, not completed controls or test results.

Configuration exports should remain private rather than being committed to this public repository.

## Other Configuration Still to Document

The reviewed screens do not establish VLAN subnet addresses, gateway addresses, DHCP scopes, DNS forwarding, NAT settings or the operating mode of the upstream router.

Those details will be captured from the relevant configuration screens rather than copied from earlier planning assumptions.

## Related Documentation

[Network foundation project](../projects/project-01-network-foundation/README.md)  
[Active Directory project](../projects/project-02-active-directory/README.md)  
[Troubleshooting case studies](../Troubleshooting/Issues.md)

[Return to the portfolio overview](../README.md)
