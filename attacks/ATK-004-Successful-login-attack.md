## Purpose 

 Flags successful authentications occurring after repeated authentication failures to identify compromised credentials before attackers expand their foothold.


## Commands Used

```
hydra -t 4 -l linux -P /home/kali/Desktop/passlist.txt ssh://192.168.31.70
```

## Attacker

- **OS**: Kali Linux
- **Tool**: Custom python script

  ![attack](/screenshots/SSH-brute-force-successful-login/Command-used.png)
 

## Target

- **OS**: Debian (Linux)
- **Service Targeted**: SSH (Port `22`)


## Expected Detection

The Splunk forwarder on the Debian victim ingests `/var/log/auth.log`. The Splunk search is expected to detect more than 5 failed SSH login attempts with one successful login originating from the single source IP address within a short time window. This should trigger a high-severity alert.


## Actual Detection 

Splunk alert was fired successfully when multiple SSH failures occurs with one successful login. 


## Screenshots 

# Alert Triggered

 ![attack](/screenshots/SSH-brute-force-successful-login/Alert%20fired%20Successfully.png)


## MITRE Mapping

`MITRE ID : T1110.001`

`Phase : Attempt`

`Technique Name : Brute Force: Password Guessing`

`Tactic : Credential Access (TA0006)`


`MITRE ID : T1078`

`Phase : Success`

`Technique Name : Valid account`

`Tactic : Initial Access (TA0001), Persistence (TA0003), Privilege Escalation (TA0004)`
