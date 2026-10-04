# Detection Engineering Lab

> **Status:** Work in progress. See the [roadmap](ROADMAP.md) for what's done and what's coming.

A home lab for building and testing threat detections, mapped to MITRE ATT&CK.

## Stack
- **SIEM:** Splunk Enterprise
- **Endpoint telemetry:** Sysmon (SwiftOnSecurity config) and Windows Event Logs
- **Forwarding:** Splunk Universal Forwarder
- **Environment:** VirtualBox, Active Directory domain (`lab.local`)

## How I work
1. Pick an ATT&CK technique
2. Generate the behavior in the lab
3. Write the detection search
4. Confirm it fires, then tune out noise
5. Document it in `detections/`

## Contents
- [Lab setup](lab-setup.md)
- [ATT&CK coverage tracker](coverage.md)
- [Detections](detections/)

- [Roadmap](ROADMAP.md)
