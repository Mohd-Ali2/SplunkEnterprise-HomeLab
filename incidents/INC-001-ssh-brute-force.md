# Incident Report – SSH Brute Force Detection

## Date

2026-08-04 15:51:00 IST

## Severity

Medium

## Status

Resolved

## Affected Host

Debian Linux

## Splunk Alert

**Alert SSH Brute Force Detected (Linux)**

## MITRE ATT&CK

- **T1110 – Brute Force**

## Description

The alert detected multiple failed SSH login attempts from a single source IP address within a short period of time, indicating a possible brute-force attack.

## Evidence

### Alert Screenshot

![Alert](/screenshots/SSH-brute-force-linux/Alert-for-SSH-brute-force-attack.png)

### SPL Query

```spl
index=* host="linux" ("Failed password" OR "invalid")
| stats count as failed_attempts by source_ip
| where failed_attempts > 5
| sort - failed_attempts
```

### Raw Log Snippet

```text
2026-08-04T10:20:35.561779+00:00 linux sshd-session[4264]:
Connection closed by invalid user Admin 192.168.31.185 port 47174 [preauth]
```

**Log Source**

- Host: linux
- Source: `/var/log/auth.log`
- Sourcetype: `linux_secure`
- Username: `Admin`

## Response Actions Taken

- Verified the alert in Splunk.
- Confirmed multiple failed SSH authentication attempts from `192.168.31.185`.
- Confirmed that no successful SSH login occurred during the attack.
- Recorded the activity as a **true positive** generated during the lab simulation.

## Conclusion

The detection successfully identified the simulated SSH brute-force attack and generated the expected alert. The incident was investigated and confirmed as a true positive.
