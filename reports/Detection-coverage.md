Purpose



Show what your lab can detect.



Sections

Detection Strategy

Data Sources Used

Detection Categories

Authentication

Brute Force

Persistence

PowerShell

Linux Activity

Account Management

Alert Inventory

MITRE ATT\&CK Coverage

Event IDs Covered

SPL Coverage

Detection Limitations

Future Detection Ideas



Include a table like:



Detection	Windows/Linux	Event IDs	MITRE

Failed Logins	Windows	4625	T1110

SMB Brute Force	Windows	4625	T1110

SSH Brute Force	Linux	auth.log	T1110

PowerShell Encoded Command	Windows	Sysmon 1	T1059.001

Cron Persistence	Linux	cron/syslog	T1053.003

User Account Creation	Windows	4720	T1136

