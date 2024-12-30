Thread: zip-sumamu-0001-draft
sumamu | 2024-03-27 15:20:03 UTC | #1

|Field|Description|
| --- | --- |
|zip|ZIP:sumamu-0002|
|title|NoM Multichain infrastructure|
|author|@sumamu @sumoshi 
|status|Draft|
|type|Hard fork|
|acceptance| upon usage by the community|
|activation| upon usage by the community|
|created|2023-03-07|
|license|GPL v3.0|
|link|https://forum2.zenon.org/t/zip-sumamu-0002-final/1327 |

**I. Abstract**

A blockchain interoperability solution is paramount for every blockchain network that wants to develop a sustainable, thriving ecosystem. Users are able to frictionlessly swap assets between different blockchain networks through a seamless procedure enabled by user-friendly interfaces.

This integration with the wider blockchain ecosystem will simultaneously attract more users (builders, developers, marketers, liquidity providers, etc.) and will also unlock a core component of the Network of Momentum: the Protocol Level Liquidity.

**II. Motivation**

*Decentralized cross-chain bridges*

One of the most important elements of a decentralized network is represented by its interoperability with the wider ecosystem. The unconfined flow of assets between NoM and other blockchain networks will unlock a new network participant in NoM as first-class citizen - the LP provider and boost the ecosystem in terms of user base, network activity, use-cases, etc.

Furthermore, in order to achieve protocol level liquidity and successfully kickstart the Orbital Program, a bidirectional mechanism to allow the flow of assets between NoM and other blockchain networks is required.

*Why do we need a decentralized cross-chain bridge?*

Current centralized exchanges (CEX) are single point of failures by either going rogue (e.g. FTX saga), shutting down due to regulatory pressures, or simply hacked and user funds drained (e.g. QuadrigaCX). Moreover, centralized exchanges have several other limitations and weaknesses:

* KYC mishandling and user account censorship
* cumbersome listing procedures or requirements
* prohibitive listing fees
* manipulative behavior (e.g. wash trading)
* delistings due to regulatory pressure
* opaque order book

Decentralized exchanges (DEX) and liquidity pool-based DEX AMMs (e.g. Synapse, Multichain, cBridge, Uniswap, Pancakeswap, etc.) are better suited for trustlessly swapping assets within or between blockchain ecosystems: a frictionless, user-centric approach that benefits every participant.

In order to fulfill the vision of a decentralized ecosystem, a robust multi-chain interoperability solution is crucial to be deployed and maintained at protocol level with a layered security approach.

Protocol Level Liquidity

*What is Protocol Level Liquidity?*

Protocol Level Liquidity is a way to incentivize liquidity providers by allocating and distributing funds for them directly from the network emission in a trustlessly and automated manner. NoM has a dual-coin inflation in ZNN (Zenon) and QSR (Quasar). A fraction of this dual-coin emission is reserved for the liquidity embedded, a system smart contract that is currently tasked to safely store it for the upcoming Orbital Program.

*What is the Orbital Program?*

Orbital Program is a protocol level liquidity program that incentivizes liquidity providers to participate and pool together liquidity for the wrapped representations of ZNN, QSR and ZTS tokens in exchange for the aforementioned fraction of the dual-coin emission. This program will create a sustainable model for external liquidity providers to participate into the network.

*Why is this necessary?*

Without proper incentive mechanisms, LPs will not be interested to join the Orbital Program and this in turn will hurt the ecosystem by limiting the potential of external users that would swap their assets to NoM. Moreover, beyond Orbital Program, new untapped markets and gateways to access NoM are necessary for a healthy development of the ecosystem.

**III. Specification**

There are several distinct components that will enable a multi-chain vision with Orbital Program at its core:

1. The embedded contracts (bridge and liquidity)
2. The orchestrator layer
3. The EVM smart contracts

The possibility to exchange and swap assets in a trustless, decentralized way between NoM and other networks is conditioned by the existence of a decentralized bridge solution.

The liquidity embedded in its current form does not have the means to distribute rewards to liquidity providers in a trustless and automated way.

A robust interoperability solution must also maximize the compatibility with other blockchain networks:

A. Compatibility with account based networks

A.1. Compatibility with account based EVM networks (Ethereum, BNB Smart Chain, etc.)

The initial phase will consist of an implementation specifically designed for EVM compatibility:

* Execution compatibility: Ethereum virtual machine (i.e. Solidity)
* Cryptographic compatibility: ECDSA signatures (i.e. secp256k1)
* API compatibility: ETH JSON-RPC (i.e. Ethereum JSON-RPC API)

This interoperability solution will unlock liquidity from a wide range of both Layer-1 and Layer-2 EVM compatible networks such as Ethereum, BNB Smart Chain, Polygon, Avalanche, Arbitrum, etc.

Liquidity pools will be gradually deployed on those networks for the wrapped representations of ZTS assets, enabling a seamless process for users to access and get onboarded into the NoM ecosystem.

A.2. Compatibility with account based non-EVM networks (Polkadot, Cosmos, etc.)

In the future, more non-EVM networks can be connected by implementing custom integrations:

* Execution compatibility: Virtual machine type (i.e. WASM)
* Cryptographic compatibility: EdDSA signatures (i.e. Ed25519)
* API compatibility: custom API for each network

B. Compatibility with UTXO networks (Bitcoin, Litecoin, etc.)

In the next phase, compatibility with UTXO networks, in particular Bitcoin, is expected to be implemented and rolled-out. Further design changes are necessary for optimal integration with existent BIP340, BIP341 (e.g. Schnorr signatures - Musig2, MAST, Tapscript, etc.).

**IV. Rationale**

*Security focused design*

The whole design architecture of the decentralized cross-chain bridge is focused around security considerations.

Not a single centralized entity except the end user is able to move funds and several security mechanisms are organized in a layered structure to prevent and deter malicious actors from exploiting the infrastructure. The TSS participants are only able to sign transactions; they do not have the possibility to move user funds.

*Time-challenge as a security primitive*

Every sensitive action is split into two separate stages and is safeguarded by a time-challenge security primitive. This primitive is used throughout the codebase for every sensitive action that either involves moving funds or other critical actions.

*Wrap and Unwrap*

* ZTS = native Zenon Token Standard asset on NoM e.g. ZNN
* wZTS = wrapped Zenon Token Standard asset on a particular destination network e.g. wZNN
* ERC-20 = native Ethereum token on Ethereum mainnet e.g. DAI
* zERC-20 = wrapped Zenon Token Standard asset on NoM e.g. zDAI

Source NoM -> Destination Ethereum

* ZNN (ZTS on NoM) -> wrap -> wZNN (ERC-20 on Ethereum)
* zDAI (ZTS on NoM) -> unwrap -> DAI (ERC-20 on Ethereum)

Source Ethereum -> Destination NoM

* wZNN (ERC-20 on Ethereum) -> unwrap -> ZNN (ZTS on NoM)
* DAI (ERC-20 on Ethereum) -> wrap -> zDAI (ZTS on NoM)

Additionally, the two step procedure is enforced to either wrap or unwrap assets:

* Stage 1 *Request Action*: this signals the intention of a user to wrap or unwrap his assets.
* Stage 2 *Redeem Action*: this action settles the user's request and actually delivers the swapped assets to its corresponding address.

*Code coverage*

The codebase has extensive unit-testing to cover common and exotic edge-cases that might appear in different scenarios.

*What actors will participate in the NoM multi-chain infrastructure?*

1. Guardians
They will be elected from prominent members of the community. They will act as judges in case of a major failure of the infrastructure. They are responsible to safeguard the infrastructure in case of an emergency.

2. Admin
The role of the admin is to manage the infrastructure. It cannot move funds and its permissions are limited in scope. The embedded contracts are designed to be managed by the community members through a governance module, similar to Accelerator-Z. At the moment the governance capabilities of NoM are insufficient to ensure this functionality. Until a solution is developed, the admin will be managed by code maintainers.

3. Pillars as TSS participants
All the nodes of the orchestrator will run on Pillar nodes. This design decision is based on the consideration that the security of the whole network depends on consensus running nodes. They already have the technical background and know-how to operate nodes and a sufficient stake in the network to responsibly manage this critical piece of infrastructure. Pillars will be able to be part of the orchestrator peer-to-peer layer (libp2p) and participate in the threshold signature (TSS) ceremonies.

4. Liquidity Provides
Liquidity Provides (LPs) are users with disposable capital that are incentivized through the Orbital Program to directly participate into the network by staking their liquidity in order to receive dual-coin (ZNN and QSR) rewards. They must ensure adequate levels of liquidity for users to be able to frictionlessly swap their assets in and out of the ecosystem.

*What motivated the design?*

This particular interoperability solution allows easy transfers from NoM to other networks. The embedded bridge contract allows the control of native ZTS assets on NoM, while EVM Solidity contracts allow the control of wrapped ZTS assets on EVM compatible chains.

*Decentralized cross-chain bridge: end-to-end flow*

The bridge is based on lock-and-release/mint-and-burn mechanisms: native assets are locked/burned on one side and released/minted on the other side. Depending on the nature of the swap, the following scenarios may appear:

* Example native ZNN/wZNN (native ZNN and wZNN as ERC-20 token):
Native ZNN is locked in the bridge embedded contract on NoM and its wrapped representation, wZNN is minted by the Ethereum contract. For the opposite direction, wZNN is burned by the ETH smart contract and native ZNN is released by the embedded bridge.

* Example stablecoin DAI/zDAI (DAI as ERC-20 token and zDAI as ZTS token):
DAI stablecoin is locked in the Ethereum smart contract, while the embedded contract mints the equivalent amount on NoM. For the opposite direction, zDAI is burned by the embedded contract and ETH token DAI released by the ETH smart contract.

*Orbital Program: end-to-end flow*

The Orbital liquidity embedded contract is based on the staking embedded contract.

A liquidity provider that wants to participate in the Orbital Program must supply a liquidity pool with the corresponding assets, swap the resulting LP token to NoM and lock it up into the liquidity embedded to earn dual-coin rewards.

For example, an Ethereum user wants to become a liquidity provider (LP) and deposit ETH and wZNN into a pool in order to participate into the Orbital Program. Depending on how much liquidity they provide for the wZNN/ETH pool on Uniswap, they will receive a proportional amount of ERC-20 LP tokens. In the next step, the LP must swap the ERC-20 LP tokens to the ZTS zLP tokens on NoM using the decentralized cross-chain bridge. In order to become eligible for receiving dual-coin rewards from NoM's emission, the LP must deposit the zLP tokens into the liquidity embedded contract. The liquidity embedded contract mirrors the staking embedded contract in terms of locking the tokens for a predefined time period. However, it differs from a rewards' perspective: participating LPs get both ZNN and QSR.

**V. Implementation**

The implementation is fully open-source on Github with a permissive licensing model - GNU General Public License v3.0 to allow builders to develop a healthy middleware ecosystem for the Network of Momentum. The codebase in written in Go v1.20 and the EVM smart contracts are written in Solidity v0.8.17

The core components of the infrastructure - *go-tss*, *tss-lib* modules are properly audited are are used in production by high ranking cryptocurrencies (e.g. Thorchain).

Audits:

Thorchain go-tss: [https://github.com/thorchain/Resources/tree/master/Audits
](https://github.com/thorchain/Resources/tree/master/Audits%EF%BF%BCtss-lib)Binance tss-lib: https://github.com/bnb-chain/tss-lib/releases/download/v1.0.0/audit-binance-tss-lib-final-20191018.pdf

Security considerations:

IPFS libp2p: https://docs.libp2p.io/concepts/security/security-considerations/

[Codebase structure](https://github.com/HyperCore-Team):

1. go-zenon
1.1 Embedded bridge contract
1.2. Embedded liquidity contract

2. EVM smart contracts

3. Orchestrator layer
3.1 go-tss
3.2 tss-lib

4. Testing environment: https://github.com/HyperCore-Team/dockerized-testnet

**VI. License**

GNU General Public License v3.0

**VII. ZIP Comments**

**VIII. ZIP References**

[Orbital Program](https://medium.com/@zenon.network/orbital-program-protocol-level-liquidity-2f9567830105)
[Hyperspace interoperability: cross-chain bridge](https://medium.com/@zenon.network/hyperspace-x-accelerator-z-towards-a-dao-of-daos-38dfad496365)

**IX. ZIP License**

This ZIP is licensed under GNU General Public License v3.0

-------------------------

0x3639 | 2023-03-08 14:15:31 UTC | #2

@sumamu 

- Will the orchestrator require upgraded Pillar infrastructure requirements?  
- How are the TSS participants selected?
- How many participants are there for the signing event?  
- What actions require signature?

-------------------------

0x3639 | 2023-03-08 14:43:26 UTC | #3

Would you be willing to describe the technical work flow of how the bridge works?

-------------------------

sol | 2023-03-08 23:10:36 UTC | #4

Hi Sumamu,
Thank you for developing a bridging solution for the community. I know your team has put a lot of effort into this.

[quote="0x3639, post:3, topic:1327"]
describe the technical work flow of how the bridge works?
[/quote]

Since you're producing code that updates the protocol, we need a clear definition of the changes involved. This ZIP is lacking details with respect to what protocol code is being updated and why. 

I see many changes to the liquidity contract, a new bridge contract, EVM contracts, new RPC endpoints, a fee structure, new user addresses, etc. 

Please provide information about 
- how to use/maintain this code
- security model and any (internal or external) audit results
- if possible, any lessons you may have learned along the way
- alternate solution considerations and why you made certain decisions
- documentation

My biggest fear is a bridge hack. Can you convince us that you have implemented the right security measures to avoid/minimize that possibility?

-------------------------

TrevorLeahy3 | 2023-03-08 23:17:44 UTC | #5

Hello sir, thanks for your efforts on this.

Im just going to say ive concerns around assumptions that are being made around the bridge participants such as TSS nodes and maintainers/admin. Is there an expectation that current community members are going to step in for this from day 1? 

What about incentives for pillars? In the AMA you mentioned the sentinel rewards is that still on the table? I know Orbital is part of the plan but that will not go beyond LP is that correct?

Any info or plans for this side of things would be appreciated.

-------------------------

0x3639 | 2023-03-09 02:40:54 UTC | #6

@sumamu 

Over the past 12 months Kaine has pushed all development to community developers.  It's unclear what we can expect Mr. Kaine to do going forward.  Does he expect the community to signal support of PRs and he will simply approve them. Or will Kaine be reviewing code himself? Absent any clear direction, we need to assume that Kaine will not review the code thoroughly, and it's on the community to review and approve code.  

In addition, until now Pillar operators assumed Kaine was delivering code that was audited and tested. Pillars accepted the code and upgraded without audit.  Going forward, we cannot assume that.  If we are going to change the code run by Pillars we need the buy in from the most experienced and involved Pillar operators.  Other Pillars will look to more involved / experienced operators to signal support.  Kaine's approval is not enough for deeZNNutz.com to run code he approves.  I will run code that our community developers audit and approve.  

In addition, sounds like there were some design decisions that could impact hardware requirements and Orbital Distributions.  We need to discuss those changes with Pillars and the community before accepting them. These are not decisions Kaine should approve independently.  The community needs to understand them and Pillars need to support them.    

One Pillar operator noted this code below has a rather large contract interface: https://github.com/HyperCore-Team/go-zenon/blob/embedded-bridge/vm/embedded/embedded.go#L40

He would like an explanation of each method and justification.

We would like to understand the the voting system for "guardians".  How will they be chosen?  What will they be expected to do?

How will the bridge be maintained long term?

We really appreciate all your hard work.  Let's engage with the community and get buy in from those involved.

-------------------------

sumamu | 2023-03-09 10:36:30 UTC | #7

[quote="0x3639, post:2, topic:1327"]
* Will the orchestrator require upgraded Pillar infrastructure requirements?
[/quote]
No. The Pillars will only have to run the `orchestrator`. Indeed, the `orchestrator` will require a connection to an Ethereum node (and other networks in the future), but it's up to the Pillar if that node is local or remote (e.g. Quicknode). The `orchestrator` node can run on a separate VPS with connections to both a Zenon node `znnd` and an Ethereum node.

[quote="0x3639, post:2, topic:1327"]
* How are the TSS participants selected?
[/quote]
The TSS participants would need to satisfy the following conditions when the TSS key generation (`keygen`) ceremony starts:
  * Be an active Pillar i.e. produced at least 1 momentum in the past 24 hours
  * Run the `orchestrator`
  * `orchestrator` is correctly configured

[quote="0x3639, post:2, topic:1327"]
* How many participants are there for the signing event?
[/quote]
The signing ceremony requires at least `k out of n` signers, where `n` is the number of participants in the `keygen` ceremony and `k` is the minimum number of participants (`66% of n`).

[quote="0x3639, post:2, topic:1327"]
* What actions require signature?
[/quote]
Any confirmed event that transfers assets requires a TSS signature.

[quote="0x3639, post:3, topic:1327, full:true"]
Would you be willing to describe the technical work flow of how the bridge works?
[/quote]
Yes, the documentation is work in progress.

[quote="sol, post:4, topic:1327"]
My biggest fear is a bridge hack. Can you convince us that you have implemented the right security measures to avoid/minimize that possibility?
[/quote]
This exact concern has led us to create the `time-challenge` cryptographic security primitive. Moreover, the codebase has extensive code coverage: unit-tests for all the added methods. More information will be present in the docs.

[quote="TrevorLeahy3, post:5, topic:1327"]
Is there an expectation that current community members are going to step in for this from day 1?
[/quote]
No, there isn't. The bridge will only become active once the minimum participation threshold is reached.

[quote="TrevorLeahy3, post:5, topic:1327"]
What about incentives for pillars? In the AMA you mentioned the sentinel rewards is that still on the table? I know Orbital is part of the plan but that will not go beyond LP is that correct?
[/quote]
At the moment there is no additional inflation for incentivizing bridge participants. Pillars can voluntarily decide if they run an `orchestrator` node or not, if they believe it will benefit the ecosystem.

[quote="0x3639, post:6, topic:1327"]
We would like to understand the voting system for “guardians”. How will they be chosen? What will they be expected to do?
[/quote]
The guardians operate on a majority voting system `>50%`. They are able to cast votes only in the extreme case when the bridge is in an emergency state. Their only purpose is to elect a new `admin`.

[quote="0x3639, post:6, topic:1327"]
In addition, until now Pillar operators assumed Kaine was delivering code that was audited and tested. Pillars accepted the code and upgraded without audit. Going forward, we cannot assume that. If we are going to change the code run by Pillars we need the buy in from the most experienced and involved Pillar operators. Other Pillars will look to more involved / experienced operators to signal support. Kaine’s approval is not enough for [deeZNNutz.com](http://deeZNNutz.com) to run code he approves. I will run code that our community developers audit and approve.
[/quote]
The components used for building this bridge are already audited. Moreover, any piece of code that we wrote is thoroughly covered by unit-tests. We have internally reviewed and audited the code on multiple occasions and anyone is welcomed to do the same since the entire codebase is public.

[quote="0x3639, post:6, topic:1327"]
How will the bridge be maintained long term?
[/quote]
The codebase is designed to require minimal maintenance. Any additional maintenance can be done either by us or the community and funded by Accelerator-Z.

@0x3639 can you help me modify the ZIP number? I want to change it from `ZIP:sumamu-0002` to `ZIP:sumamu-0003` since version `ZIP-0002` is reserved for [HTLCs](https://github.com/georgezgeorgez/ZIP.deeZNNutz)

-------------------------

MoonBaZe | 2023-03-09 10:43:22 UTC | #8

I am both a dev and a pillar operator and I will definitely review the code before running it.

-------------------------

MoonBaZe | 2023-03-09 10:46:01 UTC | #9

@sumamu 

When do you expect to finish the documentation so we can have a look and understand what you have been working on?

-------------------------

CryptoFish | 2023-03-09 11:18:34 UTC | #10

[quote="sumamu, post:7, topic:1327"]
@0x3639 can you help me modify the ZIP number? I want to change it from `ZIP:sumamu-0002` to `ZIP:sumamu-0003` since version `ZIP-0002` is reserved for [HTLCs](https://github.com/georgezgeorgez/ZIP.deeZNNutz)
[/quote]

According to the ZIP spec outlined in https://forum2.zenon.org/t/zip-deeznnutz-0001-final I think it should be ZIP:sumamu-0001 instead. I'm not sure if you're running a pillar otherwise the ZIP draft should be sponsered by a pillar and named accordingly.

-------------------------

0x3639 | 2023-03-09 12:47:36 UTC | #11

[quote="sumamu, post:7, topic:1327"]
can you help me modify the ZIP number? I want to change it from `ZIP:sumamu-0002` to `ZIP:sumamu-0003` since version `ZIP-0002` is reserved for [HTLCs](https://github.com/georgezgeorgez/ZIP.deeZNNutz)
[/quote]

Yes, I changed the title to ZIP:sumamu-0001 DRAFT

This is your first ZIP with no sponsor so I left it under your name.  I changed it to DRAFT because it might change after feedback from the community.  The ZIP framework also says the name should be under the name of a Pillar once it's sponsored by them.  

Some potential Pillars that are also coders who could be good sponsors are:

@MoonBaZe 
@georgezgeorgez 
@vilkris 

georgezgeorgez and vilkris are very open contributors to the project.  MoonBaZe could be too, but maybe under an alt.  Other Pillars will look to these guys (and other community devs) to review the code, understand the code, and support your work.  The only thing we can rely on Kaine to do is merge the code into /zenon-network.  The community review and Pillar support is all that matters to me to run the code.  For example, if George supports this code, posts it to his Ignition repo, and starts running it, I will too.  

I recommend you reach out to one of these guys and ask them to sponsor the ZIP.  When they do, they will change the name of the ZIP, host it in their ZIP repo, and help others become comfortable.

-------------------------

sol | 2023-03-09 15:32:33 UTC | #12

Do we have a plan to respond to a liquidity drain attack?
Some bridges impose limits that reduce the effectiveness of such attacks.

Should this ZIP include contingency measures for [potential exploits](https://crosschainbridges.blog/2022/10/13/analyzing-bridge-hacks/)?

-------------------------

0x3639 | 2023-03-09 16:53:19 UTC | #13

TC has a mechanism where TX over a certain limit take longer to process so the community has time to review them.

-------------------------

sumamu | 2023-03-10 16:50:38 UTC | #14

We took extensive security measures to prevent and deter malicious activities.

The philosophy underpinning the architecture is based on the `Law of Action-Reaction`. There can be no effect without a cause: every `redeem` transaction processed by the bridge must adhere to this causality principle. This means that funds must be `locked`/`burned` on the source network in order to be redeemed on the destination network.

[quote="sol, post:12, topic:1327"]
Do we have a plan to respond to a liquidity drain attack?
[/quote]

*Every action* that involves *redeeming funds* is **guarded** by the **time-challenge** primitive. 

After the redeem request is created, there is a window during which the funds are unredeemable. Also during this window, the `orchestrator` nodes will check if there is a corresponding transaction on the source network that `locks`/`burns` the funds. In case it doesn't exist, the `orchestrator` nodes will start the `halting` process of the bridge.

[quote="sol, post:12, topic:1327"]
Some bridges impose limits that reduce the effectiveness of such attacks.
[/quote]

The mechanism presented earlier applies to *every* transaction, *regardless of the amount*.

[quote="sol, post:12, topic:1327"]
Should this ZIP include contingency measures for [potential exploits ](https://crosschainbridges.blog/2022/10/13/analyzing-bridge-hacks/)?
[/quote]

1. Smart Contract Bug

The smart contracts are subjected to static analysis procedures and extensive unit-testing. Any additional external audits are welcomed.

2. Underlying blockchain implementation bug

The embedded contracts have been thoroughly tested with over 280 independent functionalities and edge-cases covered by 50 unit-tests.

3. Off-chain infrastructure bug

There are two distinct off-chain entities that are logically and physically distributed (`orchestrator` nodes and `admin`) that can halt the bridge in case of any malicious activity.

4. Crypto key exploit

The `orchestrator` nodes relies on a *TSS scheme* which *distributes* shares to every participant and is *decentralized by design*: the private key is not reassembled when signing messages. The `go-tss` and `tss-lib` libraries are already audited.

5. Key security risk assumption failure

The `admin` key is kept in cold-storage. Moreover, if the `admin` key is lost or stolen, the bridge will enter emergency mode,  and the `guardians` can elect a new `admin` to restore functionality. 

Additionally, we are looking to integrated a hardware security module `HSM` to manage sensitive cryptographic material.

[quote="0x3639, post:13, topic:1327, full:true"]
TC has a mechanism where TX over a certain limit take longer to process so the community has time to review them.
[/quote]

This is exactly our `time-challenge` security primitive, but we apply it for every transaction.

-------------------------

sol | 2023-03-10 17:10:29 UTC | #15

Thank you for elaborating, I appreciate the detailed response.

[quote="sol, post:12, topic:1327"]
Should this ZIP include contingency measures for [potential exploits ](https://crosschainbridges.blog/2022/10/13/analyzing-bridge-hacks/)?
[/quote]

What I mean by this is, complex software is rarely flawless and we only have one liquidity pool. We don't have the luxury of replenishing the funds.

Should the ZIP also propose a set of actions in case the bridge is exploited? Or should this be a separate conversation?

-------------------------

sumamu | 2023-03-11 19:51:33 UTC | #16

[quote="sol, post:15, topic:1327"]
Should the ZIP also propose a set of actions in case the bridge is exploited? Or should this be a separate conversation?
[/quote]

Happy you've asked this. This is the exact reason why we have a dedicated [emergency state](https://github.com/HyperCore-Team/orchestrator/blob/e87d833d1664844499530152960137060b4e7740/common/global_state.go#L12) and why we designed a layered security architecture based on the `Law of Action-Reaction`:
1. A time-challenge primitive for every transaction
2. A distributed halting mechanism (check point number 3 from the previous post)
3. Guardians voting system as fallback

The time invested in the security details of this project was tremendous to say at least.

-------------------------

sol | 2023-03-11 20:24:03 UTC | #17

I don't think many people understand how the emergency state works.
Will you be releasing technical documentation soon?

-------------------------

sumamu | 2023-03-20 12:28:50 UTC | #18

The NoM Multi-chain Infrastructure documentation is published on Github:

https://github.com/HyperCore-Team/nom-multichain-docs

-------------------------

sumamu | 2023-03-21 10:29:10 UTC | #19

The documentation is now available in web format here:

https://hypercore-team.github.io/

-------------------------

sol | 2023-05-02 18:15:49 UTC | #20

Do you have any flowcharts that map out ways functions can be accessed?
Like a high-level view of the bridge/liquidity solution to assist with identifying conditions that trigger specific functions.

If possible, can you please provide this as part of the documentation?

-------------------------

