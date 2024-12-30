Thread: network-of-momentum-phase-1
aliencoder | 2023-12-04 22:25:04 UTC | #1

# Network of Momentum Phase 1

Solving Dynamic Plasma, merge-mining, PoW links and positive incentive feedback loops all at once. 

Prepare mentally before reading this post. 

*Disclaimer: it's still work in progress.*

## Objectives

During NoM Phase 1, we aim to attain the following goals:

- Establish a self-sustaining network by fostering positive feedback loops that will attract users and builders.
- Implement a balance between ASIC-friendly and CPU-friendly Proof of Work (PoW) algorithms as outlined in the whitepaper.
- Incorporate the recording of PoW onto the block-lattice for our fork selection algorithm.
- Encourage adoption by integrating a hybrid multi-lane fee system into the network.

The concept of peer-to-peer mining pools was introduced to decentralize the mining operations for any given proof-of-work blockchain. The concentration of hashrate into the hands of a few centralized pools is dangerous for a number of reasons.

### Properties

By integrating the first decentralized, peer-to-peer (merge)-mining pool for Bitcoin & RandomX and several other algorithms, we aim to enhance the following properties that are at the core of our shared ethos:

#### **Censorship-resistance**

There is no centralized server to steal hashrate, impose a certain block template for example mining empty blocks in Bitcoin or even worse blacklisting certain transactions. We already see that centralized mining pools in certain jurisdictions can be targeted and forced to comply.

#### **Decentralization**

By communicating exclusively through the peer-to-peer network, miners coordinate by working on a share-chain. If properly implemented, it can be as efficient as a centralized pool.

There is no pool admin: attacks by rogue pool operators on Bitcoin are no longer possible.

Moreover, miners with older ASICs can turn them on even if they have a lower hashrate and contribute on a lower difficulty share-chain and still be profitable.

#### **Merge-mining BTC & ZNN**

By directing hashpower to NoM, miners will earn ZNN rewards from Pillars. We need to divert ZNN away from delegators in order to be able to properly incentivize miners and lay out the foundation for Phase 1. 

Bitcoins will be generated. TSS will be leveraged for a decentralized custody of the freshly mined BTC. ZNN will be backed by physical BTC. This positive feedback loop aims to encourages participation and further decentralizes the distribution of the hashpower.

#### **Ledger weight**

In Nakamoto consensus, participants choose the heaviest chain that has the most hashpower invested into it. The share-chains obtained with PoW will be embedded contracts with account-chains that will add up to NoM's ledger weight and be used to "anchor" the consensus as described in the whitepaper.

#### **Dynamic difficulty**

Here comes into play the CPU-friendly PoW algorithm: a separate share-chain based on RandomX (can be merge-mined with Monero) where miners can generate share-blocks. This share-chain will be used to compute a threshold for the dynamic difficulty for PoW (CPU-friendly) feeless transactions.

#### **PoW links**

Sentinel nodes relay only transactions with a minimum amount of (RandomX) PoW. Transactions (account-blocks) must have the minimum PoW threshold to be accepted by the network and further relayed to other Sentinel nodes. This creates a competition to "mine" transactions in order to be able to successfully route them through the network. Sentinels should be paid on the amount of transactions they have routed in any given epoch. Remember Sentinels generate both ZNN and QSR. Interesting design choice. (work in progress)

#### **ZNN fee**

In order to achieve global scale and global adoption, clients submitting transactions should be able to avoid computing PoW, especially if they are on battery powered devices. Fusing QSR requires PoW, so we must adopt a third option that will take into account another critical aspect of a healthy network: incentivizing the peer-to-peer layer comprised of full nodes. Therefore, clients should be able to attach a ZNN fee to their transaction that will be divided downstream between all the full nodes that propagate the transaction. Initially I've proposed burning the fee, but it doesn't solve the incentive problem of full nodes that are costly to operate and much needed for a decentralized and censorship-resistant p2p layer.

Stay tuned for the next chapter: the implementation (work in progress).

## Network participants

- Pillars: generate ZNN
- Sentinels: generate ZNN & QSR
- Delegators: generate ZNN
- Stakers: generate QSR
- Liquidity Providers: generate ZNN & QSR
- Miners: generate ZNN & QSR
- Full nodes: generate ZNN

In NoM Phase 1 there will be two new first class network participants:

- Miners: supply hashpower to the network. They will be rewarded in ZNN and QSR (redirected from delegators, stakers and Sentinels)
- Full nodes: the backbone of the p2p network that relay transactions. They will receive ZNN for relaying transactions throughout the network.

Open questions:

- Perpetual AZ funding: how to replenish AZ funds?
- ZNN burn: we cannot burn part of the fees because we sabotage the sybil-resistance property of the p2p layer.

## Implementation

In order to actually implement those ideas we need to build upon several building blocks.

### **Primitives & Building Blocks**

#### Threshold signature scheme

Required to hold and spend BTC in a trustless manner. Top Pillars will run a [FROST](https://github.com/ZcashFoundation/frost) / [ROAST](https://eprint.iacr.org/2022/550.pdf) / [Sparkle](https://eprint.iacr.org/2023/445.pdf) TSS ceremony to jointly create a key for the decentralized custody of the BTC. We can either integrate this directly into `znnd` or into the `orchestrator` binary.

The on-chain BTC will be used to pay for block space e.g. to create [tapscripts](https://bitcoinops.org/en/topics/tapscript/).

The Pillars already run full `znnd` full nodes and must also run the `bitcoind` full node to communicate with the peer-to-peer Bitcoin network.

#### Merge-mined share-chain

A new embedded contract for the share-chain. Embedded contracts have an account-chain [structure](https://zenon.tools/accounts/z1qxemdeddedxdrydgexxxxxxxxxxxxxxxmqgr0d) that is suited to host a share-chain.

The share-chain is basically a separate blockchain that is merge-mined with the target blockchain. In our case we have Bitcoin (ASIC-friendly, used to add weight to the ledger and Monero (CPU-friendly, used to compute the minimum difficulty for feeless transactions via PoW).

The best part is that our network already has the data structure required to build the share-chain: the account-chain of the embedded contract. Also the account-chain is guaranteed to have ordering by NoM consensus. This is important for accounting purposes, such that miners that participated and created valid shares (account-blocks) are incentivized by Pillars with delegation rewards.

- **Bitcoin** merge-mining: embedded contract for `SHA-256d`

ZNN is backed by BTC, so it means that miners are already are paid in BTC (if ZNN will be redeemable in BTC) and also capture the potential upside of ZNN. If ZNN rewards aren't enough, we can set a flexible payout in BTC for the top x% miners that contributed with the most hashpower to the network during a given epoch. Pillars can independently access and attest this information from the embedded contract. It really boils down to how much hashpower we can attract on the network. We have the possibility to setup two competing merge-mined share-chains and only reward extra (with BTC) the highest difficulty share-chain. From what I've analyzed, Monero implemented this concept (mini-share-chain) where small miners (up to x hash/s) can participate. The idea is to avoid the variance caused by miners with more hashrate and the payouts will even out on longer timeframes.

#### Dynamic difficulty algorithm

- **Monero** merge-mining: embedded contract for `RandomX`; due to [incentive incompatibility](https://theory.stanford.edu/~tim/papers/bitcoin.pdf), I suggest implementing 2 share-chains *lite* and *max* depending on the miner's hashpower. The [difficulty algos](https://github.com/zawy12/difficulty-algorithms) will be computed such that all PoW transactions must satisfy the current difficulty.

#### Hybrid multi-lane load balancing algorithm

Load balancing algorithm that will dynamically adjust the size of transaction lanes based on ongoing user traffic:

1. Feeless PoW lane with dynamic difficulty adjusted based on a weighted average of the CPU-friendly share-chain.
2. Feeless QSR fusing lane.
3. Fee lane with ZNN that goes into the incentivization of full node transaction routing.

#### Routing algorithm

We can borrow ideas from [here](https://wiki.saito.io/consensus/sybil-proof) to create a new incentives layer for the peer-to-peer network of full nodes that relay transactions.

#### PoW links

Sentinels must attach a PoW to every transaction and relay it to another Sentinel node before reaching a Pillar. This PoW can be outsourced to miners. Sentinels will compete for RandomX miners, creating a new economy around this model. Sentinel operators will be able to setup off-chain reward mechanisms for miners adding weight to the PoW links. We must also take into account the additional data that is added to every transaction. Sentinels should use an [aggregate signature scheme](https://crypto.stanford.edu/~dabo/pubs/papers/aggsurvey.pdf) - "reducing message size in secure routing protocols such as SBGP".

-------------------------

Chadass | 2023-12-03 01:21:46 UTC | #2

How does the fee solve the public nodes incentives problem? At which volume of tx VS number of nodes it becomes an actual incentives so you can pay 30$ per month and run a nodes on a VPS? Let's say there's 10 times the amount of tx we have now per day and all uses fee VS 1 node to incentive, is that 30$ or is the node operator actually losing money?

Also is Narwal and Tusk part of the Phase 1?

-------------------------

aliencoder | 2023-12-03 11:07:14 UTC | #3

[quote="Chadass, post:2, topic:253"]
How does the fee solve the public nodes incentives problem?
[/quote]

Check my [previous post](https://forum.hypercore.one/t/the-p2p-revolution-pow-links-reloaded/248).

[quote="Chadass, post:2, topic:253"]
At which volume of tx VS number of nodes it becomes an actual incentives so you can pay 30$ per month and run a nodes on a VPS?
[/quote]

Do you even read posts? I've already answered this [here](https://forum.hypercore.one/t/the-p2p-revolution-network-of-momentum-phase-1/245/12?u=aliencoder).

[quote="Chadass, post:2, topic:253"]
Also is Narwal and Tusk part of the Phase 1?
[/quote]

Yes. The more I [read](https://arxiv.org/pdf/2102.08325.pdf) about DAG consensus, the more I'm impressed with Zenon's whitepaper: "We construct DAG-Rider in two layers: a communication layer and a zero-overhead ordering layer.". The consensus protocol will run on the meta-DAG.

-------------------------

Chadass | 2023-12-03 13:09:24 UTC | #4

How much time you think will be needed for the implementation part?

-------------------------

aliencoder | 2023-12-03 21:38:56 UTC | #5

Once I finish the architecture and specs, I hope we can shift most dev effort into it.

NoM Phase 1 will be a game changer for the L1 landscape. It will obsolete all "scalable" L1s.

-------------------------

Chadass | 2023-12-04 01:03:49 UTC | #6

Do you have an estimate of time needed ? I'm simply curious here.

-------------------------

1776 | 2023-12-04 16:48:54 UTC | #7

[quote="aliencoder, post:5, topic:253"]
NoM Phase 1 will be a game changer for the L1 landscape. It will obsolete all “scalable” L1s.
[/quote]

Can you summarize the "how" for this in 1-2 sentences for Hypergrowth efforts?

-------------------------

aliencoder | 2023-12-04 18:04:15 UTC | #8

[quote="Chadass, post:6, topic:253"]
Do you have an estimate of time needed
[/quote]

I can give you once we are all on the same page.

[quote="1776, post:7, topic:253"]
Can you summarize the “how” for this in 1-2 sentences for Hypergrowth efforts?
[/quote]

I want to finish the post and then you can feed the content into ChatGPT. The key takeaway is that the majority of L1s are based on inferior proof-of-stake consensus and broken incentives - that's why even Ethereum with near unlimited funding and support wasn't able to scale. They realized that scaling on L1 is a mirage by moving the problem on the shoulders of L2s.

-------------------------

KayRSwon | 2023-12-05 02:15:32 UTC | #9

Instead of creating an architecture for fees to pillars and delegators, is there not a way to allow those with extra QSR to fuse some plasma as a service?

-------------------------

aliencoder | 2023-12-05 08:18:56 UTC | #10

Inspired by the ZTS issuance mechanism that burns 1 ZNN in order to be able to create a new ZTS token, the bridge fee system and how the Pillar slot mechanism works (Pillars have a disincentive to disassemble their node because by doing it they basically waste all their invested QSR), I'm proposing the following operations to create long term sustainability (replenish AZ funds) and achieve mint-and-burn equilibrium for both ZNN and QSR:

[quote="aliencoder, post:1, topic:253"]
* Perpetual AZ funding: how to replenish AZ funds?
[/quote]

Sentinel revoke => 1% rewards ZNN & QSR redirected to AZ (or fixed amounts)
Stake revoke => 1% reward ZNN redirected to AZ (or fixed amount)
LP unstake => 1% rewards ZNN & QSR redirected to AZ (or fixed amount)

Why? It creates a disincentive to abandon the network (revoking, unstaking means that you will no longer have skin in the game) and at the same time, a little part of what you've gained from the network will go into its long term sustainability efforts (Accelerator-Z). 

Please notice that I've excluded Pillars because they already sacrifice a lot of QSR to create the Pillar slots in the first place and are operating critical network infra (including the bridge infra and potentially extension chains). Also miners and full nodes that have real world upfront costs in terms of electricity and hardware.

[quote="aliencoder, post:1, topic:253"]
ZNN burn: we cannot burn part of the fees because we sabotage the sybil-resistance property of the p2p layer.
[/quote]

ZTS token issuance => 1 ZNN burned
Undelegate => 1 ZNN burned
QSR unfuse => 1 QSR burned

Why? Disincentivizes frequent change of delegations and potential spamming using the QSR lane.

-------------------------

Nostromo | 2023-12-05 09:09:29 UTC | #11

Hi aliencoder, this is a huge thread. I'm a beginner dev who just started learning Flutter with the hopes of contributing to  s y r i u s  in the future.

There is a lot going on in this thread, with each area deserving a lot of thought. I have many questions, but I will restrain from bombarding you all at once.

The first question I have is: What is a Sentinel?

There is a recurring theme in your thoughts about incentivization. It seems that a portion of the minted ZNN and QSR is being dispensed by the Sentinel contract every day without tangible network contribution.

This is a peculiar situation. Either there is an intended purpose for a Sentinel yet to come, or those emissions could be used elsewhere more effectively.

An idea that seems cool to me (though I have no scope on the realities of the implementation) would be to have Sentinels as full nodes. Because of the incentive, it would be reasonable to target higher-end hardware. This could allow end users to run 'light' nodes as access points.

Economically, this could make sense as the price of ZNN and QSR rises against BTC and fiat, it becomes progressively more lucrative to run a Sentinel, causing more to come online to meet the demand.

Additionally, one could devise a system where the Sentinels keep each other honest and punish dishonest nodes.

From a layman's perspective, this seems like it could work, but I'm sure there are probably some glaring flaws here.
I'm eager to read your views on this and your general thoughts on Sentinels as well.

-------------------------

1776 | 2023-12-05 09:33:15 UTC | #12

100% for this AZ funding mechanism.  Was always concerned about relying solely on the goodwill of donations.  

[quote="aliencoder, post:10, topic:253"]
Sentinel revoke => 1% rewards ZNN & QSR redirected to AZ (or fixed amounts)
Stake revoke => 1% reward ZNN redirected to AZ (or fixed amount)
LP unstake => 1% rewards ZNN & QSR redirected to AZ (or fixed amount)
[/quote]

-------------------------

0x3639 | 2023-12-05 10:25:32 UTC | #13

[quote="Nostromo, post:11, topic:253"]
The first question I have is: What is a Sentinel?
[/quote]

Have a look at the white paper: https://znn.link/whitepaper

-------------------------

0x3639 | 2023-12-05 10:37:59 UTC | #14

[quote="aliencoder, post:10, topic:253"]
Sentinel revoke => 1% rewards ZNN & QSR redirected to AZ (or fixed amounts)
[/quote]
Are you proposing that 1% of 5000 znn 1% of 50,000 QSR divert to AZ upon revoke?  Seems like a small price to pay.  We were talking about diverting 50% of emissions to AZ in TG a few days ago.  We might consider increasing the percentages / amounts initially and then phase them down over time.

-------------------------

Nostromo | 2023-12-05 11:10:39 UTC | #15


Hello, sir. Yes, I have read the whitepaper, and it provides a fairly vague description.

I suggested the idea above based on how nodes are described in the white paper. Sentinels are portrayed as trustless nodes that act as observers, requiring moderate resources. Additionally, there are Sentry nodes, described as basic nodes that are lightweight and store a pruned ledger. This setup closely resembles the one I described above.

All things considered it's worth noting that the whitepaper is labeled as a draft, and there has been some deviation from it with the implementation of the alpha net.

The alphanet wiki is intriguing, as it defines a Sentinel as a full node in the "definitions" section ( https://github.com/zenon-network/znn-wiki/blob/master/definitions.md#sentinel-node ). 
In the "deploy" section, it states, "The znn-controller works only for Pillars for the moment. Sentinel support will be available after Alphanet launch."

So, the question arises: Is it worthwhile to devise an incentivization process for remote full node operators if this Sentinel and Sentry dynamic will be implemented? 
And along the same line of reasoning, does the fee lane proposal for dynamic plasma make sense to implement under this circumstance?

-------------------------

0x3639 | 2023-12-05 11:18:40 UTC | #16

[quote="Nostromo, post:15, topic:253"]
So, the question arises: Is it worthwhile to devise an incentivization process for remote full node operators if this Sentinel and Sentry dynamic will be implemented?
[/quote]

Good question.  Sentinels are expensive to launch 5,000/50,000.  If the goal is to have lots of them,  we probably cannot rely on sentinels alone as public nodes.  We discussed that here.  Read that thread.

https://forum.hypercore.one/t/the-p2p-revolution-network-of-momentum-phase-1/245/17?u=0x3639

[quote="Nostromo, post:15, topic:253"]
And along the same line of reasoning, does the fee lane proposal for dynamic plasma make sense to implement under this circumstance?
[/quote]

Read this post.  I don’t think the fee lane is fully vetted yet.  We need to reconcile Alien’s latest thinking with the work on Dynamic Plasma. 

https://forum.hypercore.one/t/ideas-for-dynamic-plasma/233

-------------------------

Nostromo | 2023-12-05 13:27:29 UTC | #17

> Sentinels are expensive to launch 5,000/50,000. If the goal is to have lots of them, we probably cannot rely on sentinels alone as public nodes.

The central question is whether the goal is to have many Sentinels, how many are considered enough? It is not immediately obvious that more equals better.

Bitcoin, which I just looked up, has an estimated 13 thousand full nodes in the network. They help create consensus, where the longest chain is what individual nodes accept as the valid version of the blockchain. At least that's how I understand it.

However, we don't have that design. Our Pillars agree on what the valid version of the blockchain is. As far as I can tell, our full nodes serve as a medium for the transactional layer, which is separated from the consensus layer.

So, in that sense, the question remains: how many Sentinels does one need for network stability?

The cost to launch a Sentinel is crucial as it protects from economic attacks, it makes it very difficult for an attacker to launch 100 Sentinels at once, for example.

A large benefit for prospective operators is that the cost is redeemable when a Sentinel is revoked, making a Sentinel profitable after the first day (In ZNN & QSR scope).

-------------------------

0x3639 | 2023-12-05 12:21:21 UTC | #18

Devs are considering this possibility.

-------------------------

Nostromo | 2023-12-05 12:24:48 UTC | #19

@aliencoder I feel like I'm at the risk of seeming like I'm trying to throw a spanner in the works of your ideas.

I want to express that I think the BTC mining pool on the share chain or extension chain is an incredible idea! I'd love to see that fleshed out and am keen to learn about merge mining and how this could be implemented.

-------------------------

0x3639 | 2023-12-05 12:44:58 UTC | #20

[quote="Nostromo, post:19, topic:253"]
I feel like I’m at the risk of seeming like I’m trying to throw a spanner in the works of your ideas
[/quote]

Best ideas win around here so I’m curious to see where this conversation goes.  

Regarding your question about what is a Sentinel.  As I understand it, a Sentinel is a full node that is tasked with relaying messages a minimum of 3 hops and adds PoW links to each message.  Alien posted some recent research into this idea and why it’s valuable.  Maybe you read that paper.

https://forum.hypercore.one/t/the-p2p-revolution-pow-links-reloaded/248?u=0x3639

So my original question was, why can’t the Sentinel serve as an incentivized public node in the network. They are a full node and they are incentivized.  

I guess I did not fully appreciate that nodes really don’t offer network security like BTC.  So if that is the case, why are more nodes better? Why aren’t Sentinel nodes enough as the main public node in the network.  And how many Sentinels are necessary to perform the message relay function and to act as a public node?    

I’ll look at the white paper again to try and learn more.

-------------------------

Nostromo | 2023-12-05 13:13:59 UTC | #21

>  Sentinel is a full node that is tasked with relaying messages a minimum of 3 hops and adds PoW links to each message

Wow, I just had a look at that paper, and it goes way above my head. Very complicated and needs study to understand.

But from what I can gather, this three-hop path creates Sybil resistance and causes nodes to act in a certain way.

This is pure speculation, but we have an anti-Sybil mechanism implemented that isn't described in the whitepaper at all: Plasma. Could it be that Plasma superseded the PoW link idea for Sybil resistance?

Or maybe the PoW links are used for the Sentinels to keep each other in check and honest? I don't know; that paper was too advanced to make heads or tails of it for me.

-------------------------

0x3639 | 2023-12-05 13:24:22 UTC | #22

[quote="Nostromo, post:21, topic:253"]
Or maybe the PoW links are used for the Sentinels to keep each other in check and honest? I don’t know; that paper was too advanced to make heads or tails of it for me.
[/quote]

“ the PoW link will serve an additional objective in the consensus algorithm, representing an eliminatory criteria to select between two conflicting transactions in case of a double spend. ”

-------------------------

Chadass | 2023-12-05 13:47:40 UTC | #23

[quote="aliencoder, post:10, topic:253"]
ZTS token issuance => 1 ZNN burned
Undelegate => 1 ZNN burned
QSR unfuse => 1 QSR burned
[/quote]

I'd totally disagree with the Undelegate cost. It's often about moving from Pillars changing their rewards politic or going offline so why the delegate should bear that cost?

-------------------------

Nostromo | 2023-12-05 13:50:58 UTC | #24

That is curious indeed because the whitepaper also states that Sentinels don't participate in the consensus algorithm. However, it then adds that they create PoW links for transactions, as mentioned on the bottom of page 7.

This is somewhat contrary to your quote. It does make conceptual sense to have it like this to settle a double spend, though.

The question is, how are double spends settled now, without PoW links? Perhaps because it's currently all very sequential, it eliminates the possibility of double spends?

Perhaps this comes into play in a more asynchronous environment. 
Reading the initial lite paper Sharding was mentioned but that seems to now have shifted to Narwhal and Tusk. 

I find the Pow links difficult to understand.

-------------------------

aliencoder | 2023-12-05 14:31:15 UTC | #25

[quote="0x3639, post:14, topic:253"]
Are you proposing that 1% of 5000 znn 1% of 50,000 QSR divert to AZ upon revoke
[/quote]

It's just an example.

[quote="0x3639, post:14, topic:253"]
We might consider increasing the percentages / amounts initially
[/quote]

I agree, but let's see what others have to say. Should be kept at reasonable levels.

[quote="Nostromo, post:15, topic:253"]
Is it worthwhile to devise an incentivization process for remote full node operators if this Sentinel and Sentry dynamic will be implemented?
[/quote]

Sentinels cannot sustain the whole network. They also serve other own purpose: crafting PoW links.

Full nodes can take the role of Sentries. In NoM's architecture a full node is actually a node participating in the p2p layer. It doesn't need to store the meta-DAG (consensus layer), that's why in the whitepaper they are described as "lightweight". They also service end users (via RPCs).

[quote="Nostromo, post:15, topic:253"]
And along the same line of reasoning, does the fee lane proposal for dynamic plasma make sense to implement under this circumstance?
[/quote]

[quote="0x3639, post:16, topic:253"]
We need to reconcile Alien’s latest thinking with the work on Dynamic Plasma.
[/quote]

It does, because there are no incentives for the p2p layer that is critical for any decentralized network.

[quote="Nostromo, post:17, topic:253"]
where the longest chain is what individual nodes accept as the valid version of the blockchain
[/quote]

[quote="Nostromo, post:17, topic:253"]
which is separated from the consensus layer.
[/quote]

Good observations. The consensus layer is indeed separated and this is intentional: the transactional ledger gets its weight from PoW that clients (and eventually miners) will generate. In Bitcoin you have the longest chain with the most proof-of-work (created by miners with PoW) invested into it. In NoM, you have the meta-DAG (created by Pillars with PoS) and the heaviest ledger (created by clients and miners with PoW).

[quote="Nostromo, post:17, topic:253"]
So, in that sense, the question remains: how many Sentinels does one need for network stability?
[/quote]

Even if 20% of the current number of Sentinels will still exist during Phase 1, I think it will still be OK.

[quote="Nostromo, post:17, topic:253"]
The cost to launch a Sentinel is crucial as it protects from economic attacks, it makes it very difficult for an attacker to launch 100 Sentinels at once, for example.
[/quote]

You'll need 500k ZNN and 5M QSR (locked capital) *and* you still need some PoW for the PoW links if you don't want to incentivize RandomX miners at all.

[quote="Chadass, post:23, topic:253"]
moving from Pillars changing their rewards politic or going offline so why the delegate should bear that cost
[/quote]

Usually delegators are "reward" hopping. As a delegator, you will do your DYOR twice if you know that undelegation has a cost. It's not even an upfront cost, so it's reasonable because you make rewards in the meantime. A Pillar going offline is a rare event, we can treat it as a special situation where the 1 ZNN burn fee won't apply (because we can check if the Pillar is disassembled or not).

[quote="0x3639, post:20, topic:253"]
They are a full node and they are incentivized.
[/quote]

There won't be enough of them. There can be up to several hundred Sentinels in the network (even less because it won't be profitable to operate one because the rewards are fixed). Bitcoin has tens of thousands of full nodes in the p2p network.

[quote="0x3639, post:20, topic:253"]
I guess I did not fully appreciate that nodes really don’t offer network security like BTC
[/quote]

Of course full nodes offer security. But not "direct" security like miners. It's more "political" in the sense that miners can fork Bitcoin, but full nodes can only accept a particular version as the canonical chain. Anyone remembering #UASF during the fork wars? It's a separation of powers between miners that control the hashrate and full nodes that control chain "vetting". The same separation of powers in NoM is between Pillars that control consensus and clients - including Sentinels, merge-miners, etc. that control ledger weight.

-------------------------

Chadass | 2023-12-05 19:54:01 UTC | #26

[quote="aliencoder, post:25, topic:253"]
It does, because there are no incentives for the p2p layer that is critical for any decentralized network.
[/quote]

It's not critical for BTC.

-------------------------

Chadass | 2023-12-05 19:54:32 UTC | #27

[quote="aliencoder, post:25, topic:253"]
Usually delegators are “reward” hopping. As a delegator, you will do your DYOR twice if you know that undelegation has a cost. It’s not even an upfront cost, so it’s reasonable because you make rewards in the meantime. A Pillar going offline is a rare event, we can treat it as a special situation where the 1 ZNN burn fee won’t apply (because we can check if the Pillar is disassembled or not).
[/quote]

You can't predict pillars missmanagement or suddenly going MIA.

-------------------------

Shazz | 2023-12-05 21:31:43 UTC | #28

I suggest we dont tinker with emissions before there's any usability that can drive growth. Lets focus on stuff that actually matters and finally allows zenon to escape this bubble. The AZ contract is well funded. Demand will offset emissions. Diverting emissions into AZ prematurely is just procrastiation to actually building usability.

-------------------------

Nostromo | 2023-12-06 02:44:22 UTC | #30

@aliencoder thanks for answering questions; I understand that this can be time-consuming, so I really appreciate it.

I have been doing a bit of reading, and I'd like to drill a bit further into the Sentries and Sentinel dynamic. I will describe some topology related only to the transactional layer as I understand it, and I'd appreciate it if you could point out errors or add anything of note.

So we have a peer-to-peer layer; Sentry nodes facilitate communication and data propagation. When a Sentry joins the network, it needs to discover other Sentries to establish connections and exchange handshakes. Sentries maintain multiple connections with other Sentries, and the P2P layer creates a dynamic network allowing nodes to join or leave without disrupting overall functionality.

A Sentry node does not require a copy of the entire ledger, as it may reference a pruned version or use a zk proof to reference a 'checkpoint' of the ledger. This allows a user to run a Sentry and join the network, bypassing the need to sync and download the entire ledger.

When a user initiates a transaction, their Sentry broadcasts it to the network of Sentries, where it is propagated to all other connected Sentries. They check whether the transaction adheres to the prescribed format and verify the digital signatures.

Sentinels, on the other hand, store the entire ledger and are the source of truth for the transactional ledger. Sentries acquire their pruned ledger from the Sentinels or query the Sentinels via zk proofs for the ledger.

Once a transaction has propagated sufficiently via the Sentries, the Sentinels then add PoW links to the transaction, which guards against a double spend. Once the transaction has sufficient weight, it may be forwarded to the consensus layer to be included in a block.

This is my understanding so far. Is it somewhat accurate? I have some more in-detail questions, but I just want to make sure I haven't made any huge errors and solidify a baseline of understanding.

-------------------------

0x3639 | 2023-12-06 03:12:26 UTC | #31

I know this is a question to Alien, but you seem to have some ideas into how Sentries could work.  I’ve looked at the white paper trying to understand how Sentries works and it’s pretty vague.  Seems like a Sentry is different than a Public node.

What is the purpose of running a node for specific account only?  Maybe faster and lighter to run?  Seems like we have three actors running similar information: Sentry, Public Node, and Sentinels.  

If Sentinels are public full nodes, why run a Sentry?  Maybe because they are light and fast and quick.  Maybe something that can be run on a phone for my account chain only to send and receive TXs.  So why do we need public nodes assuming we have a sufficent number of Sentinels?  @aliencoder thinks the public node provides security.  But you seem to be questioning that assertion.  @Nostromo I think it would be helpful to agree on the function of a public node and their role in providing security.  

![IMG_1270|690x188](upload://jFm83p9UzgWRTBZml4q7lmEIptg.jpeg)

-------------------------

Nostromo | 2023-12-06 04:13:16 UTC | #32

I also thought that it might be something low-impact that users can run. Just now, I have been reading about block lattice structures as I was trying to understand the PoW Link topic a bit better and how it relates to double spends.

I found two interesting points:

1. Block lattice structures inherently prevent double spending as each account chain maintains its own chronological order of transactions. Since transactions are confirmed by the account owner, there is no need for a global consensus mechanism to prevent double spends.
2. Nodes in a block lattice network need to stay synchronized with the state of each account-chain. This can be achieved through a gossip protocol or other mechanisms to ensure that all nodes have a consistent view of the ledger.

Maybe the Sentry nodes are dedicated to account chains, and the Sentinels are dedicated to the overall coherence of all account chains?

Phew, complicated stuff to wrap your head around.

-------------------------

Nostromo | 2023-12-06 10:58:00 UTC | #33

This section of the whitepaper spells out the transaction flow and node properties (at the bottom of page 9): 

"The flow of issuing a transaction is as follows: a user will have assigned some representative nodes, sentinel nodes that will process their transactions and that can be queried in order to pull new information regarding the account chain or the state of the ledger.

However, in order to prevent denial of service attacks, the queries can require a fee that needs to be applied in order to return a valid response: for example, a user can use the sentinel nodes for querying the state of the ledger or sentry nodes to get updates regarding its account chain.

As we highlighted earlier in the Definitions subsection, not all network participants are also consensus
nodes; only full nodes (i.e. pillar and sentinel nodes) keep both the transactional ledger and consensus ledger"

The language here is quite opaque, but the phrasing of, "query sentry nodes to get up updates regarding its account chain". That sounds like the account is paired/belongs to the sentry.

*edit: actually I think I misinterpreted that - when saying it's account chain I think it's referring to the account chains of the ledger and not the Sentry.

-------------------------

aliencoder | 2023-12-06 11:01:35 UTC | #34

[quote="Chadass, post:26, topic:253"]
It’s not critical for BTC.
[/quote]

[quote="aliencoder, post:1, topic:245"]
Bitcoin survived because it chose the path of small blocks to safeguard the peer to peer network.

Small blocks represent the trade-off made to preserve the status-quo of the current peer-to-peer network that relies on volunteers around to world to operate and maintain it.
[/quote]

Again, you either don't read my [posts](https://forum.hypercore.one/t/the-p2p-revolution-network-of-momentum-phase-1/245) or simply you ignore them. I won't answer you anymore if you totally ignore what I say.

[quote="Chadass, post:27, topic:253"]
You can’t predict pillars missmanagement or suddenly going MIA.
[/quote]

I don't want to predict anything. If a Pillar is disassembled, we can check that and remove the undelegation fee for this particular case.

[quote="Shazz, post:28, topic:253"]
I suggest we dont tinker with emissions
[/quote]

I agree. We don't change emissions. We just align all network participants and operations to create a self-sustainable network. This should be the main objective for Phase 1.

[quote="Shazz, post:29, topic:253, full:true"]
I agree this makes absolutely no sense. We need EXTERNAL DEMAND, not additional taxes on existing holders ffs
[/quote]

This is not a "tax on holders". It is a mechanism to deter spam and create long term sustainability. External demand will come after we finish the main components that will drive utility and continuous growth.

[quote="Nostromo, post:30, topic:253"]
They check whether the transaction adheres to the prescribed format and verify the digital signatures.
[/quote]

In my opinion Sentries were initially envisioned as light nodes. But they should definitely act as public full nodes that support the p2p network.

[quote="Nostromo, post:30, topic:253"]
which guards against a double spend
[/quote]

The consensus nodes guard against double spends. The PoW link only represents an eliminatory criteria used by honest consensus nodes to deterministically select which transaction should be included into the meta-DAG for ordering.

[quote="0x3639, post:31, topic:253"]
So why do we need public nodes assuming we have a sufficent number of Sentinels?
[/quote]

Because we won't have a sufficient amount of Sentinels. I've calculated earlier a maximum number. We need tens of thousands of public nodes for a truly decentralized network.

[quote="Nostromo, post:32, topic:253"]
Since transactions are confirmed by the account owner, there is no need for a global consensus mechanism to prevent double spends.
[/quote]

The block-lattice can't prevent double spends on its own, it needs the meta-DAG for consensus (ordering).

Some parts of the whitepaper are a little vague, but remember it is just a draft version. Even Mr Kaine pointed into this direction, especially with the incentivization of the p2p layer.

I have another insight to share about the meta-DAG related to the accumulation of PoW in the transactional ledger: the meta-DAG will be transient, as it will get garbage collected.

"To this end, Narwhal leverages the properties of a consensus protocol (such as the one we discuss in the previous section) to agree on the garbage collection round. Blocks from earlier rounds can be safely be stored off the main validator and all later messages from previous rounds can be safely ignored." from [Narwhal and Tusk: A DAG-based Mempool and Efficient BFT Consensus](https://arxiv.org/pdf/2105.11827.pdf).

-------------------------

Nostromo | 2023-12-06 12:35:13 UTC | #36

> In my opinion Sentries were initially envisioned as light nodes. But they should definitely act as public full nodes that support the p2p network.

My question here is, if they don't possess a copy of the ledgers and don't participate in consensus per se, can they still be considered full nodes?

In my perhaps idealized view, a Sentry could be so lightweight that it could be incorporated into nearly every type of client, partially eliminating the need for infrastructure providers as every user would have their 'embedded node' serving as a gateway to the network.

I understand your perspective in incentivizing public nodes to address the issue of centralized node providers. However, if we had thousands of public full nodes as you propose, how would you devise a system for users to connect to the most appropriate node for them?

Looking at Ethereum, for example, most users simply use centralized node providers. Many may be unaware of it, choosing this option because it's the default setting provided by their wallet.

How can we ensure that we don't face the same fate?

-------------------------

aliencoder | 2023-12-06 13:02:12 UTC | #37

[quote="Nostromo, post:36, topic:253"]
if they don’t possess a copy of the ledgers and don’t participate in consensus per se, can they still be considered full nodes
[/quote]

Yes, in Bitcoin full nodes don't participate into the consensus protocol either - miners do. I don't know yet if they need to store the entire dual-ledger or only the transactional ledger as the whitepaper states.

[quote="Nostromo, post:36, topic:253"]
partially eliminating the need for infrastructure providers
[/quote]

Totally eliminating*

[quote="Nostromo, post:36, topic:253"]
how would you devise a system for users to connect to the most appropriate node for them?
[/quote]

[quote="Nostromo, post:36, topic:253"]
How can we ensure that we don’t face the same fate?
[/quote]

By incentivizing public full/light nodes with transaction fees as described in the beginning. This way the market forces will keep Infura type businesses out of monopolizing (and centralizing) the p2p layer and ensure QoS for end users.

-------------------------

Nostromo | 2023-12-06 13:38:36 UTC | #38

> By incentivizing public full/light nodes with transaction fees as described in the beginning

That's definitely a very interesting idea. How would the incentive be distributed? Would the transaction fee go directly to the node?

-------------------------

0x3639 | 2023-12-06 13:41:09 UTC | #39

[quote="Nostromo, post:33, topic:253"]
However, in order to prevent denial of service attacks, the queries can require a fee that needs to be applied in order to return a valid response: for example, a user can use the sentinel nodes for querying the state of the ledger or sentry nodes to get updates regarding its account chain.
[/quote]

In this context, do you think a “fee” represents PoW, Plasma, and/or a fee paid.  Maybe you read our discussion on Dynamic Plasma and the extended discussion on fees. 

if this includes a fee paid, how do we reconcile that with our marketing efforts of a “feeless” L1?

-------------------------

Nostromo | 2023-12-06 13:43:45 UTC | #40

Yeah I think the fee in this context is plasma, as it prevents the denial service attacks.

-------------------------

0x3639 | 2023-12-06 14:01:26 UTC | #41

[quote="Nostromo, post:36, topic:253"]
In my perhaps idealized view, a Sentry could be so lightweight that it could be incorporated into nearly every type of client, partially eliminating the need for infrastructure providers as every user would have their ‘embedded node’ serving as a gateway to the network.
[/quote]

If these Sentry nodes existed though the IBD concepts Kaine discussed in TG, why do users need access to  full nodes?  As questioned here, how do users know which node to select?  Why create a new incentive for full nodes if a user can download and confirm their ledger and access the network with a 2” IBD.

Maybe no one is thinking about Sentry nodes because there is very little about them in the WP and they are mostly dismissed.  

If I understand this concept correctly, users only need a Sentry to make TXs.  And if the Sentry existed, why would a user ever need to query a Sentinel?

-------------------------

0x3639 | 2023-12-06 13:56:38 UTC | #42

Kaine or someone posted links to BTC IBDs that can be run in a browser take 2 seconds to verify .

-------------------------

Nostromo | 2023-12-06 14:10:36 UTC | #43

>If these Sentry nodes existed though the IBD concepts Kaine discussed in TG, why do user need full nodes? As questioned here, how do users know which node to select? Why create a new incentive for full nodes if a user can download and confirm their ledger and access the network with a 2” IBD.

Yes, if it were possible this way, it would seem preferable in my view and arguably more decentralized.

>  if the Sentry existed, why would a user ever need to query a Sentinel?

I would think that maybe the Sentry would query the Sentinel on behalf of the user for certain things, the IBD being one of them.

Curiously I just looked up the classical definitions for Sentinel and Sentry 
A Sentinel is somebody that stands guard and keeps watch.
A Sentry is somebody that keeps guard and controls access to a place.

-------------------------

0x3639 | 2023-12-06 14:12:26 UTC | #44

[quote="Nostromo, post:43, topic:253"]
I would that maybe the Sentry would query the Sentinel on half of the user for certain things, the IBD being one ot them.
[/quote]

Makes sense.  How does a Sentry know which Sentinel to query for the IBD or can that be handled on a P2P layer where it’s randomized.   I’m looking for that BTC IBD website.  

Found these.  Messages from Kaine on TG seem to align with your thoughts here

![IMG_1272|690x272](upload://r30OQTggilkipMVWa2LEzvacz3M.jpeg)
![IMG_1273|325x500](upload://ulqU56Q7DmK0s4BLXFUJzsjOwyz.jpeg)

-------------------------

0x3639 | 2023-12-06 14:15:42 UTC | #45

Found it https://zerosync.org/demo/

-------------------------

Nostromo | 2023-12-06 14:21:48 UTC | #46

> How does a Sentry know which Sentinel to query for the IBD

I assume that, since all the Sentinels have the same version of the ledgers due to being in consensus, any Sentry could acquire it from any of them. I'm not sure about the protocol's method for selecting the Sentinel; randomization seems like a good approach.

-------------------------

aliencoder | 2023-12-06 16:16:32 UTC | #47

[quote="Nostromo, post:38, topic:253"]
How would the incentive be distributed?
[/quote]

Check [this](https://forum.hypercore.one/t/the-p2p-revolution-pow-links-reloaded/248/4).

[quote="0x3639, post:39, topic:253"]
if this includes a fee paid, how do we reconcile that with our marketing efforts of a “feeless” L1?
[/quote]

Feeless paradigm => Plasma paradigm (credits to @Zyler)

[quote="0x3639, post:41, topic:253"]
why do users need access to full nodes?
[/quote]

Not every user will be able to run a (public) full node. Even if it's the lightest node possible. That's why we have the Sentry concept. 

In my opinion a public (full) node is a Sentry.

[quote="0x3639, post:41, topic:253"]
Why create a new incentive for full nodes if a user can download and confirm their ledger and access the network with a 2” IBD.
[/quote]

Because we also need public nodes. And again, not every client will be able to run a node.

-------------------------

0x3639 | 2023-12-06 16:32:11 UTC | #48

[quote="aliencoder, post:47, topic:253"]
In my opinion a public (full) node is a Sentry.
[/quote]

Kaine talks about solving the IBD issue in Phase I.  He has been talking about that over and over. @aliencoder where does your Roadmap address IBDs?  My guess is that solving the IBD issue is more than just allowing public nodes to sync fast.  The idea of running an embedded Sentry in any device is appealing. It could serve as the entry point to the network for individual users.   Why rely on another public node when you can rely on yourself? 

Why can’t something like zerosync be used to run a Sentry node on any device that syncs in 2 seconds. Or Helios from A16Z - a light client that can sync and verify an RPC in seconds.  

I dont think a Sentry is defined as a public node in the whitepaper.  @Nostromo references the relevant sections of the whitepaper above.

@aliencoder take a look on TG and search for IBD and kaine.

-------------------------

Stark | 2023-12-06 19:20:21 UTC | #49

[quote="Nostromo, post:43, topic:253"]
A Sentinel is somebody that stands guard and keeps watch.
A Sentry is somebody that keeps guard and controls access to a place.
[/quote]

The definitions are probably meaningful. Same as your finding, just different wording: 

A sentinel is a lookout, a watchman on the city wall who sounds alarm.
Sentries are guards, boots on the ground.

-------------------------

aliencoder | 2023-12-06 20:29:52 UTC | #50

[quote="0x3639, post:48, topic:253"]
The idea of running an embedded Sentry in any device is appealing
[/quote]

I agree. We should have a light client design. And I have some ideas, but I'll share them after we have on-chain PoW and the anchoring of the consensus that I've talked about. We have many things to accomplish until then.

[quote="0x3639, post:48, topic:253"]
Why rely on another public node when you can rely on yourself?

Why can’t something like zerosync be used to run a Sentry node on any device that syncs in 2 seconds. Or Helios from A16Z - a light client that can sync and verify an RPC in seconds.
[/quote]

Don't get me wrong - we should have a light client like Helios. But public full nodes are not light clients. Public full nodes are the p2p infrastructure and we need proper incentivization for its maintenance.

-------------------------

Chadass | 2023-12-06 20:59:21 UTC | #51

[quote="aliencoder, post:34, topic:253"]
Again, you either don’t read my [posts](https://forum.hypercore.one/t/the-p2p-revolution-network-of-momentum-phase-1/245) or simply you ignore them. I won’t answer you anymore if you totally ignore what I say.
[/quote]

There's no discussion about growing the blocks size for BTC? There's no forks with bigger blocks ? 

[quote="aliencoder, post:34, topic:253"]
I don’t want to predict anything. If a Pillar is disassembled, we can check that and remove the undelegation fee for this particular case.
[/quote]

Pillars can set their rewards to 0 or even lower them, pushing the delegator to move, or not. Don't make it a closed market. Also, I never talked about Pillars disassembling. It seems you don't read my posts, or ignore them.

-------------------------

Chadass | 2023-12-06 20:59:00 UTC | #52

[quote="aliencoder, post:34, topic:253"]
Because we won’t have a sufficient amount of Sentinels. I’ve calculated earlier a maximum number. We need tens of thousands of public nodes for a truly decentralized network.
[/quote]


How is the incentives you're proposing sufficient for that many nodes?

-------------------------

0x3639 | 2023-12-06 21:26:24 UTC | #53

[quote="aliencoder, post:50, topic:253"]
Public full nodes are the p2p infrastructure and we need proper incentivization for its maintenance.
[/quote]

I'm not convinced the White Paper anticipates incentivized public nodes beyond Sentinels and introducing a completely new incentivized pubic node that was not originally anticipated will be difficult and maybe impossible to get consensus on.

-------------------------

0x3639 | 2023-12-06 21:34:06 UTC | #54

![Screenshot 2023-12-06 at 3.33.35 PM|399x500](upload://4W5y8qr9csO4rbXqBjny1ypvzdv.png)

-------------------------

0x3639 | 2023-12-06 21:37:10 UTC | #55

![Screenshot 2023-12-06 at 3.32.36 PM|690x337](upload://flgGUkMvCYvptuJb3jIMj8NK654.png)
![Screenshot 2023-12-06 at 3.31.34 PM|550x500](upload://nnStF042EUt4oeM5CVwNE6MMU2K.png)
![Screenshot 2023-12-06 at 3.30.38 PM|690x221](upload://vsFjdAPIPQHcbt9LabkaQMc2Jrn.png)
![Screenshot 2023-12-06 at 3.30.23 PM|690x276](upload://5Jtp6qZBq8jCGTXi6QpG5RrCJYo.png)
![Screenshot 2023-12-06 at 3.30.04 PM|690x140](upload://vSi0sIkSQqtk9aIxAevpicpYRYg.png)
![Screenshot 2023-12-06 at 3.29.47 PM|690x175](upload://bIskHQRqr5V3Ruh1wqfjMmAQLwL.png)
![Screenshot 2023-12-06 at 3.28.21 PM|690x182](upload://8j1m0x9BJ5C1HsGtHfnFiLfSdCO.png)

-------------------------

aliencoder | 2023-12-06 22:19:38 UTC | #56

[quote="Chadass, post:51, topic:253"]
There’s no discussion about growing the blocks size for BTC? There’s no forks with bigger blocks ?
[/quote]

There was a lot of discussion and one solution emerged victorious. A rational solution.

[quote="Chadass, post:51, topic:253"]
Pillars can set their rewards to 0 or even lower them, pushing the delegator to move, or not.
[/quote]

Here I agree with you. We need to take this into account: setting the reward percentage as a Pillar will burn 100 ZNN, so Pillars will also think twice before enforcing a new payout scheme.

[quote="Chadass, post:51, topic:253"]
Don’t make it a closed market
[/quote]

How is the market closed? I want a free market more than anyone.

[quote="Chadass, post:51, topic:253"]
Also, I never talked about Pillars disassembling.
[/quote]

[quote="Chadass, post:23, topic:253"]
going offline
[/quote]

Going offline can also mean disassembling. If you meant that Pillars go offline aka they're not producing momentums, delegators should think twice before supporting such a Pillar.

[quote="Chadass, post:52, topic:253"]
How is the incentives you’re proposing sufficient for that many nodes?
[/quote]

[quote="aliencoder, post:3, topic:253"]
[quote="Chadass, post:2, topic:253"]
How does the fee solve the public nodes incentives problem?
[/quote]

Check my [previous post ](https://forum.hypercore.one/t/the-p2p-revolution-pow-links-reloaded/248).
[/quote]

[quote="0x3639, post:53, topic:253"]
introducing a completely new incentivized pubic node that was not originally anticipated will be difficult and maybe impossible to get consensus on.
[/quote]

SegWit was approved with 95% hashrate and at the time *was* [controversial](https://bitcoinmagazine.com/technical/the-long-road-to-segwit-how-bitcoins-biggest-protocol-upgrade-became-reality).

We should think with an open mind. May the best solution win.

-------------------------

0x3639 | 2023-12-07 10:00:42 UTC | #57

Our new inquisitor has raised some good questions.

---
FROM ABOVE

The cost to launch a Sentinel is crucial as it protects from economic attacks, it makes it very difficult for an attacker to launch 100 Sentinels at once, for example.

A large benefit for prospective operators is that the cost is redeemable when a Sentinel is revoked, making a Sentinel profitable after the first day (In ZNN & QSR scope).

The central question is whether the goal is to have many Sentinels, how many are considered enough? It is not immediately obvious that more equals better.

Bitcoin, which I just looked up, has an estimated 13 thousand full nodes in the network. They help create consensus, where the longest chain is what individual nodes accept as the valid version of the blockchain. At least that’s how I understand it.

However, we don’t have that design. Our Pillars agree on what the valid version of the blockchain is. As far as I can tell, our full nodes serve as a medium for the transactional layer, which is separated from the consensus layer.

So, in that sense, the question remains: how many Sentinels does one need for network stability?

The cost to launch a Sentinel is crucial as it protects from economic attacks, it makes it very difficult for an attacker to launch 100 Sentinels at once, for example.

A large benefit for prospective operators is that the cost is redeemable when a Sentinel is revoked, making a Sentinel profitable after the first day (In ZNN & QSR scope).

---

I don't think we know many more Sentinels are "better".  Everything I read in the whitepaper and in telegram points to Sentinels, not public nodes, acting as a means for IDB on a "light client" or Sentry.  Kaine was designing solutions to current problems in crypto.  Central public nodes are a problem.  He devised a solution. 

Client > Sentry > Sentinel

Why introduce a new incentivized public node that replicates the problems we already have today in crypto?  If pillars keep consensus, why do more public nodes provide more security?  The nodes are just an entry point to the network (I think).

I cannot find a reference anywhere to an incentivized public node other than to a sentinel.  Sentinels and pillars keep the full ledger and are incentivized to do so.

-------------------------

Zyler | 2023-12-07 06:17:45 UTC | #58

Just to follow up, I'm saying "Plasma Paradigm" is better than "Feeless Paradigm" regardless of whether ZNN fees are added or not.
Feeless = inaccurate, because to the user it is not feeless. Initial token cost of qsr or electricity/hardware for PoW. It also sounds scammy and makes a percentage of people instantly skeptical as it's "too good to be true", which is technically the case tbh.
Plasma = interesting and it's accurate. They can learn about it and then find out that QSR doesn't spend, just locks for time ... so from a network perspective there is a feeless lane.

We won't lose any existing holders, there's only cultists left anyway. And it's better going forwards. But hey, we're leaderless, so say whatever you want. But I'll be referring to plasma paradigm and I will encourage others to do the same

-------------------------

aliencoder | 2023-12-07 17:23:49 UTC | #59

[quote="0x3639, post:57, topic:253"]
They help create consensus, where the longest chain is what individual nodes accept as the valid version of the blockchain. At least that’s how I understand it.
[/quote]

Exactly. They represent the balancing of powers within Bitcoin. Miners, full nodes and users (devs and regular users) all have equal powers.

[quote="0x3639, post:57, topic:253"]
Our Pillars agree on what the valid version of the blockchain is. As far as I can tell, our full nodes serve as a medium for the transactional layer, which is separated from the consensus layer.
[/quote]

Yes, but Pillars are not alone: we have regular users that add PoW to the ledger.

We will also have miners (same but with more hashpower than regular users), Sentinels that craft the PoW links (with their own set of miners) and full nodes/Sentries (or a lighter version) that should store the transactional ledger that is the heaviest (similar to longest chain of most accumulated PoW).

[quote="0x3639, post:57, topic:253"]
Kaine was designing solutions to current problems in crypto
[/quote]

And he also was in favor of incentivizing the p2p layer.

I'll think more about it and come up with my proposal regarding Sentries and full nodes.

-------------------------

Nostromo | 2023-12-07 23:53:53 UTC | #60

I've been revisiting the lite paper, and it's fascinating to see how the design has evolved and the functions of Sentries and Sentinels have changed.

In the lite paper, it appears that the initial paradigm was to create an asynchronous sharded network, as sharding was at the forefront of network scaling in 2017. The role of Sentinels was to facilitate inter-sharding communication and validate the integrity of shards.

A Sentry was meant to participate in the pre-approval process of transactions, presumably validating transaction formats and signatures. It needed to provide confiscatable capital to penalize dishonest behavior.

Originally, it seems like a Sentry was a more traditional type of full node, and the Sentinel was modified to be more of a meta node dedicated to the coherence and communication of shard space.

Interestingly, the lite paper also discusses fairness principles that resonate throughout all permutations of the protocol:

1. Fairness of access
2. Fairness of ordering
3. Fairness of timestamping

As we move along the timeline and get to the white paper, it seems that the sharding paradigm shifted, and a block lattice structure was selected for the transactional layer. From my limited understanding, a block lattice is far superior in terms of asynchronous behavior than sharding.

From the white paper: "Every user has its own autonomous account chain that can be updated independently from the rest. The blocks from different account chains acknowledge each other and collectively form a mesh-like structure. Because the account chains can grow concurrently, the throughput can be quickly scaled up. The block lattice has many advantages - scalability, simplicity, and it can be secure provided it is implemented with an adequate consensus algorithm. We have separated the ledger architecture to achieve better complexity and faster processing times when a user wants to query nodes for transactional data."

With the move away from sharding and into the Block Lattice - Meta DAG paradigm, the roles for Sentries and Sentinels also changed. Sentinels are no longer needed for shard integrity but now seem responsible for the source of transactional truth and lattice integrity and transaction routing.

It also seems that the properties of the Sentry and Sentinel in the lite paper are mostly consolidated into the Sentinel of the white paper. The Sentry has evolved into a trusted node.

Another interesting area of the lite paper is where they talk about digital signatures and using Ed25519 over ECDSA.

I'm not sure what NoM currently uses, but the lite-paper states that an Intel Xeon E5620 2.4Ghz CPU can validate ~100K key pairs per second. I assume that current-day CPUs can significantly increase that number. The point being that if we can expect higher-end hardware from a full node Sentinel, they should be able to process a very large number of transactions.

-------------------------

Nostromo | 2023-12-08 00:39:03 UTC | #61

By the by, having a hardware target also seems crucial to get the most out of dynamic plasma.

-------------------------

0x3639 | 2023-12-08 19:30:58 UTC | #62

I think this is the version you are referring to.  It's not in the main repo.  @Nostromo are you looking at the Revised 5/28/18?  Maybe I will submit a PR to add to the repo.  

https://www.allcryptowhitepapers.com/wp-content/uploads/2019/07/lightpaper.pdf

-------------------------

Nostromo | 2023-12-10 11:26:32 UTC | #63


 /* edit 
I moved this post into a new thread.
Check out the Gravity Wallet thread for details.

https://forum.hypercore.one/t/gravity-wallet/

-------------------------

Shazz | 2023-12-10 08:59:45 UTC | #64

This is an excellent proposal. And once we have zBTC https://twitter.com/cryptocheshire/status/1733572567774941593?t=dNH0ZHKy-5IRlKifjZ4sSg&s=19 feeless btc transactions can be done as well. We can also position the wallet as an alternative to LN...

Agree with the points re: secondary markets for qsr and IBD. The main vonstraint here is to establish a market for native zts (rather than wrapped) which can be achieved with a CEX listing or our own dex. 

The IBD challenge is quite high prio for some of our devs afaik

-------------------------

aliencoder | 2023-12-31 11:36:08 UTC | #65

I want to map all actions (either active or passive) that will be performed on NoM Phase 1:

## User
- Fuse
- Unfuse
- Generate (initial) PoW for Plasma
- ZTS token issuance
- Transfer ZTS without extra data
- Transfer ZTS with extra data
- Create AZ project
- Create AZ phase
- Vote for AZ project
- Vote for AZ phase

## Delegator
- Delegate
- Undelegate

## Staker
- Stake
- Unstake

## Sentinel
- Deploy Sentinel
- Revoke Sentinel

## Pillar
- Deploy Pillar
- Revoke Pillar
- Pillar change reward percentages
- Pillar change rewards address
- Pillar change producer address

## Full node
- Relay transaction
- Initial blockchain download (IBD) sync

## Miner
- PoW links creation (merge-mining CPU-friendly PoW)
- Merge-mining Bitcoin (merge-mining ASIC-friendly PoW)

## Liquidity provider
- Stake LP token
- Unstake LP token

-------------------------

0x3639 | 2023-12-29 17:05:51 UTC | #66

are these new actions?  Looks like we have some today?  Like:

- Stake
- Unstake

-------------------------

aliencoder | 2023-12-29 17:11:44 UTC | #67

[quote="0x3639, post:66, topic:253"]
are these new actions?
[/quote]

All actions combined (Phase 0 and Phase 1). We need those to be able to determine how current and future incentives/disincentives might work.

For example, we have a disincentive for revoking Pillars (QSR required for the Pillar slot are burned).

I've suggested we have a disincentive for unfusing QSR (burn) and undelegating ZNN (burn).

-------------------------

coinselor | 2023-12-29 17:49:53 UTC | #68

missing:

* Pillar change producer address

-------------------------

VTO | 2023-12-30 10:30:51 UTC | #69

[quote="aliencoder, post:67, topic:253"]
I’ve suggested we have a disincentive for unfusing QSR (burn) and undelegating ZNN (burn).
[/quote]

:-1:

-------------------------

aliencoder | 2023-12-31 11:38:12 UTC | #70

[quote="aliencoder, post:65, topic:253"]
I want to map all actions
[/quote]

Added LP actions. 

Thanks @coinselor for the missing Pillar action.

[quote="VTO, post:69, topic:253"]
:-1:
[/quote]

I know it's unpopular, but here are the arguments:
- Unfusing disincentive is necessary to deter a spam attack on the QSR lane.
- Undelegating disincentive is necessary to deter delegate hopping. It is very similar to [pool hopping](https://bitcoin.stackexchange.com/questions/5072/what-is-pool-hopping) that can be seen in the Bitcoin mining industry. 

Currently delegators and Sentinels have no responsibilities. This must change in NoM Phase 1 if we want to transition to a self-sustainable network.

-------------------------

Stark | 2023-12-31 21:11:56 UTC | #71

[quote="aliencoder, post:70, topic:253"]
Unfusing disincentive is necessary to deter a spam attack on the QSR lane.
[/quote]

Would a QSR lockup period accomplish the desired outcome?

[quote="aliencoder, post:70, topic:253"]
Undelegating disincentive is necessary to deter delegate hopping.
[/quote]

Would a minimum delegation period accomplish the desired outcome?

-------------------------

coinselor | 2024-01-01 07:56:28 UTC | #72

Interesting fact about pool hopping, I was unaware of the concept. 

Are you saying we can mathematically increase our delegation APR by algorithmically changing pillars currently as an exploit to how momentums are produced (not just hopping to highgest paying APR and accounting for weight increase)? Or do you envision this being a problem specifically when merge-mining shares are implemented?

-------------------------

aliencoder | 2024-01-05 08:10:47 UTC | #73

[quote="Stark, post:71, topic:253"]
Would a QSR lockup period accomplish the desired outcome?
[/quote]

QSR already has a predefined lockup period. This alone won't deter spammer. What deters a rational participant is economic punishment. 

We can build a [gaussian function](https://www.researchgate.net/profile/Jan-Bender-2/publication/344261032/figure/fig1/AS:936230099357696@1600226058151/Gaussian-bell-function-normal-distribution-N-0-s-2-with-varying-variance-s-2-For.png): maximum throughput can be achieved only after a certain amount of time has passed and not indefinitely after that. Unfusing having a cost will also deter rational attackers because they will need to refuse the QSR to get maximum throughput again.

[quote="Stark, post:71, topic:253"]
Would a minimum delegation period accomplish the desired outcome?
[/quote]

This won't prevent hopping, just delay it. 

[quote="coinselor, post:72, topic:253"]
Are you saying we can mathematically increase our delegation APR by algorithmically changing pillars currently as an exploit to how momentums are produced
[/quote]

Yes. You can exploit the system right now if you have a proper script.

[quote="coinselor, post:72, topic:253"]
Or do you envision this being a problem specifically when merge-mining shares are implemented?
[/quote]

Delegators are not miners. But the concept is similar: they delegate stake to Pillars (proxy staking) in the same way miners are pointing hashpower to mining pools (proxy mining). The problem is that delegators are not expending physical resources in the same way miners do.

-------------------------

Stark | 2024-01-05 15:42:08 UTC | #74

[quote="aliencoder, post:73, topic:253"]
This won’t prevent hopping, just delay it.
[/quote]

I see what you mean.

It seems like when it comes to delegation hopping, frequency-of-hop is a key factor. Setting an undelegation assessment on a time curve would negate the benefit of hopping. The longer a person stays the delegated to one pillar, the less benefit they might gain by strategically hopping, right? If correct, the fee could be a percentage that reduces over time. 

[quote="aliencoder, post:73, topic:253"]
What deters a rational participant is economic punishment.
[/quote]

I don't think we want to deter rational participation. We just want to ensure that the network can operate within the maximum defined parameters. With that, nobody needs to be punished.

Bitcoin has no punishment system in the protocol. The protocol has parameters which require the very same resources to cheat, as to use the network as intended. Simplicity and an economy of natural cost vs benefit. 

*Zenon security is based on value and incentive.*
![Screen Shot 2024-01-05 at 10.36.36 AM|600x362, 50%](upload://1nk8PR69upLgiStKPS7I2aojR7r.png)

-------------------------

aliencoder | 2024-01-09 10:06:12 UTC | #75

[quote="Stark, post:74, topic:253"]
I don’t think we want to deter rational participation. We just want to ensure that the network can operate within the maximum defined parameters. With that, nobody needs to be punished.
[/quote]

We want to deter spam and other types of attacks that harm the network.

[quote="Stark, post:74, topic:253"]
Bitcoin has no punishment system in the protocol. The protocol has parameters which require the very same resources to cheat, as to use the network as intended. Simplicity and an economy of natural cost vs benefit.
[/quote]

Bitcoin has punishment in the physical world: your miner costs money and consumes electricity. If you are mining a fork, you waste resources.

-------------------------

0x3639 | 2024-02-13 14:10:49 UTC | #76

@aliencoder I hope you don't mind if I reuse some of this language in the roadmap post.

-------------------------

aliencoder | 2024-02-13 17:09:31 UTC | #77

Not at all, if you need further clarifications dm me.

-------------------------

