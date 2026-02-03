# Detection Engineering Notes and Analysis

This repository documents hands on detection research based on lab testing, log analysis, and real SOC workflows.

The focus is on how attacker techniques actually appear in logs, what detection logic works in practice, what fails, and where false positives are introduced. All content is written from a defensive perspective for analysts and detection engineers.

This is not offensive tooling or exploit development.

---

## What this repository contains

### DLL Hijacking and Side Loading

Analysis and detection notes for DLL hijacking and side loading activity on Windows systems.

Topics covered:
- How legitimate executables load malicious DLLs
- Common execution paths abused during side loading
- Correlation between process execution, file creation, and image load events
- Behavior based detection logic instead of file name matching
- False positives observed during real testing

Common false positives identified:
- Chrome and Chromium based applications
- Visual Studio Code
- Python executions
- Electron based desktop applications

The emphasis is on separating expected application behavior from activity that actually warrants investigation.

---

### PowerShell Encoded Command Detection

Research into how encoded PowerShell commands appear in logs and how attackers evade simple detections.

Includes:
- ScriptBlock and module logging behavior (4104, 4103, 400, 800)
- Why parameter obfuscation breaks keyword based detections
- Splunk queries that failed and why
- Regex based detection approaches
- Context driven detections to reduce noise
- Example Sigma style detection logic built from lab observations

All testing is performed with realistic telemetry rather than ideal enterprise setups.

---

## Detection philosophy

Effective detection is rarely about single indicators.

This repository focuses on:
- Behavioral correlation over static signatures
- Understanding how SIEM platforms index and tokenize data
- Reducing false positives before increasing alert volume
- Writing detections analysts can realistically investigate

Guiding question:
Would this detection survive in a real SOC environment?

---

## Who this repository is for

- SOC analysts
- Detection engineers
- Threat hunters
- Blue team practitioners tuning detections
- Security professionals learning how attacks surface in logs

---
## Open to Collaboration

Interested in working with teams on:
- Detection engineering frameworks
- Threat hunting operations
- SOC scaling and optimization

If you're solving hard detection problems, let's talk.

---

## Support the project

If you find this repository useful or learn something from it, consider giving it a star.  
It helps the research reach more analysts and encourages continued work.

---

## Connect and follow the work

GitHub  
https://github.com/Manishrawat21

LinkedIn  
https://www.linkedin.com/in/manishrawat-soc/

Medium  
[Detection write ups and lab based research](https://medium.com/@maxxrawat007)  

---

## Notes

All queries and detection logic are starting points and should be adapted to your environment.

This repository evolves as new detection research is added.
