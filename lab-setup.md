# Lab Setup

## Virtual machines (VirtualBox)
| VM | Role | OS |
|---|---|---|
| SIEM-Splunk | Splunk Enterprise | Ubuntu |
| Domain Controller | Active Directory (`lab.local`) | Windows Server 2022 |
| Workstation01 | Domain-joined endpoint | Windows 11 Enterprise |

<img width="800" alt="lab  virtual machines running in VirtualBox" src="https://github.com/user-attachments/assets/60566d68-b6f3-41a2-8dc4-d7554ffa53a5" />

*The three lab VMs running in VirtualBox: the Splunk SIEM, the domain controller, and a Windows 11 workstation.*

## Network
All VMs share an internal network (`LAB-INT`, 192.168.56.0/24) with static IPs.

## Data pipeline
- Sysmon installed on Windows hosts with the SwiftOnSecurity config
- Splunk Universal Forwarder sends Windows Event Logs and Sysmon events to Splunk
- Two indexes: `sysmon` and `wineventlog`

<img width="800" alt="Sysmon events by event code in Splunk" src="https://github.com/user-attachments/assets/8275da3f-568a-488c-b2d7-c6f6730d9fd8" />

*Sysmon telemetry arriving in the `sysmon` index. EventCode 1 (process creation) is the most common, followed by 22 (DNS queries).*

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
