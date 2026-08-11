# Lab Setup Overview

Here is a quick breakdown of how I built and connected the virtual environment for this SOC home lab.

## 1. The Virtual Machines
The lab is built using VirtualBox and consists of four main virtual machines:
* **Splunk Server:** The central brain of the lab. It runs Splunk Enterprise, receives all the logs, and hosts the dashboards and alerts.
* **Windows 11 Endpoint:** The primary victim machine. It is configured with Sysmon and native Windows Event Logs to track local and network attacks.
* **Linux Endpoint (Debian):** The secondary victim machine. It is configured to monitor SSH traffic, system calls, and cron jobs.
* **Kali Linux (Attacker):** The offensive machine used to launch brute-force attacks, create rogue accounts, and establish persistence against the two endpoints.

## 2. The Data Flow
To make this function like a real Security Operations Center, the machines need to talk to each other. Here is how the data flows:
1. The **Attacker (Kali)** launches an attack against the Windows or Linux endpoints.
2. The **Endpoints** generate telemetry (e.g., Sysmon Event ID 1, Linux auth logs, Windows Logon Type 3).
3. The **Splunk Universal Forwarders**, which are installed on both endpoints, pick up these logs in real-time.
4. The forwarders securely ship the logs over the network on port `9997` directly to the **Splunk Server** for indexing and alerting.

## 3. Architecture Diagram
If you want to see a visual representation of how these machines and log forwarders are connected, you can check out the `lab-architecture.png` file located in the `/diagrams` folder of this repository.
