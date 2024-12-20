Title: Zenon Network: Merged Mining Bitcoin - Zyler9985 - Medium

URL Source: https://medium.com/@Zyler9985/zenon-network-merged-mining-bitcoin-fb7ccf60161e

Published Time: 2023-12-09T19:10:01.556Z

Markdown Content:
[![Image 9: Zyler9985](https://miro.medium.com/v2/resize:fill:44:44/1*KaL4NYzSxXL6fDt1krksEA.png)](https://medium.com/@Zyler9985?source=post_page---byline--fb7ccf60161e--------------------------------)

This article aims to present an overview for how and why Zenon would implement merged mining with Bitcoin. Alienc0der shared his ideas in the dev forums, and the resulting discussion formed the basis for this article. There may be another dev team with different ideas on how to approach merge-mining, and even Alienc0der may refine his proposal so as such consider these ideas subject to revision, debate and iteration. But they are so exciting they are worth sharing as an article. Let’s go!

## We are going to cover:

1. How would the miners get paid?
2. Who are the miners?
3. How will the mined BTC be used?
4. How safe/decentralised is the shared-custody TSS BTC vault?
5. Why would miners want to join Zenon?

Disclaimer: This article is not financial advice and may contain speculation

![Image 10](https://miro.medium.com/v2/resize:fit:700/1*b4BvaM2V8zRo3VnfZw7cDw.jpeg)

1. How would the miners get paid?

---

Zenon Network as a protocol emits ZNN and QSR to the “participants” of Zenon Network. There are 5 participants: Pillars, Sentinels, Delegators, Stakers and Liquidity Providers. Their emissions are different, for example Pillars earn only ZNN, and they are allocated 50% of the ZNN which is minted daily. Note: Pillars can change what percentage of their rewards to share with their delegators, from 0% to 100%.

One possible implementation of the merged mining is to create an additional 6th participant: Miners. The allocation of protocol emissions would need to be redesigned. To give an arbitrary example; Pillars and Delegators could have their emissions decreased to allow for say 10% of the ZNN minted daily to be allocated to Miners.

The Miners are using their powerful hardware to mine BTC, but they are not paid in BTC. The BTC is considered a ‘public good’ and is held in a shared-custody TSS vault. **How will that BTC be used? How safe is the vault?** We’ll get to that later, but first we need to understand how the Miners are getting paid.

As explained above, the Miners are rewarded in ZNN protocol emissions (in this example, 10% of the ZNN which is minted daily). They are rewarded in proportion to the hash power they contributed while mining BTC. The Pillars will be “the accountants” to determine and verify who contributed the most hash, and should therefore be given more ZNN. For example, a powerful miner who is contributing 30% of the hash power to mine BTC for Zenon’s vault will be given 30% of the ZNN which is allocated for miners; and 30% of the 10% allocated for miners means that miner will be earning 3% of the ZNN which is minted daily.

So Miners are competing with each other to earn more ZNN, which should lead to more powerful hardware to gain an advantage … and while they are doing that, Zenon Network as a whole benefits because it means that more Bitcoin is being mined and stored in the vault.

2. Who are the miners?

---

There is an important distinction to make. There are two types of miners in Zenon, and they mine different things. We’ll use experimental nomenclature for the sake of clarity.

1.  The **primary miners** in Zenon are the **Zargonites**, and they mine BTC. From a protocol emissions perspective, they are considered a new 6th participant. They are an entity with powerful hardware. They point their hashpower to a Zenon embedded contract and start mining BTC to be sent to Zenon’s BTC vault, and in exchange they are sent ZNN to their SYRIUS address in proportion to the hash they contributed.
2.  The **secondary miners** in Zenon are the **Quavians**, and they do not mine BTC. Recall that to send a transaction in Zenon, users need to generate plasma. One of the ways they can do this is by doing PoW. But the PoW is not wasted, it uses the RandomX algorithm and can therefore be used to merge-mine any compatible cryptocurrency. Because the PoW is recycled, anyone choosing to transact via PoW can be considered a Quavian, at least for that moment.

Note that the Quavians are not really trying to merge-mine; the PoW will mainly be used for other things such as PoW links … but the elegant design of the NoM is such that nothing goes to waste.

RandomX is ASIC-resistant and therefore friendly to small hardware, such as people using their smartphone to transact. This prevents the wasting of PoW. But would the Quavians be rewarded anything, since their hashpower is extremely low? Normally, it’s true that hashpower below a threshold is too small to register. But if an implementation similar to [Braidpool](https://blog.opdup.com/2021/06/30/can-braidpool-reuse-p2pool-components.html) is done, this means users can adjust the difficulty, such that even a very small “share” is added to the sharechain (a sharechain is an accounting system all mining pool protocols use, even though they have variations of it).

3. How will the mined BTC be used?

---

Recall the BTC mined is not paid directly to anyone; it is stored in the shared-custody TSS vault. It will be used to benefit Zenon Network as a whole, and can therefore be considered a ‘public good’.

The mined BTC will be used to pay for BTC block space for smart contracts to be executed on Zenon. The Taproot upgrade for BTC allowed for Tapscripts to be more complex (via a de facto increase in character limit). So Zenon will have a system in place to sustainably mine BTC and pay for Tapscripts which it will use for smart contracts: **Unlocking DeFi with native Bitcoin**.

What can also be done is the BTC in the vault is used to back ‘zBTC’ which will be minted as a new ZTS, such that you will have a representative BTC on Zenon which enjoys all the characteristics of a ZTS such as feeless (if you compute PoW or fuse/lock/stake QSR), fast transactions and privacy too if it is used in a PTLC atomic swap.

## **4\. How safe/decentralised is the shared-custody TSS vault?**

The BTC will be in a shared-custody TSS vault. Let’s break that down.

TSS technology is complicated to build, but simple in what it is trying to accomplish. From a total of T participants, you need at least N participants to agree for a decision to go ahead. Failure to meet the threshold — then nothing happens. For example, there is a corporate boardroom with 10 executives. Some of them want to spend money from their treasury on an advertising campaign. If the threshold is 8, then at least 8 of the executives need to agree and sign the document to allow the spending of funds.

In Zenon the vault is controlled by the Pillars, but in the future the vault might be controlled by a larger set of participants by leveraging [Mithril Protocol’s](https://mithril.network/doc/) STM (Stake-based threshold multisignatures).

So it could be that a Pillar’s vote only counts if it has a minimum weight of delegation, which is a sign of trust — this not only mitigates the potential for a bad actor to push things through, but it also makes the process more inclusive and democratic for all. This can even be applied for the ZIPs framework, such that it is more like the network’s capital votes, rather than the network’s validators. So the vault is as safe as Zenon is decentralised, and you can read more about Zenon’s decentralisation here:

5. Why would miners want to join Zenon?

---

Firstly, how does Bitcoin as an ecosystem benefit? Not only does Zenon’s DeFi with native BTC enrich Bitcoin’s ecosystem, but Zenon’s miners are increasing Bitcoin’s overall hash power and security. Furthermore, Zenon as a decentralised BTC mining pool protocol will hopefully grow and compete with the existing BTC mining pools which have centralisation concerns (the top 3 control approximately 80% of the hash rate). Challenging the top 3 to fracture their dominance is an ambitious and righteous goal.

Secondly, how do individual Bitcoin miners benefit? We just covered that by helping Bitcoin’s ecosystem overall, it should increase the value of their BTC bags, so there’s that. But also, the more BTC is mined for Zenon’s vault? It enables Zenon to put that BTC to good use, which should increase the overall value of Zenon’s ecosystem … meaning that ZNN should go up in value, and the miners are being paid in ZNN remember?

Finally, there is talk of using Bitcoin’s security to anchor Zenon’s consensus protocol — an essential milestone in realising Zenon as a true hybrid of PoW/PoS. This is important as hardcore Bitcoiners will always regard a pure PoS network as something with weak security.

Perhaps there are more reasons, but these are the ones that come to mind. Miners will want to join Zenon because of a mutually beneficial relationship where their BTC becomes more valuable, the ZNN they are paid becomes more valuable, and they may even be paid more ZNN if they are competitive with generating hash power relative to the other miners. And finally, because Zenon will be a true PoW/PoS hybrid network.

The competitive nature of mining BTC led to the creation of mining pools, as by pooling your resources together you were more likely to find a block to be rewarded. It sucks that you have to share your reward with other members of the pool, but it’s better than no reward at all. This game-theory has continued until now the top 3 pools control roughly 80% of the network’s hash. Fortunately, there’s been a shift away from traditional setups towards peer-to-peer protocols. Before a central operator could abuse their power to do opaque accounting like unfair payouts and fees, as well as censor transactions. Peer-to-peer protocols are trustless by design and aligned with the ethos of eliminating third parties from transactions.

You have to wonder, what would happen if a decentralised network (as a subset of its functionality) acted as an alternative and unique BTC mining pool protocol? Especially with the positive feedback loop potential? The vulnerabilities and shortcomings in peer-to-peer protocols may become apparent as Zenon shows via contrast. Like with Ethereum, sometimes you don’t notice how bad it is until a competitor comes along who does everything better and is amazing in all the ways they are not.

## Conclusion

A huge shoutout to Alienc0der for sharing his ideas on the dev forums and for answering questions from the community in the comments. Here is one of his remarks in his parting thoughts:

“Zenon can become the first decentralized network to simultaneously mine, hold and use on-chain BTC trustlessly, providing added value and acting as a Bitcoin L2. There would be a symbiotic relationship with Bitcoin by providing hashrate in exchange for block space (mine & pay sats/vbyte).”

Alienc0der paints an exciting and rousing picture to say the least. Zenon is uniquely positioned to be able to implement these ideas, because unlike other networks Zenon is truely decentralised and every facet of its design is optimised to deliver maximum scalability. When you consider that to create a decentralised validator set — done properly and honestly — it is a process which takes years. For that reason alone, Zenon may already have an insurmountable lead against competitors … food for thought.

## Thanks for reading!

– Zyler

## Sources

Forum discussions [HERE](https://forum.hypercore.one/t/nom-as-p2p-mining-infrastructure-for-bitcoin/239/19), [HERE](https://forum.hypercore.one/t/the-p2p-revolution-decentralizing-decision-making/267/2) and [HERE](https://forum.zenon.org/t/nom-as-decentralized-p2p-bitcoin-mining-pool/1685/9).

## Join The Community

[Zenon.Network](https://zenon.network/)[Twitter/X](https://twitter.com/Zenon_Network)[Telegram](https://t.me/zenonnetwork)
[Discord](https://discord.com/invite/zenonnetwork)
**Zenon Community Public Key:
**npub1msvlamqj6j5azykts7sewtzr062a0km0p4hajw2dmchtm5xpz0aqylw09w

## The Zyler Reading List

1.  [**The Zenon Storybook**](https://twitter.com/zyler9985/status/1735373467577663905) (updated version coming soon)
2.  [**Progressive Decentralisation**](https://medium.com/@Zyler9985/zenon-network-iii-game-theory-for-progressive-decentralisation-38f94457b03e)
3.  [**A Blistering Need For Speed**](https://medium.com/@Zyler9985/zenon-network-a-blistering-need-for-speed-ce34246c2f01)
4.  [**Alien Plans For Bitcoin**](https://medium.com/@Zyler9985/zenon-network-viii-alien-plans-for-bitcoin-804e1ba60a3c)
5.  [**Why Zenon Is Regulation-Proof**](https://medium.com/@Zyler9985/why-zenon-is-regulation-proof-b696c3a03d0d)
6.  [**Zenon’s Synergy With Nostr**](https://medium.com/@Zyler9985/zenons-synergy-with-nostr-c36fe2bf955c)
7.  [**Merged Mining Bitcoin**](https://medium.com/@Zyler9985/zenon-network-merged-mining-bitcoin-fb7ccf60161e) (updated version coming soon)
8.  [**How Zenon Mirrors The Bitcoin Ethos**](https://medium.com/@Zyler9985/how-zenon-mirrors-the-bitcoin-ethos-142300e59e64)
9.  [**The Zenon Ethos**](https://medium.com/@Zyler9985/the-zenon-ethos-4e0ab0dff12b)
10. [**Zenon Network: A Noir Story**](https://medium.com/@Zyler9985/zenon-network-a-noir-story-a06cc8945439)
11. [**The Dream of Satoshi’s Ethereum**](https://www.slideshare.net/zylert888/the-dream-of-satoshis-ethereumpdf)
12. Zenostroin (Coming 2024)
