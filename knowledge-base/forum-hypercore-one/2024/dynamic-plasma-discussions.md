Title: Dynamic plasma discussions

URL Source: https://forum.hypercore.one/t/dynamic-plasma-discussions/62/print

Published Time: 2023-05-17T12:45:23+00:00

Markdown Content:
I couldn’t find another place where Dynamic plasma has been discussed and I know [@georgezgeorgez](https://forum.hypercore.one/u/georgezgeorgez) is looking into it, so I created this topic.

[sumamu](https://forum.hypercore.one/u/sumamu) May 17, 2023, 12:47pm  2

[@georgezgeorgez](https://forum.hypercore.one/u/georgezgeorgez), which one of the following approaches do you think would be best?

*   an overall network difficulty
*   individual difficulty for each account-chain
*   a combination of both

I would go with the third option, a combination of both. At the moment we have network-wide hardcoded values.

Transactions happen at account-chain level (block-lattice), while momentums “sync” the dual-ledger.

so “difficulty” has historically referred to PoW requirements

we need a per momentum plasma cap  
and then the ability for users to specify an amount of plasma for a tx which gets refunded upon confirmation  
there is a plasma cap per account

that all works without pow  
what is also needed is a conversion between pow and plasma (the balancing of pow and pos)

there isn’t really an obvious natural balancing mechanism  
unless we create a separate lane for pow txs  
e.g pow competes for X% amount of network bandwidth

i’m not sure what adjusting difficulty on a per account chain basis achieves

i have some ideas of using sentinel pow to gauge the pow → plasma calculation  
but pow plasma will be asic resistant randomX while sentinel pow may make sense to go with sha256 for merge mining infrastructure

[sumamu](https://forum.hypercore.one/u/sumamu) May 17, 2023, 5:18pm  5

What is the reason for a per momentum plasma cap?

So the use would send more plasma than necessary and the plasma that is not consume would be refunded?

Is this a cap for the total amount of plasma an account would be able to hold or a plasma cap on the amount of plasma an account would be able to consume?

There is a mechanism that converts PoW to plasma already. So we could simply adjust the ratio of plasma for PoW and/or change the PoW algorithm.

The PoW to plasma conversion ratio could serve as a control mechanism, so we’d adjust it based on network congestion.

It could be used to rate limit accountchains transaction rate to prevent spamming. We could combine this with a way to limit accountchain creation by forcing every new (with height == 0) accounchain’s first block (height == 1) to be a RECEIVE transaction, this way they would first need to receive something from another address. This way, in case there’s a spam attack, the attacker is also limited from creating countless accountchains, since the attacker’s previous accountchains are also limited.

I don’t understand why or how sentinels would be doing PoW. I was thinking we could use sentinels as oracles instead.

Isn’t the point of dynamic plasma to protect the network against spamming while in case of high usage still allowing transactions to happen in a feeless way (PoW or Fuse QSR).

If we’d eliminate PoW altogether, it would become increasingly difficult to onboard new members who’d need to Fuse QSR in order to make any transactions during high usage. And to Fuse QSR they’d still need to make at least 2 transactions with PoW first.

[0x3639](https://forum.hypercore.one/u/0x3639) May 17, 2023, 5:43pm  6

Here are some posts from Kaine that might be helpful.

[sumamu](https://forum.hypercore.one/u/sumamu) May 17, 2023, 5:46pm  7

Made an attempt at completing the initial instructions provided by Mr. Kaine.  
The result makes sense and provides an easy and efficient direction for implementation of dynamic plasma:

1.  \[When producing a momentum, pillars should\] **order txs sorted** \[descending\] **by** \[the amount of\] **plasma** \[used. So that transactions with higher plasma are included first. If the maximum amount of transactions that can be included in the produced momentum is reached, the remaining transactions should remain in the mempool until eventually they are able to be included in a momentum, which would happen when the network usage lowers.\]
    
2.  **replace the PoW algo with RandomX** \[which is ASIC-resistant, in order to prevent the network from being spammed by an actor with access to an ASIC\]
    
3.  **find a way to balance PoW and QSR fusing** \[so both can be used when creating transactions in order to maintain the feeless properties of the network\]
    

0x provided some responses already.

Why a per momentum cap?  
Network growth needs to be bounded to ensure accessibility of full nodes / decentralization. Plasma is a measure of computational resource utilization. A consistent load is efficient and ensures nodes won’t crash. Technology improves over time so we probably can account for that by making the cap subject to governance. Long term some sort of benchmark oracle to target a certain level of consumer hardware.

The plasma cap already exists. Your account gets plasma based on QSR fused. Fusing anymore than 5000 QSR doesn’t do anything. All of the plasma associated with a tx is returned once the tx is confirmed.

Sentinels have been described as the public backbone of the network creating pow links and acting as oracles. Sentinels creating pow links have been described since the whitepaper. Incentivizing pow links incentivizes running a public node which is necessary for tx relay and IBD. It requires some thought to understand why.

Requiring the first tx be a receive on any account chain is not a good idea. Privacy is a big part of the appeal of PoW. Single use addresses have a role. And getting initial funds from an embedded contract, e.g htlc/ptlc require a contract send to start.

Who/what is going to set the pow → plasma rate?  
A centralized admin? It should be algorithmic.  
And again hardware gets better over time.

[sumamu](https://forum.hypercore.one/u/sumamu) May 18, 2023, 6:39am  9

It’s those responses that I’ve used to write my last message:

Does what I’ve described seem right to you?

What would stop us from adjusting this limit?

You’re right.

Is it because being a public node allows (for example) embedded nodes to connect to them → and when a user sends a transaction they would be first to see that new transaction, → then add a PoW-link to that transaction in order to prove they’ve seen it first → and later on get rewarded based on the amount of PoW they contributed to the chain?

Like you said, `It should be algorithmic.`

Not necessarily from the start, we could hardcode a rate after running some benchmarks.

Plasma requirements will be higher when the network usage will be higher, so more PoW will also be required.

Once there’s need for an algorithmically adjusted PoW to Plasma rate, it will be implemented.

Yeah your description is good.

The 5000 QSR is a hardcoded limit. There’s nothing stopping us from changing it.  
But without a max, it means that people with the most QSR can be guaranteed throughput in every momentum, possibly crowding out everyone else

For the PoW links, yes ![Image 208: :slight_smile:](https://forum.hypercore.one/images/emoji/twitter/slight_smile.png?v=12)  
Both the “pow” and the “link” part are very important.  
We will have a minimum number of links required, e.g 3

As you said, it means that they will be the public backbone to try to and make themselves available for ephemeral clients such as embedded nodes to be the first to receive a tx

But also because of the minimum links, after they make a pow link on a tx, they are incentived to quickly send it to all other public nodes in the network  
(this is critical once the network implements virtual voting)

ephemeral nodes are likely to send their initiated txs to all their peers  
the pow is important because creates a criteria for double spend filtering and also it prevents sentinels from hoarding txs  
if someone owns multiple sentinels and a pillar, without pow they are incentivized to hoard txs they see first, do all the pow links quickly internally, and then send it to their pillar if it has an upcoming momentum  
with pow, that person’s pow likely can’t compete with the pow of the entire network working on those txs  
the best chance to get your pow links confirmed, is by sending it to everyone

[sumamu](https://forum.hypercore.one/u/sumamu) May 18, 2023, 11:28am  11

I’m now starting to understand that we’re talking about different stages of the dynamic plasma mechanism.

You’re already thinking and planning for the version of dynamic plasma that accounts for the innovations in the whitepaper.

On the other hand, I’m considering the first steps we need take in that direction with an emphasis on moving away from the current state.

Current stateThe state in which a rather small amount of spamming could potentially hinder network transactions.

Short-term improvements keep us afloat and the long-term vision moves us forward.

[sumamu](https://forum.hypercore.one/u/sumamu) May 20, 2023, 9:15am  12

Putting upper limits on anything plasma-related won’t work. It’d be like if Satoshi decided to put a cap on Bitcoin’s difficulty or on transaction fees to avoid crowding out everyone else.

We’re going to have to choose between the risk of potentially hindering the network due to either high “difficulty” or high spam.

Transaction ordering in momentums shouldn’t necessarily be enforced. The general algo will sort them descending by the amount of plasma included, but if pillars decided to alter the algo and sort transactions in their produced momentums some other way, they could.  
If this were the case, pillars might employ some other ways for prioritizing transactions, like prioritizing transactions for their delegators.

There is a fundamental difference between PoW and QSR  
PoW is an open system, PoS is not. One can bring additional external resources to compete for PoW.

In our current structure, it is impossible to enforce priority by plasma.  
In the future, when we move to virtual voting, it will be enforced.

[0x3639](https://forum.hypercore.one/u/0x3639)

May 22, 2023, 10:53am  14

I’m posting this here for my own notes.

[![Image 209: Screenshot 2023-05-22 at 5.52.40 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/72bb930fcbb91f421297edc6b968d5b3bfd392b3_2_690x315.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/72bb930fcbb91f421297edc6b968d5b3bfd392b3.png "Screenshot 2023-05-22 at 5.52.40 AM")

[![Image 210: Screenshot 2023-05-22 at 5.59.05 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/e970cc1cf60639e3f949c49e91dbf58fe42342c5_2_690x178.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/e970cc1cf60639e3f949c49e91dbf58fe42342c5.png "Screenshot 2023-05-22 at 5.59.05 AM")

[sumamu](https://forum.hypercore.one/u/sumamu) May 22, 2023, 10:57am  15

So there should be upper limits for plasma coming from either QSR fusing/PoW?

My thoughts exactly.

Indeed, the majority will need to order the transactions in the same way so they’ll have the same hash to vote on.

[0x3639](https://forum.hypercore.one/u/0x3639)

May 22, 2023, 2:37pm  16

Sharing link here written by [@CryptoFish](https://forum.hypercore.one/u/cryptofish) regarding the current implementation of PoW and Plasma. I will try to understand this.

[@georgezgeorgez](https://forum.hypercore.one/u/georgezgeorgez) [@sumamu](https://forum.hypercore.one/u/sumamu) [@0x3639](https://forum.hypercore.one/u/0x3639) let’s focus again on Dynamic Plasma. I’m already working on the extension chain and we’ll need a higher network throughput. At least we should remove the hardcoded cap.

[Bzed](https://forum.hypercore.one/u/Bzed) June 25, 2023, 8:17pm  18

What needs to change with the structure to make priority by plasma realistic? Or are you just sort of conceding that this upgrade will be a significant change to the network?

[0x3639](https://forum.hypercore.one/u/0x3639) June 27, 2023, 12:09am  19

[@georgezgeorgez](https://forum.hypercore.one/u/georgezgeorgez) what would happen if we simply remove the cap with no additional changes? I assume it would not be a problem until we test the upper limits of the network… And then TXs would queue up and wait.

[@aliencoder](https://forum.hypercore.one/u/aliencoder) I read you are targeting Q2 / Q3 for the sidechain. Is it safe to assume you would prefer dynamic plasma to be in place by Sept 2023?

I don’t think that’s a good idea. It is not so simple.  
We need dynamic plasma for sure.  
But I also don’t see a hard dependency on it for extension chains.

Yes. I’ll coordinate with you and help you get it done.

I agree. Anyway the `ext-chain` will be on devnet/testnet first.

[sumamu](https://forum.hypercore.one/u/sumamu) July 14, 2023, 4:56pm  22

How can I help with this?

For the dynamic plasma implementation we’ll need a fairly good ASIC-resistant algorithm. Afaik MrK proposed [RandomX](https://github.com/tevador/RandomX) - Proof of work algorithm based on random code execution.

I’ve done some research and arrived to the same conclusion: RandomX is the best option. I’ve also found a project that offers a [Dart wrapper](https://github.com/gmpassos/dart_randomx) for it. I think it’s mandatory to have full support for every client from day 1.

[0x3639](https://forum.hypercore.one/u/0x3639) August 2, 2023, 6:32pm  24

I used RandomX for a year to CPU mine some shitcoins. During that time I never had any issues with it.

[Stark](https://forum.hypercore.one/u/Stark) August 5, 2023, 10:53am  25

I’m out of my depth here, but these comments made me wonder if the rate should be related to bitcoin as an external reference point, in some way.

[Chadass](https://forum.hypercore.one/u/Chadass) August 5, 2023, 1:16pm  26

Isn’t the dynamic plasma made in order to avoid the network to clog by making computationally expensive transactions more plasma demanding than simpler ones? If that’s the case I don’t see why you would need to relate to Bitcoin or an admin in any way. It’s just a layer of adjustable difficulty with two markets: electricity and QSR.

[0x3639](https://forum.hypercore.one/u/0x3639) September 22, 2023, 4:30pm  27

In the Dev Meeting #2 today, [@MoonBaze](https://forum.hypercore.one/u/moonbaze) proposed a solution to Dynamic Plasma. I will paste his ideas below. You can see the conversation starting [here on Discord](https://discord.com/channels/920058192560533504/1150019456718876843/1154757664635629619).

> After thinking about it for a while, the question “How can we implement an anti spam mechanism?” transformed to “How can we make sure that a regular user can still make a transaction if the network is spammed?”. Implementation options that I considered were:
> 
> 1.  Charging a fee for opening an account (so an attacker could not generate new addresses and spam from them). Every account would have a number of free (plasma / pow) transactions an epoch and after that they would have to pay for something like a slot of 200 (e.g) txs. So if someone wants to spam the network it would cost them.  
>     Cons: hard to implement, exchanges would have to pay, making it harder to integrate
>     
> 2.  Changing the PoW algorithm with something like RandomX which is harder to brute force and sorting txs by their pow, but someone with some rented hardware could still keep the PoW to a level that is hard enough for a regular user, even half an hour of something makes the network unusable.  
>     \[7:35 AM\]
>     
> 3.  Making the network feelessless . Removing plasma and pow, we would have something like ethereum but maybe qsr will decrease in value, we already are a feeless transaction.
>     
> 4.  Having 3 as a seed, (this one I like the most and I already started playing with it), we could introduce optional fees. Think of a congested network with PoW / Plasma transactions by a malitios actor, one could send a transaction with some fee and have higher priority than him. The algorithm of sorting transcations in a momentum could have the following priority: embedded send, embedded receive, txs with fees, txs with total plasam, hash. In regular conditions no one has to pay but in a congested network you could and the attacker would just waste his resources. The fee level must be chosen to a level that if the attacker wants to spam the network with fees transactions it would still cost him (something like 200 base fee level will cost 1 znn)
>     
> 
> What do you think? I already have implemented these fees and increased momentum by accountBlock sizes rathed than lenght. I tested with 1600 accBlocks per momentum already.

[0x3639](https://forum.hypercore.one/u/0x3639) September 22, 2023, 4:31pm  28

Please, before anyone responds to this proposal, please read the entire [discussion here](https://discord.com/channels/920058192560533504/1150019456718876843/1154757664635629619). We had an informative discussion and that will help the community understand the issues.

[0x3639](https://forum.hypercore.one/u/0x3639) September 22, 2023, 4:42pm  29

The idea of introducing a fee seems like an interesting solution to overcome 100% network utilization. Over time the network could migrate to a fee model if block space is fully utilized like other chains. Is that good or bad?

My question is, does the original network architecture contemplate a transition like this. QSR was designed to launch Pillars and process TX. If QSR stops becoming fuel for the network, what does that do to the usefulness and value of QSR? It will change the dynamics of QSR in our network. We need to fully understand that impact.

Also, if we design a system with a fee but allow PoW / QSR to overcome the fee we now need to design a system that takes into account 3 variables: fee, PoW and Plasma.

In a separate conversation, [@georgezgeorgez](https://forum.hypercore.one/u/georgezgeorgez) threw out the idea of using a fixed allocation for PoW. For example, 25%. So PoW would consume no more than 25% of network utilization (or block space?) and Plasma 75%. I’m regurgitating that idea to start the conversation here.

[coinselor](https://forum.hypercore.one/u/coinselor) September 22, 2023, 5:00pm  30

> MoonBaze: I have read some of the ideas on the forum, using a plasma cap or something similar would just not work. An attacker would outPoW a regular user

I’d like to second bzed’s petition for a more granular and in-depth explanation of what you see as the shortcomings of the PoW+Plasma anti-spam mechanism envisioned by founding developers. Some of us can’t really offer implementation/technical solutions of workarounds for any specific problem, but we can certainly help play the role of a malicious actor / regular user and brainstorm alternative solutions not considered or fully explored.

Here are some thought-provoking arguments:

**Attack Cost**

From what I was able to understand, one of MoonBaze’s recurring arguments was making sure an attacker/spammer would suffer an economic loss. In a feeless network, where transactions only require a dynamic amount of PoW or Plasma, both have a cost associated to them. PoW = electricity for sha256 / computational resources for RandomX. Plasma, although reimbursed at a later point in the future, also has a significant cost. An attacker would need to buy QSR, and freeze the capital in order to generate Plasma. This is a significant cost that cannot be understimated at the scale of clogging the network. QSR is a volatile asset and it will be locked for a minimum period of time we can control, the price when the attacker is done spamming might have changed significantly, especially if he successfully breaks the network.

Additionally, there are other variables we can consider to deter a malicious actor, for instance:

*   QSR Min Lock-up time
*   accountBlock age / trust score (an account that has been a network participant for longer might require less resources to get a transaction through the mempool i.e good aliens get fast lane subscription)

Finally, I would like to mention that the goal is not to prevent network congestion but deterring a malicious actor from congesting the network.

[0x3639](https://forum.hypercore.one/u/0x3639) September 22, 2023, 5:26pm  31

I think one of his concerns was that it would be easy to spam the network with CPU / Plasma and overcome the ordering system we develop.

[Chadass](https://forum.hypercore.one/u/Chadass) September 22, 2023, 5:29pm  32

I don’t understand the need to have fee when the cost of sending a tx is here no matter the state of the network. What does it change ? If I want to attack a network with a dynamic plasma leveraging pow and QSR I rent pow ressources or and buy QSR. If you make it not feeless I buy enough to spam and that’s it. How it is economically harder to attack ? You don’t freeze you capital with QSR, you can dump it later and QSR price is relatively volatile, for now.

Beside the same argument can be directed toward the capital you’re trying to get your hand on through your attack: its price is unpredictable, especially if the attack is made public, and so the capacity of reimbursement of the electricity cost is a bet.

[coinselor](https://forum.hypercore.one/u/coinselor) September 22, 2023, 5:52pm  33

In my mind, CPU / PoW is just a fall-back mechanism so that new accounts don’t require to have fused Plasma in order to submit a transaction **under normal conditions of available block space.** If network is congested, PoW goes out the window as a meaningful way to transact on the network, plasma will be required.

As you said, all that matters in this situation, is the ordering system we develop. If I’m at account block 5k and you are a new account trying to spam the network and the Blockspace plasma threshold (gas price) to include a transaction in the block is 100 plasma. We will both submit a transaction with 100 plasma fused in, yet mine could be seen by the network as superior, let’s say by multiplying my account block with the fused plasma, effectively making my transaction have 500K fused plasma. Good luck matching that as an attacker.

This is just a crude idea, but we have options. That’s my point. QSR/Plasma is not a freebie resource.

[coinselor](https://forum.hypercore.one/u/coinselor) September 22, 2023, 6:02pm  34

The times I’ve fused QSR, it locks the QSR for a min amount of time. Granted, a malicious actor could prepare an attack by fusing the QSR, then just waiting out the min lock time before unleashing the attack, but at least we’ll see it coming with on-chain analysis ![Image 211: :joy:](https://forum.hypercore.one/images/emoji/twitter/joy.png?v=12)

[Chadass](https://forum.hypercore.one/u/Chadass) September 22, 2023, 7:27pm  35

Hard to say. A malicious actor could accumulate over weeks or even months and only fuse at random times and random amounts.

My point is that anything can be attacked but you got one too with the 500k plasma exemple.

“QSR/Plasma is not a freebie resource.” and as I said before, feeless is a marketing narrative. We already have fee.

[0x3639](https://forum.hypercore.one/u/0x3639) September 22, 2023, 8:08pm  36

Going over Moons comments from today.

> The thing is that not all account blocks use that much Data so we could use the remaining space to insert other account blocks. Rather than capping the momentum by 100 acc blocks, no matter the size, we could cap it by the maximum size a momentum has now 100 \* (440 + 16384) / 440 ( size of a regular send block) could take us up to ~3800 regular send / receive account blocks per momentum

If someone wanted to spam the network with 3800 send/receive TXs constantly and each address had 100QSR that’s 380,000. That’s not much to fill the network. And if someone has 2m QSR to fuck with us they could allocated 526 qsr per address. That is an annoyingly large amount. that means users would need to fuse more then 526 to process a transaction.

But to Georges point, if we are successful forget spam, that will be the network usage. Blocks will be full. under this scenario, how do your get your TX processed if you don’t have 526 qsr?

[0x3639](https://forum.hypercore.one/u/0x3639) September 22, 2023, 8:14pm  37

Maybe TXs should be allocated a time of waiting. Sort of like a QSR multiplier. The longer a TX waits, the plasma multiplier goes up. That way if all TXs have 500 fused, someone trying to process a TX with 200 fused will eventually get processed.

[Chadass](https://forum.hypercore.one/u/Chadass) September 22, 2023, 8:18pm  38

That looks elegant

[0x3639](https://forum.hypercore.one/u/0x3639) September 22, 2023, 9:09pm  39

From chatGPT

**Proposed System for Transaction Processing on Zenon Network:**

1.  **Priority Queue:** Implement a priority queue for transactions. Transactions with higher PoW or more fused QSR get higher priority.
2.  **Dynamic Thresholding:** Set a dynamic threshold for PoW and QSR based on network usage. When network usage is high, increase the threshold, ensuring only high PoW or fused QSR transactions are processed.
3.  **Hybrid Processing:** For transactions that don’t meet the high threshold of PoW or fused QSR, allow them to combine both. For instance, a transaction with moderate PoW can be boosted with some QSR fusion to meet the threshold.
4.  **Fallback Mechanism:** In extreme network congestion, allow a fallback mechanism where a certain percentage of transactions are processed based purely on first-come-first-serve, ensuring that all users have a chance for their transactions to be processed.
5.  **Feedback Loop:** Continuously monitor the network and adjust the thresholds based on feedback. If transactions are getting delayed or the network is not congested, lower the thresholds.
6.  **Client-Side Processing:** Encourage clients to perform PoW or fuse QSR before sending transactions, especially during high network usage times. Provide clear guidelines and tools for clients to estimate the required PoW or QSR for quick transaction processing.

This system ensures that transactions with higher PoW or fused QSR are processed faster, maintaining the integrity and efficiency of the Zenon Network, especially during high usage times.

[0x3639](https://forum.hypercore.one/u/0x3639) September 22, 2023, 9:13pm  40

```
from queue import PriorityQueue

class Transaction:
    def __init__(self, pow_value, qsr_fused):
        self.pow_value = pow_value
        self.qsr_fused = qsr_fused

    def __lt__(self, other):
        return (self.pow_value + self.qsr_fused) > (other.pow_value + other.qsr_fused)

class ZenonNetwork:
    def __init__(self):
        self.transaction_queue = PriorityQueue()
        self.POW_THRESHOLD = 10  # Initial threshold for PoW
        self.QSR_THRESHOLD = 10  # Initial threshold for QSR fused

    def adjust_thresholds(self, network_usage):
        if network_usage > 80:  # High network usage
            self.POW_THRESHOLD += 5
            self.QSR_THRESHOLD += 5
        elif network_usage < 30:  # Low network usage
            self.POW_THRESHOLD -= 5
            self.QSR_THRESHOLD -= 5

    def add_transaction(self, transaction):
        if transaction.pow_value >= self.POW_THRESHOLD or transaction.qsr_fused >= self.QSR_THRESHOLD:
            self.transaction_queue.put(transaction)
        elif transaction.pow_value + transaction.qsr_fused >= self.POW_THRESHOLD:
            self.transaction_queue.put(transaction)

    def process_transaction(self):
        if not self.transaction_queue.empty():
            return self.transaction_queue.get()
        else:
            return None

    def fallback_mechanism(self, transaction_list):
        # Process a percentage of transactions based on first-come-first-serve
        percentage_to_process = 0.1  # 10% as an example
        num_to_process = int(len(transaction_list) * percentage_to_process)
        for i in range(num_to_process):
            self.transaction_queue.put(transaction_list[i])

    def client_side_processing(self, transaction):
        # Encourage clients to perform PoW or fuse QSR
        if transaction.pow_value < self.POW_THRESHOLD and transaction.qsr_fused < self.QSR_THRESHOLD:
            print("Consider increasing PoW or fusing more QSR for faster processing.")
        else:
            self.add_transaction(transaction)

```

[0x3639](https://forum.hypercore.one/u/0x3639) September 22, 2023, 9:20pm  41

> Dynamic plasma development stages:  
> 1 order txs (sorted by plasma)  
> 2 replace the current PoW with RandomX  
> 3 find a way to balance PoW and QSR fusing  
> Source: [Telegram: Contact @zenonnetwork](https://t.me/zenonnetwork/275773)

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 22, 2023, 9:47pm  42

The thing with any dynamic plasma + any PoW algorithm is that an adversary will always be able to accumulate some QSR for fuse and also very performant hardware to compute some hashes until the nonce is found. We must have the assumptions that the attacker could even be state level at some point and could have an insane amount of money and resources. Imagine we are in full bull market and someone spams the network, because they have a short or for every other reason, ( if we have fees it would be in our interest because they would buy a lot of ZNN to spam with fees ) then it would be unusable, just like it happened to Solana a lot of times. Even renting some CPU / GPU / ASIC for like 10k$ / month would be able to PoW to fill al the account block slots in a momentum and it’s not even that much money for an attack that lasts a month.

Adding this feature of optional fees would render this attack useless as any user could pay the base fee and frontrun the pow/fuse txs. As I said earlier, if the spam attack is with fees, it’s in our interest because they have to buy znn and they also burn them which creates deflation. As george pointed out, in a fully usable network, it could reach a point where anyone just pays the fee to be first. I don’t see a problem having fees here as it is much easier for a user to do something in order to be included. If the algorithm still required pow / plasma in that situation the user would have 2 options: 1) buy QSR (how? the network is congested) and he would have to fuse some more (how? the network is congested) 2) acquire some more processing power so one could compute the required PoW ( users just want to click and get it done, no one has time to do such things for a tx). Both options really seem impractical.

One could say, in order to pay fees you have to receive ZNN first and he would be correct but in practice not many actions happen on accounts with 0 ZNN, it’s only one receive rather than receive QSR and fuse QSR. Maybe we could create a feature so that the sender could pay the fee for the receiver and this issue is solved ( another option here would be to give receive blocks higher priority than sends but this creates an attack vector, I could explain in detail later).  
Whether or not we become a network where all the users pay the fee for a tx it’s for the free market to decide. Personally I don’t think it would happend so often and even so, I don’t consider it is a bad thing.

Later edit: Think about the Bitcoin network with block mining and us having a PoW mechanism for txs. A regular user would have to race against all the processing power of the attacker. The point at which the waiting time would increase it’s up to the attacker’s money / resources. If we cap the time (like btc 10 min) it’s even worse as it gets easier for the attacker. He could maintain even an waiting time of 1 hour. It’s still a lot (now could be ok, because nothing happens but I don’t want this in the next bull). Fees fix this. Let him use 5 ZNN as fees for all the txs. I don’t mind

[coinselor](https://forum.hypercore.one/u/coinselor) September 22, 2023, 11:11pm  43

Thanks for the in-depth reply. I clearly see how a fee directly prevents an attack in the first place, as the malicious actor would consider the associated costs of the attack.

I just want to point out that we also have other tools at our disposal that Bitcoin and other networks don’t have. Namely, the governance module + AZ. Consider the points brought up by ChatGPT, particularly Dynamic Thresholding, Fallback Mechanism, Feedback loop, heck even Hybrid processing sounds like a good idea. George has brought up multiple times the idea of the network being able to edit variables through the governance module. Could we use this to our advantage by allowing us to change the “rules” of the game to mitigate an attack vector?

The best defense is not a solid codebase with no exploits/bugs, but our ability to remain flexible/agile to patch them and pivot while maintaining our Decentralization ethos. It has luckily worked out for Bitcoin so far, being a robust codebase that is very hard to change. But what would happen if someone cracks it? We’ll see Bitcoin 2.0 and it will be messy. I think we have better tooling than Bitcoin to remedy a crisis of that magnitude.

Imagine a situation where someone is attacking the network, make it state level if you want, North Korea wants aliens to stop transacting. They have unlimited resources and are smart, accumulated QSR for years (benefitting us temporarily. Again, QSR is not a freebie) and have unlimited hashing power. The attack commences, network is instantly congested, aliens panic, Zenonhub’s anti-spam bot detector goes off. Pillar submits a governance proposal to immediately ban offending addresses from the network. Even dormant pillars instantly vote yes. It’s a spork type emergency, so it activates in 24 hours instead of 2 weeks. How you ask? I have no clue, but maybe George added some extra fields in the governance schema to do just that. Instantly accounts are banned from the network and not allowed to even dump their QSR because nodes will not process the transactions from the blacklist.

Perhaps a little of a crazy idea and even completely stupid or impossible, but again, my goal here is to help us think outside the box. QSR is not a freebie. Slash his ass for spamming our network with plasma. And make plasma the determining transaction ordering factor over PoW if it’s already not the case, as technically it should be easier (and less benefitting to us) for an offender to rent hashing power than to buy QSR.

Edit: All of this relies on us being able to identify malicious activity. If that’s not a possibility, my whole premise falls apart.

> georgezgeorgez —  
> There is no difference between an attacker and a normal user  
> From the perspective of the network

The network doesn’t know that it’s an attack, but will the humans behind the pillars be able to tell the difference?

[Chadass](https://forum.hypercore.one/u/Chadass) September 22, 2023, 11:43pm  44

What you state is true for every crypto: with enough money one could attack Bitcoin, Ethereum, anything.

[sugoibtc](https://forum.hypercore.one/u/sugoibtc) September 23, 2023, 1:57am  45

I like the fact of bringing in fees if you compare it to the BTC mempool. In the last couple of months we’ve experienced a significant rise in the use of blockspace and the increase in fees paid to be included in a block, mainly because of Ordinals. Even when increasing the fee, the network still depends on the settlement time of a new block.

A fast lane would ensure the user to be included, and just as in Web2 time equals money. I think we’re heading in the right direction if we’re going to discuss the option to include fees through a ZNN burn (maybe donate to the A-Z fund or simply burn the supply) in order to further utilize the network in case of a bull market and/or successful product.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 23, 2023, 6:16am  46

I really appreciate the interest to find a solution.

> Dynamic Thresholding, Fallback Mechanism, Feedback loop, heck even Hybrid processing sounds like a good idea. George has brought up multiple times the idea of the network being able to edit variables through the governance module

*   Dynamic Thresholding I said in my latest message why this won’t work
    
*   Fallback Mechanism, Feedback loop, heck even Hybrid processing these would require some determnistic processing which would make the attacker know what tx is going to be accepted based on some on chain seed. Randomness on chain is very hard to achieve
    

> The best defense is not a solid codebase with no exploits/bugs, but our ability to remain flexible/agile to patch them and pivot while maintaining our Decentralization ethos.

This is very wrong in my opinion, the best defense are both. When they are building a huge tower they are not like “it doesn’t matter if it’s sketchy, we have the fire department nearby to intervene when it falls”

> But what would happen if someone cracks it?

I don’t think that introducing a very powerful mechanism that would allow an user to send a tx even though the network is spammed cracks a network

> Zenonhub’s anti-spam bot detector goes off. Pillar submits a governance proposal to immediately ban offending addresses from the network. Even dormant pillars instantly vote yes. It’s a spork type emergency, so it activates in 24 hours instead of 2 weeks

This is slashing / blacklisting which just won’t work because we have the freedom to create millions of addresses

> There is no difference between an attacker and a normal user  
> From the perspective of the network

> The network doesn’t know that it’s an attack, but will the humans behind the pillars be able to tell the difference?

That’s why this optional fees solution doesn’t care. It lets the regular user decide what to do in case of a spamming attack, not the network, not the pillars nor the governance module.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 23, 2023, 6:22am  47

This is not true for every crypto. I don’t think anyone can out hash all bitcoin miners. We are talking about spamming attacks. They have no mechanism against it but no one does it because it costs the fees.

[0x3639](https://forum.hypercore.one/u/0x3639)

September 23, 2023, 10:45am  48

I was going back through TG looking at some of the guidance Kaine gave us.

From the beginning the core devs designed a network that is “feeless”. Kaine believes the architecture balances security, scalability and decentralization.

[![Image 212: Screenshot 2023-09-23 at 5.13.02 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/51714a8e89c28b52817a16995c4d6031ecfe328f_2_690x133.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/51714a8e89c28b52817a16995c4d6031ecfe328f.png "Screenshot 2023-09-23 at 5.13.02 AM")

He also said:

[![Image 213: Screenshot 2023-09-23 at 5.11.14 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/28e04f02a65ee52a03bd9688defb25826bba9bff_2_690x397.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/28e04f02a65ee52a03bd9688defb25826bba9bff.png "Screenshot 2023-09-23 at 5.11.14 AM")

I can perfectly understand how a fee will resolve the issue of sustained attack. But I cannot help but think adding a fee will disrupt the architecture of the network. The value / utility of QSR is to launch Pillars and process transactions. If we are under attack or the network is fully utilized, users will pay a fee and the utility of QSR will change. What does that do to the architecture?

Kaine references a difficulty adjustment mechanism like BTC. He also references ordering TXs by plasma and balancing PoW and QSR fusing. I cannot find anywhere where he references fees. But I just view this as guidance, not direction.

[![Image 214: Screenshot 2023-09-23 at 5.16.30 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/5a7c8b67b6a9792ae1977160478e7d31bd2b05ad_2_690x150.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/5a7c8b67b6a9792ae1977160478e7d31bd2b05ad.png "Screenshot 2023-09-23 at 5.16.30 AM")

Why not create a system of lanes?

Lane 1 = PoW  
Lane 2 = QSR Fused  
Lane 3 = Fast lane

The width of the lanes can adjust, like the BTC difficulty adjustment. The sum of the width of lanes = total throughput.

During low bandwidth, lanes adjust so that all throughput is utilized - meaning if the PoW lane is full (congested) but the QSR lane is not, the QSR lane gets narrower and the PoW lane gets wider. This happens until both lanes are full.

By changing to RandomX, it could be harder and irritating to attack the network b/ you need a bunch of CPUs. And you cannot point ASICs at it.

When both lanes are full and TXs are getting delayed I think we have a few options:

1.  Add PoW + Fused QSR to determine order - meaning a user can do both
2.  Add a time based multiplier to the PoW + Fused QSR weight. The longer someone waits, the larger the multiplier becomes. Meaning if I fuse 100QSR at Time1 and you fuse 200QSR at Time5 eventually my 100QSR weight will be larger than the 200QSR weight and the TX will get processed.

By adding a time multiplier to the fuse / pow weight eventually the TXs will get processed. TXs will get processed even if under attack or network utilization is full.

Do we need a fee if we can design the system to process all TXs? Will someone spam the network endlessly for no benefit knowing all TXs will get processed. Maybe the fast lane is based on fused QSR - some larger amount. So if you fuse X QSR you are put into the fast lane automatically and have access to first come first serve. The width of the fast lane adjusts with the balancing algo so lane width of fast / QSR / PoW all move together.

Believe it or not, chatGPT is pretty good at helping think through some of these issues.

[Chadass](https://forum.hypercore.one/u/Chadass) September 23, 2023, 2:29pm  49

I read a lot about fast lane but it mostly look like a bumped fee level. What stop an attacker to pay millions and spam the fast lane ? A highway can be crowded.

[Chadass](https://forum.hypercore.one/u/Chadass) September 23, 2023, 3:07pm  50

The most elegant option I’ve seen so far is adding a T variable so a user’s tx plasma weight increases with time no matter what the network state is and will be confirmed at some point.

The fast lane idea is just a fee market and fee markets can be congested and push regular users out. Do we want to offer yet another L1 where in case of success we all rush the fast lane for a 10$ per tx because even there it’s congested? Moonbaze assuming a user wouldn’t just sit and wait for 1 or 2 minutes for a tx to confirm is just what it is: an assumption.

[Chadass](https://forum.hypercore.one/u/Chadass) September 23, 2023, 3:08pm  51

Every kind of attack has a cost. Adding another layer of fee and branding it as fast lane just move the cost elsewhere and does not seem to solve much.

[Bzed](https://forum.hypercore.one/u/Bzed) September 23, 2023, 11:00pm  52

Im not seeing where we do need to add the third lane using fees. Aquiring QSR or dedicated hardware is a real cost and in a dynamic system that can raise/lower the required Plasma and/or PoW over time based on usage, it would add up to be a significant one.

Then the ability to balance between the two lanes and some sort of time weighted multiplier to push txs thru should give the flexibility to maintain a usable network during high usage or coordinated spam.

How does networks like visa and MasterCard deal with spamming?

[Shazz](https://forum.hypercore.one/u/Shazz) September 24, 2023, 7:31pm  54

Acquirer networks and merchant accreditation

[0x3639](https://forum.hypercore.one/u/0x3639) September 24, 2023, 7:45pm  55

Ya, users cannot spam. they will be blocked immediately and removed from the network.

[0x3639](https://forum.hypercore.one/u/0x3639)

September 25, 2023, 10:02am  56

Dust attack on KAS. Their fees are very low. Apparently it’s costing a few cents a day to attack the network causing hard drive usage to grow quickly.

[![Image 215: Screenshot 2023-09-25 at 5.00.42 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/f25a1728b79bb3c44380dd941f8c8f3d47d3c874_2_690x409.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/f25a1728b79bb3c44380dd941f8c8f3d47d3c874.png "Screenshot 2023-09-25 at 5.00.42 AM")

[0x3639](https://forum.hypercore.one/u/0x3639) September 25, 2023, 10:36am  57

Here is their solution

> The basic idea is to require that transactions charge fees if they have “excess” outputs: if a transaction has k inputs and n outputs where n\>k, it must pay a fee of n-k kaspa. However, since typical transactions have one input and two outputs (due to the change address), applying this rule directly will greatly increase fees paid by ordinary users. We avoid this by allowing transactions with at most two excess outputs that are not paying the increased fees, but _only allowing one such transaction per block_ . To avoid a DoS attack where an adversary spams the network with such transactions, preventing honest transactions from being chosen, we always choose the transaction whose _latest_ input is the _earliest_ . Additionally, we still want to allow mining pools to pay block rewards to many users. We achieve this by exempting transactions from the increased fees if at least one of their inputs is a coinbase UTXO. A transaction that is currently accepted will be henceforth denied if the following three conditions hold
> 
> 1.  It has k inputs and n outputs, with n-k\>2
> 2.  The fee paid the transaction is less than n-k Kaspa
> 3.  None of the inputs to the transaction are coinbase UTXOs
> 
> In particular, any application that creates transaction of this form will have to either refactor the compounding of transactions or increase the fee.

[0x3639](https://forum.hypercore.one/u/0x3639) September 25, 2023, 11:38am  58

Reflecting on our convo in the dev meeting, how do we create a feeless ordering system that does not differentiate between spam and real traffic? We only consider valid transactions.

KAS is getting dust attacked for a few cents a day. Maybe the attackers are short KAS and want to crash the network. Who knows. Looks like KAS is preventing the attack by keeping fees low for one “honest” tx per block and they are processing txs on a first in first out order. They are on a utxo model so they are using the number of inputs vs outputs to help classify “honest” transactions. They seem to be removing miners from this classification. The network now charges larger fees to txs that don’t meet the “honest” category.

We face the same issue, only we have two ways to process txs (PoW and fused qsr). We are not utxo so we cannot track inputs vs outputs to classify “honest” transactions. Also, kas mentions the risk of running out of HD space to keep all the spam txs.

Ideas for NoM:

*   Can QSR fuse duration impact the ordering of txs? Meaning if you agree to fuse longer, does that increase the fuse weight?
*   Adjustable lane width for PoW / QSR will help prevent PoW overcoming the network, but that will not prevent a PoW attack from inundating PoW txs and slowing them way down.
*   first in first out weighting should help honest txs get processed.
*   can we implement a “fast lane” with higher fused QSR rather than paying a fee. This can be a governance variable set by voting.
*   Can we limit the PoW per tx so that each tx requires a CPU? This could make a PoW attack much harder. No idea if this is possible.

[vilkris](https://forum.hypercore.one/u/vilkris) September 25, 2023, 12:34pm  59

A problem that RandomX introduces is that it makes browser-only onboarding into zenon infeasible, since it’s not viable to compute RandomX in a browser environment: [RandomX/README.md at master · tevador/RandomX · GitHub](https://github.com/tevador/RandomX/blob/master/README.md#does-randomx-facilitate-botnetsmalware-mining-or-web-mining)

This means that any browser based wallet will need to have a dependency to an additional “pow-generator” program running locally, or external pow-as-a-service or plasma-as-a-service infrastructure, which can complicate the onboarding experience.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 25, 2023, 6:28pm  60

In the current architecture I don’t think that transaction PoW secures the block-lattice ledger by adding weight. It is used only if you don’t have enough plasma.

> What does that do to the architecture?

We will just have optional fees, nothing is changed.

> Lane 1 = PoW  
> Lane 2 = QSR Fused  
> Lane 3 = Fast lane

This priority changes nothing as the network can still be attacked by PoW.

> Add a time based multiplier to the PoW + Fused QSR weight. The longer someone waits, the larger the multiplier becomes. Meaning if I fuse 100QSR at Time1 and you fuse 200QSR at Time5 eventually my 100QSR weight will be larger than the 200QSR weight and the TX will get processed.

This actually creates an even easier attack vector. I can just spam the network with txs with a relatively low pasma / pow and in time they could all magnify. Basically we just add a delay.

I think chadass is just trolling.

We cannot have dust attack if we choose the base fee optimal. I though of 1 ZNN / 200. Which is 200 txs with base fee to reach 1 ZNN. If we also increase the capacity of momentums then it just won’t be feaseble economically. Or if they do it won’t last long and it will help all holders by buying a lot and burning a lot.

I think that we do not have the man power to build such a complex algorithm as dynamic pow that would work perfectly, having into consideration everything nor do we have the time / money until the next bull market. Optional fees is just easier and a more elegant solution to implement and I repeat, the problem it solves it’s not only “How to protect the network from spam attack” but also “How could a regular user use the network in case of a spam attack”.

[coinselor](https://forum.hypercore.one/u/coinselor) September 25, 2023, 6:37pm  61

Wouldn’t it make more sense to use QSR for the base fee?

Given QSR fuses into plasma which equates to feeless transactions, and there are other examples of networks with a dual coin structure where they have a dedicated token for gas payments, I believe it will be less confusing.

[Chadass](https://forum.hypercore.one/u/Chadass) September 25, 2023, 6:52pm  62

I find it ridiculous even from you to write that someone disagreeing with your lazy takes is “just trolling”

Maybe it you were here in the Twitter Space we could have had a discussion.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 25, 2023, 6:56pm  63

It would be an ideea for sure. I just think it would benefit the network more to burn ZNN

[0x3639](https://forum.hypercore.one/u/0x3639) September 25, 2023, 6:57pm  64

Was thinking the same.

Hard to argue with this.

To george’s point, when the network is fully utilized (lane 1 and 2 are full) won’t everyone just pay fees to process TXs?

I wonder if the fact a fee lane exists will help prevent attacks. [@MoonBaze](https://forum.hypercore.one/u/moonbaze) do you envision the widths of the lanes be adjustable?

Maybe [@MoonBaze](https://forum.hypercore.one/u/moonbaze)’s proposal is an interim step. And we can reconsider the algo in the future when utilization is higher and we have more market cap to throw at solving the problem.

[Chadass](https://forum.hypercore.one/u/Chadass) September 25, 2023, 6:59pm  65

I still fail to see how a fee introduction mitigate a spam attack VS the plasma / pow multi lanes solution.

[0x3639](https://forum.hypercore.one/u/0x3639) September 25, 2023, 7:00pm  66

I think he is saying it solves the problem by allowing TXs to get processed under heavy spam by simply paying a fee. So it will not prevent spam, but it will allow valid TXs to get processed by paying the fee.

[Chadass](https://forum.hypercore.one/u/Chadass) September 25, 2023, 7:11pm  67

Yes but this is litteraly allowing txs being processed for people generating more pow. The difference is that we would lose an interesting difference VS other L1.

In the context of a multi lanes solution, what about a lane only dedicated to fusing plasma? In case of network congestion users would still be able to fuse and get their txs processed. An attacker would then have to both spam and acquire a lot of QSR beforehand. This under attack situation could then be addressed through governance with lanes balancing parameters changes.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 25, 2023, 7:13pm  68

In case the attacker spams the network using fees, he **won’t be able to do it for long** as it would cost him a lot of ZNN, which is why I would choose it instead of QSR. He would have to buy which would help every holder and it will be burned which in my opinion is good mechanism to further help increasing scarcity and the price.  
In case the attacker spams with pow / fuse, every regular use can still use the network as normal

[0x3639](https://forum.hypercore.one/u/0x3639) September 25, 2023, 7:20pm  69

If the PoW lane is a fixed width, won’t that help against a PoW attack? The attacker consumes the entire PoW lane and honest users just use the QSR fused lane.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 25, 2023, 7:22pm  70

What do you mean by a fix laned width?

[0x3639](https://forum.hypercore.one/u/0x3639) September 25, 2023, 7:28pm  71

For example, if we can process 100 tps, we restrict the number of tps based on plasma type.

So the PoW “lane” can process 25 tps (for example) and the fused plasma lane can process 75 tps. We can set the width of the lane (how many tps) based on the imbedded governance module George is writing. that way if someone spams PoW they can only consume 25% of the available tps.

And we can manually change the lane width based on pillar vote.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 25, 2023, 7:35pm  72

I don’t think pillars would be online so often to vote. It is hard to access embedded storage from where the momentums are created. Ideas come but we should also think about implementation. Also, to acquire QSR is really cheap and will always be much cheaper. It seems like a trivial solution.

[Chadass](https://forum.hypercore.one/u/Chadass) September 25, 2023, 7:43pm  73

It’s the same for an attacker spamming with PoW. This has a cost. Beside it could be mitigated with what we mentioned before:

*   the lanes can algorithmically be adjusted with 10% allowed to the one being under attack.
*   the governance can then take action.
*   in case of an attack on both PoW lane and plasma lane then the special lane for fusing plasma can still allow users to transact.
*   the governance can jump in to address the situation at any time.

Thus without compromising the underlying design of the NoM with an easy intuitive decision that make little sense. Decision that would also come with a marketing cost.

It seems that everyone forgot how Ethereum behaves under high congestion. I used to pay $700 for a swap. It doesn’t seem like fee address anything when your network struggles anyway.

EDIT : the addition of a T (time) variable for each tx to weight more and more would help users to transact in case of high congestion, attack or not.

[0x3639](https://forum.hypercore.one/u/0x3639) September 25, 2023, 7:44pm  74

My guess is the lane widths will not be changed frequently. The idea is to limit the throughput of each lane, start with a number and change it infrequently if the initial number is not “good”.

If someone wanted to spam 1000 tps @ 100 qsr, they need 100,000 QSR. Then a QSR war would ensue. Users would need to increase fused QSR to overcome the spammer.

Maybe that means users need to fuse 1000 QSR for a period of time. The “fee” users pay would be in increased fused QSR. that market would then find a state of equilibrium over time. It will balance the desire to spam with process honest TXs.

[Chadass](https://forum.hypercore.one/u/Chadass) September 25, 2023, 7:46pm  75

(added T variable note as discussed in the Space)

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 25, 2023, 8:09pm  76

I still consider that PoW would be easier to mass produce despite the market value of ZNN / QSR and QSR will always be cheaper to acquire than ZNN. QSR is already burned for a pillar, locked for sentinel and used to send a transaction in normal conditions which will be like 99% of the time. ZNN deflation is a mechanism we don’t have and is useful. Right now we need an anti spam solution. We won’t have 700$ for a tx unless we have EVM on L1 which will not happen in minimum 2 years at the rate things happen here.

[0x3639](https://forum.hypercore.one/u/0x3639) September 25, 2023, 8:28pm  77

I’m open to all solutions. I’m just trying to understand all issue and get as much community participation as possible.

[Chadass](https://forum.hypercore.one/u/Chadass) September 25, 2023, 8:42pm  78

I still consider your solution is an easy fix that doesn’t fix anything. I’m open to solutions.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 25, 2023, 9:16pm  79

Can you bring some arguments? I could also say that when qsr is 5$ people have to fuse 500$ to send a tx.

[Chadass](https://forum.hypercore.one/u/Chadass) September 25, 2023, 9:17pm  80

I did, and not only me. Please read above. In the case you’re mentioning PoW is still a valid option and the lanes can then be balanced algorithmically or / and through governance in order to address the congestion.

Is QSR is $5 then the network is also stronger VS a possible attack on the plasma lane.

[coinselor](https://forum.hypercore.one/u/coinselor) September 25, 2023, 9:53pm  81

I’m perfectly fine with this compromise. In fact, if we learn from how other ecosystems evolve i.e Ethereum, we can comfortably say that whatever we end up implementing now will be disregarded and changed in the future as the technology matures and better solutions are found.

I think we can all appreciate the effort and understand that a perfect algorithm for transaction ordering that is battle-tested, peer-reviewed, with a solid game theory/economic foundation that will stand the test of time is probably unrealistic at this point.

That said, there are still a lot of other devs who have not voiced their opinions, so I’m very eagerly awaiting their take, as clearly the implementation of Moonbaze’s proposal or suggestions for adaptations to it’s proposed solution is what matters now.

[0x3639](https://forum.hypercore.one/u/0x3639)

September 26, 2023, 12:22am  82

summary of my thoughts:

1.  QSR is a utility token to launch pillars, sentinels and process transactions.
2.  QSR that is sitting idle (not burned for Pillar or staked for Sentinel) wants to be used. Either it can be fused for transactions or leased to others for transactions (a market that will form in the future). There is an opportunity cost to fusing QSR. A spammer will consider these costs when determining if they want to use QSR to spam the network. Will someone attack the network with fused QSR? Maybe, but there is a cost to that.
3.  Can someone attack the network with PoW? yes. How can we mitigate it? Can we establish the “lanes” at the block level? Can we limit TXs in the block / momentum based on PoW or QSR?
4.  I hate to bring up guidance from Kaine, but it’s hard to avoid. Given my lack of experience with protocol development I need to rely on what he has said in TG. If Kaine envisioned a fee to process TXs he would have mentioned them. Would the early devs have marketed the project as feeless if we planned to implement a fee in the future?

[![Image 216: Screenshot 2023-09-23 at 5.16.30 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/5a7c8b67b6a9792ae1977160478e7d31bd2b05ad_2_690x150.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/5a7c8b67b6a9792ae1977160478e7d31bd2b05ad.png "Screenshot 2023-09-23 at 5.16.30 AM")

5.  I can see how fees will help order congestion and provide a fast lane. That makes sense to me. It’s hard to ignore George’s guidance that in the future it will be hard to differentiate between spam and network usage. And if we have a fee lane, why won’t all TXs migrate to higher and higher fees?
6.  Do we think Kaine will issue a spork ID for fee lane given his guidance never mentioned a fee.
7.  How do PTLCs impact this discussion? Given this will increase privacy will it become harder to differentiate between spam and honest traffic? Won’t everything just move to valid TX or not?

If we can limit TX in a block based on PoW / QSR can’t we implement lanes? And if we believe there are opportunity costs to fuse QSR isn’t that the fee we are looking for?

[0x3639](https://forum.hypercore.one/u/0x3639) September 26, 2023, 12:51am  83

On a separate note, George pointed out that without Virtual Voting, there is nothing that requires the Pillars to follow the plasma ordering we are discussing. That lead me down the “Virtual Voting” rabbit hole in the whitepaper with ChatGPT. Here is what it says about our virtual voting.

> This is off topic and not relevant to the discussion about dynamic plasma.

[](https://forum.hypercore.one/t/dynamic-plasma-discussions/62/print#consensus-timeline-virtual-epochs-1)**Consensus Timeline & Virtual Epochs:**
-------------------------------------------------------------------------------------------------------------------------------------------------

The consensus timeline is divided into virtual epochs. Within each epoch, nodes process transactions and make decisions based on the total stake present during that epoch.

### [](https://forum.hypercore.one/t/dynamic-plasma-discussions/62/print#voting-mechanism-2)**Voting Mechanism:**

The node will broadcast its vote in the next epoch.

If a node knows the transactions between two epochs and applies a deterministic ordering algorithm, all remaining honest nodes will arrive at the same decision. After a node has a supermajority of messages with all transactions between two epochs, it starts to virtually vote on the ordering.

This virtual vote isn’t a traditional vote. Instead of sending additional network messages, it uses a set of rules that define a deterministic way to order the transactions. Factors used in ordering include the PoW link weight, the timestamp of transaction arrival, and the hash of the transaction as a tiebreaker.

Once a node orders the transactions, it knows that the order is the same for all nodes. Thus, it marks them in the ledger, assigning an ID to each transaction.

### [](https://forum.hypercore.one/t/dynamic-plasma-discussions/62/print#stake-based-voting-3)**Stake-Based Voting:**

In a decentralized environment, traditional quorum-based voting is vulnerable to Sybil attacks. To counteract this, nodes can lock a certain amount of stake to obtain different roles in the network, such as becoming sentinel or pillar nodes.

The virtual voting process is determined based on the total stake during a virtual epoch. Pillar nodes with stake make decisions within the consensus algorithm to finalize transactions. Nodes can unlock their stake at any time. However, consensus nodes have an “unstaking period” they must wait through.

[Chadass](https://forum.hypercore.one/u/Chadass) September 26, 2023, 12:06pm  84

Something we didn’t discuss (or I missed it) is the way the NoM architecture might or might not react as a blockchain in case of spam or congestion. I think Sol tried to spam the network once but I’m not sure we have any other metrics.

On a side note please be more careful with tools like ChatGPT, it’s not magical, and it hallucinates a lot, like a lot. It should only be used when people actually know the content that is sumarized or the subject they ask questions for, so they can check the facts by themselves.

[0x3639](https://forum.hypercore.one/u/0x3639) September 26, 2023, 12:47pm  85

I independently verified the general accuracy of that before posting it. I agree with your caution however. It does produce random and wrong results often.

[0x3639](https://forum.hypercore.one/u/0x3639) September 26, 2023, 3:22pm  86

I’ve been following the KAS dust attack. I think basically they are censoring TXs that have the footprint of spam. They seem to be successful so far. Someone claimed it was a miner looking for higher fees to mine blocks. They got censorship instead.

[Chadass](https://forum.hypercore.one/u/Chadass) September 26, 2023, 3:43pm  87

If you need to censor it looks like your system is not that good.

[0x3639](https://forum.hypercore.one/u/0x3639) September 26, 2023, 5:31pm  88

More ideas are coming to mind. I’m going to vomit them here.

BTC has a difficulty adjustment so blocks are processed every 10 minutes. THORChain has an incentive pendulum to balance (adjust) the amount of Bond a node earns vs the LP incentives. If there is too much node bond, node yield goes down and LP rewards go up. This reduced node bond and increases LP depth. If there is not enough node bond, node yield goes up and LP rewards go down. This increases node bond and decreases LP depth.

Why can’t we have a difficulty adjustment on PoW and QSR to balance the depth of the queue per lane. The goal is to balance the TX across the two lanes. For example:

*   if the PoW lane is congested with long wait times, lower the difficulty on the QSR lane and increase difficulty on PoW lane to incentivize traffic to the QSR lane.
*   if the PoW lane is wide open with short wait time and QSR is backed up, increase the difficulty on the QSR lane and lower difficulty on the PoW lane to incentivize traffic to move to PoW.

Individual sovereignty and censorship resistance of the network can co-exist.  
In a system where validators/miners have choice over which transactions to confirm, they will have the ability to censor.  
The question becomes are there enough competing interests in the network that are unable to collude to censor. That’s a big component of decentralization.  
And where censorship resistance would come from.

Other mechanisms like threshold encryption and virtual voting can greatly increase the censorship resistance of the network. But they remove aspects such as choice.

[0x3639](https://forum.hypercore.one/u/0x3639)

September 27, 2023, 12:14pm  90

Don’t forget about this post. It explains how PoW and Plasma work today.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 28, 2023, 12:06pm  91

We don’t know if Mr Kaine v2.0 is the real one. I would not trust a stranger so much. He didn’t even know that PoW does not secure the ledger. I think in the end we would all reach the same conclusion, optional fees is a good solution for today’s problem. In a couple of years if we grow bigger, we could update the model, with better solutions, if any.

[Chadass](https://forum.hypercore.one/u/Chadass) September 28, 2023, 12:08pm  92

This kind of speculation shouldn’t even be taken into consideration. It’s near complotism level. At this point, we don’t even know if Moonbaze is the real one.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 28, 2023, 12:24pm  93

Again, you are just trolling the conversation without offering something useful to reach consensus for what solution we should choose.  
Off topic: tell me what percentage to change for delegation and I can prove who I am.

[0x3639](https://forum.hypercore.one/u/0x3639) September 28, 2023, 1:06pm  94

When Kaine snapped back at the community a few months ago and started to talk a little trash, I renamed him (in my TG contacts) to v2.0. It’s possible the person behind that account changed, but it’s the same account that has been posting for years.

I agree that we need to do what is best for the network. I view the Kaine posts as important insight we should consider. Nothing more.

[0x3639](https://forum.hypercore.one/u/0x3639)

September 28, 2023, 2:13pm  95

For what it’s worth, the dust attack on $KAS is still happening.

[![Image 217: Screenshot 2023-09-28 at 9.13.07 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/e8ce9db6ec3dacf16c33e1c78af7de28ea9ebeb8_2_690x165.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/e8ce9db6ec3dacf16c33e1c78af7de28ea9ebeb8.png "Screenshot 2023-09-28 at 9.13.07 AM")

[0x3639](https://forum.hypercore.one/u/0x3639)

September 28, 2023, 2:16pm  96

Not sure if this is relevant to our discussion regarding plasma. Just wanted to share some of the consequences of this dust attack.

[![Image 218: Screenshot 2023-09-28 at 9.15.05 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/e6f8c39804675f64d7132b01b59b56371e4aedc6_2_690x199.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/e6f8c39804675f64d7132b01b59b56371e4aedc6.png "Screenshot 2023-09-28 at 9.15.05 AM")

[0x3639](https://forum.hypercore.one/u/0x3639) September 28, 2023, 3:05pm  97

Why can’t we implement a plasma pendulum that tries to balance PoW with QSR? We can limit PoW attacks by limiting the number of TXs per block that are based on PoW. And if we create an incentive mechanism to move TXs from PoW <\> QSR based on congestion, why can’t that work?

Also, I do think we need to consider the opportunity cost of fusing QSR as a fee. If a user wants to make sure a TX gets processed, fuse more QSR. Once a spammer’s PoW gets throttled, they will need to post a lot of QSR to spam the network and there is an opportunity cost of that.

[0x3639](https://forum.hypercore.one/u/0x3639) September 28, 2023, 6:57pm  98

I’m having a few offline conversations, and wanted to throw out this idea based on conversations w/ others.

Do we expect to onboard all new users to the L1? Is that a design objective? Kaine has told us for months / years that he wants to keep the L1 clean and minimal. I assume most user activity will happen on the side chain and/or L2. What will new users do on the L1? Stake, delegate, get rewards, launch sentinels, and eventually pillars. What else will new users do on the L1?

So if we assume most users will not need to interact with the L1 frequently how does that change our design decisions?

In order to Stake and Delegate do users need to interact with the L1? If PoW is under heavy load, how does a new user perform PoW to receive QSR? Can users do that from the side chain or L2? How can we insure new users can perform enough PoW to perform their first few TXs to get QSR? Once they get QSR they can hopefully avoid a PoW bottleneck.

[Bzed](https://forum.hypercore.one/u/Bzed) September 28, 2023, 8:54pm  99

Yeah i agree its the dynamic aspect of it that seems to have potential.

Balancing between lanes and some sort of “difficulty adjusted” floating base plasma if possible.

[0x3639](https://forum.hypercore.one/u/0x3639) September 28, 2023, 9:33pm  100

If we assume most users will not interact with the L1 ever or infrequently, this might change our mindset.

And if a user needed to interact with the L1 why can’t they run their computer and built up PoW “credits” over time. If they don’t have QSR and need to make a TX on L1 and they only have PoW let them run their computer for some time to build up cumulative PoW.

Another option is the user pays a 3rd party for PoW to process a TX for them. 3rd party fee markets will spring up to generate PoW.

Another option is to have some sort of springing transaction where a user pays a fee on the L2 that once conditions are met, QSR is fused on the L1 for the user allowing a TX on the L1. QSR owners could rent their QSR to users for L1 TXs.

I’m starting to think we should not be designing systems that allows “regular” users to easily interact with the L1. Today that is all we have so it makes sense we are focused on that. But over I think we plan to migrate activity to higher levels.

[0x3639](https://forum.hypercore.one/u/0x3639) September 28, 2023, 9:36pm  101

[@MoonBaze](https://forum.hypercore.one/u/moonbaze) maybe we should start by reframing this discussion around the design goals of the L1. Do we expect for regular users to interact with the L1 “easily” once the Side Chain is live and the L2 is live?

I would like to propose that if we don’t expect average users to interact with the L1 regularly they will be less impacted by their inability to “easily” process PoW transactions. We can throttle the impact of a PoW attack at the block level (not sure how exactly) by assigning a percentage of TXs that can be PoW per block.

First time users can get access to QSR on the L1 from either (1) the L2 / side chain, (2) PoW provider, or (3) Performing extended PoW on their local computer for a “long” time.

Fees can live on the L2 and the L1 remains feeless. We can then focus on developing the algo for ordering TXs and figuring out how to dynamically adjust the number of PoW and QSR TXs per blocks (auto throttling) on the L1.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 29, 2023, 11:07am  102

As I said, choosing an optimal base fee would render dust attack useless. 1/200 ZNN e.g.

Also, any implementation that requires PoW or QSR is much more easier to attack as it is much more cheaper than buying and burning ZNN. Of course, we don’t know when we will have EVM on L1 and we only have embedded but still, we need a strong protection mechanism. Computing power at the level of sending a tx is still very trivial as computing power increases at a very high rate and QSR is really cheap. For example, with 500 qsr fused for 500 adresses ( 250k qsr ~ 15k usd ) I can make sure noone gets in a tx. We should not have a mechanism that is good for 5k,50k, 5 millions but for hundreds of millions which is ZNN fees. An attack would only benefit the network and beneficiars. Also, fees spam attack is an attack that beneficiars want. What other mechanisms makes you want to be attacked?

[0x3639](https://forum.hypercore.one/u/0x3639)

September 29, 2023, 12:23pm  103

Wouldn’t the cost of a QSR attack be higher? Was going through our notes from the last dev meeting. At 250,000 QSR an attacker would try to fill up a momentum with 3800 TXs. They would only be able to fuse 65 per address.

If they had 1m QSR, which is also possible, they could fuse 263 per address. If they did that it would mean users could overcome this attack by fusing more than 263. The system seems to balance itself naturally against this attack.

[![Image 219: Screenshot 2023-09-29 at 7.08.35 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/b9e5fe2c38e739a469e4ebf8625aa4317ff1e82c_2_690x91.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/b9e5fe2c38e739a469e4ebf8625aa4317ff1e82c.png "Screenshot 2023-09-29 at 7.08.35 AM")

The attacker would pay a “fee” for this attack in the form of lost opportunity cost of fusing 250K or 1M QSR. If we continued with the artificial cap of 100 TX (or some other number such as 500) per momentum the attack would be a lot easier and effective.

[Chadass](https://forum.hypercore.one/u/Chadass) September 29, 2023, 2:26pm  104

I challenged every single one of your ideas and you’re just going in circles. At some point you exhausted yourself and decided to undermine everything by claiming Mr. Kaine might be fake, and I am the one trolling? Read everything that has been discussed above, if you can suffer people disagreeing with you without being yelling troll every two minutes. For what I know someone can have control of your account and crypto so your delegation change isn’t a proof of anything. My point here was simply to show how ridiculous you were talking about Mr. Kaine this or that.

[Chadass](https://forum.hypercore.one/u/Chadass) September 29, 2023, 2:26pm  105

You never addressed the narrative cost of killing a Zenon narrative.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 29, 2023, 2:38pm  106

People would still have to acquire more QSR to fuse which is the equivalent of paying a fee, they just have to do some more txs to get them (while being spammed).

Chadass I just love how a non technical guy is challenging a technical one on matters that are way above your head to understand. You just see fee vs non fee and I can tell you hate fees. I will just ignore you from now on as you bring 0 value to the conversation. I am not here to fight with anyone but your ego is fueled by these clashes and you can’t stop it seems. Go on telegram and do what you know best and I will stay here to do what I know best.

[0x3639](https://forum.hypercore.one/u/0x3639) September 29, 2023, 2:55pm  107

I kindly request that we keep this conversation peaceful. These are obviously difficult topics.

Clearly I do not have a technical understanding of the protocol like moon, but I do understand quality of service in a network. Maybe we can take a short break, study / research some more, and keep discussing.

[Chadass](https://forum.hypercore.one/u/Chadass) September 29, 2023, 3:15pm  108

I love when technical guys have 0 understanding of marketing, UX, UI, story telling or narrative and blindly go for a costly ideology rather than looking for other solutions than might work even better. I’m not the only one challenging the direct fee route. If you weren’t so full of yourself, you could see it. Trolling and ignoring contradictory positions might be the usual way for you, I doubt this is how Zenon work.

You can ignore us all you want. I’m not talking to you only and I hope people will realize that mimicking what every single project does will inevitably end up with nothing different and nothing better.

There are dozens approaches of fee structures we can think of, from Chromia to what Mr. Kaine and the WP suggest. Invalidating them all on a whim indeed goes way above my head.

[0x3639](https://forum.hypercore.one/u/0x3639) September 29, 2023, 9:49pm  109

If anyone else wants to join in the conversation, I recommend you read the background here: [Discord](https://discord.com/channels/920058192560533504/1150019456718876843/1154757701021204480)

[Stark](https://forum.hypercore.one/u/Stark) September 30, 2023, 12:42am  110

1.  How do Tier 1 ISPs deal with high throughput and spam?
    
2.  What if we think of NoM pillars as a federation that governs and operates the Tier 1, L1?
    
3.  Should we expand this “Tier 1” language into marketing, to communicate the scale of our vision?
    
4.  Where is the ‘network congestion’ intercept between the cost of PoW vs the max network capacity (with narwhal and tusk)?
    
5.  How about a maximum plasma rate? For example, all transactions with max plasma (200 QSR) are queued and processed in sequence. How much QSR would an entity have to possess in order to single handedly cause congestion, given the network utilizes N & T?
    
6.  QSR distribution VS cost of PoW VS network capacity - what if it’s simply impractical and pointless to attack the network, and the federation stands to step in, in the event of some extreme situation, as it does in any case.
    
7.  Shouldn’t the network be able to handle plasma traffic up to the full amount of QSR in circulation?
    
8.  What if plasma is prioritized over PoW and PoW transactions have the option to be accelerated with plasma (replace by fee, but with plasma).
    

[Shazz](https://forum.hypercore.one/u/Shazz) September 30, 2023, 4:44am  111

Zenon’s “feeless” characteristic is one of the protocol’s biggest selling points. Chadass is right: there must be a massive reason to even consider undermining it.

[Shazz](https://forum.hypercore.one/u/Shazz) September 30, 2023, 4:56am  112

The fact that you dismiss his opposition to introducing fees on the premise that he is a non technical guy and thus shouldnt have a say in this is concerning + indicates a lack of understanding from your end on the “non technical” implications the introduction of fees would have. I.e. Zenon becomes one of thousands of shitcoin projects (no, 99% of users dont give a rats ass about decentralization).

Find a way to prevent network spam without undermining its core value props.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) September 30, 2023, 6:51am  113

I don’t mind discussing this topic with non technical people because a cryptocurrency is so much more than it’s algorithm and we have to take into consideration all the implications. I mind discussing with people like him that start to troll and harass people for no reason.

> Zenon’s “feeless” characteristic is one of the protocol’s biggest selling points.

The network would still be feeless, that’s the point. You all forget that fees are optional. A fee spam attack cannot hold too much time and with increasing momentum size we won’t have 100% utilization all the time in regular conditions.

I see that you are all against but in my opinion there is no good pow / plasma solution that we can implement correctly with the given man power / financing.

I will move on from this for now and let you all decide, I said what I had to say. I will start to look into increasing momentum capacity.

[Shazz](https://forum.hypercore.one/u/Shazz) September 30, 2023, 8:32am  114

As long as fees are kicking in dynamically to prevent spam during peak utilization rather than by default makes sense to me

I will read the entire thread but a bit short on time so just some thoughts that popped in my head. Could you charge a fee based on a tx threshold of total transaction limit by account? Get we can create many accounts so second question, could you limit free account generation e.g., each instance of syrius/ip can generate 10 accounts for free then it is x to set up each additional account.

Another thought, ideally we will have multiple classes of customers including enterprise size, small business, and individuals. Fusing massive amounts of QSR to produce plasma would be feasible for enterprise customers but a bit of rich getting richer case there - need to find a way to not punish the average person in whatever solution is designed.

Maybe plasma generation time comes into play and there is an option to pay a fee to regen plasma faster - average user sends a few tx a day can wait for plasma regen while enterprise / attacker could not so rich / attackers have fees avg person does not

Again apologies if these thoughts were discussed already but wanted to bring them up before I forgot them ![Image 220: :slight_smile:](https://forum.hypercore.one/images/emoji/twitter/slight_smile.png?v=12)

[Stark](https://forum.hypercore.one/u/Stark) September 30, 2023, 11:13pm  118

What is the average user going to do on NoM L1?

Should we think in terms of sidechain / L2’s with their own user facing fee dynamics fusing plasma, to open up channels?

[Chadass](https://forum.hypercore.one/u/Chadass) October 2, 2023, 12:03am  119

That’s another question as people build ground protocols for other’s to develop usecases ex: p2p swaps.

[Stark](https://forum.hypercore.one/u/Stark) October 6, 2023, 6:25pm  120

It seems like the parameter limits should be set, such that the network can handle throughput in the event that all QSR in circulation were to be fused to plasma.

Combine that with a separate dynamic lane for PoW, which also has maximum parameters.

A person can only breath so much air, according to their lung capacity and breathing frequency. And there are only so many people on earth. Whether we approach the equation from the volume of air on earth, or the volume of air a person can breathe, there is no danger of any one party breathing all the air.

There is a limit / constant to network throughput (which I suppose will increase with adoption) but we have the power to set the parameters on the other side of the equation - maximum transaction size, frequency of plasma recharge, etc. As long as the upper limits are set so that the network can handle it’s own circulating supply, there is no vulnerability.

3.  Spam/DoS Resistance

Nano has a unique transaction prioritisation system based on the last transaction time of an account and its balance. Through strategic categorization into specific buckets—determined by the larger of the two: account balance or transaction amount—we proactively prevent spam transactions from congesting the network. This method ensures genuine transactions are prioritised, especially from less frequently used accounts, allowing them to proceed without interference from potential spam.

In our pursuit of increasing DoS resistance, we’re drafting a peer rating system. This system will identify and manage peers that display irregular behaviours, such as sending improperly signed messages or excessively flooding the network. While the specifics are still under consideration, this measure aims to maintain network health by potentially limiting or temporarily isolating such non-compliant peers.

* * *

I like the idea of burning `ZNN` as transaction fees. This hybrid mechanism can protect the network against spammers. During peak tx periods, the network can shift to a fee based system.

It might be hard to detect spammers when the network is congested, but paying fees will discourage them and decongest the network:

Low usage =\> feeless  
Normal usage =\> hybrid  
High usage =\> fee-based system with prioritization

I also like the idea of lanes, seems very similar to Nano’s idea of “buckets”.

We can map some data points about an account and create a dynamic algo that can take into account both Plasma and fees.

`QSR` achieves equilibrium via Pillar slot burning.

We need to achieve Nash equilibrium for `ZNN` as well.

[Stark](https://forum.hypercore.one/u/Stark) October 6, 2023, 9:18pm  122

What is the point of having a bunch of QSR in circulation that can’t pass a transaction? Feels like the narrative is “fractional reserve utility”.

For a basic entrant, we’ll have ZNN, QSR, fusing, staking, delegating, plasma, bridging, extension chains, syrius, and metamask. By the way, we are feeless PoW/PoS except for when the network gets congested, or if people just use it a lot. When that happens, we have gas fees, just like every other chain.

If someone fuses a shitload QSR, why shouldn’t they be able to use the network within the maximum parameters, indefinitely?

If someone wants to perform massive PoW, why is that a bad thing?

See: “Don’t hate the player, hate the game.”

I think it is a matter of defining the dynamic parameters _up to certain limits_ within which everyone can use the network in any way that they wish.

Another out-of-the-box idea is to use the delegation mechanism to throttle bad actors.

*   Delegating your balance to a Pillar =\> vote of confidence =\> delegate action
*   Throttling accounts =\> punish bad behavior =\> throttle action

It is basically a p2p censoring mechanism. I don’t know the implications, but we can explore this solution too.

This goes hand in hand with the “lanes” idea presented earlier. There are separated lanes that get wider or narrower depending on what’s happening within the network.

[0x3639](https://forum.hypercore.one/u/0x3639)

October 6, 2023, 9:53pm  125

If we did not have fees, I guess the only way to process a TX under heavy usage would be to generate more PoW or fuse more QSR. Or apply a time multiplier to the amount fused so (time waited) x (fused amount) = (adj)fused. Eventually the adjusted fused amount would be greater than the current fused amount and older TXs would get processed.

As our echo system evolves, Pillars or Service providers could provide a fusing service as discused today. Users of the network could pay a fee or delegate to pillars to have them process TX for users by generating PoW or fusing a lot of QSR.

Can we prevent abuse by applying a nonlinear function to the amount of QSR or PoW required to process more than one TX per momentum per address? That is basically what KASPA did to prevent dust attacks (but it a different way).

[Stark](https://forum.hypercore.one/u/Stark) October 6, 2023, 10:11pm  126

For example, what if 50 QSR = high plasma.

100 QSR does not give priority over 50. 50 QSR gets you a ticket in the queue. Period.

The protocol and max parameters of a tx could be designed to assume that all of the QSR in circulation could be fused to myriad addresses, all of the addresses could submit an indefinite series of transactions, and everyone would get through, in queue.

Ideally, the headspace / max throughput of the network and the max transactions parameters balance out so that it takes seconds or less to run through the queue.

(circulating supply / high plasma) / tps = seconds to run through the queue at max usage (hypothetically?)  
(29M QSR / 50 high plasma) / 100,000 tps = 5.8 seconds

Can we just start with small parameters that fit the current capabilities and use cases of NoM and then N&T or some other solution will enable the “100,000 tps”?

[0x3639](https://forum.hypercore.one/u/0x3639) October 6, 2023, 11:19pm  127

I think the amount of QSR fused needs to be a parameter otherwise you will just need to wait in line. And there will be no reason to own more QSR other than to launch pillars and sentinels.

[Stark](https://forum.hypercore.one/u/Stark) October 7, 2023, 12:56am  128

What if the line is effectivelynever any longer than x seconds or 5 minutes or whatever?

If you want people to own more qsr then increase the requirements for high plasma. This probably necessary anyway.

What is the current effective tps of NoM?

If it’s 100 tps then 500 QSR (max) for high plasma would mean that if all 29M QSR were fused 500 QSR per address, a full capacity queue would get through in 10 minutes. (Very rough worst case scenario and not factoring PoW).

If it was just you and the spammer and the spammer had 28,999,500 QSR, to your 500, you’d have to wait 10 minutes.

This is my thesis on gas tokens on networks that tout being cheap. Nobody needs that much MATIC nor XRP.

I don’t think we’re necessarily looking for reasons for people to own bags of tokens. That’s the direction / frequency of thought that is going to make the whole narrative around tokens implode. We are getting a step ahead of this.

*   we could also have more meaning around low med and high plasma.

Advising participants that they correspond with network traffic and prioritization.

[Bzed](https://forum.hypercore.one/u/Bzed) October 7, 2023, 12:36pm  129

Are you suggesting we could use an address specific Plasma/PoW requirement based on that account chains usage?

[0x3639](https://forum.hypercore.one/u/0x3639) October 8, 2023, 1:52pm  130

that was my thinking. it could help prevent excessive TXs from one address. Maybe that would be more helpful to prevent PoW attacks. Not sure. It would be easy to spread out a large amount of QSR to thousands of addresses to avoid this.

Maybe this does not accomplish anything.

[0x3639](https://forum.hypercore.one/u/0x3639) October 8, 2023, 1:53pm  131

Everyone successful gets attacked. It’s just a matter of time.

[https://x.com/THORmaximalist/status/1711010096371671373?s=20](https://x.com/THORmaximalist/status/1711010096371671373?s=20)

[Bzed](https://forum.hypercore.one/u/Bzed) October 8, 2023, 4:57pm  132

Ok that seems like a strong approach to me. If the required pow/plasma needed is dynamic but based on the individual address throughput per momentum then there should be plenty of flexibility for other users to use the network without needing excessive amounts of pow or plasma.

Was it mentionned that we can lengthen the time for plasma to be returned to an address too? I could see that being another helpful measure.

This is where I was thinking. Instead of saying “if the network is busy you will have to pay fees” it becomes “if you plan to send more than x transactions within y timeframe you will have to pay fees”. Logically it makes sense the network is free for the average user - most would not need to make a transaction more than ever minute at the soonest - while enterprise users would need the high throughput.

Having said that not sure how we walk the line between fees being acceptable for enterprise use but prohibitive for spamming. More just thinking conceptually and how we can still claim a feeless network

[Stark](https://forum.hypercore.one/u/Stark) October 9, 2023, 12:21pm  134

What are all of the variables in the equation?

Can we list them all?

Which variables are programmable parameters?

What would a dynamic plasma equation look like?

Are there enough programmable parameters to work with, without adding another variable?

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) October 9, 2023, 6:59pm  135

Keep in mind that one could always send to an address, receive on it, resend again and so on. He will always have a new address so “if you plan to send more than x transactions within y timeframe you will have to pay fees” will not work

[Stark](https://forum.hypercore.one/u/Stark) October 11, 2023, 12:42am  136

‘Plasma lock’ could be another variable in the equation.

1.  Plasma recharge
    
2.  A plasma lock period that makes the plasma non-unfusable for a period of time. I’m sure we can come up with variables that fit within the feeless paradigm.
    

Possible to monitor creation of addresses by ip - get x free then pay for each additional address?

Could you require PoW to create new addresses and/or for tx above a certain threshold? Is this convo still going somewhere else or has it died?

[0x3639](https://forum.hypercore.one/u/0x3639) October 15, 2023, 9:24am  139

I think people are still working on this for sure. I know [@vilkris](https://forum.hypercore.one/u/vilkris) is thinking about this in the context of this [Metamask Snaps for Zenon](https://forum.hypercore.one/t/metamask-snaps-for-zenon/209) Sounds like he is making some new discoveries but no conclusions.

[vilkris](https://forum.hypercore.one/u/vilkris) October 15, 2023, 10:32am  140

You can create as many addresses as you want without internet. It’s just a cryptographic algorithm that “creates” a new address.

Well the situation is that one side wants to implement dynamic plasma by adding optional fees, and the other side wants to explore alternatives that only rely on PoW and QSR fused as plasma.

I think both of these options still need a mechanism that balances PoW and plasma dynamically, so I would advocate to find solutions to that problem first.

In case people looking into dynamic plasma haven’t investigated Nano yet, I think we could get some good insights from them. They’re feeless and they use PoW as an anti-spam mechanism on their network and it has a lot of similarities to our PoW mechanism.

Apparently this is their current mechanism for tx prioritization (archive link because their forum is down): [https://web.archive.org/web/20230426170346/https://forum.nano.org/t/time-as-a-currency-pos4qos-pos-based-anti-spam-via-timestamping/1332](https://web.archive.org/web/20230426170346/https://forum.nano.org/t/time-as-a-currency-pos4qos-pos-based-anti-spam-via-timestamping/1332)  
Not saying we have to copy this, but it can give us ideas.

Yes and I’m theorizing that the use of pillar operated TX provider services could reduce the effect of heightened network difficulty on regular users using the provider services. Providers will be competing for delegators, so they’ll have the incentive to invest into PoW infrastructure/QSR and thus would be more capable of handling heightened difficulty in order to provide a smooth service for their delegators.

With that said I don’t have all the answers to how these provider services would work and it still needs more research to determine their feasibility.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) October 17, 2023, 6:54pm  141

[https://twitter.com/LiveOverflow/status/1714342123724574979](https://twitter.com/LiveOverflow/status/1714342123724574979)

This seems like the same issue to me, I don’t see any solution now that would not render sending a transaction impossible for the regular user in case of spam without optional fees.

[Chadass](https://forum.hypercore.one/u/Chadass) October 17, 2023, 9:29pm  142

In case of spam wouldn’t the fee be astronomically high? We saw that on both BTC and ETH with hundreds of $$$ required to send a tx in case of high congestion. How is this a solution?

[Stark](https://forum.hypercore.one/u/Stark) October 19, 2023, 1:49am  143

When a node performs PoW, does that contribute to faster or bigger momentums? If PoW adds value, I don’t understand why it should ever cause a problem.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) October 19, 2023, 10:23am  144

The base fee is relatively small, 1/200 ZNN, which could be modified in the future by governance maybe in case znn goes to 200$ for example.

I still believe that giving the user a choice is the best option, it’s much better rather than them not being able to even send a tx. We need both a dynamic plasma / pow mechanism and optional fees in order to have a complete solution.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) October 19, 2023, 10:23am  145

PoW does not add value, it’s just an anti spam mechanism right now

Pow adds weight.  
And weight adds value because there is cost to fabricating chain data.

I agree a holistic approach is the best one in the long run.

.

[MoonBaze](https://forum.hypercore.one/u/MoonBaze) October 19, 2023, 8:49pm  148

Not in the current implementation

**Dynamic Plasma Proposal**

Current implementation:

1.  Every address has a corresponding account-chain where every account-block represents a transaction.
2.  Transactions are confirmed by the consensus in a separate structure which forms the dual-ledger
3.  Currently, a basic anti-spam mechanism exists:  
    3.1 Plasma obtained by generating Proof-of-Work: every user can generate a SHA-3 based PoW to send or receive transactions.  
    3.2 Plasma obtained by fusing QSR: every user can fuse a minimum of 10 QSR for any address for a minimum of 10 hours to send or receive transactions.

**Problems with current implementation**

1.  There is no positive feedback loop built into the system because transactions are feeless (Ethereum for example burns fees =\> the more the system is used =\> the better for every stakeholder in the system)
2.  ZNN needs to achieve equilibrium like QSR (burned or used as fee)
3.  Thresholds are hardcoded

**Solution**

Implement a hybrid Plasma system with 2 lanes:

1.  A feeless lane where users can still use PoW and QSR to generate Plasma.
2.  A fee-based lane where users _**burn**_\* an amount of ZNN to generate Plasma.

(\*) Burning ZNN makes sense long term, as validators already produce ZNN inflation indefinitely.

*   We need an algorithm to balance those lanes as the network gets congested.
    
*   We need to remove the hardcoded values from the feeless mechanism and implement dynamic thresholds.
    
*   We need to replace SHA-3 with an ASIC-resistant PoW.
    
*   Also we need a method to measure transaction “quality” that will determine the minimum Plasma thresholds:
    
    *   transaction amount in ZNN/QSR
    *   current balance of the account-chain in ZNN/QSR
    *   last transaction time of the account-chain
    *   number of account-blocks in the account-chain

**Future work: PoW links**

The whitepaper mentions PoW links where Sentinels take the role of crafting them by attaching a PoW and signing them (MrK already specified that this PoW can be outsourced to other clients). Currently, validators have the role of adding transactions to blocks and processing them. However, this can introduce new problems such as:

*   Censoring transactions
*   MEV
*   Improper ordering of transactions

By adding a separate layer of nodes to “prepare” transactions, many of those problems can be avoided.

[@georgezgeorgez](https://forum.hypercore.one/u/georgezgeorgez) [@MoonBaze](https://forum.hypercore.one/u/moonbaze) [@sumamu](https://forum.hypercore.one/u/sumamu) [@0x3639](https://forum.hypercore.one/u/0x3639) [@sol](https://forum.hypercore.one/u/sol) [@CryptoFish](https://forum.hypercore.one/u/cryptofish) [@Chadass](https://forum.hypercore.one/u/chadass)

[Chadass](https://forum.hypercore.one/u/Chadass) November 4, 2023, 5:31pm  150

I will dig into this asap but so far it sounds like a god compromise given the discussion we had. Thanks for this.

By adding a fee-based lane, we will also streamline integrations with the wider crypto ecosystem:

*   integrations with popular wallets such as [TrustWallet](https://github.com/trustwallet/wallet-core)
*   integrations with CEX
*   other integrations that require a different model from the standard one based on fees

[Shazz](https://forum.hypercore.one/u/Shazz) November 4, 2023, 10:00pm  152

If fees are introduced (apparently as a hitherto unknown necessity due to most peoples’ beliefs that merge mining would be sufficient), what will be the share of feeless txs vs paid ones at high network usage and doesnt this ultimately undermine one of the key value props of zenon (assuming it will actually become an L1 eventually)?

If merge mining is implemented, won’t there be fees to pay to miners too though?

[Stark](https://forum.hypercore.one/u/Stark) November 4, 2023, 10:32pm  153

How about using btc as gas?

[Chadass](https://forum.hypercore.one/u/Chadass) November 4, 2023, 11:04pm  154

Why? To be able to say we’re feeless because it’s another coin? What would be the benefit?

[Stark](https://forum.hypercore.one/u/Stark) November 5, 2023, 5:16pm  155

What are the stated purposes of introducing a fee mechanism?

Do those purposes imply any reason to use ZNN or QSR?

What is the hardest and most valuable cryptocurrency?

Would having a reserve of BTC locked in NoM serve some utility purpose in terms of interop or defi?

How do Bitcoin devs perceive projects that feature tokens?

Why do most projects use one token for governance, staking, yield, and gas?

What problems result from using one (or two) currencies for everything?

What other projects use BTC as the principle protocol level gas currency?

Would btc gas provide some minimum viable reasoning for the new logos and stickers?

Does it feel intriguing?

I think I might rather see NoM remain feeless, and then see an extension chain that might use BTC as gas. However, if this fee thing turns out to be widely supported and inevitable, then I feel BTC gas would be a much higher vibe than ZNN/QSR. Could the BTC lane be dynamic?

Maybe NoM is fundamentally feeless, but BTC gas transactions have priority up to 100% if the demand arises.

I have more questions, than answers, but I hope some others will be willing discuss the questions I posed above.

[Shazz](https://forum.hypercore.one/u/Shazz) November 5, 2023, 5:37pm  156

Maybe it would help the discussion in this thread (it’s a dev chat after all) if the questions asked were more narrowed down and to the point [@Stark](https://forum.hypercore.one/u/stark) - or use the other forum for less technical brainstorming? Just a suggestion since we have few dev resources

[Stark](https://forum.hypercore.one/u/Stark) November 5, 2023, 5:54pm  157

Btw, I am 100 percent ok with being banned if my participation in this forum is outside the scope. I only know how to be myself and if the way I interpret these discussions and this forum is incorrect, just kick me out. No hard feelings.

Creating a feedback positive loop inside the ecosystem. Burning ZNN benefits every stakeholder from the ecosystem.

QSR is already used as proxy for generating Plasma. Burning ZNN makes sense in the long term, as QSR is already burned for creating Pillar slots.

Bitcoin.

This is beyond the scope of this discussion. We can use the TSS that secures the bridge to create a BTC vault.

Scams.

Simplicity.

This is beyond the scope of this discussion.

Liquid network I guess. To incorporate BTC as gas into the network we need access to the state of the Bitcoin blockchain. It’s feasible, but I don’t see an implementation at this stage.

Burning ZNN is the most logical thing to implement right now, because at the moment ZNN is only produced as inflation. We need a counter-balancing force.

A minimum threshold for feeless transactions can be implemented (reserving min 10% of a momentum’s capacity).

I guess Pillars setting up PoW pools will distribute a fraction of their rewards accordingly (similarly to paying delegators right now). IMO merge mining is another topic that should be discussed separately from dynamic plasma.

[Chadass](https://forum.hypercore.one/u/Chadass) November 5, 2023, 9:20pm  160

I just add to my first answe here and to precise things for [@aliencoder](https://forum.hypercore.one/u/aliencoder) and others: fee by themlselves WILL NOT benefit anykind of holders. I assume the idea here is that having fee means ZNN are burned which would translate in a somewhat better price action.

I never saw it, ever. It simply doesn’t work that way. The fee rarely balance the inflation. It’s never more than a minuscule % VS the tokens emission.

What you need is demand (hype, usecase, whatever). Your price action is the result of a lot of factors and a ton of highly inflationary systems (fee or not) see themselves going up - price wise - with the force of a thousand virgins and for a very long time - even with tokens unlocks hammering the supply on a montly basis. Talking about (not nash) equilibrium between burning mechanisms and inflationary policies is dangerously naive.

If this is one of the main reason for people to throw away the feeless paradigm we thought was the core of ZNN I suggest to reconsider.

Don’t try to induce in error the readers with this statement: I was proposing a hybrid system with a feeless lane.

Dynamic Plasma implementation

*   Feeless (no change)
*   Hybrid (2 lanes: one feeless, one with fees)
*   Fees

[Shazz](https://forum.hypercore.one/u/Shazz) November 6, 2023, 9:29am  163

What’s the ultimate consequence of option 1) feeless (no change) in terms of scalability limitations?

[0x3639](https://forum.hypercore.one/u/0x3639) November 6, 2023, 1:59pm  164

This is a good point.

[Stark](https://forum.hypercore.one/u/Stark) November 6, 2023, 2:44pm  165

Is there a counterpoint to the suggestion that the introduction of fees creates an incentive to spamming the feeless lane?

Or another perspective on the same concept: Won’t entities prefer to use the feeless lane rather than use the fee lane? And therefore wont the feeless lane conceivably be constantly maxed out and dominated as the result of not solving feeless dynamic plasma? It seems like this results in a defacto fee based L1 for all intensive purposes.

Does creating two lanes result in a hydra? (Two headed problem.)

If I read correctly, the tokenomic inflation/deflation theme is very prevalent - which makes me ask “Are we intending to solve for dynamic plasma, or are we hoping to redesign the token economy?”

[Chadass](https://forum.hypercore.one/u/Chadass) November 6, 2023, 6:38pm  166

I don’t induce anyone in error - I think everyone can read - and no, an article about how ETH became sound doesn’t counter the fact that is didn’t work on ETH and other cryptos for the benefit of holders. Check the charts.

[0x3639](https://forum.hypercore.one/u/0x3639) November 6, 2023, 7:52pm  167

I think the issue is we don’t want fees, but no one has presented a solution to dynamic plasma that “works” without fees. Right now I’m keeping an open mind to the possibility a solution exists without fees.

[0x3639](https://forum.hypercore.one/u/0x3639) November 6, 2023, 7:58pm  168

Thinking about this a little more. If we don’t have a fee lane, Trustwallet, for example, would need to incorporate PoW and/or QSR fusing into the wallet in order to support NoM. That is unlikely for a long time. Therefore, we would need to rely on a Metamask Snap if [@vilkris](https://forum.hypercore.one/u/vilkris) can overcome the technical issues.

If we don’t have a fee BUT we solve the Metamask technical issues, won’t NoM work with CEX so long as they work with Metamask?

The problem is that ordinary users will be pushed out of the system if the PoW is too difficult. By introducing another lane, the dynamic algo and market forces will balance the usage in a more uniform fashion.

By having a fee-based lane, you can spam the feeless lane as long as you want, but you won’t congest the network. That’s exactly the reason you’ll find a dynamic algo in my proposal that balances the two lanes by taking into consideration network usage and other parameters.

We can kill 2 birds with one stone: solving dynamic plasma and creating deflation for ZNN.

The ETH chart looks great. Hope I can say the same for ZNN.

Because dynamic plasma is about solving network spam. And to solve this issue, a holistic approach is needed where we need to think outside the box.

Let’s be honest, without aligning with the rest of the market won’t bring us closer to “mass adoption”. Imo we have another 6-8 months left to build before we enter the bull market. With a “standard” fee system we can start integrating with popular multi-chain wallets that will open up millions of potential buyers.

No, because CEX use custom backends, not Metamask to process user funds. Similar to multi-chain wallets, CEX prefer standard implementations. And we need CEX to bring even more users than multi-chain wallets.

You can see that I’m trying my best to answer everyone’s questions. [@Shazz](https://forum.hypercore.one/u/shazz) [@Stark](https://forum.hypercore.one/u/stark) [@Chadass](https://forum.hypercore.one/u/chadass) [@0x3639](https://forum.hypercore.one/u/0x3639)

* * *

Another positive outcome for the hybrid system:

An attacker will need both PoW and ZNN to be able to successfully overwhelm the network. This fact is greatly reducing the attack surface for a sophisticated attacker, as he needs to open 2 fronts in order to spam the network.

Even though I don’t like fees, [@aliencoder](https://forum.hypercore.one/u/aliencoder) is pretty convincing in his arguments

[sol](https://forum.hypercore.one/u/sol) November 7, 2023, 5:42pm  171

I’d like to bring the focus back to an important topic: dynamic plasma requirements as a function of network utilization.

Despite 170 posts in this thread, there aren’t many about the problem we are trying to solve.  
Instead, we’re debating the entirely separate topics of tokenomics, emissions, and price action. Anyone that’s passionate about these, please feel free to start another thread. Those changes belong in a separate ZIP.

After almost a year of deliberation, [this is the only thread that proposes solutions to balance PoW and fused QSR plasma.](https://forum.zenon.org/t/dynamic-plasma/1211) I believe a few devs are still drafting their proposals, myself included.

Here’s an excellent summary of relevant data: [KB: PoW and Plasma - ╰ Network - Forum](https://forum.zenon.org/t/kb-pow-and-plasma/1325)  
These variables/functions should be the primary focus of our discussion.

Considerations:

*   bandwidth constraints / momentum capacity
*   difficulty adjustment periods
*   fluctuating transaction / data costs based on recent network conditions
*   fused QSR limitations
*   the ratio of PoW plasma to fused QSR plasma
*   exceptions, such as guaranteed tx priority for certain tx types
*   RBF, but with more plasma

A few points about the work we need to accomplish:

1.  We need both node and client PoCs for RandomX integration. Vilkris has started that work [here](https://github.com/hypercore-one/znn-pow-links-cpp/tree/randomx-poc).
2.  We need a node PoC for transaction ordering based on transaction plasma. Even if we can’t enforce it, I’d expect most pillars will use this code.
3.  We need to define an algorithm that balances plasma requirements based on network conditions. Afterwards, we’ll need a node PoC.

* * *

In terms of feeless spam control:

1.  Prioritize fused QSR over PoW bandwidth
    *   In the absence of fused QSR tx, PoW tx should be able to use all available bandwidth
    *   In the presence of an abundance of fused QSR tx, PoW tx bandwidth should be limited.
2.  Allow fused QSR to be frozen and seized via governance
    *   This threat alone should deter actors from spamming senselessly
    *   I can elaborate in a future post if anyone wants to know more
    *   A penalty is not censorship
3.  Account-based plasma requirements
    *   If an account submits many tx in a short period of time, their subsequent txs cost more plasma during a cooldown period.
    *   I’m not sure if this is feasible

Are there other feeless ways to limit spam?

The problem we are trying to solve is deeper than you think. I’ve brainstormed many scenarios that include only the feeless design and a hybrid system is the only way to really get the best of both worlds. Otherwise we’re running in circles.

We are debating only tokenomics related to anti-spam mechanisms. Burning ZNN indirectly benefits everyone from this ecosystem.

Bitcoin is successful not only because it has great tech, but it also has powerful incentive structures.

I agree: burn ZNN fee \> Fuse QSR fee \> PoW fee

I won’t support anything like this and it’s dangerous to even propose it (I’m against this proposal, not your opinion).

I agree and I’ve proposed this earlier.

Without a fee based mechanism, one cannot limit a sophisticated attacker to spam the network. By combining all of those mechanisms in a hybrid design, we can achieve a system that will deter even a determined attacker.

[sol](https://forum.hypercore.one/u/sol) November 8, 2023, 8:02pm  175

We’re already doing this because three people decided fees are the only way to counter spam.

Let’s talk about the drawbacks that will result from the introduction of fees.

1.  Increased risk that consensus nodes accept/refuse certain transaction types
    *   people are worried that my proposal introduces censorship risk, when this is arguably worse
2.  Increased risk of PoW and fused QSR spam in order to force the average user to buy and burn ZNN
    *   we should probably brainstorm the game theory for the incentive changes
    *   George warned that fees could introduce perverse incentives
3.  Reputational damage from years of marketing a feeless paradigm, only to concede to the status quo and force users to pay transaction fees
    *   inb4 “fees are optional” tg sticker packs
4.  Weakened QSR utility will likely have a negative effect on its future price action
5.  Risk that feeless zapps won’t be feasible under certain conditions

* * *

Your reasoning for fees is:

1.  PoW and QSR are relatively inexpensive and permissionless, therefore it will be trivial to spam that bandwidth
2.  Fees are progressively expensive; therefore, as a measure of last resort, malicious actors won’t be able to spam the network infinitely

My reasoning for feeless is:

1.  PoW is subject to hardware, energy, and difficulty constraints. Difficulty adjustments will already limit the threat of PoW-related congestion.
2.  Transactions will be subject to dynamic (fused QSR) plasma requirements, potentially even at the account-level.
    *   If we can algorithmically limit individual addresses from spamming, then we’re probably in good shape to scale.
    *   If not, then we can rely on governance to intervene and forcibly limit their throughput.
    *   inb4 “slippery slope”. Sure, but we’re already trusting pillars to act in the network’s best interest.
3.  Won’t Sentinels and PoW links already limit every address’ throughput anyways?

* * *

You also haven’t addressed most of the concerns that actually pertain to dynamic plasma, the ones I listed. The introduction of fees as a congestion control is just one part of the solution we need.

Let’s set aside this debate of fees vs no fees so we can move on from this deadlock and focus on the rest of the items.

Fees are part of the solution to counter spam. It’s a hybrid design.

We have a solution for this: threshold encryption to obfuscate transactions while they are in the mempool.

This risk already exists within the current system.

That is exactly what I’ve been doing for the last 2 months.

Fees alone are introducing “perverse incentives”, but Bitcoin is running fine with high fees nonetheless. But we can do even better.

Again, my proposal is a hybrid design.

I think we improve our reputation and adopt a cerebral solution: to create a hybrid design where we take the best of both worlds.

I think we all care about the future of this network, not random fudders.

QSR already has utility: fusing and spawning Pillar slots.

QSR is burned to create Pillar slots. It is also locked for fusing.

In a hybrid system, you can opt out of fees and only use PoW if you want.

My reasoning about introducing fees is that:

1.  Fees are a good deterrent when the network is spammed.
2.  A hybrid design is better than a feeless design or a design based only on fees.
3.  Burning ZNN represents the missing link in this ecosystem.
4.  If the network is spammed, one cannot fuse QSR.
5.  It is easier to attack a feeless design than a hybrid one.

If we start changing the code, we must be on the same page because we’re in the same team. I just want to be sure we have all the answers we need to proceed with the implementation.

[Shazz](https://forum.hypercore.one/u/Shazz) November 8, 2023, 10:36pm  177

Keep in mind though that znn burn from tx fees will unlikely have more than a marginal impact on the reduction of inflation. As Chadass said, we need usage, hype, adoption. Znn burn per txs is a bandaid when you have zero usage and demand.

[sol](https://forum.hypercore.one/u/sol) November 8, 2023, 11:10pm  178

Let’s just agree that the initial dynamic plasma solution won’t include the following:

*   obfuscated transactions
*   virtual voting
*   sentinel support

No, it isn’t. Transaction spam will not result in any sort of fees for the average user.  
They will only have to wait for their transactions to be confirmed.

I disagree; rational actors in fee-only systems will act in ways that benefit them.

In the hybrid system, rational and irrational adversaries can spam the network to force everyone to pay fees. They only need to reach a threshold where the average user is sufficiently deterred from waiting.  
Additionally, consensus nodes can reinforce this initiative by only accepting fee’d transactions, because it’s in their financial interest to have people buy/burn ZNN.

In a feeless system, the risk of a rational actor behaving maliciously is slim, and it becomes nonexistent with governance intervention. Irrational QSR whales won’t stand to gain financially from spam. They risk losing money in that circumstance, as network participants leave the system due to frustration.  
This is likely why no one has spammed NoM to date.

And I’m convinced a balanced PoW/QSR system with difficulty adjustments will sufficiently deter senseless PoW spam given enough time.

Keyword is weakened. I think its use case will be diminished if the proposed feeless lanes are constantly maxed out. People will resort to paying the ZNN fee, and even then, they may be forced to wait or pay a higher fee.  
The average user won’t care to run infra.

So are:

*   QSR penalties via governance
*   PoW difficulty adjustments
*   Account-based plasma adjustments

I know I’m repeating myself. That’s why I asked to move on to other discussion topics.

Better in which way? Flexibility? UX? Scalability?  
I believe the product with the lowest cost to users and best UX will outperform all solutions.  
Our chain was specifically designed to be feeless in order to compete in a landscape plagued with high fees.

This narrative is derived from an argument about tokenomics and emissions.  
Dynamic plasma doesn’t need deflationary forces.

Not necessarily; I think we can design a creative solution to this problem.  
Vilkris has been working on a provider/onboarding system, and expressed other ideas to support new users.

If we want a quick solution, of course, fees are the easiest way forward.

If it’s designed well, it should cost considerable resources to temporarily inconvenience other users.

* * *

Why don’t we design a system that models after Bitcoin’s sats/vbyte instead of lanes with dedicated/variable bandwidth?  
I understand their nodes are incentivized to accept higher tx fees, but we will probably address this with virtual voting in the future.

[Stark](https://forum.hypercore.one/u/Stark) November 8, 2023, 11:15pm  179

How about setting a very steep curve for QSR requirements for plasma? Maybe 10,000 QSR for high plasma. Plebs can use plasma faucets. QSR maxis can start a PaaS economy. Keep the base layer streamlined.

At the moment it’s just a way to attract rational investors that will see real demand for ZNN.

We’re thinking long term (like an investor would), aren’t we?

I agree.

They also wait for their 1 sat/vbyte transactions.

We’re talking about a hybrid system here.

Pillars will see that a transaction has x amount of Plasma and decide to include it into a momentum.

No one spammed NoM because no one knows NoM exists in the first place.

Let the market forces and the dynamic algorithm decide which lane is more used.

If they want to pay fees, let them pay fees. Don’t try to impose something they are not familiar with just for the sake of being different. This is the model they already know. And this is how 99% of crypto currently works. We won’t be able to list anywhere if we only pursue the feeless narrative. Again, I’m not trying to replace the feeless design, but complement it.

Flexibility and UX:

*   Users outside our bubble are already familiar with fees
*   CEX listings will be easier in the future
*   Integration with multi-chain wallets such as TrustWallet, Exodus, Coinomi will be possible
*   Market forces will decide which lane is more used
*   ZNN will become deflationary and this is a big selling point (especially in a bullmarket)

Remember that we’re in Phase 0. For Phase 1 NoM needs to evolve. Isn’t it a self-evolving tech?

The ecosystem desperately needs deflationary forces.

You always forget we’re talking about a hybrid system, where fees are only part of the solution.

I need to repeat myself too: to spam a hybrid design an attacker needs to open 2 fronts.

Because I think we can do better.

Virtual voting is consensus related. When we’ll have threshold encryption for the mempool, we won’t need to worry about which transactions get in the momentum. The pre-processing will be performed by Sentinels before Pillars will include the transactions.

[0x3639](https://forum.hypercore.one/u/0x3639) November 9, 2023, 11:51am  181

[@aliencoder](https://forum.hypercore.one/u/aliencoder) I think you make some good points. Setting aside the discussion of Dynamic Plasma, I hope we can introduce deflationary forces in the network. Maybe the Sidechain and other scaling solutions will help.

If you were to take the other side of the debate, and support feeless TXs on the base layer, how would you try to design the system to accomplish that and what are the issues with that system?

* * *

My thoughts:

We can establish two lanes (PoW and Fused QSR). The width of the lanes can be fixed or adjusted programmatically based on saturation. If someone is attacking PoW (which could be easy) a user could circumvent that by fusing QSR. If someone is attacking PoW and QSR, they need to find a lot of QSR. It’s cheap, but not easy to buy. And there are “honest” QSR whales that could help overcome any QSR spammer.

If someone has 1M QSR to spam the network they can fuse 100qsr to 10,000 addresses. Users can overcome that by fusing 101QSR. The system will eventually come into balance. And, if we eventually create a QSR marketplace to “rent” QSR, attacking the network with 1m QSR will have a cost.

Back to PoW. Can we limit the amount of PoW that can be generated by one address? So one address cannot overcome (block) the network? If we can do that, the spammer would need to spread out their PoW across several addresses. They will just be another user processing valid TXs and other valid transactions would just take longer to process. If the PoW lane is saturated and Fused is not, we can adjust the lane width. Over time it could be “costly” (time consuming or lots of QSR) to process TXs on the L1. This will be for moving large amounts of digital gold (over time). This pushes TXs to the deflationary layers - L2, L3 and Sidechains.

We already have them for QSR. We need them for ZNN too.

But without fees we have an incomplete solution. Let the market forces decide if fees or feeless is the way.

Programatically with a fixed minimum size.

You don’t want to rely on network participants for designing an architecture. Only on game theory and programmable approaches.

I see that everyone think “fees” are the bogeyman. The hybrid solution is our best shot to 10x this ecosystem in the next 6 to 8 months.

[0x3639](https://forum.hypercore.one/u/0x3639) November 9, 2023, 12:26pm  183

Feels like we should solve for Dynamic Plasma without regard to our collective desire to increase price. We all want to increase demand, price, and dev interest. But I think (hope) solving Dynamic Plasma is a different issue than solving economics.

As a thought experiment, if we separate those two desires and focus exclusively on solving the problem of Dynamic Plasma, why can’t my big picture thoughts solve the problem without fees?

[Shazz](https://forum.hypercore.one/u/Shazz) November 9, 2023, 5:26pm  184

Let’s just move ahead with the most pragmatic solution that allows us to start thinking about what to build to create actual demand.

[sol](https://forum.hypercore.one/u/sol) November 9, 2023, 5:28pm  185

You dismissed my game theory points entirely.  
Let’s move on from this deadlock and discuss the other criteria for dynamic plasma.

Until virtual voting, this is not guaranteed.  
My point was: consensus nodes will be incentivized to prioritize and only accept fee’d transactions.

No, it’s because nobody gains anything from such an attack. The only threat is irrational spam.

Why not? It’s called the feeless paradigm for a reason.  
This is one of the only attributes that sets our network apart.

Nano, IOTA, Shimmer, Decred, Banano, etc…

You’re free to discuss tokenomics in a separate thread. This is outside the scope of dynamic plasma.

[Chadass](https://forum.hypercore.one/u/Chadass) November 10, 2023, 12:30am  186

“The ETH chart looks great. Hope I can say the same for ZNN.”

You’re cherry picking the one that fits out of 99978876 cryptos. This says a lot about your knowledge when it comes to economy in this space. I don’t doubt your coding skill, but here you’re just straight wrong and dishonest. ETH just got an ETF, probably not priced in its chart right?

The entire economic point you make in order to support your views on the fee / no fee debate is moot and nonsensical. No, fee won’t benefit holders in a meaningful way.

[Chadass](https://forum.hypercore.one/u/Chadass) November 10, 2023, 12:33am  187

Let’s not undermine what makes ZNN different.

[Bzed](https://forum.hypercore.one/u/Bzed) November 10, 2023, 3:16pm  188

This continues to sound like a reasonable and effective way to deal with congestion whether its from spam or regular use.

I don’t care about the price. I care about getting this right from the first shot, because if we have limited resources.

Dynamic Plasma is the anti-spam strategy of the network. With a hybrid design, we can kill two birds with one stone.

Because if we want to solve this issue, we need to get to the root of it: an attacker can spam easier without fees.

The byproduct of generating PoW, fusing QSR or burning ZNN (fee) will be Plasma.

They will render the network unusable. RandomX will alleviate this issue, but not entirely. A hybrid design is the definitive answer.

A feeless paradigm can coexist with a fees to create a hybrid paradigm.

This network has so much more potential.

IOTA is a failed project (Shimmer included). Nano (Banano included) is suffering from spam from time to time.

Designing components for a decentralized network may overlap with tokenomics and other “non-technical” areas quite often. Bitcoin is more than the tech stack.

I’m pointing out ETH because they have a working system that burns fees and we can all see it in action.

Burning fees will benefit everyone in the long term. More activity =\> more fees burned =\> less ZNN circulating supply.

Let’s strive for a more resilient system that takes into account all the variables.

Fees + Feeless \> Feeless (it currently makes more sense than ZNN + BTC \> BTC)

This hybrid design sets us apart and offers a competitive advantage over every other network out there.

Let’s suppose I’m an attacker and I want to spam the network:

1.  I can acquire beforehand QSR in large quantities at a reasonable price
2.  I can rent cheap PoW (even with RandomX I can overpower ordinary users)
3.  I can create a random ZTS token by burning 1 ZNN
4.  I can create unlimited accounts without any costs by sending my token (I don’t need ZNN or QSR)

[Bzed](https://forum.hypercore.one/u/Bzed) November 12, 2023, 12:05am  190

Is there really any proof of this?

There are already many important ways for ZNN to be removed from circulating supply like locked up infra which is already a huge chunk. If this isnt enough for any rational investor then burning a few znn in fees surely wont change anything.

Can you explain how these points are an attack? The dynamic aspect of the algo would adjust the cost and more plasma/pow will be required. The incentive is to work within the capacity of the network.

I do not see how adding a lane for fees is a competitive advantage in any way, cant that be for the extension chain?

[Chadass](https://forum.hypercore.one/u/Chadass) November 12, 2023, 12:21am  191

No, there are none. Quite the opposite actually. Most cryptos burn fees and the impact on the circulating supply is hardly impacting anything else. The data are out there and can be accessed easily, [@aliencoder](https://forum.hypercore.one/u/aliencoder) cherry picked ETH because it fits his views and willingly ignored everything else. This is complacency and would result in poor decision; cherry picking data never worked well in research. Beside, here we have a dataset of 1 data point (wow), which is extremely questionable as ETH PA is not the result of the fee actor alone so arguing that it benefits holder is a bit rushed, at best.

[coinselor](https://forum.hypercore.one/u/coinselor) November 12, 2023, 3:01am  192

I suggest we stop wording it as introducing transaction fees.

Aliencoder is suggesting we add an additional method to generate Plasma: Burning ZNN. Doesn’t sound too unreasonable, when stated this way.

I’m way more interested in actual numbers and simulations:

*   How much Plasma would burning 1 ZNN Generate? Moonbaze suggested a flat number of transactions per ZNN burned, instead of a Plasma amount.
    
*   After the tx is confirmed, plasma levels go back up. How would this work with burning ZNN? When QSR gets unfused, account plasma is lost. When burning ZNN, do we only get temporary Plasma for a single transaction? If it’s not temporary, it will allow an user to basically acquire an “infinite” number of transactions by burning ZNN (provided network plasma threshold to be included in a momentum remains the same).
    

Ethereum is the most obvious proof, but there are others nevertheless.

Locking != removing

With 1000 participants in the network you won’t notice the difference, but at \>100k the numbers will add up.

Point 1 is as easy to accomplish if a dynamic algo is in place.

Again, I’m not arguing about price increase. Most cryptos _use_ fees because it is a standard way to deter spam and that’s it.

Exactly:

*   Burn ZNN to generate plasma.
*   Fuse (lock) QSR to generate plasma.
*   Generate PoW to generate Plasma.

Whatever works for you.

We can borrow his base fee level: 1 ZNN burned = 200 txs

Of course temporary. You burn 1 ZNN, you get 200 txs if the network activity is at a baseline. If the network gets congested, you’ll need to burn more (subject to the dynamic algo).

[Bzed](https://forum.hypercore.one/u/Bzed) November 12, 2023, 11:22am  194

But that doesnt solve Dynamic Plasma, its just another way to transact.

It is an empirical problem maybe thats the approach we need to take.

Thank you for the replies but this is not proof, just an example of it.

[0x3639](https://forum.hypercore.one/u/0x3639) November 12, 2023, 1:02pm  195

I’m still struggling to understand why we cannot prevent spam with PoW and QSR fusing alone. Maybe we stop calling it spam and just call it valid TXs. They are the same.

2 lanes | PoW and QSR

PoW lane get saturated. PoW adjustment goes up and take longer to generate PoW. Setup RandonX to work on one address at a time. 1 CPU = one PoW generator per address. If you spam the network you need lots of CPUs. It’s costly.

QSR lane gets saturated. Amount of QSR needed to process a TX goes us. As usage goes way up (in years) it’s possible users will need to rent QSR to process a TX because the threshold is too high.

Lane width - Dynamically adjust lane width to ensure both lanes are saturated. When both are saturated, we can adjust them to make sure the width is “fair” (TBD).

[](https://forum.hypercore.one/t/dynamic-plasma-discussions/62/print#issues-1)Issues
------------------------------------------------------------------------------------

*   what is someone fuses 1m QSR on one address and hogs the network while the PoW lane is full?  
    – Response: Limit QSR per address via governance.
*   what if someone fuses 1000 QSR (the threshold established) across 1000 addresses.  
    – Response: That becomes the new limit and everyone needs to fuse 1000qsr and it’s first in first out. _What if we also require a very small PoW from a CPU when QSR is saturated?_ That would mean an attacker would need 1000 CPUs or would need to process the spam sequentially from fewer CPUs slowing them down.

[Chadass](https://forum.hypercore.one/u/Chadass) November 12, 2023, 3:30pm  196

Wouldn’t it be possible to implement a PoW + QSR lanes solution and stresstest it?

[0x3639](https://forum.hypercore.one/u/0x3639)

November 12, 2023, 4:45pm  197

yes, I think it can be simulated in python. Would not be hard to simulate.

We know the max throughput from feedback from Moonbaze. 3800 send / receive account blocks per momentum.

[![Image 221: Screenshot 2023-11-12 at 10.53.31 AM](https://hypercore.nyc3.digitaloceanspaces.com/optimized/1X/bd10ac9f30026f054c96ffd240ad0af7372573a0_2_690x135.png)](https://hypercore.nyc3.digitaloceanspaces.com/original/1X/bd10ac9f30026f054c96ffd240ad0af7372573a0.png "Screenshot 2023-11-12 at 10.53.31 AM")

[0x3639](https://forum.hypercore.one/u/0x3639) November 12, 2023, 4:59pm  198

assume 3800 account blocks every 10 seconds. We can model this in excel and python. Or we can use @risk.

[Chadass](https://forum.hypercore.one/u/Chadass) November 12, 2023, 4:59pm  199

That would be interesting so we would have empirical data to make decisions.

Gr8 we should try this and see how it goes 1st.

[Chadass](https://forum.hypercore.one/u/Chadass) November 12, 2023, 8:36pm  201

We’d need to see how the chain react with unpredictable factors aka computational power from Pillars, bandwidth, memory usage, etc no?

[aliencoder](https://forum.hypercore.one/u/aliencoder) November 13, 2023, 10:07pm  202

Because spamming the network must incur economic punishment for the attacker, while offering a net-positive benefit for the whole network. Burning ZNN achieves this and can be complemented by PoW generation and QSR fusion in a tri-lane system.

[aliencoder](https://forum.hypercore.one/u/aliencoder) November 14, 2023, 10:57pm  203

Paper: [https://arxiv.org/pdf/2304.06014.pdf](https://arxiv.org/pdf/2304.06014.pdf)

Implementation: [GitHub - yHSJ/tiered-transaction-mechanism: This is a basic Java implementation of the Tiered Transaction Pricing Mechanism described in the paper "Tiered Mechanisms for Blockchain Transaction Fees" released by IOG https://arxiv.org/pdf/2304.06014.pdf](https://github.com/yHSJ/tiered-transaction-mechanism)

*   Significant later results include \[Chung and Shi(2023)\] which show that in general, no transaction fee mechanism can satisfy user incentive compatibility, miner incentive compatibility and be off-chain agreement proof all at once.

Paper: [Game-Theoretic Analysis of an Exclusively Transaction-Fee Reward Blockchain System | IEEE Journals & Magazine | IEEE Xplore](https://ieeexplore.ieee.org/document/9672122)

Implementation: [GitHub - ekruminis/blockchain-model: Simulation model of a research paper: "Game-Theoretic Analysis of an Exclusively Transaction-Fee Reward Blockchain System."](https://github.com/ekruminis/blockchain-model)

*   A conjecture can be made that in a perfect, rational system, the variance between transaction fees will be uniform; that is, users whose transaction are included into the block will pay the exact same fee. This has no correlation to the urgency of a transaction, since transactions are still restricted by the block interval - simply paying more than others will not make their transaction be confirmed any faster. Also, if the block size is limited, assuming there are enough transactions submitted, the blocks will always be full and identical for each (rational) miner.

For the PoW lane we can use this:

Rotate PoW algos (including RandomX) depending on the hash of the frontier account-block for improved resilience. This would make a PoW lane spam attack from multiple account-chains very costly because with each transaction the attacker would need to switch between CPU, GPU or ASIC hardware.

[0x3639](https://forum.hypercore.one/u/0x3639) November 15, 2023, 10:48am  205

would this impact the work [@vilkris](https://forum.hypercore.one/u/vilkris) is doing with Metamask snaps?

[Chadass](https://forum.hypercore.one/u/Chadass) November 15, 2023, 11:49am  206

Interesting. Now we talk.

[sol](https://forum.hypercore.one/u/sol) November 15, 2023, 7:11pm  207

Interesting suggestion. Perhaps we can work on this problem iteratively and harden PoW in the future. The additional complexity will delay dynamic plasma at this time.

I expect the initial feeless dynamic plasma implementation will be [similar to this](https://docs.vite.org/vite-docs/reference/quota.html), though I still think we need account-level dynamic constraints and cooldowns.

I don’t think it will impact at all. We can use 3 algos to begin with:

*   SHA3 we currently have
*   `RandomX`
*   [Equix](https://github.com/tevador/equix)

2 CPU friendly and 1 ASIC friendly alogs.

[Chadass](https://forum.hypercore.one/u/Chadass) December 28, 2023, 10:26pm  212

Let’s focus on technical discussion and keep the armchair speculative shenanigans in TG sers

My dynamic Plasma proposal can be found within the Phase 1 discussion:
