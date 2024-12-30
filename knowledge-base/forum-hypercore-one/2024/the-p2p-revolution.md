Thread: the-p2p-revolution
georgezgeorgez | 2023-05-23 12:08:06 UTC | #1

The future is P2P!
Welcome to the P2P Revolution.

With the basic primitives of HTLCs and PTLCs in place we can now begin development of a truly decentralized p2p trading market.

Bridges will enable us to provide liquidity where people expect it now.
We will build the liquidity of the future.

As Vitalik says in his recent Sunday post:

> * **Cross-chain bridges**: similar logic as oracles, but also, try to minimize how much you rely on bridges at all: hold assets on the chain where they originate and use atomic swap protocols to move value between different chains.

https://vitalik.ca/general/2023/05/21/dont_overload.html

Later today, we will release a test build of Syrius which (thanks to Vilkris) has a best in class Atomic Swap UI. We will also be posting instructions on how to join our testnet so that everyone can try Atomic Swaps and begin experiencing the P2P Revolution.

This is just the first step, and there are a lot more possibilities when it comes to the potential of P2P, such as orderbook based interfaces.
I am asking a minimum of 150k ZNN, 1.5 M QSR for myself and other team members for continued work in this direction.

-------------------------

Blueginger | 2023-05-23 18:05:37 UTC | #2

[quote="georgezgeorgez, post:1, topic:69"]
This is just the first step, and there are a lot more possibilities when it comes to the potential of P2P, such as orderbook based interfaces.
[/quote]

Can u be more detailed.

What all does 150k znn and 1.5mil QSR cover?

-------------------------

dog | 2023-05-23 21:06:49 UTC | #3

What exactly are you committing to delivering? Noting you've already submitted submissions for HTLC and PTLC

Is this to cover work already undertaken? If not what are the outcomes you are hoping to achieve?

What are the delivery and payment milestones?

How long will it take?

What benefits will it bring to Zenon? 

Is documentation and support included?

How can you justify 150k ZNN and 1.5m QSR? How was this calculated? It is too much

Why are s the ask a "minimum"? Will there be more submissions?

How many people are working on it and who are they?

What will the distribution of funds look like?

Will you and other pillars involved abstain from voting?

Why have you submitted the proposals on chain without any engagement and linked to a forum that has only 15 registered users?

Any pillar that votes yes on this proposal in it's current format is lost

-------------------------

Chadass | 2023-05-23 21:44:42 UTC | #4

I agree there should be more visibility towards PTLC I don't even know what that is and why it's being built. Let me add a few questions:

- Why PTLC when we all know atomic swap never got adopted on LTC
- What about the UX ? How will it be developped ? 
- Will there be enough in AZ to fund this ?
- What does it means for the Zenon ecosystem
- Will there be a website
- Why the funding is so high and how many hours did you work on this ?
- Do you have credentials ?
- Are you Mr. Kaine ?
- Apu ?

-------------------------

georgezgeorgez | 2023-05-24 00:03:03 UTC | #5

Thank you for the questions.
I love seeing the community doing its due diligence.

Currently the team is focused on supporting our public testnet roll-out that just went live.
https://forum.hypercore.one/t/syrius-v0-1-0-release-candidate-1-ready-for-community-testing/72

I hope that the community can appreciate an inclination towards hands-on and accessible working demos.

I will talk with the team and start putting together some answers before our next big update.
I hope that our proposal will be evaluated under a fair and consistent standard.

-------------------------

cat | 2023-05-24 00:35:48 UTC | #6

[quote="georgezgeorgez, post:5, topic:69"]
I love seeing the community doing its due diligence.
[/quote]

just when they feel like it

-------------------------

Chadass | 2023-05-24 11:26:09 UTC | #7

I see no answers and therefore will vote no to any further A.Z requests related to atomic swaps. I encourage all the pillars to do so as this technology never got adopted and nobody is able to tell us why we should implement it. Dull p2p markets are useless.

-------------------------

Blueginger | 2023-05-24 13:13:50 UTC | #8

Hope it's not just another atomic swap.
150k znn for an archaic utility doesn't justify, even if we don't have anything else to do

-------------------------

0x3639 | 2023-05-24 13:45:22 UTC | #9

[quote="dog, post:3, topic:69"]
Why have you submitted the proposals on chain without any engagement and linked to a forum that has only 15 registered users?
[/quote]

Mr. Dog:

Don't under estimate the capabilities of a 15 person forum when 33% of those people are *rockstar* contributors. 

P2P = BigPP revolution  

Watch this if you think P2P has no use case.  Might be limited today, but we could be headed in that direction given what *could* happen with regulation in the US.  

https://www.youtube.com/watch?v=JvGOc_v7yGA&t=2s

-------------------------

Chadass | 2023-05-24 15:18:28 UTC | #10

So all you got are cheesy jokes and wild speculation

-------------------------

georgezgeorgez | 2023-05-24 23:03:51 UTC | #12

Let's start answering questions with who we are and what our purpose is:

https://forum.hypercore.one/t/welcome-to-hypercore-one/7

-------------------------

cat | 2023-05-24 23:58:22 UTC | #13

Alright, now that your team consists of 5 members, you are eligible to submit a 95K ZNN and 950K QSR proposal after completing 10 months of work. 

Btw who's the tech lead?

-------------------------

georgezgeorgez | 2023-05-25 01:18:19 UTC | #14

Among the HyperCore One team members there are no formal hierarchies or giving of orders.
All participation is opt-in.

Naturally, different team members have different talents and interests. So different team members will take on leading roles across the end-to-end delivery lifecycle.

One team member may be leading implementation in a certain area while other team members are testing, learning, peer reviewing code, and contributing to design. In a different area, the roles may be reversed.

-------------------------

georgezgeorgez | 2023-05-26 16:00:32 UTC | #15

I suppose the next question that would make sense to address is:

**Why such a large ask?**

Our holistic end-to-end delivery model means that we will work with the community to create larger milestones where the value can be experienced or shown through data.

But this model also incurs a significant amount of overhead.
While this overhead greatly enables us to deliver the value that the community needs in a fast and iterative manner, it doesn't always make sense for these things to have their own AZ proposals.

Some current examples:

- We intend to maintain production quality binary builds. This carries security, integration, and testing burdens. We've started offering public testnets and related infrastructure such as faucets and explorers.

- The go-zenon codebase includes various hardcoded IDs such as spork ids and the new bridge and administrator addresses that don't work well with testnets. So we created a backwards compatible patch that would allow these values to be configured. Over time, we will productionalize this solution. A lot of other tooling such as controllers will need to be made compatible with testnets.

- Taking a holistic approach also means being aware of other work happening in the community. Oftentimes this means testing and validating the work of others in a systematic way. It means road-mapping and maintaining dynamic plans for future work.

As the ecosystem grows, this overhead will grow alongside it. In order to justify maintaining this overhead, we need a significant commitment from the community, so that we can recoup these costs over time as we deliver incremental value. This commitment will enable the five HyperCore.One team members to focus on end user value instead of worrying about if all the incidental costs will be covered.

In the next few days, we will begin working with the community to create a milestone/payout framework that the team and the pillars will both find agreeable.

As mentioned in our previous posts, all HyperCore.One participation is opt-in.
There are also some items of work that team members have delivered or are wrapping up that will fall outside of the new milestone/payout framework.

-------------------------

DrD3 | 2023-05-26 18:12:50 UTC | #16

Ty ty for the elucidation ser. I'm absolutely certain everyone in the community is grateful for your team's efforts and dedication to our ecosystem. A couple of questions:-

i) This is a very big ask and a very specific amount- how did you come to decide upon this 150k ZNN, 1.5m QSR no.? What does it come with- how many months/years of commitment can we expect from your team? Is this a full-time commitment to the Network? Is the plan to give each of the developers on your team their own pillar(s?) to run (not against this- in fact I quite like the idea of developers running pillars and taking an active part in network governance)? 

ii) Would it be possible to get an introduction to the team (though I'm sure we should be able to hangman most of them) or for the team  members to introduce themselves?  What are their specific skillsets that they are bringing to the forefront? I do not doubt our community developers but since y'all are applying for a considerable grant- I'd like to know what all we're potentially paying for.

iii) Finally, if the "ecosystem grows" the values of the rewards that you will reap from your pillars, sentinels, or from delegating, staking or LP'ing will proportionally increase. Can we come up with a payment plan that potentially takes account of this? Perhaps your team can requests payments of this large grant in batches/instalments? This way if the price value of ZNN/QSR increases the amount requested can be reduced. This can help ensure that our AZ Warchest doesn't deplete at such an accelerated (haha) rate.

-------------------------

Shazz | 2023-05-27 07:12:29 UTC | #17

"The Future is P2P!"

Can you show a use case that has a significant, validated market demand for P2P which is currently un- or underserved, and for which Zenon NoM provides a competitive edge?

If you feel such a market exists but you need support in validating its potential, whixh one(s) specifically are you looking at?

-------------------------

0x3639 | 2023-05-27 09:45:21 UTC | #18

Are you guys curious if PTLCs can be used for something other than an atomic swap of 69 ZNN <> 420 QSR between Alice and Bob?  Don't you guys have the feeling that someone knows `EXACTLY` how we will interoperate with BTC?

-------------------------

Shazz | 2023-05-27 09:47:29 UTC | #19

Curious? Yes.
Feeling? No.

-------------------------

Bzed | 2023-05-27 11:43:50 UTC | #20

Based on the work this team has already performed, and continues to perform ie Eth Bridge dependencies(95kZNN get us what again?) + ongoing Syrius upgrades + every new problem that comes up.. we are already relying on this group for basically all ongoing development. Would be highly regarded to shut down their efforts. Negotiating the amount proposed for payment is fair though, would be a great conversation for the community to get comfy with. 

This is all aside from the fact that BTC interop is completely built around P2P so clearly i am in full support of the HCone efforts.

-------------------------

Shazz | 2023-05-27 14:17:13 UTC | #21

I see nobody trying to shut down their efforts. Just requests for more clarity and reasoning for the funding request.

-------------------------

Bzed | 2023-05-27 14:51:36 UTC | #22

Im speaking mainly to the No votes coming from otherwise non participating pillars without engaging in any sort of constructive conversation.

Though also trying to provide some clarity on the fact that we already rely on this group, what more reasoning do we need to support their work? Its already the situation were in. 

The wholistic approach means(HCone) doing all the work no one else wants to do along with some major milestones for phase 1, its no speculation this isbwhat they are already doing.

-------------------------

Chadass | 2023-05-27 19:02:12 UTC | #23

Saying we rely on them as "We rely on them to do whatever they want and we just believe without even trying to understand" then, no.

We all have incentives for this to go well. I personally vote no to what is unclear or what I disagree with. Somebody might know EXACTLY about stuffs but if that's somebody can't explain it to me he or she won't have my vote. I leave beliefs to church people.

-------------------------

shaimo | 2023-05-27 18:50:07 UTC | #24

I thought we all agreed AMM was much more important than swaps so we were going to put the dev resources there. What changed?

-------------------------

Chadass | 2023-05-27 19:05:45 UTC | #25

To me nothing changed, however there's a strong devs trend to go that way because Mr. Kaine said so. My issue is that Mr. Kaine, as usual, doesn't explain clearly the why and how. I don't really care if he knows the why and even if he's right, if I don't get it, I don't go that way. I voted no to anything P2P and will continue to do so unless I'm being proven this is really important and might see the rise of a great thing involving ZNN and BTC.

I think, long story short, Sumamu asked for a decent amount of funding, then the other team trolled with overinflated asks on A.Z just in case it passes. Not a good way to do things.

I'm okay to host Twitter spaces to challenge / discuss with anyone thinking P2P is the way to go.

-------------------------

georgezgeorgez | 2023-05-27 20:22:39 UTC | #26

Mr Kaine currently controls the Spork creation and activation process.
He has provided no guidelines or criteria on what will or won't be activated on mainnet.

An AMM does not seem to be one of his priorities so continuing to develop an end-to-end AMM solution that we don't know will be accepted does not make sense for the HyperCore.One team.

Will the community be willing to pay for work done even if it doesn't get activated?
If so, we can begin putting together milestones and a delivery plan.

HyperCore.One will chase the incentives that the community creates. The main data point we have right now is that the community will pay out almost solely based on acceptance by Mr Kaine so we will work towards what we are confident will get accepted.

A governance module for pillar driven spork creation and activation is something that the HyperCore.One team will pursue in the near future. But until pillars are willing to provide governance or we have more data points, pursuing something like an AMM does not make sense.

The P2P Revolution will be a thematic movement that encompasses far more than atomic swaps.

"Bitcoin: A Peer-to-Peer Electronic Cash System"

-------------------------

Shazz | 2023-05-27 20:38:46 UTC | #27

So as long as Kaine controls spork activation we simply disregard decentralized consensus on what needs to be developed...? I sure hope not.

Please elaborate what P2P use cases are so important and demanded according to Kaine / yourself / hypercore.

-------------------------

0x3639 | 2023-05-27 20:37:35 UTC | #28

Why is P2P Important for regulation?

https://youtu.be/JvGOc_v7yGA?t=1911

-------------------------

Shazz | 2023-05-27 20:39:50 UTC | #29

Some people seem to think that regulation is the main imnovation driver in this space. I would strongly challenge this notion and argue that regulation is an enabler at this point.

-------------------------

0x3639 | 2023-05-27 20:40:18 UTC | #30

How can the P2P Revolution use Bitcoin as a data availability layer for zBTC?

-------------------------

0x3639 | 2023-05-27 20:42:07 UTC | #31

[quote="Shazz, post:29, topic:69"]
regulation is the main imnovation driver
[/quote]

??

-------------------------

0x3639 | 2023-05-27 20:52:10 UTC | #32

I think this reads as a double positive. I do think "smart" regulation will be a good thing and will improve adoption.  Especially crypto exchanges. But if the entire system becomes KYC what's the point?  Let's just fire up a sql server and run value there.  Right?

KYC will become control. And control will mean centralization.  Over time (a long time) the only way to maintain decentralization will be p2p.  But I could be very wrong too.

-------------------------

Shazz | 2023-05-27 20:55:26 UTC | #33

Market access (fiat on& offramps) is regulated. Countries where regulations are more lenient will attract more fiat which wants to enter the market. More rigid regulation is protection theatrics and will drive capital away. Existing regulatory regimes where large amounts of capital feel comfortable (HK, SGP, CH etc) will keep their importance no matter what.

Big money doesnt care about permissionlessness. Funds, asset managers, banks explicitly ask for permission.

-------------------------

sol | 2023-05-27 20:58:48 UTC | #34

[quote="Shazz, post:27, topic:69"]
So as long as Kaine controls spork activation we simply disregard decentralized consensus on what needs to be developed…? I sure hope not.
[/quote]


As long as the community runs Mr Kaine's version of znnd, we are at his mercy to merge updates and activate them on-chain.
He will arbitrarily accept or silently ignore our contributions as long as we allow him to do so.

We cannot be certain that any code we work on will be activated in production if it hasn't been sanctioned by Mr Kaine. We need a way to transfer that power to pillars.

-------------------------

Shazz | 2023-05-27 21:23:04 UTC | #35

Cool, so "decentralization" is just theatrics until said power has been transferred. Does he have the finger on the button for that transfer as well?

If so, he should fund Hypercore team until that changes. I don't feel like getting my bags diluted for a product roadmap based on faith / dogma / leadership cult rather than logical reasoning & decentralized consensus. It's been this way long enough.

Yes, I will keep making annoying points.

-------------------------

0x3639 | 2023-05-27 21:06:36 UTC | #36

unfortunately in the US we don't have a regulatory framework.  And from what I read, very large, regulated entities, steer clear of crypto b/ there is no regulatory framework (in the US).

The less regulated markets probably drive retail demand.  But again my guess is the "real" money comes from the institutions.  And they appears to be waiting for regulation.  

I do think regulation is coming to the US and it could partially destroy the entire idea of cryptocurrency.  

I'm definitely not  saying the market is going p2p in the next year, but it's a possible outcome if regulation kills the idea of crypto.  

Look at nostr.  Imagine a global p2p messaging protocol.  It's possible.  

Forget all this.  I'm most interesting in how BTC will be a data availability layer for the P2P Revolution.

-------------------------

georgezgeorgez | 2023-05-27 21:09:53 UTC | #37

> Will the community be willing to pay for work done even if it doesn’t get activated?
> If so, we can begin putting together milestones and a delivery plan.

-------------------------

Shazz | 2023-05-27 21:23:52 UTC | #38

The US is becoming less relevant for crypto by the day, mate. Look east. Esp. For institutional flow. US funds go offshore anyway.

-------------------------

Shazz | 2023-05-27 21:13:21 UTC | #39

I would be.

-------------------------

0x3639 | 2023-05-27 21:17:12 UTC | #40

why not?  You've built an AMM.  And then kaine does not activate it b/ something is more important to him.....?

If the community wants the AMM, you deliver it, kaine does not spork, then the message is clear.  Pay for the work, and remove spoke rights from Kaine.

-------------------------

shaimo | 2023-05-27 21:50:05 UTC | #41

What does an AMM have to do with Mr Kaine or with a spork?? It’s supposed to be a completely independent product…
Sure, we do need smartcontracts for that, but we need them for many other things anyway.

-------------------------

shaimo | 2023-05-27 21:52:25 UTC | #42

If we need to fork the network each time we want to deliver a dapp then something is really wrong with our architecture

-------------------------

georgezgeorgez | 2023-05-27 21:58:15 UTC | #43

We currently only have an embedded contract runtime.
Meaning that yes, every new on-chain capability on mainnet requires a spork.

There are different tradeoffs with this architecture.
With the stated focus on extension chains, it is unclear whether or not an AMM on mainnet would be accepted via spork.

-------------------------

Chadass | 2023-05-27 23:23:09 UTC | #44

This discussion is moving slowly toward Kaineless extension chains.

-------------------------

0x3639 | 2023-05-28 00:27:33 UTC | #45

Just wanted to elaborate a little.

Kaine has identified certain deliverables to achieve Phase I.  An embedded AMM is not on that roadmap.  In addition, Kaine has said he wants to keep the base layer as light as possible.  

That means we need sidechains or L2s to run an AMM if we want to deliver the roadmap kaine is recommending.  However, the community is asking for an AMM now.  George has spent time on the AMM.  The only way to deliver an AMM now is with an embedded contract and spork.  

He is wondering, will Pillars fund an AZ for his work if he finishes the AMM, submits the contract to github.com/zenon-network/ and kaine fails to generate a spork ID.  

For me, the answer is YES.  I would agree to fund the AZ for that work.  However, if the community speaks up and says they no longer want an embedded AMM and will wait several months (years) for an AMM then maybe we should reconsider.  

We can always do the embedded and migrate to L2 when it's available. And, we can also discuss removing the spork rights from kaine and give it to the pillars.  I will note, that some very inactive pillars immediately voted NO to @georgezgeorgez [6/6] AZ P2P Revolution....  

So, maybe we have more active pillars than we think.

-------------------------

Chadass | 2023-05-28 00:36:31 UTC | #46

Let me rephrase then : Whatever Kaine says should go through community consensus and for this to happen his words as holy as they are needs to be turned into proper explanation. I don't really care about him or his takes if I can't understand what he wants and why and this feeling is growing stronger in the community. There are strong church like behaviors in crypto community, but Kaine isn't a god and we should push him to explain himself more and more. Or else this is nothing more than a company ran by a CEO and the whole Bitcoin ethos and decentralisation narrative might as well collpase on itself.

-------------------------

coinselor | 2023-05-28 04:54:44 UTC | #47

I'm sure sumamu and co will deliver an EVM-compatible L2 relatively soon. I don't see the rush to have a crude AMM directly on NoM, we don't even have the users for it (or a bridge to onboard them). Let's get the bridge and wallets battle-tested, then remove its LP limits and open the floodgates with a working EVM compatible L2 + marketing.

It would be a way better product if we fork the smart contracts and the front end of a successful product like Uniswap, than to build it from scratch in NoM. 

I'm not trying to put down the work George has already put into it, but just being practical while trying to achieve the better outcome.

P2P is music to my ears.

-------------------------

0x3639 | 2023-05-28 11:01:55 UTC | #48

[quote="coinselor, post:47, topic:69"]
P2P is music to my ears.
[/quote]

P2P revolution baby!  

Setting aside whether we want / need an embedded AMM, I do believe dynamic plasma is a very high priority. I say that only because Kaine says it every time he gets the chance.   

So my vote would be to focus on dynamic plasma now, and let's see what comes of sidechains / L2s.  We can then revisit the discussion of embedded vs L2 after dynamic plasma is done.

-------------------------

0x3639 | 2023-05-29 01:00:52 UTC | #49

[quote="0x3639, post:45, topic:69"]
Kaine has said he wants to keep the base layer as light as possible.
[/quote]

RIP AMM... back to P2P Revolution. :green_heart:

https://t.me/zenonnetwork/289617

-------------------------

Chadass | 2023-05-29 02:15:20 UTC | #50

Anything Kaine says must go through a vote anyway. So not RIP until vote.

-------------------------

sol | 2023-05-29 05:29:54 UTC | #51

[quote="sol, post:34, topic:69"]
As long as the community runs Mr Kaine’s version of znnd, we are at his mercy to merge updates and activate them on-chain.
[/quote]

The governance update will probably allow Mr Kaine to retain some measure of control for a period of time, until pillars vote for sovereignty.

Personally, I don't think Mr Kaine would carry out the will of the community, even if there was overwhelming support for this feature.

-------------------------

Shazz | 2023-05-29 04:40:05 UTC | #52

Kaine's word equals 30 pillars, so RIP your decentralized consensus.

Jokes aside, it makes sense not to do the same shit as everyone else and bloat the base layer.

-------------------------

Chadass | 2023-05-29 12:21:08 UTC | #53

Of course but the reasoning should be it make sense not muh Mr. Kaine said so

-------------------------

Shazz | 2023-05-29 16:13:31 UTC | #54

Ofc

-------------------------

Bzed | 2023-06-06 15:15:23 UTC | #55

CEX's crumbling around us but P2P revolution v1 not accepted, im not mad just disappointed. Does HCone have any plans to resubmit? P2P is the hero we need i hope some pillars can come together on this.

-------------------------

Chadass | 2023-06-06 15:27:45 UTC | #56

P2P revolution was a troll toward the bridge asks.

-------------------------

georgezgeorgez | 2023-06-06 15:38:08 UTC | #57

No. We are refining the proposal.

-------------------------

Bzed | 2023-06-06 15:56:42 UTC | #58

Team of community members working in the open asking to get paid for their work (Sol doesnt even have a pillar yet) compared to team of anon rockstars with zero proven interest in the project getting immediate approval. 

I am not even judging the launch im just commenting on the different approaches and wondering honestly who is trolling who.

-------------------------

Chadass | 2023-06-06 17:46:21 UTC | #59

One project made sense, the other way less as I, personally, can't see where this whole P2P thing is going to be used. To get my vote, I'd need more clarity, especially considering how atomic swap was never adopted on LTC. The decentralized ideology has to face the market reality and the user experience to be appreciated as it should. It's not the case yet. I'm totally open to discuss this anytime. Mr. Kaine said so won't be enough. Tell me a good story about P2P and I'll buy in.

-------------------------

SultanOfStaking | 2023-06-08 01:38:48 UTC | #60

Also need to see rationale for amount of funds requested - going to start voting no for anything that doesn't have this clearly explained

-------------------------

