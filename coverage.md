# ATT&CK Coverage

<img width="700" alt="splunk reports page listing the whoami and encoded PowerShell detections" src="https://github.com/user-attachments/assets/ddde842b-5395-4bc5-9729-b14d3da01660" />

*Detections saved as Splunk reports. Each one is also running as a scheduled alert.*

| Technique | Name | Tactic | Rule | Tested | Alert |
|---|---|---|---|---|---|
| T1033 | System Owner/User Discovery | Discovery | [whoami](detections/T1033-whoami-execution.md) | Yes | Yes |
| T1059.001 | PowerShell | Execution | [encoded command](detections/T1059.001-powershell-encoded-command.md) | Yes | Yes |
| T1087 | Account Discovery | Discovery | Planned | No | No |
| T1053.005 | Scheduled Task | Persistence | Planned | No | No |
| T1136.001 | Local Account | Persistence | Planned | No | No |
| T1110 | Brute Force | Credential Access | Planned | No | No |
