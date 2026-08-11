## Purpose

To simulate unauthorized local account creation on the target machine to establish persistence and verify that Splunk detects user management events.

## Commands Used

`net user back4door @Password123 /add`

`net localgroup Administrators back4door /add`

## Target

OS : Windows 11

Target IP : 192.168.31.113

## Expected Detection

Splunk is expected to ingest Windows Security Event IDs 4720 and 4732 to successfully trigger an alert for unauthorized local administrator account creation.

## Actual Detection

he Splunk dashboard successfully fired the alert, capturing the exact timestamp, target host, and command-line execution used to create the rogue admin account.

## Screenshot

![alert](/screenshots/Account-creation/Account-creation-command.png)

## MITRE Mapping

**Persistence - Create Account (T1136) / Local Account (T1136.001)**
**Execution - Command and Scripting Interpreter (T1059) / PowerShell (T1059.001)**
