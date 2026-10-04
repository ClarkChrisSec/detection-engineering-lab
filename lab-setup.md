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
- Sysmon and the Splunk Universal Forwarder are running on the domain controller (Workstation01 is planned)
- Splunk Universal Forwarder sends Windows Event Logs and Sysmon events to Splunk
- Two indexes: `sysmon` and `wineventlog`

<img width="800" alt="splunk indexes sysmon and wineventlog with event counts" src="https://github.com/user-attachments/assets/d1713b57-bb77-4a5f-9305-92367a5109f3" />

*Dedicated indexes for Sysmon and Windows Event Logs, with event counts.*

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

<img width="600" alt="inputs.conf open in Notepad showing four WinEventLog stanzas and their index settings" src="https://github.com/user-attachments/assets/c485e3c3-c879-4b83-8f7c-6c1fc0347279" />

*The forwarder's `inputs.conf` on the Windows host, routing Sysmon events to the `sysmon` index and Application, Security, and System logs to `wineventlog`.*
