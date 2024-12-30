Thread: ideas-for-dynamic-plasma-revisited
vilkris | 2024-10-10 16:19:30 UTC | #1

A while has passed since I posted some [initial ideas](https://forum.hypercore.one/t/ideas-for-dynamic-plasma/233) for a dynamic plasma solution. Since that time I have gained a better understanding of our network's implementation and received feedback from the community on those ideas. Based on this I have revised the initial ideas, hopefully bringing us closer to a first version of dynamic plasma.

I will be referring to the initial dynamic plasma ideas as V1 and to the revised ideas as V2.

## Problems with dynamic plasma V1

### The plasma recharge concept

The main criticism for V1 has been towards the fused plasma recharge concept. The main arguments against it are the following:

* Adds unnecessary complexity without bringing much benefit.

* Bad UX for users, since the recharge rate is determined by the network and the user cannot affect it.

* Not really needed to achieve the goals of dynamic plasma.

I think these arguments are reasonable and I think that at this stage a recharge mechanism is not necessary for dynamic plasma. If such a mechanism were to be included, we may be trying to solve problems that don't exist. This is not to say that such a mechanism can't be added later on, if there is a demonstrable need for it.

### Balancing fused plasma and PoW plasma

In V1 I proposed that fused plasma and PoW plasma could be balanced by adjusting the `DifficultyPerPlasma` parameter, but this has some issues:

* Conceptually, the `DifficultyPerPlasma` parameter determines the difficulty of plasma on the account chain level. Using this parameter to balance the usage of fused plasma and PoW plasma on the momentum ledger level messes with this concept.

* The value of `DifficultyPerPlasma` is dependant on the used PoW algorithm. If we switch to another algorithm, like [RandomX](https://github.com/tevador/RandomX), then the `DifficultyPerPlasma` value will have to be adjusted.

* In order to be able to balance fused plasma and PoW plasma usage, the value of `DifficultyPerPlasma` will fluctuate, but when an account block is validated on the account chain level a hardcoded `DifficultyPerPlasma` value will have to be used. This will result in two separate `DifficultyPerPlasma` values - one for the account chains and one for the momentum ledger, which is not ideal.

## Revised ideas for dynamic plasma (V2)

The main goals that this revised concept for dynamic plasma aims to achieve are the following:

* Ensure that one resource (PoW or fusion) cannot be used to access all of the network's resources in perpetuity.

* Allow users to bid for account block confirmation via an auction mechanism.

* Keep the design simple.

### Balancing fused plasma and PoW plasma usage

To achieve the first goal, a pricing mechanism is introduced for the two plasma resources. This means that fused plasma and PoW plasma have their respective prices that are determined algorithmically by the network. The resource prices set a minimum price on fusion and PoW that an account block has to "pay" in order for the block to be eligible for inclusion in a momentum.

For example: A regular send account block requires 21,000 base plasma. If a user is generating the required plasma with PoW and the current price of PoW plasma is 1.25, then the minimum amount of PoW plasma required for the account block to be eligible for inclusion in the next momentum is 21,000 * 1.25 = 31,500 PoW plasma.

Example of the pricing algorithm for PoW plasma, when the PoW plasma usage target is 25% of the momentum's maximum capacity:

| Momentum Height | PoW Plasma Usage | Next PoW Plasma Price | Price Change |
|---|---|---|---|
|1|25%|1|0%
|2|50%|1.05|5%
|3|50%|1.16|5%
|4|50%|1.22|5%
|5|100%|1.34|10%
|6|100%|1.47|10%
|7|100%|1.62|10%
|8|100%|1.78|10%

Example implementation of the algorithm that calculates the price of a plasma resource:

```
const MIN_RESOURCE_PRICE = 1
const MAX_PRICE_CHANGE_RATE = 0.1
const PRICE_CHANGE_DENOMINATOR = 20

function calculateResourcePrice(currentPrice, usedBasePlasma, targetBasePlasma) {
    const changeRate = Math.min(((usedBasePlasma / targetBasePlasma - 1) / PRICE_CHANGE_DENOMINATOR), MAX_PRICE_CHANGE_RATE)
    const newPrice = currentPrice * (1 + changeRate)
    return newPrice >= MIN_RESOURCE_PRICE ? newPrice : MIN_RESOURCE_PRICE
}
```

### PoW base plasma & fused base plasma

Base plasma is an abstraction that represents computational resources. In order to balance how much of the network's available computational resources can be used by PoW and fusion, there has to be a mechanism to associate PoW and fused plasma usage with base plasma. Currently there is no concept of fused base plasma or PoW base plasma on the network, so a mechanism to calculate a nominal base plasma value for the resources is needed.

Example of calculating nominal base plasma values for an account block:

```
function calculateNominalBasePlasma(block, fusionPrice, workPrice) {
    const effectiveFusedPlasma = block.fusedPlasma / fusionPrice
    const effectivePowPlasma = block.powPlasma / workPrice
    const totalEffectivePlasma = effectiveFusedPlasma + effectivePowPlasma

    const nominalFusedBasePlasma = effectiveFusedPlasma / totalEffectivePlasma * block.basePlasma
    const nominalPowBasePlasma = effectivePowPlasma / totalEffectivePlasma * block.basePlasma
    return [nominalFusedBasePlasma, nominalPowBasePlasma]
}
```

Note: The resource plasma values are divided with the resource's price in order to calculate how much resource plasma is used without the mandatory plasma demanded by the resource's price. If this is not done, then a discrepancy in resource prices will skew the amount of base plasma that is allotted to a resource.

### Prioritization of account blocks

When a pillar determines which blocks to include in a momentum, it will use the following formula to calculate a priority value for an account block and sort the blocks according to this value. This allows users to bid for account block confirmation when the network is congested:

```
const priority = (block.fusedPlasma / currentFusionPrice + block.powPlasma / currentWorkPrice) / block.basePlasma
```

A pillar still has the ability to leave out blocks from a momentum at its discretion, but the network will only consider a momentum valid if all the included account blocks pay the minimum required fusion and work prices.

Note: The maximum priority an account block can have is the priority of the oldest uncommitted account block in the account chain. This is because if there are multiple uncommitted account blocks in an account chain, the sequential ordering of the blocks must be preserved.

### Embedded account blocks

Currently embedded account blocks have infinite plasma. Because of this I think it is easiest to leave embedded blocks unaffected by dynamic plasma. This means that embedded account blocks will always be included in a momentum up to a hard limit (that should not every be reached under normal conditions). 

The extra resources needed to process embedded account blocks are already paid for by the user blocks that send the commands to the embedded contracts.

### Estimating plasma fees

In V1 I proposed the usage of an Ethereum style algorithmic base fee mechanism (EIP-1559). This mechanism can be used with the revised version as well, but it is not mandatory. The benefits of this mechanism have been discussed in the [V1 thread](https://forum.hypercore.one/t/ideas-for-dynamic-plasma/233).

If the algorithmic fee estimation is not used, then we will need to create another way to estimate fees, such as using historic fee data, so that wallets can show users accurate fee estimates.

I'm in favor of the algorithmic base fee mechanism, since it simplifies fee estimation and relieves us from the burden of building a separate fee estimation mechanism into the node.

## Dynamic plasma simulator

A simple simulator for dynamic plasma V2 can be found here: https://dynamic-plasma.netlify.app

The simulator can be used to simulate how the usage of fused plasma and PoW plasma affects the resource prices.

The simulator has the following configuration:

* A momentum's maximum allowed base plasma is 4,200,000 (200 regular account blocks)

* The fused base plasma usage target is 25% of the maximum base plasma (1,050,000 plasma / 50 regular account blocks)

* The PoW base plasma usage target is 25% of the maximum base plasma (1,050,000 plasma / 50 regular account blocks)

This configuration allows for algorithmic fee estimation, since the combined usage target of fused base plasma and PoW base plasma is 50% of the maximum allowed base plasma.

## Open items

### PoW and fusion usage targets

What PoW and fusion usage targets are reasonable? Right now it's clear that only a small amount of transactions are sent with PoW plasma, which would suggest that the PoW usage target could be relatively small. But using a small target for PoW plasma means that fused plasma becomes cheaper to use, which may not be desired when the network's throughput is saturated.

An equal split between the plasma types is arguably the most fair and unopinionated choice since ultimately we don't have data that would show how the plasma types are utilized in a congested network. The usage patterns may be very different compared to a nearly empty chain. But I'd like to hear if there are other viewpoints.

### Integer vs floating point math

The calculations used in the simulator rely on floating point math but it might be a good idea to try to avoid floating point math in favor of integer math to avoid potential rounding issues.

-------------------------

Stark | 2024-10-10 22:49:45 UTC | #2

![video-output-425815BE-7688-4C8E-8A37-1C796F901B83|video](upload://rzHxpFT27hr0tHgOyMl3qOssJCa.mov)

-------------------------

0x3639 | 2024-10-11 00:49:10 UTC | #3

Have you thought about how V2 would work under very high load?  What would happen if we uncapped transactions and assumed 100,000 tps or more? Does the system work and if not should we be planning for that now?

All signs point to the chain being capable of very high throughput once N&T is implemented.  

So just wondering if we should be planning for that now?

-------------------------

cap | 2024-10-11 02:07:24 UTC | #4

IMO the equal split between plasma types seem ideal for now. 

Once network usage rises, I think that it would be smarter to tip the scale towards non-POW plasma. This will naturally cause the network emitted QSR to begin it's true utility conquest as people flock to the more optimal solution considering how much more beneficial it would be according to the users purpose.

-------------------------

vilkris | 2024-10-11 11:40:00 UTC | #5

The mechanism will work the same regardless of what the hardcoded throughput limit of the network is. More throughput will just make the cost of transactions cheaper, but I do think that a hardcoded throughput limit is needed whether it be 10 TPS or 100,000 TPS. A completely "uncapped" network doesn't make sense to me and our current network implementation certainly does not support such an idea. There can be a big difference between something that is theoretically possible and something that is actually feasible.

If our network is successful in the long run, then I am certain that whatever solution we have for dynamic plasma now will have to be adjusted and improved upon as the network matures.

-------------------------

CyberSpaghetti | 2024-10-13 11:00:41 UTC | #6

Hi, 
Awesome work you have done there, it is really positive and great to see you put so much effort, time and care into your ideas, big kudos to you! 

It certainly is an interesting idea you propose, if you don’t mind I would like to introduce you to some thoughts and ideas I’ve had regarding DP. I would like to preface though that I’m not an expert in the subject and at best a lower end intermediate skilled programmer with a focus on graphics and games. I will be speaking in generalities and will get a few details wrong, which is a problem because as we all know the devil is in the details, but nonetheless I think it could still be worthwhile.

Where to begin? Maybe I’ll start with a generalized flow from account block to momentum:

User submits a transaction and an account block is created >
Account block is submitted to node which will verify correct formatting >
The node will broadcast the account block to other nodes >
Account block is now in a pool of uncommitted blocks >
A new momentum is created and a pillar makes an array of uncommitted blocks >
The pillars filters the array in a for loop that will stop at 100 >
This limits the amount of account blocks that can be committed to the momentum 

Three things I want to highlight here are:
The entry point 
The pool 
The worker

The nodes are the entry point to the pool and they will check if requirements for entry are met.
The worker will scoop the blocks from the pool, roll them into a momentum and generate auto receive blocks to complete the transaction cycle. 


Pillars are not selective when they scoop, they filter by block type but do not prioritize one address over another, it currently is agnostic to that from what I can tell.

So now, we can ask what’s the point of plasma and what’s the point of dynamic plasma?

We can create a thought experiment and think through what happens if we try to flood the pool with transactions, say I have 50k QSR and I flood the pool. 
The QSR will be tied up in unconfirmed blocks and the pool will be large, but momentums keep clearing 100 blocks a pop, so all that has occurred is that a queue has formed and transactions take longer to complete their cycle.


 
Let’s roughly calculate the damage:
We will estimate a send and receive to cost 20 QSR 
So at 50K QSR we could theoretically pop off 1250  send transactions
The plasma of the unconfirmed blocks are tied up so you are able to pump 12.5 momentums worth of blocks into the system in a continuous and staggered fashion
At this rate you are creating a queue on average of just over 2 min.

So we can see here that it would take a lot of QSR to create major inconveniences.
(Also we have POW transactions to take into account, here we have the economic cost and time spent in POW that makes it difficult to flood the pool, but that is a topic in and of itself.)

If somebody was so motivated and decided to use say 500k or 1m QSR they could create a queue of 20 to 40 min, of course this can also just be total network usage at a given point.     

So what to do? The easiest solution would be to change the MaxAccountBlocksInMomentum variable to, say 200, now we have doubled the amount a pillar may scoop from the pool and halved the average wait time. 
Not bad, the next thing we could look at is the entry point, we could say the more unconfirmed blocks are in the pool the more plasma it will cost to enter the pool. This relationship could be established by saying the amount of plasma needed is:
Base plasma + (length of the unconfirmed blocks array * multiplier) 
In effect this would cause the rate at which blocks can be added to the pool to decrease as the size of the pool increases.

So we have a relationship here where on one end we have the rate at which pillars clear blocks from the pool and on the other end we have the rate at which they can enter the pool. 

Viewed like this there are a few things one could tweak. For example, the more we allow the pillars to scoop the less steep the multiplier needs to be. 

I hope this makes sense to you, I’ll just leave it there for now and see what you think about it.

-------------------------

0x3639 | 2024-10-14 01:38:37 UTC | #7

[quote="CyberSpaghetti, post:6, topic:495"]
In effect this would cause the rate at which blocks can be added to the pool to decrease as the size of the pool increases.
[/quote]

To be clear, we assume this would slow the addition of blocks because the cost to add them would go up?  What if it does not slow the addition of blocks because demand gets crazy before we can increase the MaxAccountBlocksInMomentum limits? does the multiplier need to be a function of the length of the queue to address this?  

Ideally we would increase MaxAccountBlocksInMomentum to address the situation above, but maybe that will not be so easy.  Or maybe Pillars are tapped out.

-------------------------

CyberSpaghetti | 2024-10-14 06:16:36 UTC | #8

Increasing the amount of plasma it costs to submit a transaction will definitely slow the rate at which blocks get added to the pool. It will take a client longer to complete the pow and generate the required plasma, which will slow the rate of blocks being added.

In similar fashion if you have 40 QSR fused and plan to make 4 transactions at once, due to the higher plasma requirement you will need more plasma than you have available. You will need to either do them in smaller batches and wait for your plasma to replenish, or you do them at once and spend time in pow to generate additional plasma. Both ways have the effect of creating a time buffer before your blocks hit the pool.

Maybe a good analogy of the system is a bathtub. 
A bathtub has a drain which can empty the water at a certain rate.
If we pour water into the tub at a rate that is lower than the rate it is able to drain then the tub stays empty.
But, if we pour water in at a rate that is greater than the rate of drainage the tub will fill and overflow eventually. We can prevent this by decreasing the rate which we pour water in to be lower than the rate we can drain. 

In this analogy the drained water is available to be fed back into the tub, so it's a circular system.
Furthermore instead of pouring the water we can also dump water, if we dump more water at once than the tub can hold then we will overflow. Hence the tub must be able to hold the maximal amount of water practically available. 
The system needs a defined maximal amount of water which is the QSR supply.
The maximum plasma, which is represents transactions, is regulated by the conversion rate from QSR to plasma and pow difficulty.

If we do dump vast amounts of the available water into the tub, we create a pool of water and we cannot continue dumping at the same rate as we will run out of the available water and will need to wait for the drainage to drain the tub and move the water back into a space where we can use it again.  

The example I previously gave wasn't meant to be directly mapped to the implementation.
So when I said increase MaxAccountBlocks to 200 it was just for illustrative purposes to demonstrate how increasing the drainage rate will effect the system.

There is a deeper and far more detailed technical discussion required when considering the drainage rate of the tub. 

The rate at which we regulate how much water is poured is a better starting point in the discussion.

-------------------------

CyberSpaghetti | 2024-10-14 05:11:29 UTC | #9

![ZenonBathTub|690x388](upload://zd57QFWB1sArmxWqUyxIf9HxYpC.png)

-------------------------

vilkris | 2024-10-14 06:18:24 UTC | #10

@CyberSpaghetti Nothing is currently stopping a node operator from creating arbitrary limits on their account pool. Enforcing rules on the momentum ledger based on the account pool is not feasible since every node can have their own account pool state.

Regarding the ideas in the starting post - is there something you think is problematic or misguided?
The main goals I have outlined are how to balance PoW and fusion usage and how to order/prioritize transactions when the network is congested.

-------------------------

CyberSpaghetti | 2024-10-14 08:42:50 UTC | #11

Some things that comes to mind from the top of the head would be:
A priority system where users bid is not very meaningful in our design - A pillar has no gain from including a block that has more or less plasma attached to it, unlike in a system where users pay fees and the validator can gain from it.
So you would just programmatically make pillars sort by highest plasma. People with the largest QSR holdings can front run the pool, I don't think that is great outcome and seems quite antithetical to the concept of feeless transactions and fairness in general.


I'm not sure that DifficultyPerPlasma is dependent on the POW algo. In the POW links library the difficulty is passed in as an argument to the main function, as such difficulty can be passed and translated to any algo implementation

you say "In order to be able to balance fused plasma and PoW plasma usage, the value of DifficultyPerPlasma will fluctuate"

I don't  know if this is correct, DifficultyPerPlasma could remain a constant. If more plasma is required  you can generate more units at the same rate of difficulty, thereby increasing your time spent on pow and protecting from transaction spam.

I am not completely sure how the difficulty gets passed into POW links cpp though.

Those are some thoughts.

-------------------------

CyberSpaghetti | 2024-10-14 08:39:29 UTC | #12

[quote="vilkris, post:10, topic:495"]
Enforcing rules on the momentum ledger based on the account pool is not feasible since every node can have their own account pool state.
[/quote]

Every node has their own state - but when a pillar worker makes an array of unconfirmed blocks, this could be used to derive plasma requirements for the next momentum and broadcast to nodes - in general terms.

-------------------------

vilkris | 2024-10-14 09:02:50 UTC | #13

[quote="CyberSpaghetti, post:11, topic:495"]
A priority system where users bid is not very meaningful in our design - A pillar has no gain from including a block that has more or less plasma attached to it, unlike in a system where users pay fees and the validator can gain from it.
So you would just programmatically make pillars sort by highest plasma. People with the largest QSR holdings can front run the pool, I don’t think that is great outcome and seems quite antithetical to the concept of feeless transactions and fairness in general.
[/quote]
An ordering mechanism is needed and ordering based on plasma fits well with the network's current design and is easy for users to understand. It should be in the interest of pillars to prefer transactions that commit the most resources (plasma) to the network. Nothing is "feeless" and the word feeless has no place in technical discussion. It's a marketing term meant to evoke an emotional response. I don't understand what you're suggesting the ordering mechanism to be.

Also, using the algorithmic fee estimation mechanism I've proposed would inhibit the effect of high plasma transactions front running the pool.

[quote="CyberSpaghetti, post:11, topic:495"]
I’m not sure that DifficultyPerPlasma is dependent on the POW algo. In the POW links library the difficulty is passed in as an argument to the main function, and so difficulty can be passed and translated to any algo.
[/quote]
I've modified the PoW lib to use RandomX to test it and this is the logic I'm following:
 
SHA3 => with difficulty 31,500,000 it takes around 30 seconds on average to generate the nonce on my computer.
RandomX => with difficulty 7,500 it takes around 30 seconds on average to generate the nonce on my computer.

This is because the hashrate of RandomX is much slower.

The difficulty values cannot be changed, since the average time should stay constant. The base plasma value should also not be changed.

This leads to:
`DifficultyPerPlasmaSha3 = 31,500,000 / 21,000`
`DifficultyPerPlasmaRandomX = 7,500 / 21,000`
 
This is why I've abstracted the difficulty of PoW into the on-chain WorkPrice variable, so that the DifficultyPerPlasma constant can be modified (if the PoW algo changes) without affecting the current on-chain price of PoW plasma.

[quote="CyberSpaghetti, post:11, topic:495"]
you say “In order to be able to balance fused plasma and PoW plasma usage, the value of DifficultyPerPlasma will fluctuate”
[/quote]
I was just referring to how it would have worked in V1.

-------------------------

CyberSpaghetti | 2024-10-14 11:49:39 UTC | #14

[quote="vilkris, post:13, topic:495"]
An ordering mechanism is needed and ordering based on plasma
[/quote]
I think this is necessary in the bathtub version too, the amount of plasma attached can be used to determine in what order the block entered the pool. So if the amount of unconfirmed blocks is increasing the transactions with lowest plasma get processed first, because they have been in the pool for longer, and if the pool is decreasing it goes the other way around, but you need something a bit more fancy to make it work, maybe use an offset or a delta or something that.

In your version you could run into the problem that if you submit a transaction with too low plasma for pillars to accept it can be there for a very long time, potentially being irretrievable for the user and these "dead" blocks could pollute the pool. 

[quote="vilkris, post:13, topic:495"]
It should be in the interest of pillars to prefer transactions that commit the most resources (plasma) to the network
[/quote]
 I don't really understand why you think this, what is your line of reasoning for this?
I would think it be in the best interest of everybody if pillars processed as many transactions as they can do safely. 

[quote="vilkris, post:13, topic:495"]
Nothing is “feeless” and the word feeless has no place in technical discussion.
[/quote]
Nano has completely feeless transactions. 

But anyway, I guess our views and vision do not align or converge on this topic, which is completely fine. I thought it was worthwhile to present a different angle, but if you don't see it that's okay :smiley:

-------------------------

aliencoder | 2024-10-14 12:29:43 UTC | #15

[quote="CyberSpaghetti, post:14, topic:495"]
In your version you could run into the problem that if you submit a transaction with too low plasma for pillars to accept it can be there for a very long time, potentially being irretrievable for the user and these “dead” blocks could pollute the pool.
[/quote]

Low sat Bitcoin txs are removed from the mempool if they timeout. Same principle can be applied to low Plasma account-blocks.

https://bitcoin.stackexchange.com/questions/46152/how-do-transactions-leave-the-memory-pool

[quote="CyberSpaghetti, post:14, topic:495"]
Nano has completely feeless transactions.
[/quote]

I agree with @vilkris here. Nothing is free in the sense that users commit computing resources for transactions. Those resources are reflected into the ledger, so everyone is benefitting in the end.

-------------------------

vilkris | 2024-10-14 12:31:15 UTC | #16

[quote="CyberSpaghetti, post:14, topic:495"]
I think this is necessary in the bathtub version too, the amount of plasma attached can be used to determine in what order the block entered the pool. So if the amount of unconfirmed blocks is increasing the transactions with lowest plasma get processed first, because they have been in the pool for longer, and if the pool is decreasing it goes the other way around, but you need something a bit more fancy to make it work, maybe use an offset or a delta or something that.
[/quote]
What's the benefit of putting the dynamic plasma requirement in front of the account pool instead of the momentum, like I'm proposing? Don't you end up with same result => you need more plasma to send transactions when the network is congested.

[quote="CyberSpaghetti, post:14, topic:495"]
In your version you could run into the problem that if you submit a transaction with too low plasma for pillars to accept it can be there for a very long time, potentially being irretrievable for the user and these “dead” blocks could pollute the pool.
[/quote]
If that happens a wallet could automatically generate more PoW for the block and replace it. If the algorithmic fee estimation is used, it should be unlikely for this to happen though, since there is reserve space in the momentum exactly for this reason.

[quote="CyberSpaghetti, post:14, topic:495"]
I don’t really understand why you think this, what is your line of reasoning for this?
I would think it be in the best interest of everybody if pillars processed as many transactions as they can do safely.
[/quote]
All nodes, not just pillars, have to process all transactions. Demanding more resources from nodes is a centralizing force and centralization is definitely not in the best interest of everybody.

[quote="CyberSpaghetti, post:14, topic:495"]
Nano has completely feeless transactions.
[/quote]
In a technical sense I disagree - just because they don't have a fee property in their transactions doesn't mean they don't have some abstracted form of a fee.

They themselves describe their fee being opportunity cost. So basically by holding Nano dormant in your account for x amount of time gives you n amount of priority.

In a sense our PoW/fusion mechanism has a similar idea => to get priority you can either stake QSR or generate PoW (wait).

The difference being that we can convert these resources into a value that represents throughput (plasma), which gives the user more immediate control over how much resources they want to commit to a transaction.
I believe this will ultimately provide a better experience for the user in a congested network.

[quote="CyberSpaghetti, post:14, topic:495"]
But anyway, I guess our views and vision do not align or converge on this topic, which is completely fine. I thought it was worthwhile to present a different angle, but if you don’t see it that’s okay :smiley:
[/quote]
I appreciate you discussing this. It is definitely welcomed.

-------------------------

CyberSpaghetti | 2024-10-15 02:57:54 UTC | #17

[quote="vilkris, post:16, topic:495"]
All nodes, not just pillars, have to process all transactions. Demanding more resources from nodes is a centralizing force and centralization is definitely not in the best interest of everybody.
[/quote]

Okay, I get it now, this statement was an a-ha moment for me to understand from where your design decisions are coming from. 

So, this statement is correct, but it's not the full picture. Account chains are updated on the transactional ledger asynchronously. So when I make a send transaction, my node adds a send block to my account chain and shares that with all the other nodes and within, however many milliseconds it takes, all the nodes have the updated version of my account chain and the transaction was 'processed'.

Importantly, all the transactions occur independent of the global consensus.  
The tps on that ledger is super fast. The transactions are already propagated and processed, albeit in an unconfirmed state, before a pillar even begins its work. 

Meta-DAG, or momentum ledger is for creating the consensus. So the pillars are a full node with extra functionality and responsibility, they create consensus and confirm and finalize blocks.

This means there is a higher computational burden on a consensus node vs a full node.

They need to make a buffer of all the blocks, iterate through them and create consensus and finality through momentums etc.
And for this and other things we incentivize the operation heavily.

In a way its quite funny to have a network that does thousands of tps on one ledger and then only confirm them at 10tps on the other. Quite obviously this is somewhat of a stupid state to be in. 

It must be obvious that any changes made must have as their goal to improve this bottleneck.

So why is it this way? I'm not sure, but I've been trying to work out what happens when momentums fail. When we have a set of pillars selected for a consensus round, what would happen if they all failed to make valid momentums? 

Fundamentally I think this may be why that account block cap was put in place, to prevent failed momentums as the highest priority. Obviously a pillar could confirm hundreds of thousands blocks, but the key is that it only has a specific window of time to do so. Dynamic Plasma is needed to put an upper bound on the buffer a pillar has to deal with. If the block buffer is too large pillars would fail momentums.   

If you put the plasma requirement in front of the momentum you are treating the block confirmation like a transaction, which it is not. You are also reinforcing the artificial bottleneck which has no correlation to actual capacity and will create bad UX.
A user will need to be made aware of the plasma trend and there needs to be a whole interface to adjust this, making it more difficult for users and other entities to have reliable transaction with predictable confirmation times. 

By putting it in front of the pool we give the pillars a safe amount of blocks to confirm that actually correlate to their capabilities creating good UX.
If the node tells you what is needed and the average confirmation time is equally distributed, you have optimal utilization of your plasma and pow and reliability and predictability for users and other entities, such as maybe different types of contracts that may be added in the future. 

There are a number of ways to do this, one could be you take the recommended specs for a pillar and benchmark how many confirmations can it perform within a given timeframe. You take that number, maybe subtract 20% and then scale all of your dynamic plasma around this.

There are also other possibly even better ways.

Anyway, this is in general terms the crux of the situation in my opinion.
But honestly I do not know how relevant this dynamic plasma situation is overall anymore, if according to Mr Kaine Phase 1 implements Narwhal consensus.

In comparison with other networks that can achieve confirmation times in the milliseconds the granularity of our momentum timeframe for confirmations seems like the grand canyon.
Narwhal will close this gap hopefully..  

But none the less, it is still worthwhile to figure things out in the alpha net implementation.

-------------------------

vilkris | 2024-10-15 14:11:47 UTC | #18

I don't think your assessment of the current network is entirely correct and your line of thought is based on a false pretense. When a pillar produces a momentum it will broadcast the momentum to its peers and all nodes will eventually receive it. When a node receives the momentum it will validate the momentum. To validate the momentum it will have to process and validate all the transactions included in the momentum. So if there are 100k transactions in the momentum, the node will have to process all of them to ensure the momentum is valid.

You can't get around the fact that if you want your node to validate the momentum ledger, then the node will have to validate all the state changes that occur on the ledger. If we start pushing massive momentums that require lots of computing power to validate in a reasonable time, then there will be very few people willing to run a node.

The difference in computational burden between pillars and regular nodes is minute, since the only additional work a pillar is doing is sorting and filtering the blocks from the account pool when creating a momentum and a pillar isn't continuously creating new momentums anyway.

In any case, if we have a way to significantly increase network throughput without too many tradeoffs, then the dynamic plasma ideas in the starting post are still valid.

[quote="CyberSpaghetti, post:17, topic:495"]
A user will need to be made aware of the plasma trend and there needs to be a whole interface to adjust this, making it more difficult for users and other entities to have reliable transaction with predictable confirmation times.
[/quote]
Hence the EIP-1559 style algorithmic fee estimation mechanism. I've stated this many times already. A wallet can automatically make reasonable decisions on behalf of the user. But what we don't want is to rob the user of the ability to make those decisions and then claim we've improved the UX.

The guiding principle being that if I want to commit more resources to get my transaction confirmed faster, then I should have the ability to do so.

-------------------------

CyberSpaghetti | 2024-10-16 01:58:21 UTC | #19

Yeah nodes need to validate the signatures, Zenon uses ed25519 signing algorithm, in this paper it is stated that a 15 year old quad core Xeon CPU,  which can now be purchased for under $80, can verify 7100 signatures a second ( https://ed25519.cr.yp.to/ed25519-20110926.pdf )

In this Rust implementation, an Intel i7 10700K which is an average consumer grade 2020 vintage CPU I believe, is benchmarked to verify signatures in 40 micro seconds, which is 0.00004 Seconds and as follows can verify 25 000 signatures a second. 
( https://github.com/dalek-cryptography/ed25519-dalek )

Beyond this, one also has the ability to batch signatures for even faster performance, as detailed in the paper above.

I can't see why there is a need to be transaction phobic, all we need is dynamic plasma to create a frame in which to play, and we will have a fantastic improvement to the current state.

[quote="vilkris, post:18, topic:495"]
I don’t think your assessment of the current network is entirely correct
[/quote]

No doubt, as I said at the beginning I will get many details wrong, most likely I will look back at my posts in 6 - 12 months and cringe at what I said, as is so often the case.

-------------------------

vilkris | 2024-10-16 04:52:14 UTC | #20

[quote="CyberSpaghetti, post:19, topic:495"]
Yeah nodes need to validate the signatures, Zenon uses ed25519 signing algorithm,
[/quote]
Yes but not only that. When processing a momentum the node has to also apply and persist the transactions onto the momentum ledger database, which is the slow part.

[quote="CyberSpaghetti, post:19, topic:495"]
I can’t see why there is a need to be transaction phobic, all we need is dynamic plasma to create a frame in which to play, and we will have a fantastic improvement to the current state.
[/quote]
The short answer is because the current node implementation simply cannot handle high TPS in the way that you're describing it. Sure the node can handle more than 10 TPS, but increasing the throughput limit of the network will require more storage space and processing power from nodes and deciding on what that limit is is not really in the scope of dynamic plasma. That's a whole different discussion to have.

There is work to be done to improve the performance of the node. I've worked on some of the issues recently:
[Improve account block validation performance](https://github.com/zenon-network/go-zenon/pull/44)
[Improve account pool performance](https://github.com/zenon-network/go-zenon/pull/43)

-------------------------

CyberSpaghetti | 2024-10-17 00:03:42 UTC | #21

That's not great, the standard for the popular high tps networks is RocksDB it seems.
Though Cosmos rolls their own levelDB and looks like it handles around 4K tps per chain on Tendermint. The hardware requirements for a Cosmos validator look the same as ours, 
4 cores
8 GB Ram
1 TB Nvme
   
Seems like there is a lot of work needed to get Zenon to a competitive level.

-------------------------

0x3639 | 2024-11-04 11:17:59 UTC | #22

@vilkris @CyberSpaghetti have a look at the article below.

GPT Summary

The article "[MEV meets DAG: Exploring MEV in DAG-based blockchains](https://hackmd.io/@0xtrojan/mev_meets_dag)" examines the potential for Miner Extractable Value (MEV) within blockchains that utilize Directed Acyclic Graph (DAG)-based consensus protocols, specifically focusing on Narwhal and Bullshark.

The article suggests that while the Narwhal-Bullshark architecture introduces unique transaction ordering mechanisms, it does not inherently eliminate MEV. The potential for MEV depends on how transactions are ordered within the DAG and the specific consensus rules applied. For instance, if transactions are ordered by gas price, as implemented in some systems, it can impact MEV dynamics. Therefore, the design and implementation of the consensus protocol and transaction ordering mechanisms built on top of Narwhal and Bullshark play a crucial role in determining the extent of MEV in such systems.

In summary, the article indicates that MEV is possible within the Narwhal-Bullshark framework, and its presence and magnitude are influenced by the specific transaction ordering strategies employed.

-------------------------

