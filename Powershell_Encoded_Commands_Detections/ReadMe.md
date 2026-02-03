# PowerShell Encoded Command Detection

This repository documents practical detection research around encoded PowerShell execution based on hands on testing in a small Splunk lab.

The goal is not to explain what encoded commands are. The goal is to show how they actually appear in logs, where basic detections fail, and what worked after testing.

This work is based on direct observation rather than theory.

## What this repo covers

- How encoded PowerShell commands are logged in practice
- Why simple string matching fails for parameter variations
- Detection logic that worked in Splunk
- False positives observed during testing
- A portable Sigma rule based on lab results

## What this repo is not

- Not malware
- Not red team tooling
- Not copy pasted documentation

Everything here is defensive and detection focused.

## Reference

This repo is based on lab work documented in a longer write up on Medium.  
The GitHub version focuses on clarity and reuse.
