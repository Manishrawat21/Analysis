***SOC Breakdown: EventID=3***

- Records when a process initiates a network connection, including source and destination details.

***Things you should look for :-***

- Image (The process initiating the network connection)
- Protocol (Type of connection used – TCP/UDP)
- SourceIp (Originating system IP address)
- SourcePort (Port used by the source system)
- DestinationIp (Target IP address the process is connecting to)
- DestinationPort (Port on the destination system)
- User (Account under which the connection was made)
- ProcessId (Unique identifier to track the process activity)

***SPL***
```
index=apt29 EventID=3
| table _time, Image, SourceIp, SourcePort, DestinationIp, DestinationPort, Protocol, User
| sort -_time
```
***Detection***

- Unusual outbound connections, especially to unknown or external IPs, may indicate command-and-control (C2) communication or data exfiltration.

I'm going to soon publish Sigma detection rules based on these patterns.
