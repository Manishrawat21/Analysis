***SOC Breakdown: Event ID 2 ***

- Records when a file’s creation timestamp is modified.

***Things you should look for :-***

- Image (The process that modified the file timestamp)
- TargetFilename (The file whose timestamp was changed)
- PreviousCreationUtcTime (Original creation time of the file)
- CreationUtcTime (Modified creation time of the file)
- ProcessId (Unique identifier to track the process activity)

***SPL***
```
index=apt29 EventID=2
| table _time, TargetFilename, PreviousCreationUtcTime, CreationUtcTime, Image, ProcessId
| sort _time
```
***Detection***

- Timestamp modification (timestomping) is often used to hide malicious files by making them appear legitimate or older than they actually are.

I'm going to soon publish Sigma detection rules based on these patterns.

Follow along if you're into SOC / threat hunting.
