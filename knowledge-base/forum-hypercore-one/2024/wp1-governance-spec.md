Thread: wp1-governance-spec
georgezgeorgez | 2024-11-05 15:13:59 UTC | #1

Starting this early to respond to everyone pinging me about 
https://forum.hypercore.one/t/universal-governance-module-proposal/544/2

This is good
Similar to my draft code but we can use his as the starting point for the governance embedded, and of course reward with incentivizes.

Based on the work items, we can see that a spec and the implementation are only part of what’s needed for the work to be useful. A systematic way for testing, consensus, and acceptance is crucial, and that’s something missing that hopefully we can solve here.

Anything touching sporks especially requires extra scrutiny since activated sporks that aren’t implemented will halt the network.

I’ve read through his code and regarding the actual design itself:

The design is simple, which is a perfect starting point. But it may be too simple.

I like the generic action method. But one thing I got stuck on for design is if all actions should have the same voting parameters.

Are all governance actions of equal importance? Does a 51% voting threshold make sense for all actions? Should they all have the same voting duration?

If the answer is no, then the requirements become more complex. Of course, this could be a version 1 vs version 2 discussion. But it should be a conscious decision to defer that complexity.

In any case, I still think the right path for new contracts should be on an extension chain first to get battle tested.

-------------------------

georgezgeorgez | 2024-11-05 15:21:57 UTC | #2

One benefit of an extension chain like hyperqube_z is that we can quickly iterate. We can deploy multiple governance contracts and then once we settle on one we like for the long term, that can be the candidate for mainnet.

-------------------------

georgezgeorgez | 2024-11-05 15:48:18 UTC | #3

One more thing I just remembered from when I was messing around with an implementation a while back. 

Currently sumoshi's implementation hardcodes a send value of 0 ZNN.

That is probably fine to handle all explicit governance methods, e.g. admin functionality on the bridge, but it does not seem outside the realm of possibility that some actions will require value transfer as well. Maybe there are some actions that are not limited to governance but still useful for governance to interact with.

For example, maybe we want governance owned tokens. ZTS creation requires 1 ZNN to burn. ZTS is not the best example since the owner can be updated after the fact, but hopefully you get my point.

Again, possible version 1 vs version X discussion. But let's be thorough about requirements as much as we can and consciously include or exclude from scope.

-------------------------

georgezgeorgez | 2024-11-07 02:39:50 UTC | #4

https://forum.hypercore.one/t/universal-governance-module-proposal/544/8?u=georgezgeorgez

Here @sumoshi21 makes the KISS argument. Keep it Simple Stupid.
And I think it's a very reasonable posture to take.
He argues to limit the scope of governance to explicit governance methods which would remove the need to consider value transfer.

However, simplicity cannot outweigh network security.

I asked earlier if it makes sense for all governance actions to be considered equally.
My opinion is no. We will have Type 1 vs Type 2 decisions. Some changes like sporks are existential and can halt or fork the network, while some changes in network variables only change relative winners and losers. Does it make sense to have the same quorum requirements and voting periods for both kinds of governance decisions? My opinion is no.

Regarding 51%, one comment sumoshi makes is:

> If you can’t count on them to vote, then you can’t count on them to upgrade the node, and then we’ve got bigger problems



Robust protocol design means anticipating worst case problems. Yes it's a big problem, but we have to provide some sort of answer.

Let's consider Bitcoin. Bitcoin PoW is open and decentralized because if a portion of miners drop out, the protocol continues to function just fine with the existing hashrate (albeit with less security), and new hashrate can come in from anywhere. PoS is not the same.

@sugoibtc brings up concerns that 51% may be too high of a threshold. And for Type 2 decisions or rubber stamping that doesn't materially affect individual pillars, it may be a valid concern.

For Type 1 decisions, I actually have the opposite concern. That 51% may be too low. Many PoS consensus mechanisms networks are only provably (mathematically) secure assuming a supermajority of honest actors or 67%. No one has done such rigorous analysis on Zenon but supermajorities are often the standard.

Politically when it comes to big changes, 51% has a big chance to fork the network. It is not a resounding consensus. Will pillars who lose 49% to 51% choose to just lay down? Especially if delegators and other network participants agree with them? It is very plausible that they choose to fork and then win in the long term. It's much less plausible with a supermajority.

(We haven't even gotten into governance which includes other actors, something many community members want considered. I personally think for network security that hard binding votes should be restricted to pillars due to the burn requirements and skin in the game.)

One possible solution is to start with a generic action method like sumoshi has but to give it a dynamic quorum requirement. It starts with supermajority quorum and YES vote requirement with a relatively long duration, but after a certain point if it doesn't meet quorum then every 2 weeks, quorum drops by a certain amount/percentage. This would allow Zenon to be robust and survive without a hardfork if we lose significant pillars. This would be the path for Type 1 decisions and the the default governance method.

For Type 2 decisions, perhaps it would make sense to implement other methods in the future that are limited in governance scope with less stringent quorum requirements. Basically a whitelist of safer governance decisions.

---

One concrete suggestion on sumoshi's proposal is that perhaps it makes sense to keep the 1 ZNN requirement but also require the vote be initiated by a pillar.

-------------------------

georgezgeorgez | 2024-11-06 17:13:03 UTC | #5

Thank you @sumoshi21 for considering my feedback.
https://forum.hypercore.one/t/universal-governance-module-proposal/544/9?u=georgezgeorgez

I agree that adding value transfer is something we can likely rule out of scope. I did give an example of use case though with ZTS creation if we want a governance owned ZTS to call Mint etc. To create a ZTS directly, it would require a 1 ZNN burn. This is not possible through AZ as you suggest since it requires specific data as well.

And also this functionality may make more sense on extension chains or when interacting with extension chains.

The suggestion for dynamic quorum would be for robustness. It's very likely that over the years pillars will stop functioning but not deconstruct (if people die without succession plans). Likely we will need a consistent mechanism to take them out of the pillar pool for both momentum creation and voting quorums, with a way to get back in (e.g. a signature of liveliness).

Consider the following: 

Let's say we get a bunch of pillars in China. 40%. But then China decides to completely cut off outside internet access. We can't reach 66% + 1 for an upgrade. We can't spork to lower the threshold since that would require the same threshold. Without a dynamic quorum, a hardfork would be required. And that could be acceptable given the circumstances. I am providing a possible solution for network survivability without hardforks.

Dynamic quorum also means people need to either vote NO for changes or get out of the way for progress. Someone who can't be bothered to vote may be bothered to upgrade if they see everyone else is. Greater momentum. Enough time would need to be given however.

-------------------------

georgezgeorgez | 2024-11-06 17:20:28 UTC | #6

If we are to remove dead pillars from quorum requirements and pillar momentums. It is doing dynamic quorum at a higher level. The percentages may not need to change then.

-------------------------

SultanOfStaking | 2024-11-06 19:36:50 UTC | #7

Dynamic quorum makes sense starting at supermajority. Would be in favor of caging inactive pillars but they should have a path to becoming active again

-------------------------

georgezgeorgez | 2024-11-06 18:35:04 UTC | #8

Yeah my thought was after a certain number of epochs of X% momentum production. (X could be Zero, since delegation mostly handles the X > 0 situation), they get caged. Then after a duration of time, they can sign a transaction to get uncaged.

Perhaps there could be separate cages for governance and for momentum production.
It could be the case where pillars want to be active momentum producer, but a bug is stopping them. Removing them from governance prematurely could hinder resolution of the issue.

-------------------------

georgezgeorgez | 2024-11-06 18:38:19 UTC | #9

Dynamic quorum is possibly a dangerous idea. I am not married to it. But something to be considered.

-------------------------

SultanOfStaking | 2024-11-06 19:45:26 UTC | #10

We had a pretty vibrant pillar community during the previous bull. I do think that once we start getting momentum many will engage once more. 

Agree on the succession plan front + desire / capability to maintain once requirements grow. I could go either way on dynamic quorum (use as v1 or if v1 being a straight supermajority fails) but am in favor of caging inactive pillars with a window similar to revocation window either way.

-------------------------

georgezgeorgez | 2024-11-07 15:20:23 UTC | #11

It could be informative to try and run through a vote off-chain. Can we reach supermajority? Can we reach simple majority?

If someone has a proposal they should try and demonstrate that it won't be stuck as soon as it launches.

For dynamic quorum, we know that after a certain (i suggest a fairly extended) period of time, that proposals without opposition will pass. It does not mean that minority can pass proposals if there is opposition.

It's not in scope for WP1 right now, but one thing I'm planning to deploy on hyperqube_z is a simple polling contract that any address can vote on.

For sporks, I am fairly adamant that we have to at least try and achieve supermajority of active pillars.

-------------------------

georgezgeorgez | 2024-11-08 00:32:43 UTC | #12

@edgepillar 
regarding https://forum.hypercore.one/t/universal-governance-module-proposal/544/11?u=georgezgeorgez

Pillars require a burn which means they have to be committed to long term.

Other form of participation are much more open to attack.

For example, if we use pillar weight/delegators, then it opens up a strategy of buying Put options on ZNN, borrowing ZNN on margin, then doing destructive governance and making money off of the puts, then returning the borrowed ZNN. This strategy is even more effective if the interest on the borrowed ZNN is also ZNN.

Regarding sentinels, I think it's too early to consider them. We should implement their primary function which will help us understand what other roles they should play.

-------------------------

edgepillar | 2024-11-08 09:53:09 UTC | #14

[quote="georgezgeorgez, post:12, topic:545, full:true"]
@edgepillar 
regarding https://forum.hypercore.one/t/universal-governance-module-proposal/544/11?u=georgezgeorgez

Pillars require a burn which means they have to be committed to long term.

Other form of participation are much more open to attack.

For example, if we use pillar weight/delegators, then it opens up a strategy of buying Put options on ZNN, borrowing ZNN on margin, then doing destructive governance and making money off of the puts, then returning the borrowed ZNN. This strategy is even more effective if the interest on the borrowed ZNN is also ZNN.

Regarding sentinels, I think it's too early to consider them. We should implement their primary function which will help us understand what other roles they should play.
[/quote]

I honestly don’t think it’s too early. It could be very useful in a situation where Pillars don’t have a very good voting participation. I don’t see anything wrong with Sentinels already taking this role in addition to their main role. 

In addition, the second highest QSR cost and lock mechanism can easily prevent possible attacks.

Since it has 1/3 of the setup cost (5k ZNN/50k QSR) compared to legacy Pillars (15k ZNN/150k QSR), it may be logical to calculate the vote weight in the same way.

-------------------------

georgezgeorgez | 2024-11-08 15:10:58 UTC | #15

Borrow time can easily exceed lock times and with a successful attack, the carrying cost on the borrowed assets can go to 0. It can have a cascading effect.

With a company, something could get shorted to 0 but there is still positive book value. The company's governance isn't immediately tied to share price. And there are usually breakers in place.

With a decentralized networks, if governance is tied purely to stake, you could short the price to 0 and destroy the network via governance in a cycle. And there's no breakers.

---

I completely agree that we need to give all classes of network participants a political voice. But that doesn't always mean a direct vote. As we integrate more PoW into the network, we probably need not only a supermajority of pillars but a majority of hashrate as well.

That could be an indirect factor that pillars have to consider, or hashrate could be baked into governance itself. Keep in mind that once Sentinel requirements go live, many of the people running sentinels now which are doing nothing, might not have the operational requirements to actually run it.

-------------------------

georgezgeorgez | 2024-11-14 08:30:29 UTC | #16

Taking an initial vote to gauge what the pillars would like to see:
https://forum.hypercore.one/t/wp1-governance-spec-feature-vote/554

-------------------------

