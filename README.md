# Infrastructure & Systems Administration Homelab

Hands-on projects in Windows infrastructure, virtualisation, networking and troubleshooting.

## About This Lab

I am a second-line IT administrator developing my skills for progression into infrastructure engineering and systems administration.

This repository documents my personal lab: what I built, how I configured it, the problems I encountered and how I checked the results.

The focus is practical understanding, not just getting through an installation. Each project aims to explain the decisions, troubleshooting and lessons behind the finished configuration.

This is a personal learning environment, separate from my production responsibilities at work.

## Start Here

| Project | What it covers | Documentation status |
|---|---|---|
| [Active Directory Deployment and Administration](projects/project-02-active-directory/README.md) | Windows Server, domain-controller deployment, client domain join, organisational units, Group Policy and user administration | Original build documented; fresh validation evidence pending |
| [Network Foundation](projects/project-01-network-foundation/README.md) | OPNsense, Cisco switching, Proxmox networking and VLAN segmentation | Existing project write-up; network records being reconciled |
| [PowerShell Command Reference](Automation/PowerShell.md) | Commands and examples from Active Directory administration and troubleshooting exercises | Reference material, not a production-ready automation tool |

**Recommended starting point:** the Active Directory project contains the most complete account of implementation, troubleshooting and recorded validation.

## Active Directory Project Highlights

The documented build includes:

- Deploying Windows Server 2022 as a domain controller with DNS.
- Configuring and joining a Windows client to the lab domain.
- Creating organisational units and managing test users through AD Users and Computers and PowerShell.
- Configuring Group Policy and recording policy-processing checks.

The project also explains where the original evidence is limited and what needs to be re-tested.

## Troubleshooting Examples

| Problem | Action taken | Recorded result |
|---|---|---|
| Windows installer could not detect the virtual disk | Loaded the VirtIO storage driver during installation | Windows installation completed |
| Client could not contact the domain controller | Corrected client DNS settings; IPv6 was also disabled during the original investigation | Domain join succeeded, but the separate effect of each change was not established |
| PowerShell user-creation commands failed | Corrected parameter spelling, line continuation and the target directory path | Corrections documented in the administration exercise |

See the [Active Directory case study](projects/project-02-active-directory/README.md#troubleshooting) for the context and limitations of these findings.

## Lab Platforms

The documented environment brings together:

| Area | Platforms and technologies |
|---|---|
| Virtualisation | Proxmox VE and Microsoft Hyper-V |
| Windows infrastructure | Windows Server, Windows clients, Active Directory Domain Services, DNS and Group Policy |
| Networking | Cisco CBS350 switching, OPNsense, VLANs and DHCP |
| Administration | PowerShell and Windows administration tools |

The lab has evolved over time. Individual project pages distinguish the original build from current validation and planned work.

## Supporting Build Records

The [original build log](Network-Design/Build-Log.md) and [hardware rebuild notes](Network-Design/Hardware-Builds.md) preserve earlier stages of the project.

These are historical working records. Some sections describe earlier configurations or plans and are being organised into clearer project documentation.

## Documentation Approach

The standard I am working towards for each project is:

**Objective → Configuration → Troubleshooting → Validation → Lessons learned**

A successful workaround is not automatically a confirmed root-cause fix. Where the original testing did not isolate the cause, the documentation states that rather than presenting an assumption as a proven result.

## Current Improvements

- Reconcile the network diagram, VLAN assignments and firewall documentation.
- Add dated screenshots and command output to support the completed exercises.
- Organise troubleshooting records into individual case studies.
- Develop and test a standalone PowerShell administration script.

Monitoring, centralised logging and further security exercises are future additions, not completed capabilities.
