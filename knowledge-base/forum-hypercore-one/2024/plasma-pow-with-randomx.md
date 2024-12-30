Thread: plasma-pow-with-randomx
vilkris | 2023-10-19 08:55:11 UTC | #1

This thread is meant to combine the research efforts regarding the possibility of using [RandomX](https://github.com/tevador/RandomX) as our Plasma PoW algorithm.

In my ongoing research into [Metamask Snaps and wallet provider services](https://forum.hypercore.one/t/metamask-snaps-for-zenon/209/1), I've also taken a look at how RandomX PoW would work in that context and I want to share some of the insights I've gained.

### Background
Our current plasma PoW hashing algorithm is SHA3-256 and this hash algorithm is fine for our current network utilization rate. Since SHA3-256 isn't an ASIC-resistant algorithm, it would be possible to create an ASIC for it, resulting in PoW generation speeds so high that it would render PoW generation on consumer hardware pointless.

Building such an ASIC isn't worth it right now, but it can be argued that in a highly utilized, multi-billion dollar network, network throughput would be so valuable that there would be sufficient economic incentive to build such an ASIC.

RandomX is an (very good) attempt at a maximally ASIC-resistant PoW algorithm. The potential gain in speed from purpose built hardware for RandomX is limited, because of how the algorithm has been [designed]( https://github.com/tevador/RandomX/blob/master/doc/design.md). Ideally with RandomX, we could be more certain that PoW generation on our network is feasible on hardware that's readily available to consumers even with high network utilization. This is a significant benefit that RandomX could provide.

Mr. Kaine has also repeatedly advocated using RandomX as the PoW algorithm for plasma generation on our network once we implement dynamic plasma.

### Downsides and potential issues with RandomX
While RandomX has many of the qualities we want (primarily the ASIC-resistance), it has some potential problems for us.

RandomX is a resource intensive algorithm. To run the algorithm in the so called "fast mode", it requires at least ~2.5 GiB of RAM. During my testing of the RandomX algorithm I noted that initializing the RandomX VM in fast mode took around 30 to 60 seconds and this is with a relatively powerful computer. With lower end hardware this time most likely increases.

This means that using the fast mode for PoW generation on clients will increase the waiting time for the user, since whenever PoW needs to be generated, the VM has to be initialized first.

One option would be to keep the VM in memory all the time so that it only needs to be initiliazed once at startup, but Syrius is already a memory hog. A total RAM requirement of 5-10 GiB to run Syrius and an embedded node is not ideal if we're targeting regular consumer computers.

This also poses challenges on mobile devices that have limited memory and due to other requirements of the algorithm, it is completely unfeasible to run RandomX in browser environments.

The alternative to fast mode is light mode. Light mode runs at a much lower hashrate, but the initialization time is much faster - only around 2 seconds on my computer. Light mode only requires 256 MiB of RAM so it is much more suitable for regular consumer hardware.

On my computer the fast mode appears to be around 5x faster than the light mode. So the question is, can clients run in light mode and maintain a fast enough hashrate to generate PoW in a reasonable amount of time?

For the sake of comparison, someone using an expensive high end CPU can reach a hashrate that is over 20 times faster than on a low end consumer laptop. If the consumer laptop is running the algorithm in light mode, the difference in speed can be 100x. With ten high end CPUs the difference can be 1000x.

These aspects should be taken into account when we consider what the role of PoW is in dynamic plasma.

### RandomX PoW generation proof-of-concept

Here's a minimal PoC implemenation of our client PoW generation library that has been modified to use RandomX instead of SHA3: https://github.com/hypercore-one/znn-pow-links-cpp/tree/randomx-poc

-------------------------

0x3639 | 2023-10-18 19:44:18 UTC | #2

[quote="vilkris, post:1, topic:224"]
PoW links library that has been modified to use RandomX instead of SHA3
[/quote]

In Light mode would that translate into 150 to 300 seconds (5x longer) to process a TX than in Fast mode?  Hopefully these long TXs will only happen to fuse QSR or process one off transactions.  Personally, I would wait 300 seconds to avoid paying $3-5 like I do today on ETH.

-------------------------

georgezgeorgez | 2023-10-18 19:52:35 UTC | #3

Actually I think pow links are meant to be sha256 for merge mining
And plasma will be randomx for accessibility to feeless txs.

-------------------------

georgezgeorgez | 2023-10-18 19:58:33 UTC | #4

Pow links will be created by sentinels and chained together.
Consensus will be changed so that a tx cannot be confirmed unless it has a minimum number of pow links.

By rewarding sentinels for creating pow links that get confirmed, the minimum link requirement means sentinels are incentivized to propagate txs to other sentinels instead of hoard txs. This is what will form the incentivized public backbone.

Pow for dynamic plasma is different. That is the determination of the pow -> plasma conversion which will impact tx prioritization once txs are ordered by plasma. The requirement for plasma will still be in place.

Pow links will be a separate system / requirement for txs which is not implemented yet.

-------------------------

georgezgeorgez | 2023-10-18 20:10:14 UTC | #5

Asic friendly
* capex > opex
* requires investment
* but lowers marginal cost to operate
* few alternative use cases
* so more inertia to hashrate
* better for infrastructure/security

asic resistant
* opex > capex
* dependent on general cpus
* many alternative use cases
* good for accessibility to infrequent use cases
* volatile hashrate
* not as good for consistent weight / security

-------------------------

vilkris | 2023-10-19 07:50:36 UTC | #6

[quote="georgezgeorgez, post:3, topic:224, full:true"]
Actually I think pow links are meant to be sha256 for merge mining
And plasma will be randomx for accessibility to feeless txs.
[/quote]
Fair enough, I was using the terminology of our current client PoW library, which is "ZNN PoW Links".
Mr. Kaine has also referred to client generated PoW as "pow-links", so I wonder if we're missing something:
> And you need both: ASIC-friendly for security and ASIC-resistant for participation. I think it's safe to say SHA-256d and RandomX are the best candidates (reminder: we currently have SHA-3 as pow-links).

The whitepaper doesn't mention anything about clients taking part in PoW link generation though.

I'll edit the post to use a different term since PoW links is ambiguous.

-------------------------

vilkris | 2023-10-19 08:50:39 UTC | #7

[quote="0x3639, post:2, topic:224"]
In Light mode would that translate into 150 to 300 seconds (5x longer) to process a TX than in Fast mode? Hopefully these long TXs will only happen to fuse QSR or process one off transactions. Personally, I would wait 300 seconds to avoid paying $3-5 like I do today on ETH.
[/quote]
The total waiting time depends completely on what the current difficulty of the network is. If transactions can be sent by just generating PoW and network users start using high-end hardware to send lots of PoW transactions, then the waiting time on regular hardware/mobile phones can become so high that it becomes unfeasible to wait that long.

Let's say that it takes around 1 minute to send a normal TX with PoW on a low-end laptop using light mode. At least theoretically someone with a high end CPU farm could send the transaction in 1 min/1000 = 0.06 seconds for example. Now the network's difficulty would have to adjust to meet the hash power of the CPU farm. So if it takes 1 minute for the CPU farm to send a transaction, the user with the low-end laptop will have to wait for 1min*1000 = 16.6 hours to generate the PoW for a transaction.

This is a simplified example but you get the point that balancing the PoW difficulty in such a way that it's suitable for low-end hardware and not too easy for high-end hardware is a challenge. So like I said we have to consider what role PoW has in dynamic plasma and what our goals are for using PoW as a tx prioritization mechanism.

-------------------------

MoonBaze | 2023-10-19 10:33:47 UTC | #8

Having any server that does pow relates to these issues

https://twitter.com/LiveOverflow/status/1714342123724574979

-------------------------

georgezgeorgez | 2023-10-19 16:08:43 UTC | #9

Yes I was confused too about Mr K calling wallet generated pow as pow-links.
So it's possible I'm missing something.

-------------------------

aliencoder | 2023-10-19 20:38:33 UTC | #10

[quote="georgezgeorgez, post:4, topic:224"]
Pow links will be created by sentinels and chained together. By rewarding sentinels for creating pow links that get confirmed, the minimum link requirement means sentinels are incentivized to propagate txs to other sentinels instead of hoard txs. This is what will form the incentivized public backbone.
[/quote]

[quote="vilkris, post:6, topic:224"]
The whitepaper doesn’t mention anything about clients taking part in PoW link generation though.
[/quote]

I think that the PoW can be safely outsourced (to others that have disposable PoW), but the actual links will be signed by the Sentinel nodes. Why would other clients provide PoW to Sentinels? Because they can be incentivized to do so by Sentinel operators.

[quote="vilkris, post:6, topic:224"]
> And you need both: ASIC-friendly for security and ASIC-resistant for participation. I think it’s safe to say SHA-256d and RandomX are the best candidates (reminder: we currently have SHA-3 as pow-links).
[/quote]

I'm guessing that MrK wants us to find a way to balance ASIC friendly with CPU friendly PoW. We want users to make transactions seamlessly, while adding weight to the ledger.

In Bitcoin, only miners are adding weight. Users are paying fees that go directly into the security budget of the network (block fees + an ever decreasing block subsidy).

In Zenon, users are not paying fees (directly), but still need to support the security budget somehow.

-------------------------

vilkris | 2023-10-20 15:06:34 UTC | #11

[quote="aliencoder, post:10, topic:224"]
I think that the PoW can be safely outsourced (to others that have disposable PoW), but the actual links will be signed by the Sentinel nodes. Why would other clients provide PoW to Sentinels? Because they can be incentivized to do so by Sentinel operators.
[/quote]
Maybe this could be the case but the whitepaper doesn't seem to suggest this.

What I don't understand is that Mr K has been clear that the PoW for dynamic plasma should be ASIC-resistant, so if George's idea of sha256 merge mining is how sentinel PoW is meant to be generated, then why is the founding team using the same terminology for these two supposedly separate PoW systems (e.g. "ZNN PoW Links" lib)?

The white paper does talk about pillars doing PoW and utilizing PoW pools (sha256 merge mining?), but that idea hasn't really been discussed by the community in detail. The whitepaper also only explicitly talks about pillars outsourcing their PoW but doesn't mention this for sentinels and talks about "small PoW" for sentinels, so it makes me think that sentinel PoW is meant to be light. Does merge mining sha256 fit that goal?

If we look at the proposed PoW links algorithm in the whitepaper, the sentinels contribute to the transaction's overall weight, but it's not clear whether the sender is allowed to pre-generate weight for the transaction so that `min_target_weight` is achieved in fewer hops. The `min_relay_dimension` constant would still set a constraint that even if `pre_generated_weight >= min_target_weight` the transaction would still need to go through `min_relay_dimension` hops. If the sender can partake in the PoW link mechanism in this way, the terminology used by the founders makes more sense to me.

[quote="aliencoder, post:10, topic:224"]
I’m guessing that MrK wants us to find a way to balance ASIC friendly with CPU friendly PoW.
[/quote]
This is what the WP has to say about PoW balancing. It only refers to it in the context of pillar generated PoW, not sentinel generated PoW:
> *D. Pillars PoW pools*
In order for the pillars to be competitive in the process of producing the proof of work, they will have the possibility to outsource it using the mining pool concept. This will create a market efficient ecosystem that will further strengthen the network and clients committing resources for Pillar pools will be rewarded proportionally to their contribution of processing power. We are also investigating the use of a custom difficulty adjustment mechanism that will balance between ASIC-friendly and ASIC-resistant hashing algorithms in order to improve network security and obtain a higher degree of decentralization. We will defer a detailed specification for a later date.

And:
> *E. Adjusting the difficulty of PoW*
> As we have previously stated, the idea behind the proof of work mechanism has multiple advantages – prevents ledger cloning, acts as an additional anti-sybil layer and provides a fair incentivization scheme for the consensus nodes. The PoW will be adjusted in order to keep an epoch at a constant time, for example 1 minute. The algorithm will check at every epoch the time needed for every pillar to solve the proof of work, will remove the outliers and then will compute a median time. We plan to release a self-balancing difficulty algorithm that will use both ASIC-friendly and ASIC-resistant hashing algorithms; if the difficulty is below a threshold an ASIC-friendly hashing algorithm will be activated, and also if the difficulty is above a threshold, an ASIC resistant will come into effect.

So based on this could it be that plasma & sentinel PoW = randomX and pillar PoW = sha256 & randomX?

-------------------------

0x3639 | 2023-10-21 16:57:42 UTC | #12

Sharing some relevant messages from TG

![Screenshot 2023-10-21 at 11.47.58 AM|690x351](upload://s3TNnqwZpeqqHJNx6k23byFiZ0p.png)

---

![Screenshot 2023-10-21 at 11.49.53 AM|690x326](upload://iQVY5NcoNFcbue1loPHeJGQV1J7.png)

---

![Screenshot 2023-10-21 at 11.51.07 AM|690x368](upload://u1UvIVaf5FIY2IBQOgskXenn5fi.png)

---

![Screenshot 2023-10-21 at 11.52.03 AM|690x403](upload://5dF4xMwqhAM3PbPESiHMddACOf2.png)

---

![Screenshot 2023-10-21 at 11.52.57 AM|690x167](upload://YQ0c9P6KhB06T7gimXR8J9U9NC.png)

---

LOOK AT THIS ONE.

> Sentinels won't need to compute PoW.

![Screenshot 2023-10-21 at 11.54.13 AM|690x420](upload://z1h1X8sfy21F7QjUwVul2Wr9udQ.png)

---

![Screenshot 2023-10-21 at 11.55.47 AM|690x173](upload://cw3JMP7XdHCR95TdU9BFfKQXmXS.png)

-------------------------

MoonBaze | 2023-10-21 19:42:27 UTC | #13

Can mr kayne v2 give us a full detailed explanation about his views? He did not say anything concrete, just theoretical stuff that we kind of already knew. Saying “just do that” without giving the reasoning behind and why is that the best solution seems sketchy.

-------------------------

Shazz | 2023-10-21 21:31:38 UTC | #14

Welcome to zenon. It's how it's always been, unfortunately

-------------------------

0x3639 | 2023-10-21 21:31:21 UTC | #15

[quote="MoonBaze, post:13, topic:224"]
Can mr kayne v2 give us a full detailed explanation about his views?
[/quote]
This would be helpful.

[quote="MoonBaze, post:13, topic:224"]
why is that the best solution seems sketchy.
[/quote]
LOL.  Hard to argue with this.

-------------------------

Chadass | 2023-10-23 15:46:22 UTC | #16

We could ask and he'll answer somewhere within 10 months.

-------------------------

