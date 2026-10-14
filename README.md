# HomeSOC — Security Monitoring & Incident Detection Lab

## Overview

HomeSOC is a personal cybersecurity project focused on developing practical Security Operations Center (SOC) skills through Windows endpoint monitoring, security event analysis, detection exercises, and investigation workflows.

The project currently uses Windows 11, Microsoft Sysmon, Windows Security Event Logging, PowerShell, and Event Viewer to generate, collect, and investigate security telemetry.

Four controlled detection labs have been implemented and verified locally, covering file system activity, failed authentication attempts, PowerShell execution, and process creation.

The next phase of the project involves integrating Wazuh as a centralized SIEM platform to collect and investigate security events through a unified dashboard.

---

## Project Objectives

The main objectives of HomeSOC are to:

- Develop practical SOC monitoring and investigation skills.
- Understand Windows security telemetry and event logging.
- Configure and investigate Windows security auditing.
- Use Microsoft Sysmon to analyze process execution.
- Monitor PowerShell activity using Script Block Logging.
- Investigate authentication failures and file system changes.
- Correlate related Windows Security Events.
- Practice evidence collection and security investigation.
- Understand relevant MITRE ATT&CK techniques.
- Deploy and integrate Wazuh for centralized security monitoring.
- Document security investigations and findings.

---

## Current Lab Environment

The current implementation focuses on local Windows endpoint monitoring.

| Component | Implementation | Status |
|---|---|---|
| Operating System | Windows 11 | Implemented |
| Endpoint Monitoring | Microsoft Sysmon | Verified |
| Security Logging | Windows Security Event Log | Verified |
| PowerShell Monitoring | Script Block Logging — Event ID 4104 | Verified locally |
| Authentication Monitoring | Windows Security Event ID 4625 | Verified |
| File Activity Monitoring | Windows Security Events 4663 and 4660 | Verified |
| Investigation Tool | Windows Event Viewer | Used |
| SIEM Platform | Wazuh | Pending |
| Endpoint Agent | Wazuh Agent | Pending |

The monitoring exercises were performed directly on the Windows 11 endpoint.

Wazuh SIEM integration and centralized log collection have not yet been deployed.

---

## Lab Architecture

### Current Architecture — Local Monitoring

Windows 11 Endpoint

- Microsoft Sysmon
- Windows Security Auditing
- PowerShell Script Block Logging
- Windows Event Logs
- Windows Event Viewer
- Local Event Investigation
- Evidence Collection and Documentation

Security events are generated through controlled activities and investigated directly using Windows Event Viewer.

### Planned Architecture — Wazuh SIEM Integration

The future architecture will include:

- Windows 11 monitored endpoint
- Microsoft Sysmon
- Windows Event Logs
- Wazuh Agent
- Wazuh Server
- Wazuh Indexer
- Wazuh Dashboard
- Centralized Security Monitoring and Investigation

The planned implementation will forward selected Windows security telemetry to Wazuh for centralized analysis, alerting, and investigation.

Wazuh deployment remains pending due to local hardware resource considerations.

---

## Technologies and Tools

| Technology | Purpose |
|---|---|
| Windows 11 | Monitored endpoint |
| Microsoft Sysmon | Process execution telemetry |
| Windows Event Viewer | Local security event investigation |
| PowerShell | Controlled test execution and system configuration |
| Windows Security Auditing | Authentication and file activity monitoring |
| GitHub | Project documentation and evidence |
| MITRE ATT&CK | Security technique reference and investigation context |
| Wazuh | Planned centralized SIEM integration |

---

## Detection Labs

The project contains four documented detection exercises.

### Lab 01 — File Integrity Monitoring

**Status:** Local monitoring verified — Wazuh integration pending.

Implemented Windows File System Auditing to investigate controlled file creation, modification, and deletion activities.

**Key activities:**
- Configured Windows File System Auditing.
- Created a dedicated monitored directory.
- Generated controlled file operations.
- Investigated Windows Security Event IDs 4663 and 4660.
- Correlated process and handle identifiers to investigate file deletion.

**Primary skills:** File activity monitoring, security event analysis, event correlation.

[View Detection Lab 01](Detection-Labs/01-file-integrity-monitoring.md)

### Lab 02 — Failed Authentication Detection

**Status:** Local monitoring verified — Wazuh integration pending.

Investigated controlled failed authentication attempts using Windows Security Event Logs.

**Key activities:**
- Verified Windows logon auditing.
- Created a dedicated test account.
- Generated a controlled failed authentication attempt.
- Identified Windows Security Event ID 4625.
- Examined failure codes, affected accounts, and authentication details.

**Primary skills:** Authentication monitoring, Windows security log analysis.

[View Detection Lab 02](Detection-Labs/02-failed-authentication-detection.md)

### Lab 03 — PowerShell Monitoring

**Status:** Local monitoring verified — Wazuh integration pending.

Configured PowerShell Script Block Logging and investigated recorded script execution activity.

**Key activities:**
- Checked the existing Script Block Logging configuration.
- Enabled PowerShell Script Block Logging.
- Executed a harmless test command.
- Identified Windows Event ID 4104.
- Examined the recorded script block content.

**Primary skills:** PowerShell telemetry, script execution monitoring, security investigation.

[View Detection Lab 03](Detection-Labs/03-powershell-monitoring.md)

### Lab 04 — Sysmon Process Analysis

**Status:** Local monitoring verified — Wazuh integration pending.

Used Microsoft Sysmon to investigate process creation and parent-child process relationships.

**Key activities:**
- Enabled and verified Microsoft Sysmon.
- Investigated Sysmon Event ID 1.
- Examined Microsoft Notepad process creation.
- Investigated PowerShell launching `whoami.exe`.
- Analyzed process identifiers, command lines, integrity levels, executable paths, and file hashes.

**Primary skills:** Process telemetry, parent-child process analysis, endpoint investigation.

[View Detection Lab 04](Detection-Labs/04-sysmon-process-analysis.md)

---

## Security Events Investigated

| Event ID | Log Source | Investigation |
|---|---|---|
| 1 | Microsoft Sysmon | Process creation |
| 4104 | PowerShell Operational | Script block execution |
| 4625 | Windows Security | Failed authentication |
| 4663 | Windows Security | File system access |
| 4660 | Windows Security | Object deletion |

These events were generated or examined during controlled local monitoring exercises.

All observed test activities were legitimate and intentionally performed in the lab environment.

---

## SOC Investigation Workflow

The current investigation approach follows these steps:

1. Configure the required Windows telemetry source.
2. Generate controlled test activity.
3. Locate the corresponding security event.
4. Examine event identifiers, timestamps, processes, and other relevant fields.
5. Collect and review security evidence.
6. Correlate related events where applicable.
7. Assess the observed activity.
8. Reference MITRE ATT&CK where relevant.
9. Document the investigation and findings.

The workflow currently uses local Windows security logs.

Centralized alert investigation through Wazuh remains a future project objective.

---

## Evidence and Documentation

Each detection lab includes relevant documentation such as:

- Lab objectives and environment details.
- Implementation steps.
- Controlled testing procedures.
- Observed Windows Security Events.
- Event analysis and investigation findings.
- Screenshots captured from Windows Event Viewer.
- Security assessments and lessons learned.

Screenshots have been reviewed and personal Windows account information has been redacted where appropriate before publication.

Evidence is maintained in the [Screenshots](Screenshots/) directory.

---

## Project Progress

### Phase 1 — Local Windows Security Monitoring

- [x] Create HomeSOC GitHub repository.
- [x] Plan the initial monitoring architecture.
- [x] Enable and verify Microsoft Sysmon.
- [x] Investigate Sysmon process creation events.
- [x] Configure and test PowerShell Script Block Logging.
- [x] Investigate failed Windows authentication events.
- [x] Configure Windows File System Auditing.
- [x] Investigate file creation and modification activity.
- [x] Correlate file deletion events.
- [x] Collect and redact investigation screenshots.
- [x] Document all four local detection labs.

### Phase 2 — Wazuh SIEM Integration

- [ ] Deploy Wazuh in a suitable environment.
- [ ] Install the Wazuh Agent on the Windows endpoint.
- [ ] Enroll and verify the monitored endpoint.
- [ ] Integrate Windows Security Event Logs.
- [ ] Integrate Microsoft Sysmon telemetry.
- [ ] Configure Wazuh File Integrity Monitoring.
- [ ] Generate and investigate centralized security alerts.
- [ ] Document Wazuh detection results.

### Phase 3 — Further SOC Development

- [ ] Create formal incident investigation reports.
- [ ] Add an architecture diagram reflecting the implemented environment.
- [ ] Develop additional controlled security detection scenarios.
- [ ] Explore relevant MITRE ATT&CK mappings.
- [ ] Improve alert investigation and event correlation workflows.
- [ ] Prepare a project showcase for LinkedIn.

---

## Current Project Status

**Active Development — Local Monitoring Phase Completed**

Four Windows security monitoring labs have been implemented, investigated, and documented.

The project currently demonstrates local Windows security event analysis, process monitoring, authentication monitoring, and file activity investigation.

The next major milestone is deploying Wazuh and integrating the Windows endpoint for centralized monitoring.

The project does not currently include a functioning Wazuh dashboard or verified centralized SIEM alerts.

---

## Future Improvements

Planned improvements include:

- Centralized monitoring using Wazuh.
- Additional endpoint telemetry collection.
- File Integrity Monitoring through Wazuh.
- Custom detection rules and alert investigation.
- Formal incident investigation reports.
- Controlled security simulations in an isolated virtual environment.
- Expanded MITRE ATT&CK technique analysis.
- Improved SOC architecture and documentation.

---

## Disclaimer

HomeSOC is an educational cybersecurity project intended for authorized security monitoring and controlled testing.

All documented activities were conducted in a lab environment using systems owned or explicitly controlled by the project author.

The project is intended to support practical learning and cybersecurity skill development.
