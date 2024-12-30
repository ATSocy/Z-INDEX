Thread: ideas-for-dynamic-plasma
vilkris | 2023-11-16 23:06:07 UTC | #1

There has been a lot of discussion surrounding dynamic plasma lately, and different ideas have been presented by community members. I've spent some time researching the topic and I've attempted to combine some ideas in this post and present some ideas for a dynamic plasma implementation.

I didn't post this in the dynamic plasma thread, since I wanted to create a thread that focuses mainly on the pros/cons of the ideas presented in this post.

# Background
### Why do we need dynamic plasma
Currently our network has a hardcoded throughput limit of 100 account blocks per momentum. For an account block to be eligible for inclusion in a momentum, the account block has to have a minimum amount of plasma committed to it. This minimum amount of plasma needed is dependent on the type of the transaction. For example, calling an embedded contract requires a higher plasma commitment than a normal send transaction.

Since our network utilization rate is so low right now, this mechanism works without issues. There is always space in the momentum so users do not need to compete for their account block to get included in the next momentum.

Once the network utilization rate picks up, we will start running into problems. Since a momentum can fit a finite number of account blocks, there has to be a mechanism that allows users to compete for inclusion in a momentum.

### What is plasma
The founding team [introduced](https://medium.com/@zenon.network/plasma-the-new-fee-paradigm-for-the-next-gen-decentralized-network-4ec3f27e4a6b) plasma as "**an anti-spam mechanism that acts as the network gas**" and "**as a third dimension asset similar to the mana concept employed by many popular games**".

Based on this and based on the current implementation of plasma, we can come to the conclusion that plasma has three purposes: mitigating spam, representing a computational cost for transactions, and allowing for transactions to be prioritized (competing for inclusion in a momentum).

The current implementation only fulfills one of these purposes: representing a computational cost associated with a transaction. The anti-spam properties of the current implementation are relatively weak and there is no mechanism that allows for users to compete for inclusion in a momentum.

### Plasma as a representation of computational resources
Using "gas" to represent computational resources is a widely utilized concept in other blockchains such as Ethereum. Ethereum transactions require the user to commit a minimum amount of gas to the transaction in order for it to be eligible for inclusion in the next block. The minimum computational cost for a regular ETH transaction is 21,000 gas units. This amount of gas has to be committed to every transaction. The gas is paid for in ETH and the protocol burns this gas when the transaction is processed. This is only a theoretical minimum fee, since in practice the total fee for a transaction is more than this and fluctuates based on network usage.

The reasoning for why the requirement is 21,000 gas units can be found [here](https://ethereum-magicians.org/t/some-medium-term-dust-cleanup-ideas/6287). Based on Vitalik's explanation we can see that the gas units required for a transaction are based on the actual computational resources that are needed to process the transaction.

In our network a regular transaction also has a computational cost of 21,000 gas units, or rather, plasma. Whether these computational requirements are based on actual testing and benchmarking or just on guesstimation is unknown. The computational cost differs depending on the transaction's complexity. For example, calling an embedded contract to collect rewards has a computational cost of 73,500 plasma since it requires more computational resources to process the transaction.

The maximum account blocks allowed in a momentum is currently 100 and the amount of plasma the most expensive transaction requires is 105,000 (registering a pillar). Based on this we can calculate that the theoretical maximum computational units our network will currently process is 10,500,000 units per momentum.

### Plasma as a transaction prioritization mechanism
As stated before, our network doesn't have any transaction prioritization mechanism currently, but plasma can be used for this purpose, with the basic idea being that committing more plasma to the transaction means higher prioritization of the transaction.

### Plasma as an anti-spam mechanism
The third purpose of plasma is to work as an anti-spam mechanism. To me, on-chain spam can be defined as any activity that floods the chain with transactions with the intention to significantly limit the ability of others to use the network. There can be many reasons for conducting a spam attack - for financial gain, for example.

The most common anti-spam mechanism used by networks is to require a transaction's sender to pay a fee. The idea being that the cost of fees will be greater than the potential gain from an attack.

I think that the anti-spam properties of our current plasma implementation are limited, mainly because the rate at which plasma is currently "recharged". It's too fast to effectively throttle an account's ability to send transactions.

# Ideas for an initial dynamic plasma implementation
Below are some ideas for how to fulfill the goals presented above. Example implementations and pseudo-code examples of  the following algorithms can be found [here](https://github.com/vilkris4/dynamic-plasma-ideas).

## Goal 1: Computational resources
This goal is already partially met in the current plasma implementation. But since we have finite momentum space, we need to increase the cost of computational resources when demand increases.
To meet the goal, we could utilize a dynamic algorithm that adjusts the "price" of computational resources based on network utilization which is readjusted on every momentum.

The basic idea being that the readjustment algorithm targets half full momentums. This means that if the previous momentum was more than half full, the price of plasma increases. If the previous momentum was less than half full, the price of plasma decreases. If the momentum was exactly half full, then the price stays the same. For a transaction to be eligible for inclusion in the next momentum, the account block has to commit at least the base plasma requirement for the transaction multiplied by the minimum price of plasma, the "base price".

Instead of the current per momentum transaction cap, we would have a per momentum base plasma cap, since different transactions require a different amount of base plasma as explained before.

The price of plasma will increase exponentially if there are momentums that are over half full consecutively, meaning that it is economically unviable for momentum size to stay high indefinitely.

Example:

| Momentum Height | Momentum Fullness | Base Price  | Price Change |
|---|---|---|---|
|1|50%|1000|0%
|2|100%|1000|0%
|3|100%|1125|12.5%
|4|100%|1265|12.5%
|5|100%|1423|12.5%
|6|100%|1600|12.5%
|7|100%|1800|12.5%
|8|100%|2025|12.5%

The main benefit of targeting half full momentums, instead of full momentums, is that the base price for plasma is adjusted algorithmically, reducing the need for a bidding war among users when there is a short term spike in momentum space demand. It is also easier for wallets to predict the minimum plasma price needed for a transaction.

This is similar to how Ethereum's current fee adjustment algorithm works as described in [EIP-1559](https://eips.ethereum.org/EIPS/eip-1559).

## Goal 2: Transaction prioritization
Even with a dynamically adjusting base price for plasma, there still needs to be a way to prioritize transactions in the situation where the momentum cannot fit all the transactions that are eligible. This could be achieved by simply prioritizing account blocks based on the price of plasma used in the account block.

`plasmaPrice = ab.UsedPlasma / ab.BasePlasma`

To be eligible for inclusion the account block must fulfill: `plasmaPrice >= momentum.BasePrice`

This allows a user to commit more plasma to their transaction than what is needed, in order to have a better chance of being included in the next momentum if the network is congested.

Note 1: Account blocks sent by embedded contracts have endless plasma and should probably always have the highest priority, so this is something that has to be taken into account when determining the per momentum base plasma cap.

Note 2: Since we currently have no way of "forcing" pillars to order transactions in a specific order, there is no way to guarantee that pillars prioritize transactions as intended. I think the best that we can do right now, is minimize the incentives for pillars to alter the ordering of transactions.

## Goal 3: Anti-spam
The anti-spam aspect of plasma is probably the trickiest goal to achieve, depending on what the requirements are. The dynamic adjustment algorithm presented in Goal 1 works as an anti-spam mechanism, but it is probably not enough on its own.

### PoW Plasma anti-spam
Currently there is a hard coded PoW-to-Plasma conversion rate, meaning that a given amount of PoW will always be converted to a specific amount of plasma. Currently there is also a hard coded limit to how much PoW can be converted to plasma for an account block.

If account blocks are prioritized based on plasma, then having a hard coded limit to how much PoW plasma can be generated can make PoW transactions unviable when there's high demand for momentum space.

But if the hard coded cap, for how much PoW plasma can be generated, is removed, then a user with a significant amount of computing power would be able to generate huge amounts of plasma and gain an undue amount of control over total network bandwidth.

To mitigate this problem, we could introduce a dynamic PoW-to-Plasma conversion rate (difficulty-per-plasma), that is dependent on network utilization and how much of the total plasma is being generated by PoW.

In the example algorithm a difficulty-per-plasma value is readjusted on every momentum. The target PoW plasma rate in a momentum is set to 20% - this means that when the momentum is over or equal to half full, the PoW plasma percent should be 20%. If it's less than that, the difficulty-per-plasma will decrease, if it's more than that, the value will increase. If the momentum is less than half full, the PoW plasma target is 100%, meaning that the PoW plasma percent can be 100% of the momentum without penalty.

The example algorithm's output when PoW plasma is 100% of the momentum's plasma and the momentum is equal to or over half full:
| Momentum Height | Momentum Fullness| PoW plasma | Difficulty-per-plasma | Difficulty-per-plasma change |
|---|---|---|---|---|
|1|>=50%|100%|1000|0%
|2|>=50%|100%|1500|50%
|3|>=50%|100%|2250|50%
|4|>=50%|100%|3375|50%
|5|>=50%|100%|5062|50%

The example algorithm's output when PoW plasma is 10% of the momentum's plasma and the momentum is equal to or over half full:
| Momentum Height | Momentum Fullness| PoW plasma | Difficulty-per-plasma | Difficulty-per-plasma change |
|---|---|---|---|---|
|1|>=50%|10%|1000|0%
|2|>=50%|10%|937|-6.3%
|3|>=50%|10%|878|-6.3%
|4|>=50%|10%|823|-6.3%
|5|>=50%|10%|771|-6.3%

With this algorithm, even a user with a significant amount of computing power, would not be able to occupy over 20% of momentum space indefinitely.

### Fused Plasma anti-spam
Currently, whenever fused plasma is used to send a transaction, that plasma gets recharged once the transaction is confirmed. This means that, if transactions are prioritized based on plasma, a malicious user with a significant amount of QSR could easily outbid others for inclusion in a momentum.

This problem is relevant since we will probably have to continue to have a conservative network max throughput, even with dynamic plasma, at least initially. My view is that we don't really have any data to justify raising this throughput limit. Raising the throughput limit is generally a centralizing force, so we would need to do benchmarking to find a throughput limit that can be handled by regular consumer hardware. We want users to be able to run their own nodes.

To work around this problem, we could introduce a dynamic plasma recharge rate, so that fused plasma gets recharged at a rate that is dynamically adjusted. Instead of only requiring one confirmation to recharge all fused plasma, the plasma would be recharged at a per confirmation recharge rate.

This will act as a counter force to the temptation of excessively committing plasma to a transaction. The more plasma committed, the longer it will take to get it recharged, limiting an account's ability to occupy momentum space and freeing up bandwidth for other users. This recharge rate would be dependent on the current network utilization rate.

Example of the recharge rate algorithm (recharge rate = QSR/confirmation):
| Momentum Height | Momentum Fullness | Momentum Recharge Rate | Target Recharge Rate  | Recharge Rate Change |
|---|---|---|---|---|
|1|0%|100|100|0%
|2|100%|50|0.01|-50%
|3|100%|25|0.01|-50%
|4|100%|12.5|0.01|-50%
|5|100%|6.25|0.01|-50%
|6|100%|3.12|0.01|-50%
|7|100%|1.56|0.01|-50%
|8|100%|0.78|0.01|-50%
|9|100%|0.39|0.01|-50%
|10|100%|0.2|0.01|-50%
|11|100%|0.1|0.01|-50%
|12|100%|0.05|0.01|-50%
|13|100%|0.02|0.01|-50%
|14|100%|0.01|0.01|-50%

Another example:
| Momentum Height | Momentum Fullness| Momentum Recharge Rate | Target Recharge Rate  | Recharge Rate Change |
|---|---|---|---|---|
|1|100%|0.01|0.1|0%
|2|50%|0.02|1|100%
|3|50%|0.04|1|100%
|4|50%|0.08|1|100%
|5|50%|0.16|1|100%
|6|50%|0.32|1|100%
|7|50%|0.64|1|100%
|8|50%|1|1|56%

From these examples we can see that every momentum has its own plasma recharge rate depending on how full the momentum is and what the previous momentum's recharge rate was. The account chains that have an account block included in a given momentum will be subject to the plasma recharge rate of that momentum.

This introduces a "real" penalty for using fused plasma, since when there is high demand for momentum space, it will take a long time for plasma to recharge.

For example: If account chain A included an account block in momentum 5, and committed 10 QSR as fused plasma to that account block, it would take 63 confirmations (~10 minutes) to fully recharge the fused plasma.

[Here](https://github.com/vilkris4/dynamic-plasma-ideas/blob/main/available_plasma.js) is a pseudo-code example of how the committed, or "confined" plasma, is calculated so that the current available fused plasma for an account chain can be calculated.

Note: In order to not overload terms used in the existing go-zenon codebase, I'm using the term "confined" to mean the plasma that is committed to account blocks and that cannot be used until it has been recharged. 

#### Fused plasma recharge rate considerations
One downside of this recharge rate idea is that it limits addresses to a low maximum sustained TPS. If the recharge rate is 1 QSR/confirmation, when blocks are at target fullness, then this means that every address is limited to a sustained throughput of ~0.01 TPS (assuming no PoW is used). This is also assuming the plasma base price is only 1.

For the vast majority of users this would probably not be an issue, but businesses and more complex use cases may well need a higher sustained TPS.

To alleviate this problem, we could also introduce a recharge rate multiplier that would linearly increase the recharge rate of accounts that have more than some threshold amount of QSR fused. This would probably have to be accompanied by some kind of account level limit of how many transactions could be sent within n momentums.

If the network max throughput can be increased, then the recharge rates could also be increased.

# Attack scenarios
Below are a few examples of how the proposed ideas for dynamic plasma would help mitigate the effects of spam attacks.

### Scenario 1: Fused Plasma spam
I simulated the following attack scenario with the example code, where the attacker owns 1M QSR and fuses it as plasma evenly to 20,000 addresses (50 QSR per address). His goal is to block users that have less than 50 QSR fused from using the network.

```
Attack result
------
Able to block users with less than 50 fused QSR for 29.17 minutes
Attack can be repeated in 227.27 minutes
```
From the result we can see that users with less than 50 QSR would basically have to wait a maximum of ~30 minutes for their transaction to be included in a momentum. They would also be subject to a very slow plasma recharge rate, unless they wait for network demand to decrease. The attacker could repeat the attack in ~3 hours and 47 minutes.

This is of course a highly simplified simulation since there would most likely be users with more than 50 QSR who would still be able to use the network during the attack, which would result in a longer waiting time for someone with only 50 QSR. On the other hand, if the attacker is only using fused QSR, then the PoW difficulty will decrease, making it easier for users to generate plasma via PoW.

### Scenario 2: Fused Plasma spam
We can modify the first scenario a bit and say the attacker's goal is to block users that have less than 1000 QSR fused from using the network.

```
Attack result
------
Able to block users with less than 1000 fused QSR for 0.67 minutes
Attack can be repeated in 430.50 minutes
```
We can see that in this scenario the attacker would only be able to block users with less than 1000 QSR for ~40 seconds and would have to wait ~7 hours and 10 minutes to repeat the attack. 

### Scenario 3: Pre-computed PoW attack
This needs more consideration, but I'm not sure if the dynamic difficulty adjustment is enough to mitigate this attack vector; someone pre-computing a massive amount of PoW over days, months, years, and then using it spam the network. Should PoW expire?

# What about burning ZNN to generate plasma
The adjustment mechanisms presented in this post can be adjusted, so that new ways of generating plasma can be introduced. If it makes sense from a tokenomic, marketing, and technical standpoint.

Hard coded targets for different "plasma resources" can be introduced, or the plasma resources can directly compete with each other and let market forces dictate at what rate different resources are used.

For example, we could add novel ways of generating plasma, like burning some amount of Bitcoin would generate some amount of plasma. This may not actually make sense, but the point is we could potentially unlock new use cases like this.

# Remarks
This post became longer than I initially intended. It has lots of stuff to consider, so I appreciate anyone taking the time to read through it. Since there are many angles to consider when it comes to a dynamic plasma solution, I may have failed to consider something important, so feedback and critique is welcomed.

-------------------------

Chadass | 2023-11-16 23:46:10 UTC | #2

Amazing. Literally amazing.

-------------------------

0x3639 | 2023-11-17 00:42:35 UTC | #3

This is really thoughtful @vilkris.  Thank you very much for working on this.  I will read a few times and prepare some questions.

-------------------------

georgezgeorgez | 2023-11-17 01:01:55 UTC | #4

Definitely need more time to digest it. 
Thanks for putting your thoughts in a well formatted / readable manner as always.

My impressions after an initial appetizer read through:

I like the reference to EIP-1559. A lot of the motivations they cite we will share if not now then later. But need to think hard about what makes sense for feeless. The incentives/psychology around bidding wars are a little different.

Per momentum plasma recharge seems to introduce a lot of complexity.
What kind of data structures/indices will be needed to support it?
What's the worse case for additional computations needed per momentum on nodes?

PoW to Plasma method, nothing controversial here. Main parameters would be the target %, adjustment period, and adjustment rate/curve.

-------------------------

sol | 2023-11-17 01:50:12 UTC | #5

Thank you very much for your thoughtful and well-written post about dynamic plasma.

I wasn't a fan of dedicated bandwidth/lanes, and I'm glad to see your ideas align with the philosophy of indiscriminate plasma consumption instead of segregating transactions into different queues.

I also appreciate the modeling work you've shared with us; this can be used to conduct further experimentation if we choose to adjust the initial variables.

re: increasing throughput limit
I agree that the current throughput is sufficient at this time, in terms of AccountBlocks/Momentum and data/AccountBlock.

-------

[quote="vilkris, post:1, topic:233"]
The account chains that have an account block included in a given momentum will be subject to the plasma recharge rate of that momentum.
[/quote]

I have similar concerns as George.
Will this recharge rate variable be stored in account chains, or indexed elsewhere like the plasma contract?
If an account has a recharge rate of 0.01, then the network decongests, can they claim a more optimal recharge rate by submitting another transaction?
Or will their initial transaction's plasma continue to emit at the same rate?

[quote="vilkris, post:1, topic:233"]
we could also introduce a recharge rate multiplier that would linearly increase the recharge rate of accounts that have more than some threshold amount of QSR fused. This would probably have to be accompanied by some kind of account level limit of how many transactions could be sent within n momentums.
[/quote]

Similar thought here: where would we track transactions-per-address-per-period?

I'm unsure if we should implement global (per momentum) recharge rates. 
If we're considering tracking rates per address, maybe we can only target accounts that are significantly contributing to congestion.
I expect this to be more complex but it could lead to a better experience for low-frequency, low-fuse addresses.

-----

For pre-computed PoW, would the following be feasible?
Let's say nodes only accept PoW nonces that were generated within the last N momentums.
* Nodes provide a difficulty to client
* Client must generate a PoW nonce based on the difficulty and a recent momentum N's hash
* Client signs their AccountBlock and broadcasts it
* Nodes must verify that the PoW nonce meets the difficulty requirement and could only have been generated with N momentum's hash, potentially having to iteratively calculate until a match is found or all options are exhausted.

For this solution, I'm concerned about the validation load for nodes.

-------

Some other considerations that I mentioned in a previous post:
1. fused QSR limitations
2. exceptions, such as guaranteed tx priority for certain tx types
   - "Account blocks sent by embedded contracts have endless plasma"
   - Can we also include calls to Plasma.fuse()? This should improve the onboarding experience.
3. RBF, but with more plasma

-------------------------

coinselor | 2023-11-17 02:45:57 UTC | #6

[quote="vilkris, post:1, topic:233"]
Note 2: Since we currently have no way of “forcing” pillars to order transactions in a specific order, there is no way to guarantee that pillars prioritize transactions as intended. I think the best that we can do right now, is minimize the incentives for pillars to alter the ordering of transactions.
[/quote]

Can someone please elaborate on what Vilkris means by 'minimize the incentives for pillars to alter the ordering of transactions'? Are we talking future nasty stuff like MEV? We don't have zApps and seems like the idea is to keep the base layer lean, so there shouldn't be much to be gained, what are they going to do prioritize an AZ vote or a collection of rewards? Additionally, wouldn't this be a non-issue once pow-links are implemented?

Finally, why wouldn't we be able to force transaction ordering based on plasma with the same spork that implements dynamic plasma?

-------------------------

vilkris | 2023-11-17 10:37:52 UTC | #7

[quote="georgezgeorgez, post:4, topic:233"]
Per momentum plasma recharge seems to introduce a lot of complexity.
What kind of data structures/indices will be needed to support it?
What’s the worse case for additional computations needed per momentum on nodes?
[/quote]

[quote="sol, post:5, topic:233"]
Will this recharge rate variable be stored in account chains, or indexed elsewhere like the plasma contract?
[/quote]

Currently calculating an account's available plasma requires 3 database reads. With the recharge rate, it would require 6 database reads, without increasing the amount of indexes. The current "chain plasma" database index would be replaced with a "confined plasma" index.

This is meant to replace/improve the existing concept of account chain "committed" plasma.

[quote="sol, post:5, topic:233"]
If an account has a recharge rate of 0.01, then the network decongests, can they claim a more optimal recharge rate by submitting another transaction?
Or will their initial transaction’s plasma continue to emit at the same rate?
[/quote]
With the pseudo code example I provided, they could claim a new recharge rate by submitting a new transaction. This might not be something we would want, so I need to think about it a bit.

[quote="sol, post:5, topic:233"]
Similar thought here: where would we track transactions-per-address-per-period?
[/quote]
I don't know yet. Maybe in the database.
[quote="sol, post:5, topic:233"]
I’m unsure if we should implement global (per momentum) recharge rates.
[/quote]
It has tradeoffs, but I think globally rate limiting fused plasma usage is a reasonable way to distribute the limited network bandwidth amongst different addresses.
[quote="sol, post:5, topic:233"]
If we’re considering tracking rates per address, maybe we can only target accounts that are significantly contributing to congestion.
[/quote]
I'm not sure how this could be done in a fair manner. A spammer can disguise himself as a "regular user" with endless on-chain identities. Like in the example attack scenario 1, the attacker is using 20,000 addresses, and can send transactions at a very low per-address rate, but at a very high combined rate. Ultimately what the recharge rate does is it attempts to distribute bandwidth to as many addresses as possible when there is high network usage.

[quote="sol, post:5, topic:233"]
I expect this to be more complex but it could lead to a better experience for low-frequency, low-fuse addresses.
[/quote]
With the recharge rate, I think the experience would be relatively good for low-frequency addresses in a congested network. Since if you have enough fused plasma to send a few consecutive transactions at a time, it won't matter if it takes hours to get it back, if you only need to send a few transactions a day.

[quote="sol, post:5, topic:233"]
and could only have been generated with N momentum’s hash
[/quote]
Can this be done? If so, maybe we could add the account block's `momentumAcknowledged.hash` to the PoW hash and require the `momentumAcknowledged.height` property to be at max N distance from the frontier height. It should have a negligible effect on computational load to validate it.

[quote="sol, post:5, topic:233"]
1. fused QSR limitations
[/quote]
I don't think the ideas proposed in my post would require any limitations on fused QSR per account.

[quote="sol, post:5, topic:233"]
* * Can we also include calls to Plasma.fuse()? This should improve the onboarding experience.
[/quote]
How to prevent abuse?

[quote="sol, post:5, topic:233"]
3. RBF, but with more plasma
[/quote]
Yes, this needs to be considered.

-------------------------

vilkris | 2023-11-17 10:50:01 UTC | #8

[quote="coinselor, post:6, topic:233"]
Can someone please elaborate on what Vilkris means by ‘minimize the incentives for pillars to alter the ordering of transactions’? Are we talking future nasty stuff like MEV?
[/quote]
This was just a general comment that we should keep in mind that pillars can decide the ordering of transactions as they wish (by customizing go-zenon). So an initial dynamic plasma solution should take this into account and ideally not introduce new incentives to pillars to alter the ordering. The ideas in my post should not introduce any new incentives in that regard.

In the future we can implement ways to enforce a certain ordering of transactions.

-------------------------

0x3639 | 2023-11-17 11:22:01 UTC | #9

[quote="vilkris, post:1, topic:233"]
The main benefit of targeting half full momentums,
[/quote]

Why 50% and not 75% or some other number less than 100% but greater than 50%?  Will a higher percent allow for more block utilization without adjustments?

[quote="vilkris, post:1, topic:233"]
One downside of this recharge rate idea is that it limits addresses to a low maximum sustained TPS.
[/quote]

We need to consider the possibility that someone will launch a game on NoM and they will need to interact more quickly.  Maybe we decide that happens at the L2 only.  

[quote="vilkris, post:1, topic:233"]
Should PoW expire?
[/quote]
maybe.  what if there is a legit mining purpose for degens to create PoW plasma farms to be rented in the future?  Something to consider.  In fact, can I do that today and store PoW?

-------------------------

vilkris | 2023-11-17 12:46:11 UTC | #10

[quote="0x3639, post:9, topic:233"]
Why 50% and not 75% or some other number less than 100% but greater than 50%? Will a higher percent allow for more block utilization without adjustments?
[/quote]
From [here](https://notes.ethereum.org/@vbuterin/eip-1559-faq#EIP-1559-FAQ):

> **Why limit = target * 2? Why not 4? Or 8?**
It could easily be higher than 2. The higher the limit/target ratio the greater the fee market efficiency benefits of EIP 1559. It depends on how severe the short term spikes are that we are willing to accept; 2x is fairly conservative. We could even launch EIP 1559 with a limit/target of 2 to start off, and increase it over time as we see the network functioning okay even under short-term spikes.

So the reasoning Ethereum used 50% is that the higher the target is, the smaller the fee market efficiency benefits are. I am also assuming they concluded that having 50% of momentum space as a buffer zone to handle short term spikes in demand, is sufficient. Of course we don't have any real data to analyze what the optimal target would be for our network, so 50% is a neutral choice.

[quote="0x3639, post:9, topic:233"]
We need to consider the possibility that someone will launch a game on NoM and they will need to interact more quickly. Maybe we decide that happens at the L2 only.
[/quote]
This is why I think introducing a recharge rate multiplier that is based on the account's total fused plasma amount is needed. You can get a better sustained TPS but you'll need to buy more $QSR. If our network max throughput is around 10TPS, then how much of that TPS should a single entity be able to consume at a sustained rate? Use cases that require high sustained TPS aren't really feasible on our base layer.

[quote="0x3639, post:9, topic:233"]
maybe. what if there is a legit mining purpose for degens to create PoW plasma farms to be rented in the future? Something to consider. In fact, can I do that today and store PoW?
[/quote]
Maybe the PoW expiration shouldn't be too extreme. For example, if it was 24 hours, then it would still allow for some use cases but reduce the effectiveness of a pre-computed PoW attack.

PoW can be pre-computed and stored as a hash, but the PoW is only valid for a specific address, and only for one transaction.

-------------------------

CryptoFish | 2023-11-17 12:47:18 UTC | #11

Amazing work @vilkris. Very well written and thought out process. It even has code samples. I've been following the discussions and still trying to wrap my head around it. Will study your work.

-------------------------

aliencoder | 2023-11-17 20:47:30 UTC | #12

Very nice read @vilkris, I've enjoyed it!

[quote="vilkris, post:1, topic:233"]
# What about burning ZNN to generate plasma
[/quote]

I appreciate bringing into the discussion the hybrid approach I'm proposing.

Also I would like to bring into the discussion the following:

**Goal 4: Storage costs**

If we are targeting a minimal L1, we will need an efficient way to store rollups/data for L2s. Long term storage for blockchains is still an [open research question](https://longhashvc.medium.com/storage-proofs-achieving-state-awareness-across-time-and-chains-0f6e4e898550).

[quote="sol, post:5, topic:233"]
For pre-computed PoW, would the following be feasible?
[/quote]

One of the best strategies to prevent PoW "hoarding" is to make it dependent on memory that is not readily accessible and unpredictable (eg on-chain data). Modern CPU friendly algos like [RandomX](https://github.com/tevador/RandomX/blob/master/doc/design.md) are employing many other different strategies to prevent ASICs from being developed in the first place.

[quote="sol, post:5, topic:233"]
For this solution, I’m concerned about the validation load for nodes.
[/quote]

The whole objective of PoW is to be hard to produce and easy to verify using `CheckPoWNonce`. Nodes must read the on-chain difficulty instead of reading the hardcoded `PoWDifficultyPerPlasma = 1500`.

In order to prevent the pre-computation, I suggest we rely on a weighted average of `MomentumsPerHour` to create a base difficulty for the PoW and a validity timestamp.

```go
func (ab *AccountBlock) ComputeHash() types.Hash {
	return types.NewHash(common.JoinBytes(
		common.Uint64ToBytes(ab.Version),
		common.Uint64ToBytes(ab.ChainIdentifier),
		common.Uint64ToBytes(ab.BlockType),
		ab.PreviousHash.Bytes(),
		common.Uint64ToBytes(ab.Height),
		ab.MomentumAcknowledged.Bytes(),
		ab.Address.Bytes(),
		ab.ToAddress.Bytes(),
		common.BigIntToBytes(ab.Amount),
		ab.TokenStandard.Bytes(),
		ab.FromBlockHash.Bytes(),
		ab.DescendantBlocksHash().Bytes(),
		types.NewHash(ab.Data).Bytes(),
		common.Uint64ToBytes(ab.FusedPlasma),
		common.Uint64ToBytes(ab.Difficulty),
		ab.Nonce.Data[:],
	))
```

More specifically, we can use the `TimestampUnix` of the `MomentumAcknowledged` and check if `TimestampUnix + 3600 > currentTimestamp`.

I've also proposed rotating between 3 distinct PoW algos: `SHA-3`, `RandomX` and `Equix` depending on an external piece of information (eg hash of momentum `frontierMomentum - 31`).

```go
// SHA-3 = 0, RandomX = 1, Equix = 2
hash := "0000009f4b552.."
hashInt := new(big.Int)
 _, ok := hashInt.SetString(hash, 16)
if !ok {
        log.Fatalf("Invalid hash: %s", hash)
}

algo := getAlgo(hashInt)
fmt.Printf("Hash %s corresponds to %d\n", hash, algo)

func getAlgo(hashInt *big.Int) int {
    const numAlgos = 3
    maxVal := new(big.Int)
    maxVal.Exp(big.NewInt(2), big.NewInt(256), nil)
    algoSize := new(big.Int).Div(maxVal, big.NewInt(numAlgos))
    algo := new(big.Int).Div(hashInt, algoSize).Int64()
    return int(algo)
}
```
This program will categorize any given hash into 3 buckets (0, 1 and 2, corresponding to `SHA-3`, `RandomX` and `Equix`) based on its integer value. The categorization is consistent for any hash such that the same hash will fall into the same "bucket". Due to the nature of cryptographic hashes, this distribution should be fairly even, assuming the hashes are uniformly distributed (a fundamental property of cryptographic hash functions).

Nodes already have this information and they need to `switch` between the appropriate `CheckPoWNonce`. Clients also have access to this info in order to compute the proof of work.

-------------------------

vilkris | 2023-11-19 19:14:49 UTC | #13

[quote="aliencoder, post:12, topic:233"]
I appreciate bringing into the discussion the hybrid approach I’m proposing.
[/quote]
I think the hybrid approach you talked about has reasonable arguments in favor of it and that's why I wanted to leave the door open for that possibility. But I think burning ZNN also introduces potential problems that we will really need to think through. I'm also trying to limit the scope of the initial dynamic plasma implementation so that we don't introduce too many new concepts and changes.

[quote="aliencoder, post:12, topic:233"]
**Goal 4: Storage costs**

If we are targeting a minimal L1, we will need an efficient way to store rollups/data for L2s. Long term storage for blockchains is still an [open research question ](https://longhashvc.medium.com/storage-proofs-achieving-state-awareness-across-time-and-chains-0f6e4e898550).
[/quote]
Could you elaborate a bit more how this goal ties into dynamic plasma, and is this goal something that should be solved with plasma?

As you probably know, additional tx data has a cost of 68 plasma/byte currently. Ethereum lowered their data cost from 68 gas/byte to 16 gas/byte, to better support the use case you mentioned: [EIP-2028](https://eips.ethereum.org/EIPS/eip-2028). Of course just lowering the cost doesn't exactly contribute to the goal of a minimal L1.

[quote="aliencoder, post:12, topic:233"]
I suggest we rely on a weighted average of `MomentumsPerHour` to create a base difficulty for the PoW and a validity timestamp.
[/quote]
I'm not sure I understand what this means. Does this differ from the ideas presented in my earlier posts?

[quote="aliencoder, post:12, topic:233"]
I’ve also proposed rotating between 3 distinct PoW algos: `SHA-3`, `RandomX` and `Equix` depending on an external piece of information (eg hash of momentum `frontierMomentum - 31`).
[/quote]
If RandomX is one of the algorithms, then an attacker will need general purpose CPUs to do a PoW attack. I'd imagine the performance gain is roughly the same for all the algorithms when using a general purpose CPU. So how does adding more algorithms increase the attack cost, since there isn't really a need for the attacker to have different hardware for the different algorithms?

-------------------------

aliencoder | 2023-11-19 20:27:07 UTC | #14

[quote="vilkris, post:13, topic:233"]
I’m also trying to limit the scope of the initial dynamic plasma implementation so that we don’t introduce too many new concepts and changes.
[/quote]

If we start implementing a solution, it should be the best solution we can come up with.

[quote="vilkris, post:13, topic:233"]
As you probably know, additional tx data has a cost of 68 plasma/byte currently.
[/quote]

We can stick with it for the moment.

[quote="vilkris, post:13, topic:233"]
Does this differ from the ideas presented in my earlier posts?
[/quote]

We can introduce a validity timestamp such that plasma generated via PoW will expire if not used.

[quote="vilkris, post:13, topic:233"]
So how does adding more algorithms increase the attack cost, since there isn’t really a need for the attacker to have different hardware for the different algorithms?
[/quote]

The idea is to make the attack prohibitively expensive for an attacker. You can rent hash power from Nicehash or similar platforms. If we only use [RandomX](https://www.nicehash.com/algorithm/randomxmonero#), we are exposed. 

[quote="vilkris, post:13, topic:233"]
the performance gain is roughly the same for all the algorithms when using a general purpose CPU
[/quote]

Exactly: rotating between multiple PoW algos decreases the attack surface and it doesn't impact the end users at all.

-------------------------

vilkris | 2023-11-19 21:10:46 UTC | #15

[quote="aliencoder, post:14, topic:233"]
The idea is to make the attack prohibitively expensive for an attacker. You can rent hash power from Nicehash or similar platforms. If we only use [RandomX](https://www.nicehash.com/algorithm/randomxmonero#), we are exposed.
[/quote]
This is why every project should use their own configuration to mitigate this attack, as stated in the RandomX [docs](https://github.com/tevador/RandomX/blob/master/doc/configuration.md#randomx-configuration):
>We recommend each project using RandomX to select a unique configuration to prevent network attacks from hashpower rental services.

Rental services are renting the Monero RandomX variant, which would be useless for our network.

The incentives to rent out PoW in our network are completely different from Monero.

-------------------------

aliencoder | 2023-11-20 07:58:05 UTC | #16

[quote="vilkris, post:15, topic:233"]
Rental services are renting the Monero RandomX variant, which would be useless for our network.

The incentives to rent out PoW in our network are completely different from Monero.
[/quote]

I agree. Just highlighting that even RandomX is Nicehashable :slight_smile: 

Another argument behind rotating multiple PoW algos is that we already have a working SHA-3 implementation that is ASIC friendly and it works well enough. 

The only con is that clients will need to support 3 different PoW implementations which will add up some complexity. 

But yet again some PoW algos are simpler than others to implement and support. I still think the best idea to move forward is to keep SHA-3 and add RandomX and another one that is simple to implement.

-------------------------

vilkris | 2023-11-20 10:24:56 UTC | #17

[quote="aliencoder, post:16, topic:233"]
Just highlighting that even RandomX is Nicehashable
[/quote]

Sure, but so is a PoW algorithm that consists of multiple hash functions, like x11 or x13. If a market were to form for PoW on our network, the sellers would just sell hashpower that computes the triple hash PoW algorithm using a general purpose CPU.

-------------------------

aliencoder | 2023-11-20 23:04:13 UTC | #18

[quote="vilkris, post:17, topic:233"]
the sellers would just sell hashpower that computes the triple hash PoW algorithm using a general purpose CPU
[/quote]

The PoW algos aren't chained together, they're independent.

I'm thinking of creating a decentralized Bitcoin mining pool and implementing SHA-256 to merge-mine Bitcoin while computing the PoW.

Food for thought: 
1. [P2Pool](https://en.bitcoin.it/wiki/P2Pool)
2. [Pros and cons](https://bitcoin.stackexchange.com/questions/20219/what-are-the-pros-and-cons-of-p2p-mining-pools)
3. [Mining decentralization](https://bitcoinmagazine.com/technical/p2pool-bitcoin-mining-decentralization)
4. [P2P Braidpool](https://github.com/braidpool/braidpool) and [specs](https://blog.opdup.com/specification.html)

-------------------------

vilkris | 2023-12-11 15:18:19 UTC | #19

I've spent some more time thinking about the practical feasibility of the ideas presented in the starting post and I've also considered some of the questions that were raised in this thread.

The formulas related to the dynamic plasma ideas are presented [here](https://github.com/vilkris4/dynamic-plasma-ideas/blob/main/dynamic_plasma_formulas.md). I hope this format makes it easier to understand the underlying principles. I'll be using the terminology introduced in that document.

## Plasma recharge rate over N account blocks
In order to prevent the situation where an account can claim a more optimal recharge rate by submitting a new account block when the network decongests, I've modified the recharge rate algorithm slightly from the initial version.

The modified idea is that a confirmation target is calculated once an account block is included in a momentum. The confirmation target is the amount of confirmations the frontier account block needs in order to recharge all of the account's confined plasma.

Confined plasma is the plasma that is "locked" in account blocks and it has to get recharged before it can be used again.

Example:
|Momentum Height|Block Height|Block Fused Plasma|Confined Plasma|Recharge Rate (plasma/confirmation)|Confirmation Target|
|---|---|---|---|---|---|
|1|1|21000|21000|21|1000
|...|
|100|2|21000|39900|2100|900+10=910
|...|
|1010|3|21000|21000|2100|10

In the second account block, we can see that 100 confirmations have elapsed since the first block was included in a momentum. These confirmations are subtracted from the new confirmation target and the second account block's confirmation target is added to the new confirmation target. This ensures that the user has to wait for all of the confirmation targets from previous account blocks to be surpassed in order to recharge all of the plasma.

This also means that every account has its own per confirmation recharge rate that depends on three things:
1. What the network's base recharge rate was when an account block was included in a momentum.

2. What the previous account block's confirmation target and confined plasma amount was.

3. How much total fused plasma the account has.

## Sustained TPS of an account
In order to allow accounts to have a higher sustained TPS than what the network's base recharge rate would allow, we could use a recharge rate multiplier that depends on the total fused plasma of an account. The more fused plasma an account has, the bigger the recharge rate multiplier.

Example:
|Account|QSR Fused as Plasma|Current Base Recharge Rate|Multiplier|Account Recharge Rate|
|---|---|---|---|---|
|1|50|2100|0.5x|1050
|2|100|2100|1x|2100
|3|8000|2100|80x|168000

From this we can calculate that for an address with 10,000 QSR fused as plasma, the sustained TPS for the account would be 1 TPS, when the base recharge rate is 2,100 (meaning that the momentum is exactly half full). If momentum space demand increases they will not be able to sustain that TPS unless they fuse more plasma, but if our total network max TPS is only 10-20 TPS, then I think these are reasonable numbers. For comparison, it would be very expensive for a user to sustain 1 TPS on other networks such as Bitcoin and Ethereum, which have similar throughput capabilities as our network.

From the example above we can also calculate that the absolute maximum amount of confirmations an address needs to recharge all of its fused plasma is 10,000 confirmations (=27.78 hours), regardless of how much fused plasma the account has. This should be acceptable from a UX point of view.

### Transactions per period
I initially thought we would need a transactions-per-address-per-period cap, but I don't think this is needed anymore, since the recharge rate will effectively rate control an account in a similar manner.

## Implementation complexity introduced by the dynamic plasma recharge rate
After looking at how to actually implement the dynamic recharge rate, I've come to the conclusion that it would need two new database indexes: one for the confirmation target and one for the confined plasma amount.

These values are computed and stored when the transaction gets included in a momentum. The values are stored in the momentum store. The computations are simple and should have a negligible effect overall. The database has to be read 4 times and written to 2 times. For reference, currently when an account block is stored into the momentum store, it takes 5-7 reads and 3-4 writes (depending on the transaction's type).

When querying an account's available fused plasma, it requires 8 database reads. In the current implementation this operation requires 3 database reads.

Looking at some (old) [benchmarks](https://github.com/google/leveldb#performance) for LevelDB, it does not seem like the plasma recharge rate would be a bottleneck, even with a significantly higher amount of network throughput.

I'm open to suggestions if someone has a better understanding or ideas for how to determine "how much additional complexity is too much".

## RBF
I think the already existing RBF implementation is good enough. A transaction that is in the mempool can be replaced by committing a greater amount of plasma to it. We will need to think about client support for this once network utilization starts picking up.

## Full vs. half-full momentums
In the initial post I presented the idea for using half-full momentums, mainly as a way to improve end-user UX by making the estimation of transaction plasma requirements easier. I think most of the reasoning Ethereum has stated for using half-full blocks applies to our network as well.

If we were to use full blocks (like on Bitcoin for example), this would mean that we would not have an algorithmically adjusted base price for plasma (as presented in the first post), but transactions would be included in momentums purely based on the plasma price used for the transaction and the estimation for what is a sufficient plasma price for a transaction would have to be done off chain, leading to additional complexity in clients.

Using full momentums would also mean that the base recharge rate for fused plasma would have to be calculated in a different way. For example, the base recharge rate could still be based on how full the previous momentum was. But this might lead to very slow overall recharge rates once momentum space is in high demand and when most, if not all, momentums are full.

-------------------------

Chadass | 2023-12-11 19:56:01 UTC | #20

I second this. I always prefer data driven decisions over ideology.

-------------------------

Nostromo | 2023-12-12 02:51:39 UTC | #21

Bravo, sir! Your presentation is incredibly thorough, meticulously thought through, and well-presented, particularly the pseudo code on Git. I'm still digesting everything and learning myself, so please forgive my ignorance. I am a bit perplexed by the assumption that the recharge rate and sustained TPS of an account are based on the precedent that the network is only operating at 10-20 TPS.

I don't understand why it should continue to be so low. If we employ a block lattice structure like Nano, is it not reasonable to assume that we should be able to achieve a similar throughput? Nano, for instance, claims up to 7000 TPS.

Every single indicator points towards the network being designed for high throughput. While I find your idea for multipliers based on previous momentums and recharge cooldowns truly awesome (I love the pseudo code and equations you posted), I wonder if you could consider a scenario where the network is unthrottled?

In this scenario, let's take the requirements section from the Zenon GitHub wiki and mandate nodes to have:

* CPU: At least 4 cores
* RAM: At least 4 GB
* Storage: At least 40 GB of free space
* Network: More than 100 Mbps of dedicated bandwidth

-------------------------

coinselor | 2023-12-12 16:18:29 UTC | #22


Keeping up with the nano similarities, I've been researching their system to find any insights we could apply.

Interestingly, we both utilize a minimal "Proof of Work" (PoW) and incorporate the concept of "lanes." In their framework, these lanes are divided into various buckets based on transaction sizes. They also take into account the age of accounts, discouraging attackers from utilizing multiple new accounts.

While I'm not fully versed in the technical specifics of their approach, I believe Vilkris' suggestion for a plasma recharge rate, leveraging our plasma fee abstraction, presents a more refined strategy than their complex bucket divisions.

There's potential to learn from their method of distinguishing between "regular" and "spammy" transactions.

Below are some resources that could be informative:

[Buckets](https://docs.nano.org/protocol-design/spam-work-and-prioritization/#)

[Dynamic PoW](https://blog.nano.org/dynamic-proof-of-work-prioritization-4618b78c5be9)

[Post Update Stress Test Results](https://www.reddit.com/user/Qwahzi/comments/1318nse/nano_stress_tests_measuring_bps_cps_tps_in_the/)

-------------------------

vilkris | 2023-12-12 19:43:56 UTC | #23

[quote="Nostromo, post:21, topic:233"]
I am a bit perplexed by the assumption that the recharge rate and sustained TPS of an account are based on the precedent that the network is only operating at 10-20 TPS.
[/quote]
Increasing network throughput has been out of the scope of the ideas I've presented.

The throughput of the network isn't really relevant to the underlying mechanisms behind the proposed ideas. If we can increase network throughput then the recharge rates and sustained TPS could be increased as well. The constants used in the algorithms can always be reconsidered with future protocol advancements.

At 7000 TPS the recharge rates would be significantly faster.

We don't really have any benchmarks to help us make an educated guess on what kind of throughput the network can sustain with the current implementation. I think we would need to start with that if we want to consider increasing network throughput, but increasing network throughput without actual end user demand for that throughput isn't that high of a priority in my opinion.

[quote="coinselor, post:22, topic:233"]
Keeping up with the nano similarities, I’ve been researching their system to find any insights we could apply.
[/quote]
I also did some research on Nano a while ago. They have some similarities and their bucket approach probably has more or less the same end result as the recharge rate.

-------------------------

Nostromo | 2023-12-13 01:05:10 UTC | #24

In my understanding, the reason for the transaction cap was because there was no dynamic plasma. I thought DP was meant to allow scaling while adding protection?

If you implement DP and keep the transaction cap, then what's the point of DP? The network functions fine now with the transaction cap in place.

I understand that you can change the values; I just thought it could have advantages to design it with the intention of scaling in mind. That changes the calculus of the recharge rate, the cost of plasma, the rate of plasma to permissible transactions, and so on. Additionally the cap could be removed with DP implementation.

For arguments' sake, if the network capacity is 5000 tps but we implement it for 10 tps, you are making it 500x more expensive for users to use plasma and wait for recharges. And maybe more importantly, you are going to make the POW very expensive too.

Why would a user buy lots of QSR to fuse into plasma and deal with long recharge times when they could just pay fractions of a cent for a transaction on another chain?

Furthermore, I disagree that we should only concern ourselves with transaction throughput once there is demand. In simplified terms, there are two main ways users become aware and use a network: marketing and use cases.

In a competitive market where tps is one of the main metrics, I think it goes without saying that a next-gen blockchain with 10 tps is a bit of a troll.

And in terms of use cases, having 500x more expensive plasma is not appealing to anybody wanting to transact more than once every few minutes.

Besides, being on the backfoot to correct something once or if demand sets in is always a much worse option than accommodating for it beforehand, if at all possible.

Maybe that involves benchmarking nodes and/or developing DP that can adjust to a variable transaction processing capacity of the network.

To me, the idea of the zero-transaction-fee paradigm is to allow users to transact freely and cheaply while managing adequate network protection and equal access.

-------------------------

Nostromo | 2023-12-13 01:39:47 UTC | #25

I apologize if I sound argumentative.
I just want to reiterate that the mechanics you have presented are really impressive and awesome.

-------------------------

Chadass | 2023-12-13 02:54:09 UTC | #26

Aside of the technical side, an uncapped network gives the marketing team more selling points, and it'll be easier to onboard projects. Saying we might one day have more than 10 tps isn't the same as saying that right now they can build with 20k tps in mind.

-------------------------

vilkris | 2023-12-13 15:08:15 UTC | #27

[quote="Nostromo, post:24, topic:233"]
If you implement DP and keep the transaction cap, then what’s the point of DP? The network functions fine now with the transaction cap in place.
[/quote]
This is the first thing I explained in the initial post. My definition of dynamic plasma doesn't include increasing network throughput, it's about the goals that I stated: network gas, tx prioritization and anti-spam. These are needed regardless of what our network throughput is.

Higher TPS would result in lower plasma requirements, but to achieve high throughput we need to lay a foundation for it. We need improvements to IBD, we need pruned nodes, and we have to consider what kind of hardware/storage/bandwidth requirements we want to target, since in general higher TPS is a centralizing force and storage requirements can increase fast.

[quote="Nostromo, post:24, topic:233"]
I understand that you can change the values; I just thought it could have advantages to design it with the intention of scaling in mind. That changes the calculus of the recharge rate, the cost of plasma, the rate of plasma to permissible transactions, and so on. Additionally the cap could be removed with DP implementation.
[/quote]
What issues do you see with the ideas I've presented, with regard to scaling?

[quote="Nostromo, post:24, topic:233"]
And in terms of use cases, having 500x more expensive plasma is not appealing to anybody wanting to transact more than once every few minutes.
[/quote]
At the current network utilization rate, the plasma requirements/PoW requirements would stay roughly the same and the recharge rates would be fast. Ideally we will be able to increase network throughput alongside the adoption of our network.

[quote="Nostromo, post:24, topic:233"]
Besides, being on the backfoot to correct something once or if demand sets in is always a much worse option than accommodating for it beforehand, if at all possible.
[/quote]
I don't think anyone disagrees. We have limited dev resources though, so we need to prioritize and take things one step at a time.

-------------------------

Nostromo | 2023-12-15 02:21:51 UTC | #28

[quote="vilkris, post:27, topic:233"]
What issues do you see with the ideas I’ve presented, with regard to scaling?
[/quote]

I'm currently quite pressed for time, so this post will be brief.

I had a chance to look at the formulas for Dynamic Plasma, particularly focusing on the Plasma Base Price Formula.

I believe the issue is that, for scaling, the Plasma table needs to be removed, and the definition of plasma needs to correlate with network resources. Having a plasma table with relational constants is very inflexible.

We should define plasma, for instance, like satoshi/vbyte for storage and wei/computation. This way, we can determine the real cost of a transaction and represent it in plasma. Then, you might be able to simplify the formulas a bit. I haven't given it as much thought as you, so perhaps the formula works as is with a plasma/byte-esque definition.

I wonder about the "c" value: the base price change denominator. How is this one determined?

[quote="vilkris, post:27, topic:233"]
we have to consider what kind of hardware/storage/bandwidth requirements we want to target
[/quote]

Regarding having a plasma ceiling per momentum (I assume that is what your plasma target of momentum is for?) and nodes, my vote would be with the recommended requirements the developers of Alphanet outlined in the official wiki. We could define a plasma ceiling from there.

I am against the notion that a node should be able to run on a potato. This philosophy makes sense for a low tp network like Bitcoin that aims for decentralization of nodes.
High transactional decentralized networks, by their nature, have a computational cost. For a similar comparison, look at Nano and their distribution of nodes, comparing their recommended specs to ours.
The sentry(trusted) - Sentinel(trustless) paradigm makes our nodes much better than Nanos'.  

You seem to have a good understanding of storage costs, database reads, and all that jazz. It would be awesome if you could define a plasma/byte equivalent, and we could move away from a plasma table.

-------------------------

vilkris | 2023-12-15 16:13:14 UTC | #29

First off, thanks for taking the time to look at the formulas. I appreciate it.

[quote="Nostromo, post:28, topic:233"]
I believe the issue is that, for scaling, the Plasma table needs to be removed, and the definition of plasma needs to correlate with network resources. Having a plasma table with relational constants is very inflexible.
[/quote]
I'm not sure I understand what you mean with "plasma needs to correlate with network resources", since I think that's what it does already. As I explained in the initial post, one purpose of plasma is to represent computational resources, and that's essentially the purpose of the plasma table. The values in the table represent the computational cost of the operation in question. The required amount of computational resources for a given operation should always be the same, so I don't see why the values can't be constants.

We only have embedded smart contracts on our base layer, meaning that we should be able to define the plasma requirements as known values. In Ethereum for example, the gas requirements for smart contract operations are calculated based on [conversion rates of low-level-computer-operations-to-gas](https://docs.google.com/spreadsheets/d/1m89CVujrQe5LAFJ8-YAUCcNK950dUzMQPMJBxRtGCqs/edit#gid=0).

Both use hard coded "tables" but ours is highly simplified compared to Ethereum.

The Plasma Base Price formula is essentially the same algorithm that Ethereum uses for the same purpose ([EIP-1559](https://notes.ethereum.org/@vbuterin/eip-1559-faq#EIP-1559-FAQ)).

[quote="Nostromo, post:28, topic:233"]
We should define plasma, for instance, like satoshi/vbyte for storage and wei/computation. This way, we can determine the real cost of a transaction and represent it in plasma. Then, you might be able to simplify the formulas a bit. I haven’t given it as much thought as you, so perhaps the formula works as is with a plasma/byte-esque definition.
[/quote]
The plasma/resource conversions in our codebase mimic those of Ethereum. For extra data in account blocks we have the following definition: `ABByteDataPlasma = 68`, which means that every extra byte in an account block costs 68 plasma. The account block base plasma, which is 21,000 plasma, already covers the data/storage cost of a vanilla account block that has no extra data, which is again [similar to Ethereum](https://ethereum-magicians.org/t/some-medium-term-dust-cleanup-ideas/6287/1#why-do-txs-cost-21000-gas-1).

So based on this I think the requirement to represent the real cost of a transaction in plasma, is already fulfilled in that sense.

[quote="Nostromo, post:28, topic:233"]
I wonder about the “c” value: the base price change denominator. How is this one determined?
[/quote]
When targeting half full momentums and when `c=8`, the maximum base price change between momentums can be +/-12.5%. The bigger the `c` value is, the smaller the maximum change can be between momentums. The reason I chose 8 is because that is what Ethereum uses and apparently it has worked well for them. Again, the Base Price formula is basically the same as Ethereum's.

Also, based on the simulations I've done, it appears to provide a decent balance between spam mitigation and UX.

[quote="Nostromo, post:28, topic:233"]
Regarding having a plasma ceiling per momentum (I assume that is what your plasma target of momentum is for?) and nodes, my vote would be with the recommended requirements the developers of Alphanet outlined in the official wiki. We could define a plasma ceiling from there.
[/quote]
Yes, the per momentum base plasma cap is a hard ceiling. Those recommended requirements are not enough to run a public node currently. To run a public node smoothly you need at least 32GB of RAM and more than 4 cores on a dedicated server. Like I said in my previous post, we have issues with the node and our current bottleneck appears to be the P2P layer. In a local network the recommended requirements should be more than enough though.

These node issues are obviously something we need to sort out before we can start considering any significant increase in throughput limits.

The throughput limits can be increased later on, and this is why I previously said that in my opinion increasing throughput isn't necessarily a high priority right now, taking into account that there is no demand for it. That doesn't mean that the design decisions we make now shouldn't carefully take into account how they affect performance and scalability.

-------------------------

Nostromo | 2023-12-19 04:23:50 UTC | #30

That explains a lot; thank you for the detailed response. I also read the post about plasma and the plasma table on the other forum, which has helped me understand it much better.

The plasma table is used to query plasma utilized by a transaction, so it's definitely necessary ( ...I'm a dope 😆).

When looking at `go-zenon/vm/const/plasma.go`, I can see the definition of the Plasma table. Interestingly, there is a distinction made for `AlphanetPlasmaTable`.

So, we have three types of transactions:

* `EmbeddedSimple`
* `EmbeddedWithdraw`
* `EmbeddedDoubleWithdraw`

The plasma cost of an `EmbeddedSimple` is calculated as:


```
EmbeddedSimplePlasma = 2.5 * AccountBlockBasePlasma
```

Essentially, each embedded type has its own multiplier to `AccountBlockBasePlasma`: 2.5, 3.5, and 4.5. I would assume that these multipliers need to become dynamic for Dynamic Plasma?

Furthermore, we not only have a definition for `TxPlasma` and `TxDataPlasma` but also how these values relate to fusion units of an account.

`MaxFusionUnitsPerAccount` limits each account to a maximum of 5000 fusion units.

```
PlasmaPerFusionUnit = 2100
MaxFusionPlasmaForAccount = 5000 * 2100 = 10,500,000
```

So, I guess currently a max fused account could fire off an embeddedSimple 200 times at the cost of 52,500 per pop.

I'm not quite clear on the `MaxFussedAmountforAccount` variable. Firstly, there is a typo; it should be `MaxFused` to remain consistent with naming. Apart from that, it's a huge number. I assume it could just be the theoretical limit.

Am I correct in my understanding? I think being able to fire off 200 transactions is quite hectic, and it's no wonder we needed the transaction cap for now.
However, if we could make the multipliers dynamic, that would reduce the number of sustained transactions somebody could perform.

-------------------------

Nostromo | 2023-12-19 07:53:12 UTC | #31

For transactions to non-embedded addresses, the `ABByteDataPlasma` value could be made dynamic with a multiplier.

-------------------------

vilkris | 2023-12-20 09:30:08 UTC | #32

[quote="Nostromo, post:30, topic:233"]
Essentially, each embedded type has its own multiplier to `AccountBlockBasePlasma`: 2.5, 3.5, and 4.5. I would assume that these multipliers need to become dynamic for Dynamic Plasma?
[/quote]
Again, the plasma table only represents the computational requirements of an operation, which stay the same regardless of network utilization. These multipliers appear to be ball park estimates to represent the computational requirements, not fine-grained estimates, like in Ethereum. But I think ball park estimates are fine for us, at least now.

The `BasePrice` variable I've presented introduces a dynamic price on the computational resources based on demand, and essentially does what you're suggesting.

[quote="Nostromo, post:30, topic:233"]
So, I guess currently a max fused account could fire off an embeddedSimple 200 times at the cost of 52,500 per pop.

I’m not quite clear on the `MaxFussedAmountforAccount` variable. Firstly, there is a typo; it should be `MaxFused` to remain consistent with naming. Apart from that, it’s a huge number. I assume it could just be the theoretical limit.
[/quote]
Since the rate control mechanisms of the current plasma implementation are minimal, I think the founding devs wanted to have some kind of hard cap, that limits the amount of transactions an account can send. But as you can see, the rate at which an account can fire transactions leaves the network open to spam attacks, which is why dynamic plasma is a high priority in my opinion.

[quote="Nostromo, post:30, topic:233"]
Am I correct in my understanding? I think being able to fire off 200 transactions is quite hectic, and it’s no wonder we needed the transaction cap for now.
However, if we could make the multipliers dynamic, that would reduce the number of sustained transactions somebody could perform.
[/quote]
Yes and that's exactly what the ideas I've presented are trying to achieve. The plasma recharge rates effectively throttle the number of sustained transactions somebody can send.

-------------------------

Nostromo | 2023-12-20 12:12:52 UTC | #33

Plasma recharge rates are an interesting topic that delves into the roots of why QSR exists. I've been thinking about QSR quite a bit lately, especially in light of the Gravity wallet. I've also been pondering dynamic plasma implementation, aliencoders' fee proposal, and other related matters.

I've come to the conclusion that one of the main utilities of QSR is tokenized throughput. Obvious, right? We all know that... Yes, but do we really understand it?
Owning QSR is equal to owning a percentage of network throughput. It's a novel and brilliant concept, perhaps making one need to rethink how spam should be defined within that context.

Say, for instance, somebody owns 1% of the QSR supply, this makes them eligible for 1% of the throughput. If that person decides to use their position and 'spam' the network with transactions, could that actually benefit the network?

With dynamic Plasma, it will make the plasma cost per transaction more expensive for everybody. That means more fused QSR and more QSR bought, causing deflationary pressures and price rises.

Now, consider the price, especially once demand really kicks in. The 1% network 'spammer' now sees the value of QSR holdings rise, and they sell some... can you see what's happening here? A decentralization of holdings and throughput over time.

In my opinion, recharges may not be needed. Despite thinking along the same lines as you and wanting to take advantage of the accounts-based system, I believe in this instance it would involve unnecessary computation. A global dynamic plasma is far more conducive to the system.

I think we should take tokenized throughput quite literally and with that be transaction agnostic as well, and realize that network utilization is designed to drive decentralization.

-------------------------

Nostromo | 2023-12-20 12:08:17 UTC | #34

[quote="vilkris, post:32, topic:233"]
These multipliers appear to be ball park estimates to represent the computational requirements, not fine-grained estimates, like in Ethereum. But I think ball park estimates are fine for us, at least now.
[/quote]

Yes, I think making these multipliers dynamic instead of hardcoded would be efficient. Basically saying the more transactions that occurred in the last momentum, the higher this multiplier goes. 
Making the cost to transact progressively more expensive and inexpensive in correlation to the amount of transactions processed.

-------------------------

0x3639 | 2023-12-20 18:16:38 UTC | #35

[quote="Nostromo, post:33, topic:233"]
aliencoders’ fee proposal,
[/quote]

do you have an opinion on @aliencoder fee proposal?

-------------------------

vilkris | 2023-12-20 18:35:23 UTC | #36

[quote="Nostromo, post:33, topic:233"]
Now, consider the price, especially once demand really kicks in. The 1% network ‘spammer’ now sees the value of QSR holdings rise, and they sell some… can you see what’s happening here? A decentralization of holdings and throughput over time.
[/quote]
What if they don't sell because their intention is to attack the network? They can indefinitely keep the cost of transactions so high, that almost no one will be able to use the network. A short selling attack could be profitable for example.

-------------------------

aliencoder | 2023-12-20 19:04:36 UTC | #37

I've also proposed a burn mechanism when you unfuse the QSR.

-------------------------

0x3639 | 2023-12-20 22:21:00 UTC | #38

[quote="vilkris, post:36, topic:233"]
What if they don’t sell because their intention is to attack the network?
[/quote]

This question comes up with Bitcoin too.  What if a state actor attacks bitcoin PoW for non-economic reasons?  This is a good question and I think one "answer" is, yes that is possible, but they have not done it yet.  Try it and let's see what happens.

@Nostromo raises an interesting question about the purpose of $qsr.  Does $qsr represent ownership of network throughput?  If so, I think the recharge rate diminishes the value of $qsr is some way. With "recharge" applied, the value of $qsr is derived from the ability to process one TX fast.  We are sort of "socializing" the value of $qsr in order to prevent spam.  Not sure if that is a correct analogy.  

I think we should explore what happens if we don't impose the recharge rate as a thought experiment.  I guess it's as simple as the amount of plasma needed to process a TX goes up.  Is that a bad thing for the value of $qsr?

My guess is a few OGs have 1 to 3 million $qsr.  That is a total guess. But from what we can tell, they are honest actors.  It will be hard for a "bad actor" to get enough $qsr to attack the network.  But... never say never.  

I think a more likely scenario is someone gets enough $qsr to manipulate the value of $znn or $qsr.  We are too small for a non-economic actor to care (right now).  And if someone is trying to manipulate the value, as @Nostromo points out, it will result in the redistribution of $qsr eventually.  Is that a bad thing?

-------------------------

Nostromo | 2023-12-21 04:30:07 UTC | #39

[quote="vilkris, post:36, topic:233"]
they can indefinitely keep the cost of transactions so high, that almost no one will be able to use the network
[/quote]

 I don't think they can; you would need to own a very large percentage of QSR to do this and you would need to overcome the daily inflation and actively buy and hoard the circulating supply. Maybe at launch of AlphaNet there may have been risk of this and one could speculate that this was the reason it did not launch with dynamic plasma.

[quote="vilkris, post:36, topic:233"]
What if they don’t sell because their intention is to attack the network? 
[/quote]

It could be that in the future there is an application that uses, for argument's sake, 3% of the network throughput, continuously making transactions. Would you consider that an attack on the network? I would say that is network utilization, and from the point of view of the network dynamics, there is no difference between an application using 3% of the network or a QSR whale with bots making dummy transactions using 3% of the network.

[quote="0x3639, post:35, topic:233"]
do you have an opinion on @aliencoder fee proposal?
[/quote]

I think it's superfluous and would break network dynamics to some extent. Sometimes things that are very well designed look too simple, and one may feel tempted to add complexity. Chess is such a good game because of well-balanced simple rules.

[quote="aliencoder, post:37, topic:233, full:true"]
I’ve also proposed a burn mechanism when you unfuse the QSR.
[/quote]

Sorry, I am against this too. Being able to choose beneficiary addresses to fuse plasma is a simple but powerful feature. A forced burn would make this problematic. I think that QSR is already very deflationary.

-------------------------

vilkris | 2023-12-21 11:32:25 UTC | #40

[quote="Nostromo, post:39, topic:233"]
I don’t think they can; you would need to own a very large percentage of QSR to do this and you would need to overcome the daily inflation and actively buy and hoard the circulating supply.
[/quote]
Do you have some example calculations? With the current implementation you only need 1,000 QSR to fill up every single momentum indefinitely. If transactions are prioritized by plasma, you need 100,000 QSR to fill up every single momentum with 1,000 QSR/tx, so that anyone with less than 1,000 QSR will be blocked from sending vanilla transactions, unless they spend a significant time generating PoW, which isn't really an option for mobile/browser wallets. To collect delegation rewards a user would need 3,500 QSR in this situation. What good is daily inflation when you can't use the network anyway?

It should be assumed that accumulating hundreds of thousands of QSR is feasible, or otherwise we won't have new pillars.

If the argument is that we attempt to raise the throughput to 1,000 TPS or something similar, then that means that with 100,000 QSR you can bloat the node database at 200,000 B/s indefinitely, if a tx is 200 B. This means 16 GB per day and would have a toll on node decentralization and users would basically have to rely on centralized node provider services, assuming node providers find a way to monetize their services. That money has to come from somewhere, most likely the users.

[quote="Nostromo, post:39, topic:233"]
It could be that in the future there is an application that uses, for argument’s sake, 3% of the network throughput, continuously making transactions. Would you consider that an attack on the network? I would say that is network utilization, and from the point of view of the network dynamics, there is no difference between an application using 3% of the network or a QSR whale with bots making dummy transactions using 3% of the network.
[/quote]
Please define what you mean with 3% of network throughput. Throughput per momentum, per time window?

I defined what I mean by spam in the initial post. You're right that the network doesn't understand what spam is:
[quote="vilkris, post:1, topic:233"]
To me, on-chain spam can be defined as any activity that floods the chain with transactions with the intention to significantly limit the ability of others to use the network. There can be many reasons for conducting a spam attack - for financial gain, for example.
[/quote]
[quote="0x3639, post:38, topic:233"]
My guess is a few OGs have 1 to 3 million $qsr. That is a total guess. But from what we can tell, they are honest actors. It will be hard for a “bad actor” to get enough $qsr to attack the network. But… never say never.
[/quote]
Sure, but trying to guess what motives people may have now or in the future is not really in line with the crypto ethos. There are countless addresses that that have +100k QSR. You can't prove they all belong, and always will belong, to good actors.

Every blockchain that is worth anything has been attacked by irrational actors and by people "proving a point". On our network the consequences of a serious spam attack could be detrimental without proper mitigations.

[quote="0x3639, post:38, topic:233"]
@Nostromo raises an interesting question about the purpose of $qsr. Does $qsr represent ownership of network throughput? If so, I think the recharge rate diminishes the value of $qsr is some way. With “recharge” applied, the value of $qsr is derived from the ability to process one TX fast. We are sort of “socializing” the value of $qsr in order to prevent spam. Not sure if that is a correct analogy.
[/quote]
To be precise, QSR doesn't represent throughput, plasma does. And plasma represents ownership of throughput even with the recharge rates. The rules are the same for everyone. What it does is it rate controls how fast an account can send transactions within a time window. If there is no recharge time, then the time window becomes one momentum, and it will become impossible for people with 100 QSR fused on their account to claim their miniscule share of the bandwidth, if network utilization and plasma usage is maxed out.

@Nostromo Don't get me wrong, I'm all for a simpler solution that doesn't need any additional rate controlling measures, but I haven't seen the numbers that would allow for this.

-------------------------

0x3639 | 2023-12-21 11:58:41 UTC | #41

[quote="vilkris, post:40, topic:233"]
And plasma represents ownership of throughput even with the recharge rates.
[/quote]

Assuming we exclude plasma generated by PoW (for simplicity), is it accurate to say the following:

WITHOUT a recharge mechanism, the amount of $qsr owned by a user represents their prorata share of network throughput at all times.  

WITH a recharge mechanism, the amount of $qsr owned by a user represents their  prorata share of network throughput at a point in time based on network conditions?  

I'm just trying to frame the issue so people who are not following the technical details can understand the specific issue we are discussing.  

Also, I do want to point out that [KASPA was attacked](https://forum.hypercore.one/t/dynamic-plasma-discussions/62/56?u=0x3639) with a dust attack that caused the chain to bloat.  They ended up "censoring" valid transactions that they classified as "spam".  However, before applying a patch, their chain was bloated with many GB of data.  From what I can remember, the miners attacked the chain with the hopes of increasing fees, but I'm not 100% sure of that.

-------------------------

vilkris | 2023-12-21 12:48:24 UTC | #42

[quote="0x3639, post:41, topic:233"]
WITHOUT a recharge mechanism, the amount of $qsr owned by a user represents their prorata share of network throughput at all times.
[/quote]
The QSR has to be fused as plasma but yes that would be a highly simplified way of presenting it.

The statement is misleading in my opinion though, since if you're talking about throughput share per momentum, then without adding additional complexity, you cannot guarantee that in a highly utilized network people with low amounts of fused plasma will ever get their share of bandwidth, since a momentum can only accommodate so many transactions.

So maybe the statement is true in theory, but it's inaccurate in practice.

[quote="0x3639, post:41, topic:233"]
WITH a recharge mechanism, the amount of $qsr owned by a user represents their prorata share of network throughput at a point in time based on network conditions?
[/quote]
I think that's pretty accurate.

-------------------------

Nostromo | 2023-12-22 00:07:50 UTC | #43

[quote="vilkris, post:40, topic:233"]
that means that with 100,000 QSR you can bloat the node database at 200,000 B/s indefinitely
[/quote]

Let's assume there's no transaction cap, allowing nodes to add transactions to a momentum until it reaches the size or time limit.

Now, if someone saturates a momentum with 100K QSR worth of plasma, due to the global dynamic plasma variable multiplier, saturating the next momentum will cost them 200K QSR of plasma. The subsequent cost will double with each saturation attempt. (Note: The numbers used are just placeholders and don't necessarily need to be exponential either.)

For the attacker, it's a losing battle, but for the average user, the impact might not be very noticeable.

Consider a user with only 5% of the maximum 5000 fusion units available for an account. This gives them 250 fusion units, providing 525,000 plasma to work with.

Assuming the transaction is 200B at nil dynamic multipliers, it should cost 34,600 plasma. At this rate, the user could make 15 transactions to a Momentum if desired.

However, when the attacker starts saturating, our user can now only add 7.5 transactions, then the next 3.75, and so on. For light to medium user this would be hardly noticeable considering a Momentum occurs every 10 seconds.
  
An exponential multiplier simplifies the example, but one could use an equation to create a J curve or something along those lines.

This system seems very flexible, performing it's purpose whether the network has 5K tps or 500K tps. While it makes sense to me, there might be potential logical errors that need consideration though.

[quote="vilkris, post:40, topic:233"]
This means 16 GB per day and would have a toll on node decentralization and users would basically have to rely on centralized node provider services, assuming node providers find a way to monetize their services.
[/quote]

Nano, for instance, addresses this issue through ledger pruning.
I believe our advantage lies in the MetaDag. While I'm not certain, if I were to guess, I'd say this design decision is partly intended to address that problem.

Sentinels are highly incentivized, particularly as the ZNN and QSR values, compared to BTC, increase substantially. I estimate that in the future, there will be up to thousands of trustless Sentinel nodes and potentially many millions of trusted Sentry nodes that sync very rapidly with zk-proofs.

-------------------------

aliencoder | 2023-12-21 19:59:06 UTC | #44

[quote="Nostromo, post:43, topic:233"]
I believe our advantage lies in the MetaDag
[/quote]

The meta-DAG should be garbage collected as per the Narwhal and Tusk paper. The block-lattice can be also pruned, but I think what matters is the PoW accumulation that enforces the canonical ledger.

[quote="Nostromo, post:43, topic:233"]
there will be up to thousands of trustless Sentinel nodes
[/quote]

The cost of spawning a Sentinel node is 5000 ZNN and 50k QSR. Hundreds of Sentinels is more accurate given the current circulating supply.

-------------------------

Nostromo | 2023-12-22 00:01:42 UTC | #45

[quote="aliencoder, post:44, topic:233"]
The meta-DAG should be garbage collected as per the Narwhal and Tusk paper. The block-lattice can be also pruned, but I think what matters is the PoW accumulation that enforces the canonical ledger.
[/quote]

Ah, that makes sense. I had a hard time understanding why we should have PoW links adding weight, to be honest, but as I read that, it clicked for me.

[quote="aliencoder, post:44, topic:233"]
The cost of spawning a Sentinel node is 5000 ZNN and 50k QSR. Hundreds of Sentinels is more accurate given the current circulating supply.
[/quote]

Yeah, I realized that after I posted it too and thought I'd edit it, but then I thought maybe it would not be unreasonable to change the Sentinel requirements once the network reaches certain milestones. 
For example, if the combined value of ZNN and QSR has gone up by a factor of 1000 from where it is now, it may be possible through governance to reduce the Sentinel requirements by a factor of 10, or something along those lines.

-------------------------

Nostromo | 2023-12-22 02:08:37 UTC | #46

[quote="0x3639, post:41, topic:233"]
WITHOUT a recharge mechanism, the amount of $qsr owned by a user represents their prorata share of network throughput at all times.
[/quote]

[quote="Nostromo, post:33, topic:233"]
somebody owns 1% of the QSR supply, this makes them eligible for 1% of the throughput
[/quote]

I might have been a bit off with this statement in a previous post.

To transition from QSR to plasma, one needs to go through two conversions: QSR to Fusion units and then Fusion units to Plasma.

For instance, let's say somebody has QSR representing 0.00002% of the total throughput, according to the circulating supply of QSR. The threshold to transact, due to dynamic plasma, at a given moment may be 0.000025%. In such a case, that user would need to complete additional PoW for a node to accept their transaction.

This two-step conversion process is quite cool, as I just realized, especially in the context of QSR price increases. One can adjust the conversion rate of QSR to Fusion units without compromising the conversion ratio of Fusion units to Plasma. This feature is quite brilliant and could allow for dynamic QSR plasma cost as well, especially if we had BTC as a currency that could be queried on the network.

-------------------------

vilkris | 2023-12-22 14:12:47 UTC | #47

[quote="Nostromo, post:43, topic:233"]
This system seems very flexible, performing it’s purpose whether the network has 5K tps or 500K tps. While it makes sense to me, there might be potential logical errors that need consideration though.
[/quote]
For plasma requirements to stay relatively low, a simplified mechanism like this requires +1k TPS though, right?

[quote="Nostromo, post:43, topic:233"]
Nano, for instance, addresses this issue through ledger pruning.
I believe our advantage lies in the MetaDag. While I’m not certain, if I were to guess, I’d say this design decision is partly intended to address that problem.

Sentinels are highly incentivized, particularly as the ZNN and QSR values, compared to BTC, increase substantially. I estimate that in the future, there will be up to thousands of trustless Sentinel nodes and potentially many millions of trusted Sentry nodes that sync very rapidly with zk-proofs.
[/quote]
It will take us quite some time to implement all the things you're talking about. I'm more concerned about how we're going to prevent spam attacks from crippling our network in the meantime.

[quote="Nostromo, post:45, topic:233"]
Yeah, I realized that after I posted it too and thought I’d edit it, but then I thought maybe it would not be unreasonable to change the Sentinel requirements once the network reaches certain milestones.
[/quote]
I think something like this would be needed so that the amount of sentinels continues to grow with the network.

[quote="Nostromo, post:46, topic:233"]
This feature is quite brilliant and could allow for dynamic QSR plasma cost as well
[/quote]
Yeah we will probably have to consider this at some point. If we want to support a userbase of millions of people, then the current QSR to plasma conversion ratio is too low, since there simply isn't enough QSR for such a userbase.

-------------------------

Nostromo | 2023-12-23 00:32:45 UTC | #48

[quote="vilkris, post:47, topic:233"]
For plasma requirements to stay relatively low, a simplified mechanism like this requires +1k TPS though, right?
[/quote]

Yes, I think it would make for a miserable experience if it were 10 TPS.

Removing that transaction cap is a necessity for Dynamic Plasma. I have been trying to figure out what size Momentums are, and I can't find any info on it.

I searched the Telegram chat for "Momentum size," and it shows only 8 messages, with one of them being Mr. Kaine saying that a Momentum will have a hard cap. He does not elaborate on whether that will be a hard cap of plasma or megabytes. I'm assuming it is megabytes; that makes more sense to me, but I could be wrong. 

This is a mental model that I'm working with at the moment, and it could be inaccurate:

TPS is mostly limited by what nodes can process, i.e., their hardware and bandwidth. They handle the account blocks.

To be able to keep the transactional ledger lean, they really only need to keep track of account frontiers and can disregard accounts with no balance.

Pillars, using the metaDag, can abstract a transaction's size and cement it. I think you could make a momentum size hard cap of something like 3MB and be able to fit hundreds of thousands of transactions in one. Over 10 years, the DAG would only be around 120 GB.

That's pretty extraordinary if that is somewhat in the ballpark of accuracy.

-------------------------

vilkris | 2023-12-23 11:28:39 UTC | #49

[quote="Nostromo, post:48, topic:233"]
I searched the Telegram chat for “Momentum size,” and it shows only 8 messages, with one of them being Mr. Kaine saying that a Momentum will have a hard cap. He does not elaborate on whether that will be a hard cap of plasma or megabytes. I’m assuming it is megabytes; that makes more sense to me, but I could be wrong.
[/quote]

The momentum has to store the headers of the transactions that are included and those make up most of the momentum's size. I tested that a header is 66 bytes, meaning that a momentum with 100 transactions is roughly 6,600 bytes. So with a limit of 3 MB, this would mean that a momentum could roughly store 45,450 headers, if we're only accounting for the headers.

But I don't understand why a megabyte limit would be superior to a plasma limit, since plasma is an abstracted representation of storage and computational complexity, both of which should be taken into account.

The size of a basic account block appears to be around 420 bytes, which is over double than what I estimated earlier.

[quote="Nostromo, post:48, topic:233"]
Over 10 years, the DAG would only be around 120 GB.
[/quote]
I'm not sure how you arrived at this figure. If the network is maxed out all the time and if one momentum is 3 MB, then that would mean 25,920 MB per day (8,640 momentums per day) and 94.6 TB in ten years. And that's only the consensus ledger.

-------------------------

Nostromo | 2023-12-23 12:32:44 UTC | #50

[quote="vilkris, post:49, topic:233"]
I’m not sure how you arrived at this figure
[/quote]

Wow, I messed up that calculation; it seemed like a really low number. 😅

Thanks for correcting that. The 66 bytes for a header is interesting. Suppose we wanted to target maybe 5,000 transactions per Momentum; that would be 0.33 MB. If that was the hard cap... let me do the numbers correctly this time.

0.33 MB per Momentum = 1.98 MB a minute = 118.8 MB an hour = 2.85 GB a day = 1.04 TB a year.

That still seems like a lot (even though assuming 100% Momentum utilization inflates the number by a lot), Dynamic plasma prevents the Momentums from filling consistently.

I'm not sure what would be a reasonable estimate for average Momentum utilization over a year, maybe 40% - 70%?

-------------------------

Nostromo | 2023-12-23 12:54:20 UTC | #51

[quote="vilkris, post:49, topic:233"]
But I don’t understand why a megabyte limit would be superior to a plasma limit, since plasma is an abstracted representation of storage and computational complexity, both of which should be taken into account.
[/quote]

Yes, perhaps Plasma works better for the hard cap. Thinking about it that way, it does have advantages. Interesting.

*edit: Maybe the computational cost is already accounted for because embedded transactions have the plasma multipliers in place.

-------------------------

SultanOfStaking | 2023-12-27 13:23:21 UTC | #52

To some degree if we can implement a fee now I dont see why we couldnt implement one later if true feeless network is not feasible. we have no daaps... we have nothing to worry about WRT tps and spam right now. I would think we do simplest thing to keep us moving forward (dynamic plasma) and as the platform organically grows we periodically / collectively assess if fees are needed or if we can solve any issues with other means. to me, saying lets slap a fee in our network at this stage seems premature

-------------------------

SultanOfStaking | 2023-12-27 13:28:57 UTC | #53

To be clear, I am not a dev but I do understand there are ripple effects to every decision, and this is a pretty big decision - so take this as an uniformed thought on the subject (also remember many pillar owners are not technical so they may be thinking the same thing).  I enjoy reading this thread and will continue to follow along. Not 100% opposed to a fee at some point for the benefit of the network but struggling to see why we have to decide on it / implement it now.

-------------------------

Shazz | 2023-12-28 02:17:30 UTC | #54

Whatever solution we agree on we should do it quick if we dont want to skip yet another bull run to get some real adoption

-------------------------

Chadass | 2023-12-27 17:06:46 UTC | #55

There is and there will be no real adoption. I agree on the first take though.

-------------------------

Stark | 2023-12-27 18:17:15 UTC | #56

In regards to the facet of the discussion that pertains to fees being familiar and simple for end users: App developers, wallets, dexs, etc have the option to use feeless PoW/PoS plasma on the backend, while charging fees to the end user, in ZNN or any currency of their choosing. Savvy developers who intend to reach retail will choose to accept fees in the currencies that are most convenient for retail.

If owning QSR equates to owning a stake in network capacity, initiatives that charge fees in other currencies will drive immense value into NoM. Requiring users to pay for services and usage in a specific native currencies such as ETH, ZNN, etc is never going to be the way that this technology goes mainstream, because the mainstream masses use fiat currencies.

See the way brands like Nike are onboarding customers to ETH NFTs, by accepting credit card payments.

Every time a normie buys an NFT with a credit card, more value moves into the cryptosphere. That value may very well move back out when the developer buys a lambo, but the point is that fiat onramps and offramps *integrate* crypto into the global economy.

Thus, with PoW and QSR based plasma, NoM developers have the freedom to accept payments in any currency they so desire. (See: Gravity Wallet concept.)

-------------------------

Stark | 2023-12-27 18:20:55 UTC | #57

Is there a way that...

1. A wallet with zero plasma broadcasts a transaction to a receiving address.
2. The receiving address looks at the transaction and decides if it fits certain criteria.
3. If so, the receiving address fuses plasma for the sender.

-------------------------

Nostromo | 2023-12-28 02:21:37 UTC | #58

I think this could be possible, like a plasma rental application. You send 10 ZNN to the address, and the application fuses plasma for 2 months, for example.

This wouldn't be done trustlessly by the network though unless you had an embedded contract that could facilitate it, but one could create an trusted application to do it.

-------------------------

0x3639 | 2023-12-30 16:43:51 UTC | #59

Here is an interesting conversations about SOL fees and MEV.  It's a little boring and only somewhat related.

https://www.youtube.com/watch?v=p2jHGi-yOBk

-------------------------

0x3639 | 2023-12-30 16:46:51 UTC | #60

This is another discussion of fee markets.  It's a little more related to our discussion here. 

One take away for me is these fee discussions on other L1s take years to address and seem to be contentious.  

https://www.youtube.com/watch?v=-9s2SjN1Pg0

-------------------------

0x3639 | 2024-08-26 12:15:36 UTC | #61

Some folks have contacted me about the status of dynamic plasma.  I re-read this post and TBH it's really hard to follow at this point.  I just wanted to point of that if anyone has feedback or suggestions on the design I think now is the time to provide that feedback.  

I'm going to share a private chat with a now deleted alt in TG with the following feedback.  

![Screenshot 2024-08-25 at 1.11.16 PM|558x500](upload://qnV8I3zXMpEFIcSbLIDNWcUWpum.png)

I'm not entirely sure how this works.  In the example above:

If 100 QSR ($0.10 ea) represents 0.0001% of the network throughput today and costs $10 to acquire, does dynamic fusing say if the price goes to $1.00 each we only need 10 QSR to acquire 0.0001% of the network throughput?  

Also, I assume the share of the network goes down over time based on inflation. 
 For example, if the price of qsr remains constant 100 qsr will represent less and less network throughput over time due to inflation.

-------------------------

vilkris | 2024-08-26 12:44:06 UTC | #62

The more urgent node performance updates have been blocking me from working on dynamic plasma, but now that they are more or less finished, I've been working on a second version of dynamic plasma, which aims to simplify the design. I am planning on presenting the second version in a new thread in order to recap the current status and make it easier for others to follow.

-------------------------

Stark | 2024-08-26 15:34:37 UTC | #63

As network capacity increases, users will generally need less % of the throughput and therefore less qsr.

-------------------------

0x3639 | 2024-08-26 22:49:01 UTC | #64

I guess I'm more interested when demand for block space exceeds supply of block space.

When this happens the demand for QSR goes up.  As demand goes up price goes up.  As price goes up the cost to buy qsr and process TXs goes up (assuming no PoW or dynamic fusing).  The message from the deleted TG account seems to imply that as price goes up, the amount of QSR needed to process a TX should go down.

In my mind these two forces seem to negate each other.  I think he (the screen shot above) is implying the following:

Assume blocks are saturated and there is no qsr inflation (to make the example EZ).  Demand for QSR goes up to process TXs, price of QSR goes up because demand is up, amount of QSR (plasma) needed to process a tx goes down (dynamic fusing) to keep the "cost" of a TX stable. Now that it takes less QSR to process a TX demand goes down and therefore the price of QSR goes down.  This up and down price movement should cause the price of QSR to be stable over time and the only thing that causes the price to go up is a reduction in supply (launch pillars of sentinels).  

Now remove the assumption that there is no inflation.  The long term price of QSR becomes a balancing act between inflation vs launching nodes.

This is a super over simplification but generally this is what I think `deleted account` was proposing.  

I guess the market cap of QSR becomes the overall cost to access 100% of the total computing power of the network less the governance value associated with ZNN to control the network plus a speculation factor.  

Am I looking at this correctly?  Maybe I'm totally wrong.

-------------------------

