<div align="center">

<img src="./assets/banner.svg" alt="SOC Home Lab" width="100%"/>

<br>

![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-00f5ff?style=flat-square&labelColor=061326&logo=wazuh&logoColor=00f5ff)
![Windows](https://img.shields.io/badge/Endpoint-Windows%2010-7aa2ff?style=flat-square&labelColor=061326&logo=windows11&logoColor=white)
![Linux](https://img.shields.io/badge/Endpoint-Ubuntu-ffb703?style=flat-square&labelColor=061326&logo=ubuntu&logoColor=white)
![Kali](https://img.shields.io/badge/Attacker-Kali%20Linux-ff4d6d?style=flat-square&labelColor=061326&logo=kalilinux&logoColor=white)
![MITRE](https://img.shields.io/badge/Mapped-MITRE%20ATT%26CK-ffffff?style=flat-square&labelColor=061326)
![Modules](https://img.shields.io/badge/Modules-6%2F6%20complete-39ff14?style=flat-square&labelColor=061326)

<br>

### *"You can't defend what you can't see."*

[`OVERVIEW`](#-sheet-01--overview) &nbsp;·&nbsp; [`TOPOLOGY`](#-sheet-02--topology) &nbsp;·&nbsp; [`MODULES`](#-sheet-03--module-index) &nbsp;·&nbsp; [`DETECTIONS`](#-sheet-04--detection-map) &nbsp;·&nbsp; [`BOM`](#-sheet-05--bill-of-materials) &nbsp;·&nbsp; [`REPLICATE`](#-sheet-06--replicate)

<img src="./assets/divider.svg" width="100%"/>

</div>

## 📐 SHEET 01 — OVERVIEW

A fully operational **Security Operations Center** built from the ground up. Endpoints stream live telemetry into **Wazuh**, custom detection logic turns raw logs into high-fidelity alerts, and every scenario is **simulated, detected, and documented**.

<table align="center">
<tr>
<td align="center" width="25%"><h3>🔭</h3><b>VISIBILITY</b><br><sub>Windows + Linux telemetry in a single pane</sub></td>
<td align="center" width="25%"><h3>🎯</h3><b>DETECTION</b><br><sub>Custom rules &amp; decoders, battle-tested</sub></td>
<td align="center" width="25%"><h3>🪪</h3><b>IDENTITY</b><br><sub>Account &amp; privilege change tracking</sub></td>
<td align="center" width="25%"><h3>🧿</h3><b>INTEGRITY</b><br><sub>Real-time file tamper detection</sub></td>
</tr>
</table>

<div align="center"><img src="./assets/divider.svg" width="100%"/></div>

## 🧭 SHEET 02 — TOPOLOGY

```mermaid
flowchart LR
    subgraph LAN["ISOLATED LAB NETWORK"]
        K["🐉 Kali Linux<br/>Attacker"]
        W["🪟 Windows 10<br/>Wazuh Agent + Sysmon"]
        U["🐧 Ubuntu<br/>Wazuh Agent + Syslog"]
    end
    subgraph SOC["SOC LAYER"]
        M["🧠 Wazuh Manager<br/>Rules · Decoders · Correlation"]
        D["🖥️ Dashboard<br/>Alerts · Hunting · FIM"]
    end
    K -- "attacks" --> W
    K -- "attacks" --> U
    W -- "telemetry" --> M
    U -- "telemetry" --> M
    M -- "enriched alerts" --> D

    linkStyle 0,1 stroke:#ff4d6d,stroke-width:2px
    linkStyle 2,3 stroke:#00f5ff,stroke-width:2px
    style LAN fill:#0a1a30,stroke:#5ec8ff,stroke-width:2px,color:#fff
    style SOC fill:#08283a,stroke:#00f5ff,stroke-width:2px,color:#fff
    style K fill:#2a0b14,stroke:#ff4d6d,stroke-width:2px,color:#fff
    style W fill:#0a1a30,stroke:#7aa2ff,stroke-width:2px,color:#fff
    style U fill:#2a1a05,stroke:#ffb703,stroke-width:2px,color:#fff
    style M fill:#06222b,stroke:#00f5ff,stroke-width:3px,color:#fff
    style D fill:#06222b,stroke:#00f5ff,stroke-width:2px,color:#fff
```

<div align="center"><img src="./assets/divider.svg" width="100%"/></div>

## 🧩 SHEET 03 — MODULE INDEX

| Sheet | Module | What it covers | Status |
|:--:|:--|:--|:--:|
| `00` | 🏛️ [**Lab Architecture**](./00-Lab-Architecture) | Network blueprint, components & data flow | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=061326) |
| `01` | 🪟 [**Windows Security Monitoring**](./01-Windows-Security-Monitoring) | Event logs, logons & endpoint telemetry | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=061326) |
| `02` | 🐧 [**Linux Security Monitoring**](./02-Linux-Security-Monitoring) | Auth logs, SSH activity, brute-force detection | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=061326) |
| `03` | 🧠 [**Wazuh Detection Engineering**](./03-Wazuh-Detection-Engineering) | Custom rules, decoders & alert tuning | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=061326) |
| `04` | 👤 [**Windows User Account Management**](./04-Windows-User-Account-Management) | Rogue accounts, group changes, privilege abuse | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=061326) |
| `05` | 🧿 [**Wazuh File Integrity Monitoring**](./05-Wazuh-File-Integrity-Monitoring) | Detect create / modify / delete on critical files | ![](https://img.shields.io/badge/-COMPLETE-39ff14?style=flat-square&labelColor=061326) |

<div align="center"><img src="./assets/divider.svg" width="100%"/></div>

## 🎯 SHEET 04 — DETECTION MAP

How the lab's simulations line up with **MITRE ATT&CK**:

| Simulated activity | Detected in | Technique |
|:--|:--:|:--|
| 🔑 SSH brute force | `02` Linux Monitoring | **T1110** · Brute Force |
| 🚪 Use of valid Windows accounts | `01` Windows Monitoring | **T1078** · Valid Accounts |
| 🧷 Rogue local account created | `04` Account Management | **T1136** · Create Account |
| 🔼 Group / privilege change | `04` Account Management | **T1098** · Account Manipulation |
| 💣 Tampering with critical files | `05` File Integrity | **T1565** · Data Manipulation |

> Also simulated: **suspicious PowerShell** activity (**T1059.001**).

```text
 [ EVENT ] ─▶ [ COLLECT ] ─▶ [ DECODE ] ─▶ [ RULE MATCH ] ─▶ [ ALERT ] ─▶ [ TRIAGE ]
  attack        agent ships    parse into     custom logic      severity     analyst
  simulated     raw logs       fields         fires             assigned     validates
```

<div align="center"><img src="./assets/divider.svg" width="100%"/></div>

## 🧰 SHEET 05 — BILL OF MATERIALS

| Component | Role in the lab |
|:--|:--|
| **Wazuh** Manager · Dashboard · Agents | SIEM core: collection, rules, correlation, alerting |
| **Windows 10** + **Sysmon** | Monitored endpoint with rich process and event telemetry |
| **Ubuntu** | Monitored Linux endpoint (auth logs, syslog) |
| **Kali Linux** | Attacker machine for simulations |
| **VMware** | Hypervisor hosting the isolated network |

<div align="center">

![Wazuh](https://img.shields.io/badge/Wazuh-005571?style=for-the-badge&logo=wazuh&logoColor=white)
![Windows](https://img.shields.io/badge/Windows%20Events-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![Linux](https://img.shields.io/badge/Linux%20Syslog-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Sysmon](https://img.shields.io/badge/Sysmon-1f1f1f?style=for-the-badge&logo=microsoft&logoColor=white)
![Kali](https://img.shields.io/badge/Kali%20Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![MITRE](https://img.shields.io/badge/MITRE%20ATT%26CK-ff3b3b?style=for-the-badge)

</div>

**Skills demonstrated:** `SIEM Operations` · `Log Analysis` · `Threat Detection` · `Detection Engineering` · `Incident Triage` · `Security Documentation`

<div align="center"><img src="./assets/divider.svg" width="100%"/></div>


<details>
<summary><b>📂 &nbsp;Repository file system</b></summary>

```text
SOC-Home-Lab/
├── assets/                              banner & divider graphics
├── 00-Lab-Architecture/                 blueprint & data flow
├── 01-Windows-Security-Monitoring/      windows telemetry
├── 02-Linux-Security-Monitoring/        linux auth & syslog
├── 03-Wazuh-Detection-Engineering/      custom rules & decoders
├── 04-Windows-User-Account-Management/  identity & privilege tracking
├── 05-Wazuh-File-Integrity-Monitoring/  FIM configuration
└── README.md
```

</details>

<div align="center">

<img src="./assets/divider.svg" width="100%"/>

```text
┌──────────────────────────────────────────────────┐
│  DWG   SOC-HOME-LAB          REV   05            │
│  SIEM  WAZUH                 STATUS OPERATIONAL  │
│  BUILT TO LEARN. DOCUMENTED TO PROVE IT.         │
└──────────────────────────────────────────────────┘
```

</div>
