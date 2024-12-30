Thread: orchestrator-keygen-peer-list
0x3639 | 2023-09-02 18:23:26 UTC | #1

If you want a script to parse your log files to count the number of remote peers trying to perform the keygen do the following

```
nano peerlist.sh
```

Paste this script into that file.


```
#!/bin/bash

# Get logs from journalctl for the last 1 day
logs=$(journalctl --since "1 day ago" --unit=orchestrator -n 100000 --no-pager | grep "remote peer")

# Parse the logs to extract remote peer addresses
addresses=$(echo "$logs" | grep -oP '"remote peer":"\K[^"]+' | sort | uniq)

# Print the unique addresses
echo "Unique 'remote peer' addresses over the last 1day:"
echo "$addresses"

# Count the total number of unique addresses
total_unique=$(echo "$addresses" | wc -l)

echo "Total unique 'remote peer' addresses: $total_unique"
```

```
chmod +x peerlist.sh
./peerlist.sh
```

-------------------------

