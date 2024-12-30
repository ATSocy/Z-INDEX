Thread: merge-mining-feasiblity
MoonBaze | 2024-02-26 14:20:53 UTC | #1

To delve right into the topic, merge mining is the concept of mining 2 different chains at once, without splitting the processing power, while only looking for one nonce because the block templates are the same. The only difference is the difficulty. The main blockchain, in our case Bitcoin, will have the main net difficulty and the other chain (share chain) that will be implemented into an embedded will have a lower difficulty. Once in a while, when a miner finds a good nonce ( solution / share ) for the share chain, the resulting hash will also be good for the Bitcoin main net, that block will be broadcasted and accepted by the network. And so, we mined 2 blocks for 2 networks in the same time.

How can this concept be implemented on Zenon Network?
We will need 3 main components: Embedded Contract, Miners, Hauler ( Proxy between them )

1. Embedded Contract with the following roles:
* Maintain a list of Bitcoin block headers. 
This is needed so that the hauler can use this as source of reference when creating the block template.
Creating a block template requires the following fields:

1. **version** - This 4-byte little endian field indicates the version of the Bitcoin protocol under which the node is publishing the block.
2. **hashPrevBlock** - This 32-byte little endian field is the double SHA256 hash of the previous block header. This forms the edge of the previous block that joins it to the blockchain DAG.
3. **hashMerkleRoot** - This 32-byte little endian field represents the Merkle root of the Merkle tree that contains the transactions which are timestamped in the block.
4. **time** - This 4-byte field is the Unix epoch timestamp that is applied to all transactions in the block. Current network policy only requires this value to be accurate within 2 hours of the validating nodes’ local timestamp. The timestamp has 1-second precision.
5. **bits** - This 4-byte field yields the difficulty target value of the proof-of-work) puzzle, as determined by the network rules.
6. **nonce** - This stands for ‘number used once’. The values of this 4-byte field are cycled through to modulate the block header. The hash of the header is then checked against the difficulty target. Nodes provide adequate information such that when all 4.3 billion values of a nonce have been tried, they can modulate the input field in the block’s coinbase transaction and recalculate the Merkle root. This changes the serialized string of the block header, giving another 4.3 billion unique nonce values to iterate in their search for a hash puzzle solution under the difficulty target. 
</br>Knowing this, the constant values will be version, hashPrevBlock, bits, time and can be fetched from the embedded. The variable ones are nonce ( which will be submitted when providing the share) and the merkle root hash. Here it is a little bit tricky. This hash can be constructed from the hashes of all the transactions that will be included in the block, in a particular order, including the coinbase one ( in our case it need to have the destination address the TSS address, or whatever we use to hold the coins ). When a miner is submitting a share, we need to prove that the merkle root hash is constructed from a list of transactions that contains the correct coinbase transaction ( that has TSS address as destination ). The only way to prove this is to reconstruct all the hashes that lead to the merkle root. The most trivial way is to send all transactions when sending the share so the embedded can reconstruct and check it. We cannot do that as that would mean each miner would send every few minutes ( 2500 hashes * 32 bytes ). What we could do, as we only care about the coinbase transaction is this: send only the hashes needed (the ones in red squares) to reconstruct the root using only the coinbase transaction ( which must be known by the embedded ) . </br>
![image|690x291](upload://e7gtDLGSloIOnu0OVRKnhdEq5Fk.jpeg)
</br>This way each share would contain log 2 of n hashes, where n is the number of transactions in a Bitcoin block. log 2 of 4096 is 12. Let's upper bound this to 13 maybe, we would have 13 * 32 bytes which is a lot less for now. I will think of other ways we could still optimize this in terms of chain space and I also ask you to come with new ideas on how to validate that a share ( constant values + nonce + merkle root) contains the correct coinbase transaction. Also, the randomness space comes from nonce, and the input  field of the coinbase transaction (4 more bytes). So we could accept every coinbase transaction as long as the destination address and amount is correct. Maybe we could have more TSS addresses, so more randomness space for miners and accept any (just an idea).
</br>Here we also need a mechanism on the correctness of the Bitcoin header blockchain. We could have a committee where every member would send a transaction specifying which one is the next block header ( when a new Bitcoin block is mined ) and the one with a majority is cemented. This leads to space overhead in time. One other option would be to have an algorithm that decides which member should post the next header and if others believe it is wrong or he does not post, they could intervene.

* Maintain a database of each share submitted for the share chain
</br>We need to track how many correct shares each miner sent so that we could incentivize them.

* Maintain a difficulty and block time logic 
</br>The same mechanism as Bitcoin's so share chain has a block time of 2-3 minutes. This is just an example, the topic open for debate, higher time means lower space for our chain as less shares would be sent.

* Algorithm to pay the miners
</br> Each miner would be paid based on how many shares he sent in an epoch and the total number of shares from that epoch. They will be paid in ZNN and (why not ?) BTC ( as ZTS or some way, after we actually mine a block, just an idea for now). Here we need to discuss where to get the ZNN from. We could decrease the percentages of rewards from other contracts (Pillars, Sentinels, LP providers)

* In the future we could have 2 share chains, one for small miners like CPU and one for ASICs or Graphics Card.

2. Hauler ( I came up with this name as it is a very important component on actual physical mining and it is used to transport almost everything to and from the mine )
</br>Its role is to gather information about Bitcoin mempool, Embedded latest block header and coinbase transaction template, send jobs to the miner, send shares to the Embedded and broadcast a valid Bitcoin block if found.
</br> It needs a connection a Zenon node, it needs a connection to a Bitcoin full node so he knows the mempool and can construct a valid mining job (using the transactions) for the miner.
</br> It needs to handle multiple miners and know how to distribute jobs so that no redundant work is done ( a nonce is not tried twice by two different miners )
</br> **Very important note**, every hardware owner should run its own hauler as connecting to any other ones, means that the jobs received could be tampered with and the coinbase transaction would be different. ( You could mine for them actually, even if only a percent of the jobs are tampered )

3. Miner
</br> Every miner that is compatible with the Stratum protocol can merge mine! :pick:  :hammer_and_pick:  :pick:
It just needs a connection to a Hauler. 

This post shows that implementing merge mining on the Zenon Network is feasible, we still need to discuss the details on the topics that I've mentioned. Also, any other ideas, complaints, optimizations about my view are very welcomed! I hope I did not miss any information, but will edit the post if so, and will gladly answer questions.

-------------------------

0x3639 | 2024-02-26 13:33:39 UTC | #2

Thank you for your post.  Can you please clarify these two items?

[quote="MoonBaze, post:1, topic:381"]
Once in a while, when a miner finds a good nonce ( solution / share ) for the share chain, the resulting hash will also be good for the Bitcoin main net, that block will be broadcasted and accepted by the network. And so, we mined 2 blocks for 2 networks in the same time.
[/quote]

Does this make finding a BTC block even harder than mining BTC individually?  What if the miner finds a solution to the main chain (BTC) but that solution does not work for the share chain (NoM).  Or is that not possible because we share a "block template"?  Not sure how that works if the difficulty adjustment and time frames are different between BTC and NoM.

[quote="MoonBaze, post:1, topic:381"]
**Very important note**, every hardware owner should run it’s own hauler as connecting to any other ones, means that the jobs received could be tempered with and the coinbase transaction would be different. ( You could mine for them actually, even if only a percent of the jobs are tampered )
[/quote]
Meaning, anyone who wants to Mine, needs to run their own hauler?

-------------------------

MoonBaze | 2024-02-26 14:19:39 UTC | #3

> Does this make finding a BTC block even harder than mining BTC individually?

It is not harder, it is the same. A better example. Let's say BTC hash threshold is 10,  and share chain threshold is 100. If a miner finds a nonce that leads to a hash with value 50, it is good for the share chain but not good for BTC. If a miner finds a nonce that leads to a hash with value 5, it is good for both because the chains have the same block template and the same latest block. The only difference is in difficulty

> What if the miner finds a solution to the main chain (BTC) but that solution does not work for the share chain (NoM)

If no Hauler is modifying its source code, that would not be possible. Otherwise he would just be mining something else.

>  Not sure how that works if the difficulty adjustment and time frames are different between BTC and NoM.

Do not think about our consensus and 10 seconds time delay between momentums. It has nothing to do with this. All the logic I have explained will be implemented in the embedded. The emebedded will contain the share chain

> Meaning, anyone who wants to Mine, needs to run their own hauler?

Yes and no. You could connect to anyone but the Hauler will be the one that sends the share so connecting your miner to others Hauler means that he could send you modified jobs ( for example find the nonce for this template that contains my coinbase tx not the one from embedded and if you find it you will mine a block for him) or he could send some correct share for the share chain as coming from him instead of you. 
If you trust the other one you could connect to him sure

-------------------------

0x3639 | 2024-02-26 13:46:16 UTC | #4

Thanks.  That make sense!

-------------------------

coinselor | 2024-02-26 15:21:40 UTC | #5

Appreciate the in-depth explanation.

[quote="MoonBaze, post:3, topic:381"]
It is not harder, it is the same. A better example. Let’s say BTC hash threshold is 10, and share chain threshold is 100. If a miner finds a nonce that leads to a hash with value 50, it is good for the share chain but not good for BTC. If a miner finds a nonce that leads to a hash with value 5, it is good for both because the chains have the same block template and the same latest block. The only difference is in difficulty

[/quote]

I'm glad 0x asked, this ELI5 explanation helped a lot!

Here's a few more newbie questions:

- It seems the randomness space of only 4 bytes is a concern, as you pointed to a few workarounds to increase it. Is this only a concern as difficulty increases? Is the nonce space much larger for btc? Why is ours limited to 4 bytes?

- I assume optimizations around increasing chain weight are because data will live forever in the embedded contract, so in every full node moving forward? Couldn't we prune historical data after certain intervals? 

- Embedded/NoM has no connection to a bitcoin full node. Is the idea that "a committee", say like the orchestrators now, will be running a bitcoin full node and submitting the required data to the embedded node as NoM transactions? Couldn't this "agreement" be done off-chain? 

Hauler is a great name!

-------------------------

MoonBaze | 2024-02-26 18:09:26 UTC | #6

> It seems the randomness space of only 4 bytes is a concern, as you pointed to a few workarounds to increase it. Is this only a concern as difficulty increases? Is the nonce space much larger for BTC? Why is ours limited to 4 bytes?

We have the same random space as BTC. Randomness comes from nonce ( 4 bytes ) and from merkle root hash, (maybe also from timestamp). We can change the merkle root by changing the coinbase transaction's input field (4 bytes) or by changing the order of any two transactions, or by adding / removing transactions. Each of these actions result in a different merkle root hash, hence a different block template. There are options, we just need to be efficient.

> I assume optimizations around increasing chain weight are because data will live forever in the embedded contract, so in every full node moving forward? Couldn’t we prune historical data after certain intervals?

We could let's say keep in storage only the headers of the last 100 blocks but what we cannot delete is when a Hauler sends in an account block the share of the miner that **must** contain the necessary data to prove that the list of transactions whose merkle root hash is mentioned, contains the correct coinbase transaction ( which as we speak contains the nonce + at most 13 * 32 bytes, for sure other data we will see. For 1000 miners we are speaking about 0,4 MB every 2-3 minutes.

> Embedded/NoM has no connection to a bitcoin full node. Is the idea that “a committee”, say like the orchestrators now, will be running a bitcoin full node and submitting the required data to the embedded node as NoM transactions? Couldn’t this “agreement” be done off-chain?

Theoretically yes, we would have p2p network between haulers, each would send others their shares ( nonce + the 13 hashes) and by some mechanism they could agree on the correct ones and only send some account blocks to specify who mined how many shares. This seems more complex and with other problems that need to be solved like how could you tell a share (basically nonce + merkle root hash) comes from a hauler after he broadcasts it, roles for who can send the account block to account for shares and so on.

> Hauler is a great name!

:man_construction_worker:

-------------------------

0x3639 | 2024-02-27 14:06:51 UTC | #7

[quote="MoonBaze, post:6, topic:381"]
For 1000 miners we are speaking about 0,4 MB every 2-3 minutes.
[/quote]
Thats around 84G per year.  If we had 10,000 miners it would be 840G per year.  Do you think that is a problem?  Maybe not initially.

-------------------------

aliencoder | 2024-02-27 21:34:47 UTC | #8

[quote="MoonBaze, post:1, topic:381"]
a mechanism on the correctness of the Bitcoin header blockchain
[/quote]

[quote="MoonBaze, post:1, topic:381"]
the one with a majority is cemented
[/quote]

This can be signed via TSS off-chain for agreement and published on-chain.

[quote="MoonBaze, post:1, topic:381"]
means that the jobs received could be tampered with and the coinbase transaction would be different.
[/quote]

We can create a mechanism to slash malicious Haulers that change the TSS coinbase address for example by requiring an upfront `ZNN` collateral.

-------------------------

aliencoder | 2024-02-28 23:14:15 UTC | #9

The main bottleneck that we encounter is chain bloating. More specifically bloating the merge-mining embedded account-chain.

[quote="0x3639, post:7, topic:381"]
Do you think that is a problem?
[/quote]

MrK emphasized that we should keep the base layer minimal.

We need to find a solution for *efficient* on-chain storage (and processing) of valid share-blocks.

[quote="MoonBaze, post:6, topic:381"]
For 1000 miners we are speaking about 0,4 MB every 2-3 minutes.
[/quote]

Here zero-knowledge proofs are coming to the rescue.. more specifically [Merkle proofs](https://zk-plus.github.io/tutorials/basics/merkle-proof).

[quote="MoonBaze, post:1, topic:381"]
![image](upload://e7gtDLGSloIOnu0OVRKnhdEq5Fk)
[/quote]

"To generate a proof, we need to provide the hashes of the sibling nodes along the path from this leaf that result in the Merkle Root.

zkSNARKs allows to prove the possession of a valid Merkle Proof without disclosing the candidate element or the Merkle Path.

Merkle proofs enable demonstrating that a certain element is a part of a given set without revealing which element it is. The Merkle Tree stores a list of elements, and the zkSNARK is used to prove knowledge of a path from a leaf element to the root of the Merkle Tree. By executing the Merkle Proof inside a zkSNARK, the candidate element and the Merkle path can be kept private".

Basically, we only need to post the Merkle zk-proof on-chain and verify it.

-------------------------

MoonBaze | 2024-03-05 10:49:20 UTC | #10

I have played with https://github.com/hashcloak/merkle_trees_gnark and using only the hashes in red ( described above) we can actually reduce the space from a maximum of 13 hashes of 32 bytes to 4 (maximum 5 hashes) of 32 bytes which is a great improvement so far. Very good idea to execute Merkle Proof inside a zkSNARK.

-------------------------

MoonBaze | 2024-04-04 16:36:19 UTC | #11

I might need some help implementing the Stratum part. We need to find someone who knows Golang and Stratum protocol and is willing to help with the server part. I can handle the embedded and everything else. If you know anyone willing to help, not for free of course, that would be perfect.

-------------------------

sugoibtc | 2024-04-04 19:32:56 UTC | #12

[quote="MoonBaze, post:11, topic:381, full:true"]
I might need some help implementing the Stratum part. We need to find someone who knows Golang and Stratum protocol and is willing to help with the server part. I can handle the embedded and everything else. If you know anyone willing to help, not for free of course, that would be perfect.
[/quote]



Are there any other specific skills that you are looking for in a person? We might be able to do some outreach in order to find someone.

Will the payment be through A-Z funds?

-------------------------

0x3639 | 2024-04-04 21:10:39 UTC | #13

Here are the contributors on their repo.  They must know a thing or two about Stratum.  

https://github.com/stratum-mining/stratum/graphs/contributors

-------------------------

0x3639 | 2024-04-04 21:16:00 UTC | #14

This guys knows what's up.

https://github.com/GitGab19

-------------------------

MoonBaze | 2024-04-05 18:55:42 UTC | #15

I just need someone who can write a stable Stratum server for our needs, which are actually standard for merge mining. It can also be a different binary and not written in Golang.

The payment should be from AZ, they could just sell for ETH. I could pay him upfront with some starting ZNN and then get it back.

-------------------------

Shuccck | 2024-04-06 16:57:25 UTC | #16

This is something I can work on! Thanks to @sugoibtc for telling me about this platform and this in particular

-------------------------

MoonBaze | 2024-04-09 09:06:12 UTC | #17

Update:
I have started to work on the Embedded Contract after lots of documentation on how mining actually works in technical terms and planning the implementation. You can follow the progress here: [git](https://github.com/MoonBaZZe/go-zenon).
So far I have implemented the logic to store a Bitcoin header chain, add / edit share chains with custom difficulties (maybe different reward multiplier based on the difficulty), copied all the security from Bridge with administrator, guardians and the TSS address. Also tests follow the same design as the one from Bridge because they seem very well written and are easy to use.

Me and @Shuccck are in contact and we have agreed that he will work on the Stratum server under my guidance.

I will now work on accepting the shares logic with that ZK circuit and leave the rewards part at the end. I am also thinking to create a custom update for this contract so we update after / before a few momentums of the pillar update because sometimes it is very slow. The rewards will be based on how much PoW each address has brought, per epoch (24h), so far.

After having a stable version of embedded I will also start to work on the Hauler and then just integrate the Stratum server because it will be coded as a github repo in Golang so I can just import it as a module.


We must decide on where should the rewards come from? Reduce from other percentage? Mint extra?
Should we increase the rewards amount as hash rate increases so we continuously stimulate new miners to come? Come with ideas.

-------------------------

Bzed | 2024-04-09 22:59:42 UTC | #18

Theres plenty of rewards to go around from the current distribution but its hard to say whats an ideal ratio for all participants without knowing the role Sentinels are going to play.

Aside from that, staking and delegating could easily be cut by 1/4 to 1/3 and still hand out well over 8% APR. When compared to mainstream yields thats still healthy. 

Pillars imo do not need a reduction in rewards they need as much incentive as possible right now. 

Then LP could stand to reduce too but with other pool options coming up in the short/medium term like QSR and maybe others that portion of rewards is likely going to be diluted anyways so could be left as is to help compensate for its higher risk.

-------------------------

aliencoder | 2024-04-10 09:13:50 UTC | #19

[quote="Bzed, post:18, topic:381"]
Aside from that, staking and delegating could easily be cut by 1/4 to 1/3 and still hand out well over 8% APR.
[/quote]

Even a 1/3 & 1/2 reduction will get you a healthy APR.

[quote="Bzed, post:18, topic:381"]
Pillars imo do not need a reduction in rewards they need as much incentive as possible right now.
[/quote]

Agree. They do the heavy lifting right now: running critical infra including the `orchestrator layer` and the `extension-chain`.

[quote="Bzed, post:18, topic:381"]
Then LP could stand to reduce too but
[/quote]

Agree here as well. Hopefully we'll see other chains connected in the near future.

I would also bring up in the discussion Sentinels. They aren't actively participating in the network and we can redirect extra value towards the miners.

A beautifully balanced landscape of participants will emerge:

- Users -> feeless transactions, bridge incentives
- Devs -> AZ grants
- Miners -> protocol emission
- Stakers -> protocol emission
- Delegators -> protocol emission
- Liquidity Providers -> protocol emission
- Sentries (TBA) -> protocol emission
- Sentinels -> protocol emission
- Pillars -> protocol emission, extension-chain incentives

We'll also need a sustainable way to replenish Accelerator-Z for devs.

-------------------------

MoonBaze | 2024-04-17 13:55:03 UTC | #20

Update:
The [hauler](https://github.com/MoonBaZZe/hauler) is starting to look good on the znn part, there are still some things to implement on btc part. 
The [sdk](https://github.com/MoonBaZZe/znn-sdk-go/tree/merge-mining) is also up to date.
The [stratum](https://github.com/Shucck/go-stratum-server) server is being developed and updated to be compatible with the logic of the hauler.
In the next days, I will put on a testnet and see how the hauler behaves and then connect some miners. 

I am also thinking that everyone could run a hauler architecture with a znn fee, ( 1 / 20 shares will go to the owner of the hauler for example), miners would just need an ip to connect and the mining will start immediately, without any additional setup.

-------------------------

0x3639 | 2024-04-17 14:07:09 UTC | #21

[quote="MoonBaze, post:20, topic:381"]
The [stratum ](https://github.com/Shucck/go-stratum-server) server is being developed
[/quote]

Are you able to work with the dev @sugoibtc introduced us to?

-------------------------

Weather.Man | 2024-04-18 06:19:01 UTC | #22

Have you thought about the incentive and fee structures any further? 

There are still parts of your proposal I don't really understand. 
Say I'm a miner and point my equipment to the hauler ip and start hashing, what happens if the pool finds a block and I want withdraw my Bitcoin, how is the accruing of shares of the bitcoin handled? Where is it stored and how does it get withdrawn

I don't really see any connective tissue around the mining that enables this, but maybe I'm just not looking. 

Furthermore I think the incentives are an issue, it doesn't seem right that you or any other dev can decide what the rewards for everybody else should be.
Above it is discussed that 1/2 reduction is still a healthy APR.

I think that it is pretty obvious that it is incredibly unattractive for investors if devs can or will just on a whim slash rewards by half for investors. That does not fall in line with decentralized ethos and I doubt it will find broader support. 

In my opinion to change things like rewards there needs to be a governance mechanism in place and this cannot just be the arbitrary decision of a developer.

A recent example of this how what may have initially seemed clever but probably was a mistake is the bridging fee. Touted as self sustaining marking marketing mechanism it has failed to create any momentum at all and if anything has people skeptical to bridge and caused confusion.
During the last pump many people were in the telegram confused about this fee.

Further more now that we are getting CEXs soon we can see the somewhat silly loophole this has created. A person can buy wZNN on uniswap get a 3% percent bonus and then eventually sell on a CEX without spending the 3% penalty for bridging back. 
Meaning that over time the wrapped znn on ETH will be probably be useless as nobody will bridge to sell.

So this goes to go show that 'clever' ideas can easily be the opposite, Just something to keep in mind.

-------------------------

Weather.Man | 2024-04-18 06:13:51 UTC | #23

I read through your original post again and can see how you are proposing to keep track of the shares.
I do see though that the original post plans to pay miners in ZNN and not BTC.

Honestly I really don't see the point to any of this - it feels you are trying to shoehorn in a mining pool without any clear purpose or goals. 

Please try and take a counter point and show why a miner would use their expensive hardware to mine for znn, what a bitcoin mining pool would accomplish for the network and why network emissions/rewards should be diverted to this, why is it advantageous for the mining pool to keep the bitcoin, what purpose will that serve? 

Have you considered maybe offing a mining pool with zero fees to miners and all they would need to pay are transaction fees for withdrawing from the pool? Something like this would be very useful and I think would get broad support.

-------------------------

Stark | 2024-04-19 10:35:33 UTC | #24

This seems opportune.

![IMG_2802|442x500](upload://A4xjfXS6otkXX1jRXn0ehlgr11j.jpeg)


https://x.com/callebtc/status/1781264396670345652?s=46

-------------------------

MoonBaze | 2024-04-22 10:00:52 UTC | #25

Thank you for your input, those are some valid things to consider.

> Say I’m a miner and point my equipment to the hauler ip and start hashing, what happens if the pool finds a block and I want withdraw my Bitcoin, how is the accruing of shares of the bitcoin handled? Where is it stored and how does it get withdrawn

We can use a 1:1 zts to bitcoin and they would be able to withdraw using HTLC / PTLC. We could wrap the bitcoin on ethereum and people could just bridge it.

> Furthermore I think the incentives are an issue, it doesn’t seem right that you or any other dev can decide what the rewards for everybody else should be.

This is why I asked here on the forum, I don't intend to take the decision by myself. I want us, as a community, to find the optimal solution.

> I think that it is pretty obvious that it is incredibly unattractive for investors if devs can or will just on a whim slash rewards by half for investors. That does not fall in line with decentralized ethos and I doubt it will find broader support.

No dev has that power, he just proposes and the pillars will vote and actually run the new code eventually. It's still decentralized, but a dev can come with an idea and implementation which, based on the community input, reaches a form that satisfies a majority.

> In my opinion to change things like rewards there needs to be a governance mechanism in place and this cannot just be the arbitrary decision of a developer.

If we wait for that, we would miss a lot of new ideas

> Honestly I really don’t see the point to any of this - it feels you are trying to shoehorn in a mining pool without any clear purpose or goals.

We will be able to have BTC as a store of value for the network as it's scarcity increases. We could use them as funds for further projects ( supposing we only pay a percentage to miners, not 100% and the rest in ZNN).

> Please try and take a counter point and show why a miner would use their expensive hardware to mine for znn

I am pretty sure that a miner will come where it's most profitable, despite it's actual cost of equipment. At the beginning we won't have that many Bitcoin blocks mined so less BTC rewards, but they will get Znn. Probably miners with older equipment will come at first, because they earn so little on the current pools base on their hash power.

> what a bitcoin mining pool would accomplish for the network

In the future we can integrate the produced PoW into our consensus, enhancing security. NoM, secured by Bitcoin miners.

> why network emissions/rewards should be diverted to this

This can be seen as V1, we won't just be a mining pool, we will benefit from the gained PoW in the future and I think this deserves network emissions. Sentinels right now don't offer any value to the network.

> why is it advantageous for the mining pool to keep the bitcoin

I answered 

> Have you considered maybe offing a mining pool with zero fees to miners and all they would need to pay are transaction fees for withdrawing from the pool? Something like this would be very useful and I think would get broad support.

We could do that, yes.

-------------------------

MoonBaze | 2024-04-22 10:31:57 UTC | #26

[quote="MoonBaze, post:25, topic:381"]
the beginning we won’t have that many Bitcoin blocks mined so less BTC rewards, but they will get Znn. Probably miners with older equipment will come at first, because they earn so little on the current pools base on their hash power.
[/quote]

Yes, looking good so far

-------------------------

aliencoder | 2024-04-22 17:44:21 UTC | #27

[quote="Weather.Man, post:22, topic:381"]
I think that it is pretty obvious that it is incredibly unattractive for investors if devs can or will just on a whim slash rewards by half for investors. That does not fall in line with decentralized ethos and I doubt it will find broader support.
[/quote]

The community must agree and adopt those changes. I want to highlight that we don't touch the current inflation, we just rearrange how the inflation is distributed to network participants in order to maximize the potential for everyone in the ecosystem.

[quote="Weather.Man, post:22, topic:381"]
what happens if the pool finds a block and I want withdraw my Bitcoin, how is the accruing of shares of the bitcoin handled?
[/quote]

I've proposed that all the mined BTC will be managed by the network as a collective. For example, a part of the mined Bitcoin can be used to buyback ZNN from a dedicated `BTC/ZNN` protocol level liquidity pool.

[quote="Weather.Man, post:22, topic:381"]
this cannot just be the arbitrary decision of a developer.
[/quote]

This is why we are all discussing this on a public forum.

[quote="Weather.Man, post:23, topic:381"]
Please try and take a counter point and show why a miner would use their expensive hardware to mine for znn
[/quote]

Because the mined BTC will be used (by NoM as a collective entity) to:
- Buy block space and enable Bitcoin smart contracts => programmability for Bitcoin
- Secure NoM by anchoring it (using PoW) into the Bitcoin chain => security for NoM

This will in turn make ZNN more valuable as the network will be more secure and will unlock more uses-cases for Bitcoin as well.

[quote="Weather.Man, post:23, topic:381"]
why network emissions/rewards should be diverted to this
[/quote]

Because there will be another type of network participant (the miners) that will supply PoW and must be incentivized to do so.

-------------------------

MoonBaze | 2024-04-25 12:42:18 UTC | #28

It seems that @Shuccck is a scammer. He is afk for almost a week, we need another Stratum developer in Golang, one that accepts payment after the work is done. @sugoibtc @0x3639
Later edit: he is not a scammer.

-------------------------

sugoibtc | 2024-04-25 08:51:16 UTC | #29

Damn...That sucks to hear man. I tried reaching out to him after he had some wallet questions, but hasn't gotten back to me since the 21st... Did he atleast deliver something that you can work with/pay him out?

-------------------------

MoonBaze | 2024-04-25 12:42:05 UTC | #30

Nevermind he is back, he just got a problem

-------------------------

Weather.Man | 2024-04-25 15:38:11 UTC | #31

[quote="aliencoder, post:27, topic:381"]
Because the mined BTC will be used (by NoM as a collective entity) to:

* Buy block space and enable Bitcoin smart contracts => programmability for Bitcoin
* Secure NoM by anchoring it (using PoW) into the Bitcoin chain => security for NoM

This will in turn make ZNN more valuable as the network will be more secure and will unlock more uses-cases for Bitcoin as well.
[/quote]

This is not part of the post and the ideas he has outlined above. 
There is literally no description on how consensus would be effected by the mining. So really one could say that this is just wishful thinking with no concrete path to accomplish it whatsoever.  

The idea that a Bitcoin miner will use their rigs to mine bitcoin in exchange for ZNN is - in my view - so completely divorced from reality and displays a complete lack of economic understanding to how the Bitcoin mining community operates. This attitude and outlook then furthermore undermines lofty statements regarding anchoring consensus to the mining. 

Anyway good luck with it, interested to see it working on a test net.

-------------------------

coinselor | 2024-04-25 15:55:02 UTC | #32

Disappears and comes back. Already acting like a true alien.

-------------------------

aliencoder | 2024-04-26 18:21:50 UTC | #33

[quote="Weather.Man, post:31, topic:381"]
There is literally no description on how consensus would be effected by the mining
[/quote]

Because this will be implemented at a later stage. The merge-mining will provide 2 benefits for NoM:
- `SHA-256 ASIC proof-of-work` that will provide additional weight for the dual-ledger system
- Anchoring of the consensus into Bitcoin

We need to discuss at a later date how we can actually integrate it into the consensus layer.

[quote="Weather.Man, post:31, topic:381"]
The idea that a Bitcoin miner will use their rigs to mine bitcoin in exchange for ZNN
[/quote]

Merge-mining means that you mine 2 coins at the same time with the same hashpower. I agree that we must align with Bitcoin miners to boost their earnings (to be economically incentivized to participate). You can read more [over here](https://medium.com/iovlabs-innovation-stories/modern-merge-mining-f294e45101a0). Miners with low hashrate will be the first ones to come and merge-mine on NoM.

Another discussion is around what happens with the freshly mined BTC. The miner should be able to choose what happens with the rewards. If they are going to NoM's treasury and they're used in a smart way (buy block space and inject zk-proofs on Bitcoin), this will boost the value of ZNN and subsequently the value of their earnings.

Another way to think about it is that ZNN will be backed by BTC, coupled with an increased utility of ZNN (contracts executing on NoM benefiting from Bitcoin's security).

-------------------------

MoonBaze | 2024-05-08 07:36:07 UTC | #34

I have managed to put on a test net, it runs a hauler that keeps the header chain updated and once I integrate the stratum server will be able to also post shares. Do you know anyone from the community who is willing to create a minimal interface which shows data about the header chain, side chains and shares of the miners?

-------------------------

Shuccck | 2024-07-28 21:03:24 UTC | #35

Hi guys! @MoonBaze has been afk for a month now! The stratum server according to him is already good to go for integration! And as such I should have been have received the balance on our agreement! I’m stuck here guys! I’ve contacted @sugoibtc twice about this but rn i don’t know what to do again
![IMG_4374|231x500](upload://92KG0YLFk1FOZMHCRXy71cDhGPe.png)

-------------------------

edgepillar | 2024-07-28 23:24:39 UTC | #36

maybe @0x3639 can put you in touch with @MoonBaze via [matrix chat](https://forum.hypercore.one/t/matrix-chat-server-for-zenon-development/475) if he is available.

-------------------------

0x3639 | 2024-07-28 23:39:44 UTC | #37

Hello. I can try to help. Can you DM me what you have been paid and what you are owed?  I believe we (@coinselor ) sent some znn urgently a few months back before some work was done. But that is the last I heard of anything.  

Talk soon.

-------------------------

Shuccck | 2024-07-29 06:39:43 UTC | #38

Okay thanks

-------------------------

0x3639 | 2024-07-29 11:05:19 UTC | #39

you can contact me here in the forum or

matrix
@deeznnutz:zenon.chat

telegram
@zerox3639

Just let me know where you are contacting me so I can help.

-------------------------

Shuccck | 2024-07-29 21:07:30 UTC | #40

Okay! I’d text you on telegram! Thanks

-------------------------

MoonBaze | 2024-07-30 10:02:18 UTC | #41

As of today, I have decided I will stop working with Shucck. He was always paid ( 3446.5 ZNN in total ), even in advance for the work he has done and for over a month no task was given to him that would require more payment. I did not have time lately to test the code, integrate it and check what else we need but I am sure it is not complete. I am afk now but when I come back I will work by myself.

-------------------------

Shuccck | 2024-07-30 16:31:33 UTC | #42

![IMG_4777|231x500](upload://8OxeCFDmCjkdrBAmRmmZl2XMA2x.png)

As I said in the chat yesterday! It has come through!

-------------------------

0x3639 | 2024-07-30 16:37:01 UTC | #43

Sounds good.  Thanks for responding.  @Shuccck did contact me via telegram and I mentioned we needed to hear back from you before taking any action.  thx!

-------------------------

aliencoder | 2024-11-18 21:56:43 UTC | #44

The main challenge with the current approach is the amount of data that will end up on the embedded account-chain.

If the merge-mined chain operates at 20x the pace of Bitcoin blocks (with adjusted difficulty), the on-chain storage required for 1 year would be approximately ~2.69 GB. With 100x the pace of Bitcoin blocks (block time around 6 seconds) we will have ~15Gb on-chain storage annualy. We can't go that fast because our current implementation is capped at 10s block time.

This is without using zk-proofs to minimize the on-chain footprint. Depending on what proof system we use, the on-chain storage requirements can decrease with a factor of 2 up to 10x.

Here is a [Circom implementation](https://github.com/Turupawn/CircomMerkleInclusion/blob/master/verify-merkle-path.circom) that verifies the Merkle path:

**Proof Data**: The zk-SNARK proof, which is typically around 128 bytes in size.

**Public Inputs**: In the context of verifying a Merkle path, this would include:

• **Merkle Root**: The root hash of the Merkle tree (32 bytes).

• **Leaf Hash**: The hash of the leaf node (32 bytes).

• **Leaf Index**: The position of the leaf in the tree, which can be represented in a few bytes depending on the tree’s size.

The total on-chain data required for each proof verification would be approximately:

• **Proof**: 128 bytes

• **Merkle Root**: 32 bytes

• **Leaf Hash**: 32 bytes

• **Leaf Index**: ~4 bytes (assuming a tree with up to 2³² leaves)

**Total**: ~196 bytes per proof verification.

We can optimize even more by creating and posting a proof once every 100 share-chain blocks. It's not feasible to create a zk proof for each share-block, that's why batching share-chain blocks is the logical step forward. The share-chain be coordinated off-chain by the mining entities and the on-chain embedded will be required to attest the share-chain integrity and release rewards accordingly. Basically we end up creating a zk-rollup for merge-mining Bitcoin with NoM as DA and settlement layer.

-------------------------

0x3639 | 2024-11-19 00:14:51 UTC | #45

I'm still trying to wrap my head around how merge mining will benefit NoM.

In order for merge mining to be useful to NoM doesn't the consensus protocol need to take into consideration the PoW (by the BTC miner)?  Is this contemplated in the whitepaper and how do we propose to incorporate these changes with Sentinels and N&T?  This sounds like a gigabrain project that requires a massive lift.

Today, the only way a BTC miner will use their equipment to merge mine is if the miner receives their share of the BTC rewards (less a fee).  I don't think we can assume a BTC miner will use their expensive equipment to only earn ZNN while Zenon Network accumulates the BTC.  Is the current design to be a decentralized mining pool where NoM acts as a decentralized "orchestrator" for mining.  We become an [Ocean.xyz](https://ocean.xyz/) of sorts?

In previous posts we discussed miners becoming a new ecosystem player (a new citizen) that was not contemplated in the WP (I think).  This seems like a very large change that requires considerable analysis.  Is someone looking into this?

thx

-------------------------

aliencoder | 2024-11-19 10:02:32 UTC | #46

[quote="0x3639, post:45, topic:381"]
In order for merge mining to be useful to NoM doesn’t the consensus protocol need to take into consideration the PoW (by the BTC miner)?
[/quote]

This is a great question. My idea is to anchor NoM into Bitcoin. But we need to take it step by step.

[quote="0x3639, post:45, topic:381"]
Is this contemplated in the whitepaper and how do we propose to incorporate these changes with Sentinels and N&T?
[/quote]

Afaik the whitepaper mentions ASIC PoW that Bitcoin miners can provide and contribute to ledger weight.

[quote="0x3639, post:45, topic:381"]
Is the current design to be a decentralized mining pool where NoM acts as a decentralized “orchestrator” for mining.
[/quote]

Yes, this is the idea: creating the first decentralized p2p mining pool on BTC. We won't gather much hashpower in the beginning, but we can attract a lot of attention.

[quote="0x3639, post:45, topic:381"]
I don’t think we can assume a BTC miner will use their expensive equipment to only earn ZNN while Zenon Network accumulates the BTC.
[/quote]

Non-competitive BTC miners can redirect their hashpower towards NoM. I agree that we need to incentivize them with both `BTC` and `ZNN`/`QSR` to gather hashpower. That's why we can redirect 90% of the mined `BTC` back to them (directly on NoM as `zBTC`) in the beginning + `ZNN` and `QSR`. After that we can adjust the amount of `BTC`. This is an open discussion.

[quote="0x3639, post:45, topic:381"]
that was not contemplated in the WP (I think). This seems like a very large change that requires considerable analysis.
[/quote]

Actually this is specified in the whitepeper (PoW pools and ASIC hashpower) as well as it's aligned with the core design of NoM as a dual PoS and PoW chain.

-------------------------

0x3639 | 2024-11-19 10:59:42 UTC | #47

[quote="aliencoder, post:46, topic:381"]
Actually this is specified in the whitepeper (PoW pools and ASIC hashpower) as well as it’s aligned with the core design of NoM as a dual PoS and PoW chain.
[/quote]

Thank you for those responses.  This makes more sense to me now.  I'll take a look at the WP again.

-------------------------

0x3639 | 2024-11-19 18:32:02 UTC | #48

From the WP:

"In order for the pillars to be competitive in the process of producing the proof of work, they will have the possibility to outsource it using the mining pool concept. This will create a market-efficient ecosystem that will further strengthen the network and clients committing resources for Pillar pools will be rewarded proportionally to their contribution of processing power."

So I guess the idea is to build a decentralized mining pool that (initially) does not interact with the consensus in any way.  It's "just" a decentralized mining pool where older miners can merge mine zBTC (convertible to BTC eventually) and ZNN/QSR.  I wonder how we can award zBTC with the understanding it will be convertible to BTC without knowing how that will work.  Maybe the miners earn BTC rather than zBTC??

Over time as the project evolves we believe (per the WP) Pillars will need to perform a serious amount of PoW in order to be competitive.  So much so, they will need to outsource that PoW to mining pools through the merge mining concept.    

So by building a decentralized mining pool today on NoM we can more "easily" transition to Pillar PoW outsourcing in the future.

Does that look directionally accurate?

-------------------------

Stark | 2024-11-19 17:37:13 UTC | #49

1. Are noncompetitive BTC miners cost effective in terms of the cost of electricity?

2. Why not target competitive miners?

-------------------------

coinselor | 2024-11-19 18:09:01 UTC | #50

[quote="Stark, post:49, topic:381"]
Are noncompetitive BTC miners cost effective in terms of the cost of electricity?
[/quote]

I think you answered your own question. They are non-competitive for the exact reason that their hashrate per kw produced is lower. Most of these miners are either offline or mining random altcoins with a centralized service that mines alt coins and dumps them for btc while charging middleman fees as they please.

-------------------------

aliencoder | 2024-11-20 21:38:01 UTC | #51

[quote="0x3639, post:48, topic:381"]
Does that look directionally accurate?
[/quote]

I think the main takeaway is the emphasis on the integration of a PoS & PoW mechanism.

[quote="Stark, post:49, topic:381"]
Are noncompetitive BTC miners cost effective in terms of the cost of electricity?
[/quote]

They aren't if they only mine BTC. But this is the idea, to onboard them and create incentives for them to start mining again. This is a win-win for them (they'll earn ZNN and QSR in the process) and they will also help decentralizing the hashrate.

[quote="Stark, post:49, topic:381"]
Why not target competitive miners?
[/quote]

Because we will have a harder time to convert them. We need to first prove the concept and if we get enough traction and have the right incentives, they will come.

-------------------------

