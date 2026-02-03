```spl
title: Suspicious PowerShell Encoded Command Execution
description: Detects encoded PowerShell execution combined with suspicious behavior
status: experimental
author: Manish Rawat

logsource:
  product: windows
  service: powershell

detection:
  encoded_execution:
    EventCode: 4104
    Message|contains:
      - enc
      - encoded
      - eNcO

  suspicious_context:
    Message|contains:
      - Invoke-Expression
      - iex
      - DownloadString
      - WindowStyle hidden
      - NoProfile

  filter_known:
    User|contains:
      - SYSTEM
      - ADMINISTRATOR

  condition: encoded_execution and suspicious_context and not filter_known

falsepositives:
  - Administrative automation
  - Software deployment tools
  - Remote management agents

level: high

tags:
  - attack.execution
  - attack.t1059.001
```
