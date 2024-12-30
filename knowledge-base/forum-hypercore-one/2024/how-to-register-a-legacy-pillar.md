Thread: how-to-register-a-legacy-pillar
0x3639 | 2024-03-24 16:17:35 UTC | #1

# How to Registering a Pillar with a Legacy Slot

Below you will find the steps to setup a Node and Register a Legacy Pillar slot with that node.

## Setup the Pillar on Ubuntu 22.04

1. Ensure that GCC is installed on your system. If not, install it using your package manager, e.g., for Ubuntu:
```
sudo apt-get install gcc
```

2. Download the znn_controller in order to start syncing znnd, this will also give you the Producer address.

```
wget https://github.com/zenon-network/znn_controller_dart/releases/download/v0.0.4-alpha/znn_controller-linux-x86_64.zip
unzip znn_controller-linux-x86_64.zip
sudo ./znn_controller
```

3. After running the controller, select `deploy` to deploy the Node and establish the Producer Address

4. Setting up your Firewall. Install UFW (Uncomplicated Firewall) and configure it to allow all outbound and inbound traffic on ports 22 and 35995 for both TCP and UDP:

- **Install UFW**:
Open a terminal and run the following command to install UFW:

```
sudo apt update
sudo apt install ufw
```

- **Enable UFW**:
After installing, you need to enable UFW with the following command:

```
sudo ufw enable
```

- **Allow SSH (Port 22)**:
By default, SSH operates on port 22. To allow inbound and outbound traffic on this port, run:

```
sudo ufw allow 22/tcp
```

- **Allow Traffic on Port 35995 (TCP and UDP)**:
To allow both inbound and outbound traffic on port 35995 for both TCP and UDP, execute the following commands:

```
sudo ufw allow 35995/tcp
sudo ufw allow 35995/udp
```

- **Verify the Rules**:
To ensure that the rules have been added correctly, you can list all the active rules with:

```
sudo ufw status
```

- **Optional - Deny All Incoming Traffic**:
If you want to deny all other incoming traffic (recommended for security reasons) but allow outgoing traffic, you can set the default policies as follows:

```
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Note: This step is optional and is recommended for security. If you perform this step, only the ports you've explicitly allowed (like 22 and 35995) will accept incoming traffic.

- **Reload UFW**:
After making all the changes, reload UFW to apply the new rules:

```
sudo ufw reload
```

That's it! The node should be running and it's being protected by UFW and configured to allow traffic on ports 22 and 35995 for both TCP and UDP. Remember to periodically check and update your firewall rules to ensure the security of your system.

## Build the Modified Dart CLI on the Computer with Syrius
Next we are going to build the ZNN Dart CLI with the `pillar.registerLegacy` command.  Open the computer where `syrius` is installed.  These instructions assume you are using a mac.

### Install Dart SDK (>2.14.0 < 3.0.0)

The cli tool does not support the latest Dart SDK. It is constrained to >2.14.0 < 3.0.0.

Also the znn_sdk_dart (to Sentrify nodes) requires >=2.19.0 <3.0.0. So it is advised to download Dart SDK 2.19.0 (?).

Move into your root directory
```
cd ~
```
Download Dart 2.19.0
```
wget https://storage.googleapis.com/dart-archive/channels/stable/release/2.19.0/sdk/dartsdk-linux-x64-release.zip 
```
Unzip Dart
```
unzip dartsdk-linux-x64-release.zip
```
Copy the Dart sdk into `/usr/local/bin/`
```
sudo cp dart-sdk/bin/dart /usr/local/bin/
```
Update your path to ensure `/usr/local/bin/` is included
```
export PATH="$PATH:/usr/local/bin"
```
Check to make sure Dart is accessible 
```
dart --version
```

### Clone the Dart CLI repository and switch to the correct branch:

```
cd ~
git clone https://github.com/vilkris4/znn_cli_dart.git
cd znn_cli_dart
git checkout register_legacy_pillar
```

### Build the project:

```
make
cd build
```

Once you have the necessary tools set up and have obtained a valid public key and signature needed to register a legacy Pillar, follow these instructions. Every command should be accompanied by the `-u ws://127.0.0.1:35998` flag to connect to a local node.  You cannot use a node with big int support.  These instructions assume you are using the public node provided by hypercore.one.  The instructions were recreated from these [Reference Instructions](https://github.com/vilkris4/znn_cli_dart/blob/register_legacy_pillar/docs/tutorials/legacy_pillar_registration.md).  Please reference them if you are using Windows to run the CLI.  

### Step 1
Fuse 150 QSR as Plasma to the address (NOT the producer address) you will be using for the Pillar.

### Step 2
Verify that the address you will be using for the Pillar has the required ZNN (15,000) and QSR (150,000). Add the `-i` flag to the end of the command and specify the index of the address you will be using for the Pillar. If you are using Syrius, you can view the address list to get the index of the address. The index of the first address is 0, the second one is 1, the third one is 2, etc.

```
./znn-cli balance -i 0 -u wss://legacy.hc1node.com:35998
```
or
```
./znn-cli balance -i 0 -k [KeystoreName] -u wss://legacy.hc1node.com:35998
```

## Step 3
Deposit the 150,000 QSR needed to register the Pillar. The QSR will be burned when the Pillar is registered. Again, add the `-i` flag to the end of the command to specify the index of the address.

```
./znn-cli pillar.depositQsr 150000 -i 0 -u wss://legacy.hc1node.com:35998
```

## Step 4
Wait a short while and verify the QSR was deposited successfully.

```
./znn-cli pillar.getDepositedQsr -i 0 -u wss://legacy.hc1node.com:35998
```

## Step 5
Everything is now set up and the pillar can be registered. You should have obtained the `legacyPillarPubKey` and `legacyPillarSignature` from the seller of the legacy Pillar slot.
Register the pillar with the following command. Replace the arguments with your own values and remember to add the `-i` flag to the end of the command to specify the index of the address you are using.
Double check that there are no typos in the name, since it cannot be changed once the Pillar has been registered.


```
./znn-cli pillar.registerLegacy name producerAddress rewardAddress giveBlockRewardPercentage giveDelegateRewardPercentage legacyPillarPubKey legacyPillarSignature -i 0 -u wss://legacy.hc1node.com:35998
```

**Example command with real arguments:**
```
./znn-cli pillar.registerLegacy Anvil z1qzkd8urw7c4wg6x0cvd2nrzr4ke9d4zh0tvd8s z1qptjd99906x57ej6n55zvmsdm234lngrsreyc2 0 0 BGAjJAT6H2LkTDe3I1Iwoh2XGr+17u8gXI6k1bESJALhW/pInYwN8FEi8zCVUqQc55Tb+GpyP6MpiwCglm2M/Po= H0+k3lo/QvW+myeQ2GzKKjUWyJh96xERkiuyXStNNTocL+5NaCiTjC/b+E2NEHcT1jt/B3gf5L5T1rbXlCfA7VA= -i 0 -u wss://legacy.hc1node.com:35998
```

## Step 6
Wait a short while and verify the Pillar was registered successfully by checking the Pillar list.

```
./znn-cli pillar.list -u wss://legacy.hc1node.com:35998
```

-------------------------

sumamu | 2023-10-10 13:33:24 UTC | #2

Nice work! Thanks for sharing! It's not easy to figure out how to do this.

-------------------------

vilkris | 2023-10-10 13:39:45 UTC | #3

I wouldn't advise on registering the pillar on the VM. Importing your wallet keystore onto a VM is not a good idea.

If you have the address you'll be using for the pillar on your local machine in Syrius, then you can do the pillar registration on your local machine.

The producer address/node still has to be set up on the VM.

-------------------------

0x3639 | 2023-10-10 15:04:15 UTC | #5

[quote="vilkris, post:3, topic:192"]
I wouldn’t advise on registering the pillar on the VM. Importing your wallet keystore onto a VM is not a good idea.
[/quote]

You are right.  These instructions got a little expanded based on feedback from multiple participants.  Initially they were generic but we have expanded them with each not launch.  

But I agree, the 24 seed wallet should NOT be imported into the pillar.  I'm going to adjust these instructions.  I think the issue is many users probably don't have multiple linux machines to do this from.    So doing it from the Pillar is "EZ" but not safe.

-------------------------

0x3639 | 2023-10-10 15:05:22 UTC | #6

[quote="0x3639, post:1, topic:192"]
`wss://secure.deeznnodez.com:35998`
[/quote]

I also wanted to point out that I took down my legacy node recently.  I forgot that users needed it for Legacy Pillar launches.  I will need to get one running again.

-------------------------

vilkris | 2023-10-10 19:09:04 UTC | #7

[quote="0x3639, post:5, topic:192"]
I think the issue is many users probably don’t have multiple linux machines to do this from. So doing it from the Pillar is “EZ” but not safe.
[/quote]
Maybe I'm missing something but why the need for multiple linux machines?

The producer node will of course have to be on a linux machine, but I would think it's easier to register the pillar with your Syrius keystore on your local machine and then use Syrius to control the pillar.

-------------------------

0x3639 | 2023-10-10 19:13:08 UTC | #8

[quote="vilkris, post:7, topic:192"]
The producer node will of course have to be on a linux machine, but I would think it’s easier to register the pillar with your Syrius keystore on your local machine and then use Syrius to control the pillar.
[/quote]

The issue for me was windows.  I run syrius on windows and suck at everything else on windows.  So I needed another linux machine to build the tool.

So when I did it I had the Pillar on a VPS, SYRIUS on windows, and then spun up a local VM on ubuntu to activate the legacy pillar.

-------------------------

