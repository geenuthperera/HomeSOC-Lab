# Detection Labs

This directory contains controlled security monitoring and detection exercises performed as part of the HomeSOC project.

Each lab focuses on a different type of Windows security telemetry and SOC investigation workflow.

## Lab Index

| Lab | Topic | Primary Skill |
|---|---|---|
| [Lab 01](01-file-integrity-monitoring.md) | File Integrity Monitoring | File change detection |
| [Lab 02](02-failed-authentication-detection.md) | Failed Authentication Detection | Windows security log analysis |
| [Lab 03](03-powershell-monitoring.md) | PowerShell Monitoring | PowerShell event analysis |
| [Lab 04](04-sysmon-process-analysis.md) | Sysmon Process Analysis | Process telemetry and parent-child analysis |

## Planned Workflow

Each detection lab follows the same investigation process:

1. Configure the required telemetry source.
2. Generate controlled test activity.
3. Review the event locally on the Windows endpoint.
4. Review the corresponding telemetry in Wazuh.
5. Collect evidence.
6. Analyze the event.
7. Map relevant activity to MITRE ATT&CK where appropriate.
8. Document the findings.

## Current Status

All labs are currently in the planning stage and will be updated with real observations, screenshots, and analysis after the Wazuh environment is deployed.
