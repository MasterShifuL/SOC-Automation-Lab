# 🔁 Shuffle Workflow – Mimikatz Detection & Automation

## 📌 Overview
This workflow automates the detection and response process for a Mimikatz attack using Shuffle (SOAR).

It receives alerts from Wazuh, extracts the SHA256 hash from Sysmon logs, enriches it using VirusTotal, and creates an incident in TheHive if the file is malicious.

---

## ⚙️ Workflow Steps

### 1. Webhook Trigger
- Receives alert data from Wazuh
- Input includes full log data from Sysmon

---

### 2. Extract SHA256 Hash
- Uses regex to extract SHA256 from raw log:
SHA256=([a-fA-F0-9]{64})


- Source field:
data.win.eventdata.hashes


- Ensures only valid SHA256 hashes are processed

---

### 3. VirusTotal Enrichment
- Sends SHA256 hash to VirusTotal API:
https://www.virustotal.com/api/v3/files/{hash}


- Retrieves:
  - Detection count
  - Threat classification
  - Reputation data

---

### 4. Decision Logic
- If file is detected as malicious:
  - Continue to incident creation
- If not:
  - Workflow stops

---

### 5. Create Case in TheHive
- Automatically creates a case with:
  - Title: "Mimikatz Usage Detected"
  - Severity: High
  - Tags: wazuh, mimikatz, T1003

---

### 6. Email Notification
- Sends alert to SOC analyst via SMTP
- Includes:
  - Hostname
  - IP Address
  - Detection details

---

## 🔄 Data Flow Summary

Wazuh → Shuffle → VirusTotal → TheHive → Email → SOC Analyst

---

## 🧠 Key Design Decisions

- Regex-based hash extraction ensures accuracy from raw logs
- VirusTotal integration provides external threat intelligence
- Automated case creation reduces manual SOC workload
- Email notification enables quick response

---

## ⚠️ Notes

- VirusTotal API key is not included in this repository
- Workflow depends on Sysmon logs containing SHA256 hashes
- Detection is based on filename (can be bypassed)

---

## 🚀 Future Improvements

- Add automated response (process termination / host isolation)
- Improve detection using behavioral rules
- Integrate additional threat intelligence sources
