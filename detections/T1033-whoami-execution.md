# T1033 - System Owner/User Discovery (whoami)

**Tactic:** Discovery
**Data source:** Sysmon EventCode 1 (Process Creation)

## Detection (SPL)
```spl
index=sysmon EventCode=1 (Image="*\\whoami.exe" OR OriginalFileName="whoami.exe")
| table _time, host, User, ParentImage, ParentCommandLine, CommandLine
```

## Why it works
Matches on both `Image` and `OriginalFileName`, so it still catches a renamed copy of the binary.

## How I tested it
Ran `whoami` from an elevated PowerShell session on the Windows host. The event appeared with PowerShell as the parent process.

<img width="800" alt="t1033-Splunk showing a whoami execution launched from PowerShell on the domain controller" src="https://github.com/user-attachments/assets/59e801a2-a2be-4dbe-80c3-b75cae8e383c" />

   *Splunk detecting `whoami.exe` launched from PowerShell on the domain controller. For this screenshot I added a host filter and a PowerShell parent filter to the rule so it shows just this one test run.*

## What the event looks like
<img width="700" alt="Expanded Sysmon process creation event showing CommandLine, Image, ParentImage, and User fields" src="https://github.com/user-attachments/assets/90707471-7dab-4445-8691-42c1c5c4123e" />

*The Sysmon process creation event behind the detection. `Image` and `CommandLine` identify the binary, `ParentImage` shows PowerShell launched it, and `User` holds two values.*

## False positives
Admins and scripts run `whoami` legitimately. In a real environment, tune by parent process and user, and alert on unusual parents (such as Office apps or web servers).

## Alerting

Scheduled to run every 5 minutes over a 5-minute window, and to trigger on any result.

<img width="448" alt="Splunk alert settings: scheduled every 5 minutes, last 5 minutes, trigger when results are greater than 0" src="https://github.com/user-attachments/assets/be1cbff2-7d92-4cb4-8564-9bee6a607622" />

*Alert configuration: runs every 5 minutes over a 5-minute window, and triggers when the result count is greater than 0.*

<img width="800" alt="Splunk Alerts page showing the whoami alert enabled with its next scheduled run" src="https://github.com/user-attachments/assets/89b1d982-f338-4bf3-bb32-84f310c383da" />

*The alert is enabled and scheduled in Splunk.*

<img width="800" alt="Splunk Triggered Alerts page showing the whoami alert firing with Medium severity" src="https://github.com/user-attachments/assets/7dd5b7ed-3043-4d93-af4c-a23ddc4390f4" />

*The alert firing after I ran `whoami` on the domain controller.*

## Notes

**About `NOT_TRANSLATED` in the User field:** In my Splunk results the `User` field is multivalued. It holds two values for the same event: `NOT_TRANSLATED` and `LAB\Administrator`. The account that ran the command is `LAB\Administrator`. Because the field has two values, a search such as `User="LAB\\Administrator"` still matches, but a table column shows both values stacked. This rule matches on the process (`Image` / `OriginalFileName`), so it isn't affected.
