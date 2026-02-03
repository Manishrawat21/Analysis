# PowerShell Encoded Command Detection

This section focuses on detecting PowerShell encoded command execution based on **actual log behavior**, not theory alone.

The work here is split between **theoretical understanding** and **practical lab testing**. The theory explains *why* attackers use encoding. The lab work shows *how it really looks* once logs hit a SIEM.

This repository contains the practical side. The theory is documented separately.

---

## Background

PowerShell encoded commands are commonly used to:
- Hide intent from command line logging
- Bypass simple keyword based detections
- Obfuscate payloads delivered through phishing or loaders

The challenge is not identifying encoding itself, but **distinguishing malicious use from legitimate automation**.

---

## How this research was done

Testing was performed in a local lab using:
- Windows host
- PowerShell logging enabled
- Splunk Enterprise for log analysis

PowerShell events analyzed:
- 4104 ScriptBlock logging
- 4103 Module logging
- 400 Engine start
- 800 Module loading

No Sysmon, no EDR telemetry, and no advanced correlation.  
This reflects what many environments actually have available.

---

## Practical findings

### Parameter obfuscation breaks simple detection

One key finding was how variations such as mixed case parameters bypass naive queries.

Examples:
- `-EncodedCommand`
- `-enc`
- `-e`
- `-eNcO`

Splunk tokenizes command line data in a way that makes literal string matching unreliable. Detection logic must account for this behavior.

---

### Why regex matters

Keyword matching alone failed during testing.

Regex based detection proved more reliable for:
- Catching parameter variations
- Handling tokenization issues
- Reducing missed detections

Example approach:
- Look for encoded parameters
- Combine with suspicious command context
- Filter known benign automation

---

### Encoded PowerShell execution stages

Encoded PowerShell execution appears in layers:

1. Raw encoded command in execution context  
2. Decoded but still obfuscated content in ScriptBlock logs  
3. Final resolved command PowerShell actually runs  

Visibility into ScriptBlock logging is critical for understanding intent.

---

## Detection approach used here

The detections in this repository focus on:
- Encoded command execution combined with suspicious functions
- Use of evasion flags such as hidden windows or no profile
- Context over standalone indicators
- False positive reduction based on observed behavior

Example detections include:
- Regex based encoded parameter matching
- Encoded commands combined with `Invoke-Expression`
- Encoded commands attempting to download content

---

## False positives to expect

Encoded PowerShell is not always malicious.

Common legitimate sources include:
- Administrative automation
- Software deployment tools
- RMM and management agents
- Developer scripts

Each detection should be tuned against known baseline activity.

---

## Related write ups

The theoretical background and deeper discussion are documented in a separate Medium article.

- **Theory:** [Why attackers rely on PowerShell encoding and how obfuscation works](https://medium.com/system-weakness/powershell-encoded-commands-why-attackers-love-it-and-how-we-hunt-it-ff680f5c8c35)  
- **Practice:** What actually appears in logs and how to detect it effectively  

---

## Notes

All queries and detection logic are starting points.  
They must be adapted to your environment, logging coverage, and threat model.

This work is based on real lab testing and will continue to evolve as new techniques are tested.
