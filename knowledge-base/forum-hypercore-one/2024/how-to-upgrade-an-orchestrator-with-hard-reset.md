Thread: how-to-upgrade-an-orchestrator-with-hard-reset
0x3639 | 2024-02-02 20:07:12 UTC | #1

Here is an upgrade script to automatically upgrade the orchestrator and perform a hard reset.

## Install Requirements

`sudo apt-get install jq`

## Create Bash Script

`nano upgrade_orchestrator.sh`

```
#!/bin/bash

set -e

# Get the latest release from GitHub API
latest_release=$(curl -s https://api.github.com/repos/HyperCore-Team/orchestrator/releases/latest | jq -r ".assets[] | select(.name | contains(\"linux-amd64.zip\")) | .browser_download_url")

# Clean up
rm -rf orchestrator-linux-amd64.zip orchestrator-linux-amd64

# Download the latest release
wget -O orchestrator-linux-amd64.zip "$latest_release"
unzip -o orchestrator-linux-amd64.zip
sudo systemctl stop orchestrator
sleep 10
sudo cp orchestrator-linux-amd64 /usr/local/bin/

# Perform Hard Reset - remove queues and events
rm -rf ~/.orchestrator/queues
rm -rf ~/.orchestrator/events

# Restart Orchestrator
sudo systemctl start orchestrator
sleep 10

# Check Status of Orchestrator
sudo systemctl status orchestrator
```

Save the bash script and make it executable `sudo chmod +x upgrade_orchestrator.sh`

Run the upgrade script `sudo ./upgrade_orchestrator.sh`

-------------------------

