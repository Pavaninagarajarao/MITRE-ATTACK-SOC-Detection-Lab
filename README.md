# MITRE ATT&CK SOC Detection Lab

Home lab simulating MITRE ATT&CK techniques with Atomic Red Team and detecting them in Splunk using Sysmon telemetry.

## Overview
This project documents an end-to-end purple team detection lab built from scratch:
- Deployed Splunk with a Universal Forwarder and custom indexes
- Installed and tuned Sysmon for enriched Windows event logging
- Executed MITRE ATT&CK-mapped techniques using Atomic Red Team
- Wrote and validated Splunk detection rules (SPL) for each technique
- Documented every detection like a real SOC analyst would

## Tools Used
- Splunk Enterprise / Universal Forwarder
- Sysmon
- Atomic Red Team
- MITRE ATT&CK Framework

## Detections
- [T1059.001 – Encoded PowerShell Execution](detections/T1059.001-encoded-powershell.md)
- [T1082 – System Information Discovery](detections/T1082-system-info-discovery.md)
- T1003.001 – LSASS Credential Dumping *(in progress — see Known Gaps below)*

## Dashboard
A Splunk dashboard ("ATT&CK Detection Coverage") visualizes technique coverage across the lab, including:
- Sysmon Process Creation Events (T1059 coverage)
- LSASS Access Attempts (T1003.001)
- Triggered Alerts Summary

See `screenshots/ATT&CK-Detection-Coverage-Dashboard.png` for a full view.

## Known Gaps
This lab is a work in progress. Documenting gaps honestly is part of thinking like a real analyst:

- **T1003.001 (LSASS Credential Dumping):** The detection panel currently shows "No results found." This technique has not yet been successfully triggered via Atomic Red Team in this lab, or the underlying SPL query needs tuning to correctly match Sysmon Event ID 10 (ProcessAccess) against lsass.exe. Planned next step.
- **Triggered Alerts Summary:** This dashboard panel is not yet populated, as no saved searches have been configured to fire as alerts. Next step is to convert key detection searches into scheduled Splunk alerts.

## Screenshots
See the `screenshots/` folder for dashboard views, detection hits, and event code references.

## What This Demonstrates
- **SIEM deployment and configuration:** Deployed Splunk with a Universal Forwarder, created custom indexes, and validated log ingestion from a Windows endpoint
- **Endpoint telemetry tuning:** Installed and configured Sysmon using an industry-standard baseline config to enrich Windows event logging
- **Adversary simulation:** Used Atomic Red Team to execute MITRE ATT&CK-mapped techniques including PowerShell execution, process discovery, and LSASS credential access
- **Detection engineering:** Wrote and saved Splunk detection rules mapped to specific ATT&CK technique IDs, with tuned logic to reduce false positives
- **Threat hunting:** Built SPL queries to identify suspicious process creation, encoded command lines, and LSASS memory access patterns
- **SOC documentation:** Created detection runbooks with technique context, true positive examples, false positive guidance, and response steps
- **Dashboard development:** Built a Splunk dashboard to visualize ATT&CK technique coverage and triggered alert history
- **Lab design:** Designed and operated an end-to-end purple team detection lab independently, from infrastructure setup through detection validation
