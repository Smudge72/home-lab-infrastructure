# Active Directory Deployment and Administration

A practical Windows domain lab covering server deployment, client integration, directory administration, Group Policy and troubleshooting.

## Objective

Build a working Active Directory environment and practise the tasks involved in deploying, administering and troubleshooting Windows domain services.

This is a personal learning project, separate from my production responsibilities at work. The activities below describe the original completed build, rather than a new assessment of the lab's current state.

## Environment

| Component | Configuration |
|---|---|
| Primary virtualisation platform | Proxmox VE |
| Secondary lab platform | Microsoft Hyper-V |
| Domain controller | DC01 — Windows Server 2022 |
| Client | CLIENT01 — Windows client VM |
| Lab domain | lab.local |
| Directory services | Active Directory Domain Services and DNS |
| Administration tools | AD Users and Computers, Group Policy Management and PowerShell |

The domain name records the original lab configuration; it is not a naming recommendation for a new production environment.

## Implementation

### Domain controller and client

Installed Windows Server 2022, configured static addressing, installed Active Directory Domain Services and promoted DC01 to a domain controller with DNS.

Created CLIENT01 in Proxmox using UEFI and VirtIO storage and networking. Configured the client to use the domain controller for DNS, joined it to the domain and verified domain membership.

### Directory administration

Created organisational units for users, computers, groups and service accounts. Moved the client computer and test users into the appropriate OUs.

Practised user creation through both Active Directory Users and Computers and a PowerShell loop using `New-ADUser`. Used `Set-ADUser` to correct account attributes.

These were lab administration exercises, not a production-ready provisioning tool.

### Group Policy

Created a policy named `Workstation Baseline` and linked it at domain level.

The initial exercise configured an eight-character minimum password length and enabled password complexity. These were training settings, not a proposed production security baseline.

The build notes record successful policy application and rejection of passwords that did not meet the configured requirements.

## Troubleshooting

### Windows installer could not detect the virtual disk

**Observation:** The client installer did not display a usable disk.

**Action:** Loaded the VirtIO storage driver during installation, then installed the VirtIO guest tools after Windows setup.

**Recorded outcome:** Windows installation completed.

### Client could not contact the domain controller

**Observation:** Domain join failed with a message that the domain controller could not be contacted.

**Action:** Corrected the client's DNS configuration to use DC01. IPv6 was also disabled during the original troubleshooting session.

**Recorded outcome:** Name resolution and domain join succeeded after these changes.

**Limitation:** Two settings were changed, so the original test does not establish that IPv6 caused the failure. A follow-up test should isolate the DNS correction with IPv6 enabled rather than treating IPv6 disabling as a standard fix.

### PowerShell user creation errors

**Observation:** User-creation commands failed during the administration exercise.

**Corrections:** Fixed the spelling of `UserPrincipalName`, corrected line-continuation problems and corrected the target directory path.

**Lesson:** Check parameter names and the actual distinguished name of the target OU before repeating a bulk operation.

## Recorded Validation

| Check | Method recorded in the build |
|---|---|
| Domain name resolution | `nslookup lab.local` |
| Signed-in identity | `whoami` |
| Domain membership | `systeminfo` filtered for the Domain field |
| Group Policy processing | `gpupdate /force` and `gpresult /r` |

These checks record the original validation approach. Fresh output and dated screenshots will be added when the lab is revalidated.

## Next Validation Work

- Capture current evidence of domain membership, OU structure and applied policy.
- Re-test the domain-join scenario with IPv6 enabled, changing one variable at a time.
- Record the effective domain password policy and its enforcement separately from client policy processing.

## Skills Practised

Windows Server deployment, virtual machine configuration, Active Directory administration, DNS troubleshooting, Group Policy configuration and PowerShell-assisted user management.

[Return to the portfolio overview](../../README.md)
