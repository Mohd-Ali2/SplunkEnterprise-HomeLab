## Incident Report: SSH Brute-Force Attack 

**Incident ID:** INC-2026-001  
**Date of Report:** YYYY-MM-DD  
**Analyst:** Faiz  
**Status:** Closed  

---

### 1. Executive Summary
A high-volume SSH brute-force attack was detected targeting the primary Debian Linux server. The threat actor attempted unauthorized credential access over port `22`. The Wazuh SIEM successfully detected the anomaly, and custom Python SOAR automation enriched the threat data, confirming the malicious nature of the source IP. The attack was successfully contained with no data exfiltration or lateral movement observed.

### 2. Detection & Analysis
* **Initial Detection:** Wazuh SIEM rule ID `5712` triggered due to >5 failed login attempts within a 60-second window.
* **Log Source:** `/var/log/auth.log`
* **Target Asset:** Debian Linux VM (`192.168.1.15`)
* **Attacker IP:** `[Insert Attacker IP here]`
* **Threat Enrichment:** The attacker IP was queried against the AbuseIPDB API, returning a malicious confidence score of **100%**.

### 3. Indicators of Compromise (IoCs)
* **Source IP:** `[Insert Attacker IP here]`
* **Targeted Usernames:** `root`, `admin`, `test`
* **MITRE ATT&CK Mapping:** 
  * Tactic: Credential Access (TA0006)
  * Technique: Brute Force (T1110)
  * Sub-Technique: Password Guessing (T1110.001)

### 4. Timeline of Events
* **14:00 IST:** Unauthorized brute-force script initiated from the attacker machine.
* **14:01 IST:** Target `/var/log/auth.log` records repetitive "Failed password" entries.
* **14:02 IST:** Wazuh forwarder ingests logs; SIEM correlation rule fires.
* **14:03 IST:** Python SOAR script extracts the IP, queries VirusTotal/AbuseIPDB, and dispatches a Slack webhook alert.
* **14:15 IST:** Analyst acknowledges the alert and begins containment protocols.

### 5. Containment, Eradication & Recovery
* **Containment:** The malicious source IP was permanently blocked at the local firewall level using `iptables`.
* **Eradication:** Verified no successful authentications occurred prior to the IP block. The `root` account login via SSH was disabled to prevent future credential stuffing.
* **Recovery:** SSH service was restarted. Normal network traffic monitoring resumed. 

### 6. Post-Incident & Lessons Learned
* **What went well:** The automated SOAR pipeline accurately enriched the threat within seconds, drastically reducing manual triage time.
* **Improvements needed:** SSH should be reconfigured to utilize key-based authentication exclusively, disabling password-based logins entirely.
