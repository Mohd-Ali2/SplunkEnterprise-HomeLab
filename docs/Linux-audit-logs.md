# Linux Audit Logs

Here is a quick overview of how I set up logging on the Linux endpoint to track attacker activity.

## 1. audit.rules Configuration
To get deeper visibility into the Linux machine, I used `auditd` (Linux Audit Daemon). I edited the `audit.rules` file to tell the system exactly which commands and system calls to watch for. This helps capture malicious activity while filtering out normal background noise.

## 2. File Integrity & Events Captured
Using those audit rules, I set up the system to capture two main things:
* **Events:** Tracking command executions and processes. This is exactly how I was able to catch the attacker running the malicious `crontab` reverse shell command.
* **File Integrity Monitoring:** Watching critical system files like `/etc/passwd` and `/etc/shadow`. If an attacker tries to edit these files to create a backdoor user, `auditd` immediately generates a log.

## 3. Ensuring SSH Logging
To make sure my SSH brute-force alerts would work, I verified that the system was properly logging all authentication attempts. These events (both successful and failed SSH logins) are natively captured in `/var/log/auth.log`.

## 4. rsyslog Forwarding
`auditd` generates the logs locally, but they need to get to Splunk. I configured `rsyslog` to format and route these logs so the Splunk Universal Forwarder could easily read them and send them over to the main Splunk server for analysis.
