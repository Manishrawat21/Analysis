***SOC Breakdown: Event ID 1***

- Records the creation of a new process, including its command line, parent process, and execution context for security monitoring.

***Things you should look for :-***

- Image (The executable that was launched)
- CommandLine (The exact command used to start the process)
- ParentCommandLine (The command that initiated the parent process)
- ParentImage (The process that spawned this process)
- ProcessId (Unique identifier of the process, useful for tracking its lifecycle and correlating events)
- User (The account under which the process was executed)

***SPL***

```
index=apt29 EventID=1
| table _time, ParentImage, Image, CommandLine, User, ProcessId
| sort _time
```

***Detection***

I'm going to soon publish Sigma detection rules based on these patterns.

Follow along if you're into SOC / threat hunting.
