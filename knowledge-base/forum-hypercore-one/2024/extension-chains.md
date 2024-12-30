Thread: extension-chains
aliencoder | 2023-05-09 19:31:50 UTC | #1

In my opinion a Layer-2 and/or sidechain implementation will bring EVM/WASM compatibility for NoM and will greatly expand the ecosystem. The NoM Multichain Technology can become a de-facto hub for interoperability within the ecosystem.

This way, the base layer remains minimal & efficient as Mr Kaine emphasizes and all the heavy work/bloat is kept in a separate execution domain.

Pillars produce inflation as `ZNN` and they will also run the `orchestrator` nodes. It makes sense for them to also act as validators for a L2/sidechain where fees are paid in `ZNN`. The L2/sidechain should not produce additional/separate inflation. Pillars can bridge part of their `ZNN` inflation into the L2/sidechain ecosystem and they will be incentivized to bridge more if usage is high.

`ZNN` is not a gas token because the L2/sidechain will use a wrapped representation of it. It can be called `eZNN` or `xZNN` (execution ZNN).

We can use the decentralized bridge @sumamu built and tweak it to support this type of wrapping. It would be a little bit different from wrapping `ZNN` to `wZNN` and unwrapping it later because `xZNN` will actually be consumed/burnt in the extension chain, so it won’t be a 1:1 backing.

`xZNN` can be associated with the gas concept for the extension chain.

Since there won’t be any inflation, the extension chain will only have a fee distribution mechanism:

* 33% distributed to builders (contract deployers)
* 33% distributed to extension chain validators
* 34% burned (similar to ETH)

-------------------------

aliencoder | 2023-05-09 19:33:12 UTC | #2

Wanted to discuss how to approach the extension chain development.

-------------------------

0x3639 | 2023-05-10 09:32:24 UTC | #3

Are there any other chains like this that I can read about?  

Wanted to make sure you saw this.  @georgezgeorgez shared it some time ago: https://mirror.xyz/sovlabs.eth/pZl5kAtNIRQiKAjuFvDOQCmFIamGnf0oul3as_DhqGA

Will this be a zkrollup L2?

What sort of validator requirements do you think we will have?

Just want to make sure I understand how the ZNN > xZNN would work.  Alice deposits 100 ZNN into the "portal" and gets 100 xZNN on the L2. Alice does some "stuff" on the L2 and pays 3 xZNN in fees.  The fees are paid to the deployer (1) , validator (1) , and burned (1).   We have 100 ZNN locked up and 99 xZNN accounted for.  

When the 1 xZNN is burned, I assume that also burns the ZNN also?  There was another Cosmos chain that had a model like this that mooned a few months ago.  Need to find it. We should look at how the fee mechanism worked.

-------------------------

georgezgeorgez | 2023-05-10 02:23:38 UTC | #4

> It would be a little bit different from wrapping `ZNN` to `wZNN` and unwrapping it later because `xZNN` will actually be consumed/burnt in the extension chain, so it won’t be a 1:1 backing.

-------------------------

0x3639 | 2023-05-10 02:25:24 UTC | #5

Canto...  The shitposting on Twitter was so insane I actually had to block the word $canto.  Maybe we should look at the tokenomics.  

## How Does Canto Work?

Canto advocates for DeFi primitives like decentralized exchanges, lending protocols, and units of account to be public utilities. That is why they are provided free-to-use on Canto. In other words, a Canto DEX, a Canto Lending Market, and a fully collateralized stablecoin are all built natively into Canto.

Canto aims to pioneer the concept of rent extraction resistance. As part of its policy to provide free public infrastructure, Canto designed its smart contracts in a revenue-sharing manner. More precisely, smart contract creators receive a 20% share of all transaction fees generated from users interacting with a project. The aim is to provide a new ground for economic experiments in [web3](https://coinmarketcap.com/alexandria/glossary/web-3-0), where DeFi builders and [NFT](https://coinmarketcap.com/alexandria/glossary/non-fungible-token) creators can collectively benefit from a flourishing blockchain ecosystem.

https://www.youtube.com/watch?v=vba3Fdx1960

-------------------------

aliencoder | 2023-05-10 08:46:36 UTC | #6

[quote="0x3639, post:3, topic:52"]
Will this be a zkrollup L2?
[/quote]

No. As MrK mentioned, this would be more like a sidechain.

@sumamu has the necessary resources to build a proper zero-knowledge based L2.

[quote="0x3639, post:5, topic:52"]
Maybe we should look at the tokenomics.
[/quote]

I've already investigated Canto and why it mooned. The golden fee was in place: `contractDeploymentFee`

This single piece of ingenuity attracts builders which in turn attract users.

That's why I proposed the following fee distribution mechanism:

[quote="aliencoder, post:1, topic:52"]

* 33% distributed to builders (contract deployers)
* 33% distributed to extension chain validators
* 34% burned (similar to ETH)
[/quote]

What I really want to debate is how the extension chain will interact with the mainchain.

-------------------------

0x3639 | 2023-05-10 09:58:38 UTC | #7

got it.  so will the contract deployer and chain validators receive $ZNN or $xZNN?

-------------------------

0x3639 | 2023-05-15 11:09:45 UTC | #8

[quote="aliencoder, post:6, topic:52"]
What I really want to debate is how the extension chain will interact with the mainchain.
[/quote]

@georgezgeorgez do you have any thoughts on this question?  

[quote="georgezgeorgez, post:4, topic:52"]
It would be a little bit different from wrapping `ZNN` to `wZNN` and unwrapping it later because `xZNN` will actually be consumed/burnt in the extension chain, so it won’t be a 1:1 backing.
[/quote]

If I understand this correctly, users will not own xZNN.  When a contract is called on the sidechain, (and per the 33%, 33%, 34% distribution above), the builder received 0.33 ZNN, the validators receive 0.33 ZNN, and 0.34 ZNN is burned.  this 1 ZNN will get represented as 1 xZNN on the sidechain and it will be consumed entirely to do the work.  Is this correct?

-------------------------

aliencoder | 2023-05-15 13:45:11 UTC | #9

[quote="0x3639, post:7, topic:52"]
so will the contract deployer and chain validators receive $ZNN or $xZNN?
[/quote]

Users will bridge/swap/convert `ZNN` for `xZNN` through an embedded contract (eg `ext-chain-embedded`) in order to be able to use their favorite dApps that will be live on the extension chain (for example Unizwap, games, meme tokens, NFT collections, etc.).

Users will be required to pay gas fees to interact with the EVM smart contracts. Therefore, they will consume `xZNN` and it will be redistributed according to the specified percentages directly by the system contract to the contract deployer, burn address and ext-chain validators.

More users => more activity => higher gas fees => more `xZNN` gets consumed => higher payouts for builders and validators and less `ZNN` in circulation. It's a win-win-win situation for everybody.

The embedded that will convert `ZNN` to `xZNN` needs to be carefully designed, because there won't be a 1:1 backing (we need to take into account `xZNN` burning).

-------------------------

Blueginger | 2023-08-07 18:53:12 UTC | #10

Any updates?

-------------------------

aliencoder | 2023-08-07 20:12:25 UTC | #11

I'm finishing some work on Syrius and will get back to the `ext-chain` development.

-------------------------

Chadass | 2023-08-15 08:44:00 UTC | #12

One the ext chain is live on testnet it could be great, marketing wise, to run a stresstest on it. Just seeing those sweet sweet millions tps rolling in

-------------------------

aliencoder | 2023-09-04 08:39:07 UTC | #13

The first EVM compatible extension chain is now live :alien: :flying_saucer:

How to connect an EVM compatible wallet to the `ext-chain`:

1. Install [Metamask](https://metamask.io/)
2. Create a new wallet
3. Go to `Settings` -> `Networks`

- Network name: `XZNN`
- New RPC URL: https://ext-testnet.zenon.community
- ChainID: 73405
- Symbol: `xZNN`

4. Post your address below and request `xZNN` for testing. Maximum amount is `10000 xZNN` per user.

-------------------------

Chadass | 2023-09-03 00:29:29 UTC | #14

Who will be running the nodes when the chain enter in mainnet stage?

-------------------------

aliencoder | 2023-09-03 09:50:22 UTC | #15

This is still an open question. One possibility is to create a `restaking` embedded where Pillars or Sentinels can register to be part of the validation set of the `ext-chain`.

-------------------------

0x3639 | 2023-09-03 21:34:38 UTC | #16

[quote="aliencoder, post:13, topic:52"]
4, Post your address below and request `xZNN` for testing. Maximum amount is `10000 xZNN` per user.
[/quote]

0x6DF301ECe246B1eedBDB3db61B96be495db80e03

-------------------------

aliencoder | 2023-09-12 21:51:14 UTC | #17

[quote="0x3639, post:16, topic:52"]
0x6DF301ECe246B1eedBDB3db61B96be495db80e03
[/quote]

Sent. Please check.

-------------------------

tapwoot | 2023-09-18 19:17:38 UTC | #18

pls send me xZNN 
0x61C94aaC2842d1A93f6BF4ab8873504a52717bD9

getting this error, RPC URL isn't working atm?

![image|382x500](upload://g8tWW7EUSn5LkcxwR1uPyr8lT5V.png)

-------------------------

aliencoder | 2023-09-18 20:34:36 UTC | #19

[quote="tapwoot, post:18, topic:52"]
getting this error, RPC URL isn’t working atm?
[/quote]

Yes. New updated will be pushed soon. The testnet will be up again in the following days.

-------------------------

sol | 2023-09-18 22:48:33 UTC | #20

I was having this issue in Firefox, but not Chrome. I can't explain why.

-------------------------

0x3639 | 2023-11-30 01:26:38 UTC | #21

![Screenshot 2023-11-29 at 7.26.00 PM|690x302](upload://tyB36ppk0DnQYzH3u66YrcUjPXT.png)

-------------------------

aliencoder | 2023-12-02 08:30:07 UTC | #22

Try again now:

Network name: **XZNN**
New RPC URL: **https://ext-testnet.zenon.community**
Chain ID: 73405
Currency symbol: **xZNN**
Block explorer URL: **TBA**

I've sent you 10000 XZNN here: 0x61C94aaC2842d1A93f6BF4ab8873504a52717bD9

-------------------------

Stark | 2023-12-03 15:20:40 UTC | #23

xZNN please, sir.
excited to test.

-------------------------

aliencoder | 2023-12-03 19:47:35 UTC | #24

[quote="Stark, post:23, topic:52"]
xZNN please, sir.
[/quote]

Post your address.

-------------------------

Stark | 2023-12-04 22:50:52 UTC | #25

0x707B4911d50B5a3b55b01f1C6bbE57ea5db6a372
:face_with_peeking_eye:

-------------------------

aliencoder | 2024-03-20 14:13:48 UTC | #26

After many attempts to find a good candidate for the extension-chain codebase, I finally settled for [Cronos](https://github.com/crypto-org-chain/cronos).

It has a cleaner codebase than OKX's exchain and also a well maintained [Ethermint](https://github.com/crypto-org-chain/ethermint) dependency.

Other clean Ethermint implementations like Evmos or Berachain have [restrictive licensing terms](https://github.com/evmos/evmos/blob/main/LICENSE) that limit fair usage.

Ethermint follows [EIP-1559](https://eips.ethereum.org/EIPS/eip-1559). This means the the extension-chain will also inherit this burning fee mechanism.

At the moment this aligns with the objective to create a deflationary force within the ecosystem, given the fact that the extension-chain won't have any inflation at all.

Users will be able to wrap `ZNN` into `xZNN` and use it to pay gas fees in order to interact with EVM smart contracts on the extension-chain.

Pillars will need to run the infrastructure. Given it's a Cosmos fork, a small number of Pillars is required to bootstrap the network (up to 20 Pillars).

However, the [specs](https://docs.cronos.org/for-node-hosts/running-nodes/cronos-mainnet) required to join this validator set are a bit higher than a typical `znnd` node in terms of hardware resources.

We can further incentivize extension-chain Pillar nodes with a `ZNN` bridge fee (when user enter or exit the extension-chain).

I want to hear your opinions on this subject.

-------------------------

0x3639 | 2024-03-20 14:18:17 UTC | #27

[quote="aliencoder, post:26, topic:52"]
However, the [specs ](https://docs.cronos.org/for-node-hosts/running-nodes/cronos-mainnet)
[/quote]

Which DB are we running?  The RAM requirements are different.

> RAM: 4 GB (LevelDB) or 64G RAM (RocksDB)

-------------------------

aliencoder | 2024-03-20 15:05:48 UTC | #28

[quote="0x3639, post:27, topic:52"]
Which DB are we running?
[/quote]

Since we won't have huge activity right from the beginning, I'd go with [goleveldb](https://crypto-org.gitbook.io/cronos-documentation-3/for-node-hosts/running-nodes/cronos-node-best-practises#db_backend).

[quote="aliencoder, post:26, topic:52"]
We can further incentivize extension-chain Pillar nodes with a `ZNN` bridge fee (when user enter or exit the extension-chain).
[/quote]

What do you think about this? We can collect exit fees from users and distribute them to active extension-chain Pillars.

-------------------------

0x3639 | 2024-03-20 15:47:38 UTC | #29

[quote="aliencoder, post:28, topic:52"]
What do you think about this? We can collect exit fees from users and distribute them to active extension-chain Pillars.
[/quote]

I think previously we discussed a fee model in the xChain that was 33% to smart contract, 33% to validators and 34% burned.  Is that not feasible?

Maybe we should research how other are doing this where a native token is not involved.  It's probably entrance / exit fee or a share of the TX fees for interacting with smart contracts.  I'll search around and see what I learn.

-------------------------

aliencoder | 2024-03-20 16:09:42 UTC | #30

[quote="0x3639, post:29, topic:52"]
I think previously we discussed a fee model in the xChain that was 33% to smart contract, 33% to validators and 34% burned. Is that not feasible?
[/quote]

It's feasible, but not in the short term. The default fee mechanism for Ethermint is EIP-1559 and changing it requires time and resources.

[quote="0x3639, post:29, topic:52"]
It’s probably entrance / exit fee
[/quote]

We don't want to put an entrance tax because we want to drive users into the extension-chain where they have EVM to play with. Custom transaction fees are more difficult to implement. 

What we want to achieve now is a sustainable extension-chain that drives value to the ecosystem in the short term. Burning `xZNN` fees will drive the demand for native `ZNN`, too. I just want to know if/what additional incentives for Pillars participating in the extension-chain are needed.

-------------------------

0x3639 | 2024-03-20 22:18:39 UTC | #31

[quote="aliencoder, post:26, topic:52"]
I finally settled for [Cronos](https://github.com/crypto-org-chain/cronos).
[/quote]

![image|690x255](upload://z37gXrPXxWCxOCkDvnqu0z8BcnM.png)

-------------------------

0x3639 | 2024-03-21 01:53:08 UTC | #32

[quote="aliencoder, post:30, topic:52"]
I just want to know if/what additional incentives for Pillars participating in the extension-chain are needed.
[/quote]

The native Cronos chain does not seem to reward validators.  Or I cannot find that in their documents. I'll keep looking.

-------------------------

aliencoder | 2024-03-21 10:20:45 UTC | #33

[quote="0x3639, post:32, topic:52"]
The native Cronos chain does not seem to reward validators
[/quote]

They have 2 chains: a Cosmos fork without EVM and Cronos, a Cosmos fork with EVM (Ethermint). They don't have inflation in Cronos. Every chain with vanilla Ethermint have the default EIP-1559 mechanism in regard to fees.

The easiest solution is to implement a bridge tax for either `ZNN` -> `xZNN`, `xZNN` -> `ZNN` or both. 

I would not tax the `ZNN` to `xZNN` because we must encourage users to swap and use the extension-chain to burn as many fees as possible.

However, I would tax `xZNN` to `ZNN` because the users porting back their coins to the mainchain will create inflation (staking, delegating, etc.).

This tax will be distributed to the set of active extension-chain Pillars.

-------------------------

0x3639 | 2024-03-21 10:27:54 UTC | #34

[quote="aliencoder, post:33, topic:52"]
I would not tax the `ZNN` to `xZNN`
[/quote]

Agree

[quote="aliencoder, post:33, topic:52"]
EIP-1559 mechanism in regard to fees.
[/quote]

### EIP 1559 Summary
EIP-1559 introduces two components to transaction fees: a base fee and a tip (or priority fee).

* **Base Fee:** This is an algorithmically determined fee that fluctuates based on network congestion. When the network exceeds a certain level of utilization, the base fee increases; when it's underutilized, the base fee decreases. This fee is burned, meaning it is removed from circulation, which can have a deflationary effect on the total supply of Ether (ETH) over time.
* **Tip (Priority Fee):** To incentivize miners (or validators, post-Ethereum's transition to Proof of Stake with the Merge) to include a transaction in the blockchain more quickly, users can add a tip. This tip goes directly to the miners/validators as a reward for processing the transaction.


#### Questions
Because usage will be low initially, validators will likely not receive Tips.  There will be no need to include them to process TX.

1) Is there any reason we cannot start with small xZNN to ZNN exit fees and later transition to Tips as the network grows?
2) Will contract deployers get compensated in any way?

-------------------------

aliencoder | 2024-03-21 11:44:47 UTC | #35

[quote="0x3639, post:34, topic:52"]
* Is there any reason we cannot start with small xZNN to ZNN exit fees and later transition to Tips as the network grows?
[/quote]

Theoretically transactions tips are part of the EIP-1559, so we have the functionality built-in right from the beginning.

[quote="0x3639, post:34, topic:52"]
1. Will contract deployers get compensated in any way?
[/quote]

Initially, no. But we can do that post-launch with a hard-fork.

-------------------------

0x3639 | 2024-03-21 11:47:24 UTC | #36

I support a small exit fee from xZNN to ZNN to incentivize validators.  Maybe we start with no fees for some period of time to build interest.

-------------------------

Chadass | 2024-03-21 13:36:45 UTC | #37

Aliencoder thinking delegating create additional inflation... This project is doomed.

-------------------------

sugoibtc | 2024-03-21 13:44:35 UTC | #38

@aliencoder 

will the transactions on the xchain also have fees? Or will the user only pay a fee when they bridge their xZNN back to ZNN

-------------------------

aliencoder | 2024-03-21 14:25:59 UTC | #39

[quote="sugoibtc, post:38, topic:52"]
will the transactions on the xchain also have fees?
[/quote]

Every transaction on the `xchain` will have a fee (negligible in the beginning/if network usage is low). The users swapping `xZNN` back to `ZNN` will pay an additional fee that will be used to incentivize the Pillars validating the `xchain`.

-------------------------

0x3639 | 2024-03-21 14:42:31 UTC | #40

[quote="Chadass, post:37, topic:52"]
delegating create additional inflation
[/quote]

the mainchain will create inflation (staking, delegating, etc.) != delegating create additional inflation

-------------------------

aliencoder | 2024-04-12 16:05:47 UTC | #42

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

aliencoder | 2024-04-01 21:23:06 UTC | #43

I've included the steps to run a seed node. It will be used to bootstrap the p2p network. All nodes will initially connect to the seed node(s).

-------------------------

build_republic | 2024-04-02 14:45:14 UTC | #44

Pretty amazing.

How do you (or the community at large really) view the pros/cons of forking/launching their own extension chains?

For example if build_republic wanted to launch an extension chain with the same specs and call it "Andromeda" to set parameters for people building in our community, is that accretive or needlessly complex?

-------------------------

aliencoder | 2024-04-02 15:52:44 UTC | #45

[quote="build_republic, post:44, topic:52"]
How do you (or the community at large really) view the pros/cons of forking/launching their own extension chains?
[/quote]

Positive. This is the idea of extension-chains: add value and enhance NoM. They should also inherit security from NoM and, by extension (in the future) from Bitcoin. You can view them as side-chains like Cosmos app-chains or Polkadot para-chains, but with a more streamlined approach regarding setup and security. This will be the next milestone in developing an ecosystem of NoM extension-chains.

[quote="build_republic, post:44, topic:52"]
For example if build_republic wanted to launch an extension chain
[/quote]

I would encourage Build Republic to launch their own custom extension-chain that fits their users' needs.

-------------------------

0x3639 | 2024-04-02 19:01:27 UTC | #46

[quote="aliencoder, post:42, topic:52"]
Open Syrius desktop wallet, import your `producer` keystore from the Pillar’s machine and sign a message
[/quote]

I wanted to be 100% sure that we need to sign the message from the `producer` address and NOT the pillar address.  if that is the case @aliencoder I need to redo mine.

-------------------------

aliencoder | 2024-04-02 19:38:32 UTC | #47

[quote="0x3639, post:46, topic:52"]
I wanted to be 100% sure that we need to sign the message from the `producer` address and NOT the pillar address
[/quote]

Yes. The reason we use the `producer` keystore is that it already acts as a "hot" wallet by participating in momentum signing for consensus operations. **DO NOT** touch the Pillar owner keystore. It must be kept in cold storage.

-------------------------

0x3639 | 2024-04-02 19:44:43 UTC | #48

OK I need to redo what I sent you.

-------------------------

coinselor | 2024-04-02 20:46:48 UTC | #49

[quote="aliencoder, post:42, topic:52"]
|Config [p2p]|Setting|
| --- | --- |
|pex|false|
|persistent_peers|list of sentry node IDs|
|private_peer_ids|none|
|unconditional_peer_ids|optionally sentry node IDs|
|addr_book_strict|false|

#### Sentry Node Configuration

|Config [p2p]|Setting|
| --- | --- |
|pex|true|
|persistent_peers|validator node, optionally other sentry nodes|
|private_peer_ids|validator node ID|
|unconditional_peer_ids|validator node ID, optionally sentry node IDs|
|addr_book_strict|false|
[/quote]

I find this step confusing. Omitting pex/addr_book_strict, no doubts there:

For the Sentry (single sentry setup):

`persistent peers = "validator-node-id@validatorip:26656"` (assumed p2p tendermint port)
`private_peer_ids = "validator-node-id"`
`unconditional_peer_ids = "validator-node-id"`


For the Validator (multiple sentry setup as an example) :

`persistent peers = "sentry1-node-id@sentry1ip:26656,sentry2-node-id@sentry2ip:26656"`
`private_peer_ids = ""`
`unconditional_peer_ids = "sentry1-node-id,sentry2-node-id"`

Does this look right?

-------------------------

0x3639 | 2024-04-02 20:55:15 UTC | #50

[quote="aliencoder, post:42, topic:52"]
`26656/tcp`
[/quote]

just wanted to confirm that port `26656/tcp` is the only port needed for peering and basic node functions.

-------------------------

0x3639 | 2024-04-03 00:46:43 UTC | #51

[quote="aliencoder, post:42, topic:52"]
```
supernovad init seed --chain-id supernova_74506-1
```
[/quote]

I setup a seed node with no issues.  I wanted to confirm these instructions do not mention starting the binary.  I assume that will come later?

-------------------------

aliencoder | 2024-04-03 09:40:10 UTC | #52

[quote="coinselor, post:49, topic:52"]
Does this look right?
[/quote]

Yes.

[quote="0x3639, post:51, topic:52"]
I wanted to confirm these instructions do not mention starting the binary. I assume that will come later?
[/quote]

I've included a `systemd service` setup in the tutorial as a final step, check it out!

-------------------------

aliencoder | 2024-04-04 09:06:03 UTC | #55

I've updated the post. The service must be started after everyone that wants to participate has the `genesis.json` file properly loaded. 

I'm still gathering `gentxs` from Pillars. I'll wait until Friday night for new entries.

Thank you everyone for your participation and commitment so far! :alien:

-------------------------

0x3639 | 2024-04-05 10:55:03 UTC | #56

My plan is to start without the sentry first.  That is just one more thing to troubleshoot if something is wrong.  Once the testnet is up and running,  I will add the sentry, but only after I know the network is up and my validator is working as expected.

-------------------------

build_republic | 2024-04-05 15:23:07 UTC | #57

Is there anyone in the community who might be able to spin up professional docs (def. A-Z worthy) for launching an extension chain?

Most EVM L2s are Optimism-based, likely in no small part to their docs:  https://docs.optimism.io/stack/getting-started

-------------------------

aliencoder | 2024-04-05 21:19:34 UTC | #58

❗❗❗ Please make sure you're running the latest `supernovad` binary ❗❗❗ 

```bash
cd /root/supernova
git pull
make build
```

Kudos to @0x3639 @tapwoot for the seed nodes. Please add them in the `config.toml` (Step 14).

-------------------------

aliencoder | 2024-04-06 19:16:14 UTC | #59

Some participants provided either malformed or invalid signatures.

Malformed signatures: @mehowz
Invalid signatures: @0x3639 @nbd

Update: @SultanOfStaking is ready now :white_check_mark:

-------------------------

coinselor | 2024-04-06 18:02:16 UTC | #60

A+ tryhard alien :saluting_face: .

Can we currently vote on AZ with producer keystore? This would make sense to keep the Pillar key in cold storage. 

![image|689x104](upload://6d6SqKBMKQzng8JsRMAcptuWA1U.png)

My producer keystore has indeed the pub key exposed, but it just has a random "unknown" transaction from a random day. I had never imported it/used it on syrius until I signed the gentx. How can this be?

-------------------------

aliencoder | 2024-04-12 16:22:53 UTC | #61

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

0x3639 | 2024-04-06 21:21:18 UTC | #62

I see @coinselor was added to the seed list.  Do we need to update the `config.toml` to add his IP?

-------------------------

aliencoder | 2024-04-06 21:25:42 UTC | #63

[quote="0x3639, post:62, topic:52"]
Do we need to update the `config.toml` to add his IP?
[/quote]

I recommend updating the `config.toml` with all 3 seeder nodes.

-------------------------

tapwoot | 2024-04-06 22:41:15 UTC | #64

what is the final updated seed list for everyone including @coinselor ?

/selfreply ->nvm you've updated the original post for everyone ty sir

-------------------------

0x3639 | 2024-04-07 02:44:14 UTC | #65

[quote="tapwoot, post:64, topic:52"]
what is the final updated seed list for everyone including @coinselor ?
[/quote]

```
seeds = "11a552f46f9f9cca4167dcabfa011acd3e6b4704@149.28.128.53:26656,cffa8675227fc3f028a527678ac491309715f632@208.115.200.17:26656,1adcbd9a8a53d93505fb50e88660feb45d5089e4@5.196.22.239:26656"
```

-------------------------

edgepillar | 2024-04-07 07:24:09 UTC | #66

I also updated the seeds line.

-------------------------

aliencoder | 2024-04-07 12:46:52 UTC | #67

Unfortunately, I've discovered a small mistake in the `gentx` command (the `chain-id`) and you'll need to redo the genesis transaction for your extension-chain Pillar.

```bash
rm -rf /root/.supernova/config/gentx/gentx-*
supernovad gentx pillar_moniker 1000000000000000000000stake --chain-id supernova_74506-1 --moniker="pillar_moniker" --min-self-delegation="1000000" --details *insert signature*  --ip="127.0.0.1"
```

Please note that I've added the `--ip` parameter where I've specified the localhost instead of the public IP. We can't remove the `memo` field after it's signed because we invalidate the signature by doing so.

-------------------------

aliencoder | 2024-04-07 18:39:44 UTC | #68

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

aliencoder | 2024-04-12 16:22:35 UTC | #69

Please add @mehowbrainz's seed node to the `seeds` entry in the `config.toml`:

```
seeds = "b91ab16e7454eeaabcb0d4c5d2f900a08ed518aa@5.196.22.239:26656,7efe3e47afbbf38c44179d3802aee4cad7af47eb@208.115.200.55:26656,7cd3cb605a8da6a7be20736c171ee33d307d6f88@3.94.70.251:26656"
```

-------------------------

aliencoder | 2024-04-24 21:33:22 UTC | #70

I will prepare the mainnet rollout for Supernova ZVM. We still need to accomplish 2 things in the meanwhile:

1. A fully functional explorer: @mehowz's dev is helping us with devops and @0x3639 can host the archive node for it
2. A fully functional bridge interface to seamlessly swap `ZNN` and `xZNN`. Here @dexter can help us or anyone that has experience with frontend development.

-------------------------

0x3639 | 2024-04-24 21:36:45 UTC | #71

[quote="aliencoder, post:70, topic:52"]
A fully functional explorer: @mehowz’s dev is helping us with devops and @0x3639 can host the archive node for it
[/quote]

Sounds like mehowz will not be able to setup the infra.  I will plan to host it.  

@aliencoder do we have a faucet for the testnet?  Someone was asking in TG today.

-------------------------

aliencoder | 2024-04-25 08:59:23 UTC | #72

[quote="0x3639, post:71, topic:52"]
@aliencoder do we have a faucet for the testnet? Someone was asking in TG today.
[/quote]

We can setup a faucet if someone is interested to host it.

-------------------------

0x3639 | 2024-04-25 09:31:41 UTC | #73

yes I'm happy to do that if no one else wants to.

-------------------------

SultanOfStaking | 2024-04-30 00:10:34 UTC | #74

Are we set on 1 & 2 or are these still open?

-------------------------

aliencoder | 2024-04-30 08:27:32 UTC | #75

[quote="aliencoder, post:70, topic:52"]
* A fully functional explorer: @mehowz’s dev is helping us with devops and @0x3639 can host the archive node for it
[/quote]

@0x3639 is on it. Hopefully we'll have a fully functional explorer.

[quote="aliencoder, post:70, topic:52"]
1. A fully functional bridge interface to seamlessly swap `ZNN` and `xZNN`. Here @dexter can help us or anyone that has experience with frontend development.
[/quote]

Here is a little bit more tricky. We should also start integrating EVM support into Syrius @CryptoFish (for `xZNN`).

-------------------------

aliencoder | 2024-06-09 20:14:00 UTC | #76

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

0x3639 | 2024-06-10 00:27:40 UTC | #77

Guys

Before everyone tries this we should work through the issue I'm having w/ the upgrade.  I would hate for everyone to try to upgrade, fail, and halt the chain.  Maybe one person should try and see if you get this error too.  

```
Jun 10 00:22:52 sn-archive1 kernel: [84986.200862] traps: supernovad[18282] trap invalid opcode ip:4ced660 sp:7fffafde9b18 error:0 in supernovad[1c2f000+34d3000]
Jun 10 00:22:52 sn-archive1 systemd[1]: supernova.service: Main process exited, code=dumped, status=4/ILL
Jun 10 00:22:52 sn-archive1 systemd[1]: supernova.service: Failed with result 'core-dump'.
Jun 10 00:22:52 sn-archive1 systemd[1]: supernova.service: Scheduled restart job, restart counter is at 5.
Jun 10 00:22:52 sn-archive1 systemd[1]: Stopped supernova service.
Jun 10 00:22:52 sn-archive1 systemd[1]: supernova.service: Start request repeated too quickly.
Jun 10 00:22:52 sn-archive1 systemd[1]: supernova.service: Failed with result 'core-dump'.
Jun 10 00:22:52 sn-archive1 systemd[1]: Failed to start supernova service.
```

-------------------------

