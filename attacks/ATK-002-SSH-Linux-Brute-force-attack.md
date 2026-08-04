## Purpose

To generate repeated failed SSH authentication logs on the victim machine, simulating a real-world brute-force attack. This traffic will be forwarded to Splunk server.

## Commands Used

```bash
python3 ssh_sc.py
```

## Attacker

- **OS**: Kali Linux
- **Tool**: Custom python script

## Target

- **OS**: Debian (Linux)
- **Service Targeted**: SSH (Port `22`)

## Expected Detection

The Splunk forwarder on the Debian victim ingests `/var/log/auth.log`. The Splunk search is expected to detect more than 5 failed ssh login attempts originating from the single source IP address within a short time window. This should trigger a high-severity alert.

## Actual Detection

The Splunk alert triggered successfully. The dashboard displayed multiple 'Failed password' events for usernames, all originating from the attacker IP. The correlation search fired after script completing its run.

## Screenshots

## MITRE Mapping

**Credential Access - Brute Force (T1110) / Password Guessing (T1110.001)**
