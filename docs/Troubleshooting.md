# Troubleshooting

While building this lab, I ran into a few common issues. Here is a quick breakdown of the problems I faced and how I fixed them, just in case anything breaks.

## 1. Splunk UF Not Sending Data
If logs weren't showing up in Splunk, the first thing I checked was if the Universal Forwarder service was actually running on the endpoint. Sometimes, just restarting the `SplunkForwarder` service fixed it. If that didn't work, I looked at the `splunkd.log` file on the forwarder to see exactly why it was failing to connect to the main server.

## 2. Permission Errors
This happened mostly on the Linux machine. The Splunk forwarder would be running fine, but it wasn't sending the SSH or audit logs. It turned out to be a permission issue—the `splunk` user account didn't have the right permissions to read files like `/var/log/auth.log`. Giving the Splunk user read access fixed the problem immediately.

## 3. Timezone Issues
At one point, the logs arriving in Splunk had timestamps from the future or the past, which completely broke my detection alerts. I had to go back and make sure all my virtual machines (Windows, Kali, and the Splunk server) were perfectly synced to the exact same time zone.

## 4. Network Connectivity
Since everything was running inside VirtualBox, sometimes the VMs couldn't talk to each other. If the data stopped flowing, I would run a quick `ping` between the machines. Usually, the issue was that the Windows firewall was blocking port `9997` (which the forwarder uses to send logs) or I had the VMs on the wrong VirtualBox network adapters.

## 5. Disk Space
Splunk has a built-in safety feature where it will completely stop indexing logs if your hard drive hits around 90% capacity. Because I built this lab on virtual machines with small hard drives, I ran into this warning. To fix it, I just had to clear out some old files, adjust my retention settings, and make sure my VM had enough free space. 

## 6. Missing Sourcetype
Sometimes the logs would arrive in Splunk, but they looked like a broken, unreadable mess of text. This almost always meant I messed up the `inputs.conf` file on the forwarder. If you forget to define the `sourcetype`, or if you misspell it (like typing `wineventlog` instead of `WinEventLog:Security`), Splunk won't know how to format the data. Fixing the typo in the config file and restarting the forwarder fixed the parsing issues.
