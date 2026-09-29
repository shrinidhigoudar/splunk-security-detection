\# Architecture



\## Overview



This project implements a small Detection Engineering / SOC lab using Splunk Enterprise.



The lab uses two virtual machines on an isolated internal network:



\- \*\*Kali Linux VM\*\* — runs Splunk Enterprise and acts as the attacker/SIEM.

\- \*\*Windows 11 VM\*\* — monitored target that generates Windows Security Event Logs.



The Windows events are collected by the Splunk Universal Forwarder and forwarded to Splunk Enterprise for detection and investigation.



\## Architecture Diagram



!\[Splunk Security Detection Architecture](architecture.png)



\## Network Flow



```text

Windows 11 VM

192.168.56.5

&#x20;     |

&#x20;     | Windows Security Events

&#x20;     | Splunk Universal Forwarder

&#x20;     |

&#x20;     | TCP 9997

&#x20;     v

Kali Linux VM

192.168.56.4

&#x20;     |

&#x20;     | Splunk Enterprise

&#x20;     |

&#x20;     v

SPL Detection Searches

&#x20;     |

&#x20;     v

Splunk Alerts

```



The forwarding connection uses TCP port `9997`. Splunk Enterprise listens on Kali, while the Universal Forwarder on Windows sends the collected events to the Kali Splunk instance.



\## Detection Flow



The Windows VM generates relevant Security events, including:



\- `4625` — failed logon

\- `4688` — process creation



These events are forwarded to Splunk, where SPL searches identify suspicious activity and are configured as scheduled alerts.



The two main detections are:



\- RDP Brute Force

\- MSHTA LOLBin execution



\## Components



| Component | Role |

|---|---|

| Windows 11 VM | Monitored endpoint and event source |

| Splunk Universal Forwarder | Collects and forwards Windows events |

| Kali Linux VM | Splunk server and attack/testing environment |

| Splunk Enterprise | SIEM, search and alerting platform |

| SPL | Detection and investigation queries |

