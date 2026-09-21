# HomeSOC Lab Architecture

## Overview

The HomeSOC environment is designed to collect and analyze Windows
security telemetry using Wazuh and Microsoft Sysmon.

The lab initially focuses on endpoint monitoring and will later be
expanded with an isolated Kali Linux system for controlled security
testing.

## Architecture

```mermaid
flowchart TD

    A["Windows 11 Endpoint"] --> B["Windows Event Logs"]
    A --> C["Microsoft Sysmon"]

    B --> D["Wazuh Agent"]
    C --> D

    D --> E["Wazuh SIEM"]

    E --> F["Security Events"]
    E --> G["Threat Detection"]
    E --> H["File Integrity Monitoring"]

    F --> I["SOC Investigation"]
    G --> I
    H --> I

    I --> J["Evidence Collection"]
    J --> K["MITRE ATT&CK Mapping"]
    K --> L["Incident Report"]

    M["Kali Linux VM - Future Expansion"] -. "Controlled Lab Activity" .-> A
```

## Data Flow

The primary monitoring workflow is:

Windows Endpoint  
→ Windows Event Logs / Sysmon  
→ Wazuh Agent  
→ Wazuh SIEM  
→ Security Alert  
→ Investigation  
→ Incident Documentation

## Planned Components

| Component | Purpose |
|---|---|
| Windows 11 | Monitored endpoint |
| Wazuh Agent | Security telemetry collection |
| Sysmon | Advanced Windows event logging |
| Wazuh SIEM | Log analysis and threat detection |
| Windows Event Viewer | Local event investigation |
| MITRE ATT&CK | Threat technique mapping |
| Kali Linux | Future controlled security testing environment |
