# MSHTA LOLBin Detection

This detection looks for suspicious execution of `mshta.exe` using Windows Process Creation Event ID `4688`. The detection checks the process command line for VBScript and PowerShell indicators.

## 1. Verify Process Creation Events

```spl
index=main sourcetype="WinEventLog:Security" EventCode=4688
```

## 2. Search for MSHTA

```spl
index=main sourcetype="WinEventLog:Security" EventCode=4688 New_Process_Name="*mshta.exe"
```

## 3. Final Investigation Query

```spl
index=main sourcetype="WinEventLog:Security" EventCode=4688 New_Process_Name="*mshta.exe"
| search Process_Command_Line="*vbscript*" Process_Command_Line="*powershell*"
| table _time Account_Name ComputerName New_Process_Name Process_Command_Line Creator_Process_Name
```

## 4. Detection Logic

```text
Event 4688
    ↓
mshta.exe
    ↓
Check command line
    ↓
VBScript + PowerShell indicators
    ↓
MSHTA Detection
    ↓
Splunk Alert
```

## 5. Alert Configuration

- **Name:** MSHTA LOLBin Detection
- **Type:** Scheduled
- **Schedule:** Every 1 minute
- **Search window:** Last 5 minutes
- **Trigger:** Number of Results > 0
- **Trigger mode:** Once

## 6. MITRE ATT&CK

**T1218.005 — Mshta**
