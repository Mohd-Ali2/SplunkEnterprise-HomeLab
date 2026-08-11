# Splunk Enterprise Investigation & Detection Home Lab

![Splunk](https://img.shields.io/badge/Splunk-Enterprise-green)
![Sysmon](https://img.shields.io/badge/Sysmon-v15-blue)
![Windows](https://img.shields.io/badge/Windows-11-0078D6)
![Kali Linux](https://img.shields.io/badge/Kali-Linux-557C94)
![SIEM](https://img.shields.io/badge/SIEM-Splunk-success)
![Status](https://img.shields.io/badge/Project-In%20Progress-orange)

---

## Overview

This project demonstrates the design and implementation of a small Security Operations Center (SOC) home lab using Splunk Enterprise.

This lab simulates real-world adversary behavior across both Windows and Linux environments. By ingesting granular endpoint telemetry—including Sysmon, Windows Event Logs, and Linux system logs the project demonstrates end-to-end SOC capabilities, from threat detection and log correlation to incident response.

The goal is to gain practical experience with SIEM, endpoint telemetry, threat detection, log analysis, and SOC workflows.

---

## Lab Architecture

![Lab Architecture](diagrams/lab-architecture.png)

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

├── attacks/
├── configs/
├── diagrams/
├── docs/
├── reports/
├── screenshots/
├── spl/
└── README.md
```

---


# Screenshots

Project screenshots are available inside:

```
screenshots/
```

Including:

- Splunk installation
- Universal Forwarder installation
- Sysmon installation
- Attack execution
- Splunk detections
- Incident response

---

# Configuration Files

```
configs/
```

Contains

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

---

# SPL Queries

```
spl/

├── Account-creation-windows.spl
├── Encoded-powershell-command.spl
├── Linux-cron-persistence.spl
├── SMB-brute-force.spl
├── SSH-brute-force-linux.spl
├── Successful-Login-after-multiple-failed-attempts.spl
└── Windows-Failed-login-Type2.spl
 
```


   
    
    
    
    
    


Contains detection queries used during the investigation.

---

# Skills Demonstrated

- SIEM Administration
- Splunk Search Processing Language (SPL)
- Windows Event Log Analysis
- Sysmon Analysis
- Threat Detection
- Incident Investigation
- Incident Response
- Network Monitoring
- Endpoint Monitoring

---


# Author

**Mohammad Ali**

Cybersecurity | SOC Analyst

LinkedIn

https://www.linkedin.com/in/mohdali02/

TryhackMe

https://tryhackme.com/p/chan4o

---
