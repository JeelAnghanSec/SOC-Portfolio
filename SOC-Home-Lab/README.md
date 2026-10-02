<div align="center">

<img src="https://capsule-render.vercel.app/api?type=venom&color=0:00f5ff,40:7b2ff7,100:ff00c8&height=260&section=header&text=SOC%20HOME%20LAB&fontSize=72&fontColor=ffffff&animation=twinkling&fontAlignY=40&desc=NEURAL%20DEFENSE%20GRID%20%E2%80%A2%20DETECT%20%E2%80%A2%20CORRELATE%20%E2%80%A2%20RESPOND&descAlignY=62&descSize=16" width="100%"/>

<a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=Orbitron&weight=700&size=22&duration=2800&pause=700&color=00F5FF&center=true&vCenter=true&width=700&height=50&lines=%5B+WAZUH+CORE+%5D+ONLINE;%5B+AGENTS+%5D+WINDOWS+%2B+LINUX+SYNCED;%5B+RULES+%5D+CUSTOM+DETECTIONS+ARMED;%5B+FIM+%5D+WATCHING+EVERY+BYTE;%5B+STATUS+%5D+HUNTING+MODE+ENGAGED" alt="status"/></a>

<br>

![Wazuh](https://img.shields.io/badge/SIEM-WAZUH-00f5ff?style=for-the-badge&labelColor=0a0e17&logo=wazuh&logoColor=00f5ff)
![Windows](https://img.shields.io/badge/ENDPOINT-WINDOWS-7b2ff7?style=for-the-badge&labelColor=0a0e17&logo=windows11&logoColor=white)
![Linux](https://img.shields.io/badge/ENDPOINT-LINUX-ff00c8?style=for-the-badge&labelColor=0a0e17&logo=linux&logoColor=white)
![MITRE](https://img.shields.io/badge/MAPPED-MITRE%20ATT%26CK-ff3b3b?style=for-the-badge&labelColor=0a0e17)
![Status](https://img.shields.io/badge/GRID-ONLINE-39ff14?style=for-the-badge&labelColor=0a0e17)

<br>

**[ Overview ](#-mission-brief) · [ Architecture ](#-grid-architecture) · [ Modules ](#-mission-modules) · [ ATT&CK ](#-threat-coverage) · [ Launch ](#-initialize-sequence)**

</div>

---

## 🛰️ MISSION BRIEF

> **"You can't defend what you can't see."**

This is a fully operational **Security Operations Center** built from the ground up. Endpoints stream live telemetry into **Wazuh**, custom detection logic turns raw logs into high-fidelity alerts, and every scenario is **simulated, detected, and documented**.

<table align="center">
<tr>
<td align="center" width="25%"><h3>🔭</h3><b>VISIBILITY</b><br><sub>Windows + Linux telemetry in a single pane</sub></td>
<td align="center" width="25%"><h3>🎯</h3><b>DETECTION</b><br><sub>Custom rules &amp; decoders, battle-tested</sub></td>
<td align="center" width="25%"><h3>🪪</h3><b>IDENTITY</b><br><sub>Account &amp; privilege change tracking</sub></td>
<td align="center" width="25%"><h3>🧿</h3><b>INTEGRITY</b><br><sub>Real-time file tamper detection</sub></td>
</tr>
</table>

---

## 🧬 GRID ARCHITECTURE

```mermaid
flowchart LR
    subgraph ENDPOINTS["⚡ ENDPOINT LAYER"]
        W["🪟 Windows Host<br/>Wazuh Agent"]
        L["🐧 Linux Host<br/>Wazuh Agent"]
    end

    subgraph CORE["🧠 DETECTION CORE"]
        M["Wazuh Manager<br/>Rules · Decoders · Correlation"]
    end

    subgraph OPS["🖥️ ANALYST LAYER"]
        D["Dashboard<br/>Alerts · Hunting · FIM"]
    end

    W -- "Security Events" --> M
    L -- "auth.log / syslog" --> M
    M -- "Enriched Alerts" --> D

    classDef endpoint fill:#1a1030,stroke:#7b2ff7,stroke-width:2px,color:#fff;
    classDef core fill:#06222b,stroke:#00f5ff,stroke-width:3px,color:#fff;
    classDef ops fill:#2a0b24,stroke:#ff00c8,stroke-width:2px,color:#fff;
    class W,L endpoint;
    class M core;
    class D ops;
```

---

## 🚀 MISSION MODULES

<div align="center">

| ID | MODULE | OBJECTIVE | STATUS |
|:--:|:--|:--|:--:|
| `00` | 🏛️ **Lab Architecture** | Network blueprint, components & data flow | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=0a0e17) |
| `01` | 🪟 **Windows Security Monitoring** | Event logs, logons & endpoint telemetry | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=0a0e17) |
| `02` | 🐧 **Linux Security Monitoring** | Auth logs, SSH activity, brute-force detection | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=0a0e17) |
| `03` | 🧠 **Wazuh Detection Engineering** | Custom rules, decoders & alert tuning | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=0a0e17) |
| `04` | 👤 **Windows User Account Management** | Rogue accounts, group changes, privilege abuse | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=0a0e17) |
| `05` | 🧿 **Wazuh File Integrity Monitoring** | Detect create / modify / delete on critical files | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=0a0e17) |

</div>

<details>
<summary><b>📂 &nbsp;Expand repository file system</b></summary>

```bash
SOC-Home-Lab/
├── 00-Lab-Architecture/                 # blueprint & data flow
├── 01-Windows-Security-Monitoring/      # windows telemetry
├── 02-Linux-Security-Monitoring/        # linux auth & syslog
├── 03-Wazuh-Detection-Engineering/      # custom rules & decoders
├── 04-Windows-User-Account-Management/  # identity & privilege tracking
├── 05-Wazuh-File-Integrity-Monitoring/  # FIM configuration
└── README.md
```

</details>

---

## 🎯 THREAT COVERAGE

How the lab's detections line up with the **MITRE ATT&CK** framework:

| TACTIC | TECHNIQUE | COVERED BY |
|:--|:--|:--:|
| 🔑 Credential Access | **T1110** · Brute Force | `02` Linux Monitoring |
| 🚪 Initial Access / Persistence | **T1078** · Valid Accounts | `01` Windows Monitoring |
| 🧷 Persistence | **T1136** · Create Account | `04` Account Management |
| 🔼 Privilege Escalation | **T1098** · Account Manipulation | `04` Account Management |
| 💣 Impact / Defense Evasion | **T1565** · Data Manipulation | `05` File Integrity |

---

## 🔄 DETECTION PIPELINE

```text
  [ EVENT ] ──▶ [ COLLECT ] ──▶ [ DECODE ] ──▶ [ RULE MATCH ] ──▶ [ ALERT ] ──▶ [ TRIAGE ]
   attack        agent ships      parse into      custom logic      severity       analyst
   simulated     raw logs         fields          fires             assigned       validates
```

---

## 🧰 ARSENAL

<div align="center">

![Wazuh](https://img.shields.io/badge/Wazuh-005571?style=for-the-badge&logo=wazuh&logoColor=white)
![Windows](https://img.shields.io/badge/Windows%20Events-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![Linux](https://img.shields.io/badge/Linux%20Syslog-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Sysmon](https://img.shields.io/badge/Sysmon-1f1f1f?style=for-the-badge&logo=microsoft&logoColor=white)
![VirtualBox](https://img.shields.io/badge/VMWare-183A61?style=for-the-badge&logo=virtualbox&logoColor=white)
![MITRE](https://img.shields.io/badge/MITRE%20ATT%26CK-ff3b3b?style=for-the-badge)

</div>

**Skills demonstrated:** `SIEM Operations` · `Log Analysis` · `Threat Detection` · `Detection Engineering` · `Incident Triage` · `Security Documentation`

---

## ⚙️ INITIALIZE SEQUENCE

```bash
# STEP 01 ▸ study the blueprint
cd 00-Lab-Architecture

# STEP 02 ▸ run modules in order, each one builds on the last
# STEP 03 ▸ replay the simulations in your own lab
# STEP 04 ▸ compare your alerts with the documented results
```

---

<div align="center">

```text
╔══════════════════════════════════════════════════╗
║   > ALERTS TRIAGED ............. ∞               ║
║   > BLIND SPOTS ................ 0               ║
║   > OPERATOR STATUS ............ LEARNING 24/7   ║
╚══════════════════════════════════════════════════╝
```

### ⚡ *Built to learn. Documented to prove it.* ⚡

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:ff00c8,50:7b2ff7,100:00f5ff&height=120&section=footer" width="100%"/>

</div>
