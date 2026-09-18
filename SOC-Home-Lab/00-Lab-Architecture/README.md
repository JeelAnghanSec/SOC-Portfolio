# 🏗️ SOC Home Lab Architecture

## Overview

This section documents the architecture and components of my SOC home lab.

## Lab Components

| System | Role | Platform |
|---|---|---|
| Wazuh Server | SIEM / XDR | Linux |
| Windows Endpoint | Monitored Target | Windows 10 |
| Kali Linux | Attack Simulation | Kali Linux |

## Architecture

```text
                                       ATTACK SIMULATION
                           │
                           ▼
                    ┌──────────────┐
                    │ Kali Linux   │
                    │   Attacker   │
                    └──────┬───────┘
                           │
                 Simulated Security Events
                           │
              ┌────────────┴────────────┐
              │                         │
              ▼                         ▼
       ┌──────────────┐          ┌──────────────┐
       │ Windows 10   │          │ Ubuntu Linux │
       │ Wazuh Agent  │          │ Wazuh Agent  │
       └──────┬───────┘          └──────┬───────┘
              │                         │
              │ Security Telemetry      │ Security Telemetry
              │                         │
              └────────────┬────────────┘
                           ▼
                    ┌──────────────┐
                    │ Wazuh Server │
                    │   Manager    │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │    Wazuh     │
                    │  Dashboard   │
                    └──────┬───────┘
                           │
                           ▼
              ┌────────────────────────┐
              │ SOC Investigation      │
              │                        │
              │ • Alerts               │
              │ • Logs                 │
              │ • Security Events      │
              │ • IOCs                 │
              │ • Endpoint Monitoring  │
              └────────────────────────┘

```
---

## 📸 Lab Evidence

### Wazuh Server

The Wazuh server provides centralized security monitoring and collects security telemetry from connected endpoints.

![Wazuh Server](./images/WAZUH-SERVER.png)

---


# 🖥️ Windows Security Monitoring

This section documents the configuration and monitoring of a Windows 10 endpoint using the Wazuh Agent.


## ⚙️ Windows Wazuh Agent Service

The Wazuh Agent service is installed and configured on the Windows 10 endpoint.

![Windows Wazuh Agent Service](./images/01-Windows-services.png)

### Evidence

- Wazuh Agent service installed
- Wazuh Agent service configured
- Windows endpoint prepared for centralized security monitoring

---


# 🐧 Ubuntu Security Monitoring

This section documents the configuration and monitoring of the Ubuntu Linux
endpoint using the Wazuh Agent.


## ⚙️ Linux Wazuh Agent

The Wazuh Agent is installed and configured on the Ubuntu 24.04 LTS endpoint.

The Linux endpoint is connected to the Wazuh Server and actively sending
security telemetry.

![Ubuntu Linux Wazuh Agent Service](./images/04-Wazuh-Linux-agent.png)

### Evidence

- Wazuh Agent service installed
- Wazuh Agent service configured
- Ubuntu Linux prepared for centralized security monitoring

---

## 🛡️ Wazuh Dashboard — Windows Endpoint

The Wazuh Dashboard provides centralized visibility into the Windows endpoint and its security telemetry.

![Wazuh Windows Agent](./images/02-Wazuh-windows-agent.png)

### Evidence

- Windows endpoint registered with Wazuh
- Wazuh Agent communication established
- Endpoint monitored through Wazuh Dashboard
- Security events available for investigation

---

## 🔄 Monitoring Flow

```text
Windows 10
    │
    ▼
Wazuh Agent
    │
    ▼
Wazuh Manager
    │
    ▼
Wazuh Dashboard
    │
    ▼
Security Alerts & Investigation
