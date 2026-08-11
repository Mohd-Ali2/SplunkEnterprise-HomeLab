# Multiple Failed logins from Windows type 2

## Description

Detects multiple failed local interactive authentication attempts (Logon Type 2) originating from the physical console or local command prompts.


## MITRE ATT\&CK 

T1110 – Brute Force

Tactic: Credential Access

Description: Attempting to systematically guess passwords to gain unauthorized access to a system or account.

T1110.001 – Password Guessing

Tactic: Credential Access

Description: Repeatedly guessing a local user's password via the physical keyboard or local interactive prompts (Logon Type 2) to establish access.

## Severity

High

## Data Source

Host : Windows 11
Source : WinEventLog:Security

## SPL Query 

```
index=* EventCode=4625 Logon_Type=2
| stats count min(_time) as firstTime max(_time) as lastTime by Account_Name, ComputerName
| where count >= 3
| convert ctime(firstTime) ctime(lastTime)
| rename ComputerName AS "Target Host", Account_Name AS "Targeted Account", count AS "Failed Attempts", firstTime AS "First Attempt", lastTime AS "Last Attempt"
```

## Expected Output 

The detection should return a consolidated alert when a user fails to log in locally 3 or more times. By aggregating Windows Security Event ID 4625 (Logon Type 2), the output will display a clean table showing the Target Host, the Targeted Account (Account_Name), the total number of Failed Attempts, and the timestamps for the first and last failed attempts.

## MITRE Technique Mapping

**Tactic**
Credential Access

**Technique**
T1110.001 – Brute Force: Password Guessing

**Procedure**
An adversary or insider threat with physical access—or local console access—attempts to systematically guess a user's password to gain unauthorized access to the endpoint, resulting in multiple interactive authentication failures.

## True Positives

During the lab simulation, 4 interactive failed login attempts were manually generated within a 15-minute window (between 1:30 PM and 1:45 PM). The Splunk detection rule successfully triggered, aggregating the 4 individual 4625 events into a single alert. It correctly identified the targeted host (HP-Pavilion), the targeted Account_Name, and confirmed that the activity crossed the brute-force threshold, validating that the detection logic works as intended.



