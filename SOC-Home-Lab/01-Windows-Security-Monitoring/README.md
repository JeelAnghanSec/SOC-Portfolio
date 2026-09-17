# 🪟 Windows Security Monitoring

This project documents the deployment and security monitoring of a Windows 10 endpoint using **Wazuh Agent, Sysmon, and Windows Event Logs**.

The objective is to collect endpoint telemetry, detect suspicious activity, investigate security alerts, and document findings from a SOC analyst perspective.

---

## 🎯 Objectives

- Monitor Windows 10 endpoint activity
- Collect Windows Security Event Logs
- Deploy and configure Sysmon
- Monitor authentication activity
- Detect failed login attempts
- Investigate brute-force activity
- Monitor PowerShell execution
- Analyze process creation events
- Monitor file and system activity
- Investigate Wazuh security alerts
- Map relevant detections to MITRE ATT&CK

---

## 🏗️ Monitoring Architecture

```text
                    Windows 10 Endpoint
                           │
              ┌────────────┴────────────┐
              │                         │
        Windows Event Logs           Sysmon
              │                         │
              └────────────┬────────────┘
                           │
                      Wazuh Agent
                           │
                           ▼
                    Wazuh Manager
                           │
                           ▼
                    Wazuh Dashboard
                           │
                           ▼
                 Alert Investigation
```
## 🔧 Technologies & Tools

| Category | Technologies |
|---|---|
| SIEM / XDR | Wazuh |
| Endpoint | Windows 10 |
| Endpoint Agent | Wazuh Agent |
| Log Sources | Windows Event Logs, Sysmon |
| System Monitoring | Sysmon |
| Attack Simulation | Kali Linux |
| Detection | Wazuh Rules & Custom Rules |
| Investigation | Wazuh Dashboard |
| Threat Intelligence | VirusTotal, AbuseIPDB |
| Framework | MITRE ATT&CK |
| Scripting | PowerShell |
| Network Analysis | Wireshark |

