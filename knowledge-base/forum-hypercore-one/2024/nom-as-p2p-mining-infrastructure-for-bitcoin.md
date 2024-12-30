Thread: nom-as-p2p-mining-infrastructure-for-bitcoin
aliencoder | 2023-11-21 09:58:48 UTC | #1

Inspired by the discussion for dynamic Plasma, I'm coming up with a brand new development that seeks to decentralize the mining pools found in Bitcoin.

Every use in NoM can act like a "solo-miner" and use PoW to generate Plasma and issue feeless transactions. 

I'm thinking out loud now: is it possible to recycle this PoW and mine actual Bitcoin?

I've come across [Braidpool](https://blog.opdup.com/2021/06/30/can-braidpool-reuse-p2pool-components.html), a new concept that seems to check all the boxes:

1. A peer to peer network of miners to disseminate shares:
We already have a p2p network of "miners": they are the users of NoM.

2. A rewards calculation algorithm that incentivizes miners to disseminate them at the earliest.
Very interesting because we already have this mechanism: you want your transaction to be issued as soon as possible.

3. Payment channels to make payouts to miners so that a constant amount of blockspace is required, independent of the number of participating miners.
Here's where PTLCs come into play.

4. An anonymous hub that can’t deny rewards payouts to miners.
Can Pillars be those anonymous hubs? They already issue payouts for hundreds of delegators.

> In P2Pool the network difficulty is adjusted so that the pool finds one share every 30 seconds. This results in smaller miners struggling to find enough share and makes P2Pool economically nonviable for them. In Braidpool, this is not the case. Each miner participating in Braidpool can choose the difficulty they mine at so that they generate a share at an interval of their choosing. Small miners will mine at low difficulty to generate a share every 10 seconds, while large miners will mine at a much larger difficulty to find a share every 10 seconds. Both the difficulty and the share period can be configured by the miner.

I'm remembering some parts of the whitepaper that compares Pillars to mining pools. Is the whitepaper so forward thinking? The more I read, the more interesting those ideas become.. I'm trying to connect some dots here. 

We should definitely explore this subject.

-------------------------

0x3639 | 2023-11-21 14:43:09 UTC | #2

Let me summarize what you are thinking about to make sure I understand.

- P2P mining pool (so we don't need to join a pool and dox)
- PTLC to make payments to miners (anon)
- Generate PoW for TXs and "use" it to mine Bitcoin while not being used for plasma.  

Is this correct?

I'm wondering if Miners can generate PoW for plasma, store it up, and then sell it for TXs.  I've talked to @vilkris about this and there are limitations.  But if we can get miners involved we can really accelerate growth.  Need to be able to store the plasma, and use it for different TXs on different addresses.

-------------------------

aliencoder | 2023-11-21 17:23:31 UTC | #3

[quote="0x3639, post:2, topic:239"]
* P2P mining pool (so we don’t need to join a pool and dox)
[/quote]

Users that want feeless txs via PoW will need to participate into the P2P mining pools (setup around a Pillar hub).

[quote="0x3639, post:2, topic:239"]
* PTLC to make payments to miners (anon)
[/quote]

Actually we can store the mined Bitcoins in a TSS controlled by the Pillars. And use that Bitcoin to pay fees for embedding information into the Bitcoin blockchain.

[quote="0x3639, post:2, topic:239"]
* Generate PoW for TXs and “use” it to mine Bitcoin while not being used for plasma.
[/quote]

Generate SHA-256d PoW to mine Bitcoin *while* it is being used for feeless txs. Basically merge-mine Bitcoin while generating Plasma for feeless txs.

- NoM can become the first decentralized mining pool for Bitcoin, strengthening the hashrate, while increasing the number of mining peers (more users on NoM => more hashrate => more BTC mined => more TVL => more users, positive feedback loop)
- it can become the first network to acquire Bitcoins by mining them in a trustless way
- it can use mined BTC to embed information into the Bitcoin blockchain (tapscripts) by paying fees and unlock a myriad of use cases (including the "Holy Grail" aka Bitcoin DeFi)
- it can become the first decentralized network to simultaneously mine, hold and use on-chain BTC trustlessly, providing added value and acting as a Bitcoin L2
- creates a symbiotic relationship with Bitcoin by providing hashrate in exchange for block space (mine & pay sats/vbyte)

-------------------------

vilkris | 2023-11-22 12:45:01 UTC | #4

A couple questions:

What kind of hashrate are you expecting these p2p mining pools to realistically achieve? Considering we can roughly say that 1M laptops = 1 flagship Antminer.

Is the user providing the hashpower getting the bitcoin reward or does the reward go to the TSS?

If difficulty is converted into plasma, then what's stopping an attacker from using a cheap old ASIC and hogging all the PoW plasma, unless regular users also use ASICs?

-------------------------

aliencoder | 2023-11-22 17:23:07 UTC | #5

[quote="vilkris, post:4, topic:239"]
What kind of hashrate are you expecting these p2p mining pools to realistically achieve?
[/quote]

If properly incentivized, some people might spin up some old ASIC equipment. From the whitepaper: "the pillars can outsource the proof of work, acting as mining pools to amass resources and rewarding accordingly the clients that supply them with computational power. ". Think of Plasma as a byproduct of merge-mining Bitcoin and PoW delegation rewards. Some people will mine for Plasma, others for ZNN or both. A market will emerge.

[quote="vilkris, post:4, topic:239"]
Considering we can roughly say that 1M laptops = 1 flagship Antminer.
[/quote]

Ordinary users will generate Plasma regardless of PoW, QSR fusing or even burning ZNN as fees in order to issue transactions on the network.

[quote="vilkris, post:4, topic:239"]
If difficulty is converted into plasma, then what’s stopping an attacker from using a cheap old ASIC and hogging all the PoW plasma, unless regular users also use ASICs?
[/quote]

The attacker will spam with PoW, but the Bitcoins generated as a result will go to the network.  Also from the whitepaper: "self-balancing difficulty algorithm that will use both ASIC-friendly and ASIC-resistant hashing algorithms" and "will balance between ASIC-friendly and ASIC-resistant hashing algorithms in order to improve network security and obtain a higher degree of decentralization". Plus users will have a multi-lane system for transactions, they won't be limited in any way.

Right now I'm gathering all the pieces of the puzzle.

-------------------------

Blueginger | 2023-11-26 14:36:12 UTC | #6

If we were to go forward with this, how much time will it take approximately to implement it?

-------------------------

0x3639 | 2023-11-26 17:52:53 UTC | #7

@aliencoder are you considering this section of the whitepaper in your thinking?  Seems like this is a separate topic than what you are researching now.  

![Screenshot 2023-11-26 at 11.51.27 AM|690x499](upload://fiw3Fc5I6Ty6GxAnQkPZMh2tyx1.png)

-------------------------

Zyler | 2023-11-26 17:53:46 UTC | #8

I had some Questions :sunglasses: but it's okay if they are hard to answer at this point in time ...

So Zenon as a whole is a P2P btc mining pool, where each pillar is a miner and the btc goes to the tss?

Say the pillar outsources its PoW, making the pillar itself a small mining pool. Can that also be P2P? Or does it need to be more like a traditional mining pool, as the 3rd party miners need to trust the pillar which has control over rewards distribution and fees charged, and if the pillar goes down the mining stops? Why would 3rd party miners enter into a traditional mining pool with pillars if the future is P2P, is it cos they are incentivised by mergemined ZNN rewards too, is that the tradeoff?

And you say regular non-pillar ZNNAliens can have their PoW for transactions recycled, do they get rewarded in proportion to their hash contribution too, are they considered part of the pillar's pool? Is that where the Braid implementation comes in, because it's friendly to small miners? Doesn't Braidpool have a minimum difficulty level though, so people below the threshold won't be able to generate any shares? I guess their reward is they get to have a feeless transaction, regardless of any BTC reward ... and the recycled PoW is a public good which indirectly benefits them because it benefits zenon overall

-------------------------

Chadass | 2023-11-26 20:55:42 UTC | #9

From what I understand @aliencoder wants to make the **protocol** a mining pool, not build a business model where pillars outsource PoW. Trustless mining pool.

I'm pretty proud of my summary so please don't ruin it Alien.

-------------------------

aliencoder | 2023-11-26 21:20:23 UTC | #10

[quote="Blueginger, post:6, topic:239"]
how much time will it take approximately to implement it
[/quote]

The main thing is to get it right from the beginning. And then focus all dev effort into it.

[quote="0x3639, post:7, topic:239"]
are you considering this section of the whitepaper
[/quote]

I'm considering all sections and adapt them to today's reality.

[quote="Zyler, post:8, topic:239"]
making the pillar itself a small mining pool
[/quote]

P2P mining means that every network participant will be able to merge-mine, regardless of their status in the network (user, staker, delegator, node, etc).

> Vires in numeris

Pillars already have a pool of delegators: merge-mining can be used to further incentivize less potent hardware to participate. This is important because small miners can offset their costs by generating ZNN, while benefiting from the price exposure (larger miners with more hashpower are generating BTC for the network as a whole).

Furthermore, the BTC that will get mined is a collective good of the network (that will be used for other network operations aka paying for block space), increasing the overall value of the network. Pillars can reuse this PoW and "anchor" it into the ledger: "strengthen the ledger by adding weight into it (i.e. recording the resulting work of the PoW link".

[quote="Zyler, post:8, topic:239"]
Why would 3rd party miners enter into a traditional mining pool with pillars if the future is P2P, is it cos they are incentivised by mergemined ZNN rewards too, is that the tradeoff?
[/quote]

The mining will be done *peer-to-peer*: Pillars will only do "[miner share accounting](https://blog.opdup.com/specifications/BlockGeneration.pdf)", but with ZNN instead of BTC. The resulting BTC will go into the network's "treasury".

[quote="Zyler, post:8, topic:239"]
Doesn’t Braidpool have a minimum difficulty level though, so people below the threshold won’t be able to generate any shares?
[/quote]

"Since [small miners](https://blog.opdup.com/2021/06/30/can-braidpool-reuse-p2pool-components.html) are able to find shares at their chosen difficultly, they can claim rewards for all their PoW shares."

[quote="Chadass, post:9, topic:239"]
Trustless mining pool.
[/quote]

Exactly this is the objective. But we need to carefully design it in such a way that is both technically and economically feasible.

-------------------------

Zyler | 2023-11-27 04:02:05 UTC | #11

I think I understand better now. It seems like Zenon's hash rate can't really be forced overnight, there's an organic growth/positive feedback loop at play where more use of the NoM is required, since it's not a mining business as such as the BTC would be a public good rather than paid in proportion to hash contributed. Very interesting

-------------------------

aliencoder | 2023-11-30 22:12:32 UTC | #12

Solo-mining is [back in town](https://bitcointalk.org/index.php?topic=5237323.msg63244510#msg63244510).

Peer-to-peer merge-mining will be game-changer for miners that wish to secure additional revenue for their operations.

-------------------------

BigFrank | 2023-12-08 18:08:13 UTC | #14

Laymans terms…

By locking BTC in NoM, I can become a BTC miner and earn BTC.

is this correct?

-------------------------

coinselor | 2023-12-09 05:45:25 UTC | #16

Incorrect.

The definition of a BTC miner does not change. They provide PoW to the BTC network in exchange for the ability to mint a block when successful. If merge-mining with ZNN, they will reuse the PoW to do some NoM stuff in exchange for some benefits.

-------------------------

aliencoder | 2023-12-09 08:32:50 UTC | #17

[quote="coinselor, post:16, topic:239"]
The definition of a BTC miner does not change.
[/quote]

Exactly.

[quote="coinselor, post:16, topic:239"]
If merge-mining with ZNN, they will reuse the PoW to do some NoM stuff
[/quote]

NoM stuff = merge-mine ZNN & BTC, add weight onto the ledger via PoW share-blocks and receive ZNN in the process. The mined BTC go into a network wide TSS for decentralized custody.

Furthermore, NoM's BTC will be used to allocate Bitcoin block space for smart contracts that will get executed on NoM. Native, on-chain BTC, not a wrapped representation of it.

-------------------------

BigFrank | 2023-12-09 13:28:54 UTC | #18

Ok got it. I was pretty confused on the topic. This and some discussion in the tg helped make it clear. ty.

-------------------------

Blueginger | 2023-12-09 13:44:35 UTC | #19

[quote="aliencoder, post:17, topic:239"]
Furthermore, NoM’s BTC will be used to allocate Bitcoin block space for smart contracts that will get executed on NoM. Native, on-chain BTC, not a wrapped representation of it.
[/quote]

I didnt understand this part. How is NoM BTC native BTC?

-------------------------

coinselor | 2023-12-09 14:19:30 UTC | #20

It's not NoM BTC. It's literally NoM's BTC, as in native BTC owned by NoM (pillar's TSS).

-------------------------

Stark | 2023-12-09 14:59:24 UTC | #21

https://x.com/Zenon_Core/status/1733313255525765501?s=20

Paying it forward. Context is a campaign by Taproot Wizards to troll Luke about censoring ordinals.

-------------------------

Chadass | 2023-12-09 15:23:32 UTC | #22

It it going through TSS here? I'm not quite sure.

-------------------------

Blueginger | 2023-12-10 03:50:44 UTC | #23

It's like wznn in eth issued by locking znn in NoM? That's what sumamu bridge does isn't?

-------------------------

coinselor | 2023-12-10 18:12:24 UTC | #24

[quote="Blueginger, post:23, topic:239"]
sumamu bridge does isn’t?
[/quote]

We'll have BTC locked in a multisig controlled by Pillars. This is basically what we mean by NoM's BTC. We can then use that native BTC for a myriad of use-cases, most of which I'm not even in a position to be able to explain, but being able to post "data" into the BTC chain by submitting a BTC transaction should open up a world of possibilities.

-------------------------

Chadass | 2023-12-10 19:02:07 UTC | #25

BTC locked by pillars isn't native

-------------------------

aliencoder | 2023-12-10 19:37:47 UTC | #26

Why?

-------------------------

Chadass | 2023-12-10 19:46:42 UTC | #27

Because then you have to trust one more actor in addition to BTC aka the pillars. Beside, once locked on pillars those assets aren't the ones moving on the NoM, the ones moving are wBTC or zBTC or whatever the name of that representation will be.

Unless I'm missing an important point trusting the pillars is trusting a more decentralized version of any non self-custodian solution. You lock A, you get zA to play around with. A is comprised on your trusted solution, zA become worthless.

-------------------------

aliencoder | 2023-12-10 20:01:18 UTC | #28

Pillars will control on-chain BTC.

[quote="Chadass, post:27, topic:239"]
Beside, once locked on pillars those assets aren’t the ones moving on the NoM, the ones moving are wBTC or zBTC or whatever the name of that representation will be.
[/quote]

They won't move zBTC. They will move on-chain Bitcoin.

[quote="Chadass, post:27, topic:239"]
You lock A, you get zA to play around with.
[/quote]

Pillars don't lock BTC. They will use Bitcoin to pay for block space.

[quote="Chadass, post:27, topic:239"]
Unless I’m missing an important point trusting the pillars is trusting a more decentralized version of any non self-custodian solution
[/quote]

I have a solution for a more decentralized custody that will involve not only Pillars, but also other NoM network participants.

-------------------------

Chadass | 2023-12-10 20:29:17 UTC | #29

Oh ok. The term "locked" confused me in the discussions

-------------------------

0x3639 | 2023-12-10 22:36:37 UTC | #30

I think it's native BTC that lives on the BTC network that has a private key controlled by the Pillars via TSS.  

How do we deal with TSS as we add and remove Pillars?

-------------------------

aliencoder | 2023-12-10 22:38:31 UTC | #31

[quote="0x3639, post:30, topic:239"]
How do we deal with TSS as we add and remove Pillars?
[/quote]

The same way Thorchain handles this case: creating a new key and invalidating the previous one.

-------------------------

Chuckerboy | 2023-12-18 02:57:25 UTC | #32

[quote="aliencoder, post:10, topic:239"]
This is important because small miners can offset their costs by generating ZNN
[/quote]

and merge miner will be new participants (first class)

it will be implicate to more znn inflation offcourse or reduce other reward participants
Since we have 90m max supply hardcoded, I think we need somthing like "halving znn/qsr".
It think that is great for attract more solo merge miner participant.

-------------------------

Paesch | 2023-12-18 19:23:57 UTC | #33

If we really could mine btc via merge mining on nom, how would it influence the overall performance of the network?
How high of a hashrate could the network generate?

-------------------------

coinselor | 2023-12-18 20:04:51 UTC | #34

Here's my understanding, and I'm open to corrections if there are errors in my reasoning:

Merge-mining enables us to leverage BTC hashing power for mining ZNN at a reduced difficulty, a concept termed "share-chain" by @aliencoder .

For small miners, mining BTC alone isn't profitable, even when pooling resources and sharing block rewards. However, by allowing these miners to simultaneously mine BTC and ZNN, we're re-motivating them to contribute their hashing power to BTC. This re-engagement of small miners with BTC, as opposed to them shifting their focus to other competing cryptocurrencies or shutting down their operations, significantly aids in decentralizing the hashing power source. This is crucial, as the current concentration of hashing power is problematic.

In return for ZNN rewards, the mined BTC becomes the property of NoM, secured by a multisig of Pillars and managed through an embedded NoM contract.

While merge mining isn't a novel concept, I believe no one has yet managed to develop such a harmoniously symbiotic merge mining system with the BTC ecosystem. NoM aims to establish a "smart" layer 2 ecosystem, where native BTC can not only exist but flourish. It does this by overcoming the limitations of the native BTC layer, without any trade-offs.

Here's my question:

- As the hashrate for the NoM share-chain increases and the difficulty level adjusts, won't this eventually render small miners unprofitable again?

-------------------------

0x3639 | 2023-12-18 23:17:58 UTC | #35

[quote="coinselor, post:34, topic:239"]
As the hashrate for the NoM share-chain increases and the difficulty level adjusts, won’t this eventually render small miners unprofitable again?
[/quote]

My guess is yes, over time this will happen.  But initially the early miners will probably be very successful with limited mining capacity.

-------------------------

Chadass | 2023-12-19 00:11:34 UTC | #36

What algo will be used for mining? If it's SHA256 then ASICs will get in real fast. If it's not, then I'm curious about how it works.

-------------------------

Blueginger | 2023-12-19 01:38:57 UTC | #37

I guess we need dynamic plasma implemented for this

-------------------------

aliencoder | 2023-12-19 11:09:55 UTC | #38

[quote="Paesch, post:33, topic:239"]
how would it influence the overall performance of the network?
[/quote]

No impact. Merge-mining is decoupled from consensus.

[quote="Paesch, post:33, topic:239"]
How high of a hashrate could the network generate?
[/quote]

As high as it can get. It really depends on the profitability of miners.

[quote="coinselor, post:34, topic:239"]
* As the hashrate for the NoM share-chain increases and the difficulty level adjusts, won’t this eventually render small miners unprofitable again?
[/quote]

The embedded can support multiple share-chains (we can start with two share-chains like Monero's p2p pool), where the smallest share-chain can accommodate the smallest miners. They will collectively can generate as much as the biggest share-chain. Check [this](https://github.com/SChernykh/p2pool): "add the `--mini` parameter to your P2Pool command to connect to the **p2pool-mini** sidechain. Note that it will also change the default p2p port from 37889 to 37888."

[quote="Chadass, post:36, topic:239"]
What algo will be used for mining?
[/quote]

Do you know how Bitcoin is mined?

[quote="Blueginger, post:37, topic:239, full:true"]
I guess we need dynamic plasma implemented for this
[/quote]

Dynamic Plasma is not a hard dependency for Bitcoin merge-mining.

-------------------------

0x3639 | 2023-12-19 11:31:07 UTC | #39

[quote="Chadass, post:36, topic:239, full:true"]
What algo will be used for mining? If it’s SHA256 then ASICs will get in real fast. If it’s not, then I’m curious about how it works.
[/quote]

As I understand it we will use 2 different Algos.  User transactions will move to CPU focused PoW (RandomX or similar but could be impacted by the Metamask Snap Discussion).  

Pillars will perform PoW based on a difficulty adjustment and the Algo will switch [per the whitepaper].

"We plan to release a self-balancing difficulty algorithm that will use both ASIC-friendly [SHA256] and ASIC-resistant [RandomX] hashing algorithms; if the difficulty is below a threshold an ASIC-friendly hashing algorithm will be activated, and also if the difficulty is above a threshold, an ASIC- resistant will come into effect."

And don't forget the question vilkris asked previously about someone attacking the network with PoW.  If someone throws a ton of ASIC power at the PoW the difficulty will go up and or change and the network will BENEFIT because it will merge mine BTC with that PoW and the network will retain the BTC.

-------------------------

aliencoder | 2023-12-19 13:34:32 UTC | #40

[quote="0x3639, post:39, topic:239"]
User transactions will move to CPU focused PoW (RandomX or similar but could be impacted by the Metamask Snap Discussion).
[/quote]

User transactions will be made exclusively using a CPU PoW algorithm and the best we have is RandomX. 

This means that users will merge-mine the RandomX share-chain where the difficulty adjustment algo will deter spam attacks.

Miners that help Sentinels craft the PoW links will also compute RandomX PoW.

[quote="0x3639, post:39, topic:239"]
And don’t forget the question vilkris asked previously about someone attacking the network with PoW.
[/quote]

Users will also be able to make transactions fusing QSR and hopefully using ZNN as fee.

[quote="0x3639, post:39, topic:239"]
Pillars will perform PoW based on a difficulty adjustment and the Algo will switch.
[/quote]

Pillars and/or Sentinels won't perform the actual PoW. They are just nodes that sign/relay information. Miners and users will compute PoW.

To recap:

- Share-chains are at block-lattice level (embedded account-chains)
- NoM consensus is at the meta-DAG level
- The block-lattice will gain weight from those share-chains + user feeless transactions
- Users will perform RandomX PoW for feeless transactions and they need to satisfy a certain threshold for their tx to be accepted by the network
- The difficulty threshold will be computed based on the RandomX share-chain
- Sentinels will relay transactions and add additional weight from RandomX miners computing RandomX PoW (Sentinels must share rewards with RandomX miners to be competitive in crafting PoW links)
- Extra: RandomX PoW can be merge-mined with XMR/RandomX coins
- BTC miners will compute SHA-256d PoW on a separate share-chain(s)
- The difficulty of the BTC share-chains will be dynamically adjusted to accommodate both big and small miners
- Pillars will monitor the BTC share-chains to propagate valid Bitcoin blocks to the Bitcoin network
- Pillars will use high-quality BTC share-blocks to anchor NoM's consensus to the block-lattice
- The canonical Bitcoin blockchain is "longest chain with most PoW invested into it"
- The canonical NoM ledger is "heaviest ledger with most PoW invested into it"
- As an attacker you will need both stake and proof-of-work (users, miners) to successfully fork the network

-------------------------

Chadass | 2023-12-19 13:44:49 UTC | #41

[quote="aliencoder, post:38, topic:239"]
Do you know how Bitcoin is mined?
[/quote]

Yes. Please can you elaborate on the algo we would be using? If I understand correctly then we must use the same algo to merge mine with BTC and then I fail to see how it'll benefit small miner since ASIC can step in anytime. If we use another algo, as @0x3639 mentions, then we can mine BTC, correct?

My question comes to challenge the small miner friendly claims I've read on the forum. If there's ASICs, there's no small miners. I'm assuming here that we have a new class of actors aka the miners.

-------------------------

aliencoder | 2023-12-19 13:54:06 UTC | #42

Q: What type of miners will NoM have?
- ASIC miners that merge-mine BTC on the `SHA-256d` share-chain(s).
- CPU miners that *can* merge-mine XMR on the `RandomX` share-chain(s).

Q: How many share-chains will NoM have?
- For each category (ASIC/CPU) there will be 2 (or more in the future) share-chains to accommodate both big and small miners (such that the variance will be low for each type of share-chain), as follows:
  - If you have the most powerful Bitcoin ASIC miner you will mine on the `main` SHA-256d share-chain
  - If you have an older Bitcoin ASIC you will be able to mine on the `mini` SHA-256d share-chain
  - If you have a high-end server CPU you will able to mine on the `main` RandomX share-chain
  - If you are a user with a mid-range smartphone you will mine on the `mini` RandomX share-chain

Q: Who will merge-mine BTC?
- ASIC miners will merge-mine BTC on the `SHA-256d` share-chain(s).

Q: Who will incentivize the BTC miners?
- Pillars using the delegate-reward system that we already have proportional to their hashrate (share-blocks from the share-chain).

Q: What rewards will BTC miners receive?
- **Primary**: ZNN rewards from Pillars.
- **Secondary**: BTC rewards: blocks produced by miners that are used to anchor NoM's consensus *can* also receive BTC rewards from the Pillar's TSS.

Q: Who will compute the RandomX PoW?
- RandomX miners employed by Sentinels to create the PoW links. Sentinels will only be required to sign transactions.
- Users required to meet the minimum PoW threshold for feeless transactions.

Q: Who will incentivize the RandomX miners?
- Sentinels will compete for RandomX miners to be able to create the PoW links.

Q: How do we compute the difficulty for the PoW feeless lane?
- We compute the difficulty of the `mini` RandomX share-chain.

Q: How do we compute the difficulty for the PoW links?
- We compute the difficulty of the `main` RandomX share-chain.

Q: What rewards will RandomX miners receive?
- **Primary**: ZNN and QSR rewards from Sentinels.
- **Secondary**: XMR or other coins that are merge-minable using RandomX.

-------------------------

coinselor | 2023-12-19 18:28:03 UTC | #43

From the XMR Decentralized P2P pool linked above, it's a trustless and permissionless design, so:

Suppose I have a state-of-the-art last generation ASIC Bitcoin miner or HIgh-end server CPU, couldn't  I just split my hashrate to give the impression I'm a bunch of smaller "old" miners and take advatange of the lower difficulty share-chain(s)?

-------------------------

aliencoder | 2023-12-19 22:43:02 UTC | #44

[quote="coinselor, post:43, topic:239"]
couldn’t I just split my hashrate to give the impression I’m a bunch of smaller “old” miners and take advatange of the lower difficulty share-chain(s)?
[/quote]

You can split your hashrate, but the lower difficulty share-chain will have lower payouts, so it's not worth it.

-------------------------

Chuckerboy | 2023-12-20 02:18:25 UTC | #45

So, we dont have small miner to merge mine with BTC except with Random-X minable coin.

-------------------------

Chuckerboy | 2023-12-20 02:28:25 UTC | #46

As basic/majority users, I want to send zts token, then i want feeless trx, so i can generate pow `mini` RandomX share-chain. It can generate pow automatically, just send trx, generate Pow via CPU `main` RandomX share-chain. Righ?

Then I confuse with fused qsr lane, its basically fusing qsr is a process to generating pow, and we dont need generate pow in future to send trx?

-------------------------

aliencoder | 2023-12-20 08:19:29 UTC | #47

[quote="Chuckerboy, post:45, topic:239, full:true"]
So, we dont have small miner to merge mine with BTC except with Random-X minable coin.
[/quote]

We will have small miners to merge-mine both BTC and any RandomX minable coins on their respective `mini` share-chains.

[quote="Chuckerboy, post:46, topic:239"]
As basic/majority users
[/quote]

User transaction flow:
1. Feeless lane: proof-of-work generation for transactions
- The user computes a RandomX PoW on the `mini` share-chain to meet the required threshold and broadcasts the transaction.
- The tx is propagated throughout the network. It needs to satisfy the PoW links requirement to be valid and accepted by the consensus protocol. 
- The Sentinel node will pick up this transaction and attach a PoW that can be outsourced to a RandomX miner and sign it. 
- After that, another Sentinel node will do the same thing until the overall PoW link has sufficient weight (the difficulty target > a minimum threshold computed based on the `main` RandomX share-chain) and can be included in a momentum by a Pillar node.
2. Feeless lane: fused QSR for transactions
- Instead of computing a RandomX PoW, the user fuses (locks) a minimum number of QSR.
- The rest of the flow is similar to 1
3. Fee lane: burn/consume ZNN for transactions
- The user can optionally burn/spend ZNN to issue a transaction

-------------------------

