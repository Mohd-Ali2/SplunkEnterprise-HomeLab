# Splunk Enterprise Investigation & Detection Home Lab

![Splunk](https://img.shields.io/badge/Splunk-Enterprise-green)
![Sysmon](https://img.shields.io/badge/Sysmon-v15-blue)
![Windows](https://img.shields.io/badge/Windows-11-0078D6)
![Kali Linux](https://img.shields.io/badge/Kali-Linux-557C94)
![SIEM](https://img.shields.io/badge/SIEM-Splunk-success)
![Status](https://img.shields.io/badge/Project-In%20Progress-orange)

---

## Overview

This project is a small SOC environment built to practice the workflow used in a Security Operations Center:

**Generate Attack → Collect Logs → Detect Activity → Investigate → Document Incident**

This lab simulates real-world adversary behavior across both Windows and Linux environments. By ingesting granular endpoint telemetry—including Sysmon, Windows Event Logs, and Linux system logs the project demonstrates end-to-end SOC capabilities, from threat detection and log correlation to incident response.

The goal is to gain practical experience with SIEM, endpoint telemetry, threat detection, log analysis, and SOC workflows.

---

## Lab Architecture

![Lab Architecture](diagrams/lab-architecture.png)

### Components

- **Splunk Enterprise** – Central SIEM used for log ingestion, searching, detection, alerting, and investigation.
- **Windows 11 Endpoint** – Generates Windows Security Event Logs and Sysmon telemetry.
- **Linux Endpoint** – Generates authentication, system, audit, and cron-related logs.
- **Kali Linux** – Used as the attacker machine for controlled attack simulations.
- **Splunk Universal Forwarder** – Used to forward endpoint logs to the Splunk server.


# Technologies Used


![SSH](https://img.shields.io/badge/SSH-%23222222.svg?style=for-the-badge&logo=gnubash&logoColor=white)

![Splunk](https://img.shields.io/badge/Splunk-%23000000.svg?style=for-the-badge&logo=splunk&logoColor=white)

![Debian](https://img.shields.io/badge/Debian-%23A81D33.svg?style=for-the-badge&logo=debian&logoColor=white)

![Splunk Universal Forwarder](https://img.shields.io/badge/Splunk_Universal_Forwarder-%23000000.svg?style=for-the-badge&logo=splunk&logoColor=white)

![Sysmon](https://img.shields.io/badge/Sysmon-%230078D4.svg?style=for-the-badge&logo=microsoft&logoColor=white)

![Windows Event Logs](https://img.shields.io/badge/Windows_Event_Logs-%230078D4.svg?style=for-the-badge&logo=windows&logoColor=white)

![Kali Linux](https://img.shields.io/badge/Kali_Linux-%23557C94.svg?style=for-the-badge&logo=kali-linux&logoColor=white)

![Windows 11](https://img.shields.io/badge/Windows_11-%230078D4.svg?style=for-the-badge&logo=windows-11&logoColor=white)

![PowerShell](https://img.shields.io/badge/PowerShell-%235391FE.svg?style=for-the-badge&logo=powershell&logoColor=white)

![SMB Protocol](https://img.shields.io/badge/SMB_Protocol-%230078D4.svg?style=for-the-badge&logo=windows&logoColor=white)


---

# Project Structure

```
Splunk-Home-Lab/

├───attacks
├───configs
│   ├───linux endpoint
│   ├───splunk server
│   └───windows endpoint
├───dashboard
├───detections
├───diagrams
├───docs
├───incidents
├───screenshots
│   ├───001-SSH-brute-force-linux
│   ├───002-SMB-brute-force
│   ├───003-Powershell-encoded-command
│   ├───004-Account-creation
│   ├───005-SSH-brute-force-successful-login
│   ├───006-Windows-failed-login-type-2
│   ├───007-Linux-Cron-persistence
│   ├───Kali-linux
│   ├───Linux-Endpoint
│   ├───Splunk-Server
│   │   └───splunk-installation
│   └───Windows-Endpoint
│       ├───splunk-forwarder
│       └───sysmon
│───spl
└── README.md
```

# SOC Workflow

The project follows a simple investigation workflow:

```text
Attack Simulation
       ↓
Endpoint Activity
       ↓
Log Collection
       ↓
Splunk Ingestion
       ↓
SPL Detection
       ↓
Alert Triggered
       ↓
Event Investigation
       ↓
Incident Documentation
```

For each attack, I captured the relevant evidence and documented the investigation.

---

## Splunk Dashboard

A SOC dashboard was created to provide a central view of security activity and detection results.

![dashboard](/screenshots/005-SSH-brute-force-successful-login/After-SOC%20Dashboard%20Overview.png)

The dashboard is used to review:

- Authentication activity

- Failed login activity

- Detected attacks

- Alert activity

- Security events

Dashboard screenshots are available under:

`/screenshots`

# Screenshots

Project screenshots are available inside:

```
screenshots/
```

Including:

- Splunk installation
- Splunk Dashboard
- Universal Forwarder installation
- Sysmon installation
- Attack execution
- Splunk detections
- Incident response

## Attack Simulations

The attacks/ directory contains the documentation for each simulated attack.

`attacks/`


```
├── ATK-001-SSH-Linux-Brute-force-attack.md
├── ATK-002-SMB-attack.md
├── ATK-003-Powershell-encoded-command-attack.md
├── ATK-004-Suspicious-account-creation.md
├── ATK-005-SSH-Successful-login-brute-force-attack.md
├── ATK-006-Windows-failed-login-attack.md
└── ATK-007-Linux-Cron-persistence.md
```

Each attack document contains : 

- attack purpose
- execution details
- target
- expected detection
- actual result
- screenshots
- MITRE ATT&CK 

---

## Detection Rules

The `detections/` directory contains the detection documentation for the seven alerts created in Splunk.

```
detections/

├── DET-001-SSH-brute-force.md
├── DET-002-SMB-brute-force.md
├── DET-003-Powershell-encoded-command.md
├── DET-004-Account-creation.md
├── DET-005-Successful-login-after-failed-logins.md
├── DET-006-Windows-failed-logins-type-2.md
└── DET-007-Linux-cron.md
```

Each detection document describes:

- Detection purpose
- Data source
- Detection logic
- SPL query
- MITRE ATT&CK mapping
- Investigation points
- True positive example
- Recommended response

## SPL Queries

The spl/ directory contains the SPL queries used for the detections.

`spl/`

```
├── Account-creation-windows.spl
├── Encoded-powershell-command.spl
├── Linux-cron-persistence.spl
├── SMB-brute-force.spl
├── SSH-brute-force-linux.spl
├── Successful-Login-after-multiple-failed-attempts.spl
└── Windows-Failed-login-Type2.spl
```

These queries were used to search endpoint telemetry and identify the activity generated during the attack simulations.

# Configuration Files

```
configs/
```

## Incident Reports

The `incidents/` directory contains the investigation records for the simulated security incidents.

`incidents/`

```
├── INC-001-ssh-brute-force.md
├── INC-002-SMB-brute-force.md
├── INC-003-Encoded-powershell-command.md
├── INC-004-Suspicious-account-creation.md
├── INC-005-Succuesful-login-after-failed-attempts.md
├── INC-006-Windows-Failed-logins-type-2.md
├── INC-007-Linux-Cron-persistence.md
└── Mega-INC-report.md
```


The incident reports contain the alert information, evidence, SPL query, raw log/event information, response actions, and investigation conclusion.

# Configuration Files

```
configs/
```

## Contains

```
├───linux endpoint
│       inputs.conf
│
├───splunk server
│       indexes.conf
│       inputs.conf
│       output.conf
│
└───windows endpoint
        inputs.conf
        output.conf
        sysmonconfig-export.xml
```

These configurations cover log collection, forwarding, Splunk indexes, and Sysmon configuration.

---

## Documentation

The `docs/` directory contains setup and troubleshooting documentation.

`docs/`

```
├── How-logs-are-Collected.md
├── lab-setup.md
├── Linux-audit-logs.md
├── Sysmon-setup.md
├── Troubleshooting.md
└── Universal-Forwarder-installation.md
```

## MITRE ATT&CK

MITRE ATT&CK techniques are mapped to the simulated activity and documented within the detection and attack documentation.

The `mitre/` directory contains the dedicated ATT&CK mapping documentation.

---

# Skills Demonstrated

- Skills Demonstrated
- Splunk Enterprise Administration
- SIEM Configuration
- SPL Query Development
- Log Collection and Analysis
- Windows Event Log Analysis
- Sysmon Analysis
- Linux Log Analysis
- Security Alert Creation
- Threat Detection
- Attack Simulation
- Incident Investigation
- Incident Response
- MITRE ATT&CK Mapping
- SOC Dashboard Development
- Security Event Correlationg

---

## Project Outcome

This project provided hands-on experience with the complete SIEM investigation workflow.

I configured the environment, collected endpoint telemetry, created 7 Splunk detections, simulated 7 controlled attacks, investigated the resulting events, created 1 SOC dashboard, and documented each detection and incident.

The project demonstrates practical experience with endpoint telemetry, SPL-based detection, alert investigation, and SOC incident documentation.

# Author

**Mohammad Ali**

SOC Analyst

LinkedIn

https://www.linkedin.com/in/mohdali02/

TryhackMe

https://tryhackme.com/p/chan4o

---
