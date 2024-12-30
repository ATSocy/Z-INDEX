Thread: zenon-network-roadmap
0x3639 | 2024-11-09 20:07:09 UTC | #1

## DRAFT Zenon Network Roadmap

|Type | Description | Developer(s) | Status | ETA|
|--- | --- | --- | --- | ---|
|Core | Dynamic Plasma - Spec & Implementation | @vilkris | In Development | Q1 '25|
|Core | Dynamic Plasma - Mainnet | @vilkris | In Planning | Q2 '25|
|Core | LevelDB Analysis / IBD Download Speed | @vilkris | Under Consideration | '25|
|Core | PTLC | @georgezgeorgez | In Testing & Review | '25|
|Core | BTC Merge Mining | @MoonBaze | In Development | '25|
|Core | Hyperqube (L2) | @georgezgeorgez | In Planning & Development | Q1 '25|
|Core | libp2p | TBD | Not Started | '26|
|Core | Sentry | TBD | Not Started | '25|
|Core | Sentinels | TBD | Not Started | '25 / '26|
|Core | Narwhal & Tusk | TBD | Not Started | '26|
|Core | zApp Runtime & UnikernelZ | The Prof | In Development | '25|
|Core | ZeroSync - https://zerosync.org/ | 3rd Party | In Development | Unknown|
|Core | BTC Interop | TBD | Unknown | Unknown|
|Interoperability | syrius v0.2.0 | @cryptofish | Released | Q2 '24|
|Interoperability | syrius v0.3.0 | John Maxwell | In Development | Q1 '25|
|Interoperability | Orchestrator | @sumamu | Done | Q1 '24|
|Interoperability | Orchestrator Refactoring | @sumamu | In Development | Q2 '25|
|Interoperability | Bridge GUI | @dexter | Done | Q2 '24|
|Interoperability | Bridge GUI Refactoring | @mehowz @dexter | In Planning | '25|
|Interoperability | Supernova Extension Chain | @aliencoder | In Development | Q1 '25|
|Interoperability | Ledger Support | @CryptoFish | Under Review by Ledger | '25|
|Interoperability | PLTC SDK / CLI Support | @CryptoFish | In Development | '25|
|Interoperability | Syrius Mobile Wallet | @DrBlaze | In Testing | Q4 '24|
|Interoperability | Gravity Wallet | @Nostromo | Unknown | TBD|
|Interoperability | TG Mini App | @dexter | In Development | Q4 '24|
| |  |  |  | |

*Note: All ETAs are the Author's estimate with no input from the developers.*

## Background
![Screenshot 2023-05-22 at 6.32.03 AM|690x345](upload://xBW8CCpaYka4IS97vnF6TytHpyw.png)

## Core Upgrades
---
### Dynamic Plasma
- [Plasma design concept](https://forum.hypercore.one/t/ideas-for-dynamic-plasma/233/1)
- [Formulas](https://github.com/vilkris4/dynamic-plasma-ideas/blob/main/dynamic_plasma_formulas.md)
- [Pseudo code](https://github.com/vilkris4/dynamic-plasma-ideas)
- "Benchmarking and the new dynamic plasma components aren't really a bottle neck. There are other performance issues in the node software that I've come across and I was sidetracked by those for a bit. But those issues don't have to be in the scope of dynamic plasma"
- "Ideally I want there to be some kind of consensus amongst us [developers] for dynamic plasma. I'd like other devs to also have a deep understanding of how dynamic plasma works so that's its not just all on me"

### PLTC
- A PTLC, or Point Time-Locked Contract, is an advanced cryptographic protocol used in the blockchain and cryptocurrency space, building upon the concept of Hash Time-Locked Contracts (HTLCs). Unlike HTLCs, which rely on the revelation of a preimage of a hash to unlock a transaction, PTLCs use a different mechanism based on points on an elliptic curve, offering several advantages.
- [Code](https://github.com/zenon-network/go-zenon/pull/13) is submitted and ready for review.  @MoonBaze and @sumamu are likely reviewers.
- [Supporting information](https://forum.hypercore.one/t/ptlcs-the-standard/200) for PTLCs

### BTC Merge Mining
#### Status
- Following the post of Alien Coder about merge mining, I [@MoonBaze] started to think about it and I have found a way to implement it on our network by having 3 components:
-- An embedded that validates the partial shares
-- The miners that use the Stratum protocol
-- a proxy that connects the 2, is also connected to a bitcoin node and handles jobs and posting the blocks and proofs
- I have also started to implement the proxy so far with the specification of Stratum v2, but it's in incipial phase.
- https://stratumprotocol.org/

#### Properties

By integrating the first decentralized, peer-to-peer (merge)-mining pool for Bitcoin & RandomX and several other algorithms, we aim to enhance the following properties that are at the core of our shared ethos:

##### **Censorship-resistance**

There is no centralized server to steal hashrate, impose a certain block template for example mining empty blocks in Bitcoin or even worse blacklisting certain transactions. We already see that centralized mining pools in certain jurisdictions can be targeted and forced to comply.

##### **Decentralization**

By communicating exclusively through the peer-to-peer network, miners coordinate by working on a share-chain. If properly implemented, it can be as efficient as a centralized pool.

There is no pool admin: attacks by rogue pool operators on Bitcoin are no longer possible.

Moreover, miners with older ASICs can turn them on even if they have a lower hashrate and contribute on a lower difficulty share-chain and still be profitable.

##### **Merge-mining BTC & ZNN**

By directing hashpower to NoM, miners will earn ZNN rewards from Pillars. We need to divert ZNN away from delegators in order to be able to properly incentivize miners and lay out the foundation for Phase 1.

Bitcoins will be generated. TSS will be leveraged for a decentralized custody of the freshly mined BTC. ZNN will be backed by physical BTC. This positive feedback loop aims to encourages participation and further decentralizes the distribution of the hashpower.

Sources:
- [Discord Dev Meeting 9 Feb 24](https://discord.com/channels/920058192560533504/1150019456718876843/1205496346560438282)
- [Network of Momentum Phase I Post](https://forum.hypercore.one/t/network-of-momentum-phase-1/253)


### Unknown Improvements
@georgezgeorgez is working on unknown protocol upgrades.  The scope of work and timing are unknown.  

### libp2p
`libp2p` is a modular network stack that enables the development of peer-to-peer (P2P) applications. It is designed to provide a set of protocols and components for developers to build decentralized, secure, and scalable applications. `libp2p` is part of the broader IPFS (InterPlanetary File System) ecosystem, but it can be used independently for a wide range of P2P applications beyond just file sharing.

Mr. Kaine thinks NoM should implement this network stack and it should be part of Phase I.  

### Sentry
- Trusted node that syncs rapidly with zk-proof
- [Helios](https://github.com/a16z/helios): A fast, secure, and portable light client for Ethereum
- [Zerosync](https://zerosync.org/demo/) BTC Initial Block Download (IBD) example

Source (Whitepaper): 
![image|690x188](upload://kMjiS48r1F7CfGNcfNXynAkUqXt.png)


### Sentinels
- Sentinels are full nodes that contribute to network security by relaying messages with [PoW links](https://ask.zenon.wiki/questions/D1T2/what-is-a-proof-of-work-link/E1X2).  
- Recent research [A Simple Proof of Sybil-proof](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) prove the existence of a mechanism that achieves sybil-proofness in a three-hop path.  

![Screenshot 2024-02-13 at 7.56.28 AM|690x165](upload://dTf12rI4y9tIrkgyDZaPq3SgLKP.png)


### Narwhal & Tusk
- Narwhal and Tusk introduce a new approach to improve the performance of Byzantine fault-tolerant quorum-based consensus. The authors propose separating the tasks of reliable transaction dissemination from transaction ordering.
- https://www.zenon.info/narwhal-and-tusk-on-zenon-network/

## Interoperability Solutions
---
### syrius
- Deploy https://forum.hypercore.one/t/syrius-0-2-0/328
![image|528x500](upload://z7wJtyTCqgcagd4S8HTdQYpe7uV.png)

### Orchestrator
- Stability improvements (in development)
- Upgrade bridge embedded to accommodate the extension chain

### Bridge
- Add USDT & USDC

### Extension Chain
Status notes
- Add current Pillars to exchain genesis
- Issue `maxSupply` xZNN ( and add it to `bridge` contract
- Comment out `MsgWithdraw` , `MsgDeposit` from the `x/staking` module
- Comment out blacklisting code
- Add custom logic for the `Feesplit` in `evm_hooks.go`
- We will use the `bridge` embedded to hook it up with NoM

### Ledger Support
- Ledger is under extensive development.  
- Check out the [project status page](https://forum.hypercore.one/t/project-zenon-ledger-app/112/11)
- [Zenon Network Embedded App Source Code](https://github.com/hypercore-one/ledger-app-zenon/tree/develop)
- [Zenon Ledger Demo](https://www.canva.com/design/DAFnxztm-9k/GoerdZMUjGc-LMczL6CYYg/watch?utm_content=DAFnxztm-9k&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink)
- [Zenon Ledger Command Line Demo](https://www.canva.com/design/DAFuKR2DClg/SfXEb2TmoKbrq16M36bmnQ/watch?utm_content=DAFuKR2DClg&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink)
- Testing Ledger - [How to Sideload the Embedded App](https://forum.hypercore.one/t/how-to-sideload-the-zenon-ledger-embedded-app-for-ledger-nano-s-s/247)
- Track progress of the [Ledger Code Review](https://airtable.com/appIHCUneslDfKjXu/shrqrpH9y9VRorS4J/tblw7wsOQj5Fb2UzA)

![image|690x320](upload://erZpw5hNBDIhYAeKusQdm342QOe.jpeg)


### Syrius Mobile Wallet
- Mobile wallet in [testing](https://forum.zenon.org/t/syrius-wallet-mobile-app/659/157?u=0x3639) and development
- Mobile wallet [security](https://forum.zenon.org/t/hardware-mobile-wallet/1755) considerations
- [Key sharding](https://forum.hypercore.one/t/frosted-the-first-step-towards-a-seedless-future/326) under development
- Possible [Yubikey integration](https://forum.hypercore.one/t/yubikey-encrypt-cli-tool/327) 

### Gravity Wallet
- [Project status](https://forum.hypercore.one/t/gravity-wallet/270)

## Roadmap Graphics
![image|690x388](upload://4qYfHhz2iDRLpRdapxNPrnmy45K.jpeg)


## Roadmap Notes:
- To keep this post clean, replies are auto-deleted after 7 days.

-------------------------

