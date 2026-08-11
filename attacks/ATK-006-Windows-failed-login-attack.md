## Purpose

To simulate local interactive authentication failures (Logon Type 2) to verify that Splunk successfully detects and alerts on unauthorized physical access attempts or local brute-force activity.

## Commands Used 

To generate the failed type 2 logins logs we need to manually type the wrong password at the lock screen.

## Target

OS : Windows 11

## Expected Detection 

Splunk should ingest Windows Security Event ID 4625 (An account failed to log on) specifically containing Logon Type: 2, along with the targeted account name and the time of the attempt.

## Actual Detection 

The Splunk successfully fired the alert, capturing Event ID 4625, confirming the Logon Type was 2, and identifying the targeted user account.

## Screenshots

#### Alert

![alert](/screenshots/Windows-failed-login-type-2/Triggered-Alerts.png)

#### Event

![Event](/screenshots/Windows-failed-login-type-2/Event.png)


## MITRE Mapping 

Tactic : Credential Access

Technique : T1110 – Brute Force

Procedure : T1110.001 – Password Guessing (Adversaries may use password guessing to attempt to gain access to local accounts via physical or local interactive console access).



