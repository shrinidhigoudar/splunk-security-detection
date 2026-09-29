\# Architecture



\## Overview



This project demonstrates SIEM-based security detection approache using the

same Windows test environment:



\- Splunk



The Windows 11 target VM generates security events. These events are collected

and analysed to detect suspicious activity such as RDP brute-force attempts and

MSHTA/PowerShell execution.



\## Architecture Diagram



!\[Splunk Security Detection Architecture](../screenshots/architecture.png)



\## Environment



\### Windows 11 Target VM



The Windows 11 VM is the monitored endpoint.



It generates Windows Security Event Log events such as:



\- Event ID 4625 — Failed logon

\- Event ID 4688 — New process creation



\### Splunk



Splunk is used to search and analyse the Windows security events.



The project contains two detections:



1\. RDP Brute Force Detection

2\. MSHTA LOLBin Detection



\## Data Flow



Windows 11 Target VM

→ Windows Security Events

→ SIEM

→ Detection Search / Rule

→ Alert

→ Investigation



For the Splunk implementation:



Windows 11 Target VM

→ WinEventLog:Security

→ Splunk

→ SPL Search

→ Detection Result

→ Investigation

