# IP Scanning on a specific Subnet

## Query Information


### Description
This KQL query aims to detect any machine on the network performing scanning recon scans. 

### Usage
Customise the RemotePortCount to speicific need. As IP scans will typically scan a large number of ports the higher 
the RemotePortCount number the less likely a scan will be detected. 

### References


## Defender For Endpoint
```
//Query that searches for network scanning tools such as Angry IP Scanner and Softperfect Network Scanner
let RemotePortCount = 100;
DeviceNetworkEvents
//| where Timestamp >= ago(1d)
| where RemoteIP contains "10.0.11"
//Customise below to exclude IT mangment tools such as lansweeper if used regularly
| where DeviceName !contains "lanswe"
| where InitiatingProcessIntegrityLevel contains "Medium" or InitiatingProcessIntegrityLevel contains "high"
| project Timestamp, ActionType, ReportId, DeviceName, DeviceId, Protocol, InitiatingProcessCommandLine, InitiatingProcessAccountUpn, RemotePort, LocalPort
| summarize arg_max( InitiatingProcessAccountUpn, Timestamp, DeviceId, ActionType, ReportId,  Protocol , InitiatingProcessCommandLine, RemotePort, LocalPort ),
  ActionType = count()
  by DeviceName
| where ActionType1 > RemotePortCount


```

