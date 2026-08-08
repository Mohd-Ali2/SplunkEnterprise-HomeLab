# Successful SSH Login After Multiple Failed Attempts Detection

## Description

Detects multiple failed SSH login attempts from the same source IP address followed by a successful login within a short time period.

## Data Source

- Linux: `/var/log/auth.log`

## Detection Logic

If multiple failed SSH login attempts are observed from the same source IP address and a successful SSH login occurs afterwards, an alert is generated.

## SPL Query

See:

`spl/Successful-Login-after-multiple-failed-attempts.spl`

## MITRE ATT&CK

- T1110 - Brute Force

## Investigation

- Source IP address : 192.168.31.185
- Target username : Admin
- Number of failed login attempts : 8
- Target host : Linux Debian
- Successful login occurred afterwards : True

## True Positive

During this lab, a custom Python script was used from the Kali attacker machine to generate multiple failed SSH login attempts against the Debian SSH service. A valid SSH login was then performed from the same source IP.

The detection successfully identified the failed attempts followed by the successful login.

- Source IP: 192.168.31.185
- Username: Admin
- Failed Attempts: 8
- Successful Login: Yes

## Recommended Response

- Verify whether the successful login was authorized.
- Review the account and source IP activity.
- Check what actions were performed after the successful login.
- Block the source IP if the activity is confirmed as malicious.
- Reset the affected account credentials if compromise is suspected.
