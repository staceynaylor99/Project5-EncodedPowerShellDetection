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