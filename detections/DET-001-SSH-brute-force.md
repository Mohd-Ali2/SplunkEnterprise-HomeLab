# SSH Brute Force Detection

## Description

Detects multiple failed SSH login attempts from the same source IP address within a short time period.

## Data Source

- Linux: `/var/log/auth.log`

## Detection Logic

If more than 5 failed SSH login attempts are observed from the same source IP address within 15 minutes, an alert is generated.

## SPL Query

See:

`spl/SSH-brute-force-linux.spl`

## MITRE ATT&CK

- T1110 - Brute Force

## Investigation

- Source IP address : 192.168.31.185
- Target username : Admin
- Number of failed login attempts : 8
- Target host : Linux Debian
- Whether a successful login occurred afterwards : False

## True Positive Example

During this lab, a custom Python script was executed from the Kali attacker machine against the Debian SSH service.

The detection successfully identified:

- Source IP: 192.168.31.185
- Username: admin
- Failed Attempts: 14

## Recommended Response

- Verify whether the source IP is authorized.
- Check if any login attempts were successful.
- Block the attacking IP if the activity is malicious.
- Continue monitoring for additional authentication attempts.
