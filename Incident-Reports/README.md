# HomeSOC — Security Investigation Reports

## Overview

This directory contains structured security investigation reports created as part of the HomeSOC Security Monitoring & Incident Detection Lab.

The objective is to develop practical SOC analyst skills through security event analysis, evidence collection, incident assessment, and investigation documentation.

Reports are based on controlled security monitoring exercises conducted in an authorized lab environment.

All investigations distinguish legitimate test activity from suspicious or confirmed malicious behavior.

---

## Investigation Reports

| Investigation ID | Investigation Title | Event ID | Classification | Status |
|---|---|---|---|---|
| INV-001 | [Windows Failed Authentication Investigation](INV-001-failed-authentication.md) | 4625 | Controlled Lab Activity | Closed |

---

## Investigation 001 — Failed Authentication

**Investigation Date:** October 14, 2026

**Log Source:** Windows Security Event Log

**Event ID:** 4625

**Affected Test Account:** `HomeSOC_Test`

### Summary

A controlled failed authentication attempt was generated on a Windows 11 endpoint using an intentionally incorrect password.

The resulting Windows Security Event ID 4625 was investigated through Windows Event Viewer.

The investigation examined:

- Authentication failure reason.
- Windows logon type.
- Account information.
- Authentication status and substatus codes.
- Process information.
- Source network address.

The collected evidence confirmed an expected authentication failure during authorized testing.

No genuine security compromise was established.

**Investigation Outcome:** Benign — Expected Test Activity.

[Read Full Investigation Report](INV-001-failed-authentication.md)

---

## Investigation Methodology

HomeSOC investigations follow a structured workflow:

1. Identify the security event.
2. Examine the relevant Windows logs.
3. Collect supporting evidence.
4. Analyze event details.
5. Correlate related events where applicable.
6. Assess the security significance.
7. Reference MITRE ATT&CK where appropriate.
8. Document findings and conclusions.
9. Recommend security improvements when relevant.

---

## Report Template

A reusable report template is available for future investigations.

[Security Incident Report Template](incident-template.md)

The template provides sections for investigation information, detection, evidence, technical analysis, timeline, MITRE ATT&CK mapping, impact assessment, remediation, and conclusion.

---

## Supporting Documentation

- [HomeSOC Main README](../README.md)
- [Detection Lab 02 — Failed Authentication](../Detection-Labs/02-failed-authentication-detection.md)
- [Monitoring Configurations](../Configs/README.md)
- [Evidence Screenshots](../Screenshots/)

---

## Future Investigations

Additional investigation reports may cover:

- Windows file creation, modification, and deletion.
- PowerShell Script Block Logging.
- Sysmon process creation and parent-child process relationships.
- Centralized security alerts after Wazuh integration.

These reports will be added as the relevant investigations are completed and documented.

---

## Disclaimer

All currently documented investigations are conducted for cybersecurity education and authorized security testing.

Controlled lab activities are not represented as genuine cyberattacks or confirmed security incidents.
