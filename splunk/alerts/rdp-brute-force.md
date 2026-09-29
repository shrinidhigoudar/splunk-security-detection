# RDP Brute Force Detection

This detection looks for repeated Windows failed-logon events (Event ID
`4625`). The events are grouped by account and source IP, and an alert is
triggered when the same combination reaches 5 or more failed attempts.

## 1. Verify Failed Logon Events

```spl
index=main sourcetype="WinEventLog:Security" EventCode=4625
```

## 2. Check Relevant Fields

```spl
index=main sourcetype="WinEventLog:Security" EventCode=4625
| table _time Account_Name Source_Network_Address
```

## 3. Final Detection Query

```spl
index=main sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name, Source_Network_Address
| where count >= 5
```

### Logic

```text
Event 4625
   ↓
Count failed logons
   ↓
Group by Account + Source IP
   ↓
Count >= 5
   ↓
RDP Brute Force Detection
```

## 4. Alert Configuration

- **Name:** RDP Brute Force Detection
- **Type:** Scheduled
- **Schedule:** Every 1 minute
- **Search window:** Last 5 minutes
- **Trigger:** Number of Results > 0
- **Trigger mode:** Once

## 5. MITRE ATT&CK

**T1110 — Brute Force**
