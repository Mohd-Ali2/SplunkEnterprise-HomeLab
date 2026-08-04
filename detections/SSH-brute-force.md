# SSH Brute Force Detection

## Detection Information

| Field | Value |
|-------|-------|
| Detection Name | SSH Brute Force Detection |
| Rule ID | DET-001 |
| Severity | High |
| Status | Enabled |
| Platform | Linux |
| Data Source | /var/log/auth.log |
| MITRE ATT&CK | T1110 - Brute Force |

---

## Objective

Detect multiple failed SSH authentication attempts originating from a single source IP address within a defined time window to identify potential brute-force attacks.

---

## Detection Logic

This detection monitors Linux authentication logs for repeated SSH login failures. If more than **5 failed login attempts** are observed from the same source IP address within **15 minutes**, the alert is triggered.

---

## SPL Query

See:

```text
spl/SSH-brute-force-linux.spl
```

---

## Expected Output

The alert should return:

- Timestamp
- Source IP
- Username
- Host
- Number of failed login attempts

Example:

| Source IP | Username | Attempts |
|-----------|----------|----------|
| 192.168.31.185 | admin | 14 |

---

## MITRE ATT&CK Mapping

| Category | Value |
|----------|-------|
| Tactic | Credential Access |
| Technique | Brute Force |
| Technique ID | T1110 |

---

## Investigation Guide

When this alert triggers:

1. Identify the attacking IP address.
2. Determine the targeted username(s).
3. Count the number of failed authentication attempts.
4. Check whether a successful login occurred afterwards.
5. Review authentication activity from the same IP on other systems.
6. Determine whether the activity is authorized (penetration test) or malicious.

---

## Possible False Positives

- User repeatedly entering an incorrect password.
- Automated vulnerability scanners.
- Internal penetration testing.
- Misconfigured automation scripts.

---

## Recommended Response

- Block or rate-limit the attacking IP address.
- Reset credentials if compromise is suspected.
- Enable Multi-Factor Authentication (MFA).
- Review authentication logs for lateral movement.
- Continue monitoring for additional attempts.
