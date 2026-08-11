## Date 

8-11-26 1:57:53.754 IST

## Severity 

High

## Status 

Resolved

## Affected Host 

OS : Windows 11 

Host : HP-Pavalion

## MITRE ATT\&CK 

Tactic : Credential Access

Technique : T1110 – Brute Force

Procedure : T1110.001 – Password Guessing (Adversaries may use password guessing to attempt to gain access to local accounts via physical or local interactive console access).

## Splunk Alert 

Windows Failed Logins Detected Logon Type 2


## Description 

Detects multiple failed local interactive logon attempts (Logon Type 2) on a Windows host within a short timeframe. This activity indicates a potential local brute-force attack, password guessing, or unauthorized physical console access to the endpoint.


## Evidence

The Splunk alert successfully triggered after detecting 4 consecutive local authentication failures on the target machine within a 15-minute window, exceeding the established threshold of 3 attempts.

#### Alert Screenshot 

![alert](/screenshots/Windows-failed-login-type-2/Triggered-Alerts.png)

#### Event Screenshot

![event](/screenshots/Windows-failed-login-type-2/Event.png)

## SPL Query used

```
index=* EventCode=4625 Logon_Type=2
| stats count min(_time) as firstTime max(_time) as lastTime by Account_Name, ComputerName
| where count >= 3
| convert ctime(firstTime) ctime(lastTime)
| rename ComputerName AS "Target Host", Account_Name AS "Targeted Account", count AS "Failed Attempts", firstTime AS "First Attempt", lastTime AS "Last Attempt"
```

## Raw log snippet

```
8/11/26
1:57:53.754 PM	
08/11/2026 01:57:53.754 PM
LogName=Security
EventCode=4625
EventType=0
ComputerName=HP-Pavilion
Show all 61 lines
Source_Network_Address = 127.0.0.1host = HP-Pavilionsource = WinEventLog:Securitysourcetype = WinEventLog:Security
```

## Response Action Taken

Since this was a controlled lab simulation, the following incident response steps were outlined and validated:

Investigation: Reviewed the Splunk alert to confirm the targeted machine (HP-Pavilion) and verify that the 4 failed attempts were highly concentrated in time.

Verification: Correlated the timestamps to determine if this was a known authorized user repeatedly mistyping their password, or a true unauthorized physical access attempt.

Tuning: Confirmed the Splunk alert logic correctly aggregated the raw logs into a single actionable ticket, proving the where count >= 3 threshold prevents alert fatigue.

## Conclusion

This lab successfully demonstrated the ability to monitor and alert on local brute-force attacks. By correlating Windows Event ID 4625 with Logon_Type=2 and applying a threshold, the SIEM effectively detected unauthorized interactive logon attempts while filtering out normal user typos.


