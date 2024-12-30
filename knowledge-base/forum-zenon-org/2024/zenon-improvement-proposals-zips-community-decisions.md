Thread: zenon-improvement-proposals-zips-community-decisions
romeo | 2024-03-27 15:20:11 UTC | #1

As most of you would be aware I had an Accelerator-Z proposal in to develop a framework for our incumbent improvement proposal process:

https://forum2.zenon.org/t/proposal-zenon-improvement-proposals-zip-framework-development/592

I've finalized the first version of the document and it's circulating for review now. Annex A in the framework lists some key community decisions that need to be made prior to implementing the proposed stage 1 ZIP process, listed below:

![Community Decisions|538x599, 100%](upload://seMMDbuIuUQtJ2JNu8mrkDaQiWv.png)

We need to start thinking about how we formalize agreement on this (KDP002) and also start a discussion on alternate views on any of these points. If it looks like there is not a clear agreement on any item I'll create a separate post and forum vote for each so that we can get a clearer picture prior to any formal on-chain activity.

After this - we need some of the developers with knowledge of the codebase to start putting together a plan on how a technical implementation would look. We likely all expect the core developers to make the next protocol change themselves, but after that how would we as a community deploy changes to the codebase? Has anyone mapped out how this works yet? Perhaps we will get a good insight into the process if the core devs complete a ZIP with the implementation plan detailed for NoM Phase 1

-------------------------

zyler9985 | 2022-07-25 12:35:39 UTC | #2

For KDP008: Should pillars be the only voting power for on-chain consensus within the NoM.

Is there an alternative scenario that's viable and worth discussing? 3 reasons I ask:

1-- many legacy pillars have not transitioned to alphanet
2-- of the pillars that did transition, at least half have never voted at all
3-- some pillars are quite wealthy and the top 30 vs not top 30 position may not be a strong enough incentive-system to sway their behaviour much

What about a scenario where every single address with ZNN can vote? Something like, if enough addresses vote yes, and their combined amount of ZNN is 50k, that constitutes 1 yes vote, and 70k znn is still only 1 yes vote, but 100k is 2 yes votes. Or sentinels get 0.1 of a vote each? 

I don't have a strong opinion on this, just wondering what other people might think about it. I'm sure the current system has been well thought out.

-------------------------

romeo | 2022-07-25 12:40:26 UTC | #3

I thought about that in detail, and yes it's a valid question for the future. I feel the core devs are pretty clear in their intent for the Pillars to be the governance actors for "the DAO of DAOs" - and as time progresses hopefully some of the issues you raised will organically improve (pillar participation etc.).

You could even have a joint model where Pillars get 50% of the vote and then token holders the rest on some kind of weighted system - but ideally in the long term I hope we can make the Pillar model work via delegation that actually influences Pillar votes rather than holders chasing max returns

-------------------------

zyler9985 | 2022-07-25 12:57:40 UTC | #4

That's definitely their intent, but I'd love to see their rationale for it and how flexible they are with tinkering with it. Eg. when we get more pillars (from vested pillars for example) I wonder if top 30 will be too competitive to get into, and many will stop trying? Should it be top 40? Should the top 10 get an extra boost? It's not just how they vote, it's also what they're doing for the ecosystem and delegators may want to support them. 

And that's an interesting point about the issue of yield chasers who would toss their governance power for an extra 1% APY which is so short-sighted ... I think we need educational content to address this issue and discuss zenon governance generally

-------------------------

cryptocheshire | 2022-07-25 13:22:27 UTC | #5

my $0.02:
- 1 pillar = 1 vote is a great start
- 1 sentinel = 1/3 vote would be a logical extension of 1 pillar = 1 vote
- giving delegators the right to vote through delegation is difficult because it potentially allows large holders who self-delegate to over-proportionally influence votes. Also, it would allow pillars to just "buy" voting weight through short-term increase of reward sharing. After all, most delegators have shown to not have any pillar loyalty but just chase the highest yield.

-------------------------

romeo | 2022-07-27 03:45:50 UTC | #6

the other issue with having ZNN holders vote is the consensus metrics behind it:

Say Pillar vote is 50% and ZNN vote is 50%:
- What if only 5% of circulating supply vote? Then you would have 5% of holdings count for 50% of governance.
- If you set a threshold for minimum participation (say 50% of circulating supply) how do you ensure you can meet the minimum? What about the orbital fund, or ZNN locked in Pillars/Sentinels?

A governance token solves most of these issues if it's a 1 for 1 allocation, but then you've got issues of people having multiple addresses and wallets, proof of humanity etc.

The Pillar/Delegation model seems the best fit now and potentially long term

-------------------------

DrD3 | 2022-07-29 10:26:56 UTC | #7

If we're talking about governance tokens as a substitute for pillar votes as mentioned in section 5.8 (also KDP009)- we could require that the proposer pay a price (burn a znn as during submitting a proposal) to generate/mint tokens which are delivered to each wallet (pillar and delegator) that registers to vote. Pre-determined addresses- designating a yes or no- can then be created and voters can send their tokens to either one (ensuring the entire process is transparent and on-chain).

The advantage with this model would be that each proposal would have its own token to vote with instead of having to deal with the chaos of recollecting the "governance tokens" after each vote.

-------------------------

DrD3 | 2022-07-29 10:59:49 UTC | #8

Idk I'm conflicted, on one hand its completely fair that those with more skin in the game should get the right to participate in the voting consensus. On the other hand, I want my zennies worth of commitment to NoM to be considered proportionally when a vote takes place. Instead of voting through delegation I would prefer to vote through a "voting token" 

Instead of allocating an equal 50-50% of consideration I would combine @cryptocheshire 's model of:
>  1 pillar= 1 vote
>  1 sentinel= 1/3 vote
* 1 sentry=  a fifth of a 1/3 vote (or some shit)

with a "governance token" model or "voting token" model (as I've mentioned elsewhere) for zenon holders. With this model we could gauge general community sentiment towards the proposal. 
* If 50% participants or more approve- then the draft proposal can pass (provided it has been approved by the pillars, sentinels, and sentries).
* If 50% participants or more disapprove- then the proposal must be deferred and re-evaluated taking the community opinion into account.

I agree this still has problems some that @romeo has highlighted:

> A governance token solves most of these issues if it’s a 1 for 1 allocation, but then you’ve got issues of people having multiple addresses and wallets, proof of humanity etc.

But it seems like a fairer way to ensure that every community member has some say in how he/she would like their favourite L1 DLT to operate/evolve.

-------------------------

Zyll | 2022-07-29 20:23:12 UTC | #9

Another option would be to build in the option for pillars to turn over voting to their delegates. It could be weight based on ZNN or not as you see fit. Maybe every 100 or 1000 ZNN gets a vote? 

If the operator doesn't care enough to vote themselves, they could let the popular vote of their users count as their pillar's vote. They'd have X amount of time to overrule the vote and of course the delegates should know what their vote was vs the owner's so they can decide who agrees with them. 

I guess this gets a bit like politics, but for those owners that don't care, it may be a viable solution to increase pillar votes. 

Of course it would require a lot of work to implement.

-------------------------

sultanofstaking | 2022-07-30 11:51:50 UTC | #10

A DAO pillar... if the pillar does not vote for 2 consecutive proposals voting option appears on syrius of their delegators who then determine how the pillar votes

-------------------------

romeo | 2022-07-31 11:50:18 UTC | #11

[quote="sultanofstaking, post:10, topic:869, full:true"]
A DAO pillar… if the pillar does not vote for 2 consecutive proposals voting option appears on syrius of their delegators who then determine how the pillar votes
[/quote]

this is actually a very interesting idea

-------------------------

zyler9985 | 2022-08-01 08:41:50 UTC | #12

Something that wouldn't require any changes to the protocol, but would allow delegators more active participation ...

Someone sets up a yes pillar and a no pillar, called yes and no, shares 0/0 rewards always
Whichever pillar has more weight delegated to it at the time of a new decision, (coordinated via a twitter /telegram page for both), will be their vote, and the other pillar abstains

-------------------------

zyler9985 | 2022-08-01 08:44:57 UTC | #13

This would be done in good faith, the pillar operator would choose to do this.

If they had the money, they could even set up multiple yes and no pillars, but same principle where they add up the weight of the yes vs no pillars, and they will abstain from the four no pillars if the yes pillars have greater weight
it's 0/0 rewards, and the weight would have a snapshot taken at a pre-determined time, then delegators can go back to their regular pillar after the snapshot

-------------------------

sultanofstaking | 2022-08-01 12:11:07 UTC | #14

I have been thinking about this for some time. If I ever launch another pillar it would likely be community ran and delegators determine how the pillar votes. To be transparent there is no way I am burning another 150k QSR anytime soon. Need to see how the economics shake out to determine if this is beneficial, but if we developed something like I mentioned above it would allow for any pillar to "flip the switch" to allow delegators to vote and would ensure inactive pillars can still play a role in governance. Maybe a future ZIP :)

-------------------------

coinselor | 2022-08-01 13:33:41 UTC | #15

sultanofdaos

-------------------------

0x3639 | 2022-08-01 23:23:49 UTC | #16

#fliptheswitch

Love it

-------------------------

