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

## False positives
Admins and scripts run `whoami` legitimately. In a real environment, tune by parent process and user, and alert on unusual parents (such as Office apps or web servers).
