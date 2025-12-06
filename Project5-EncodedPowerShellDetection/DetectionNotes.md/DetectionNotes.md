Detection Notes – Encoded PowerShell Activity (Sysmon Event ID 1)
Overview

This project demonstrates how Sysmon detects hidden or “encoded” PowerShell commands. Attackers often use Base64 encoding to disguise what they’re doing. This test shows what that activity looks like in Windows logs and how a SOC analyst would identify it.

How I Triggered the Event

I created a simple text message: HelloFromProject5

I converted that message into a Base64 string using PowerShell.

I ran PowerShell with the encoded text using:

powershell.exe -enc <Base64String>


Even though the message itself was harmless, this method of launching PowerShell is commonly seen in real attacks.

What Sysmon Captured (Event ID 1 – ProcessCreate)

Sysmon recorded the entire command exactly as it was executed:

Key details from the log:

Image: WindowsPowerShell.exe

CommandLine: Shows powershell.exe -enc <Base64Value>

User: My local account

Parent Process: Another PowerShell instance

Integrity Level: Medium

Hashes: MD5, SHA256, IMPHASH values included

Timestamp: Matches the exact moment I ran the test


This proves Sysmon is able to detect obfuscated PowerShell activity.

Why This Matters in Cybersecurity

Attackers often use PowerShell with encoded commands because:

Encoding hides the real command

It avoids simple detection rules

It helps malware run “fileless” in memory

It blends in with normal Windows administration tools

Sysmon defeats this by capturing:

The exact command line

The process that executed it

Parent process relationships

Hashes of the executable

Execution timestamps

This allows SOC analysts to detect hidden or obfuscated attacker behavior early in an intrusion.

Artifacts Included

event1-powershell-encoded.png – Screenshot showing Sysmon Event ID 1 capturing the encoded command

DetectionNotes.md – Detailed explanation of how Sysmon identified the activity

Summary

This project demonstrates how Sysmon’s ProcessCreate (Event ID 1) can reveal encoded or obfuscated PowerShell activity often used in real attacks. Even when the script content is hidden using Base64, Sysmon still logs the full command line, giving defenders the visibility needed to detect malicious behavior.
