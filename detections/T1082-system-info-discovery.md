# Detection: System Information Discovery

**ATT&CK Technique:** T1082 - System Information Discovery
**Tactic:** Discovery
**Data Source:** Sysmon Event ID 1 (Process Creation)
**Severity:** Medium

## Description
Detects execution of native Windows utilities commonly used by adversaries to enumerate system information (OS version, hardware, hostname, domain) during the discovery phase of an attack.

## Splunk Query

    index=sysmon EventCode=1
    | where like(CommandLine, "%tasklist%") OR like(CommandLine, "%systeminfo%") OR like(CommandLine, "%wmic%")
    | table _time, Computer, User, ParentImage, Image, CommandLine
    | sort -_time


## True Positive Example
Atomic Red Team T1082 Test 1 runs systeminfo and triggers this rule consistently.

## False Positive Considerations
IT asset management tools, helpdesk scripts, and routine system audits often run systeminfo or similar commands legitimately. Tune by whitelisting known ParentImage values for RMM or asset-inventory tools, and treat this as low-confidence on its own.

## Response Actions
1. Identify the parent process and user account that triggered the command
2. Check whether the activity aligns with scheduled IT/asset-management jobs
3. Look for this event alongside other discovery techniques to assess if it's part of a broader recon chain
4. Escalate if discovery activity is followed by lateral movement or credential access attempts
<img width="1024" height="768" alt="T1082-detection" src="https://github.com/user-attachments/assets/dc74fc23-5902-4fee-9802-a4a57a2d8965" />

