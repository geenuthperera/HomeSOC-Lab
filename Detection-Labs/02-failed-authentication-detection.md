# Detection Lab 02 — Failed Authentication Detection

## Status

🟠 In Progress — Local Windows failed authentication monitoring verified.

Wazuh SIEM integration remains pending.

---

## Objective

The objective of this lab is to generate a controlled failed authentication event on a Windows 11 endpoint and investigate the resulting security telemetry using Windows Event Viewer.

The lab demonstrates how SOC analysts can identify unsuccessful login attempts, investigate affected accounts, analyze authentication failure codes, and review relevant Windows security events.

---

## Environment

| Component | Configuration |
|---|---|
| Endpoint | Windows 11 |
| Investigation Tool | Windows Event Viewer |
| Log Source | Windows Security Event Log |
| Event ID | 4625 — An account failed to log on |
| Test Account | HomeSOC_Test |
| Account Privileges | Standard User |
| Audit Policy | Success and Failure |
| SIEM Integration | Wazuh — Planned |

---

## Lab Scenario

A dedicated local Windows account named `HomeSOC_Test` was created for controlled authentication testing.

An intentionally incorrect password was supplied during a local authentication attempt.

The resulting security telemetry was investigated in Windows Event Viewer to identify the failed account, logon type, authentication failure reason, and relevant security information.

The experiment was performed on an authorized local Windows endpoint.

---

## Implementation

### Step 1 — Verify Logon Auditing

Administrator PowerShell was used to verify the existing Windows logon auditing configuration.

The following command was executed:

```powershell
auditpol /get /subcategory:"Logon"
```

The result confirmed:

```text
Logon    Success and Failure
```

This verified that Windows was configured to audit unsuccessful logon attempts.

### Step 2 — Create a Dedicated Test Account

A local standard user account was created using Administrator PowerShell.

```powershell
net user HomeSOC_Test * /add
```

A password was configured interactively.

The account was verified using:

```powershell
net user HomeSOC_Test
```

The results confirmed that the account was active and belonged to the local Users group.

### Step 3 — Generate a Controlled Authentication Failure

A deliberately incorrect password was entered using a secure PowerShell input prompt.

```powershell
$wrongPassword = Read-Host "Enter a WRONG password for HomeSOC_Test" -AsSecureString
```

A PowerShell credential object was then created:

```powershell
$cred = [pscredential]::new("$env:COMPUTERNAME\HomeSOC_Test", $wrongPassword)
```

The following command attempted to start Command Prompt using the test credentials:

```powershell
Start-Process -FilePath "$env:WINDIR\System32\cmd.exe" -Credential $cred -WorkingDirectory "$env:WINDIR\System32"
```

Windows rejected the credentials and displayed the following error:

```text
The user name or password is incorrect.
```

The failed authentication attempt was intentional.

### Step 4 — Investigate the Windows Security Log

Windows Event Viewer was opened.

The following log was selected:

```text
Windows Logs
    Security
```

The log was filtered using:

```text
Event ID: 4625
```

A matching event was identified for the `HomeSOC_Test` account.

The event was examined to determine the authentication failure reason, logon type, failure status codes, and related process information.

---

## Evidence

### Windows Security Event ID 4625 — Failed Authentication

The following screenshot shows the failed authentication event captured in Windows Event Viewer.

![Windows Event ID 4625 — Failed Authentication](../Screenshots/windows-failed-logon-event-4625.png)

The event identifies `HomeSOC_Test` as the account involved in the failed logon attempt.

Personal Windows account and computer information was redacted before publication.

---

## Observed Results

A controlled failed authentication attempt was successfully generated and recorded in the Windows Security Event Log.

### Event Details

| Field | Observed Value |
|---|---|
| Event ID | 4625 |
| Event Description | An account failed to log on |
| Event Date | 2026-10-14 |
| Event Time | 10:55:19 AM (Sri Lanka) |
| Failed Account | HomeSOC_Test |
| Logon Type | 2 — Interactive |
| Failure Reason | Unknown user name or bad password |
| Status | 0xC000006D |
| Substatus | 0xC000006A |
| Caller Process | svchost.exe |
| Source Network Address | ::1 |
| Log Source | Windows Security |
| Audit Result | Audit Failure |

The event confirmed that Windows detected and recorded the unsuccessful authentication attempt.

---

## Analysis

### Failed Authentication Investigation

Windows Security Event ID 4625 is generated when a logon attempt fails.

The collected event identified `HomeSOC_Test` as the account for which authentication failed.

The following information was observed:

**Logon Type 2 — Interactive**

The authentication attempt was classified as an interactive logon.

**Status 0xC000006D**

Indicates a logon failure caused by invalid authentication information.

**Substatus 0xC000006A**

Indicates that an incorrect password was supplied.

**Source Network Address ::1**

The IPv6 loopback address was recorded, consistent with local activity.

**Caller Process — svchost.exe**

Windows recorded the service host executable as the caller process associated with the logon event.

### Security Assessment

The failed authentication attempt was generated intentionally during an authorized monitoring exercise.

The observed event was consistent with an incorrect-password authentication attempt against the dedicated test account.

No malicious behavior was established from this event.

The investigation confirmed that Windows Security auditing can provide useful evidence for investigating unsuccessful authentication.

A single failed authentication event does not establish a brute-force attack.

Wazuh SIEM integration remains pending.

---

## MITRE ATT&CK Mapping

Repeated unauthorized password attempts can be associated with MITRE ATT&CK technique T1110 — Brute Force.

However, this experiment involved a single controlled authentication failure rather than an actual brute-force attack.

Therefore, no malicious MITRE ATT&CK technique was confirmed from the collected evidence.

---

## Lessons Learned

- Created and verified a dedicated local Windows test account.
- Verified Windows Success and Failure logon auditing.
- Generated a controlled failed authentication attempt.
- Identified Windows Security Event ID 4625.
- Analyzed authentication status and substatus codes.
- Understood the meaning of interactive logon activity.
- Investigated the affected account and process information.
- Distinguished authorized testing from potentially malicious authentication activity.
- Collected real Windows security evidence for the HomeSOC portfolio.
- Removed the temporary test account and verified successful cleanup after completing the investigation.

---

## Post-Investigation Cleanup

Following the successful completion of Detection Lab 02, the temporary local Windows account `HomeSOC_Test` was removed from the Windows 11 endpoint.

The account was created exclusively for controlled authentication testing and was no longer required after completing the investigation and collecting Event ID 4625 evidence.

### Step 1 — Remove Temporary Test Account

Administrator PowerShell was used to remove the account:

```powershell
net user HomeSOC_Test /delete
```

Windows returned:

```text
The command completed successfully.
```

### Step 2 — Verify Account Removal

The following command was executed:

```powershell
net user HomeSOC_Test
```

Windows returned:

```text
The user name could not be found.
```

This confirmed that the temporary local account had been removed.

### Step 3 — Verify User Profile Cleanup

The following PowerShell command checked whether a profile directory remained:

```powershell
Test-Path "C:\Users\HomeSOC_Test"
```

Observed result:

```text
False
```

No remaining profile directory was detected at the specified location.

### Cleanup Summary

| Verification | Result |
|---|---|
| Temporary Account | Deleted successfully |
| Account Removal | Verified |
| Remaining Profile Directory | Not detected |
| Event ID 4625 Evidence | Preserved |
| Investigation Documentation | Preserved |

**Final Cleanup Status:** Completed.

The temporary account was successfully removed after the controlled authentication investigation. Previously collected Windows Security Event ID 4625 evidence was retained for documentation.

This cleanup demonstrates the importance of removing unnecessary test accounts after completing security exercises.

---

## Future Improvements

- Integrate Windows Security Event Log collection with a SIEM.
- Investigate multiple failed authentication events in a controlled test environment.
- Develop detection rules for unusual authentication patterns.
- Correlate authentication events with additional endpoint telemetry.
- Compare local Windows security monitoring with centralized alerting.

