# PowerShell Encoded Command Detected

## Description

Detect the execution of PowerShell with the `-EncodedCommand` parameter, which may indicate obfuscated PowerShell execution used to evade basic command-line detection.


## MITRE ATT&CK

**T1059.001** PowerShell  
**T1027** Obfuscated Files or Information

## Severity

Medium

## Data Source

- Windows Security / Sysmon
- Sysmon Event ID 1 – Process Creation
- Splunk Universal Forwarder


## SPL Query

```spl
index=* host="HP-Pavilion" sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1
Image="*\\powershell.exe"
(CommandLine="*-EncodedCommand*" OR CommandLine="*-enc*")
| table _time host User Image CommandLine ParentImage ParentCommandLine
```

## Expected Output


The detection should return Sysmon Event ID 1 process creation events where powershell.exe is executed with the -EncodedCommand parameter.


## MITRE Technique Mapping


**Tactic** : Execution

**Technique** : T1059.001 PowerShell

**Procedure** : An adversary may execute commands through PowerShell using the -EncodedCommand parameter to obfuscate the command and evade basic command-line detection.


## True Positve 

During this lab a Encoded PowerShell command was executed from attacker machine to generate the logs and fired the alert successfully. The alert was Triggered Successfully.

The detection successfully identified:

- Source IP: 192.168.31.185
- Encoded Command (base64)
  

