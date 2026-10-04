# Roadmap

This project is a work in progress. This page tracks what's done and what's next.

## Done
- [x] Virtual lab built (Splunk SIEM, Active Directory domain, Windows endpoint)
- [x] Sysmon and Windows Event Logs forwarded to Splunk
- [x] Separate indexes for Sysmon and Windows Event Logs
- [x] First detections written, tested, and documented (T1033, T1059.001)

## In progress
- [ ] More ATT&CK detections (account discovery, scheduled tasks, local account creation, brute force)
- [ ] Forwarders on the domain controller and second workstation

## Planned
- [ ] Test detections with Atomic Red Team
- [ ] Rewrite detections as Sigma rules and convert them to SPL
- [ ] Splunk dashboard for detection results
- [ ] Scheduled alerts with thresholds and throttling
- [ ] Tuning notes showing how I reduced false positives
- [ ] Active Directory detections (Kerberos, group changes)

*Last updated: October 2026*
