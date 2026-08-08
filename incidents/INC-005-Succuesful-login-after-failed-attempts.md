# Incident Report – SSH Brute Force with Successful Login

## Date

2026-08-08 14:46:01 IST

## Severity

Critical

## Status

Resolved

## Affected Host

Debian Linux

## Splunk Alert

**Successful Login After Multiple Failed Logins**

## MITRE ATT&CK

- **T1110 – Brute Force**

## Description

The alert detected multiple failed SSH login attempts from a single source IP address followed by a successful login. This can indicate that an attacker successfully guessed or obtained the target account credentials.

## Evidence

### Alert Screenshot

![attack](/screenshots/SSH-brute-force-successful-login/Alert%20fired%20Successfully.png)


### SPL Query

```spl
index=* host=linux ("Failed password" OR "invalid") | stats count as failed_attempts by source_ip, | where failed_attempts > 5 | join type=inner source_ip [ search host=linux "Accepted password" | stats count as successful_logins by source_ip ] | table source_ip, failed_attempts, successful_logins
