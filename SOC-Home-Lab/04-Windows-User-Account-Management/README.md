
# 👤 Windows User & Group Management Detection

This project documents the monitoring and investigation of Windows local user and group management activities using **Wazuh**.

The objective is to understand how account-management activities such as user creation, local group membership changes, and user deletion are recorded in Windows Security Event Logs and detected by Wazuh.

---

## 🎯 Objectives

- Create a controlled Windows test user
- Monitor Windows user-account creation
- Add the test user to a local security group
- Monitor local group membership changes
- Remove the test user from the group
- Delete the test user
- Identify the corresponding Windows Event IDs
- Verify that Wazuh receives the events
- Investigate the resulting Wazuh alerts
- Document the detection workflow

---

## 🏗️ Detection Architecture

```text
Windows 10 Endpoint
        │
        ▼
Windows Security Event Logs
        │
        ▼
    Wazuh Agent
        │
        ▼
   Wazuh Manager
        │
        ▼
   Wazuh Rules
        │
        ▼
  Wazuh Dashboard
        │
        ▼
SOC Investigation
