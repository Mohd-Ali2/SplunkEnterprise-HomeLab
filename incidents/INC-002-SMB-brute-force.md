# Incident Report – SMB Brute Force Detection

## Date

2026-08-10 11:01:50.947 IST

## Severity

High

## Status

Resolved 

## Affected Host

Windows 11

## Splunk Alert

**SMB Brute Force Attempts**

## MITRE ATT&CK

**T1110 – Brute Force**

## Description

The alert triggered when multiple failed SMB authentication were performed within a short period of time indicating possible brute force.

## Evidence

### Alert Screenshot

![Alert](/screenshots/SMB-brute-force/Alert-Triggerd.png)

### SPL Query

```spl
index=* host="HP-Pavilion" sourcetype="WinEventLog:Security" Logon_Type=3 EventCode=4625 Logon_Type=3 | stats count as Failed_smb_logins by Source_Network_Address | where Failed_smb_logins > 3
```

### Raw Log Snippet

```text
08/10/2026 11:01:50.947 AM
LogName=Security
EventCode=4625
EventType=0
ComputerName=HP-Pavilion
Source_Network_Address = 192.168.31.185host = HP-Pavilionsource = WinEventLog:Securitysourcetype = WinEventLog:Security
```

**Log Source**

- Host : Windows 11
- Source : Windows Security Event Log
- Event ID : 4625
- Logon Type : 3
- Username : `admin`
- Source Ip : 192.168.31.185
- Failed attempts : 11

## Response Actions Taken

- Verified the alert in Splunk.
- Confirmed multiple failed SMB authentication attempts from the Kali IP.
- Reviewed the Windows Security events.
- Confirmed the activity was part of the controlled lab simulation.
- Recorded the activity as a true positive.

## Conclusion

The detection successfully identified the simulated SMB brute-force attack and generated the expected alert. The incident was investigated and confirmed as a true positive.
