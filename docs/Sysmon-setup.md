# Sysmon Setup

Native Windows Event Logs are great, but they don't catch everything. Here is how I set up Sysmon (System Monitor) on the Windows machine to get deep visibility into exactly what the attacker was executing.

## 1. Sysmon Config File (SwiftOnSecurity)
If you install Sysmon by default, it logs way too much useless background noise and will crash your Splunk storage limits. To fix this, I used a modified version of the industry-standard **SwiftOnSecurity** configuration file. This acts as a smart filter, telling Sysmon to only log suspicious or important activity and ignore normal Windows background processes.

## 2. Installation Command
After downloading Sysmon from Microsoft Sysinternals, I opened a Command Prompt as Administrator and ran this command to install the service and apply my custom config:

```cmd
sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

## Important Event Codes

By setting up Sysmon, I was able to capture these high-value event IDs, which are absolutely crucial for SOC analysts :

Event ID 1 (Process Creation): This is the most important one. It shows the full command-line arguments of everything executed. This is exactly how I detected the encoded PowerShell attack.

Event ID 3 (Network Connection): Tracks which programs are making network connections (useful for catching reverse shells).

Event ID 11 (File Create): Tracks when new executables or suspicious files are dropped onto the system.

## Validation

To make sure Sysmon was actually working before I started launching attacks, I opened the Windows Event Viewer on the endpoint and navigated to:
Applications and Services Logs > Microsoft > Windows > Sysmon > Operational.

Once I saw Event ID 1 logs populating in that folder, I knew it was working and ready for the Splunk Universal Forwarder to pick up and send to the SIEM.
