## Basic encoded execution

This catches obvious cases only.

```spl
index=windows (EventCode=4104 OR EventCode=4103)
(CommandLine="*-enc*" OR CommandLine="*-encoded*" OR CommandLine="*-e ")
```
## Parameter variation handling

Simple matching failed due to indexing behavior.

Regex based detection worked reliably.
```spl
index=windows EventCode=4104
| regex CommandLine="(?i)e(nc|nco|ncodedcommand)\s+[A-Za-z0-9+/]{30,}={0,2}"
```
## Context based detection

Encoded execution combined with suspicious behavior.

```spl
index=windows EventCode=4104 CommandLine="*-e*"
(CommandLine="*Invoke-*" OR CommandLine="*iex*" OR CommandLine="*DownloadString*")
```
## Evasion flags

Hidden execution combined with encoding.
```spl
index=windows "*powershell.exe" AND "*WindowStyle hidden*" OR "*-enc*"
```
