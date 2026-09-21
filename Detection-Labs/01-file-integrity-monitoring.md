# Detection Lab 01 — File Integrity Monitoring

## Status

🟡 Planned — awaiting Wazuh environment deployment.

---

## Objective

The objective of this lab is to configure File Integrity Monitoring (FIM)
on a Windows 11 endpoint and determine whether Wazuh can detect changes
made to monitored files.

This lab will demonstrate how a SOC analyst can identify unexpected
file creation, modification, and deletion activity.

---

## Environment

| Component | Configuration |
|---|---|
| Endpoint | Windows 11 |
| SIEM | Wazuh |
| Endpoint Agent | Wazuh Agent |
| Monitoring Feature | File Integrity Monitoring |
| Test Directory | `C:\SOC-Lab` |

---

## Lab Scenario

A directory on the Windows endpoint will be monitored by Wazuh.

The following controlled actions will be performed:

1. Create a test directory.
2. Create a text file.
3. Modify the contents of the file.
4. Rename the file.
5. Delete the file.
6. Review the resulting Wazuh security events.

---

## Planned Test Directory

```text
C:\SOC-Lab
