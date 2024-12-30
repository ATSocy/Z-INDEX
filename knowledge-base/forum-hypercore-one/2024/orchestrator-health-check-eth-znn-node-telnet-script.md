Thread: orchestrator-health-check-eth-znn-node-telnet-script
0x3639 | 2023-08-28 01:12:42 UTC | #1

If you want to make sure your Orchestrator is connecting to the ETH and ZNN nodes correctly, please use this script.  This script also checks to make sure your Orchestrator is accessible on port 55055.  

### Setup Instructions

1. Copy the script below to a file, for example, `healthcheck.sh`.
2. Give execute permissions to the script: `chmod +x healthcheck.sh`
3. Run the script: `./healthcheck.sh`

Note: This script assumes that your logs are stored in `/var/log/syslog*`. If your logs are stored in a different location, you'll need to adjust the script accordingly.

```
#!/bin/bash

# Define the search queries
SEARCH_1="websocket: close 1006"
SEARCH_2="websocket: close 1001"

# Get the date 2 days ago in the format that matches log timestamps
DATE_2_DAYS_AGO=$(date -d "2 days ago" '+%Y-%m-%d')

# Count the number of instances for each search query in the logs from the last 2 days
COUNT_1=$(grep -c "$SEARCH_1" /var/log/syslog* | awk -F: -v date="$DATE_2_DAYS_AGO" '$1 ~ date {sum += $2} END {print sum+0}')
COUNT_2=$(grep -c "$SEARCH_2" /var/log/syslog* | awk -F: -v date="$DATE_2_DAYS_AGO" '$1 ~ date {sum += $2} END {print sum+0}')

# Report the number for each search query
echo "Number of instances for \"$SEARCH_1\": $COUNT_1"
echo "Number of instances for \"$SEARCH_2\": $COUNT_2"

# Get the public IP of the device
PUBLIC_IP=$(curl -s ifconfig.me)

# Check if port 55055 is open using telnet
(echo > /dev/tcp/$PUBLIC_IP/55055) &>/dev/null && echo "Port 55055 is open" || echo "Port 55055 is NOT Open. Open Port TCP 55055 on your firewall"
```

### Log References

`websocket: close 1006 (abnormal closure): unexpected EOF`
Orchestrator failed because znn node is down

`websocket: close 1001 (going away): upstream went away`
Orchestrator failed because eth node is down

-------------------------

Chadass | 2023-08-28 11:55:01 UTC | #2

I guess you need to get that:

Number of instances for "websocket: close 1006": 0
Number of instances for "websocket: close 1001": 0
Port 55055 is open

If yes I'm gucci

-------------------------

0x3639 | 2023-08-28 12:06:41 UTC | #3

[quote="Chadass, post:2, topic:188"]
Number of instances for “websocket: close 1006”: 0
Number of instances for “websocket: close 1001”: 0
Port 55055 is open
[/quote]

Yes - that is a good result!

-------------------------

mehowz | 2023-08-28 16:08:17 UTC | #4

All is well with all ZenonORG + HyperGrowth Pillars

-------------------------

aliencoder | 2023-08-30 10:00:00 UTC | #5

@0x3639 what was the website that was monitoring the orchestrators?

-------------------------

0x3639 | 2023-08-30 12:38:58 UTC | #6

https://status.bridge.zenon.community/

It's producing strange results.  Also wanted to mention this is the list of Orchestrators from the last keygen, not the current one.  

I need to automate this list eventually.  For a period of time it was showing my orchestrator down, when in fact it was up.

-------------------------

