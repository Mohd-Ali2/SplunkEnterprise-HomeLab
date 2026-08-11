# Linux Cron Persistence Detection

## Description

Detects unauthorized modifications to Linux cron jobs, specifically identifying attempts to establish persistence by injecting reverse shells or malicious scripts (using parameters like @reboot or /dev/tcp) directly into the user's crontab.

## MITRE ATT\&CK 

T1053.003 - Scheduled Task/Job: Cron

## Severity

Medium

## Data Source

`Linux Syslog / Auth logs (/var/log/syslog, /var/log/auth.log)`

`Linux Auditd (audit.log)`

`Sysmon for Linux (Event ID 1: Process Creation)`

`Splunk Universal Forwarder`


## SPL Query 

```
index=* EventCode=4625 Logon_Type=2
| stats count min(_time) as firstTime max(_time) as lastTime by Account_Name, ComputerName
| where count >= 3
| convert ctime(firstTime) ctime(lastTime)
| rename ComputerName AS "Target Host", Account_Name AS "Targeted Account", count AS "Failed Attempts", firstTime AS "First Attempt", lastTime AS "Last Attempt"
```

## Expected Output 

The detection should return a direct hit showing the exact moment the crontab command was executed. The output will display a clean table containing the Target Host, the Compromised User (e.g., root or a standard user), and the full Malicious Command string showing the reverse shell payload and the @reboot scheduling parameter.

## MITRE Technique Mapping

**Tactic** : 
Persistence, Execution

**Technique** : 
T1053.003 – Scheduled Task/Job: Cron

**Procedure** : 
An adversary pipes a malicious reverse shell payload (bash -i >& /dev/tcp/...) into the crontab utility, scheduling it to execute automatically upon system startup (@reboot) to maintain persistent remote access to the compromised Linux host.

## True Positives

During the lab simulation, a malicious one-liner was executed on the target Linux machine to append a reverse shell payload to the current user's crontab. The Splunk detection successfully identified the execution, capturing the suspicious command-line arguments (@reboot, /dev/tcp, bash -i) and identifying the compromised user and host, confirming the alert logic is functioning exactly as intended.



