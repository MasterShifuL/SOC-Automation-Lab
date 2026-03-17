
# 🛡️ SOC Playbook – Mimikatz Detection (T1003)

## 📌 Overview
This playbook defines the investigation and response steps when a Mimikatz activity is detected in the environment.

Detection is triggered by Wazuh using Sysmon logs and enriched via VirusTotal before being sent to TheHive.

---

## 🚨 Alert Details

- Detection Source: Wazuh (Sysmon logs)
- Rule ID: 100002
- Technique: Credential Dumping (MITRE ATT&CK T1003)
- Severity: High

---

## 🔍 Investigation Steps

### 1. Validate the Alert
- Confirm process name: `mimikatz.exe`
- Check Sysmon logs:
  - ProcessCreate
  - ImageLoad
- Verify hash from VirusTotal

---

### 2. Identify Affected Host
- Hostname
- IP Address
- Logged-in user

---

### 3. Analyze Process Activity
- Parent process (cmd.exe / powershell.exe?)
- Execution path
- Time of execution

---

### 4. Check Lateral Movement
- Look for:
  - Remote logins
  - Suspicious network connections
  - Multiple authentication attempts

---

### 5. Review Additional Logs
- Windows Event Logs
- Wazuh alerts
- Authentication logs

---

## ⚡ Response Actions

### Immediate Actions
- Isolate affected host from network
- Terminate malicious process
- Disable compromised user account

---

### Containment
- Reset user credentials
- Revoke active sessions
- Block suspicious IPs

---

### Eradication
- Remove malicious files
- Scan system for persistence mechanisms

---

### Recovery
- Restore system if needed
- Monitor for re-infection

---

## 🧠 Lessons Learned

- Improve detection rules (behavior-based)
- Enhance monitoring coverage
- Add automated response (future improvement)

---

## 🔄 Automation Mapping

| Step | Tool |
|-----|-----|
| Detection | Wazuh |
| Enrichment | VirusTotal |
| Case Management | TheHive |
| Automation | Shuffle |

---

## 📌 Notes

This playbook is designed for educational SOC lab purposes and simulates real-world incident response procedures.
