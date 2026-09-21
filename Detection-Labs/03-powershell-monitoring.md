# Detection Lab 03 — PowerShell Monitoring

## Status

🟡 Planned — awaiting Wazuh environment deployment.

---

## Objective

The objective of this lab is to enable and monitor PowerShell logging on a Windows 11 endpoint and determine whether Wazuh can collect and display PowerShell-related security telemetry.

This lab will demonstrate how PowerShell activity can be reviewed by a SOC analyst using Windows event logs and Wazuh.

---

## Environment

| Component | Configuration |
|---|---|
| Endpoint | Windows 11 |
| SIEM | Wazuh |
| Endpoint Agent | Wazuh Agent |
| Log Source | Microsoft-Windows-PowerShell/Operational |
| Logging Feature | PowerShell Script Block Logging |

---

## Lab Scenario

PowerShell Script Block Logging will be enabled on the Windows endpoint.

A small number of harmless PowerShell commands will then be executed.

The resulting PowerShell events will be reviewed in:

1. Windows Event Viewer
2. Wazuh SIEM
3. The relevant security event details

---

## Planned Test Procedure

1. Enable PowerShell Script Block Logging.
2. Open a new PowerShell session.
3. Execute harmless test commands.
4. Review the PowerShell Operational event log.
5. Identify the generated PowerShell events.
6. Review the corresponding events in Wazuh.
7. Compare the Windows event details with the Wazuh telemetry.

---

## Planned Test Commands

Only harmless commands will be used during this lab.

Examples:

```powershell
Get-Date
Get-Process
Get-Service
Get-ChildItem
whoami
