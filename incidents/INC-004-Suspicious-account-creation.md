# Unauthorized Account Creation 

## Date

## Severity 

High

## Status 

Resolved

## Affected Host 

Windows 11

## MITRE ATT\&CK 

T1136.001 – Create Account: Local Account

Tactic: Persistence

Description: Creating a new local user account to maintain persistent access to the system.

T1098 – Account Manipulation

Tactic: Persistence, Privilege Escalation

Description: Adding the rogue account to the Administrators group to gain elevated execution rights.

## Splunk Alert 



## Description

Detects the unauthorized creation of a local user account and its assignment to the Administrators group to establish privileged persistent access.


## Evidence

#### Alert Screenshot 

#### Event Screenshot


## SPL Query used 


## Raw log snippet

## Log Source

## Response Action Taken

## Conclusion 
