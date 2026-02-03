# DLL Hijacking Detection: Theory, Evidence, and Telemetry

DLL hijacking continues to succeed because most detection strategies focus on **what executed**, not **what was loaded**.

This repository documents the defensive analysis, real telemetry, and detection considerations required to identify DLL hijacking and DLL side-loading activity on Windows systems.

## Why This Matters

DLL hijacking does not exploit a vulnerability in the traditional sense.  
It abuses expected Windows DLL search behavior — often without triggering alerts.

When trusted executables load attacker-controlled DLLs from user-writable paths, defenders frequently miss it because:
- Module load events are not monitored
- DLL paths are not validated
- Signed processes are implicitly trusted

This repository exists to close that gap.

---

## Analysis Articles

This work is documented in two parts:

### Part 1 — Theory
**DLL Hijacking Still Works in 2025 and That’s a Problem**  
Conceptual analysis of why DLL hijacking persists and where defenders fail.

🔗 [*DLL Hijacking Still Works*](https://medium.com/system-weakness/dll-hijacking-still-works-in-2025-and-thats-a-problem-d12cdef6ddbd)

### Part 2 — Evidence
**37 Sysmon Events. One Complete DLL Hijacking Attack. Here's What Happened.**  
Event-by-event analysis of a real DLL sideloading attack using Sysmon telemetry.

🔗 [*37 Sysmon Events.*](https://medium.com/system-weakness/37-sysmon-events-one-complete-dll-hijacking-attack-heres-what-happened-09076f2e38c5)

Theory → Evidence → Detection.

---

## What You’ll Find in This Repository

- Defensive analysis of DLL hijacking behavior
- Sysmon event interpretation and correlations
- Detection logic examples (Sigma / SIEM-focused)
- Guidance on what defenders should monitor — and why

This repository intentionally avoids exploitation mechanics.

---

## Detection Philosophy

Effective detection focuses on:
- **DLL load location**
- **Signer trust mismatch**
- **Behavioral rarity**
- **Execution context**

DLL hijacking thrives in environments where module loading is not baselined.

---

## Repository Structure

```text
.
├── README.md
├── Detections/
│   └── README.md
├── False_Positives/
    └── README.md
