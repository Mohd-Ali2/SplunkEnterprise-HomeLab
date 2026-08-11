# Unauthorized Account Creation 

## Date

2026-08-11 12:53:01 IST

## Severity 

Medium

## Status 

Resolved

## Affected Host 

Windows 11

## MITRE ATT\&CK 

T1136.001 – Create Account: Local Account

Tactic: Persistence

Description: Creating a new local user account to maintain persistent access to the system.

T1098 – Account Manipulation

Tactic: Persistence, Privilege Escalation

Description: Adding the rogue account to the Administrators group to gain elevated execution rights.

## Splunk Alert 

`Windows Account Creation`


## Description

Detects the unauthorized creation of a local user account and its assignment to the Administrators group to establish privileged persistent access.


## Evidence

#### Alert Screenshot 

![alert](/screenshots/Account-creation/Triggered-Alerts.png)


#### Event Screenshot

![event](/screenshots/Account-creation/Event.png)


## SPL Query used 

```
index=* sourcetype=WinEventLog:Security EventCode=4720
| table _time ComputerName Account_Name SAM_Account_Name
```


## Raw log snippet

```
08/11/2026 12:52:00.407 PM
LogName=Security
EventCode=4720
EventType=0
ComputerName=HP-Pavilion
Show all 49 lines
host = HP-Pavilionsource = WinEventLog:Securitysourcetype = WinEventLog:Security
```

## Log Source

Host : HP-Pavalion
Source : WinEventLog:Security

## Response Action Taken

Upon verifying the alert as a True Positive, the following incident response actions were executed:
* **Containment:** Isolated the compromised host from the corporate network to prevent lateral movement.
* **Eradication:** Disabled and completely removed the rogue local account (`LabAdmin`) and revoked its local administrator privileges.
* **Credential Reset:** Forced an immediate password reset and revoked all active sessions for the compromised user (`SubjectUserName`) that was used to execute the PowerShell commands.
* **Investigation:** Initiated a full endpoint forensic scan to determine the initial access vector (e.g., malicious payload, phishing) that allowed the attacker to run commands in the first place.

## Conclusion

The detection rule successfully identified an adversary attempting to establish privileged persistence and escalate privileges on a compromised endpoint. By successfully correlating Windows Security Event IDs 4720 (Account Creation) and 4732 (Group Modification), the Splunk pipeline provided the SOC team with immediate visibility into the attack. This rapid detection allowed for swift containment, neutralizing the threat before the attacker could move laterally or exfiltrate data, fully validating the effectiveness of this detection logic.
