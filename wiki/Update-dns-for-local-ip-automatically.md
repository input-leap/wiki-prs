# Update DNS for local IP automatically
If you use your InputLeap setup in several locations, your Server IP might vary quite a lot.
This guide will describe how to set it to a fixed adress and update it automatically.

This guide will use the (free) service of noip.com, you can use any other dynamic dns service, but the commands might change a bit.

## Setup for noip.com
1. Go to https://www.noip.com/sign-up and register. Follow the steps and log into your account.
2. Go to Dynamic DNS -> No-IP Hostnames -> Create Hostname, choose a Hostname and Domain and click "Create Hostname".
3. Click "Create DDNS Key" and click "Generate DDNS Key". You will need the `username`, `password` and `DDNS Key Hostname` later.
4. Go to Dynamic DNS -> Dynamic Update Client and follow the instructions according to your system. I installed it from source according to [this article](https://www.noip.com/support/knowledgebase/install-linux-3-x-dynamic-update-client-duc#install_from_source).

## Create Skript to update the IP and service
This Part works on linux with systemd installed, it will work similar for windows but the commands have to be changed.
1. Check if your login works with `noip-duc -g <DDNS Key Hostname> --username <DDNS Key username> --password <DDNS Key password> --once`
2. Create the skript for the IP-update with
`sudo nano /usr/local/bin/noip-update-local-ip.sh`
and paste this content:
```
!/bin/bash

# Get the current local IP address
CURRENT_LOCAL_IP=$(hostname -I | awk '{print $1}')

# Run No-IP DUC with the current local IP address
noip-duc -g <DDNS Key Hostname> --username <DDNS Key username> --password <DDNS Key password> --ip-method static:$CURRENT_LOCAL_IP --once
```
3. Create the systemd service with `sudo nano /etc/systemd/system/noip-duc-local.service` and paste
```
[Unit]
Description=No-IP Dynamic Update Client (Local IP)
After=network.target

[Service]
ExecStart=/usr/local/bin/noip-update-local-ip.sh
Restart=always
RestartSec=300s
#This will update the IP every 5 minutes

[Install]
WantedBy=multi-user.target
```
4. Enable the service with `sudo systemctl enable noip-duc-local`
5. Start the service with `sudo systemctl start noip-duc-local`

Now the skript should start update the IP automatically every five minutes.

On your client, you can now just use the Hostname as Server IP.
