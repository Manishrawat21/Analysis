# False Positives – DLL Hijacking Detection

DLL hijacking detections can generate noise if context is ignored.

This section documents **legitimate software behavior** that may resemble DLL search order hijacking and explains how to distinguish it from malicious activity.

---

## Common Legitimate Sources

The following applications may load DLLs from user-writable or non-standard paths during normal operation:

- Google Chrome
- Visual Studio Code
- Python-based applications
- Electron applications
- Self-updating software frameworks

These applications often extract or load components dynamically, especially during updates or plugin execution.

---

## Why These Trigger Detections

False positives typically occur due to:

- DLLs loaded from `%TEMP%` or user profile directories
- Legitimate applications bundled with unsigned DLLs
- Short-lived processes extracting runtime dependencies
- Developer tools executing binaries outside `Program Files`

This behavior alone does **not** indicate malicious activity.

---

## How to Reduce False Positives

Consider the following context before escalating:

- **Parent process reputation** (browser, IDE, updater)
- **Execution frequency** (one-time vs repeated)
- **DLL naming patterns** (generic Windows DLL names in odd locations)
- **Process ancestry** (user-initiated vs system-launched)
- **Digital signature consistency**

DLL hijacking becomes suspicious when **multiple indicators align**, not from a single event.

---

## SOC Guidance

DLL hijacking detections should be treated as **investigation triggers**, not standalone alerts.

Effective detection requires:
- Baseline-aware monitoring
- Correlation with process execution events
- Awareness of developer and productivity tools

Noise reduction is a detection strength, not a weakness.
