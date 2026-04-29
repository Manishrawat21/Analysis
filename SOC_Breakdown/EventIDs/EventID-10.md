***SOC Breakdown: Event ID 10***
- Records when a process attempts to access or interact with another process.

***Things you should look for :-***
- SourceImage (The process attempting to access another process)
- TargetImage (The process being accessed, e.g., lsass.exe)
- GrantedAccess (Level of access requested — high privileges can be suspicious)
- CallTrace (Shows the sequence of function calls involved in the access)

***SPL***
```
index=apt29 EventID=10
| table _time, SourceImage, TargetImage, GrantedAccess, CallTrace
| sort _time
```
***Detection***

Access to sensitive processes like lsass.exe may indicate credential dumping or memory scraping activity.
