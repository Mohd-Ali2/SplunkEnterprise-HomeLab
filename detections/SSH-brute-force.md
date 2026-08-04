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

When this alert triggers, verify:

- Source IP address
- Target username
- Number of failed login attempts
- Target host
- Whether a successful login occurred afterwards

## True Positive Example

During this lab, a custom Python script was executed from the Kali attacker machine against the Debian SSH service.

The detection successfully identified:

- Source IP: 192.168.31.185
- Username: admin
- Failed Attempts: 14


## Possible False Positives

Although this lab generated a true positive, similar alerts could also be caused by:

- A user repeatedly entering an incorrect password.
- Internal penetration testing.
- Authorized vulnerability scanning.

## Recommended Response

- Verify whether the source IP is authorized.
- Check if any login attempts were successful.
- Block the attacking IP if the activity is malicious.
- Continue monitoring for additional authentication attempts.
