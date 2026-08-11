# Universal Forwarder Installation

The Splunk Universal Forwarder (UF) is the lightweight agent that sits on the endpoints and sends logs to the main SIEM. Here is a quick breakdown of how I got it up and running on my lab machines.

## 1. Prerequisites
Before installing the forwarder, I had to make sure of two things:
* The endpoints (Windows and Linux VMs) had network connectivity and could ping the main Splunk server.
* The main Splunk server was actively listening for incoming data on port `9997` (I set this up in the Splunk Web UI under Settings > Forwarding and Receiving).

## 2. Installation & Commands
I installed the forwarder agent on both my Windows and Linux target machines. 

* **For Windows:** I downloaded the MSI installer from the Splunk website. During the setup wizard, it asks for a deployment server and an indexer. I just entered the IP address of my main Splunk server for the indexer and set the receiving port to `9997`. 
* **For Linux:** I downloaded the `.deb` package for my Debian/Kali machine and installed it using the terminal :
  
  ```bash
  dpkg -i splunkforwarder-*.deb
  ```

After it installed, I went to the Splunk bin directory, started the service, and accepted the license agreement :

```
/opt/splunkforwarder/bin/splunk start --accept-license
```

## Configuration

Once installed, the forwarder needs to know what logs to grab and where exactly to send them. I managed this by editing two main files on the endpoints:

`outputs.conf`: This confirms the IP address and port (9997) of the main Splunk server where the logs are being shipped.

`inputs.conf` : This tells the forwarder which specific logs to monitor (like the Windows Security logs, Sysmon, or Linux /var/log/auth.log).

## Validation Checks

After saving my configuration files, I restarted the Splunk Forwarder service on the endpoints to apply the changes.

To make sure everything was actually working, I logged into my main Splunk web dashboard and ran a simple search :

Splunk SPL

`index=* host="HP-Pavilion"`

Once I saw fresh logs from my Windows and Linux machines popping up on the screen in real-time, I knew the forwarders were successfully connected and the data pipeline was ready for the attack simulations.
