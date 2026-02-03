## Lab environment

The lab setup was intentionally simple.

- One Windows system
- PowerShell logging enabled
- Logs forwarded to Splunk Enterprise

Enabled PowerShell events:
- 4104 ScriptBlock logging
- 4103 Module logging
- 400 Engine start
- 800 Module loading

Not available in this lab:
- Event 4688 process creation
- Sysmon
- Network telemetry
- EDR tooling

This matters because many environments operate with similar visibility.  
Detection logic here reflects those limitations.
