# 🛡️ Wazuh Detection Engineering

This project documents the development, testing, and investigation of security detections using **Wazuh** in a controlled SOC home lab environment.

The objective is to understand how security telemetry is collected, how Wazuh rules identify suspicious activity, and how detection logic can be investigated and improved from a SOC analyst perspective.

---

## 🎯 Objectives

- Understand Wazuh detection rules
- Analyze Wazuh security alerts
- Investigate rule IDs and severity levels
- Understand Wazuh decoders and rule groups
- Analyze Windows and Linux security telemetry
- Identify relevant MITRE ATT&CK mappings
- Develop and test custom Wazuh rules
- Tune detections to reduce false positives
- Validate detection logic using controlled lab activity
- Document detection engineering workflows

---

## 🏗️ Detection Engineering Architecture

```text
                Endpoint Activity
                       │
          ┌────────────┴────────────┐
          │                         │
      Windows                    Linux
          │                         │
    Event Logs / Sysmon       auth.log / journald
          │                         │
          └────────────┬────────────┘
                       │
                  Wazuh Agent
                       │
                       ▼
                 Wazuh Manager
                       │
              ┌────────┴────────┐
              │                 │
           Decoders            Rules
              │                 │
              └────────┬────────┘
                       │
                       ▼
                  Wazuh Alert
                       │
                       ▼
                SOC Investigation
                       │
                       ▼
              MITRE ATT&CK Mapping
```

---

## 🔧 Technologies & Tools

| Category | Technology |
|---|---|
| SIEM / XDR | Wazuh |
| Endpoint Monitoring | Wazuh Agent |
| Windows Telemetry | Windows Event Logs, Sysmon |
| Linux Telemetry | `/var/log/auth.log`, journald |
| Detection | Wazuh Rules |
| Log Processing | Wazuh Decoders |
| Investigation | Wazuh Dashboard |
| Attack Simulation | Kali Linux |
| Threat Framework | MITRE ATT&CK |
| Detection Testing | Controlled Lab Activity |

---

## 🖥️ Lab Environment

| Component | Role |
|---|---|
| Wazuh Server | Centralized security monitoring |
| Windows 10 | Windows security telemetry |
| Linux | Linux security telemetry |
| Kali Linux | Controlled attack simulation |

---

# 🔍 Detection Engineering Process

The detection engineering workflow used in this project follows:

```text
Security Event
      ↓
Log Collection
      ↓
Decoder
      ↓
Detection Rule
      ↓
Alert Generation
      ↓
Alert Validation
      ↓
Investigation
      ↓
MITRE ATT&CK Mapping
      ↓
Rule Tuning
      ↓
Documentation
```

---

# 🚨 Detection Development

## 1. Detection Identification

Security events are first identified from Windows and Linux endpoints.

Examples include:

- Failed authentication
- SSH authentication failures
- Suspicious PowerShell execution
- Privileged `sudo` activity
- Suspicious process execution
- File or system changes

---

## 2. Wazuh Rule Analysis

Each detection is analyzed using relevant Wazuh fields such as:

- Rule ID
- Rule level
- Rule description
- Rule groups
- Decoder
- Event source
- Source IP
- Username
- Command line
- MITRE ATT&CK mapping

---

## 3. Detection Validation

Detection rules are validated by generating controlled security events inside the isolated home lab.

The resulting telemetry is then compared with the Wazuh alert to verify that the detection works as expected.

---

## 4. Custom Detection Engineering

Custom Wazuh rules will be developed to detect security activity that requires additional detection logic beyond the default rules.

Custom rules may be used for:

- Specific commands
- Suspicious authentication patterns
- Privilege escalation
- PowerShell activity
- Suspicious processes
- File activity
- Attack simulation events

---

# 🧪 Detection Testing

Each detection will follow a controlled testing process:

```text
Generate Test Activity
        ↓
Verify Endpoint Logs
        ↓
Check Wazuh Collection
        ↓
Search Wazuh Dashboard
        ↓
Analyze Alert
        ↓
Validate Rule
        ↓
Document Result
```

---

# 📊 Detection Documentation

Each completed detection will document:

| Field | Description |
|---|---|
| Detection Name | Name of the detection |
| Data Source | Windows / Linux telemetry |
| Event | Activity being detected |
| Rule ID | Wazuh rule identifier |
| Rule Level | Alert severity |
| Rule Group | Associated Wazuh group |
| Decoder | Decoder processing the event |
| MITRE ATT&CK | Associated technique |
| Detection Logic | Logic used for detection |
| Investigation | Analyst findings |
| False Positive | Potential benign activity |
| Tuning | Detection improvements |

---

# 🧩 MITRE ATT&CK Mapping

Relevant Wazuh detections will be mapped to the **MITRE ATT&CK framework** where applicable.

Example:

```text
Wazuh Detection
      ↓
Rule Analysis
      ↓
MITRE ATT&CK Technique
      ↓
Tactic
      ↓
Investigation Context
```

---

# 📸 Lab Evidence

Detection engineering screenshots, rule configurations, alerts, and investigation evidence will be stored in the `images` directory.

```text
images/
```

Evidence will be added as individual detection scenarios are completed.

---

# 🎓 Skills Demonstrated

- Wazuh Detection Engineering
- SIEM Alert Analysis
- Wazuh Rule Analysis
- Decoder Analysis
- Custom Rule Development
- Detection Validation
- False Positive Analysis
- MITRE ATT&CK Mapping
- Security Event Correlation
- SOC Investigation

---

## ⚠️ Disclaimer

All security testing and detection development documented in this repository is performed in an isolated home lab environment for educational and defensive security research purposes.
