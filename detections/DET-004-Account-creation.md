# Unauthorized Account Creation

## Description

Detect the unauthorized creation of a local user account and its addition to the Administrators group, a technique commonly used by adversaries to establish privileged persistence on a compromised host.

## MITRE ATT\&CK 

**T1136.001** – Create Account : Local Account

**T1098** – Account Manipulation (Adding user to the Administrators group)

**T1059.001** – Command and Scripting Interpreter : PowerShell

## Severity

High

## Data Source

`Windows Security Event Logs (Event IDs 4720, 4732)`

`Windows Sysmon / Operational (Event ID 1 - Process Creation)`

`Splunk Universal Forwarder`

## SPL Query 

## Expected Output 

The detection should return Windows Security Event ID 4720 (A user account was created) and Event ID 4732 (A member was added to a security-enabled local group).


## MITRE Technique Mapping

* **Tactic:** Persistence
  * **Technique:** T1136.001 – Create Account: Local Account
  * **Procedure:** An adversary creates a new local user account on the compromised host to establish and maintain persistent access.

* **Tactic:** Persistence, Privilege Escalation
  * **Technique:** T1098 – Account Manipulation
  * **Procedure:** The adversary adds the newly created rogue account to the local `Administrators` group to ensure elevated execution rights.

## True Positives

The detection successfully identified the unauthorized account creation and privilege assignment, confirming the rule is functioning as expected and the Splunk pipeline is correctly ingesting Windows Security Event logs.



