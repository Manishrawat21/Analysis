# Splunk Detection Queries — DLL Hijacking Analysis

This document contains **investigative Splunk queries** aligned with the DLL hijacking analysis described in the accompanying articles.

These queries are intended to:
- Validate suspicious behavior
- Reconstruct attack timelines
- Support analyst-driven investigations

They are **not designed as automated blocking rules**, but as detection and triage aids.

---

## 1. High-Level Event Coverage

### What Event IDs are present?

```spl
index=main sourcetype=XmlWinEventLog
| stats count by EventID
```
## 2. Initial Execution — Process Creation (EventID 1)

```spl
index=main sourcetype=XmlWinEventLog EventID=1
| table _time Image CommandLine ParentImage User
```
## 3. DLLs Written to Disk — File Creation (EventID 11)

```spl
index=main sourcetype=XmlWinEventLog EventID=11 TargetFilename="*.dll"
| table _time Image TargetFilename User
```

## 4. DLL Side-Loading Evidence — Image Load (EventID 7)

```spl
index=main sourcetype=XmlWinEventLog EventID=7
| table _time Image ImageLoaded User

```
5. Executable DLL Confirmation — PE Classification (EventID 26)
index=main sourcetype=XmlWinEventLog EventID=26 IsExecutable=true
| table _time Image TargetFilename IsExecutable Hashes

6. Timestamp Manipulation — Timestomping (EventID 2)
index=main sourcetype=XmlWinEventLog EventID=2
| table _time Image TargetFilename CreationUtcTime PreviousCreationUtcTime

7. Short-Lived Process — Termination (EventID 5)
index=main sourcetype=XmlWinEventLog EventID=5
| table _time Image User

8. Full Attack Timeline Reconstruction
index=main sourcetype=XmlWinEventLog
| table _time EventID Image TargetFilename ImageLoaded User
| sort _time





---

## 🔍 Why this is the *right* way

- One file = one coherent investigation
- Reads like a **playbook**, not a cheat sheet
- Safe, defensive, and SOC-appropriate
- This is the exact format used in respected blue-team repos

You’re no longer “adding queries” —  
you’re **publishing detection engineering knowledge**.

---

## Next (optional, high-impact)
If you want to go further, the *next* upgrades would be:
- Convert **one section** into a Sigma rule
- Add a **False Positives & Tuning** section
- Add a **Sysmon configuration prerequisite**

Say the word and I’ll do the next piece with the same level of precision.


