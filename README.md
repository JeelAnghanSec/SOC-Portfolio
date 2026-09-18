# 🛡️ SOC Home Lab

A hands-on Security Operations Center (SOC) home lab focused on security monitoring, attack simulation, detection engineering, log analysis, and incident response using Wazuh.

---

## 🎯 Objectives

- Build a practical SOC monitoring environment
- Monitor Windows and Linux endpoints
- Simulate controlled security attacks
- Collect and analyze security logs
- Create and test custom Wazuh detection rules
- Investigate security alerts
- Map detections to MITRE ATT&CK
- Practice incident response
- Document attack and defense workflows

---

## 🏗️ Lab Architecture

```text
                  ┌─────────────────┐
                  │   Kali Linux    │
                  │    ATTACKER     │
                  └────────┬────────┘
                           │
                    Attack Simulation
                           │
                           ▼
                  ┌─────────────────┐
                  │    Windows 10   │
                  │   Wazuh Agent   │
                  │     TARGET      │
                  └────────┬────────┘
                           │
                      Security Logs
                           │
                           ▼
                  ┌─────────────────┐
                  │   Wazuh Server  │
                  │      Linux      │
                  │    SIEM / XDR   │
                  └─────────────────┘
```

**Current Status:** Wazuh Server and Windows 10 Wazuh Agent are configured. A Linux Wazuh Agent will be added in a later phase.

---

## 🔧 Technologies & Tools

| Category | Technologies |
|---|---|
| SIEM / XDR | Wazuh |
| Operating Systems | Windows 10, Linux, Kali Linux |
| Log Sources | Windows Event Logs, Linux Logs, Sysmon |
| Attack Simulation | Kali Linux |
| Detection | Wazuh Rules & Custom Rules |
| Endpoint Monitoring | Wazuh Agent |
| Threat Intelligence | VirusTotal, AbuseIPDB |
| Framework | MITRE ATT&CK |
| Network Analysis | Wireshark |
| Scripting | PowerShell, Bash, Python |

---

## 🔍 SOC Workflow

```text
Attack Simulation
       ↓
Log Generation
       ↓
Wazuh Agent
       ↓
Wazuh Server
       ↓
Security Alert
       ↓
Investigation
       ↓
Detection Engineering
       ↓
Response
       ↓
Incident Documentation
```

## 📂 Project Structure

```text
SOC-Home-Lab/
│
├── 00-Lab-Architecture/
│   ├── README.md
│   └── screenshots/
│
├── 01-Windows-Security-Monitoring/
│
├── 02-Linux-Security-Monitoring/
│
├── 03-Wazuh-Detection-Engineering/

```

---

## 🖥️ Current Lab

### Wazuh Server
- Linux
- Wazuh Manager
- Wazuh Dashboard
- Centralized security monitoring

### Windows Endpoint
- Windows 10
- Wazuh Agent
- Sysmon 
- Windows Security Event Logs
- Endpoint security monitoring

### Attacker Machine
- Kali Linux
- Controlled attack simulations

### Planned
- Ubuntu/Linux Wazuh Agent
- Linux attack detection
- Custom Wazuh detection rules
- Additional SOC investigations

---

## 🚨 Security Detection Labs

This repository will document practical security scenarios including:

- Windows authentication attacks
- Brute-force detection
- Suspicious PowerShell activity
- File integrity monitoring
- Windows Event Log analysis
- Linux SSH attacks
- Suspicious Linux commands
- Custom Wazuh detection rules
- IOC investigation
- Incident response

---

## 📊 Evidence

Each investigation will contain supporting evidence such as:

- Attacker machine screenshots
- Target machine screenshots
- Wazuh alerts
- Event logs
- Detection rules
- Investigation findings
- MITRE ATT&CK mapping
- Incident reports

---

## ⚠️ Disclaimer

All attack simulations documented in this repository are performed in an isolated home lab environment for educational and defensive security research purposes.

