Thread: bash-script-to-keep-the-orchestrator-alive
0x3639 | 2024-08-31 22:23:54 UTC | #1

## Background
If the orchestrator loses connection to the `znnd` node or `eth` node it will shut down regardless of how the service is setup. 

Here's a bash script that checks if the `orchestrator` service is running, and if not, starts it and logs an event to `/var/log/syslog`. You can then set this script to run as a cron job every minute.

### Step 1: Create the Bash Script

1. Create the script, for example, `nano /usr/local/bin/check_orchestrator.sh`.

```bash
#!/bin/bash

# Check if the service is running
if ! systemctl is-active --quiet orchestrator; then
  # If not running, start the service
  systemctl start orchestrator
  
  # Log to syslog
  logger "Orchestrator service was not running and has been started."
fi
```

2. Make the script executable:

```bash
sudo chmod +x /usr/local/bin/check_orchestrator.sh
```

### Step 2: Set Up the Cron Job

1. Open the cron job editor:

```bash
crontab -e
```

2. Add the following line to run the script every minute:

```bash
* * * * * /usr/local/bin/check_orchestrator.sh
```

### Explanation:
- `systemctl is-active --quiet orchestrator`: This checks if the `orchestrator` service is running. The `--quiet` flag ensures that no output is produced.
- `systemctl start orchestrator`: This command starts the `orchestrator` service if it is not running.
- `logger "Orchestrator service was not running and has been started."`: This logs a message to `/var/log/syslog`.

This setup will ensure that the `orchestrator` service is checked every minute, and if it is found to be stopped, it will be started, and an entry will be made in the syslog.

-------------------------

