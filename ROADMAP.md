# Roadmap

This project is a work in progress. This page tracks what's done and what's next.

## Done
- [x] Virtual lab built (Splunk SIEM, Active Directory domain, Windows endpoint)
- [x] Sysmon and Windows Event Logs forwarded to Splunk from the domain controller
- [x] Separate indexes for Sysmon and Windows Event Logs
- [x] First detections written, tested, and documented (T1033, T1059.001)
- [x] Detections saved as Splunk reports
- [x] Screenshots added showing each detection firing in the lab

## In progress
- [ ] Lab architecture diagram
- [ ] More ATT&CK detections (account discovery, scheduled tasks, local account creation, brute force)
- [ ] Forwarder on Workstation01
- [ ] Splunk Developer License (requested, needed for scheduled alerts)

## Planned
- [ ] Test detections with Atomic Red Team
- [ ] Rewrite detections as Sigma rules and convert them to SPL
- [ ] Splunk dashboard for detection results
- [ ] Scheduled alerts with thresholds and throttling
- [ ] Tuning notes showing how I reduced false positives
- [ ] Active Directory detections (Kerberos, group changes)

*Last updated: October 2026*
