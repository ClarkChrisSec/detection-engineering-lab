# Lab Setup

## Virtual machines (VirtualBox)
| VM | Role | OS |
|---|---|---|
| SIEM-Splunk | Splunk Enterprise | Ubuntu |
| Domain Controller | Active Directory (`lab.local`) | Windows Server 2022 |
| Workstation01 | Domain-joined endpoint | Windows 11 Enterprise |

## Network
All VMs share an internal network (`LAB-INT`, 192.168.56.0/24) with static IPs.

## Data pipeline
- Sysmon installed on Windows hosts with the SwiftOnSecurity config
- Splunk Universal Forwarder sends Windows Event Logs and Sysmon events to Splunk
- Two indexes: `sysmon` and `wineventlog`

## Forwarder inputs.conf
```ini
[WinEventLog://Application]
disabled = false
index = wineventlog

[WinEventLog://Security]
disabled = false
index = wineventlog

[WinEventLog://System]
disabled = false
index = wineventlog

[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = false
index = sysmon
```
