# Roadmap

This project is a work in progress. This page tracks what's done and what's next.

## Done
- [x] Virtual lab built (Splunk SIEM, Active Directory domain, Windows endpoint)
- [x] Sysmon and Windows Event Logs forwarded to Splunk from the domain controller
- [x] Separate indexes for Sysmon and Windows Event Logs
- [x] First detections written, tested, and documented (T1033, T1059.001)
- [x] Detections saved as Splunk reports
- [x] Scheduled alerts running for both detections (every 5 minutes, Triggered Alerts)
- [x] Screenshots added showing each detection and alert firing
- [x] Lab architecture diagram

## In progress
- [ ] More ATT&CK detections (account discovery, scheduled tasks, local account creation, brute force)
- [ ] Forwarder on Workstation01

## Planned
- [ ] Test detections with Atomic Red Team
- [ ] Rewrite detections as Sigma rules and convert them to SPL
- [ ] Splunk dashboard for detection results
- [ ] Alert throttling and thresholds
- [ ] Tuning notes showing how I reduced false positives
- [ ] Active Directory detections (Kerberos, group changes)

*Last updated: October 2026*
