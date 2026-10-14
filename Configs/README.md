# HomeSOC — Security Monitoring Configurations

## Overview

This directory documents the Windows security monitoring configurations used during the HomeSOC detection labs.

The configurations were tested on a Windows 11 endpoint to generate and investigate security events using Windows Event Viewer.

Four monitoring areas were covered:

1. Microsoft Sysmon process monitoring.
2. Windows failed authentication auditing.
3. PowerShell Script Block Logging.
4. Windows File System Auditing.

The documented settings reflect the controlled testing performed during the project. Some configurations were temporary and should not be interpreted as continuously enabled.

Wazuh SIEM and endpoint agent integration remain pending.

---

## 1. Microsoft Sysmon Configuration

**Related Lab:** [Detection Lab 04 — Sysmon Process Analysis](../Detection-Labs/04-sysmon-process-analysis.md)

### Objective

Collect detailed Windows process creation telemetry, including executable paths, command-line arguments, process identifiers, parent-child process relationships, integrity levels, and file hashes.

### Installation

Microsoft Sysmon was enabled using Administrator PowerShell.

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Sysmon
```

Sysmon was then initialized using:

```powershell
sysmon -i
```

The service status was verified with:

```powershell
Get-Service sysmon*
```

The Sysmon service was confirmed to be running.

### Event Log Location

```text
Event Viewer
  Applications and Services Logs
    Microsoft
      Windows
        Sysmon
          Operational
```

### Monitored Event

| Event ID | Description |
|---|---|
| 1 | Process Create |

### Verification

Controlled tests were performed by launching Microsoft Notepad and executing `whoami.exe` through PowerShell.

Sysmon Event ID 1 successfully recorded process execution information for both activities.

The installation used Sysmon's default configuration. A separate custom Sysmon XML configuration was not applied during the documented investigation.

---

## 2. Windows Authentication Auditing

**Related Lab:** [Detection Lab 02 — Failed Authentication Detection](../Detection-Labs/02-failed-authentication-detection.md)

### Objective

Investigate failed Windows authentication attempts using Security Event ID 4625.

### Audit Policy Verification

Administrator PowerShell was used to check the Logon auditing policy.

```powershell
auditpol /get /subcategory:"Logon"
```

The observed configuration was:

```text
Logon    Success and Failure
```

This confirmed that Windows auditing was configured to record successful and failed logon events.

### Event Log Location

```text
Event Viewer
  Windows Logs
    Security
```

### Monitored Event

| Event ID | Description |
|---|---|
| 4625 | An account failed to log on |

### Verification

A dedicated local account named `HomeSOC_Test` was created for controlled testing.

A failed authentication attempt was generated using an intentionally incorrect password.

Windows Security Event ID 4625 was identified and investigated.

The event contained information including:

- Failed account name.
- Logon type.
- Authentication failure reason.
- Status and substatus codes.
- Process information.
- Network information.

The observed failure included status `0xC000006D` and substatus `0xC000006A`, consistent with an unsuccessful authentication attempt involving an incorrect password.

No account passwords are included in this repository.

---

## 3. PowerShell Script Block Logging

**Related Lab:** [Detection Lab 03 — PowerShell Monitoring](../Detection-Labs/03-powershell-monitoring.md)

### Objective

Record and investigate PowerShell script execution through Windows Event ID 4104.

### Configuration Location

The Script Block Logging policy was configured using the following Windows Registry location:

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging
```

### Configuration Verification

The relevant registry property was:

```text
EnableScriptBlockLogging
```

During the lab, its value was configured as:

```text
EnableScriptBlockLogging = 1
```

A value of `1` enables Script Block Logging.

The configuration was verified using Administrator PowerShell.

### Event Log Location

```text
Event Viewer
  Applications and Services Logs
    Microsoft
      Windows
        PowerShell
          Operational
```

### Monitored Event

| Event ID | Description |
|---|---|
| 4104 | PowerShell Script Block Logging |

### Verification

A harmless PowerShell test was executed:

```powershell
$HomeSOCTest = "HomeSOC-Lab03-4104-Test"
```

Windows Event ID 4104 successfully recorded the script block text.

This demonstrated that PowerShell command content could be inspected through Windows Event Viewer.

**Configuration note:** The policy was verified as enabled during testing. Its current state should be checked independently rather than assuming it remains enabled.

---

## 4. Windows File System Auditing

**Related Lab:** [Detection Lab 01 — File Integrity Monitoring](../Detection-Labs/01-file-integrity-monitoring.md)

### Objective

Monitor controlled file creation, modification, and deletion activity using Windows Security Events.

### Test Directory

```text
C:\SOC-Lab
```

### Initial Audit Configuration

The File System Auditing policy was checked using:

```powershell
auditpol /get /subcategory:"File System"
```

The initial result was:

```text
File System    No Auditing
```

### Enable File System Auditing

Successful file system auditing was temporarily enabled using:

```powershell
auditpol /set /subcategory:"File System" /success:enable
```

The updated policy was verified:

```text
File System    Success
```

### Directory Auditing Configuration

Folder-specific auditing was configured through:

```text
C:\SOC-Lab
  Properties
    Security
      Advanced
        Auditing
```

The following settings were used:

| Setting | Value |
|---|---|
| Principal | Everyone |
| Type | Success |
| Applies to | This folder, subfolders and files |

The auditing permissions included file writing, appending, attribute changes, and deletion operations.

### Configuration Verification

The auditing entries were inspected using:

```powershell
(Get-Acl "C:\SOC-Lab" -Audit).Audit |
    Format-List IdentityReference,FileSystemRights,AuditFlags,InheritanceFlags
```

The resulting output confirmed a successful auditing entry for write and delete operations.

### Monitored Events

| Event ID | Description |
|---|---|
| 4663 | An attempt was made to access an object |
| 4660 | An object was deleted |

### Verification

Three controlled activities were completed:

1. Created a test file and wrote content.
2. Modified the file by appending content.
3. Deleted the file.

Windows successfully recorded the relevant security events.

During the deletion investigation, Events 4663 and 4660 were correlated using their matching process and handle identifiers.

### Restore Original Audit Policy

Following the investigation, the original File System Auditing policy was restored.

```powershell
auditpol /set /subcategory:"File System" /success:disable
```

The final verification returned:

```text
File System    No Auditing
```

This confirmed that the system-wide File System Auditing policy had been restored to its original state.

The directory-specific auditing entry was not removed during this cleanup.

---

## 5. Configuration Summary

| Monitoring Component | Relevant Event IDs | Verification Result |
|---|---|---|
| Microsoft Sysmon | 1 | Process creation events captured |
| Windows Authentication Auditing | 4625 | Failed authentication recorded |
| PowerShell Script Block Logging | 4104 | Script block activity recorded |
| Windows File System Auditing | 4663, 4660 | File operations recorded |

All four configurations supported successful local monitoring investigations.

These results represent controlled test outcomes rather than confirmation that all monitoring configurations remain continuously enabled.

---

## 6. Wazuh Integration Status

Wazuh SIEM integration has not yet been implemented.

The following activities remain planned:

- Deploy Wazuh Manager, Indexer, and Dashboard.
- Install the Wazuh Agent on Windows 11.
- Configure Windows Security Event Log collection.
- Configure Sysmon event collection.
- Enable Wazuh File Integrity Monitoring for selected directories.
- Generate and investigate centralized security alerts.

No verified Wazuh configuration files are currently included in this directory.

Actual Wazuh configuration examples will be added after successful deployment and testing.

---

## 7. Security Considerations

All monitoring activities were performed as part of authorized cybersecurity training.

Before publishing configuration files or screenshots:

- Remove personal Windows account information where appropriate.
- Exclude passwords, tokens, and authentication secrets.
- Avoid publishing sensitive system or network details.
- Review audit policy changes before applying them to other systems.
- Restore temporary configurations when testing is complete.

---

## Conclusion

The HomeSOC project successfully demonstrated four Windows endpoint monitoring configurations through controlled local investigations.

Microsoft Sysmon, Windows Security Auditing, and PowerShell Script Block Logging provided security telemetry that could be investigated using Windows Event Viewer.

These configurations establish a foundation for the future centralized Wazuh monitoring environment.
