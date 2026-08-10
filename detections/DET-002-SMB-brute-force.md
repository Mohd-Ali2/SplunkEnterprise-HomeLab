# SMB Brute Force Detection

## Description

Detects multiple failed SMB authentication attempts from the same source IP address within a short time period.

## Data Source

- Windows Security Event Log
- Event ID 4625
- Logon Type 3

## Detection Logic

If multiple failed network logon attempts are observed from the same source IP address, the detection generates an alert for possible SMB brute-force activity.

## SPL Query

See:

`spl/SMB-brute-force.spl`

## MITRE ATT&CK

- T1110 - Brute Force

## Investigation

- Source IP address : 192.168.31.185
- Target username : admin
- Number of failed login attempts : 11
- Target host : Windows 11
- Logon Type : 3

## True Positive

During this lab, CrackMapExec was used from the Kali attacker machine to generate multiple failed SMB authentication attempts against the Windows 11 endpoint.

The detection successfully identified the activity.

- Source IP : 192.168.31.185
- Username : admin
- Failed Attempts : 11

## Recommended Response

- Verify whether the source IP is authorized.
- Check the targeted account for successful logins.
- Review other Windows authentication events from the same IP.
- Block the source IP if the activity is malicious.
- Continue monitoring for further authentication attempts.
