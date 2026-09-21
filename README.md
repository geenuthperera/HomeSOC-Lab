# HomeSOC — Security Monitoring & Incident Detection Lab

## Overview

HomeSOC is a personal cybersecurity lab designed to develop practical
Security Operations Center (SOC) skills through endpoint monitoring,
security event analysis, threat detection, and incident investigation.

The lab uses Wazuh as the SIEM/XDR platform together with Microsoft
Sysmon and Windows Event Logging to collect and analyze security telemetry.

Controlled security events are generated within the lab environment and
investigated using a SOC analyst workflow.

---

## Project Objectives

The objectives of this project are to:

- Build a functional home SOC monitoring environment
- Collect Windows security telemetry
- Configure endpoint monitoring using Wazuh
- Use Sysmon for detailed process and system visibility
- Detect suspicious or abnormal activity
- Analyze security alerts
- Practice incident investigation
- Understand Windows event logs
- Map relevant activity to MITRE ATT&CK where appropriate
- Document findings using incident reports

---

## Lab Architecture

The planned lab consists of:

- Windows 11 endpoint
- Wazuh Agent
- Microsoft Sysmon
- Windows Event Logs
- Wazuh SIEM
- SOC investigation workflow

Future expansion will include an isolated Kali Linux virtual machine
for controlled security testing.

---

## Technologies

- Wazuh
- Microsoft Sysmon
- Windows 11
- Windows Event Viewer
- PowerShell
- VirtualBox
- Kali Linux
- MITRE ATT&CK

---

## Detection Labs

### 1. File Integrity Monitoring
Detection and investigation of unexpected file changes.

### 2. Failed Authentication Detection
Analysis of repeated Windows authentication failures.

### 3. PowerShell Monitoring
Monitoring PowerShell activity through Windows event logging.

### 4. Sysmon Process Analysis
Analysis of process creation, parent-child relationships,
command-line arguments, and related telemetry.

### 5. Network Activity Analysis
Controlled network activity generated from an isolated lab environment.

---

## SOC Investigation Workflow

Detection → Alert Review → Evidence Collection → Analysis →
MITRE ATT&CK Mapping → Incident Documentation → Remediation

---

## Project Progress

- [x] Project repository created
- [x] Initial lab architecture planned
- [ ] Wazuh environment deployed
- [ ] Windows endpoint enrolled
- [ ] Wazuh agent verified
- [ ] Sysmon installed
- [ ] Sysmon logs integrated with Wazuh
- [ ] File integrity monitoring configured
- [ ] Failed login detection tested
- [ ] PowerShell monitoring tested
- [ ] Sysmon process analysis completed
- [ ] Incident report created
- [ ] MITRE ATT&CK mappings documented
- [ ] Final architecture diagram added
- [ ] LinkedIn project published

---

## Project Status

🚧 Currently under development.

Initial architecture and documentation are being prepared while the
Wazuh environment is being provisioned.

---

## Disclaimer

This project is intended strictly for cybersecurity education and
authorized lab testing. All security testing is performed against
systems owned by or explicitly controlled by the project author.
