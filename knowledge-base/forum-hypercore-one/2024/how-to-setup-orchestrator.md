Thread: how-to-setup-orchestrator
0x3639 | 2024-01-30 19:45:10 UTC | #1

## INSTRUCTIONS TO SETUP AN ORCHESTRATOR

### Orchestrator Infrastructure Requirements

The Orchestrator can be run on the Pillar itself or a separate virtual machine.  The stand alone virtual machine requirements are:

CPU: 2 cores w/ 4 threads (4 vCores) 
RAM: 4 GB 
Disk: NVMe w/ 40 GB 
Connectivity: Public IP w/ low latency (preferably datacenter)

If you separate the Orchestrator from the Pillar you will need access to a znnd node.  If you run the Orchestrator on the Pillar itself, you can use the znnd node of the Pillar.  

### Setup ETH node

Before you get started with installing the Orchestrator, you will need to setup an Ethereum node.  You can follow these instructions to do that: [How to Setup an Ethereum Node](https://forum.hypercore.one/t/how-to-setup-an-eth-node-for-the-orchestrator/84).   Take note of the `ws` or `wss` endpoint for use in the `config.json` file below.

### Download the Orchestrator Binary
```
wget https://github.com/HyperCore-Team/orchestrator/releases/download/v0.0.7-alphanet/orchestrator-linux-amd64.zip

unzip orchestrator-linux-amd64.zip
```

### Alternatively Build the Orchestrator Binary from Source

Get Source Code
`git clone https://github.com/HyperCore-Team/orchestrator`

Build the Binary
```
cd orchestrator
go build --ldflags '-extldflags "-Wl,--allow-multiple-definition"' -o ./build/orchestrator main.go
```

### Setup the Config.json File

Move the Binary and create the `config.json` file
```
sudo cp orchestrator-linux-amd64 /usr/local/bin/
sudo /usr/local/bin/orchestrator-linux-amd64
```
After running the process above it should fail, but will create a working directory at `/root/.orchestrator/`

Next we will update the `config.json` file located at `/root/.orchestrator/config.json`

```
sudo nano /root/.orchestrator/config.json
```

Update the `config.json` file with the correct information.
- Make sure to update the websocket `Urls` for the `Ethereum` and `Zenon` nodes. 
- Make sure to provide the passphrase for the `ProducerKeyFilePassphrase`.  This can be found by running the `sudo ./znn-controller` then select `status`.  
- Note the `EvmAddress` is unique for each Orchestrator and should not be changed.  This will be created by the orchestrator. Do not change or remove it after creation.  
- Add the Bootstrap address: `"Bootstrap": "/dns/bootstrap.zenon.community/tcp/55055/p2p/12D3KooWBVQYaz3yuJor8oW7bUqoAGDZDpFBGbGerL3SprHn57pQ"
`

```
{
    "DataPath": "/root/.orchestrator",
    "EventsPath": "",
    "QueuesPath": "",
    "GlobalState": 0,
    "EvmAddress": "",
    "Networks": {
        "BSC": {
            "Urls": [
                "ws://127.0.0.1:8545"
            ],
            "FilterQuerySize": 2000
        },
        "Ethereum": {
            "Urls": [
                "INSERT"
            ],
            "FilterQuerySize": 2000
        },
        "Zenon": {
            "Urls": [
                "ws://127.0.0.1:35998"
            ],
            "FilterQuerySize": 0
        }
    },
    "TssConfig": {
        "Port": 55055,
        "PublicKey": "",
        "DecompressedPublicKey": "",
        "LocalPubKeys": [],
        "Bootstrap": "/dns/bootstrap.zenon.community/tcp/55055/p2p/12D3KooWBVQYaz3yuJor8oW7bUqoAGDZDpFBGbGerL3SprHn57pQ",
        "PubKeyWhitelist": {},
        "BaseDir": "/root/.orchestrator/tss",
        "BaseConfig": {
            "PartyTimeout": 90000000000,
            "KeyGenTimeout": 600000000000,
            "KeySignTimeout": 280000000000,
            "KeyRegroupTimeout": 60,
            "PreParamTimeout": 600000000000,
            "EnableMonitor": false
        }
    },
    "ProducerKeyFileName": "producer",
    "ProducerKeyFilePassphrase": "INSERT",
    "ProducerIndex": 0
}
```

Copy the `producer` file into the `DataPath`.  This assumes you are running the orchestrator on the pillar.
```
sudo cp /root/.znn/wallet/producer /root/.orchestrator/producer
```

*Alternatively*, if you are running the orchestrator on a different VM than the pillar, follow these instructions: 

On the Pillar Node
```
sudo cat /root/.znn/wallet/producer
```
Copy (right click mouse) the entire key (including the curly brackets). 

Then go back to the orchestrator server
```
sudo nano /root/.orchestrator/producer
```

Paste the key (make sure that you don't double the curly brackets). You can paste in terminal by right clicking.  Save the file: `ctrl+x` then `y`

## Setup Orchestrator as a Service

```
sudo nano /etc/systemd/system/orchestrator.service
```
Copy and paste to following contents into the terminal.
```
[Unit]
Description=Orchestrator Service
After=network.target

[Service]
User=root
Group=root
ExecStart=/usr/local/bin/orchestrator-linux-amd64
ExecStop=/usr/bin/pkill -9 orchestrator-linux-amd64
Restart=on-failure
TimeoutStopSec=10s
TimeoutStartSec=10s
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=orchestrator

[Install]
WantedBy=multi-user.target
```

Activate and start the `orchestrator` service

```
sudo systemctl daemon-reload
sudo systemctl enable orchestrator
sudo systemctl start orchestrator
```
Check the status of the Orchestrator Service
```
sudo systemctl status orchestrator
```

### Open Firewall

Make sure port `55055` `TCP` is open on your firewall for gossip between nodes.

### Fuse 120 QSR
Make sure you have fused at least 120 QSR to the Pillar ***Producer*** Address

## Steps to Update the Orchestrator Binary
```
wget -O orchestrator-linux-amd64.zip https://github.com/HyperCore-Team/orchestrator/releases/download/v0.0.2-alphanet/orchestrator-linux-amd64.zip #Note this could change as releases change
unzip orchestrator-linux-amd64.zip
sudo systemctl stop orchestrator
sudo cp orchestrator-linux-amd64 /usr/local/bin/
sudo systemctl start orchestrator
# check status of orchestrator by running next command
sudo systemctl status orchestrator
```

## Notes
- After starting the Orchestrator you can see your EVM address `    "EvmAddress": "",` in the `config.json` file.  You can see that address by typing `sudo cat /root/.orchestrator/config.json`
- Search for node PubKey `journalctl --unit=orchestrator -n 100000 --no-pager | grep "ic.priv"`
- Check listening ports `netstat -tulpn | grep LISTEN`

-------------------------

Chadass | 2023-05-25 13:55:26 UTC | #13

Do we need a full node for ETH running in on the same IP ? It could be great if Sumamu provide docs to do the whole thing and set that up since the deadline is quite close.

-------------------------

0x3639 | 2023-05-25 14:04:33 UTC | #14

I'm using a remote ETH node on a different IP.  If you don't run a full node yourself, I've found [Alchemy](https://www.alchemy.com/) to be pretty good.  They have a free tier that should work.

-------------------------

Chadass | 2023-05-27 19:01:11 UTC | #16

The tutorial worked flawlessly for me. I used https://www.alchemy.com/  and sat up the orchestrator on a different VPS. All up and running.

-------------------------

CryptoFish | 2023-05-28 22:47:47 UTC | #17

@sumamu through trial and error we found out that the orchestrator runs differently when running it under the bridge administrator. What are the exact key differences and why?

Can you confirm when the orchestrator is running under admin it does not participate in the tss key ceremony and does not listen on port 55055?

-------------------------

vilkris | 2023-06-02 05:53:15 UTC | #21

When running a znnd node, it is common practice to restart the node perodically (e.g. once a day), since for unknown reasons the node will slowly eat up all system RAM.

When znnd is restarted the RPC interface is unresponsive for a period of time. When the orchestrator fails to communicate with the node because of this, it shuts down/crashes, with the following log messages:

```
INFO        rpc/znn.go:47        Error when dialing ws://127.0.0.1:35998, got: dial tcp 127.0.0.1:35998: connect: connection refused
INFO        rpc/znn.go:47        Error when dialing ws://127.0.0.1:35998, got: dial tcp 127.0.0.1:35998: connect: connection refused
INFO        rpc/znn.go:47        Error when dialing ws://127.0.0.1:35998, got: dial tcp 127.0.0.1:35998: connect: connection refused
INFO        app/manager.go:37        failed to create the node        {"reason": "cannot connect to any urls to a znn node"}
cannot connect to any urls to a znn node
systemd[1]: orchestrator.service: Main process exited, code=exited, status=1/FAILURE
systemd[1]: orchestrator.service: Failed with result 'exit-code'.
```

It would be good if the orchestrator handled this situation gracefully and waited for the node connection to be restored.

-------------------------

mehowz | 2023-06-07 21:17:26 UTC | #26

Why does the orchestrator need to be stopped before it's started? I figured we only stop it before we modify the service.

-------------------------

0x3639 | 2023-06-07 21:26:28 UTC | #27

`Restart-always` will NOT allow you to stop the service ever.  Even when you stop it manually.  So the instructions to change it this time are a little different.

-------------------------

mehowz | 2023-06-08 15:23:47 UTC | #28

If you want the orchestrator to restart multiple times after it crashes (in instances where perhaps it can't connect to the Zenon / ETH node and needs to try again/wait between attempts):

Stop the orchestrator:
```
sudo systemctl stop orchestrator
```
Followed by:
```
sudo nano /etc/systemd/system/orchestrator.service
```

Then add `StartLimitBurst=999999` and `RestartSec=30` as seen below:

```
[Unit]
Description=Orchestrator Service
After=network.target
StartLimitBurst=999999 #try to restart it 999999 times

[Service]
User=root
Group=root
ExecStart=/usr/local/bin/orchestrator-linux-amd64
ExecStop=/usr/bin/pkill -9 orchestrator-linux-amd64
Restart=on-failure
RestartSec=30 #wait 30 seconds before each restart
TimeoutStopSec=10s
TimeoutStartSec=10s
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=orchestrator

[Install]
WantedBy=multi-user.target
```

Then:

```
sudo systemctl daemon-reload
sudo systemctl start orchestrator
```

Shared by @sumamu

-------------------------

0x3639 | 2023-06-08 15:25:21 UTC | #29

what was happening?  it was trying to restart and did not restart?

-------------------------

SultanOfStaking | 2023-06-08 16:02:15 UTC | #30

I am guessing this is related to those who have an auto restart on their node due to memory issues. I had same problem on automated restart of zenon node the orchestrator could not connect to zenon node and exited. The 30 sec should allow the zenon node to come back up then orchestrator connects.

-------------------------

Chadass | 2023-06-08 17:38:19 UTC | #31

Updated, testing the new settings. I had my node tweaked to restart once a day so the orchestrator wouldn't stay up. Let's see.

-------------------------

mehowz | 2023-06-09 13:49:34 UTC | #32

Yes this is exactly what was happening.

-------------------------

SultanOfStaking | 2023-06-09 15:19:28 UTC | #33

I missed your key signing ceremony so I am essentially sitting on the bench... I am orchestrating the hell out of this bench though

-------------------------

Chadass | 2023-06-09 17:20:51 UTC | #34

Will there be any rewards for Orchestrators ?

-------------------------

0x3639 | 2023-06-09 18:45:32 UTC | #35

not now.  But I want to learn and get better at running this orchestrator b/ once the side chains become available I think it will use this orchestrator and that WILL be incentivized.  So we are learning how to run this and it will (should / could) receive rewards in the future.

-------------------------

Chadass | 2023-06-12 21:43:51 UTC | #36

Since the last update I have an issue. One orchestrator is going down 
![image|690x142](upload://u0hjpyE17ZGtQTztvOIYDFL9tdX.jpeg)
![image|446x199](upload://tsHmds5nN8fAlpzgaQ9SNb8yXTy.png)

You have an idea ?

-------------------------

0x3639 | 2023-06-13 02:46:59 UTC | #37

Some others have reported issues.  Two of them changed some values in `config.json`

- GlobalState : 0 (it was 3)
- LocalPubKeys : nul (it was [])

I have not been able to trouble shoot why or discuss with HCT.  I've been traveling and will be back on Tuesday to look into this further.

-------------------------

Chadass | 2023-06-13 11:09:39 UTC | #38

I tried that but it doesn't work for me. I will look again this afternoon.

-------------------------

mehowz | 2023-06-13 18:34:34 UTC | #39

I changed my GlobalState to 0 and it now runs error-free. Had a similar error as @Chadass 

My LocalPubKeys had a bunch of keys, so I left that unchanged.

-------------------------

Chadass | 2023-06-13 21:31:06 UTC | #40

I will try adding my publeys

-------------------------

0x3639 | 2023-06-13 22:02:08 UTC | #41

I would not try that.  The pubkey [] gets auto populated by the orchestrator.  How do you know the orchestrator is failing?  Status = stopped?

-------------------------

Chadass | 2023-06-13 22:42:58 UTC | #42

I tried the solution you gave again, I noticed my config.json got back to glbalstate 3 and the old buggy values. Redoing the process.

EDIT: aaaand doesn't work.

The link to get the last update is wget https://github.com/HyperCore-Team/orchestrator/releases/download/v0.0.3-alphanet/orchestrator-linux-amd64.zip right ?

-------------------------

mehowz | 2023-06-13 23:23:30 UTC | #43

Just to confirm you're overwriting the old file (if any) and unzipping the new one right?

I can confirm that my GlobalState remains 0.

-------------------------

Chadass | 2023-06-13 23:49:58 UTC | #44

I will redo the process tomorrow

-------------------------

Chadass | 2023-06-14 09:25:58 UTC | #45

I have redone all the process and still nothing works for me. I drop my configuration file here in case Sumamu see it:

{
    "DataPath": "/root/.orchestrator",
    "EventsPath": "",
    "QueuesPath": "",
    "GlobalState": 0,
    "EvmAddress": "redacted",
    "Networks": {
        "BSC": {
            "Urls": [
                "ws://127.0.0.1:8545"
            ],
            "FilterQuerySize": 2000
        },
        "Ethereum": {
            "Urls": [
                "redacted"
            ],
            "FilterQuerySize": 2000
        },
        "Zenon": {
            "Urls": [
                "ws://127.0.0.1:35998"
            ],
            "FilterQuerySize": 0
        }
    },
    "TssConfig": {
        "Port": 55055,
        "PublicKey": "",
        "DecompressedPublicKey": "",
        "LocalPubKeys": null,
        "Bootstrap": "",
        "PubKeyWhitelist": {},
        "BaseDir": "/root/.orchestrator/tss",
        "BaseConfig": {
            "PartyTimeout": 160000000000,
            "KeyGenTimeout": 900000000000,
            "KeySignTimeout": 240000000000,
            "KeyRegroupTimeout": 60,
            "PreParamTimeout": 900000000000,
            "EnableMonitor": false
        }
    },
    "ProducerKeyFileName": "producer",
    "ProducerKeyFilePassphrase": "redacted",
    "ProducerIndex": 0
}

-------------------------

0x3639 | 2023-06-14 10:05:12 UTC | #46

[quote="mehowz, post:43, topic:61"]
overwriting the old file
[/quote]

@Chadass I was actually making this mistake myself.... until Mehowz pointed it out.

-------------------------

Chadass | 2023-06-14 12:06:13 UTC | #47

So it's

```wget https://github.com/HyperCore-Team/orchestrator/releases/download/v0.0.3-alphanet/orchestrator-linux-amd64.zip```

```
unzip orchestrator-linux-amd64.zip
```

And "A" ?

Then you edit the "old" config file right?

EDIT : It seems to work for now, I forgot ```sudo cp orchestrator-linux-amd64 /usr/local/bin/```

EDIT2 : plz ser add mine here, producer ends with "tjjzl" https://status.hypercore.one/status/orchestrators

-------------------------

0x3639 | 2023-06-14 12:34:46 UTC | #48

```
wget -O orchestrator-linux-amd64.zip https://github.com/HyperCore-Team/orchestrator/releases/download/v0.0.3-alphanet/orchestrator-linux-amd64.zip
unzip orchestrator-linux-amd64.zip
sudo systemctl stop orchestrator
sudo cp orchestrator-linux-amd64 /usr/local/bin/
sudo systemctl start orchestrator
# check status of orchestrator by running next command
sudo systemctl status orchestrator
```

Note: it is `wget -O`

I don't think you are actually upgrading the orchestrator.  What we discovered was that when you `wget` a file with a name that already exists, wget renames the file and adds `.1` after `.zip`. 

Do an `ls` in your download directory and do you see many files with `.zip.1`, `.zip.2`. if so those are the new downloads.  If you are unzipping `.zip` that is the very first download.  And you are unziping it and replace the same binary over and over.  

when you do `wget -O` it will overwrite the filename and will NOT add a number at the end.

-------------------------

0x3639 | 2023-06-14 12:31:43 UTC | #49

I've deleted a few posts in this thread that are confusing (mostly by me).  As the instructions change I'm updating the original post.

-------------------------

mehowz | 2023-06-25 15:56:01 UTC | #50

I can't edit this post, so here is the corrected version:

---------

If you want the orchestrator to restart multiple times after it crashes (in instances where perhaps it can't connect to the Zenon / ETH node and needs to try again/wait between attempts):

@sumamu had shared some configs, and here is a variation of it:

Stop the orchestrator:
```
sudo systemctl stop orchestrator
```
Followed by:
```
sudo nano /etc/systemd/system/orchestrator.service
```

Then add `StartLimitIntervalSec=300s`, `StartLimitBurst=10` and `RestartSec=60` as seen below:

```
[Unit]
Description=Orchestrator Service
After=network.target
StartLimitIntervalSec=300s
StartLimitBurst=10

[Service]
User=root
Group=root
ExecStart=/usr/local/bin/orchestrator-linux-amd64
ExecStop=/usr/bin/pkill -9 orchestrator-linux-amd64
Restart=on-failure
RestartSec=60
TimeoutStopSec=10s
TimeoutStartSec=10s
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=orchestrator

[Install]
WantedBy=multi-user.target
```

Then:

```
sudo systemctl daemon-reload
sudo systemctl start orchestrator
```

In this configuration:

StartLimitIntervalSec=300s: systemd will observe restart attempts within a 300 second (5 minute) interval.

StartLimitBurst=10: If the service fails and restarts more than 10 times within the above interval, systemd will stop trying to restart it until the interval has passed.

Restart=on-failure: The service will be restarted when the process exits with a non-zero exit code.

RestartSec=60: systemd will wait for 60 seconds before trying to restart the service after it has failed.

So, in a scenario where the service continually fails, the Orchestrator service will restart up to 10 times within a 5-minute window, with a delay of 60 seconds between each restart attempt. After 10 failed attempts within this window, systemd will stop trying to restart the service until the 5-minute interval has passed.

-------------------------

0x3639 | 2023-06-27 00:19:24 UTC | #51

I just fixed the edit post issue.  Have you had success with this?  I did not update the original instructions because I have not tested them.  If this is working well, I'll try to update my node and then update the original instructions.

-------------------------

mehowz | 2023-06-28 01:18:18 UTC | #52

Update the binary in 1 command (takes a total of 25 seconds to execute). Include the parentheses when copy/pasting the whole code block -- **and remember to update the the URL path to the .zip file between releases!**

```
(
wget -O orchestrator-linux-amd64.zip https://github.com/HyperCore-Team/orchestrator/releases/download/v0.0.3b-alphanet/orchestrator-linux-amd64.zip
sleep 5 && unzip -o orchestrator-linux-amd64.zip
sleep 5 && sudo systemctl stop orchestrator
sleep 5 && sudo cp orchestrator-linux-amd64 /usr/local/bin/
sleep 5 && sudo systemctl start orchestrator
sleep 5 && sudo systemctl status orchestrator
)
```

-------------------------

0x3639 | 2023-06-28 01:42:46 UTC | #53

Here is an upgrade script to automatically the orchestrator.  

`sudo apt-get install jq`

`nano upgrade.sh`

```
#!/bin/bash

set -e

# Get the latest release from GitHub API
latest_release=$(curl -s https://api.github.com/repos/HyperCore-Team/orchestrator/releases/latest | jq -r ".assets[] | select(.name | contains(\"linux-amd64.zip\")) | .browser_download_url")

# Download the latest release
wget -O orchestrator-linux-amd64.zip "$latest_release"
unzip -o orchestrator-linux-amd64.zip
sudo systemctl stop orchestrator
sleep 5
sudo cp orchestrator-linux-amd64 /usr/local/bin/
sudo systemctl start orchestrator
sleep 5
sudo systemctl status orchestrator
```
To use the script, save the above lines in a file, let's say `upgrade.sh` . Then, run `chmod +x upgrade.sh` to make it executable. You can then run it with `./upgrade.sh` .

-------------------------

