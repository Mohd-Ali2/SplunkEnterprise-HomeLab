# How Logs Are Collected

Here is a quick breakdown of how logs are generated, collected, and forwarded to Splunk in this lab environment.

## 1. Sources (The Endpoints)
Logs are pulled directly from the two virtual machines used for the attack simulations:
* **Windows 11** (Target for SMB, PowerShell, and local admin attacks)
* **Linux / Debian** (Target for SSH brute force and Cron persistence)

## 2. Log Types 
To get a clear picture of what the attacker is doing, I collected a few specific log types:
* **Windows Event Logs:** Mainly Security logs to track successful/failed logons and account creations.
* **Sysmon:** Installed on the Windows machine to catch advanced activity like process creation, command-line arguments, and network connections.
* **Linux Logs:** Mainly `/var/log/auth.log` and `syslog` to track SSH authentication and system changes.

## 3. Collection Method
Logs are pushed from the endpoints to the main Splunk server using the **Splunk Universal Forwarder (UF)**. 

* I installed the UF agent on both the Windows and Linux machines.
* I configured the `inputs.conf` file on each endpoint to tell the forwarder exactly which logs and directories to read.
* The UF then automatically forwards those logs to the main Splunk Indexer over port 9997. 
* *(Note: You can see my exact config files in the `/configs` folder of this repo).*

## 4. Retention Policy
Since this is a home lab running on limited storage, the data retention in Splunk is set to **30 days**. After 30 days, the older logs are automatically deleted to free up disk space.
