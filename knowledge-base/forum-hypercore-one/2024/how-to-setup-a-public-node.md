Thread: how-to-setup-a-public-node
0x3639 | 2024-03-23 21:30:51 UTC | #1

Copy and paste instructions to setup a public node on Zenon Network with Ubuntu.

## Minimum Requirements
- 4 vCPU
- 16G RAM (Nodes can operate with less than 16G of ram but can take extra time to sync from scratch.  If syncing from scratch 16G is highly recommended)
- Ubuntu 22.04 or 20.04 

## Steps to Setup
Update and upgrade your VPS

```
sudo apt-get update
sudo apt-get upgrade
```

Open the following ports in your firewall. Please note a public static IP is required.

TCP: 35995
UDP: 35995

Install ZIP and dynamic swapfile

```
sudo apt-get install zip
sudo apt-get install dphys-swapfile
```

Reboot the VPS

```
sudo reboot
```

Download the ZNN Controller Software

```
wget https://github.com/zenon-network/znn_controller_dart/releases/download/v0.0.4-alpha/znn_controller-linux-x86_64.zip
```

Unzip the file

```
unzip znn_controller-linux-x86_64.zip
```

Run the ZNN Controller installation software

```
sudo ./znn-controller
```

You should see the following output

```
Running ZNN Controller with superuser privileges
ZNN Node Controller v0.0.3 [NOTE THIS IS OLD]
Gathering system information ...
System info:
Shell: bash
User: REMOVE
Host: REMOVE
Operating system: linux
OS version: Linux 5.11.0-1022-aws #23~20.04.1-Ubuntu SMP Mon Nov 15 14:03:19 UTC 2021
Available CPU cores: 2
Dart runtime: 2.16.2 (stable) (Tue Mar 22 13:15:13 2022 +0100) on "linux_x64"
IP address: [IP ADDRESS]
  1) Deploy
  2) Status
  3) Start service
  4) Stop service
  5) Resync
  6) Help
  7) Quit
Select an option from the ones listed above
```

Select Option 1. This will download the latest node software and install everything required to run the node. This will automatically setup a service that runs on reboot. After the node is done downloading the blockchain it will be available to use in the syrius wallet.

-------------------------

