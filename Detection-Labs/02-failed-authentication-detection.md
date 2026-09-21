# Detection Lab 02 — Failed Authentication Detection

## Status

🟡 Planned — awaiting Wazuh environment deployment.

---

## Objective

The objective of this lab is to generate controlled failed authentication
events on a Windows 11 endpoint and determine whether Wazuh can detect
and display the related security telemetry.

This lab will help demonstrate how repeated login failures can be
identified and investigated by a SOC analyst.

---

## Environment

| Component | Configuration |
|---|---|
| Endpoint | Windows 11 |
| SIEM | Wazuh |
| Endpoint Agent | Wazuh Agent |
| Log Source | Windows Security Event Log |
| Test Account | Dedicated local lab account |

---

## Lab Scenario

A dedicated local Windows test account will be created.

A small number of intentional failed login attempts will then be performed
using an incorrect password.

The activity will be reviewed in Wazuh to identify:

1. Failed authentication events
2. The affected username
3. The event timestamp
4. The source endpoint
5. The relevant Windows Event ID
6. Any Wazuh rule or alert associated with the activity

---

## Planned Test Procedure

1. Create a dedicated local test account.
2. Verify the account exists.
3. Attempt to sign in using an incorrect password.
4. Repeat the failed login a small number of times.
5. Review Windows Event Viewer.
6. Review the corresponding Wazuh events.
7. Compare the local Windows event with the Wazuh alert.

---

## Expected Activity

The Windows Security log is expected to record authentication failure
events.

A commonly associated Windows event is:

```text
Event ID 4625
An account failed to log on
