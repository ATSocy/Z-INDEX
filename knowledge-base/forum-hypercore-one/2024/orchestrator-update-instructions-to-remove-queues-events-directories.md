Thread: orchestrator-update-instructions-to-remove-queues-events-directories
0x3639 | 2023-12-03 16:08:26 UTC | #1

Some orchestrators may be on the old fork and are trying to sign old messages which is preventing the bridge from working.  In order to prevent that follow these instructions:

```
sudo -i
systemctl stop orchestrator
# WAIT 10 seconds
rm -rf ~/.orchestrator/queues
rm -rf ~/.orchestrator/events
systemctl start orchestrator
```

## Hard Reset Script
If you want to automate the steps to perform a *hard reset* follow these instructions.

`nano ~/reset_orchestrator.sh`

Next paste in this script into that file

```
#!/bin/bash

# Check if the script is run as root
if [ "$EUID" -ne 0 ]
  then echo "Please run as root"
  exit
fi

echo "Stopping Orchestrator service..."
systemctl stop orchestrator

echo "Waiting for 10 seconds..."
sleep 10

echo "Removing Orchestrator queues and events directories..."
rm -rf ~/.orchestrator/queues
rm -rf ~/.orchestrator/events

echo "Starting Orchestrator service..."
systemctl start orchestrator

echo "Checking Orchestrator status..."
systemctl status orchestrator
```
Make the script executable `chmod +x ~/reset_orchestrator.sh`
Run the script `sudo ~/reset_orchestrator.sh`

### Notes
- These instructions assume your orchestrator files are located here `/root/.orchestrator`
- This is a "hard reset" of events.  I've tested these instructions and they work.  In the future @sumamu's team will create a feature that circumvents this manual step.

-------------------------

Chadass | 2023-09-10 17:59:51 UTC | #2

Will this clear the infinite signing tx on the bridge page?

-------------------------

0x3639 | 2023-09-10 18:34:18 UTC | #3

I hope so

-------------------------

mehowz | 2023-10-01 22:33:14 UTC | #4

Or this single command after `sudo -i`


```
(
sudo systemctl stop orchestrator
sleep 5 && sudo rm -rf ~/.orchestrator/queues
sleep 5 && sudo rm -rf ~/.orchestrator/events
sleep 5 && sudo systemctl start orchestrator
sleep 5 && sudo systemctl status orchestrator
)
```

-------------------------

