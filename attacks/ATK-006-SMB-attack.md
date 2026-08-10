## Purpose

To generate multiple failed authentication attempts against the windows endpoint and simulate the SMB brute force attack. The windows security events were forwarded to splunk.


## Commands Used

```
crackmapexec smb 192.168.31.113 -u admin -p /home/kali/Desktop/passlist.txt
```

## Target 

OS : Windows 11

Service Targeted : SMB

Protocol : SMB


## Expected Detection

The windows endpoint generates multiple failed network authentication events when invalid SMB credentials are used. The Splunk detection are expected to identify multiple failed logons attempts from the same IP source and trigger the SMB brute force alert.


## Actual Detection

The Splunk alert triggered successfully. Multiple failed SMB authentication attempts were detected from the Kali attacker machine against the Windows endpoint.

## Screenshots

#### Command Used

![command](screenshots/SMB-brute-force/Linux-Command.png)

#### Alert

![alert](screenshots/SMB-brute-force/Triggered-Alerts.png)


## MITRE Mapping 

**T1110 - Brute Force**



