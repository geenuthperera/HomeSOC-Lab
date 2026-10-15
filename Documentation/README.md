# HomeSOC — Project Documentation

## Overview

This directory serves as the central documentation index for the HomeSOC Security Monitoring & Incident Detection Lab.

HomeSOC is a personal cybersecurity project designed to develop practical Security Operations Center (SOC) skills through Windows endpoint monitoring, security event analysis, and controlled investigation exercises.

The project currently focuses on local Windows 11 security monitoring using:

- Microsoft Sysmon
- Windows Security Auditing
- PowerShell Script Block Logging
- Windows Event Viewer
- Windows PowerShell

Four detection labs have been implemented, tested, and documented locally.

The next development phase involves integrating Wazuh for centralized security event collection, detection, and investigation.

---

## 1. Project Documentation Structure

The HomeSOC repository is organized into several directories.

| Directory | Purpose |
|---|---|
| Architecture | Current and planned monitoring architectures |
| Configs | Security monitoring configurations and verification procedures |
| Detection-Labs | Controlled security monitoring exercises and investigations |
| Documentation | Project setup, implementation references, and documentation index |
| Incident-Reports | Formal security investigation reports |
| Screenshots | Supporting security event evidence |

### Repository Navigation

- [Main Project README](../README.md)
- [Architecture Documentation](../Architecture/README.md)
- [Monitoring Configurations](../Configs/README.md)
- [Detection Labs](../Detection-Labs/)
- [Evidence Screenshots](../Screenshots/)
- [Incident Reports Directory](../Incident-Reports/)

---

## 2. Current Implementation

**Status: Local Windows Security Monitoring Verified**

The first development phase of HomeSOC focused on generating and investigating security events directly on Windows 11.

The following monitoring capabilities were verified during controlled testing:

| Monitoring Capability | Windows Event ID | Status |
|---|---|---|
| File creation and modification | 4663 | Verified |
| File deletion investigation | 4663, 4660 | Verified |
| Failed authentication detection | 4625 | Verified |
| PowerShell Script Block Logging | 4104 | Verified |
| Sysmon process creation | 1 | Verified |

These results were obtained through local Windows Event Viewer investigations.

The project does not currently include a functioning Wazuh SIEM deployment or centralized security alerts.

---

## 3. Environment Requirements

The local monitoring exercises were performed on a Windows 11 endpoint.

### Software and Tools

| Component | Purpose |
|---|---|
| Windows 11 | Endpoint operating system |
| Windows PowerShell | Configuration and controlled testing |
| Windows Event Viewer | Security event investigation |
| Microsoft Sysmon | Detailed process monitoring |
| Windows Security Auditing | Authentication and file activity monitoring |
| GitHub | Project documentation and evidence storage |

Administrator privileges were required for certain configuration activities, including enabling auditing policies and configuring monitoring services.

### Important Notes

Windows monitoring features must be configured before their corresponding security events can be collected.

The required monitoring configurations and testing procedures are documented in the repository.

Some settings were enabled temporarily for testing and subsequently restored.

The successful local tests should not be interpreted as evidence that every monitoring feature remains continuously enabled.

---

## 4. Configuration Documentation

The monitoring configurations used throughout the project are documented in:

[HomeSOC Security Monitoring Configurations](../Configs/README.md)

The configuration documentation includes:

### Microsoft Sysmon

- Sysmon installation and initialization.
- Service verification.
- Sysmon Operational event log location.
- Event ID 1 process creation monitoring.

### Windows Authentication Auditing

- Logon auditing policy verification.
- Failed authentication test environment.
- Windows Security Event ID 4625 investigation.

### PowerShell Script Block Logging

- Registry-based logging configuration.
- Script Block Logging verification.
- PowerShell Operational event log location.
- Event ID 4104 investigation.

### Windows File System Auditing

- File System Auditing policy configuration.
- Directory-specific auditing permissions.
- Controlled file operations.
- Security Event IDs 4663 and 4660.
- Restoration of the original auditing policy.

The configuration reference documents the actual settings used during the controlled investigations.

---

## 5. Detection Lab Documentation

Each completed detection lab contains its objectives, environment details, implementation procedures, collected evidence, observed results, analysis, and security assessment.

### Detection Lab 01 — File Integrity Monitoring

[View Lab 01 Documentation](../Detection-Labs/01-file-integrity-monitoring.md)

**Objective:** Investigate controlled file creation, modification, and deletion activities using Windows Security Auditing.

The exercise included:

- Creating a dedicated test directory.
- Configuring file system auditing.
- Generating file write and modification events.
- Investigating DELETE access.
- Correlating Event IDs 4663 and 4660 using process and handle identifiers.

**Result:** Local file activity monitoring successfully verified.

Wazuh File Integrity Monitoring integration remains pending.

### Detection Lab 02 — Failed Authentication Detection

[View Lab 02 Documentation](../Detection-Labs/02-failed-authentication-detection.md)

**Objective:** Investigate unsuccessful Windows authentication attempts using Windows Security Event ID 4625.

The exercise included:

- Verifying Windows logon auditing.
- Creating a dedicated test account.
- Generating a controlled authentication failure.
- Investigating failure reasons, status codes, and logon details.

**Result:** Failed authentication event successfully captured and analyzed.

### Detection Lab 03 — PowerShell Monitoring

[View Lab 03 Documentation](../Detection-Labs/03-powershell-monitoring.md)

**Objective:** Investigate PowerShell script execution through Script Block Logging.

The exercise included:

- Checking existing logging settings.
- Enabling Script Block Logging.
- Executing a harmless PowerShell test.
- Identifying Event ID 4104.
- Reviewing recorded script block content.

**Result:** PowerShell Script Block Logging successfully verified through Event Viewer.

### Detection Lab 04 — Sysmon Process Analysis

[View Lab 04 Documentation](../Detection-Labs/04-sysmon-process-analysis.md)

**Objective:** Investigate Windows process execution and parent-child process relationships using Microsoft Sysmon.

The exercise included:

- Installing and verifying Sysmon.
- Identifying Sysmon Event ID 1.
- Investigating Microsoft Notepad execution.
- Analyzing PowerShell launching `whoami.exe`.
- Reviewing executable paths, command lines, process IDs, integrity levels, and file hashes.

**Result:** Sysmon process creation telemetry successfully collected and analyzed.

---

## 6. Security Investigation Workflow

The local HomeSOC investigation workflow follows these stages:

1. Identify the monitoring objective.
2. Verify the required Windows logging configuration.
3. Generate controlled test activity.
4. Locate the corresponding Windows Security or Operational event.
5. Examine event details and process information.
6. Correlate related events where appropriate.
7. Assess whether the observed activity is expected or suspicious.
8. Collect supporting evidence.
9. Document the investigation and findings.

### Investigation Data

Depending on the event type, the investigation may include:

- Event ID and description.
- Event timestamp.
- Executing user or account.
- Process name and executable path.
- Process ID and parent process.
- File or object name.
- Access rights and access masks.
- Authentication failure codes.
- Command-line or script block content.
- Related security events.

The collected information supports the reconstruction and explanation of observed system activity.

---

## 7. Evidence Collection

Evidence collected during the investigations is stored in:

[HomeSOC Screenshots](../Screenshots/)

The directory contains screenshots associated with:

- Windows file creation and modification.
- Windows file deletion and event correlation.
- Failed authentication attempts.
- PowerShell Script Block Logging.
- Sysmon process creation events.

Before publication, screenshots were reviewed and personal Windows account information was redacted where appropriate.

The original security event details relevant to the investigations were preserved.

---

## 8. Troubleshooting Reference

The following considerations are useful when reproducing the local monitoring exercises.

| Issue | Recommended Check |
|---|---|
| Sysmon events not appearing | Verify the Sysmon service and Operational log |
| PowerShell Event ID 4104 missing | Verify Script Block Logging configuration and correct log channel |
| Failed authentication event missing | Verify Logon auditing policy and Windows Security log |
| File modification event missing | Verify File System Auditing and directory-specific auditing permissions |
| File deletion event lacks filename | Correlate Event ID 4660 with Event ID 4663 |
| Event Viewer shows no matching events | Verify selected log, Event ID filter, and event timestamp |

More detailed implementation information is available in the corresponding detection lab documentation.

---

## 9. Architecture Documentation

The HomeSOC architecture is documented in:

[HomeSOC Architecture](../Architecture/README.md)

Two monitoring architectures are presented.

### Current Architecture

The implemented environment consists of:

Windows 11 Endpoint → Windows Security Telemetry → Windows Event Logs → Windows Event Viewer → Local Investigation → Evidence Documentation

This architecture represents the monitoring environment used during the completed labs.

### Planned Architecture

The proposed environment will integrate:

Windows 11 Endpoint → Wazuh Agent → Wazuh Manager → Wazuh Indexer → Wazuh Dashboard → Centralized Investigation

Wazuh File Integrity Monitoring will also be configured for selected directories.

The planned architecture has not yet been deployed.

---

## 10. Future Documentation

The following documentation will be added as additional features are implemented.

| Document | Purpose | Status |
|---|---|---|
| Wazuh Deployment Guide | Installation and configuration of Wazuh components | Pending |
| Wazuh Agent Setup | Windows endpoint enrollment | Pending |
| Windows Log Integration | Forwarding Windows security telemetry to Wazuh | Pending |
| Sysmon Integration | Integrating Sysmon event collection with Wazuh | Pending |
| Wazuh FIM Configuration | Centralized file integrity monitoring | Pending |
| Centralized Alert Investigation | Investigating Wazuh alerts and detections | Pending |
| Incident Investigation Reports | Formal documentation of security investigations | Pending |

These guides will be created after their corresponding implementations have been tested and verified.

---

## 11. Documentation Standards

HomeSOC documentation follows these principles:

1. Describe only configurations and activities that were actually performed.
2. Clearly distinguish implemented features from planned features.
3. Include verification steps and observed results.
4. Preserve meaningful technical evidence.
5. Avoid publishing credentials or sensitive system information.
6. Use consistent filenames and descriptive headings.
7. Reference relevant Windows Event IDs accurately.
8. Document limitations and areas requiring further development.

---

## Current Documentation Status

**Local Monitoring Phase — Documented**

The four initial HomeSOC detection labs have been implemented, tested, and documented.

The repository includes:

- A main project README.
- Current and planned architecture documentation.
- Windows monitoring configuration documentation.
- Four detection lab investigations.
- Supporting security event screenshots.

The next documentation milestones are formal incident investigation reports and, subsequently, Wazuh deployment and integration guides.

---

## Disclaimer

All documented activities were conducted for cybersecurity education and authorized security testing.

The project uses controlled test scenarios to develop defensive monitoring and investigation skills.

No unauthorized systems or accounts are targeted.
