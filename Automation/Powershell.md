# PowerShell Commands – Active Directory Lab

## Overview

This document contains all PowerShell commands used during the setup, configuration, troubleshooting, and security testing of the Active Directory lab.

---

## Active Directory Module

Import Active Directory module:

```powershell
Import-Module ActiveDirectory
```

---

## Bulk User Creation

```powershell
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

## Modify User Attributes

Update User Principal Name and SamAccountName:

```powershell
Set-ADUser sbrown -UserPrincipalName abrown@lab.local
Set-ADUser sbrown -SamAccountName abrown
```

---

## Query Active Directory Users

List all users:

```powershell
Get-ADUser -Filter * | Select Name
```

Get specific user:

```powershell
Get-ADUser -Identity abrown
```

Check if account is enabled:

```powershell
Get-ADUser abrown -Properties Enabled
```

---

## Reset User Password (Delegation Scenario)

```powershell
Set-ADAccountPassword -Identity finance -Reset -NewPassword (ConvertTo-SecureString "NewPassword123!" -AsPlainText -Force)
```

---

## Group Policy Commands

Force Group Policy update:

```powershell
gpupdate /force
```

View applied Group Policy:

```powershell
gpresult /r
```

---

## Network Troubleshooting

View full IP configuration:

```powershell
ipconfig /all
```

Test connectivity:

```powershell
ping 192.168.1.10
```

DNS lookup:

```powershell
nslookup lab.local
```

Flush DNS cache:

```powershell
ipconfig /flushdns
```

---

## Time Synchronisation (Kerberos Fix)

Force time resync:

```powershell
w32tm /resync
```

Restart time service:

```powershell
net stop w32time
net start w32time
```

Check time source:

```powershell
w32tm /query /status
```

Set domain hierarchy sync:

```powershell
w32tm /config /syncfromflags:domhier /update
```

---

## System & Identity Checks

Check current user:

```powershell
whoami
```

Check group membership:

```powershell
whoami /groups
```

Check machine name:

```powershell
hostname
```

---

## Service Management

Check Windows Search service:

```powershell
Get-Service WSearch
```

---

## RSAT Installation (Client Management Tools)

Install Active Directory tools:

```powershell
Get-WindowsCapability -Name RSAT* -Online | Where-Object Name -like "*ActiveDirectory*" | Add-WindowsCapability -Online
```

---

## Running CMD from PowerShell

Open Command Prompt:

```powershell
cmd
```

Run as admin:

```powershell
Start-Process cmd -Verb runAs
```

---

## Shutdown Commands

Shutdown machine:

```powershell
shutdown /s /t 0
```

Restart machine:

```powershell
shutdown /r /t 0
```

Log off:

```powershell
shutdown /l
```

---

## Key Takeaways

* PowerShell enables automation of Active Directory tasks
* Small syntax errors can break execution
* DNS and time synchronisation are critical for AD functionality
* Delegated permissions can be abused if misconfigured
* Administrative tools (RSAT) allow remote management of AD
