***SOC Breakdown: EventID=7***

- Records when a process loads a module (such as a DLL) into memory.

***Things you should look for :-***

- Image (The process that is loading the module)
- ImageLoaded (The DLL or module being loaded into memory)
- Description (Details about the loaded module)
- Signature (Indicates if the file is digitally signed)
- SignatureStatus (Shows whether the signature is valid or not)

***SPL***
```
index=apt29 EventID=7
| table _time, Image, ImageLoaded, Description, Signature, SignatureStatus
| sort _time
```

***Detection***

- Loading of unsigned or unusual DLLs, especially from Temp or user directories, may indicate DLL injection or malicious code execution.

I'm going to soon publish Sigma detection rules based on these patterns.

Follow along if you're into SOC / threat hunting.
