Thread: supernova-evm-extension-chain
aliencoder | 2024-04-12 16:06:16 UTC | #1

# Supernova extension-chain

Supernova will be the first Zenon EVM based extension-chain. Pillars that want to participate in the extension-chain genesis must follow the instructions below.

- Based on [Cronos](https://docs.cronos.org/) codebase
- Full `EVM` support
- `xZNN` used as native gas token
- Transaction fees are burned according to `EIP-1559`
- `ZNN` -> `xZNN` gas fee for redeem
- `xZNN` -> `ZNN` gas fee + 1% swap fee distributed to extension-chain Pillars

## Testnet Parameters

**Chain-id**: `supernova_74506-1`
**Native coin**: `xZNN`
**Management token**: `stake` (only used for Cosmos functionalities)

## Tutorial

I recommend using `Ubuntu 22.04` or latest `Debian` with `>4vCPUs` and `>8GB RAM` to run an extension-chain Pillar. 

Root access is required. The Supernova directory is located at `/root/.supernova`

1. Prepare the environment

```bash
sudo apt update && apt upgrade -y
sudo apt install build-essential jq ufw
sudo ufw enable
sudo ufw allow 26656/tcp  # Tendermint P2P
sudo ufw allow 26657/tcp  # Tendermint RPC
sudo ufw allow 1317/tcp   # Cosmos SDK REST API
sudo ufw allow 8545/tcp   # EVM HTTP RPC
sudo ufw allow 8546/tcp   # EVM WS RPC
sudo ufw reload
```

2. Install Go

```bash
git clone https://github.com/udhos/update-golang
cd update-golang
sudo ./update-golang.sh
source /etc/profile.d/golang_path.sh
```

3. Clone the repo

```bash
cd ~ && git clone https://github.com/alienc0der/supernova
```

4. Build from source:

```bash
cd supernova
git pull
make build
```

5. Add `supernovad` to `PATH`

```bash
echo 'export PATH=$PATH:/root/supernova/build' >> ~/.bashrc
source ~/.bashrc
```

6. Initialize `supernovad`. Replace `pillar_moniker` with the name of your Pillar.

```bash
supernovad init pillar_moniker --chain-id supernova_74506-1
```

7. Add `pillar_moniker` key

```bash
supernovad keys add pillar_moniker
```

8. Mint `stake` for the `pillar_moniker` account

```bash
supernovad add-genesis-account pillar_moniker 1500000000000000000000stake
```

9. Open Syrius desktop wallet, import your `producer` keystore from the Pillar's machine and sign a message

Obtain the your own `tendermint/PubKeyEd25519` using the following command:

```bash
cat ~/.supernova/config/priv_validator_key.json | jq -r '.pub_key.value'
```

Extract the `tendermint/PubKeyEd25519` public key and sign the following message:

```
Supernova *insert tendermint/PubKeyEd25519*
```

Example message (use your own `tendermint/PubKeyEd25519` extracted earlier using the `cat` command instead of the dummy "EmqJ95SK1AyKdTpauS9Fv7zmWrfIG+y+vX7h5vRQF9E=":

```
Supernova EmqJ95SK1AyKdTpauS9Fv7zmWrfIG+y+vX7h5vRQF9E=
```

Copy the signature. You will need it in the next step.

9. Issue `gentx` command with the signature from the previous step

Please note that the last parameter is `--details *insert signature*`. Replace *insert signature* with the actual signature from the previous step.

```bash
supernovad gentx pillar_moniker 1000000000000000000000stake --chain-id supernova_74506-1 --moniker="pillar_moniker" --min-self-delegation="1000000" --details *insert signature* --ip="127.0.0.1"
```

If successful, you will get the following message in the terminal window: 

**Genesis transaction written to /root/.supernova/config/gentx/gentx-0x0x0x0x0x0x0x0x0x0x.json**.

:triangular_flag_on_post: :triangular_flag_on_post: :triangular_flag_on_post: Privacy warning: remove the "memo" field from the `gentx` that contains the public IP of the VPS instance where the validator will be hosted. For a secure operation of the extension-chain validator, please check Step 11.

10. Send me via DM the resulting `gentx-0x0x0x0x0x0x0x0x0x0x.json`. Once there are more than 5 extension-chain Pillars, I will compile the `genesis.json` and post it here. After that we can coordinate to unleash the Supernova.

11. Setup a [Sentry node](https://docs.tendermint.com/v0.33/tendermint-core/validators.html) for the extension-chain Pillar (optional, recommended)

Create a new VPS with similar specs. Follow Steps 1 - 5. After that, initialize the sentry node:

```bash
supernovad init sentry --chain-id supernova_74506-1
```

Navigate to the configuration directory and edit the `config.toml` file with the parameters from the tables below. Peers are identified by `node_id@ip:port`. In order to get the `node_id`, use the following command:

```bash
supernovad tendermint show-node-id
```

```bash
vim /root/.supernova/config/config.toml
```

#### Validator Node Configuration
|Config [p2p]|Setting|
|---|---|
|pex|false|
|persistent_peers|list of sentry_node_id@ip:port|
|private_peer_ids|none|
|unconditional_peer_ids|optionally list sentry_node_id@ip:port|
|addr_book_strict|false|

#### Sentry Node Configuration
|Config [p2p]|Setting|
|---|---|
|pex|true|
|persistent_peers|validator_node_id@ip:port, optionally list sentry_node_id@ip:port|
|private_peer_ids|validator_node_id|
|unconditional_peer_ids|validator_node_id@ip:port, optionally list sentry_node_id@ip:port|
|addr_book_strict|false|

12. Enable EVM RPC endpoint for the Sentry node (optional)

SSH into your Sentry instance. Navigate to the configuration directory and edit the `app.toml` file with the parameters from the table below.

```bash
vim /root/.supernova/config/app.toml
```

|Config [json-rpc]|Setting|
|---|---|
|address|0.0.0.0:8545|
|ws-address|0.0.0.0:8546|

13. Setup a seed node (optional)

Create a new VPS with similar specs. Follow Steps 1 - 5. After that, initialize the seed node:

```bash
supernovad init seed --chain-id supernova_74506-1
```

Navigate to the configuration directory and edit the `config.toml` file with the parameters from the table below.

#### Seed Node Configuration
|Config [p2p]|Setting|
|---|---|
|laddr|tcp://0.0.0.0:26656|
|external_address|vps_instance_public_ip:26656|
|seed_mode|true|

14. Add Supernova seed nodes (kudos @0x3639 @tapwoot @coinselor)

Navigate to the configuration directory and edit the `config.toml` file with the following seed nodes:

```
seeds = "b91ab16e7454eeaabcb0d4c5d2f900a08ed518aa@5.196.22.239:26656,7efe3e47afbbf38c44179d3802aee4cad7af47eb@208.115.200.55:26656,7cd3cb605a8da6a7be20736c171ee33d307d6f88@3.94.70.251:26656"
```

15. Setup a **Systemd service** (optional, recommended)

```bash
cp /root/supernova/build/supernovad /usr/local/bin/supernovad
sudo nano /etc/systemd/system/supernova.service
```

Assuming you've completed Step 5, paste the following configuration:

```
[Unit]
Description=supernova service
After=network.target
[Service]
LimitNOFILE=32768
User=root
Group=root
Type=simple
SuccessExitStatus=SIGKILL 9
ExecStart=/usr/local/bin/supernovad start
ExecStop=/usr/bin/pkill -9 supernovad
Restart=on-failure
TimeoutStopSec=10s
TimeoutStartSec=10s
[Install]
WantedBy=multi-user.target
```

Save and reload the configuration:

```bash
systemctl daemon-reload
```

Now please wait until the `genesis.json` contains all xchain Pillars that want to participate in the Gensis of the Supernova extension-chain.

After the final version of the `genesis.json` is uploaded on your machine, please start the `supernovad` service:

```bash
systemctl start supernova.service
```

❗❗❗ Please make sure you're running the latest `supernovad` binary ❗❗❗ 

```bash
cd /root/supernova
git pull
make build
```

-------------------------

0x3639 | 2024-04-01 10:34:01 UTC | #2

what ports need to be open?

-------------------------

0x3639 | 2024-04-01 10:54:53 UTC | #3

[quote="aliencoder, post:1, topic:1862"]
```
supernovad keys add pillar_moniker
```
[/quote]

how should we respond to this question?

root@evm:~/supernova# supernovad keys add DeeZNNutz.com 
Enter keyring passphrase (attempt 1/3):

-------------------------

aliencoder | 2024-04-01 11:26:57 UTC | #4

[quote="0x3639, post:2, topic:1862, full:true"]
what ports need to be open?
[/quote]

I will provide the next steps zoon. 

At the moment we should focus on creating the `genesis.json` file.

[quote="0x3639, post:3, topic:1862"]
how should we respond to this question?
[/quote]

[quote="aliencoder, post:1, topic:1862"]
```
supernovad keys add deeznnutz
```
[/quote]

Input a strong passphrase. Make sure you remember it. You'll need it each time you make operations involving the `deeznnutz` key.

-------------------------

0x3639 | 2024-04-01 13:01:04 UTC | #5

[quote="aliencoder, post:1, topic:1862"]
`apt install build-essential`
[/quote]

should we add `jq`?

-------------------------

0x3639 | 2024-04-01 13:10:11 UTC | #6

[quote="aliencoder, post:1, topic:1862"]
`Supernova EmqJ95SK1AyKdTpauS9Fv7zmWrfIG+y+vX7h5vRQF9E=`
[/quote]

just wanted to confirm that this is the message we need to sign in syrius (with the pillar address), correct?

-------------------------

NeoShredder | 2024-04-01 13:12:27 UTC | #7

How long till mainnet?

-------------------------

0x3639 | 2024-04-01 13:42:22 UTC | #8

[quote="aliencoder, post:1, topic:1862"]
```
supernovad gentx validator 1000000000000000000000stake --chain-id supernova_73406-1 --moniker="pillar_moniker" --min-self-delegation="1000000" --details *insert signature*
```
[/quote]

I get this response.  I did replace `--details *insert signature*` with `--details MY SIGNATURE FROM SYRIUS`

Error: failed to fetch 'validator' from the keyring: validator.info: key not found
Usage:

I also noticed this command has `--details` without `=` and the others have `--command="info"`.  I also noticed  `--chain-id supernova_73406-1` does not have an `=`.  Is this correct?

-------------------------

mehowbrainz | 2024-04-01 13:37:05 UTC | #9

Thanks and congrats @aliencoder. #HyperGrowth Pillar be participating with 1 validator for the moment, open to more if needed but would like to let others join.

-------------------------

aliencoder | 2024-04-01 13:52:21 UTC | #10

[quote="0x3639, post:5, topic:1862"]
should we add `jq`?
[/quote]

Just added it.

[quote="0x3639, post:6, topic:1862"]
just wanted to confirm that this is the message we need to sign in syrius (with the pillar address), correct?
[/quote]

The message you need to sign in syrius using the Pillar's producer keystore is "Supernova *insert tendermint/PubKeyEd25519*" where `tendermint/PubKeyEd25519` was extracted earlier using the `cat ~/.supernova/config/priv_validator_key.json | jq -r '.pub_key.value'` command.

[quote="NeoShredder, post:7, topic:1862, full:true"]
How long till mainnet?
[/quote]

Testnet and after that mainnet.

[quote="0x3639, post:8, topic:1862"]
Error: failed to fetch ‘validator’ from the keyring: validator.info: key not found
[/quote]

Good catch. I've edited the post. Replace `validator` with `pillar_moniker` from Step 6.

[quote="0x3639, post:8, topic:1862"]
I also noticed this command has `--details` without `=` and the others have `--command="info"`
[/quote]

Flags can be used either way: `--details SIGNATURE` or `--details="SIGNATURE"`, doesn't matter.

[quote="0x3639, post:8, topic:1862"]
I also noticed `--chain-id supernova_73406-1` does not have an `=`. Is this correct?
[/quote]

It works both ways. The `chainId` is `supernova_73406-1`. This is the Cosmos `chainId` format. The EVM will have `73406` chain identifier.

-------------------------

0x3639 | 2024-04-01 13:57:58 UTC | #11

DeeZ Bizzles was able to complete the steps.

-------------------------

shaimo | 2024-04-01 14:00:54 UTC | #12

Does it run on the same machine as the pillar or a separate one? What are the hardware requirements?

-------------------------

aliencoder | 2024-04-01 14:04:56 UTC | #13

[quote="shaimo, post:12, topic:1862"]
Does it run on the same machine as the pillar or a separate one?
[/quote]

If you have high specs on the Pillar you can run it on the same machine, but I don't recommend it. A separate instance is better in the long run.

[quote="shaimo, post:12, topic:1862"]
What are the hardware requirements?
[/quote]

[quote="aliencoder, post:1, topic:1862"]
I recommend using `Ubuntu 22.04` or latest `Debian` with `>4vCPUs` and `>8GB RAM` to run an extension-chain Pillar.
[/quote]

-------------------------

coinselor | 2024-04-01 14:32:46 UTC | #14

How about storage? The differences in the specs you linked are quite significant.

![image|579x406](upload://yxQT3s7kXkkr5UNsG2Bt3nV6CkU.png)

-------------------------

aliencoder | 2024-04-01 15:28:02 UTC | #15

Indeed, the storage can add up by a lot over a long period of time. I think the community should also run some archive nodes in order to be able to setup a reliable block explorer.

-------------------------

aliencoder | 2024-04-01 21:20:24 UTC | #16

@0x3639 volunteered to run a seed node that will be used to bootstrap the p2p network. I've updated the post to include instructions on how to run a seed node (step 13).

Anyone else that want to run a seed node?

-------------------------

coinselor | 2024-04-01 21:27:52 UTC | #17

[quote="aliencoder, post:16, topic:1862"]
a seed node?
[/quote]

Is this just a sentry/public node with a file with hardcoded ips for other seed nodes?

I'm still wainting on VPS provisioning. Would it make sense to have the Validator be a full archival node and connect to two sentries that act as pruned nodes? Can I have one of those pruned sentries act as a seed node? Then, sign me up.

Also, can you point out where to change the prunning setting, so I can set the validator as an archival node. Or, if that's the default, change it for the sentries.

-------------------------

aliencoder | 2024-04-01 21:52:04 UTC | #18

[quote="coinselor, post:17, topic:1862"]
Is this just a sentry/public node with a file with hardcoded ips for other seed nodes?
[/quote]

No. It's used by other nodes to discover peers. Nothing is hardcoded. While the seed node itself doesn't need a list of seeds, its `nodeID@IP:PORT` will be shared with other nodes in the network. They will add the seed node's address to their `config.toml` under `p2p.seeds`.

[quote="coinselor, post:17, topic:1862"]
Would it make sense to have the Validator be a full archival node and connect to two sentries that act as pruned nodes?
[/quote]

It's possible, yes.

[quote="coinselor, post:17, topic:1862"]
Can I have one of those pruned sentries act as a seed node?
[/quote]

I wouldn't mix sentries with seed nodes. They serve different purposes. One sentry per validator is enough at the moment.

[quote="coinselor, post:17, topic:1862"]
Also, can you point out where to change the pruning setting
[/quote]

Navigate to `/root/.supernova/config/app.toml` and set `pruning = nothing` for an archival node.

-------------------------

sultanofstaking | 2024-04-01 22:45:01 UTC | #19

[quote="aliencoder, post:1, topic:1862"]
Setup a [Sentry node ](https://docs.tendermint.com/v0.33/tendermint-core/validators.html) for the extension-chain Pillar
[/quote]

As long as pillar is behind sentry we can skip this for now? Know not priority but a topology specific to NoM similar to the referenced material would be helpful with pillars, sentries, orchestrators, evm, public nodes, soon sentinels

-------------------------

aliencoder | 2024-04-02 08:08:46 UTC | #20

[quote="sultanofstaking, post:19, topic:1862"]
As long as pillar is behind sentry we can skip this for now?
[/quote]

You can install the Tendermint Sentry on one of your existing NoM Sentry machines. They shouldn't overlap since they're using different ports.

-------------------------

aliencoder | 2024-04-05 21:18:52 UTC | #21

❗❗❗ Please make sure you're running the latest `supernovad` binary ❗❗❗ 

```bash
cd /root/supernova
git pull
make build
```

Kudos to @0x3639 @tapwoot for the seed nodes. Please add them in the `config.toml` (Step 14).

-------------------------

aliencoder | 2024-04-12 16:23:02 UTC | #22

Actually all producer keystores must have the pubkey exposed because they are signing momentums. But I've only searched in the Zenon Tools explorer UI.

I need the public key in `hex` format. I'll ask again for both the public key and the signature.

Current status:

@0x3639 :white_check_mark: :seedling:
@coinselor :white_check_mark: :seedling:
@tapwoot :white_check_mark: :seedling:
@mehowz :white_check_mark: :seedling:
@SultanOfStaking :white_check_mark:
@edgepillar :white_check_mark:
@sugoibtc :white_check_mark:
@nbd :white_check_mark:

Kudos again @0x3639 @coinselor @tapwoot for the seeder nodes :seedling:

-------------------------

DrD3 | 2024-04-06 21:18:52 UTC | #23

how many do we need active for the extension to run?

-------------------------

aliencoder | 2024-04-06 21:50:04 UTC | #24

A minimum of 3 extension-chain Pillars.

I'll wait for @mehowbrainz @nbd and after that I'll post the `genesis.json` with `genesis_time ` 12 hours into the future, such that everyone will have enough time to upload the genesis and start the `supernova` service.

-------------------------

aliencoder | 2024-04-07 12:48:29 UTC | #25

Unfortunately, I've discovered a small mistake in the `gentx` command (the `chain-id`) and you'll need to redo the genesis transaction for your extension-chain Pillar.

```bash
rm -rf /root/.supernova/config/gentx/gentx-*
supernovad gentx pillar_moniker 1000000000000000000000stake --chain-id supernova_74506-1 --moniker="pillar_moniker" --min-self-delegation="1000000" --details *insert signature*  --ip="127.0.0.1"
```

Please note that I've added the `--ip` parameter where I've specified the localhost instead of the public IP. We can't remove the `memo` field after it's signed because we invalidate the signature by doing so.

-------------------------

aliencoder | 2024-04-07 18:39:31 UTC | #26

Check the hash of the `genesis.json` file:

```bash
sha256sum genesis.json
```

Should output:

```
76852615be093232825da9e16bc801445316a191bb7e4e7f806fde0cc9b42478
```

Commands to run:

```bash
supernovad tendermint unsafe-reset-all
rm /root/.supernova/config/genesis.json
nano /root/.supernova/config/genesis.json
```

Paste the contents of the `genesis.json` and `Control+x` to exit and `Y` to save. 

Fixing the `supernova.service`:

```bash
cp /root/supernova/build/supernovad /usr/local/bin/supernovad
```

Edit this line from `supernova.service`:
...
ExecStart=/usr/local/bin/supernovad start
...

```bash
systemctl daemon-reload 
```

After that you can start the `supernova service`:

```bash
systemctl start supernova.service
```

-------------------------

aliencoder | 2024-04-12 16:22:24 UTC | #27

Please add @mehowbrainz's seed node to the `seeds` entry in the `config.toml`:

```
seeds = "b91ab16e7454eeaabcb0d4c5d2f900a08ed518aa@5.196.22.239:26656,7efe3e47afbbf38c44179d3802aee4cad7af47eb@208.115.200.55:26656,7cd3cb605a8da6a7be20736c171ee33d307d6f88@3.94.70.251:26656"
```

-------------------------

aliencoder | 2024-04-24 21:34:23 UTC | #28

I will prepare the mainnet rollout for Supernova ZVM. We still need to accomplish 2 things in the meanwhile:

1. A fully functional explorer: @mehowz’s dev is helping us with devops and @0x3639 can host the archive node for it.
2. A fully functional bridge interface to seamlessly swap `ZNN` and `xZNN`. Here @dexter703 can help us or anyone that has experience with frontend development.

-------------------------

everlastingOS | 2024-04-25 19:59:12 UTC | #30

[quote="aliencoder, post:28, topic:1862"]
A fully functional bridge interface to seamlessly swap `ZNN` and `xZNN`. Here @dexter703 can help us or anyone that has experience with frontend development.
[/quote]

Is it possible to have a P2P bridge in S Y R I U S?

-------------------------

aliencoder | 2024-04-26 09:18:19 UTC | #31

[quote="everlastingOS, post:30, topic:1862"]
Is it possible to have a P2P bridge in S Y R I U S?
[/quote]

The swaps between `xZNN` and `ZNN` are enabled by the bridge `orchestrators`. If anyone is interested in creating a bridge interface in Flutter, then we can integrate it directly into Syrius. 

But we first need support for Ethereum in Syrius to make this possible (Supernova uses Ethereum's `secp256k1` and RPCs to operate).

-------------------------

DyDDy | 2024-04-26 11:42:38 UTC | #32

@aliencoder If you need any help with art stuff, or a collection to test (NFT) please let me know via TG (@itsdyddy) or here.

-------------------------

aliencoder | 2024-04-27 12:29:18 UTC | #33

[quote="DyDDy, post:32, topic:1862"]
or a collection to test
[/quote]

You can prepare a new collection for the extension-chain mainnet launch (zoon).

-------------------------

dexter703 | 2024-06-06 09:10:52 UTC | #34

Hello, Aliens :vulcan_salute:

[quote="aliencoder, post:28, topic:1862"]
1. A fully functional bridge interface to seamlessly swap `ZNN` and `xZNN`. Here @dexter703 can help us or anyone that has experience with frontend development.
[/quote]

I've re-purposed the Zenon Bridge interface to support Supernova ZVM.

Supernova Testnet Bridge interface:

https://bridge.supernova-testnet.zenon.community

@0x3639 @mehowbrainz @aliencoder you can start testing it.

-------------------------

aliencoder | 2024-06-09 20:13:02 UTC | #35

Thank you @dexter703! You've done an amazing work so far!

I've released a statically linked `supernovad` binary with `rocksdb` support to enable faster transaction throughput and block sync.

`rocksdb` is much more efficient than `goleveldb` given that it's written in `C++` and is maintained by Facebook:

https://github.com/facebook/rocksdb/

Please download and update your `supernovad` binary:

https://github.com/alienc0der/supernova/releases/tag/v0.0.1-50-g365b09c-2-gf52ef95

If you're running a `supernova` node, please:

1. Delete all blockchain files from `~/.supernova/data` directory,
2. Add `db_backend = "rocksdb"` to `~/.supernova/config/config.toml`.
3. Resync from scratch. `rocksdb` is not compatible with `goleveldb` format.

It is mandatory by all Pillars that run extension-chain validators to upgrade to `supernovad` with `rocksdb` support.

-------------------------

