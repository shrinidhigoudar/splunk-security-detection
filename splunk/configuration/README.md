# Splunk Configuration

## Lab Components

- Kali Linux VM — Splunk Enterprise
- Windows VM — Splunk Universal Forwarder 

## Splunk Resources

- Splunk Enterprise: https://www.splunk.com/en_us/download/splunk-enterprise.html
- Splunk Universal Forwarder: https://www.splunk.com/en_us/download/universal-forwarder.html

## Lab Setup

The Splunk Enterprise `.deb` package was installed on Kali under:

```text
/opt/splunk
```

The Splunk Universal Forwarder was installed on the Windows VM.

```text
Kali Linux: 192.168.56.4(manually given the IP)
Windows VM: 192.168.56.5(manually given the IP)
Forwarding Port: TCP 9997
```

Windows Security Event Logs were collected using:

```text
C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf
```

Configuration:

```ini
[WinEventLog://Security]
disabled = 0
index = main
sourcetype = WinEventLog:Security
```
