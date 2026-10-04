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

## False positives
Admins and scripts run `whoami` legitimately. In a real environment, tune by parent process and user, and alert on unusual parents (such as Office apps or web servers).


## Notes

**About `NOT_TRANSLATED` in the User field:** In my Splunk results the `User` field shows `NOT_TRANSLATED` in front of `LAB\Administrator`. The account that ran the command is `LAB\Administrator`. The prefix appears to come from how the forwarder resolves the account name, and it doesn't change the detection. The rule matches on the process (`Image` / `OriginalFileName`) rather than the user. If a future rule filters on `User`, it will need to account for the prefix.
