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
---

## 📸 Lab Evidence

### Wazuh Server

The Wazuh server provides centralized security monitoring and collects security telemetry from connected endpoints.

![Wazuh Server](./images/WAZUH-SERVER.png)
