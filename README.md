# Active Directory Home Lab (Proxmox & Hyper-V)

## Overview

This project documents the design, deployment, and management of a fully functional Active Directory lab environment.

The lab was built across two platforms:

* **Primary Environment:** Proxmox (bare-metal hypervisor)
* **Secondary Environment:** Hyper-V (workstation-based)

The goal was to simulate real-world enterprise infrastructure while developing practical skills in system administration and foundational security.

---

## Host Environments

### Primary Host (Proxmox)

* Platform: Proxmox VE
* Type: Bare-metal (Type 1 hypervisor)
* Purpose: Core lab environment

#### Networking

* Bridge: vmbr0 (bridged)
* Allows:

  * VM-to-VM communication
  * Access to local network and internet
  * Realistic enterprise-style networking

---

### Secondary Host (Hyper-V)

* Platform: Microsoft Hyper-V (Alienware workstation)
* Type: Type 1 hypervisor (hosted on Windows)
* Purpose: Testing and rapid iteration

#### Use Cases

* Quick VM deployment
* Testing configurations before Proxmox rollout
* Comparing behaviour across hypervisors

---

## Lab Architecture

| Role              | Hostname | OS                  | IP Address   |
| ----------------- | -------- | ------------------- | ------------ |
| Domain Controller | DC01     | Windows Server 2022 | 192.168.1.10 |
| Client Machine    | CLIENT01 | Windows 10/11       | 192.168.1.50 |

---

## Build Process

### 1. Domain Controller Deployment

* Installed Windows Server 2022
* Configured static IP
* Installed AD DS role
* Promoted to Domain Controller

Configuration:

* Forest: lab.local
* DNS: Installed and configured automatically

---

### 2. Client VM Deployment

* Created CLIENT01 in Proxmox
* Configured:

  * Machine: q35
  * BIOS: OVMF (UEFI)
  * Disk: VirtIO SCSI
  * Network: VirtIO

---

### 3. Windows Installation Issues (Resolved)

Issue:

* No disk detected during installation

Fix:

* Loaded VirtIO driver:
  vioscsi → w10 → amd64

Post-install:

* Installed virtio-win-guest-tools.exe

---

### 4. Network Configuration

Configured static IP on CLIENT01:

* IP Address: 192.168.1.50
* Subnet Mask: 255.255.255.0
* Gateway: 192.168.1.1
* DNS Server: 192.168.1.10 (Domain Controller)

---

### 5. Domain Join (Troubleshooting)

Issue:

* "Active Directory Domain Controller could not be contacted"

Root Cause:

* DNS misconfiguration
* IPv6 taking priority

Fix:

* Disabled IPv6
* Set DNS to DC only

Validation:

* ping <DC-IP>
* nslookup lab.local

---

### 6. Domain Join

* Joined CLIENT01 to lab.local
* Restarted system

Verification:

* whoami
* systeminfo | findstr /B /C:"Domain"

---

## Active Directory Configuration

### Organizational Unit Structure

Created:

* Users
* Computers
* Groups
* Service Accounts

Actions:

* Moved CLIENT01 → Computers OU
* Moved users → Users OU

---

### User Management

#### Manual Creation

* Created initial test users in ADUC

#### PowerShell Automation

```powershell
Import-Module ActiveDirectory

$users = @(
    @{Name="Alice Brown"; Sam="abrown"},
    @{Name="Tom White"; Sam="twhite"},
    @{Name="Emma Green"; Sam="egreen"}
)

foreach ($user in $users) {
    New-ADUser -Name $user.Name `
        -SamAccountName $user.Sam `
        -UserPrincipalName "$($user.Sam)@lab.local" `
        -Path "OU=Users,DC=lab,DC=local" `
        -AccountPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force) `
        -Enabled $true
}
```

---

### Troubleshooting (PowerShell)

Issues encountered:

* Incorrect parameter:
  UserPrincipleName → corrected to UserPrincipalName

* Line continuation errors:
  Caused parameters like -Enabled to fail

* OU path issues:
  OU vs CN confusion

---

### User Attribute Correction

```powershell
Set-ADUser sbrown -UserPrincipalName abrown@lab.local
Set-ADUser sbrown -SamAccountName abrown
```

---

## Group Policy

### GPO Creation

* Name: Workstation Baseline
* Created using Group Policy Management (gpmc.msc)

---

### Configuration

Path:

Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Account Policies
→ Password Policy

Settings applied:

* Minimum password length = 8
* Password complexity = Enabled

---

### Linking

* Linked at domain level: lab.local

---

### Deployment & Verification

On CLIENT01:

```powershell
gpupdate /force
gpresult /r
```

Validation:

* GPO applied successfully
* Weak passwords rejected

---

## Key Lessons Learned

* DNS is critical for Active Directory functionality
* Incorrect DNS prevents domain join
* IPv6 can interfere in lab environments
* OU structure is essential for scalability
* PowerShell syntax must be exact
* GPO scope determines effectiveness

---

## Skills Demonstrated

* Active Directory deployment and management
* DNS troubleshooting and resolution
* Virtualisation using Proxmox and Hyper-V
* Windows client/server integration
* PowerShell automation
* Group Policy configuration and enforcement
* Structured troubleshooting methodology

---

## Next Steps

* Implement role-based access control (RBAC)
* Expand Group Policy configurations
* Introduce security misconfigurations
* Simulate privilege escalation scenarios
* Add monitoring and logging

---

## Summary

This lab demonstrates the ability to design, build, troubleshoot, and manage a Windows domain environment across multiple virtualisation platforms, reflecting real-world system administration and security practices.

