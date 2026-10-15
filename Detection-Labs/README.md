# HomeSOC — Detection Labs

## Overview

This directory contains controlled Windows security monitoring and investigation exercises performed as part of the HomeSOC Security Monitoring & Incident Detection Lab.

The objective is to develop practical SOC analyst skills through security event collection, log analysis, evidence correlation, and investigation documentation.

Four local Windows monitoring exercises have been implemented and verified.

Wazuh SIEM integration remains pending.

---

## Detection Lab Index

| Lab | Investigation | Primary Event IDs | Local Status |
|---|---|---|---|
| 01 | [File Integrity Monitoring](01-file-integrity-monitoring.md) | 4663, 4660 | Verified |
| 02 | [Failed Authentication Detection](02-failed-authentication-detection.md) | 4625 | Verified |
| 03 | [PowerShell Monitoring](03-powershell-monitoring.md) | 4104 | Verified |
| 04 | [Sysmon Process Analysis](04-sysmon-process-analysis.md) | 1 | Verified |

All four exercises were conducted on a Windows 11 endpoint and investigated using Windows Event Viewer.

---

## Completed Investigations

### Lab 01 — File Integrity Monitoring

Windows File System Auditing was configured to investigate controlled file creation, modification, and deletion operations.

Security Event IDs 4663 and 4660 were examined and correlated.

Wazuh File Integrity Monitoring remains pending.

### Lab 02 — Failed Authentication Detection

A controlled failed authentication attempt was generated using a dedicated local test account.

Windows Security Event ID 4625 was examined to investigate authentication failures, account information, and status codes.

### Lab 03 — PowerShell Monitoring

PowerShell Script Block Logging was configured and verified.

Windows Event ID 4104 successfully recorded the controlled PowerShell test command.

### Lab 04 — Sysmon Process Analysis

Microsoft Sysmon was used to investigate process creation activity.

Sysmon Event ID 1 recorded Microsoft Notepad execution and PowerShell launching `whoami.exe`.

Parent-child process relationships, command lines, process identifiers, and executable metadata were analyzed.

---

## Local SOC Investigation Workflow

The completed monitoring exercises followed a structured investigation process:

1. Verify the Windows monitoring configuration.
2. Generate controlled security events.
3. Identify the relevant Windows Event IDs.
4. Analyze event details and related telemetry.
5. Correlate events where appropriate.
6. Collect and redact supporting evidence.
7. Assess the security significance of observed activity.
8. Document technical findings and investigation results.

All observed exercises were authorized and intentionally generated.

---

## Supporting Documentation

- [Monitoring Configurations](../Configs/README.md)
- [Current and Planned Architecture](../Architecture/README.md)
- [Project Documentation](../Documentation/README.md)
- [Evidence Screenshots](../Screenshots/)
- [Security Investigation Reports](../Incident-Reports/)

---

## Future Wazuh Integration

The next project phase will extend local monitoring through centralized security event collection and analysis.

Planned activities include:

- Deploying the Wazuh monitoring environment.
- Installing and enrolling the Windows Wazuh Agent.
- Integrating Windows Security Event Logs.
- Integrating Microsoft Sysmon telemetry.
- Configuring Wazuh File Integrity Monitoring.
- Investigating centralized security alerts.
- Documenting additional SOC investigations.

These activities have not yet been implemented.

---

## Current Status

**Phase 1 — Local Windows Security Monitoring: Completed**

Four controlled detection labs have been successfully implemented, investigated, and documented using local Windows security telemetry.

**Phase 2 — Wazuh SIEM Integration: Pending**

The project currently demonstrates local Windows endpoint monitoring rather than a fully deployed centralized SOC environment.

---

## Disclaimer

All detection labs were performed for cybersecurity education and authorized security testing.

The documented activities represent controlled monitoring exercises and must not be interpreted as confirmed real-world cyberattacks.
