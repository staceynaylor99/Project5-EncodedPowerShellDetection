Encoded PowerShell Detection (Sysmon Event ID 1)

This project demonstrates how Sysmon detects hidden or “encoded” PowerShell commands. Attackers often use Base64 encoding to disguise malicious actions. This lab simulates that behavior safely and shows how to identify it using Sysmon logs.

Objectives

Simulate attacker-style encoded PowerShell execution

Capture Sysmon ProcessCreate (Event ID 1) logs

Analyze the command-line details

Understand how SOC analysts detect obfuscated PowerShell activity

Document findings in a clear, professional format

What I Did

Created a simple text message in PowerShell:
HelloFromProject5

Converted the message into Base64.

Executed an encoded command using:

powershell.exe -enc <Base64String>


Located the event inside Sysmon logs.

Collected a screenshot of the event and documented the findings.

Key Findings

Sysmon successfully captured:

The PowerShell executable used

The -enc (encoded command) flag

The Base64 payload

The user who ran the command

The parent process

File hashes (MD5, SHA256, IMPHASH)

Timestamps and execution context

This data is crucial for detecting early-stage attacker behavior, especially when PowerShell is used for obfuscation.

MITRE ATT&CK Mapping

T1059.001 – PowerShell
Attackers commonly use PowerShell with encoded commands to hide activity.

Included Files

DetectionNotes.md — detailed notes and analysis

/screenshots — event1-powershell-encoded.png

Skills Demonstrated

Sysmon log analysis

Recognizing encoded PowerShell techniques

Mapping behavior to MITRE ATT&CK

Creating detection documentation for SOC workflows

Portfolio-ready threat detection project
