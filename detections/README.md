# Detection Logic

This folder contains **defensive detection logic** related to DLL hijacking and DLL side-loading activity on Windows systems.

The focus is on:
- Identifying suspicious DLL load behavior
- Highlighting risky execution paths
- Closing visibility gaps between process execution and module loading

## Intended Use

All content here is intended for:
- SOC analysts
- Detection engineers
- Blue team practitioners

This repository does **not** provide exploitation steps or malware development guidance.

## Detection Focus Areas

- DLLs loaded from user-writable directories
- Unsigned or unknown DLLs loaded by signed executables
- Rare or first-seen DLL names
- Short-lived processes with abnormal module loads

## Telemetry Sources

Examples of relevant telemetry include:
- Sysmon Event ID 7 (Image Loaded)
- Sysmon Event ID 11 (File Create)
- Sysmon Event ID 1 (Process Create)

Detection logic may be expressed using:
- Sigma rules
- SIEM queries (e.g., Splunk)
- Behavioral heuristics

---

Detection logic is intentionally conservative and designed to support investigation, not replace analyst judgment.
