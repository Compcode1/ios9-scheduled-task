IOC 9 – Scheduled Task Persistence with Encoded PowerShell
Overview
This case study documents an attacker’s use of Windows-native binaries to establish persistent, fileless execution using Task Scheduler and obfuscated PowerShell. The operation was designed to silently launch a hidden beacon on schedule, relying entirely on legitimate system components to avoid detection.

Key Objectives
Demonstrate detection of fileless persistence using host-based triage.

Analyze attacker behavior across OS and OSI layers.

Reinforce technical interpretation with analogies and metaphorical clarity.

Core Detection Flow
Triggered by EDR alert: PowerShell process launched by schtasks.exe.

Verified via Event ID 4698 (new scheduled task) and registry Run key.

Script was base64-encoded and executed with hidden window.

Beaconing observed through Invoke-WebRequest to external domain.

Notable Techniques Used
Scheduled task configured to run powershell.exe silently.

Payload passed via base64 encoding to avoid basic string detection.

Redundant persistence using both Task Scheduler and Run key.

Fileless execution with no dropped malware binary.

Outcome
The scheduled task and registry key were removed. Outbound domains were blocked. The host was isolated and memory-captured for runtime analysis. IOC was logged into central SIEM and a detection rule was created for base64 PowerShell launched from scheduled tasks.
