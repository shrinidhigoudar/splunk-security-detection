\# MSHTA LOLBin Detection



This detection looks for suspicious execution of `mshta.exe` using Windows

Process Creation Event ID `4688`. The detection checks the process command

line for VBScript and PowerShell indicators.



\## 1. Verify Process Creation Events



```spl

index=main sourcetype="WinEventLog:Security" EventCode=4688

```



\## 2. Search for MSHTA



```spl

index=main sourcetype="WinEventLog:Security" EventCode=4688 New\_Process\_Name="\*mshta.exe"

```



\## 3. Final Investigation Query



```spl

index=main sourcetype="WinEventLog:Security" EventCode=4688 New\_Process\_Name="\*mshta.exe"

| search Process\_Command\_Line="\*vbscript\*" Process\_Command\_Line="\*powershell\*"

| table \_time Account\_Name ComputerName New\_Process\_Name Process\_Command\_Line Creator\_Process\_Name

```



\## 4. Detection Logic



```text

Event 4688

&#x20;  ↓

mshta.exe

&#x20;  ↓

Check command line

&#x20;  ↓

VBScript + PowerShell indicators

&#x20;  ↓

MSHTA Detection

&#x20;  ↓

Splunk Alert

```



\## 5. Alert Configuration



\- \*\*Name:\*\* MSHTA LOLBin Detection

\- \*\*Type:\*\* Scheduled

\- \*\*Schedule:\*\* Every 1 minute

\- \*\*Search window:\*\* Last 5 minutes

\- \*\*Trigger:\*\* Number of Results > 0

\- \*\*Trigger mode:\*\* Once



\## 6. MITRE ATT\&CK



\*\*T1218.005 — Mshta\*\*

