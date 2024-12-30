Thread: road-to-100x
sumamu | 2024-03-27 15:19:55 UTC | #1

Well, technically it's 120x, but 100x is more common in crypto, so I went with that.

First of all, I would like to point out this very informative article written by @0x3639, which explains the Liquidity Bootstrap & Provisioning Campaign in great detail:
https://www.zenon.info/liquidity-bootstrap-provisioning-campaign/

# What does it mean?

In crypto, the term 100x commonly refers to finding a gem that will get you an 100x on your investment.

But in this context, it's actually about a combo of 2 multipliers that together can go up to 120x:
- the LP staking multiplier
- the liquidity bootstrap campaign multiplier (new)

It is also a powerful message that can be used by the marketing and sales teams in the community and it can be applied to many aspects:
- 100x adoption
- 100x scaling
- 100x tps
- 100x speed


# What's the LP staking multiplier?

After providing liquidity in the main pool, the provider can swap their LPs to NoM and stake the received ZTS LP token for a period between 1 and 12 months and a multiplier from 1x to 12x.

# What does the LP staking multiplier apply to?

When Orbital distributes the rewards, it adds all the amounts staked together and splits the rewards to each stake entry based on the percentage it represents of the total amount.

For example, if there are 3 stake entries of 20 ZNN + 30 ZNN + 50 ZNN, once you add them together you'd get a total of 100 ZNN. When Orbital distributes ~500 ZNN, it will split the ~500 ZNN between all the stake entries, so the 20 ZNN entry will get 20% of the ~500 ZNN, which is ~100 ZNN.

However, if the 20 ZNN entry is staked for 12 months, with a multiplier of 12x and the other 2 entries are staked for 1 month with a multiplier of 1x, then the total would be calculated as 20 ZNN * 12 + 30 ZNN + 50 ZNN = 240 ZNN + 30 ZNN + 50 ZNN = 320 ZNN. This means the 20 ZNN entry now gets a 75% share of the ~500 ZNN rewards, which is ~375 ZNN.

# What is the liquidity bootstrap multiplier?

The Orbital program distributes 561.6 ZNN + 1250 QSR every day. The contract also has a reserve of ~290k ZNN and ~674k QSR, out of which a configurable amount can also be distributed daily depending how and when we, the community, decide to do that.

With this is mind, I'm proposing a new multiplier of 1x to 10x, the Liquidity Bootstrap Multiplier, to be applied to the amount of rewards distributed daily like this:
- 1x multiplier if the LP has  0-1000 ETH (561.6 ZNN + 1250 QSR distributed daily)
- 2x multiplier if the LP has 1000-2000 ETH (1123.2 ZNN + 2500 QSR distributed daily)
- ...
- 10x multiplier if the LP has 9000-10000 ETH (5616 ZNN + 25000 QSR distributed daily)

This will be reset to 1x after the campaign ends or the Orbital program runs out of reserves (~290k ZNN + ~674k QSR)

# So how do we get to 100x?

The LP staking multiplier gets us 1-12X.
The liquidity bootstrap multiplier gets us 1-10x.
So we get a combined multiplier of 1-120x!

# What do you want from us?

I want to get your feedback on this and to work together to find the best way to start this campaign. 

During this campaign the community should coordinate marketing efforts to reach towards the defined targets.

# How do we add liquidity if there's a cap?

Right now there are ~166k wZNN in the pool. The cap is at 100k wZNN. More liquidity can be added when at least 66k wZNN are removed from the pool and that can happen in 2 ways:
- LPs remove their liquidity
- ETH is swapped for more than 66k wZNN on Uniswap

# What's the endgame?

Having a deep liquidity pool consolidated on the way up. Imagine if we reached 10000 ETH in the pool with 100k wZNN. 1 wZNN = 0.1 ETH? Crazy, right?

# Why didn't you answer my question before I asked it!?

Did my best, but please ask and I'll answer.

-------------------------

bayrum | 2023-06-15 20:58:33 UTC | #2

Let's differentiate once forever orbital program and liquidity bootstrap
" **Orbital program runs out of reserves** (~290k ZNN + ~674k QSR)"  I thought orbital program is coming from emission and cannot runs out of reserves?!?! Do I make a mistake?

Liquidity bootstrap = Just a bonus over the standard orbital program?!?!

Are you saying that over the orbital program which are coming from emission (561) we gone have forever an x1 bootstrap over the orbital program that equal 561x2 = 1122 as you say here : **This will be reset to 1x after the campaign ends** ???

Everything looks great but I would decrease X2 from 1000-2000ETH to 500-1500 ! 
Good luck!

-------------------------

sumamu | 2023-06-15 21:01:58 UTC | #3

Orbital Program distributes 561.6 ZNN + 1250 QSR daily from the network emission. This will be the baseline (1x) and it is unlimited.

Orbital Program also has additional reserves of ~290k ZNN + ~674k QSR. Liquidity bootstrap will be distributing rewards from the reserves (starting with 2x), which are limited.

-------------------------

romeo | 2023-06-15 21:17:11 UTC | #4

[quote="sumamu, post:1, topic:1484"]
Right now there are ~166k wZNN in the pool. The cap is at 100k wZNN. More liquidity can be added when at least 66k wZNN are removed from the pool and that can happen in 2 ways
[/quote]

There's a motivating factor here for those already in the LP vs those who aren't. I think clear direction/decision is required first about the cap and when it will be lifted so that the community knows when they can participate and what will be available as rewards at that time (orbital + bootstrap or just orbital x1 for example)

-------------------------

crack | 2023-06-15 21:19:24 UTC | #5

additional reserves of ~290k ZNN + ~674k QSR is not just for ETH bridge IMO. We need it for other LP reward of other L1 Bridge next time

-------------------------

vibe.znn | 2023-06-15 21:18:42 UTC | #6

[quote="sumamu, post:1, topic:1484"]
# How do we add liquidity if there’s a cap?

Right now there are ~166k wZNN in the pool. The cap is at 100k wZNN. More liquidity can be added when at least 66k wZNN are removed from the pool and that can happen in 2 ways:

* LPs remove their liquidity
* ETH is swapped for more than 66k wZNN on Uniswap

# What’s the endgame?

Having a deep liquidity pool consolidated on the way up. Imagine if we reached 10000 ETH in the pool with 100k wZNN. 1 wZNN = 0.1 ETH? Crazy, right?
[/quote]

Please just open up the pool for anyone. this way we can ORGANICALLY grow with a fair market.

-------------------------

vibe.znn | 2023-06-15 21:25:33 UTC | #7

[quote="sumamu, post:1, topic:1484"]
1 wZNN = 0.1 ETH? Crazy, right?
[/quote]

would we be able to sell? Or only the current 27 (!) LP holders be able to benefit?

-------------------------

bayrum | 2023-06-15 21:24:06 UTC | #8

60k znn are staked now, thats around 44eth = ROI around 160% (by my calculation most of stakers locked for 12 months) at this price to gather 440 eth that would be 600k znn staked = 16 roi% . Taking in consideration impermanent loss LP will not be worth. Someone need to do better calculation but 2x multiplier is too high, maybe 300eth-500eth?

-------------------------

crack | 2023-06-15 21:25:32 UTC | #9

More liquidity, will need more buyer or seller to impact price go up and go down, this point is very different with Cex case.

-------------------------

SugoiBTC | 2023-06-15 21:51:56 UTC | #10

In regards to the 100k wZNN cap, wasn't that supposed to be part of the liquidity bootstrap mechanism?

The initial cap would be ongoing for 30-90 days if I remember correctly. So would that be another way for new LP'ers to join in?

-------------------------

ZNNAYIID | 2023-06-15 22:27:49 UTC | #11

[quote="vibe.znn, post:7, topic:1484"]
only the current 27 (!) LP holders be able to benefit
[/quote]

It's even less since not everyone staked their lp tokens.

[quote="sumamu, post:1, topic:1484"]
Right now there are ~166k wZNN in the pool. The cap is at 100k wZNN. More liquidity can be added when at least 66k wZNN are removed from the pool and that can happen in 2 ways:

* LPs remove their liquidity
* ETH is swapped for more than 66k wZNN on Uniswap
[/quote]

As much as I don't care about the cap rn, I think Liquidity bootstrap shouldn't be enabled until the cap is removed, otherwise around 20 lp providers will get all of it. 

And I agree that those who've been early and risked their ZNN to provide liquidity should be rewarded, but not until all the orbital funds are drained, 2 weeks is enough to reward early providers imo, especially when we talk about less than 27 addresses.

[quote="sumamu, post:1, topic:1484"]
Having a deep liquidity pool consolidated on the way up.
[/quote]
 Keep in mind that most of lp providers will remove their liquidity once the multiplier resets to x1, so use orbital funds wisely.

-------------------------

sultanofstaking | 2023-06-16 00:02:24 UTC | #12

[quote="ZNNAYIID, post:11, topic:1484"]
As much as I don’t care about the cap rn, I think Liquidity bootstrap shouldn’t be enabled until the cap is removed, otherwise around 20 lp providers will get all of it.
[/quote]

Agree would rather these rewards go towards attracting new participants vs OGs...

-------------------------

DrD3 | 2023-06-16 08:34:11 UTC | #13

I dont really see a problem with this solution. Unless I'm interpreting it incorrectly the 2x multiplier only activates once there's a 1000+ ETH- there's like what 124wETH there rn?

![Screenshot 2023-06-16 at 10.21.21 AM 1|485x500](upload://spb5xJYPF9U5lrGmasazqRS3mdr.png)
 
We'd need 9x the current amount of liquidity before Orbital's 'surplus reserves' (i.e the 2x) are even tapped into- so the only benefit early adopters really received is the 30-90 day bootstrap campaign where they hold greater ratios in the LP and ergo Orbital's daily dish out.  


That being said I would like to see more transparency and communication from Sumamu & Co. I think a lot of the early LP providers were lulled in with the promise of already receiving the bootstrap rewards. Additionally, many of us did voice our fears that the 100k cap would be filled-up very quickly by whales trying to capitalize and unfortunately this is exactly what happened. Wish we could have discussed implementing a cap on individual contributions or other alternative solutions.

-------------------------

sumamu | 2023-06-16 11:03:26 UTC | #14

[quote="vibe.znn, post:7, topic:1484"]
would we be able to sell? Or only the current 27 (!) LP holders be able to benefit?
[/quote]

If price goes up, the wZNN in the pool goes down, so anyone will be able to join and benefit.

[quote="crack, post:9, topic:1484"]
More liquidity, will need more buyer or seller to impact price go up
[/quote]

You got that right!

[quote="SugoiBTC, post:10, topic:1484"]
The initial cap would be ongoing for 30-90 days if I remember correctly.
[/quote]

Yes, all restrictions will be lifted after the campaign ends. 

[quote="ZNNAYIID, post:11, topic:1484"]
Keep in mind that most of lp providers will remove their liquidity once the multiplier resets to x1, so use orbital funds wisely.
[/quote]

That's a good prediction.

[quote="DrD3, post:13, topic:1484"]
I dont really see a problem with this solution. Unless I’m interpreting it incorrectly the 2x multiplier only activates once there’s a 1000+ ETH- there’s like what 124wETH there rn?
[/quote]

That's correct. We're here to decide if we should go with 1000, 2000, ..., 9000 ETH, or something else.

[quote="DrD3, post:13, topic:1484"]
That being said I would like to see more transparency and communication from Sumamu & Co.
[/quote]

I'm here to do just that.

[quote="DrD3, post:13, topic:1484"]
Wish we could have discussed implementing a cap on individual contributions or other alternative solutions.
[/quote]

It's easy to spin new addresses so that wouldn't have worked.

-------------------------

SugoiBTC | 2023-06-16 17:34:18 UTC | #15

[quote="sumamu, post:14, topic:1484"]
Yes, all restrictions will be lifted after the campaign ends.
[/quote]

When does the Bootstrap campaign end exactly? Is the community able to vote on the duration of the campaign?

-------------------------

bayrum | 2023-06-17 07:14:18 UTC | #16

- We were lulled with early bootstrap rewards!!!!  Stacked eth it’s 44 eth not 120eth(because only 60k znn is stacked) !!!! in this way we need 20x price to touch those early bootstrap rewards, we are not going to 20x even with honeypot and 1 year from here
- Honeypot it’s a failure, almost one week since we cannot sell and we sold only 1k 😂😂😂😂😂😂, in this way after honeypot ends we would have sell 10kznn and no significant eth added. 
Overall- bootstrap being accesed only by hitting  1000eth it’s a scam against early providers whom got promised something else and now it’s going to be unattainable.

-------------------------

romeo | 2023-06-17 08:05:53 UTC | #17

I'd suggest we stop referring to the LP as a honeypot.

It's clearly not and it projects bad optics particularly if people are googling/researching it and these posts come up

Yes we can't sell at he moment, yes it was advertised as such and was expected, no it is not permanent.

-------------------------

sumamu | 2023-06-17 08:23:50 UTC | #18

Well said. Also, anyone can create new wZNN markets on Uniswap with other ERC20s: 
- wZNN <> DAI
- wZNN <> USDT
- wZNN <> USDC
- and so on

-------------------------

bayrum | 2023-06-17 08:48:47 UTC | #19

June 12 - "Liquidity bootstrap & provisioning campaign starts today."

"However, during the bootstrap campaign, participants will receive extra rewards and additional security measures."

Where are the extra rewards for early LP? Liquidity bootstrap campaign started one week ago and no extra rewards as promised!!!!

-------------------------

sumamu | 2023-06-17 09:18:36 UTC | #20

[quote="bayrum, post:19, topic:1484"]
Where are the extra rewards for early LP? Liquidity bootstrap campaign started one week ago and no extra rewards as promised!!!
[/quote]

The extra rewards are being discussed here. We need to decide on the intervals for the multipliers.

-------------------------

TrevorLeahy3 | 2023-06-17 16:08:41 UTC | #21

So to be clear the rewards are payed to ZNNETHLP holders on NoM but the threshold interval for the amount of ETH is on the etherium side?

Participating in the LP is considerably more risky than collecting staking rewards or delegating so if their APR is around 15% would be fair to see the LP rewards hold above maybe 50% or more. 

So theres plenty of room to dilute the pool a bit more and still have a strong APR. 

Would suggest an interval of 500ETH or if we're really feeling generous a lower amount maybe even 321ETH

What needs to happen from a security/testing perspective during this campaign? Is there anything we can be pushing for to make the most of this cap/window? Put out some bug bounties?

-------------------------

sumamu | 2023-06-19 09:29:28 UTC | #22


[poll name=poll3 type=regular results=on_vote chartType=bar close=2023-06-20T23:45:00.000Z]
# Vote liquidity bootstrap interval step
* Use 300 eth for the liquidity bootstrap multiplier
* Use 500 eth for the liquidity bootstrap multiplier
* Keep 1000 eth for the liquidity bootstrap multiplier
[/poll]

Second, there's been an error with the with the amount of liquidity added and the cap. It was set at 100k wZNN, however, there are way more wZNN already added. So to fix this, the cap should be equal to the current amount of wZNN in the pool.

Should the liquidity cap be increased from 100k wZNN to 162k wznn?
[poll name=poll4 type=regular results=on_vote chartType=bar close=2023-06-20T23:45:00.000Z]
# Vote liquidity cap increase
* Increase liquidity cap to 162k wZNN
* Keep  liquidity cap at 100k wZNN
[/poll]

-------------------------

ZNNAYIID | 2023-06-19 10:12:33 UTC | #23

Why not give the community an option to add more than the current amount? You are still not taking into consideration what the community thinks and still making your own decisions.
Also where is a poll for the 30 days cap, and whether you should change that or not?

-------------------------

romeo | 2023-06-19 10:27:03 UTC | #24

I'm keen to know when/how the cap will be lifted - as that would provide guidance on my vote for the liquidity bootstrap interval level

-------------------------

ZNNAYIID | 2023-06-19 10:28:37 UTC | #25

I really feel like this poll was made to make the community believe that you are now more open to discuss and take into consideration what community believes is the right decision, but in reality this poll has a few options chosen by you, not the community.

-------------------------

sumamu | 2023-06-19 10:40:36 UTC | #28

Both aspects have been discussed before. The liquidity cap is only for the first 30 days and it has 2 purposes:
- reduce risks
- consolidate liquidity on the way up

If most liquidity is added at the current ratio, it will be more difficult for the price to go up. This way, every time ETH is swapped to wZNN, more liquidity can be added. 

Once the 30 days passed, all limitation are disabled. Liquidity bootstrap campaign started on June 12th.

-------------------------

vibe.znn | 2023-06-19 11:59:26 UTC | #29

[quote="sumamu, post:28, topic:1484"]
Liquidity bootstrap campaign started on June 12th.
[/quote]

So July 12th we can both sell AND add liquidity in the current pool? why is everything so opaque with this process ...?

-------------------------

aliencoder | 2023-06-19 13:46:31 UTC | #30

[quote="sumamu, post:28, topic:1484"]
If most liquidity is added at the current ratio, it will be more difficult for the price to go up
[/quote]

Better consolidate at $10 than at $1... at least we have a chance to be sustainable at $10 and more

-------------------------

sultanofstaking | 2023-06-19 14:02:26 UTC | #31

We need something to encourage buys tho, at this pace we will be at $10 in 2026

-------------------------

aliencoder | 2023-06-19 14:06:28 UTC | #32

I think next year we'll be at least $30 if we continue delivering stuff

-------------------------

sumamu | 2023-06-19 15:44:41 UTC | #33

[poll type=regular results=on_vote chartType=bar public=true close=2023-06-20T23:45:00.000Z]
# Remove cap for liquidity bootstrap?
* Yes
* No
[/poll]

-------------------------

sumamu | 2023-06-19 14:18:56 UTC | #34

[quote="sultanofstaking, post:31, topic:1484, full:true"]
We need something to encourage buys tho, at this pace we will be at $10 in 2026
[/quote]

Affiliate program coming in a few weeks and it will give everyone a way to get incentivized for finding ways to bring in new Alienz.

-------------------------

georgezgeorgez | 2023-06-19 14:19:08 UTC | #35

[quote="aliencoder, post:30, topic:1484"]
Better consolidate at $10 than at $1…
[/quote]

Better consolidate at $100 than $10...

We can temporarily divorce the pool from the full effects of free market forces to try and create upward price action. But that will only work so long as new LPs believe price equilibrium is moving along with it.

[The more you extend a spring...](https://en.wikipedia.org/wiki/Hooke's_law)

-------------------------

aliencoder | 2023-06-19 14:23:04 UTC | #36

That's why we need marketing asap. Any kind of marketing efforts should be encouraged at this point.

-------------------------

sultanofstaking | 2023-06-19 14:54:23 UTC | #37

I think if this were positioned as we are doing a guarded launch of the bridge for 45 days. We are doing this because we need time to draw early liquidity, continue testing including security and reward functionality, onboard guardians etc etc. We also need this time to finish the affiliate program which will launch in parallel w/ lifting of the restrictions on the bridge (assuming no critical issues are identified - we will let you if that were to happen). During this period, the best thing you - the community can do is begin thinking about how you will attract new aliens to our community using your affiliate link and begin testing your strategy to fine tune it in time for the full launch. Here is link to affiliate program to help you / link to successful examples of how others have done this. Start building interest now so when this launches we are in the best position....

Ok super long ramble but you get the idea. I would basically have zero questions and say "ok... makes sense". 

It is the silence where we fill in the gaps ourselves and next thing you know you have loose cannons like myself posting twitter polls :)

-------------------------

sumamu | 2023-06-19 14:52:44 UTC | #38

Can an admin make voters public for this poll, please? I forgot to check that box.

-------------------------

mehowbrainz | 2023-06-19 15:44:56 UTC | #40

Done.

-------------------------

sumamu | 2023-06-19 15:45:14 UTC | #41

Thanks! Did that reset the votes?

-------------------------

mehowbrainz | 2023-06-19 15:45:38 UTC | #42

Looks like it!

-------------------------

sumamu | 2023-06-19 15:49:00 UTC | #43

Everyone, please vote again!

-------------------------

mr.ztark | 2023-06-19 16:34:46 UTC | #44

tldr; If the LP is too deep, the market price can not move.

The conversation about the LP has been too much focused on the rewards, and not enough focused on how deep the LP should be.

It matters less, whether LPs are getting fat rewards, than whether the LP for our only trading pool is at proper depth.

The fat rewards are designed to offset (hopefully) high impermanent loss, but the price will never move if the LP gets too deep. The dilemma is that when people only look at current price, they might overcrowd the pool. This causes the price to not go up, and while those participants might reap rewards for 12 months, this whole project could just fizzle out if the price doesn't move for 12 months,

I believe market decentralization - but achieving that is a process. And that is probably what @sumamu is trying to achieve.

Education and gradual steps are crucial. If a bunch of people ape into the LP because of the community fanfare and complaints about fat rewards, without understanding what they are doing, it's just going to backfire on everyone at large.

1. The rewards will not be fat, they will just be slightly ahead of sentinel rewards.
2. The price of ZNN will not be able to increase, which devalues AZ and everyone's stake.
3. If by some miracle, the price does overcome of the excessively-deep LP, participants will get rekt by impermanent loss.

I hope some people with more knowledge on this subject will chime in on this frequency. 

My observation is that you want between 10%-20% of the value of the circulating supply mcap to be in the LP. With ZNN at such a low and undervalued mcap, we would ideally be at 10%. 

I think some people are already having this conversation and some have it in their minds, but it is going over the heads of many, and completely missed by even more.

-------------------------

mr.ztark | 2023-06-19 16:51:49 UTC | #45

Is there more advantage to having a thin (right-sized) LP and allowing some people to get fat rewards initially, who will then get rekt by IL while we moon back to $26?

It's hard to speculate because of the time axis, but does anyone have 1 or more permutations for what ZNN market price needs to reach in order for (LP impermanent loss) + (LP rewards) to breakeven over 12 months?

One of my points is to caution people on having strong opinions that may not be fully informed and knowledgeable. 

We have a tendency to form opinions on everything, because we are conditioned to do so.

“You always own the option of having no opinion. There is never any need to get worked up or to trouble your soul about things you can't control. These things are not asking to be judged by you. Leave them alone.”

― Marcus Aurelius

-------------------------

sultanofstaking | 2023-06-19 16:59:01 UTC | #46

[quote="mr.ztark, post:45, topic:1484"]
One of my points is to caution people on having strong opinions that may not be fully informed and knowledgeable.
[/quote]

100% agree with this - myself included.

But in order for any of this to work we need buyers right? Otherwise we’re just waiting 30 days for the same result.

-------------------------

sumamu | 2023-06-19 17:08:07 UTC | #47

Amazing read @mr.ztark! You are right about many things and it's clear you have a good understanding on how these aspects impact the market. You'd bring a lot of value to the community by sharing more insights and educating us.

-------------------------

sultanofstaking | 2023-06-19 17:08:34 UTC | #48

One thing I fully agree with is George’s point on more discussion being required. I logged in earlier and was excited to see 11 people in here. I should not be excited to see 11 people lol

To ztarks point earlier I think many votes in these polls would change if they had a better understanding of the dynamics at play

-------------------------

mr.ztark | 2023-06-19 17:11:10 UTC | #49

Yes, 100 percent. We need new Aliens. 

Are you suggesting that opening up the LP will bring in new LPers? 

I'm not assuming that's what you're saying, but I don't know I believe that someone who is not already zenonized is going to buy a big bag of ZNN and pair with ETH to collect NoM rewards.

I feel like the LP program is a hedge play and incentivized development program designed for aliens. And that we should manage it as such.

...pursuant to this perspective... How about rewinding and framing it more truthfully: like this: 

**This is a highly incentivized and high risk program that ZNN Aliens may participate in, in order to bootstrap the ZNN/ETH LP. Only the most knowledgeable and risk tolerant aliens should participate. First come, first served.** *The pool / rewards / etc will be managed and optimized by Sumamu according to industry standards and with respect for the recommendations of subject matter experts in the community.*

This is really how it was, but in hindsight, people seem to be forgetting.

-------------------------

sumamu | 2023-06-19 17:11:33 UTC | #50

[quote="mr.ztark, post:49, topic:1484"]
**This is a highly incentivized and high risk program that ZNN Aliens may participate in, in order to bootstrap the ZNN/ETH LP. Only the most knowledgeable and risk tolerant aliens should participate.** *The pool / rewards / etc will be managed and optimized by Sumamu according to industry standards and with respect for the recommendations of subject matter experts in the community.*
[/quote]

Where should we put this?

-------------------------

dat_she_pepe | 2023-06-19 17:42:42 UTC | #51

Make a cool no boomer game

-------------------------

mr.ztark | 2023-06-19 17:46:22 UTC | #52

And full disclosure, I am not participating in the LP.

-------------------------

sultanofstaking | 2023-06-19 17:52:41 UTC | #53

[quote="mr.ztark, post:49, topic:1484"]
Are you suggesting that opening up the LP will bring in new LPers?
[/quote]

No. I think the affiliate program is great but of course there are challenges in drawing a large number of people to a limited bridge. 

Maybe a game would work but not sure what can be deployed in time.

Feels like the marketing aspect is the missing link to this entire thing and with $200 volume over 30 days we’re just waiting hoping someone will ape in. 

Maybe I’m missing something

-------------------------

mr.ztark | 2023-06-19 18:08:09 UTC | #54

I agree. The eth pair is awesome and carries deeper implications that will be revealed and I look forward too expounding upon, zoon. Once we have this incredible marketing incentive program that mehowz is building, we are going to start to move forward in a very powerful way.

-------------------------

dat_she_pepe | 2023-06-19 18:23:01 UTC | #55

A marketing program in a bear market is a bad idea. But that's another topic.

-------------------------

bayrum | 2023-06-19 18:29:17 UTC | #56

Why exactly? We can gather more people, we get more exposure, more buyers, more developers will hear about us, more traction.

-------------------------

ZNNAYIID | 2023-06-19 19:27:20 UTC | #57

For those who still didn’t vote, liquidity bootstrap is basically more rewards (which were accumulated during these past months) in addition to orbital rewards, so basically the question is : do you want this bootstrap rewards to be given to the 20 persons providing liquidity or more providers should join. 

I get that some people want “thin” liquidity so we can finally “moon” but as you can see since the cap was implemented no one is buying lol

-------------------------

rexznn | 2023-06-19 19:55:52 UTC | #58

I think what the guys above said makes sense, if we have hella deep liquidity at current price ($1.30ish), it won't move much even on decent volume which makes our whole task more difficult. 

Unless you are expecting some big listing that promotes Zenon very broadly where we get attention from the market (like trending on CG and Twitter) then this isn't a good idea. We have to build this attention and liquidity up in lockstep and it won't happen overnight.

-------------------------

ZNNAYIID | 2023-06-19 20:04:37 UTC | #59

and you think when the price pump on thin liquidity, it will be easy to get more lp providers so we can't prevent dumping on this thin liquidity? it's not that easy really. 
We will end up with a shitty chart just like the one we had before on bsc. 
cmc and  coingeckop reseted our chart, so let's grow slowly and steadily and don't ruin this one again.

-------------------------

sumamu | 2023-06-19 21:13:13 UTC | #60

I'm abstaining from voting so I don't influence other's choice.

-------------------------

sultanofstaking | 2023-06-19 21:11:28 UTC | #61

Thats not fair

-------------------------

sultanofstaking | 2023-06-19 21:22:29 UTC | #62

I would rather just lock the entire bridge (buys, sells, LP) until affiliate is ready (assuming that is 30 days) then release both in parallel OR just lift all restrictions now. 

Maybe Sumamu knew nobody would buy and we would spend 30 days arguing amongst ourselves and they are just doing this for their pleasure.

-------------------------

sultanofstaking | 2023-06-19 21:28:25 UTC | #63

I tried to get my wife to buy some wZNN to help move the needle but she is in a bad mood.

-------------------------

sumamu | 2023-06-19 21:36:27 UTC | #64

Maybe try again next week?

-------------------------

mr.ztark | 2023-06-20 00:16:01 UTC | #65

The important thing is to right-size the LP for the sake of LP, and not for the rewards rate. Nobody can predict IL with certainty and you seems to be making a case based on the hindsight of seeing the ZNN/ETH price stagnate. 

These are factors that LP participants and non-participants should have considered. If I wanted to participate in this program I would have been the first.

-------------------------

crack | 2023-06-20 02:52:29 UTC | #66

[quote="sumamu, post:50, topic:1484"]
Where should we put this?
[/quote]

Once we click "add liquidity" ? 
And can you put the accurate APY on staking history base on real time APY

-------------------------

bayrum | 2023-06-20 06:48:12 UTC | #67

I agree, if they were really motivated to participate they would have been first, keeping their laptop with them everywhere and waiting for sumamu to launch the bridge. I do  not believe it’s a good idea that non-expert persons can decide the faith of bridge by voting. Sumamu was already doing a good job and his rules seems to work properly until now.(If now we vote the faith of the bridge it would have been better to vote the selling situation)
Bridge it’s a high risk investment for providers, and it’s should be high rewarding(Take into account huge impermanent loss, risk of hacking and losing the funds) by removing liqudity cap it will became a high risk investement low rewarding which is unfair for early motivated znn aliens + if we got hacked we lose more funds. Deeper liquidity= punishing the motivated people, rewarding the not so motivated people, price will not move up which is already very low.

-------------------------

bayrum | 2023-06-20 15:08:53 UTC | #68

![Screenshot (683)|521x123](upload://neEcAO5deJUAsoAR0xBkTGkXeAH.png)

@sumamu Are you taking in consideration to keep the cap for longer than mentioned? This would help the price moving faster upward and keeping the ROI positive for lp providers instead of having more lp providers leading possibly to a negative ROI for all of them.

-------------------------

aliencoder | 2023-06-20 15:16:11 UTC | #69

Very interesting. Many people complained that there is an artificial liquidity cap, but the voting result so far says otherwise.

-------------------------

sumamu | 2023-06-20 15:16:27 UTC | #70

[quote="bayrum, post:68, topic:1484"]
@sumamu Are you taking in consideration to keep the cap for longer than mentioned? This would help the price moving faster upward and keeping the ROI positive for lp providers instead of having more lp providers leading possibly to a negative ROI for all of them.
[/quote]

30 days, so July 12th. 

If the campaign would be successful it can be reconsidered, but right now we're having nearly zero marketing efforts, so none of the objectives are getting fulfilled: [consolidating liquidity] + [on the way up].

If there were substantial marketing efforts, the situation would be very different.

-------------------------

sumamu | 2023-06-20 15:20:33 UTC | #71

[quote="aliencoder, post:69, topic:1484, full:true"]
Very interesting. Many people complained that there is an artificial liquidity cap, but the voting result so far says otherwise.
[/quote]

Yeah, good luck building something while waiting for everyone to express, discuss and evaluate each other's opinions. 

We're getting ~50% Yes / ~50% No votes on important decisions.

-------------------------

bayrum | 2023-06-20 16:05:24 UTC | #73

1st scenario: selling is enabled on 12th july, big dump will happen and we get a pool of 200k-250k wznn and 100weth, we have to consolidate up from here. 

2nd scenario: selling is enabled, big dump to 200-250k wznn and 100weth, adding liquidity is allowed, pool will get deep to around 400k-450k?!?

 How to consolidate fast if buying 5000wznn will impact the price only 1%(pooled wznn 400-450k)?!?! 
 Selling 5000wznn with 162k wznn pooled price impact it’s 3.62%(see pic). 
 Mr.Stark said a good price impact for 5000znn at 1.35$ should be between 3.5%-5%. Without lifting the liquidity restriction price impact will decrease already to almost 2% after the dump and with market efforts we can go back to 3-5% price impact again. 
![image|230x500](upload://thErKk16VE7J54lNEgLIn3ukSxh.png)

-------------------------

sumamu | 2023-06-20 16:10:54 UTC | #75

Great, another alt. It's just a vote on a poll.

-------------------------

SugoiBTC | 2023-06-20 16:19:33 UTC | #76

wen yeezus pillar ser

-------------------------

ZNNAYIID | 2023-06-20 16:31:40 UTC | #77

Lol I thought the handle was mrkaine at first

-------------------------

dat_she_pepe | 2023-06-20 23:21:03 UTC | #78

u mad?

-------------------------

angelo_a_jr | 2023-06-21 14:45:47 UTC | #79

For anyone who wants to do the mathz on impermanent loss to make an informed decision on LP, here's a dead simple calculator.  Note this does NOT take into account the rewards but simply price action between the two tokens:


https://dailydefi.org/tools/impermanent-loss-calculator/

-------------------------

bayrum | 2023-07-15 09:06:50 UTC | #80

Are you still planning to add this paragraph on bridge page? And a message that the real roi% it’s not that on the page and can fluctuate due to impermanent loss.

-------------------------

