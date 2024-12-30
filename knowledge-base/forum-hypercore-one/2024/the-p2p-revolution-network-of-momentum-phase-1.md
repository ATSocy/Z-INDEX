Thread: the-p2p-revolution-network-of-momentum-phase-1
aliencoder | 2023-11-27 21:27:07 UTC | #1

**Objective: Deliver Network of Momentum Phase 1**

Our current objective is to transition to NoM Phase 1. We have a basic list of things we need to do in order to successfully deliver Phase 1. I'm here to expand this list and provide some missing pieces of the puzzle.

**Missing links**

* Network incentives
* Peer-to-peer layer
* PoW links
* Dynamic Plasma

I've started this list with the network incentives point because it is the backbone of a decentralized network. This is the reason why Bitcoin still exists today and will exist in the future as well. I'll be quoting the original whitepaper to support my views. I'll use the whitepaper as a reference point and adapt it to our current realities.

> "In order for the network to function properly, a cryptoeconomic layer will be put in place for all network participants."

Bitcoin is a peer-to-peer cash system that runs on a decentralized network of (full) nodes that are maintained and operated by volunteers. During the Block Size Wars, there was an ongoing debate to sacrifice decentralization for better scalability. The wars ended with irrelevant forks appearing and disappearing and Bitcoin surviving and thriving ever since. It survived because it chose the path of small blocks to safeguard the peer to peer network.

Small blocks represent the trade-off made to preserve the status-quo of the current peer-to-peer network that relies on volunteers around to world to operate and maintain it. If the size of the blocks were to be raised back in 2017, the volunteer based p2p network would have crumbled and killed one of the most important properties of Bitcoin: decentralization.

Why? Because running a node in Bitcoin is purely based a voluntary decision. Miners are engaged in the hashing competition, not running decentralized infrastructure. Many blockchains made the fatal mistake to scale too early, putting immense pressure on their underlying, volunteer based peer to peer networks. This totally compromised decentralization in favor of scaling. How many of you can run a Solana or a BNB Chain full node?

> "... a novel anti-sybil and anti-spam mechanism called proof of work links that will enhance connectivity within the network and limit certain attacks by sharing their commitment and contributing resources for routing and efficient data delivery."

Luckily, this mistake was avoided by Zenon by imposing a hard cap for transaction throughput. We still have a chance to get it right. That's why we need to create strong incentives for a thriving peer-to-peer network layer.

Now let's see how and why a hybrid system will prevail, where feeless transactions will coexist with fee based transactions.

> "The sentinel nodes will benefit from the fees by consuming them in order to compute the PoW links."

In a healthy peer to peer network that aims for decentralization, participants are incentivized to run full nodes. That is exactly the reason why Syrius wallet features an embedded full node. Every one of you running a full node is great for decentralization and self-sovereignty, but without enough public nodes, we saw how the p2p network struggled to serve new users entering into the ecosystem. If there are no incentives to run full nodes, free riding issues will arise and the peer to peer network will eventually collapse. Bitcoin avoided this by hard capping the block size, but NoM is designed to scale Bitcoin, so we can't afford this cap indefinitely.

Therefore, fee based incentives are mandatory for the provisioning of the peer to peer layer. Moreover, users should have all the options to transact the way they want to. Even the whitepaper embraces fees in order to deter denial of service attacks and incur a cost for the attacker:

> "... adding a transaction fee, which means that the attacker will make the sentinels unavailable at the cost of investing resources in the system, which is a positive aspect for the network and a negative one for the attacker, taking into account that the consensus is unaffected."

In my opinion, the following hybrid system will emerge for NoM Phase 1:

* Feeless transactions
  * Supply PoW
  * Fuse QSR
* Fee based transactions
  * Supply ZNN
  * Burn ZNN

To be continued ...

-------------------------

Chadass | 2023-11-27 23:10:24 UTC | #2

Nice post but I still think you're overstretching your fee views out of ideology. Plasma abstract the fee away but they still exist in the form of QSR (token cost) and PoW (electricity cost). I fail to see why we should sacrifice one of the core of the NoM in the sake of abritrary non benchmarked views.

-------------------------

Zyler | 2023-11-28 05:08:37 UTC | #3

Have some prawn dumplings, you're not you when you're hangry

-------------------------

Zyler | 2023-11-28 05:34:22 UTC | #4

From what you're saying, we need to incentivise people to run full nodes/public nodes to allow NoM to indefinitely scale Bitcoin's indeterminate growth? I see you talking about sentinels ... I think we should hear the fully fleshed out argument before deciding. 

I kind of agree with chadass. We already have fees in the form of electricity/qsr. I'm concerned because last I heard the NoM devs were quite divided on this, but I guess that's why you're elaborating on the case for fees ...

-------------------------

0x3639 | 2023-11-28 11:06:44 UTC | #5

I'm reading the white paper again.  I do think some sections of the white paper refer to a "fee" as PoW performed or Plasma fused by the user.  

However, there are other sections of the paper that I believe refer to a "fee" as something different than generating plasma.  For example, this section on page 9.  This refers to incentivized nodes.  

We all know running nodes is costly.  And those who run them are centralizing forces.  But if the network was designed to incentivize running nodes through fees, we can change that.

>  However, in order to prevent denial of service attacks, the queries can require a fee that needs to be applied in order to return a valid response: for example, a user can use the sentinel nodes for querying the state of the ledger or sentry nodes to get updates regarding its account chain.

![Screenshot 2023-11-28 at 4.48.36 AM|690x389](upload://iieW6puaplOjJof0IeeD9sN9xez.png)

![Screenshot 2023-11-28 at 5.05.48 AM|690x129](upload://2abozlZ8RnpS2K60fBrqmuSiH4w.png)


I could not find anything in particular from Kaine on this topic in TG, except for this.  

![Screenshot 2023-11-27 at 7.26.59 PM|690x213](upload://vGq1pDMQ1tPAYtJ3uB0hbIsKVrl.png)

-------------------------

0x3639 | 2023-11-28 11:20:42 UTC | #6

Take a look at the white paper again with an open mind.  I think ensuring feeless transactions is very important, critical.  

There are several discussions in the white paper that seem to refer to fees as something other than fused plasma.  Specifically related to Sentinels in order to incentivize nodes. Aliens arguments are correct about BTC and the block wars.  Had they increased block size fewer people would be running full nodes.

NoM hopes to scale BTC.  We will need to uncap our limits.  How do we do that while ensuring decentralization and participation?  We need to incentivize participants to run full nodes (sentinels).  Pillars and Sentinels are the only players that have both chains.

We don't want people querying Pillars and eventually it will be costly and centralized for a few individuals to run public nodes as we scale.   

Solution > Incentive sentinels to run the full node and allow them to be searched.  I don't know how this "fee" relates to the emissions given to Sentinels for performing their job.  

Is the fee discussed in the white paper a new fee, or does it refer to the emissions paid to Sentinels to do their job?

-------------------------

Chadass | 2023-11-28 13:56:52 UTC | #7

I think Vilkris proposal makes sense and should be investigated for real rather than coming back with another big stretch in order to make the network lessfee.

-------------------------

aliencoder | 2023-11-28 18:23:41 UTC | #8

[quote="Zyler, post:4, topic:245"]
we need to incentivise people to run full nodes/public nodes to allow NoM to indefinitely scale Bitcoin’s indeterminate growth
[/quote]

We need to incentivize the public infrastructure with fees paid by users. Users are able to opt out of the fee lane. It is not mandatory to pay fees. 

Bitcoin sacrificed scaling for decentralization such that everyone can run Bitcoin Core on their Raspberry Pi with a modest internet connection.

If we want to scale, we need a strong (if you make money you also afford better hardware, etc) p2p layer that doesn't rely on volunteers. So far my point is valid: only @0x3639 and a few other community members run public infrastructure for NoM. This isn't sustainable in the long term. 


[quote="0x3639, post:6, topic:245"]
Specifically related to Sentinels in order to incentivize nodes
[/quote]

Sentinels are already rewarded by the protocol with rewards. Public nodes that service users are not. Full nodes must be incentivized.

[quote="0x3639, post:6, topic:245"]
We need to incentivize participants to run full nodes (sentinels).
[/quote]

Sentinels are a special kind of full node that create PoW links and are already incentivized by protocol rewards. Full nodes on the other hand are public nodes that participate in the p2p network and are not incentivized at all. That's why 99% of people in crypto don't run public infrastructure (except Bitcoiners), despite benefitting from it (censorship resistant p2p payments).

[quote="0x3639, post:6, topic:245"]
Is the fee discussed in the white paper a new fee, or does it refer to the emissions paid to Sentinels to do their job?
[/quote]

There is some ambiguity regarding this, but whoever wrote this whitepaper *knows* that incentivizing the peer to peer layer with fees is critical in maintaining decentralization. 

Therefore, implementing a hybrid system satisfies all the conditions presented in the whitepaper. Moreover, Mr Kaine specifically wrote that he is in favor of "incentivizing network decentralization at p2p layer".

@Chadass please come up with arguments if you want to participate in the discussion. I don't think you fully understand the implications for the long term sustainability of the network.

-------------------------

Chadass | 2023-11-28 19:54:52 UTC | #9

[quote="aliencoder, post:8, topic:245"]
please come up with arguments if you want to participate in the discussion. I don’t think you fully understand the implications for the long term sustainability of the network.
[/quote]

I came with argument numerous times, including here, you came with ideology and rephrasing your point over and over.

My main point is the following: how abstracting the fee with plasma through QSR and PoW offers less security and scalability / robustness than using native tokens as fee. Both comes with a cost that mitigate spam and attacks, however the later is a bandaid. I'm not the only one saying that. 

Beside and those are your words from another post on this forum: "we don't have the manpower to implement the feeless route" which means you're willing to go for a "good enough" idea which poorly mimick others. You never answered this one, and that's a pretty big one. You might be more technical than anyone of us, but after you wrote that, you can't keep talking about long term implication. The decision we will take right now will indeed have long term implication, I don't think you fully understand that. You can't keep ignoring whatever doesn't fit your narrative. 

Lastly, you talk about incentives for public nodes. Okay good, but do you genuinely think the fee will work here? We have already rewards for Sentinels, Pillars and stakers, a part of that could go to public nodes and that would be much more effective. 0.000003 ZNN per tx will incentive what? Nobody will run public nodes for a fraction of a cent per month. Imagining QSR would apreciate just because of that is a stretch.

Maybe you just want more funding?

![image|690x191](upload://5YurfAVcS8DTp3rot1Kjo6TPv0C.jpeg)

-------------------------

Stark | 2023-11-28 19:58:04 UTC | #10

@aliencoder - given unlimited resources, can you envision / describe a feeless solution?

-------------------------

0x3639 | 2023-11-28 20:06:30 UTC | #11

[quote="aliencoder, post:8, topic:245"]
Sentinels are a special kind of full node that create PoW links and are already incentivized by protocol rewards. Full nodes on the other hand are public nodes that participate in the p2p network and are not incentivized at all.
[/quote]

I'll read the white paper again.  Does it distinguish between Sentinels and full nodes? I was thinking Sentinels are the full nodes, but maybe I'm confused.

Some are discussing using the bridge fee with the [extraData](https://github.com/MoonBaZZe/go-zenon/tree/extraData)  rpc endpoint as a way to incentivize nodes.  I personally do not think that is sustainable.  I think the incentivization needs to live within our ecosystem.  

Why can't Sentinels act as full nodes open to the public and they receive their incentivization through protocol emissions?

-------------------------

aliencoder | 2023-11-28 23:04:24 UTC | #12

[quote="Chadass, post:9, topic:245"]
how abstracting the fee with plasma through QSR and PoW offers less security and scalability / robustness than using native tokens as fee
[/quote]

Native token as fee equals utility. Whether you want to admit it or not, this is the case. And again, I don't want to replace PoW or QSR fusing.

[quote="Chadass, post:9, topic:245"]
we don’t have the manpower to implement the feeless route
[/quote]

Can you post a screenshot where I say this?

[quote="Chadass, post:9, topic:245"]
You can’t keep ignoring whatever doesn’t fit your narrative.
[/quote]

I don't have a narrative. I have plans to make this network sustainable in the long run.

[quote="Chadass, post:9, topic:245"]
Nobody will run public nodes for a fraction of a cent per month.
[/quote]

I agree. That's why we can compute a rough estimate:

Let's say the network will be able to process 100 TPS and momentums will be at 10% capacity on average => 864000 transactions settled daily
Let's assume an average fee of 0.02 ZNN per tx (for the fee lane) and that 33% of all transactions are on the fee lane => 5760 ZNN daily for incentivizing public nodes.

FYI current ZNN daily emission is 4320 ZNN that is divided between all network participants (all Pillars, Sentinels, stakers, delegators). Public full nodes will be able to earn much more, creating a market around servicing users. We should also burn a fraction of those fees in order to achieve equilibrium for ZNN.

The numbers are conservative and we can make more accurate simulations, but you get the point.

[quote="Chadass, post:9, topic:245"]
Maybe you just want more funding?
[/quote]

I don't seek funding. I seek a comprehensive solution.

[quote="Stark, post:10, topic:245, full:true"]
@aliencoder - given unlimited resources, can you envision / describe a feeless solution?
[/quote]

This is a cryptoeconomic problem, not a technical one. We can't solve everything with technical solutions. Bitcoin is amazing because it managed to solve economic and technical problems at the same time.

[quote="0x3639, post:11, topic:245"]
Does it distinguish between Sentinels and full nodes?
[/quote]

Yes. Sentinels create PoW links. Full nodes *can* be Sentinel nodes *if* they lock collateral. The backbone of the peer-to-peer network are full nodes. Not your node, not your rules.

[quote="0x3639, post:11, topic:245"]
I personally do not think that is sustainable
[/quote]

It's an amazing first step in the right direction. But not enough.

[quote="0x3639, post:11, topic:245"]
Why can’t Sentinels act as full nodes open to the public and they receive their incentivization through protocol emissions?
[/quote]

Sentinels need to lock collateral. You need to be heavily invested into the network to setup a Sentinel node. And Sentinels are fine, they already receive their fair share of rewards from protocol emissions.

But not everyone will have that kind of collateral in the future. The peer-to-peer layer is not incentivized and we already saw that no one except a few members will setup public nodes. This is definitely not sustainable in the long run.

-------------------------

Bzed | 2023-11-28 23:03:47 UTC | #13

Would sentinels need to be public to relay txs and attach pow links?

-------------------------

sol | 2023-11-29 06:16:37 UTC | #14

A few months ago, I made [a post](https://forum.hypercore.one/t/public-rpc-node-incentives/148) about incentivizing public nodes, in which I focus more on third-party funding mechanisms. The solutions could work but they may also not be sustainable.

I didn't take into account two other revenue streams:
- transaction fees
- protocol emissions

I'm not entirely in favor of introducing fee lanes and whatnot, but we could potentially alter emissions to pay access nodes.

Saito pays its consensus (pillar), routing (sentinel), and access nodes [[1](https://twitter.com/SaitoOfficial/status/1613496573886857224), [2](https://wiki.saito.io/consensus/attack-vectors)].

I'm envisioning a similar solution:
- pillars continue to be rewarded as they are today
- sentinels are paid per pow link
- access nodes are paid for the transactions they forward to sentinels
- sentinels and access nodes are paid from protocol emissions for their participation in confirmed transactions

Alternatively, same model except:
- sentinels are paid per pow link from emissions
- access nodes are paid by users with non-plasma transaction fees
  - users can avoid this by running their own infra or connecting to a different node

Anyways, multiple solutions to this problem. Hopefully we solve this one soon.

-------------------------

coinselor | 2023-11-29 01:25:59 UTC | #15

Couldn't we learn a thing or two from Nostr?

They have literally 0 incentives to run a Relay, yet they seem to be thriving. Is it sustainable? I don't know, but I'm sure they have had this argument before.

Maybe this is an opportunity to not only add P2P BTC merge mining into the picture, but look at how we could help Nostr too. I've seen @georgezgeorgez mention leveraging nostr as a communication protocol for stuff like markets, running our own relays would be a requirement in that case. These technologies are complementary to our grand vision. My two cents.

-------------------------

aliencoder | 2023-11-29 10:40:14 UTC | #16

[quote="sol, post:14, topic:245"]
The solutions could work but they may also not be sustainable.
[/quote]

The problem with 3rd party solutions is that they're not sustainable over long periods of time or supporting a huge user base.

[quote="sol, post:14, topic:245"]
access nodes are paid by users with non-plasma transaction fees
[/quote]

This looks like the model I'm describing. Users are not forced to pay fees if they run their own node (thus supporting the p2p layer).

[quote="sol, post:14, topic:245"]
Hopefully we solve this one soon.
[/quote]

We must solve this issue before Phase 1.

[quote="coinselor, post:15, topic:245"]
They have literally 0 incentives to run a Relay
[/quote]

They are [not a peer-to-peer](https://github.com/nostr-protocol/nostr) network: "it does not rely on P2P techniques, and therefore it works."

[quote="coinselor, post:15, topic:245"]
Is it sustainable? I don’t know, but I’m sure they have had this argument before.
[/quote]

The answers are in the [README](https://github.com/nostr-protocol/nostr).

[quote="coinselor, post:15, topic:245"]
Maybe this is an opportunity to not only add P2P BTC merge mining into the picture
[/quote]

We will add p2p merge-mining for sure, but let's first solve all remaining issues before starting the actual implementation.

[quote="coinselor, post:15, topic:245"]
These technologies are complementary
[/quote]

I also see Nostr as a complementary tech, but not at the core of our stack.

-------------------------

0x3639 | 2023-11-29 11:17:02 UTC | #17

[quote="sol, post:14, topic:245"]
Alternatively, same model except:

* sentinels are paid per pow link from emissions
* access nodes are paid by users with non-plasma transaction fees
  * users can avoid this by running their own infra or connecting to a different node

Anyways, multiple solutions to this problem. Hopefully we solve this one soon.
[/quote]

Now I'm starting to understand.  Slow learner.

Pillars > Full Node and Provide consensus and incentivized by the protocol

Sentinel > Full Node, costly to setup, their job is to relay messages and generate PoW links.  They are compensated through protocol emissions.  They are expensive to setup and "hard" to run.  It will be difficult for the general public to run them so we cannot rely on Sentinels as "Public Nodes".  There won't be enough of them.

Public Nodes > We need as many as possible to improve security and decentralization.  There is no incentive to run them today.  But users need access to them to process TXs and query the chain.  We don't want "Infura" to run them and we don't want me to run them.  We want the community to run them, like BTC.  But, our nodes might be more costly to run (for a number of reasons).  So there needs to be an incentive. 

This is where fees come in.  I don't think we want to introduce more inflation into the system and emit protocol rewards to Public Nodes.  We don't need more inflation.  Users can avoid node fees by running their own node.  But if they don't have the technical skills or desire to do that, they can just add a fee to their TX to pay for someone else's node.  That way we don't rely on Infura or me, and we have a public p2p node layer that is paid for by 3rd party fees.  

A user could avoid fees by simply syncing syrius and use the embedded node.  But if they cannot wait, they can use the public node "layer" and pay a fee.

1) Does a user select a public node from a "list" and pay a fee to them?
2) Or, is there a public node "layer" that shares in all fees received provided they are up and offering access to the network?

-------------------------

aliencoder | 2023-11-29 11:39:17 UTC | #18

[quote="0x3639, post:17, topic:245"]
There won’t be enough of them.
[/quote]

Exactly. With 5k ZNN/50k QSR we can compute a max upper limit to how many Sentinels the network can have.

[quote="0x3639, post:17, topic:245"]
There is no incentive to run them today.
[/quote]

Even in Bitcoin there are no incentives, but there is a very low entry barrier (and a "node" culture) such that the average Joe can still run a node.

[quote="0x3639, post:17, topic:245"]
A user could avoid fees by simply syncing syrius and use the embedded node.
[/quote]

I'll add that the nodes that service users must be public. But running your own node is a starting point.

[quote="0x3639, post:17, topic:245"]
* Does a user select a public node from a “list” and pay a fee to them?
[/quote]

This seems like an "UX" problem.

[quote="0x3639, post:17, topic:245"]
1. Or, is there a public node “layer” that shares in all fees received provided they are up and offering access to the network?
[/quote]

Only public full nodes that gossip (route) transactions should be incentivized. We must be able to quantify their work. 

*Sentries* are a good candidate to take this role for the network.

-------------------------

0x3639 | 2023-11-29 12:00:17 UTC | #19

With this approach we can still market NoM as feeless.  But if a user wants access to a public node and is not willing to sync syrius themself, they have an option to pay a small fee.

I think this discussion is separate from Dynamic Plasma.  Accessing a public node is different than ensuring your TX gets processed.  

1) Will users get confused by paying a fee to access a public node and then experience difficulties in getting a TX processed?  Or do you think incentivized Public Nodes and Dynamic Plasma are linked?
2) Will a user be confused by paying a fee to access a public node and also needing to generate Plasma?

-------------------------

aliencoder | 2023-11-29 15:54:46 UTC | #20

[quote="0x3639, post:19, topic:245"]
Or do you think incentivized Public Nodes and Dynamic Plasma are linked?
[/quote]

They are linked because dynamic Plasma is the system that protects the network against spam, while enhancing its operations (adding weight to the ledger via PoW, provisioning the p2p layer via fees, etc). Plasma should be generated with PoW, QSR and ZNN.

[quote="aliencoder, post:12, topic:245"]
Let’s say the network will be able to process 100 TPS and momentums will be at 10% capacity on average => 864000 transactions settled daily
Let’s assume an average fee of 0.02 ZNN per tx (for the fee lane) and that 33% of all transactions are on the fee lane => 5760 ZNN daily for incentivizing public nodes.
[/quote]

Public nodes will be incentivized only by the users that pay fees. They will compete to service users regardless, because they will see only the "plasma" field. Ideally, they won't know how that Plasma was generated. This remains an open question.

If we solve dynamic Plasma and fix the incentive problems, we can obtain all the properties required by a self-sufficient, decentralized network.

I want to highlight that only **public nodes** should be incentivized aka the ones that actually route transactions and contribute towards the peer-to-peer layer.

-------------------------

coinselor | 2023-11-29 15:57:42 UTC | #21

Apologies, forgot for a second Nostr relays act as servers, appreciate the reminder. It's worth noting though, that they are considering P2P elements for things like media storage using [bitorrent](https://github.com/lovvtide/nostr-torrent) + NIP-94. 

I'm not trying to deter the conversation from adding a cryptoeconomic incentive to the P2P layer, in fact, I think a cryptoeconomic solution is probably more robust and sustainable. 

I'm just pointing out other P2P networks that are thriving without them to look for inspiration in thinking outside the box. Another example, the [Folding@Home](https://foldingathome.org) project, aimed at understanding protein folding and assisting in medical research, also thrived on voluntary participation. It's a great example of how a P2P network can contribute to scientific advancements without a direct financial reward system.

-------------------------

aliencoder | 2023-11-29 16:04:11 UTC | #22

[quote="coinselor, post:21, topic:245"]
voluntary participation
[/quote]

Do you run a public Zenon node? How many people are running public full nodes right now?

-------------------------

sol | 2023-11-29 16:09:24 UTC | #23

48, but only two or three are primarily used by the community.

https://zenonhub.io/stats/nodes

-------------------------

vilkris | 2023-11-29 16:21:01 UTC | #24

Just dropping an idea here. Currently you can already require a user to pay a fee to publish a transaction via your node, but it would need some customizations to go-zenon and clients.

I think this should work:
1. User sends node provider two signed transactions. The first one is the actual transaction and the second one is the fee transaction going to the node provider's address.
2. Node provider verifies both transactions (checks plasma, balances etc.).
3. Node provider publishes both transactions at the same time and by doing so receives the fee.

If the user doesn't provide the fee transaction the node provider just ignores the user's request.

This would allow node providers to set whatever fees they want and request whatever ZTS they want as payment. The downside is that the user has to have enough plasma to be able to send two transactions back-to-back (or maybe the node provider allows 10/tx per payment or something). But this should be relatively easy to implement and wouldn't need protocol changes.

-------------------------

0x3639 | 2023-11-29 17:34:49 UTC | #25

I like an idea like this a lot more than relying on bridge fees.  Does not seem right to rely on an ETH bridge to fund nodes to process TXs on a different chain.

-------------------------

aliencoder | 2023-11-29 22:52:54 UTC | #26

[quote="vilkris, post:24, topic:245"]
This would allow node providers to set whatever fees they want and request whatever ZTS they want as payment.
[/quote]

The problem that might arise in this situation is that the node you are connected to can be malicious for example:
- Feeding you wrong data
- Not broadcasting your transaction (or delaying it)

[quote="vilkris, post:24, topic:245"]
wouldn’t need protocol changes.
[/quote]

A more robust solution needs to take into account these factors as well.

[quote="0x3639, post:25, topic:245"]
I like an idea like this a lot more than relying on bridge fees
[/quote]

I like it too, but we need a better solution that takes into account the p2p layer (not only RPCs).

-------------------------

Chadass | 2023-11-30 14:05:50 UTC | #27

[quote="aliencoder, post:12, topic:245"]
I don’t seek funding. I seek a comprehensive solution.
[/quote]

Answer this then

![image|690x191](upload://r5wjlSLb0Rd7VHEgNWGdQaViW8Y.png)


As for the token utility, that's the poorest answer one could ever give. It's moot and does nothing. Again, check the data on Coingecko or elsewhere. Fee never helped in anyway.

Now I will rephrase it : plasma is already a fee abstraction. We should keep working in a way that doesn't betray the design that makes the NoM different and good. It can be improved and this is the direction the discussion should takes.

-------------------------

Chadass | 2023-11-30 14:06:33 UTC | #28

As said before, the emission can take care of this without using bridge fee.

-------------------------

aliencoder | 2023-11-30 16:35:55 UTC | #29

[quote="Chadass, post:27, topic:245"]
Answer this then
[/quote]

What? The text from the screenshot is not mine.

[quote="Chadass, post:27, topic:245"]
Fee never helped in anyway.
[/quote]

[quote="Chadass, post:27, topic:245"]
Now I will rephrase it : plasma is already a fee abstraction.
[/quote]

And we'll keep it that way. I've just added ZNN burn as a way to generate Plasma.

-------------------------

Zyler | 2023-11-30 16:44:23 UTC | #30

@Chadass alienc0der never said that, he actually said the opposite. You're thinking of moonbaze, but even then, that's not what moonbaze was saying. He still has other reasoning from what I interpreted. screenshots below
![alien|690x170](upload://vWUek0vXLAXh86DlKrzZE1yl7hF.png)
![moonbaze|690x190](upload://wWxkuGdWL3iwPO4KvjHaojOkXzl.png)

-------------------------

Chadass | 2023-11-30 16:52:54 UTC | #31

[quote="Zyler, post:30, topic:245"]
below
[/quote]

The screenshot you shared isn't the one I shared. Both agreed. Plus, your argument doesn't address the feeless reasoning and it doesn't address the twisted idea of the fee as an utility that helps : it does not help.

The fee proposal, even with lanes, doesn't helps with a design where plasma abstracts the fee.

-------------------------

