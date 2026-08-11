# Lab Setup Overview

Here is a quick breakdown of how I built and connected the virtual environment for this SOC home lab.

## 1. The Environment Setup
The lab network consists of four main systems, each serving a specific role in the attack and defense lifecycle:
* **Splunk Server:** The central SIEM of the lab. It runs Splunk Enterprise, ingests all the endpoint telemetry, and hosts the detection alerts and dashboards.
* **Windows 11 Endpoint:** The primary target host. It is heavily monitored using Sysmon and native Windows Event Logs to track local and network-based attacks.
* **Linux Endpoint:** The secondary target host. It is configured with `auditd` and system logging to monitor SSH traffic, command executions, and cron jobs.
* **Attacker Machine (Kali Linux):** The offensive system used to execute the simulated attacks, such as brute-forcing credentials and deploying reverse shells against the targets.

## 2. The Data Flow
To make this function like a real Security Operations Center, the machines need to talk to each other. Here is how the data flows:
1. The **Attacker (Kali)** launches an attack against the Windows or Linux endpoints.
2. The **Endpoints** generate telemetry (e.g., Sysmon Event ID 1, Linux auth logs, Windows Logon Type 3).
3. The **Splunk Universal Forwarders**, which are installed on both endpoints, pick up these logs in real-time.
4. The forwarders securely ship the logs over the network on port `9997` directly to the **Splunk Server** for indexing and alerting.

## 3. Architecture Diagram
If you want to see a visual representation of how these machines and log forwarders are connected, you can check out the `lab-architecture.png` file located in the `/diagrams` folder of this repository.
