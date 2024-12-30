Thread: deprecation-plan-for-legacy-wznn
sol | 2024-03-27 15:19:51 UTC | #1

Many returning aliens have lamented their forgotten holdings on BSC and I think it's time to address the technical debt.
I'm sure the community's uncertainty hasn't instilled much confidence in these folks; it may influence their decision to leave or stay. 

Let's discuss some options.

[details="Option 0: Status quo"]
Thanks for playing!
[/details]

[details="Option 1: Swap on BSC"]
- Deploy a contract to BSC that accepts the old token as input and reimburses the same amount to the user
- Dependency: bridge must support BSC
- Cost: inexpensive
- Time: unknown
[/details]

[details="Option 2a: Snapshot + Claim on BSC"]
- Take a snapshot and deploy a merkle tree contract to BSC
  - Context: [Snapshot](https://github.com/gweidart/ERC20-snapshot) and [Contract + Frontend](https://github.com/Scream-Finance/merkle-airdrop-bdei/tree/master)
- Dependency: bridge must support BSC
- Cost: inexpensive
- Time: unknown
[/details]

[details="Option 2b: Snapshot + Claim on ETH"]
- Like 2a, but deploy a merkle tree contract to ETH
- Cost: relatively expensive for the user
- Time: any time we want
[/details]

[details="Option 2c: Snapshot + Claim on extension chain"]
- Like 2a, but deploy a merkle tree contract to the extension chain
- Dependency: the extension chain's mainnet must be live
- Cost: inexpensive
- Time: tbd
[/details]

[details="Option 3a: Private Reclaim on NoM"]
- Host a service that allows users to sign a message with their Metamask wallet and claim ZNN on NoM
- Private ledger
- Dependency: service provider manages frontend and backend
- Risk: service provider is trusted to manage funds responsibly
- Cost: feeless
- Time: any time we want
[/details]

[details="Option 3b: Public Reclaim on NoM"]
- Like 3a, but the ledger is published and auditable
- Dependency: service provider manages frontend
- Risk: service provider is trusted to manage funds responsibly
- Cost: feeless
- Time: any time we want
- Downside (privacy): BSC <-> NoM address relations will be published on-chain
[/details]

I've taken the initiative to [capture a snapshot of legacy wZNN](https://github.com/Sol-Sanctum/legacy-wznn-snapshot/tree/master) from the time of its inception to the block after the last legacy bridge transaction.
Whether we use this data or not is up for debate.

------------

After much deliberation, I'll open up a poll to gauge community feedback.
I'd recommend reading the thread before voting.

Depending on the result, we will probably follow up with a pillar vote to reinforce the decision.
The plan will likely be carried out in 2024-2025.

[poll type=regular results=always public=true chartType=bar close=2023-12-12T05:00:00.000Z]
# What should we do with the 87k ZNN?
* reimburse holders with a snapshot
* reimburse current holders
* do nothing
[/poll]

-------------------------

romeo | 2023-11-22 08:16:44 UTC | #2

Thank you taking initiative on this @sol 

Can we confirm, when the bridge was depreciated was all the locked ZNN in the bridge transferred to the AZ contract? And that for every wZNN on BSC there was an equal amount allocated on the NoM?

If so to me it makes sense to release equivalent znn to anyone who can prove they held the wZNN on BSC before your snapshot - perhaps with a percentage penalty for the hassle, which will remain in the AZ contract

Claiming would be on a case by case basis. Proof can be a tx to a specified wallet from the prospective wZNN wallet?

Just throwing out some thoughts for discussion

-------------------------

sol | 2023-11-22 14:26:56 UTC | #3

I can't find the transaction but Sumamu provided some insight [here](https://t.me/zenonnetwork/301946).

We should have enough ZNN to reimburse all legacy wZNN holders.

-------------------------

coinselor | 2023-11-22 15:38:16 UTC | #4

Post-snaptshot cases:

- User thought it was going to 0 given price action and sold at a loss
- User found out bridge was deprecated and tokens useless and sold at a loss
- User bought not knowing bridge was deprecated and tokens useless and held
- User knew tokens were useless and yolo bought

Regardless of the situation, if we go with the snapshot route, we make all these and similar valid "market" actions invalid. 

I think we should choose the cleaner option moving forward, whichever requires 0 explanation. I'm done explaining stuff in the future: "yeah, if you were in the LP and holding wZNN previous to the summer solstice, you get xZNN."

 To me we either choose:

- Thanks for playing!

or

- Make every wZNN on BSC whole wherever (extension chain, private ledger, public ledger, etc)

-------------------------

dat_she_pepe | 2023-11-22 17:26:07 UTC | #5

The later would be catastrophic. People had one year.

-------------------------

sol | 2023-11-22 17:57:27 UTC | #6

[quote="dat_she_pepe, post:5, topic:1686, full:true"]
The later would be catastrophic. People had one year.
[/quote]

Better we deal with this sooner than later.

If we don't reimburse these holders, the network will have effectively stolen 87k ZNN without any notice.
The excuse of "they had one year" was only for transferring tokens from BSC to NoM, not entirely forfeiting those funds to the network. We never said that those tokens would be void. 
The penalty for not adhering to the instructions at the time was being locked out of NoM until we devise a plan -- this plan we're debating now.

We have the ability to make them whole.
I believe this is the right thing to do and people will appreciate that.

Personally, I think we should snapshot and announce the existing tokens are absolutely worthless, so people can pull their liquidity. We may be deploying a replacement wZNN on BSC in the future and this legacy contract could complicate things.
I don't think we should reward speculators that would profit from other people selling at loss because of Mr Kaine's bridge closure.

Or we announce the BSC token is an isolated proxy investment for ZNN and will be redeemable for a native version in the future. The supply cannot change, people can add liq and trade if they want.
Again, I think some people will be upset if we suddenly support this market after abandoning it.

[quote="coinselor, post:4, topic:1686"]
I’m done explaining stuff in the future: “yeah, if you were in the LP and holding wZNN previous to the summer solstice, you get xZNN.”
[/quote]

That doesn't sound very complicated to me. "We snapshotted this block height, claim your tokens here."

-------------------------

coinselor | 2023-11-22 18:07:04 UTC | #7

[quote="sol, post:6, topic:1686"]
I don’t think we should reward speculators that would profit from other people selling at loss because of Mr Kaine’s bridge closure.
[/quote]

Aren't you basically rewarding people who said "screw this I got rugged again and sold after the snapshot?" I don't understand why this market participant is more valuable than the others.

The volume is not 0. That market has moved for a long time. We can see this in the amount of people that have joined tg lately. 

[quote="sol, post:6, topic:1686"]
Or we announce the BSC token is an isolated proxy investment for ZNN and will be redeemable for a native version in the future.
[/quote]

is this a fancy way of saying we make every wZNN on BSC whole?

Listen, whatever decision we take, the second it becomes "official" the market will react: 

If we forfeit the tokens, the market goes to 0 from 30 cents
if we announce a snapshot, the market prob doesn't move much. We actually want this to go to 0 or arbitrage to parity with ETH wZNN. That's a lot cleaner, imho.
If we officially support BSC wZNN it will be bought and either arbitraged down or up into the wZNN ETH liquidity when markets get connected.

-------------------------

sol | 2023-11-22 18:25:49 UTC | #8

[quote="coinselor, post:7, topic:1686"]
Aren’t you basically rewarding people who said “screw this I got rugged again and sold after the snapshot?” I don’t understand why this market participant is more valuable than the others.
[/quote]

Essentially, we're paying for Mr Kaine's poor communication and lack of support.
Anyone that failed to bridge in time was holding an unsupported token; I wouldn't blame them for dumping. 
Those tokens were valid up until Mr Kaine closed the bridge. In my mind, they should be able to claim the full value of their holdings, even if they made a little profit afterwards.

I don't see why we should be rewarding trading bots and speculative degens, the ones who were producing trading volume until now. The entire community had decided to abandon the token, following Mr Kaine's lead. No reasonable person would have bought that token unless they thought we'd suddenly announce support one day.

-------------------------

Stark | 2023-11-22 20:01:00 UTC | #9

Option 0 is the wisest path, at this time.
 
In 3 years there will either be very large transaction volume, or none at all.

In due time, we will have ample resources, or none at all. As a decentralized project, we should operate with the absolute lightest effective touch. Options 2 and 3 seem heavy handed to me. Option 1 requires a new contract and bridge.

 Mt Gox is the analog.

Let nature takes its course. This isn't for us to solve, right now. When the solution finds its time, it will be very easy to realize.

-------------------------

sumamu | 2023-11-22 20:40:00 UTC | #10

First of all thank you @sol for this initiative.

Clearly deprecating the BSC.wZNN token can't really happen because even if the active community considers it deprecated, the holders could always come back and argue about it.

So as long as there are any holders, there's always a chance for this to happen, as we've already seen.

Therefore, as much as I would've liked to solve this situation without a BSC bridge, the snapshot solution will only be temporary, because there will still be some BSC.wZNN holders since it can still be traded.

What happens when new holders BSC.wZNN holders join the community and argue that they didn't know?

The only permanent solution is for the BSC.wZNN supply to go to zero.

So our options for achieving this would be:
- snapshot only BURNED tokens and take the snapshot one supply goes below a threshold
- bridge to BSC and deploy a simple contract that allows holders to burn the old BSC.wZNN and claim the new one

___

On the other hand, while writing this post, I've also been thinking that very few BSC.wZNN holders have actually expressed interest, and it's been a long-known fact that the BSC.wZNN token has been deprecated.

Deprecating a token has worked for other projects, so why not this one?

-------------------------

0x3639 | 2023-11-22 20:49:07 UTC | #11

[quote="sumamu, post:10, topic:1686"]
Deprecating a token has worked for other projects, so why not this one?
[/quote]

The rune token on BSC and ETH were deprecated over a period of time like we did.  Having all these tokens out there creates overhead and I don't think it's unreasonable for a "small" but mighty project to sunset a token as conditions change.  I think people who invest in small cap crypto projects must expect stuff like this to happen.  It's a regular occurrence.  

I have legacy tokens that I expect this to happen and I check into TG or Discord ever few months just to make sure they aren't going to burn their tokens.  

Not sure the answer, but dedicating a lot of resources to this right now could be a distraction.  Do we want zUSDT, side chain, zk, or bridge to BSC?  Tough decisions.  Maybe the legacy token holders should gather a bounty to compensate a dev to recover them.  As was mentioned in TG, we are all community members with limited resources.  We cannot go to our "financial partner" to fund this.

-------------------------

sol | 2023-11-22 20:55:37 UTC | #12

[quote="sumamu, post:10, topic:1686"]
What happens when new holders BSC.wZNN holders join the community and argue that they didn’t know?
[/quote]

Depends on the outcome of this thread but I would assume the response will be "You bought the wrong ticker, silly!"

[quote="0x3639, post:11, topic:1686"]
I check into TG or Discord ever few months just to make sure they aren’t going to burn their tokens.
[/quote]

Many of us have grown accustomed to this, but my point is that we should decide how we will use those 87k ZNN. We have the ability to reimburse, but will we collectively decide against that?

-------------------------

sol | 2023-11-22 20:58:36 UTC | #13

[quote="Stark, post:9, topic:1686"]
This isn’t for us to solve, right now. When the solution finds its time, it will be very easy to realize.
[/quote]

I'd like to clarify: most of the options have dependencies that we will probably have in the future.

Merely knowing the plan is better than not having one at all.

-------------------------

Stark | 2023-11-22 20:59:03 UTC | #14

[quote="0x3639, post:11, topic:1686"]
I have legacy tokens that I expect this to happen and I check into TG or Discord ever few months just to make sure they aren’t going to burn their tokens.
[/quote]

Agree, I lost tokens in several projects. Some of them are still active. I don't think it's anyone's fault beside myself.

With that stated, the tokens exist in the mainnet supply and can very plausibly be reclaimed in the future. Worst case scenario, once the value of that 85K ZNN reaches a certain value, a bridge will be built. 

That's the beauty a actually a strength of NoM. In centralized projects, their deprecated tokens will never be reclaimed. In NoM it's possible.

-------------------------

0x3639 | 2023-11-22 21:06:58 UTC | #15

what if we ask people to submit an AZ and proof of ownership with a signed message from the BSC account?

-------------------------

sol | 2023-11-22 21:07:41 UTC | #16

That doesn't scale well with 1000+ holders.

-------------------------

sumamu | 2023-11-22 21:14:36 UTC | #17

We'd still have to take the snapshot first, otherwise ownership could change.

-------------------------

romeo | 2023-11-22 22:37:50 UTC | #18

Depreciation of the BSC contract is essential - whether it's bridged across or burned doesn't matter. We need to remove this invalid market sooner rather than later.

Do we all agree on that point?

-------------------------

Derek1982 | 2023-11-23 07:41:44 UTC | #20

Could we also take the same approach with the community members who have legacy znn stuck on Mercatox, now that they have confirmed that they did not swap to alphanet. If members can provide proof of ownership of the legacy znn on Mercatox they could be reimbursed using the same mechanism as wznn stuck on the deprecated bridge

-------------------------

0x3639 | 2023-11-23 10:12:26 UTC | #21

[quote="sol, post:16, topic:1686, full:true"]
That doesn’t scale well with 1000+ holders.
[/quote]

True.  Was hoping it was < 10 people.  But when $ZNN hits $1000 might be a different case.  I honestly don't know what to think.  Burning old wrapped tokens after announcing the event for more than 12 months happens in crypto.  

Here is my recommendation.  We wait.  We have the snapshot.  When the price goes up these tokens will be worth more and maybe the wZNN BSC holders can hire a dev to retrieve them.  They could fund the work as a Percent of funds retrieved.  My $0.02.

-------------------------

Rom | 2023-11-23 13:28:52 UTC | #22

Sol,
Thank you for adressing this matter. 

I heavely invested in the network in 2021 nearly 90K, not in a speculative purpuse, but because the project is claiming to be fully decentralised, disruptive and free of VCs. 

few days ago i wanted to send my wznn from the BSC chain to the syrius wallet to skate them, this is how i discovered this issue.

I saw a few tweets on november 2021, that didnt stipulate at all that the WZNN could be lost, burnt or who knows. (Please find below the 'tweets'). i probably missed tweets, messages, updates... but even though investors must be fully respected in any project and can't be spoiled in anyways. I'm sure we are all agree on that.
 
@Sol exposed the issue in a respectful and professional way. On the github he proposed * distribute equivalent, valid ZNN to these holders.
Can we please all agree with that? And this case will be a very strong opportunity to be publicly exposed, it will bring more confidence and will embrace for sure new investors into the journey of Zenon. 

best,

Here are the tweets:
@Zenon_Network
twitter/Zenon_Network
[3 nov. 2022]
"Starting with the 10th of November, the bridge will enter into partial maintenance mode: the [$ZNN flow will be closed and only swaps from [$wZNN] will still be possible. The complete termination of the 2-way Bridge will occur during December."
@ Zenon_Network
twitter/Zenon_Network
[3 nov. 2022]
All users are encouraged to swap their [$wZNN]

-------------------------

Srobb | 2023-11-23 13:55:06 UTC | #23

I'm with @Rom here in that all investors should be respected. I too did not see anywhere saying the wZNN on BSC would be destroyed/worthless so assumed in time the bridge would be rebuilt in order to change the wZNN to mainnet.

Given the options above I believe that creating some sort of swap portal that must be verified with a signed transaction from the holders BSC account to swap to mainnet.

I'm not a dev, just an investor and would like to see resolution to this current problem.

Happy to discuss other methods of anyone else has opinions

Thanks

-------------------------

oginotvavra | 2023-11-23 14:02:03 UTC | #24

Just to summarize your post, are you asking others to **invest** in development just because you haven't been interested in the project for more than 2 years?

-------------------------

Rom | 2023-11-23 18:55:49 UTC | #25

Just to summarise, you didn’t get the point here and go on attacking/pointing. The subject is extremely serious it’s not a game of who is right or wrong, but finding a solution regarding the investors. 
I’ll reformulate: 
The mistake here is on the communication, never got or saw a red flag, a clear message that I could be in the situation with other potentiel 1000 of investors. 
We are not talking about a video game buta  lot of money invested. That’s why they is some rules as soon as they is 1$ in the game.
I think when you invested what I invested my implication speaks it self. 

Because of behaviour like that people are running away from DEX. 
I’m betting on the strong community of Zenon to be above that and solve our issue asap.

-------------------------

oginotvavra | 2023-11-23 15:09:05 UTC | #26

Cmon, I'm no attacking anyone..I'm just giving the other side's perspective, and I totally get that you're trying. Anyway, agree with deeznnutzs idea:

Here is my recommendation. We wait. We have the snapshot. When the price goes up these tokens will be worth more and maybe the wZNN BSC holders can hire a dev to retrieve them. They could fund the work as a Percent of funds retrieved. My $0.02.

-------------------------

Stark | 2023-11-23 15:23:07 UTC | #27

Three salient points:

1. Self custody of native tokens is fundamentally an individual responsibility.
2. A solution for recovering these assets is reasonable and possible.
3. The question is how, and when to develop a solution.

When one of these points is disregarded, conflict emerges.
When all points are regarded, we find that we all aiming in the same direction.

The most natural solution to this dilemma is to see what a great opportunity it is, for wrapped BSC token holders to get involved and recruit or incentivize new devs to join the decentralized developer community of Zenon. The rational incentive to do so, will likely increase.

-------------------------

cryptocheshire | 2023-11-23 16:11:41 UTC | #28

I emphasize with anyone affected, but to relativize your statememt that comms are at fault: If you were off the grid, how was anyone supposed to get the message to you? The funds weren't burned or stolen, they were moved to shared pillar custody (AZ contract) after months of public warnings. While people here are willing to find an amenable solution, the onus to keep track of one's investments in this space is always the holder's. And you chose not to keep it on the mainnet but on BSC. What if BSC had gone down? Would you have blamed this community as well?

I oppose we spend valuable dev resources on this. If you want those funds to be released from AZ, stop blaming everyone but yourself and submit a formal AZ proposal. Onwards.

-------------------------

sol | 2023-11-23 16:54:16 UTC | #29

Agree with most of your points, though I don't think most investors have the ability to propose and develop a solution to reclaim their funds.
Individual AZ payouts won't scale with the demand.

In my opinion, the best solutions are 2a and 2c (reclaim on any EVM chain that isn't ETH).
Simple to develop, simple reclaim for investors.
Dependencies will take some time to deploy.

-------------------------

Kieudung | 2023-11-23 17:45:27 UTC | #30

Hi friend I am a WZNN user since 2021 when winter arrives I simply bought WZNN in BSC and kept it at $3 with TX proof I was sad to hear the project moved to ETH That's all that's left of me so I'm looking forward to community help

-------------------------

Rom | 2023-11-23 18:39:52 UTC | #31

Sol, when you said simple to develop, what will be your estimation in term of dev time? Could we hve access to some documents regarding this topic? what kind of dev do we need here? anyone you know would be happy to take this job? 
Regarding the amount that is stuck on the BSC i dont think it will be difficult to finance this action. Is in the interest of everyone to solve this.
Thank you

-------------------------

sol | 2023-11-23 18:49:14 UTC | #32

This [frontend + contract code](https://github.com/Scream-Finance/merkle-airdrop-bdei/tree/master) should be easy to update and deploy.

I'd be willing to do this though we don't have the dependencies for a smooth user experience.
We could launch it on ETH today but I doubt many people will want to pay those fees.

-------------------------

Rom | 2023-11-23 18:49:51 UTC | #33

I got some of your points but you didn't get mine sorry. i wasn't off the grid, i even share the main tweets here, i'm questionning the communication that we all received i didnt saw or understand that the bridge will be closed for wznn=>znn, it's not what it's written. that's my point. after i probably missed other communication but again investors are not all of them technical or connected to all the channels. we just need to understand both parts and respect both side of the community ;)

-------------------------

Rom | 2023-11-23 18:52:23 UTC | #34

got it. And how is your estimation for the option that would be 1 for 1, less the share part of the cost of dev?

-------------------------

sol | 2023-11-23 18:56:32 UTC | #35

Options 1-3 in the original post propose 1-to-1 redemptions.
Options 1 and 2 should take a couple days to setup. Option 3 will take longer, maybe a few weeks.

-------------------------

Stark | 2023-11-23 19:17:15 UTC | #36

In order to avoid future calamity and confusion, the solution should involve the BSC token holders sending their tokens to a burn address, or the equivalent effect of taking them out of circulation, permanently.

-------------------------

oginotvavra | 2023-11-23 19:18:18 UTC | #37

The communication was crystal clear (Im also not technical). Its only your own fault. This should not be paid by AZ

-------------------------

dat_she_pepe | 2023-11-23 19:20:06 UTC | #38

Ok then but take a snapshot prior to the bridge closure. If not people are going to get rekt speculating and buying right now.

-------------------------

sol | 2023-11-23 19:23:43 UTC | #39

[quote="dat_she_pepe, post:38, topic:1686"]
Ok then but take a snapshot prior to the bridge closure
[/quote]

[quote="Stark, post:36, topic:1686"]
the solution should involve the BSC token holders sending their tokens to a burn address, or the equivalent effect of taking them out of circulation, permanently.
[/quote]

Both of these solutions are mutually exclusive.

Personally, I don't think a token burn is necessary. 
It is a cleaner solution, though.

[quote="sol, post:12, topic:1686"]
“You bought the wrong ticker, silly!”
[/quote]

-------------------------

Stark | 2023-11-23 21:18:05 UTC | #40

We can't pull the liquidity nor halt the contract. If the tokens are left in circulation then the market stays open as a frayed tangled end that will cause headaches.

Moreover, the premise that there are 1:1 tokens on mainnet will be violated, unless the holders forfeit and burn them permanently.

Judging by the behavior of the unwitting user, it seems reasonable to assume people will continue to trade these tokens. 

Also wrong that they would be able claim mainnet and then also sell on BSC for BNB.

-------------------------

dat_she_pepe | 2023-11-24 02:11:33 UTC | #41

Burning the wZNN on BSC and offering wZNN on ext chain on NoM seems to be the cleanest solution assuming the goal is to fix the horrendous communication from Mr. Kaine and get rid of the BSC problem. 1 ZNN burned = 1 ZNN you can redeem. 

Am I getting it right @sol ?

-------------------------

sol | 2023-11-24 02:19:34 UTC | #42

Sure, it's the cleanest solution in terms of killing off the old token.
There's no guarantee that every token will be burned or liquidity pulled.

And it hurts the people that panic sold after we stopped supporting it.

-------------------------

dat_she_pepe | 2023-11-24 03:00:07 UTC | #43

All solutions come with tradeoffs however this one is conceptually elegant no? Let's say every tokens on BSC can be burn indefinitely:

Cons:
- We add a little bit more supply but not that much. Roughly 3 months of inflation is I'm not mistaken.
- People on BSC aren't equal, some have sold, some didn't.

Pros:
- The additional supply might be even lower due to people never burning their wZNN from the BSC chain. The ones who will burn will do so over time. Overall the impact could be negligible.
- Community members can rejoin. Some of them could even be future contributors. 


The snapshot solution provide roughly the same outcomes with a twist as the ones who sold post snapshot can now enjoy free money and keep their wZNN. Someone on one side of the market will be unhappy whatever is being decided. However the non snapshot burn address solution would shut down complains forever.

-------------------------

aliencoder | 2023-11-24 10:06:46 UTC | #44

Who remembers this [Medium article](https://medium.com/@zenon.network/alphanet-swap-cycles-658981a9d8bd)?

> To prevent swap apathy, we are introducing a novel **Swap Decay** mechanism intended to stimulate participants to transition to Alphanet as fast as possible.

>  Thinking long term, replacing or updating those cryptosystems with quantum-resistant cryptography is a matter of how not when.

> If proven a success, the Swap Decay mechanism will be re-used for NoM Phase 1 to smoothen the transition to state-of-the-art quantum-resistant crypto systems. Efforts will also be made to improve and standardize the solution to be suitable for other established cryptocurrency networks.

@Rom Regarding the BSC token migration, every participant had more than enough time to bridge their BSC tokens back to NoM. Why didn't you swap them on time? It's your responsibility to keep track of what's happening and you also had plenty of time.

I lost many tokens because I didn't swap them on time or because it is no longer possible. Do I blame anyone for this? 

If you care about your investment both in financial and emotional terms, you need to always keep an eye on those tokens regardless of market conditions: all summer long no one bothered to ask those questions. I suspect many speculators were awakened by the pump and want to capitalize on the good faith of our community.

If you are in crypto, you should know better than anyone that with great power come great responsibility: self-custody, token migrations, etc.

-------------------------

sol | 2023-11-24 12:07:29 UTC | #45

We never announced that the wZNN tokens would be forfeit.

-------------------------

0x3639 | 2023-11-24 14:58:03 UTC | #46

My recollection is we did.  I think .org had a banner on their site and tweeted many times.  But I would need to spend time fact checking myself.  

Maybe after we pull all the zenon_network tweets we can search them quickly. 

@mehowbrainz didn't you have a banner on .org?  Or am I smoking something?

-------------------------

dat_she_pepe | 2023-11-24 20:08:40 UTC | #47

I to agree with @sol on this. The communication was a disaster, as it always used to be back then. 

However in the end it doesn't matter. You guys are having the wrong discussion and doing so, you're completely missing the point: what benefits the network? We will always disagree on what's fair and what's not. So let's look at this from the above perspective. What I see is the following:

- The additional supply is not that much. The network doesn't care.
- Even if some woke up on this pump, it doesn't matter. Ultimately allowing BSC wZNN to be redeemed would allow some to jump back in and amongst them, there might be future contributors. THIS benefits the network.
- What about being on the wrong side of the market? The network doesn't care.
- The network however cares about getting rid of the BSC fud for good.

-------------------------

Samwinter1888 | 2023-11-24 20:25:17 UTC | #48

[quote="sol, post:45, topic:1686"]
forfeit
[/quote]

It was announced many times on official twitter page, that tokes should be moved of bsc and that bridge would be closed, than the deadlines kept moving forward many times, so in reality there was enough time for people to move tokens back onchain

-------------------------

dat_she_pepe | 2023-11-24 20:26:38 UTC | #49

Wrong discussion again.

-------------------------

Samwinter1888 | 2023-11-24 20:29:17 UTC | #50

I agree that it would be a good idea to get rid of the fud connected to bsc, but some people bought those tokens for a fraction of their cost after the bridge was gone and letting them move them back onchain is not exactly "fair"

-------------------------

dat_she_pepe | 2023-11-24 20:33:19 UTC | #51

As said above we'll always disagree on what's fair and what's not and at the end it doesn't matter. At the end I could say some people bought but are so unfamiliar with crypto that they didn't get what was happening. Those people exist. What's fair for them? Ultimately, there's always someone on the wrong side of the market and so what ?  It's a mere blip in the sea. We call it an arbitrage. There are many. This shouldn't even be considered. Let's burn all BSC tokens and move on free for good.

PS : I also remember Syrius not mentioning the bridge closure anywhere. This was the crappiest communication ever...

-------------------------

Samwinter1888 | 2023-11-24 20:34:05 UTC | #52

Maybe now some people that bought those supper cheap zennies are on the wrong side of the market and might want to get on the right side by persuading everyone that it is the right thing to do.

-------------------------

dat_she_pepe | 2023-11-24 20:34:51 UTC | #53

How does this matter from the network perspective? There will always be arbitrages. Whatever we announce and decide, smart people will play.

-------------------------

Samwinter1888 | 2023-11-24 20:43:39 UTC | #54

From the network perspective, it matters that some who bought very cheap would put unecessary pressure on the  price and the whole point of returning those tokens to poor guys who did not read the notices and sold at very cheap price, would be lost. 

One of the ways would be to refund those who did not touch their coins after the bridge was taken down, but it would be unfair on those who bought cheap zennies with intent to make arbitrage gain.

-------------------------

dat_she_pepe | 2023-11-24 20:46:58 UTC | #55

As said above, the additional supply injected would be minimal - less than three months of inflation I reckon. On this we don't even know how much will be kept / sold and how much will be effectively claimed. So, probably less.

It also can be said that bringing back possible valuable contributors is very good mid & long term.

-------------------------

Samwinter1888 | 2023-11-24 20:49:50 UTC | #56

It seems reasonable to refund those who did not touch their coins before the bridge went down, as they were not aware of what was happening. All the trade that went after the brigde went down is just sponsoring those who want to make extra gains at almost no cost, which is not benefiting the network.

-------------------------

Samwinter1888 | 2023-11-24 21:31:25 UTC | #57

The guys who bought it at fair price, I think should be able to get them back.

Arb people that want to invest a fraction of the cost and make huge gains, no point of paying them. They were aware of the bridge going down, they moved their coins in time and bought of those that were late trying to make extra gains. Yes they would loose their invested money, but arb is risky.

Surely no one that was aware of the bridge going down and their tokens being lost would leave them on bsc, only those who were not informed about it for some reason like not following the project closely.

-------------------------

Ppaesch | 2023-11-24 21:44:13 UTC | #58

I think that it is not the  duty of the network to make holders whole that arent responsible enough to track their investments and take the necessary steps if needed.
I am at max for reopening the bridge, this way the whole network would profit from a growing liq pool and we would have an alternative to excessive swap fees on ether.

-------------------------

dat_she_pepe | 2023-11-24 23:30:23 UTC | #59

Just reopening the bridge is the simplest way no?

-------------------------

nbd | 2023-11-24 23:34:18 UTC | #60

The simplest way is to NOT refund. They had plenty of time to bridge their tokens back to syrius.

-------------------------

zyler9985 | 2023-11-25 03:45:49 UTC | #61

I think there's only one approach which makes sense – make them whole.

We are struggling to get new members, and the last thing we need is more FUD. Making them whole will be something those members really appreciate, we can view it as an easy way to grow/maintain our membership and to promote a positive reputation as caring about our members.

It's easy to blame them for not being responsible and burn them. There is some justification for being like this. I just think it's smarter from a membership growth, PR perspective as well as cultural to be more lenient, especially given the dubious communication back then before we were community-run.

Even the ETH wZNN should come with a disclaimer/warning btw. True Bitcoiners don't wrap their BTC and neither do true aliens. Regardless of probability we should warn about the risk of hacks or migrations and remind people to keep an eye on their investment. No other project bothers to be so nice, but we should create trends not follow them. My 2 cents.

-------------------------

Ppaesch | 2023-11-25 08:52:34 UTC | #62

imo we already stated that we care about our members as holders that suffered from the bridge exploit made (more than) whole. That happened because it was not the fault of the holders, but the fault of the bridge contract. in this case here it is the fault of the holders that slept on various notifications for months.
every admin in the tg was more than willing to help, we even had how to videos. iirc even you made a guide how to swap to the mainnet.
i am still for reopening the bridge, idk though how much work this would be.

-------------------------

zyler9985 | 2023-11-25 10:54:51 UTC | #63

Blame is debatable. The bridge exploit is also the fault of the holders, because they chose to use a bridge which had not been audited. They knew the risks and were not responsible, they should have bridged their assets to native if they wanted to minimise risk. They should have taken better care of their assets.

My point is that we should choose leniency for the sake of growing our users and positive PR, as we don't currently have a huge amount of them.

As for how it's done? I don't have an opinion yet. It could be that in 1-2 years we are in a position to easily help them, or there could be some other way to get it done sooner.

-------------------------

0x3639 | 2023-11-25 11:01:49 UTC | #64

[quote="dat_she_pepe, post:59, topic:1686, full:true"]
Just reopening the bridge is the simplest way no?
[/quote]

we dont have tokens in the bridge to refund.  They were moved to AZ.

-------------------------

NeoShredder | 2023-11-25 13:33:01 UTC | #65

Bsc wZNN bridging shudnt be a high priority rn.
But if sumamu team can launch a bridge to bsc with present code, maybe it's easier. One way bridge only

-------------------------

coinselor | 2023-11-25 19:03:32 UTC | #66

How about a "refund" that's not a free lunch?

We use the 87K ZNN to add liquidity to Uniswap and lock it for a year. All Yield goes to AZ. Eventually, after a year of staking, anyone with BSC wZNN can burn and claim their LP stake. 

Same output, not a free launch. AZ earns compensation as yield. If we megapump, investors suffer impermanent loss when withdrawing their share of the LP.

Only problem I see is the ETH liquidity counterpart. Otherwise we'll have to forcefully sell their ZNN at current prices when adding liquidity.

Idea: AZ borrows wQSR and we create a wQSR-wZNN LP. Upon breaking the LP position, AZ claims the share of the wQSR and pays the BSC wZNN user submitting a claim. 

There's probably an elegant solution here.

Thoughts?

-------------------------

dat_she_pepe | 2023-11-25 20:10:43 UTC | #67

I fail to see how this get rid of the fud that could and will blowback. As you said impermanent loss and the ETH side make it very complicated. 

Instead of a relatively small amount of supply smoothly hitting the market, you'd need to straight dump half. 

The QSR market is a math to explore though.

-------------------------

TrevorLeahy3 | 2023-11-25 20:52:21 UTC | #68

The network has a history of being good to its participants, and i agree its worth reducing the fud from this angle with the simplest solution possible.

It is bsc though so i dont think its needs to be pretty, snapshot(pre deprecation), burn the contract, whatevers the easiest way to make claims and we move on.

-------------------------

Stark | 2023-11-26 12:05:19 UTC | #69

Recommend changing the thread title to avoid confusion in the future. We'll have people reading this, thinking it pertains to PIVX.

The wisest, most comprehensive option that will age the most gracefully, is one that is:

1. the most hands-off
2. let's the free market be a free market 
3. requires **no** arbitrary decisions, such as choosing a snapshot date
4. removes wZNN from circulation
5. mitigates or effectively eliminates the wZNN/wBNB LP

The only two viable options are to open a one-way bridge, or do nothing. The "bridge" (burn & swap) doesn't have stay open forever, because a second or third swap & burn initiative could open at any time in the future, because it would simply work with respect for the wZNN token supply.

A retroactive snapshot would be an action that goes in direct opposition to the free actions that holders took to buy and sell after whatever arbitrary date might be chosen for the snapshot. Some holders plausibly actively traded wZNN numerous times against BNB and the broader market. We should refrain from trying to travel backward in time whenever possible. There's nothing in the past for us.

A casual discussion about judging the past is a lot different from making an actual present-day decision that will affect the future. Let's look in the right direction.

My observation is that every wZNN holder who came into chat after the bridge was closed, was met primarily ridiculed and derided. They were also advised that it's possible that some kind of solution could arise and/or that whatever they decide to do with their BSC wZNN, was completely up to them. 

If they sold or bought more BSC wZNN, or stayed in the LP (all three user cases exist), they did so on their own volition and their own physical button clicks, or lack thereof. Taking an action that retroactively negates the free actions of holders, will not stand well in the test of time. 

Who will be the one to make an arbitrary snapshot & drop, that does nothing to remove BSC wZNN from circulation and write it into code?

-------------------------

angelo_a_jr | 2023-11-26 22:49:47 UTC | #70

Option 0 for awhile.

This should not be high priority, we have larger objectives ahead of us.  

Appeasing people who had considerable advance notice will only introduce more drama to drag out.

If we expect people to hold their own keys, they should certainly be responsible enough to track their own investments.  

I haven't met a single professional investor in crypto, TradFi, or any asset class for that matter that does not keep close tabs on their investments, no matter how small.  

There was 12+ months notice, drive on.

-------------------------

dat_she_pepe | 2023-11-27 15:13:35 UTC | #71

Wrong discussion, again.

-------------------------

sol | 2023-11-27 16:25:08 UTC | #72

[quote="Stark, post:69, topic:1686"]
Taking an action that retroactively negates the free actions of holders, will not stand well in the test of time.
[/quote]

As Hewwo stated, we can't appease both sides of the market.
We have to decide between:
1. making pre-bridge closure holders whole (snapshot)
2. making current holders whole (burn contract)
3. doing nothing (both sides are abandoned)

I see a surprising amount of contention in this thread and Telegram, specifically towards the notion of reimbursement. I was hoping more of you would be empathetic towards our returning alien brethren. 
As others have mentioned, Mr Kaine refunded us when the bridge liquidity was rugged. We can continue in this spirit with the funds that *we* rugged on BSC.

In terms of the greatest benefit, I believe #1 will satisfy the most genuine holders at the expense of liquidity providers.
Though I appreciate their service, LPs are more experienced and should be much more vigilant of market forces. I would rather place the onus of responsibility on them than on passive holders with less experience.

That being said, I also see reasons why we should opt for burning the token, prioritizing current holders.
I like this outcome less, since our organization's atrocious communication caused people to sell at a loss and we would be rewarding opportunistic speculators instead.

Is anyone going to mention it? 
The arbitrage opportunity is currently 5:1.


[quote="Stark, post:69, topic:1686"]
Who will be the one to make an arbitrary snapshot & drop, that does nothing to remove BSC wZNN from circulation and write it into code?
[/quote]

I'll volunteer for all options I presented in the original post. I won't take action until we have some sort of consensus.

-------------------------

Kieudung | 2023-11-27 17:29:25 UTC | #73

I think you should give those who have come back 1 last chance

-------------------------

dat_she_pepe | 2023-11-27 19:27:52 UTC | #74

I vote to just burn the whole wZNN supply on BSC. Make it a ritual to free CZ for more marketing hype. Stick "4" everywhere and summon @mehowbrainz 

Bam. Pump.

-------------------------

defi99 | 2023-11-27 20:26:43 UTC | #75

IMO the purpose of the 1 year depreciating bridge for BSC was intended to have the outcome we are now seeing.

If you made significant investments into ZNN and did not take action for an entire YEAR, that's on you. There were several twitter posts leading up to the 1 year start and throughout the entire 1 year period.

Also, TG was active throughout the entire ordeal for those that would have needed help.

Snooze ya' looze.

-------------------------

SugoiBTC | 2023-11-27 21:22:25 UTC | #76

Sooooo wen poll guys? This way we can gauge the community's opinion on this matter. From there we can discuss further.

-------------------------

dat_she_pepe | 2023-11-27 23:15:55 UTC | #77

Wrong discussion, again. Stop struggling in attempt to find people you can blame. This is petty.

-------------------------

sol | 2023-11-28 00:26:44 UTC | #78

[quote="SugoiBTC, post:76, topic:1686"]
wen poll
[/quote]

I updated the op with a poll. 

If you made it this far in the thread, please consider voting.

-------------------------

NeoShredder | 2023-11-28 01:05:06 UTC | #79

https://forum2.zenon.org/t/deprecation-plan-for-legacy-wznn/1686?

The poll ☝️

-------------------------

0x3639 | 2023-11-28 01:23:02 UTC | #80

I voted do nothing because this has happened to me and I accepted responsibility for not following the project closely.  I'm open to changing my mind in the future.

-------------------------

shaimo | 2023-11-28 14:23:22 UTC | #81

Whatever the final decision is on who to reimburse and how much, i think two things we should do:
1. Make it claimable and not airdropped - people who are long gone and/or not following the announcements are out of luck.
2. Make it limited in time. A few weeks. Maybe a couple of months.
All unclaimed funds go back to treasury.

I think the snapshot should be that of yesterday - before posting this thread:
1. Those who sold after deprecation knew they were giving up their znn, and don’t deserve to get it back.
2. Those who bought after deprecation thought they were buying real znn, and should indeed get it.
3. Anyone buying after this post is just gambling they might be getting very cheap znn.

-------------------------

nbd | 2023-11-28 14:25:58 UTC | #82

[quote="sol, post:72, topic:1686"]
Is anyone going to mention it?
The arbitrage opportunity is currently 5:1.
[/quote]

too obvious to be mentioned I guess
brb gonna buy some wznn on bsc and vote on "reimburse current holders"

-------------------------

nbd | 2023-11-28 14:29:52 UTC | #83

I don't think it's a good idea since some people were buying these last weeks after this discussion started knowing there's a possibility they can benefit from the empathy of the community

-------------------------

Asgardians-Pillar | 2023-11-28 14:42:24 UTC | #84

IMO 
1 of the nastiest things in crypto would have to be getting fucked out of your stash when not paying attention even it is for multiple years what you bought should always be able to converted to the newest version. That's not how it works in crypto but it should.

That said I would snapshot the depreciation date and do a vested airdrop afterwards. Lock that shit up 1y and then give it back in 5% bags over 20 months. Or something like that.

-------------------------

shaimo | 2023-11-28 15:37:27 UTC | #85

I didn’t check on chain but in that case just set it for the day before that discussion started

-------------------------

SugoiBTC | 2023-11-28 19:21:52 UTC | #86

I also think that a snapshot for BSC holders **before** the bridge deprecation would be most fair. Any speculators after that should not be included.

Although token migrations are common and people that act too late are prone to lose their bag, we're in a position to do the right thing here. Instead of selling, they just held their wZNN on BSC without doing anything. 

We will never know the real reason why these investors did not check in on their investments, but these guys HODL'ed all the way. 

Let's welcome these aliens back into the community :)

-------------------------

Stark | 2023-11-28 21:46:11 UTC | #87

I know one person who had a few wallets and simply overlooked some BSC wZNN. There are a lot of different scenarios. I'm sort of ambivalent about it because it's out of my hands, but my friend would be happy to get her wZNN swapped in one way or another.

-------------------------

Stark | 2023-11-28 22:06:43 UTC | #88

This makes the most sense as it supports the die hard holders. Everyone in this thread has had plenty of good reasons to give up on Zenon, and yet here we are. I don't think anyone who sold for any reason should be reimbursed. 

They also received BNB for their trade, so it wouldn't balance on the books. For all we know they reinvested the BNB and made millions on $shibinarydogepoopoo

-------------------------

DrD3 | 2023-11-29 08:21:11 UTC | #89

Ehhh Idk about reimbursing bsc wznn holders with a snapshot. 

* Were the holders/speculators informed about the bsc bridge depreciation? Yes.
* Were they given ample enough time to bridge their tokens? Yes- >1 year.
* Was it their responsibility to check in on their investment? Yes. 
* Did they come because the chart blew up for a hot minute? Probably.
* Would it be to their benefit if we made them whole? Absolutely.
* Can we make them whole with a snapshot/airdrop? We can.
* Should we? Absolutely not!

People investing in internet magic money often forget the basic #1 core tenet- that it is their personal responsibility to look after their holdings. If you lose your seed phrase, or the hard-disk you were mining your coins gets damaged beyond repair, or if you don't check in on your investment because you forgot- its all on **you**. Those crying about the latter right now should return to the confines/comforts of a safer more regulated financial space- where this would not happen.

-- just my two quassies.

-------------------------

lukasl | 2023-11-29 08:32:13 UTC | #90

I came on the telegram before all this pump. Because I was outside crypto and I wasn't informed about the decision to discontinue the bridge and now I'm stuck on BSC. 

It's not like you get an official email that the bridge is getting turned off. You'd have to be in the telegram + open the telegram and read the important messages.

If this isn't done, it would be like the chain stole that tokens when there actually is a fix and make us whole. 

1 wZNN still equals 1 ZNN. 

The simple reason that we weren't present when this decision was taken place is not a good enough reason to just leave us in the dark.

Put yourself in our shoes. You invested in a project you saw potential, didn't sell when it hit rock bottom, but because of the whole crypto cycle, people returned to their day to day jobs and didn't pay attention as it was in the bull run. And now you find out that your tokens are useless because you didn't bridge at the right time.

-------------------------

oginotvavra | 2023-11-29 10:10:36 UTC | #91

It's the same thing over and over again. It's your investment and only your own responsibility. For a year straight, investors have been warning to do the swap (twitter+tg. After a year and a half, they all come back and ask others to fix their inactivity, their disinterest, their problems.

-------------------------

dat_she_pepe | 2023-11-30 14:11:32 UTC | #92

What about the solution of taking ALL the wZNN and locking those in a QSR / ZNN LPs ? The A.Z could lend the funds so the pool can be increased and locked for a year. After 1 year everyone's happy AND we get liquidity there.

- Holders who forgot to swap are taken care of
- People who bought without realizing it wasn't the right token and got hurt are taken care of
- **The network benefits from the operation as QSR finally gets a somewhat liquid market**
- Nobody gets hurt
- Whoever made a mistake is taught a lesson so everyone's happy

-------------------------

Samwinter1888 | 2023-11-30 14:32:50 UTC | #93

Maybe we should unlock those tokens over a period of  1 or 2 years in equal parts so it would not put sell pressure on the network

-------------------------

Stark | 2023-11-30 15:45:19 UTC | #94

imagine someone irl loans you money with an APR to help you get on your feet. You decide at some point to change the terms of the loan. You tell some friends at the bar that you're changing the terms, and then you post a notice on the front door of your home for everyone to see.

When they come back to check on the status of their due funds, you ridicule them. because this is crypto. We're merely building the **trustless** backbone of the future.

They should have been paying attention to the rumors at the bar and checking the bulletin board to make sure you wouldn't change the terms of the programmatically trustless system, and ethical premise of your very existence.

-------------------------

Phuong | 2023-12-01 09:41:18 UTC | #95

I was told this is a "punishment" and I am a bad person for suggesting this lmao

-------------------------

dat_she_pepe | 2023-12-01 16:09:52 UTC | #96

You were seeking for guilty people rather than for solutions so yeah kinda.

-------------------------

aliencoder | 2023-12-09 22:19:31 UTC | #97

Another project that deprecated its token: https://blog.aragon.org/a-new-chapter-for-the-aragon-project/

"The AA will send the assets to a smart contract that will autonomously allow all ANT holders to execute the redemption transparently onchain over the course of **12 months**. No further funds will be sent to the Aragon DAO. From this moment forward, there is no purpose in continuing to hold ANT.

At the end of the redemption period, the redeemed ANT will be burnt and any remaining ETH will be sent to the Ethereum address of the new product-focused structure".

-------------------------

Rom | 2023-12-28 15:09:56 UTC | #98

Thank You for expressing this good point of you.

-------------------------

Stark | 2024-01-02 21:37:52 UTC | #99

1. There is no reason to fabricate a "final date" on the redemption of the BSC tokens.

2. Choosing a date and deciding upon a snapshot is an intervention. 

3. A one-way bridge, can be opened permanently or temporarily. If the bridge is open for one month, and then taken offline, that doesn't interfere with the option for another future initiative to create another redemption window.

4. If a snapshot is effected, this is the same as "undo-ing" the subsequent free actions (trades) of individuals.

5. Instead of trying to be the arbiters and judge what we think is "good or bad", we should try to avoid interfering with forces that are greater than us. Time moves forward. Snapshot would be retroactive. Simply opening a one-way redemption would be pro-active. 

P.S. Worrying about whether someone is going to profit, is a conflation of issues. After all, anyone who sold, received BNB. So, if they now received ZNN from a snapshot, they would be profiting. This is the fallacy of fairness.

P.P.S. If nobody decides to pursue developing a solution, it doesn't bother me at all. I'm not advocation for a solution, but if there will be action taken by the network, I will advocate for an avenue that will bode well in the long run.

-------------------------

Stark | 2024-07-08 00:49:23 UTC | #100

![Screenshot 2024-07-07 at 8.06.01 PM|438x499](upload://sMPCJOMW6ROHp8QJ4nBrlT5bUq0.png)
FYI and posterity.

-------------------------

