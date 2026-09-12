# Infrastructure Troubleshooting Case Studies

Practical examples of problems encountered while building the lab, the changes made and the outcomes recorded.

These cases come from the [original build log](../Network-Design/Build-Log.md). They describe the original build rather than a fresh assessment of the current environment.

## Case Index

| Case | Area | Recorded status |
|---|---|---|
| [01 — Proxmox connectivity](#01--proxmox-connectivity) | Physical connectivity and hypervisor access | Connectivity restored after changing to Ethernet |
| [02 — Unexpected APIPA addressing](#02--unexpected-apipa-addressing) | IP addressing and DHCP investigation | Static-address workaround applied; DHCP cause unresolved in the notes |
| [03 — Windows ping failure](#03--windows-ping-failure) | Connectivity testing and host firewall rules | ICMP echo rule change recorded as the resolution |

For domain-join, VirtIO storage-driver and PowerShell troubleshooting, see the [Active Directory project](../projects/project-02-active-directory/README.md#troubleshooting).

---

## 01 — Proxmox Connectivity

### Problem

Connectivity problems occurred during the Proxmox build while using a Wi-Fi connection.

### Action Taken

Changed the connection from Wi-Fi to Ethernet and used a ping check to verify connectivity.

### Recorded Outcome

The build log records that switching to Ethernet resolved the connectivity issue.

The notes do not preserve enough information about the original network path to establish the precise underlying cause.

### Lesson Learned

Start by establishing the actual connection path before changing services or virtual-machine settings.

In this case, changing the physical connection restored connectivity. A stronger troubleshooting record would also capture the relevant interface settings and the results before and after the change.

---

## 02 — Unexpected APIPA Addressing

### Problem

A Windows system had a `169.254.x.x` address instead of the expected lab address.

The original build notes describe this as a DHCP issue.

### Action Taken

Assigned static IP addresses so that the lab build could continue.

### Recorded Outcome

Static addressing was used as a workaround. The wider build subsequently records working connectivity between lab systems.

The notes do not identify why the expected DHCP address was not obtained or record a successful DHCP retest.

**Status: workaround applied; DHCP root cause not established in the original record.**

### Lesson Learned

Keep service restoration separate from root-cause resolution.

The static configuration allowed progress, but it did not demonstrate that DHCP had been repaired. The outstanding investigation should remain visible rather than being marked as a completed DHCP fix.

---

## 03 — Windows Ping Failure

### Problem

Ping tests failed during connectivity checks between lab systems.

### Action Taken

The build notes identify the Windows firewall as blocking ICMP and record enabling ICMP echo rules.

### Recorded Outcome

The ICMP rule change is recorded as the resolution.

The original notes do not include the exact rule configuration or before-and-after test output.

### Lesson Learned

Investigate the specific traffic being tested rather than treating a failed ping as proof that every network service is unavailable.

For a repeatable record, document the source, destination, relevant firewall rule and result of the same test after the change.

---

## Evidence to Capture During Revalidation

The original notes preserve the actions and reported outcomes. The next documentation improvement is to attach dated evidence to each case.

| Case | Evidence to capture |
|---|---|
| Proxmox connectivity | Relevant connection path, interface configuration, management access and connectivity-test results |
| APIPA addressing | Client configuration, intended DHCP service and network segment, investigation findings and the outcome of a controlled DHCP retest |
| Windows ping failure | Source and destination, active firewall profile, applicable ICMP rule and repeat-test output |

These are planned evidence-capture tasks, not tests claimed as completed.

Any published screenshots or output should be reviewed for credentials, personal information and unrelated systems.

## Troubleshooting Record Standard

For future incidents, capture:

**Symptom → Evidence → Hypothesis → Change → Repeat Test → Outcome**

Record unsuccessful tests as well as successful changes. Distinguish a confirmed cause from a working hypothesis, and a workaround from a permanent resolution.

## Related Documentation

[Active Directory deployment and administration](../projects/project-02-active-directory/README.md)  
[Original build log](../Network-Design/Build-Log.md)  
[PowerShell command reference](../Automation/PowerShell.md)

[Return to the portfolio overview](../README.md)
