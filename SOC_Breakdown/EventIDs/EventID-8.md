***SOC Breakdown: EventID=8***
- Records when a process creates a thread in another process.

***Things you should look for :-***
- SourceImage (The process that is creating the remote thread)
- TargetImage (The process where the thread is being injected)
- StartModule (The module from which the thread starts execution)
- StartFunction (The function where execution begins)
- RuleName (Indicates if a detection rule was triggered)

***SPL***
```
index=apt29 EventID=8
| table _time, SourceImage, TargetImage, StartModule, StartFunction
| sort _time
```
***Detection***

Creating threads in other processes is commonly used for process injection, which attackers use to execute malicious code inside legitimate processes.

I'm going to soon publish Sigma detection rules based on these patterns.
Follow along if you're into SOC / threat hunting.
