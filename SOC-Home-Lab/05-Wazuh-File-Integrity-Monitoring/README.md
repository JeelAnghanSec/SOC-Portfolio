# 🛡️ Wazuh File Integrity Monitoring (FIM) 

This is **Task 05** of my `SOC-Home-Lab` project, focused on implementing and testing **File Integrity Monitoring (FIM)** using **Wazuh** on a Windows 10 endpoint.

The task covers creating a directory to represent a sensitive data location, configuring real-time `syscheck` monitoring for that directory in `ossec.conf`, creating a baseline file, and modifying it to trigger a detection. The resulting Wazuh alert is then reviewed to demonstrate the checksum comparison, rule metadata, and MITRE ATT&CK mapping produced by the FIM engine.

---

## 🎯 Objectives

- Create a dedicated directory to simulate a sensitive data store
- Configure the Wazuh agent to monitor the directory in real time via `syscheck`
- Create a baseline file to establish an integrity checksum
- Modify the file to simulate unauthorized/tampering activity
- Verify Wazuh generates a real-time FIM alert on file modification
- Review the generated alert fields and rule metadata
- Review cryptographic checksum changes (MD5, SHA1, SHA256)
- Map the detected activity to the MITRE ATT&CK framework
- Review compliance framework mappings (GDPR, HIPAA, GPG13)
- Document the task as part of the SOC Home Lab project

---

## 🏗️ Task Architecture

```mermaid
flowchart TD
    A[Windows 10 Endpoint - JEEL-Windows] --> B[Create Monitored Directory C:\Security_Data]
    B --> C[Configure ossec.conf - syscheck realtime]
    C --> D[Create Baseline File important.txt]
    D --> E[Modify File Content]
    E --> F[Wazuh Agent Detects Checksum Change]
    F --> G[Wazuh Manager]
    G --> H[Detection Rule 550 - Integrity Checksum Changed]
    H --> I[Wazuh Dashboard - FIM Module]
    I --> J[Alert Review]
    J --> K[MITRE ATT&CK T1565.001 Mapping]
```

---

## 🔧 Technologies & Tools

| Category | Technology |
|---|---|
| SIEM / XDR | Wazuh |
| Endpoint | Windows 10 |
| Endpoint Agent | Wazuh Agent |
| Monitoring Method | Syscheck (File Integrity Monitoring) — Real-time |
| Configuration File | `ossec.conf` |
| Review Tool | Wazuh Dashboard (FIM Module) |
| Detection | Wazuh Rule ID 550 |
| Framework | MITRE ATT&CK |
| Testing Environment | Controlled SOC Home Lab |

---

## 🧪 Task Walkthrough

### 1️⃣ Create the Monitored Directory

A dedicated folder, `C:\Security_Data`, was created on the endpoint to simulate a sensitive data store that requires integrity monitoring.

![Create FIM Monitoring Folder](images/01-create-fim-monitoring-folder.png)

---

### 2️⃣ Create a Baseline Test File

A test file, `important.txt`, was created inside the monitored directory with placeholder content. This establishes the baseline checksum (MD5/SHA1/SHA256) that Wazuh will use for future comparison.

![Create FIM Test File](images/02-create-fim-test-file.png)

---

### 3️⃣ Configure Real-Time FIM in `ossec.conf`

The Wazuh agent configuration was edited to add `C:\Security_Data` as a **real-time monitored directory** under the `<syscheck>` block, alongside the existing default Windows monitoring rules:

```xml
<directories realtime="yes">C:\Security_Data</directories>
```

Real-time mode (as opposed to scheduled scanning) ensures that any file event — creation, modification, or deletion — inside the directory is detected and forwarded to the Wazuh manager immediately.

![Configure ossec.conf FIM Rule](images/03-configure-ossec-fim-rule.png)

---

### 4️⃣ Modify the Monitored File

The test file was accessed via a Remote Desktop session (`DESKTOP-MOVB2SI`) and modified by appending new content, simulating an unauthorized or unexpected change to a sensitive file.

![Modify Monitored File](images/04-modify-monitored-file.png)

---

### 5️⃣ Verify the FIM Alert in Wazuh

Within seconds of the modification, the Wazuh **File Integrity Monitoring** dashboard for agent `JEEL-Windows` (agent ID `001`) recorded the event. The `Events` view confirms the modified path (`c:\security_data\important.txt`), the `modified` syscheck event type, and the triggering detection rule.

![Wazuh FIM Alert](images/05-wazuh-fim-alert.png)

---

### 6️⃣ Review the Full Alert Document

Drilling into the raw alert document provides full detail: the exact timestamp, agent metadata, decoder used, and the complete `full_log` showing the old and new modification times and hash values.

![Wazuh FIM File Integrity Details](images/06-wazuh-fim-file-integrity-details.png)

---

## 🔍 Detection Rule & Alert Analysis

| Field | Value |
|---|---|
| **Timestamp** | Sep 22, 2026 @ 16:24:17.036 |
| **Agent Name** | JEEL-Windows |
| **Agent ID** | 001 |
| **Agent IP** | 192.168.111.143 |
| **Decoder** | `syscheck_integrity_changed` |
| **Monitored Path** | `c:\security_data\important.txt` |
| **Syscheck Event** | modified |
| **Changed Attributes** | `mtime`, `md5`, `sha1`, `sha256` |
| **Old MD5** | `19515176da24793d795798b3b9e68e54` |
| **New MD5** | `6e70ee86b61506ca9a411a46670e3031` |
| **Rule ID** | 550 |
| **Rule Level** | 7 |
| **Rule Description** | Integrity checksum changed |
| **Rule Groups** | `ossec`, `syscheck`, `syscheck_entry_modified`, `syscheck_file` |
| **Rule Fired Times** | 2 |

The change in the MD5/SHA1/SHA256 checksums — not just the modification time — confirms that the **actual content** of the file was altered, ruling out a simple metadata-only change (e.g., a touch or permission update).

---

## 🗺️ MITRE ATT&CK Mapping

| Technique ID | Technique Name | Relevance |
|---|---|---|
| **T1565.001** | Data Manipulation: Stored Data Manipulation | The unauthorized modification of file content on disk mirrors adversary behavior where stored data is altered to manipulate business/operational outcomes or conceal malicious activity. Wazuh's real-time checksum comparison provides direct detection coverage for this technique. |

---

## 📌 Key Takeaways

- Real-time `syscheck` detected the unauthorized file modification within seconds of the change, with no reliance on scheduled scan intervals.
- The alert fired at **rule level 7**, appropriately reflecting a moderate-severity integrity violation rather than a routine, low-priority event.
- Full cryptographic hash comparison (MD5, SHA1, SHA256) gave high-confidence evidence that file **content**, not just metadata, was changed.
- The `full_log` field preserved forensic detail — old vs. new modification time and old vs. new hash values — enough to reconstruct what changed without touching the endpoint directly.
- Automatic mapping to **MITRE ATT&CK T1565.001** and to GDPR/HIPAA/GPG13 controls shows how a single low-level telemetry event can support both threat detection and compliance reporting simultaneously.
- This task highlights FIM's value for monitoring sensitive directories (credential stores, configuration files, financial/PII data folders) where unauthorized changes should never occur silently.

---

## ✅ Conclusion

This task, as part of my SOC Home Lab project, demonstrates end-to-end configuration and validation of **Wazuh File Integrity Monitoring** — from editing the agent's `ossec.conf` to triggering, detecting, and reviewing a real-world-style tampering event. It builds practical skills in FIM configuration, alert triage, checksum-based analysis, and mapping detections to both the MITRE ATT&CK framework and regulatory compliance controls.

---

## 📁 Folder Structure

```
05-Wazuh-File-Integrity-Monitoring/
├── images/
│   ├── 01-create-fim-monitoring-folder.png
│   ├── 02-create-fim-test-file.png
│   ├── 03-configure-ossec-fim-rule.png
│   ├── 04-modify-monitored-file.png
│   ├── 05-wazuh-fim-alert.png
│   └── 06-wazuh-fim-file-integrity-details.png
└── README.md
```
