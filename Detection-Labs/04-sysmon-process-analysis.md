# Detection Lab 04 — Sysmon Process Analysis

## Status

🟡 Planned — awaiting Wazuh environment deployment.

---

## Objective

The objective of this lab is to use Microsoft Sysmon to collect detailed
process creation telemetry from a Windows 11 endpoint and analyze that
activity through Windows Event Viewer and Wazuh.

This lab will help demonstrate how SOC analysts investigate process
execution, parent-child process relationships, command-line activity,
and executable metadata.

---

## Environment

| Component | Configuration |
|---|---|
| Endpoint | Windows 11 |
| SIEM | Wazuh |
| Endpoint Agent | Wazuh Agent |
| Monitoring Tool | Microsoft Sysmon |
| Log Source | Microsoft-Windows-Sysmon/Operational |
| Primary Event | Sysmon Event ID 1 — Process Create |

---

## Lab Scenario

Microsoft Sysmon will be installed and configured on the Windows endpoint.

Several harmless applications and commands will then be executed to
generate process creation events.

The resulting telemetry will be reviewed to understand how Windows
process activity appears in Sysmon and Wazuh.

---

## Planned Test Procedure

1. Install Microsoft Sysmon.
2. Apply a Sysmon configuration.
3. Verify that the Sysmon service is running.
4. Open Windows Event Viewer.
5. Execute several harmless applications or commands.
6. Locate Sysmon process creation events.
7. Review the same telemetry in Wazuh.
8. Compare parent and child process relationships.
9. Document relevant process details.

---

## Planned Test Activity

Harmless programs and commands will be used during this exercise.

Examples:

```text
notepad.exe
cmd.exe
powershell.exe
whoami
ipconfig
