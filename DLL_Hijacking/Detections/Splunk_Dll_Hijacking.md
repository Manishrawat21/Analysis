# Splunk Detection Queries: DLL Hijacking Analysis

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
## 5. Executable DLL Confirmation — PE Classification (EventID 26)

```spl
index=main sourcetype=XmlWinEventLog EventID=26 IsExecutable=true
| table _time Image TargetFilename IsExecutable Hashes
```

## 6. Timestamp Manipulation — Timestomping (EventID 2)

```spl
index=main sourcetype=XmlWinEventLog EventID=2
| table _time Image TargetFilename CreationUtcTime PreviousCreationUtcTime
```

### 7. Short-Lived Process — Termination (EventID 5)

```spl
index=main sourcetype=XmlWinEventLog EventID=5
| table _time Image User
```

## 8. Full Attack Timeline Reconstruction

```spl
index=main sourcetype=XmlWinEventLog
| table _time EventID Image TargetFilename ImageLoaded User
| sort _time
```




