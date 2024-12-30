Thread: dynamic-plasma
0x3639 | 2023-02-09 17:39:00 UTC | #1

I'm working on the January 2023 Dev update and was thinking about the next priorities for the network.  Mr. Kaine thinks we should focus on dynamic plasma.  I came across this [post in Telegram](https://t.me/zenonnetwork/267337) written by Henlopedia and wanted to recreate (Copy / Paste) it here for discussion.  

--- 

Mr Kaine's comments about dynamic plasma difficulty really got me thinking about Plasma-nomics.
I came up with 2 simplified models how this could look.

I'm sure there are a bunch of flaws in my thinking, I'll try not to be too confusing. 
I would like to see your opinion on this.

## Assumptions 

Let's say NoM is a pipe, and we define the throughput from 1 - 10.
10 being maxed out. 

Now let's use these simple parameters to build a model and use arbitrary numbers for Plasma and QSR. 

We will suppose when NoM throughput == 1 that one transaction is equal to 100 Plasma which in turn is equal to 10 QSR 

So level 1 = lowest POW diff = 100 PLASMA = 10 QSR = 1 Tx ~ 100 SATS

## MODEL 1
Let's suppose this scales linear up to a threshold where it switches to exponential so that we approach infinity the closer we get to 10.

POW difficulty, PLASMA, QSR scale in the same direction

So it would look something like this 

level 1 = 100 PL = 10 QSR = 1 Tx ~ 100 SATS
level 2 = 200 PL = 20 QSR = 1 Tx ~ 200 SATS
..
level 7 = 700 PL = 70 QSR = 1 Tx ~ 700 SATS
level 8 = 1400 PL = 140 QSR = 1 Tx ~ 1400 SATS
level 9 = 1960000 PL = 19600 QSR = 1 Tx ~ 196000 SATS
level 10 = infinity = 1 Tx ~ all the SATS

This sort of table would have the desired effect of curbing usage as throughput limits are approaching, transacting would become increasingly expensive.

The game theory implications:

cons:

- users will need to acquire an ever increasing amount of QSR to maintain transaction parity as the network scales
- due to usage and burn QSR scarcity increases, making QSR more expensive
- users are required to keep up with an increasingly faster spinning hamster wheel to maintain their transaction parity and ability to participate, this disincentivizes the onboarding of new users
- QSR whales are incentivized to spam the network, at zero cost of their own, to artificiality bloat the throughput, and force higher plasma thresholds. This in turn increases QSR demand as more needed to maintain parity and inflates the price.

pros:
 
- Network can never be maxed
- Users can transact at zero cost by locking collateral 
- hamster wheel dynamic makes it probable that locked collateral increases in value over time  
- Eventually a transaction equilibrium is achieved as the QSR whales disperse their stacks to the masses. As this occurs the nature of transactions  shift to a utilitarian nature 

Observations:

This model somewhat mirrors the POW Ethereum paradigm where miners charge an increasing rate as network usage increases. Overall the base chain becomes increasingly expensive to use and incentivizes layer 2 solutions.

## MODEL 2

POW difficulty, PLASMA scale in the same direction BUT QSR scales inverse to PLASMA in the opposite direction. 

(The rate of scaling can be adjusted to different values - the main point here is that it runs opposite direction to Plasma)

So it would look something like this 

level 1 = 100 PL = 10 QSR = 1 Tx ~ 100 SATS
level 2 = 200 PL =  5 QSR = 1 Tx ~ 200 SATS
level 3 = 300 PL =  2.5 QSR = 1 Tx ~ 300 SATS
level 4 = 400 PL =  1.25 QSR = 1 Tx ~ 400 SATS
level 5 = 500 PL =  0.625 QSR = 1 Tx ~ 500 SATS
level 6 = 600 PL =  0.31258 QSR = 1 Tx ~ 600 SATS
level 7 = 700 PL =  0.15625 QSR = 1 Tx ~ 700 SATS
level 8 = 1400 PL = 0.078125 QSR = 1 Tx ~ 1400 SATS
level 9 = 1960000 PL = 0.00610351 QSR = 1 Tx ~ 1960000 SATS
level 10 = infinity = 0.00000372 QSR = 1 Tx ~ all the SATS


A lot of the same tenants present in this model as with model 1, but the game theory is way more interesting.

The game theory implications:

In this table there will be a point when the levels increase where QSR will be very undervalued.

Say we are at level 2, and a user has just been using POW for their daily transactions (2), it takes 5 min for each transaction. 
They have a good gaming GPU so it's no big deal they think. Now we go to level three and each transaction takes 10 min and they hear the GPU fans fire up.
They notice the QSR cost of transacting has just halved but their POW effort has increased, the market hasn't quite caught up and the price of QSR is still the same as before the increase. So they buy 5 QSR and fuse it for their daily needs. Now demand rises and price forms a new consensus around POW value. 
This would be very good incentive structuring .

In addition to this the users are even further incentivised because they are now in a reverse scenario than the hamster wheel in Model 1. They will never have to chase transaction parity after their initial acquisition unless usage dramatically drops.

Anyway these are just some initial thoughts about Plasma-nomics.

There are actually quite a few more things that I would like to add but I can't be fucked typing anymore.

Please try to finds any holes in the logic and/or conceptual flaws. Of course this is all speculation and I have no idea what the devs actually have in mind. Nothing in the whitepaper about this. Maybe I got a bit too carried away with assumptions and speculation lol.

-------------------------

TrevorLeahy3 | 2023-01-31 01:58:12 UTC | #2

I guess my big question's around what data/measurable we have reliably available to make ongoing adjustments from? If the pow difficulty here is on the individual account chains but were trying to manage throughput for everyone? 


Transactions per momentum wouldnt take into account the data exchange from msg or smart contracts.. Sol you mentionned something about a utilization modifier does that come into play here? With something like that couldnt  we just have a loop that floats the pow difficulty based on usage from a certain # of the previous momentums? 

Interesting models on increasing or decreasing QSR respective of Plasma ill have to think on that for a bit..

-------------------------

zyler9985 | 2023-02-01 03:12:13 UTC | #3

I think whether it's model 1,2 or a 3rd one, it's ideal to consider bad actors. Someone who wants to spam the network on purpose – so even if model 1 incentivises qsr whales to spam the network, is it easy for someone not already a whale? Not really because they'd have to buy all the qsr first. So model 1 is a protection against people coming in and buying up huge amounts of it, even though this will still happen.

Then balance countering bad actors, both rational and irrational (motivated by money vs malice) ... and balance this with what's best for the user. Remember most people have old shitty phones that overheat and so on from even small PoW... part of the block size wars in bitcoin was better decentralisation if old crappy hardware is still capable of doing the job. 

I know my thoughts aren't that organised on the topic, but these are initial concerns and considerations that come to mind.

-------------------------

mehowbrainz | 2023-02-09 17:39:12 UTC | #4

Topic moved to #development:funding-staging

-------------------------

romeo | 2023-03-06 12:04:14 UTC | #5

With Option 1 - what if the maximum fused Plasma an account could have is capped at a level lower than what would be required for Level 9 for example. That way - the incentive to spam the network to inflate the value of QSR is minimized as they would be impacting their own tx capacity.

Obviously any tx that would require more than maximum level of plasma would have to be something fairly significant 

should we start by brainstorming what type of txs would require a higher amount of plasma?

-------------------------

