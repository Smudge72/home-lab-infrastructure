# PowerShell & Windows Administration Reference

A task-based reference covering Active Directory administration, identity checks, network diagnostics and Group Policy.

## Purpose

The original lab exercises used PowerShell to query users, create test accounts and correct account attributes. Windows command-line tools supported connectivity, policy and time-service checks.

This page organises those activities into a practical reference. The account-creation and password-reset examples have been revised for safer handling and still require lab testing.

This is a collection of separate examples, not a single script to run from start to finish.

## Before Using the Examples

Use an authorised lab administration machine with the Active Directory PowerShell module available.

The domain, server, OU and account names below reflect the original lab examples. Verify them against the current environment before running any commands.

Start with read-only checks. The account-change examples retain `-WhatIf`, which previews the intended operation without applying that change. A preview does not prove that a real operation will pass every permissions or policy check.

---

## 1. Identity and Diagnostic Checks

These commands inspect the current environment without changing its configuration.

| Command | Purpose |
|---|---|
| `hostname` | Identify the machine being used |
| `whoami` | Identify the current user context |
| `whoami /groups` | Inspect group information in the current security token |
| `ipconfig /all` | Inspect interface addressing, DNS configuration and DHCP information |
| `nslookup lab.local` | Query DNS for the original lab domain |
| `gpresult /r` | Display a summary of Resultant Set of Policy information |
| `w32tm /query /status` | Inspect Windows Time service status and its reported time source |

These are Windows command-line utilities that can be run from PowerShell; they are not PowerShell cmdlets.

Record the machine, user context and relevant output when using them in a troubleshooting case.

References: [Microsoft gpresult documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/gpresult) and [Windows Time service tools](https://learn.microsoft.com/en-us/windows-server/networking/windows-time-service/windows-time-service-tools-and-settings).

## 2. Query Active Directory Users

Load the module, select the lab domain controller and inspect a sample account:

```powershell
Import-Module ActiveDirectory -ErrorAction Stop

$server = 'DC01.lab.local'

Get-ADUser -Identity 'abrown' -Server $server -ErrorAction Stop |
    Select-Object Name, SamAccountName, UserPrincipalName,
        Enabled, DistinguishedName
```

This retrieves account information; it does not change the user.

Use the distinguished name to check where the account is located rather than assuming it is in the intended OU.

Reference: [Microsoft Get-ADUser documentation](https://learn.microsoft.com/en-us/powershell/module/activedirectory/get-aduser).

---

## 3. Account Creation Exercise — Revised Preview

The original exercise created three sample users using a loop.

This revised version checks the target OU, skips existing account names and previews the creation of disabled accounts. Password assignment and account enablement are deliberately separate tasks.

**Validation status:** revised reference example; not yet re-tested in the lab.

```powershell
try {
    Import-Module ActiveDirectory -ErrorAction Stop

    $server = 'DC01.lab.local'
    $targetOU = 'OU=Users,DC=lab,DC=local'

    # Stop if the specified lab OU cannot be found.
    $null = Get-ADOrganizationalUnit -Identity $targetOU `
        -Server $server -ErrorAction Stop

    $users = @(
        @{ Name = 'Alice Brown'; Sam = 'abrown' }
        @{ Name = 'Tom White';   Sam = 'twhite' }
        @{ Name = 'Emma Green';  Sam = 'egreen' }
    )

    foreach ($user in $users) {
        $sam = $user.Sam

        $existing = Get-ADUser -Filter "SamAccountName -eq '$sam'" `
            -Server $server -ErrorAction Stop

        if ($existing) {
            Write-Warning "Skipping existing account: $sam"
            continue
        }

        # Splatting keeps the creation parameters together.
        $parameters = @{
            Name              = $user.Name
            SamAccountName    = $sam
            UserPrincipalName = "$sam@lab.local"
            Path              = $targetOU
            Server            = $server
            Enabled           = $false
            ErrorAction       = 'Stop'
        }

        # Preview only: no account is created while -WhatIf remains.
        New-ADUser @parameters -WhatIf
    }
}
catch {
    throw "Account-creation preview stopped: $($_.Exception.Message)"
}
```

The duplicate check covers the sample account names; this is not a complete provisioning validation framework.

Before any live test, review the target directory and proposed names. After an approved change, independently query the resulting objects and record their OU, identifiers and enabled state.

References: [Microsoft New-ADUser documentation](https://learn.microsoft.com/en-us/powershell/module/activedirectory/new-aduser) and [Get-ADOrganizationalUnit documentation](https://learn.microsoft.com/en-us/powershell/module/activedirectory/get-adorganizationalunit).

## 4. Password Reset — Revised Preview

This example retrieves a specific lab account and prompts for a password as a secure string rather than embedding a password in the source.

It retains `-WhatIf`, so the password reset is not applied.

**Validation status:** revised reference example; not yet re-tested in the lab.

```powershell
Import-Module ActiveDirectory -ErrorAction Stop

$server = 'DC01.lab.local'
$account = Get-ADUser -Identity 'abrown' -Server $server -ErrorAction Stop

$account | Select-Object Name, SamAccountName, DistinguishedName

$newPassword = Read-Host 'Enter a new lab password' -AsSecureString

try {
    Set-ADAccountPassword -Identity $account -Server $server `
        -Reset -NewPassword $newPassword -WhatIf -ErrorAction Stop
}
finally {
    $newPassword.Dispose()
}
```

For an actual reset, confirm the target account and authority to make the change. Password-policy compliance and the account's intended sign-in behaviour must be checked during the live test.

Do not place real passwords in scripts, screenshots, documentation or commit messages.

Reference: [Microsoft Set-ADAccountPassword documentation](https://learn.microsoft.com/en-us/powershell/module/activedirectory/set-adaccountpassword).

---

## 5. Group Policy — Inspect Before Refreshing

Inspect the currently reported policy results:

```powershell
gpresult /r
```

The following command is different: it requests policy reprocessing and can apply configuration changes. It is not a read-only diagnostic check.

```powershell
gpupdate /force
```

For a controlled policy test, capture the original result, make the intended policy change, refresh policy and inspect the result again.

Policy-processing output and the behaviour of the affected setting should both be checked.

References: [Microsoft gpresult documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/gpresult) and [gpupdate documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/gpupdate).

## Lessons From the Original Exercises

The original build recorded errors involving the spelling of `UserPrincipalName`, PowerShell line continuation and the distinction between OU and container paths.

The improved approach is to inspect the target first, keep parameters readable, stop on unexpected errors and verify the result separately from the command used to make the change.

## Related Documentation

[Active Directory project](../projects/project-02-active-directory/README.md)  
[Troubleshooting case studies](../Troubleshooting/Issues.md)  
[Return to the portfolio overview](../README.md)
