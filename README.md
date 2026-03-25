# 🛡️ Incident Response Case Study – WinRing0 Abuse

## 📌 Overview
This repository documents a real-world malware investigation involving persistent payload execution via a vulnerable driver (WinRing0) on a Windows system.

The infection triggered repeated antivirus detections but persisted across reboots, requiring manual forensic analysis and remediation.

---

## ⚠️ Initial Symptoms
- Repeated Windows Defender alerts (VulnerableDriver:WinNT/WinRing0)
- Temporary `.tmp` files created in user Temp directory
- Malware reappearing after reboot
- No obvious malicious processes visible

---

## 🔍 Investigation Process

### 1. Persistence Analysis
Tools used:
- Autoruns (Sysinternals)

Findings:
- Suspicious scheduled tasks
- References to low-level drivers
- Startup persistence entries

---

### 2. Dynamic Analysis
Tool:
- Process Monitor (ProcMon) with boot logging

Method:
- Filtered for `CreateFile` operations
- Focused on `%Temp%` directory

Key finding:
- Identified parent process:
  PCMeterV0.4.exe

---

### 3. File Validation
Tool:
- VirusTotal

Results:
- Main executable → clean
- Associated DLL → flagged as:
- Vulnerable Driver
- HackTool

Conclusion:
A legitimate tool using an unsafe driver was leveraged as an attack vector.

---

## 💣 Root Cause
The application used a vulnerable driver (similar to WinRing0), allowing execution of malicious payloads in temporary directories.

---

## 🔗 Persistence Mechanisms
- Scheduled Tasks (`PCMeter`)
- Program Files installation directory
- WMI/WBEM components
- Temporary payload execution

---

## 🧹 Remediation Steps
- Terminated malicious process
- Removed scheduled tasks
- Deleted application directory and associated files
- Cleared WMI-related components
- Cleaned Temp and AppData directories

---

## ✅ Validation
- System rebooted
- No further `.tmp` file creation
- No antivirus detections
- Clean ProcMon and Autoruns output

---

## 🧠 Key Takeaways
- Vulnerable drivers are a critical attack vector
- Antivirus may detect payloads but miss root cause
- Behavioral analysis is essential
- Legitimate software can be abused

---

## 🎯 Outcome
✔ Persistent malware removed  
✔ Root cause identified  
✔ System cleaned without OS reinstall  

---

## 🛠️ Tools Used
- Process Monitor (Sysinternals)
- Autoruns (Sysinternals)
- VirusTotal
- Windows Defender

---
