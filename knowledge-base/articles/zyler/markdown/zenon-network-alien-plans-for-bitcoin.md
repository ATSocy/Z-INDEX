Title: Zenon Network: Alien Plans For Bitcoin - Zyler9985 - Medium

URL Source: https://medium.com/@Zyler9985/zenon-network-viii-alien-plans-for-bitcoin-804e1ba60a3c

Published Time: 2023-07-11T08:01:08.376Z

Markdown Content:
[![Image 11: Zyler9985](https://miro.medium.com/v2/resize:fill:44:44/1*KaL4NYzSxXL6fDt1krksEA.png)](https://medium.com/@Zyler9985?source=post_page---byline--804e1ba60a3c--------------------------------)

The purpose of this article is to explain and outline Zenon’s roadmap with specific focus on its hugely ambitious goal of becoming the preferred global platform for DeFi with native Bitcoin.

Disclaimer: This article is not financial advice and may contain speculation

![Image 12](https://miro.medium.com/v2/resize:fit:700/1*Lz7zdTzfR7SLarOvaHfa1A.jpeg)

Bitcoin is a digital energy. But it requires help to do more advanced things at scale.

## Foreword

You cannot simply become the preferred global platform for DeFi with native Bitcoin without meeting certain pre-requisites first. The road to getting there is also long and complex. And ideally you would have read other articles to be familiar with Zenon first. For this article, we are going to break the grand plan into **5** **stages**.

Put simply, it’s a clusterf\*ck to explain all of this, especially given the speculation involved and the fact that I’m just a glorified ape with a typewriter who moonlights as a noob marketer. But there is glory in the attempt!

## STAGE 1 — Achieved

For a sidechain to be accepted by Bitcoiners, the first and most basic pre-requisite is it needs to be decentralised. Decentralised in every way at every level, the early distribution such that the coins are owned and controlled by people not by institutions (which present large & coordinated capital ie. centralisation). Zenon has managed this incredible achievement (read the entire article series to learn more). Zenon mirrors the Bitcoin Ethos in every way and is basically Satoshi’s Ethereum.

## STAGE 2 — Achieved

Pieter Wuille, one of the chief architects behind the Taproot upgrade of Bitcoin, now famously declared that the real work will be in building wallets/protocols that make use of its advantages. Eerily prophetic, the new use-cases are starting to catch fire, beginning with the Ordinals craze in 2023. But beyond bloating the chain with JPEGs — are there more meaningful ways to leverage the highly anticipated agreed soft fork of November 2021? It is just a coincidence that Zenon’s mainnet went live a few days after the Taproot upgrade, or that Zenon’s founders signed block 709632 with ASCII art?

![Image 13](https://miro.medium.com/v2/resize:fit:700/0*NMFbFAoBBubsSmd7.png)

## STAGE 3 — Achieved

The initial validator set is decentralised as are the early holders. Ideally we will continue to grow the user base and provide ways to funnel in small fish before the big and coordinated money arrives, mitigating their impact and blunting any vector in the direction of centralisation.

This means increasing accessibility and facilitating the smooth inflow of capital into NoM. The NoM Multichain Tech allows for this, as does the mobile wallet and extension wallet. There is also the affiliate marketing system combined with Accelerator-Z to support marketers with growing the number of users, the volume and network effect. The affiliate marketing system and Accelerator-Z are both live and functioning. Furthermore, aliencoder’s EVM-compatible layer-2 will lead to some early games and NFTs, further facilitating an inflow of people from the wider crypto ecosystem (it’s necessary to onboard some of those people before appealing to Bitcoiners later in our maturity).

## STAGE 4 — WIP

Aside from the sidechain being decentralised at every level, it also needs to be extremely scalable and feeless. It basically needs a unique solution to the blockchain trilemma which elevates it above the rest. This way, even if someone eventually copies our tech, they wouldn’t be able to copy our decentralisation or rival our network effect or momentum.

The Bitcoin stuff is probably already figured out, if not running on private testnets. But you can’t release that stuff to a janky network. It needs to be scalable, dynamic and the consensus needs to be upgraded to fulfil the whitepaper’s vision, as at the time of writing only maybe 80% of the whitepaper is actualised.

-   **Unique architecture**. It is a dual-ledger with a block-lattice and meta-dag. A unique layer-1 which is sovereign and built from scratch.
-   **Dynamic Plasma**. The transaction throughput management mechanism for the NoM needs to be fully implemented.
-   **Sentinels**. The consensus needs to be upgraded by sentinels partaking in this, delivering the proof-of-work links.
-   **Narwhal and Tusk**. The NoM is DAG-based tech and in accordance with this research paper \>100k tps is possible with proper implementation.
-   **Layer-2 for SC**. There is already research into a highly scalable one which is turing-complete, uses zero-knowledge proofs and unikernals

## STAGE 5 — WIP

By now Zenon should be mature enough to begin building, testing and releasing the native Bitcoin interoperability solutions. From this will come the smart contracts/applications for DeFi with native Bitcoin. We will also have the capacity to absorb and support a huge inflow of people as per our adoption goals.

The rest of this article discusses the ideas being considered for native Bitcoin interoperability. It covers **six major ideas**.

## Idea #1: TSS technology

TSS stands for Threshold Signature Scheme. In practice, TSS allows N participants from a total of T participants to approve the spending of assets, as long as the threshold of N is reached. For example, the signing authority may be distributed amongst 4 parties, and as long as at least 3 agree, the Bitcoin can be spent.

In the context of Zenon, the participants would be Pillars (Zenon nomenclature for validator nodes). They would take on the role of being custodians for the Bitcoin. The ecdsa–TSS could control Native Bitcoin or Bitcoin wrapped on Zenon (zBTC).

## Idea #2: Atomic Swaps

HTLC (Hashed Time-Locked Contract) is a smart contract where the assets are locked until a condition is met, such as a time limit or the presentation of a cryptographic proof. PTLC (Point Time-Locked Contract) is a variant which enables greater privacy. MuSig2 is a multi-signature algorithm that allows multiple parties to collaboratively approve a transaction. Combining PTLC with MuSig2 allows for transactions where the control is distributed amongst multiple parties and the permission of all participants is required for it to proceed.

In practice this allows for more complexity with Bitcoin transactions while maintaining a high level of security and reliability. Within the atomic swaps discussion there has been a mention of the [xClaim](https://www.xclaim.io/) method. In their 2019 research paper, they describe a more efficient implementation for trustless atomic swaps which is cheaper and faster and leverages the concept of cryptocurrency-backed assets (CbAs). Click [here](https://forum.zenon.org/t/pitch-btc-znn-tech-and-no-bs/1422/4) for another resource for people exploring something similar.

## Idea #3: Layer-2 Solutions (EVM-compatible)

The current consensus amongst the community devs is that the layer-1 should remain feeless, minimalist and efficient; the heavy work and bloat being kept to a separate execution domain. This means the smart contracts will happen on two different types of layer-2 solutions that are currently being worked on. They are not mutually exclusive; one is for interoperability while the other is for scalability.

The first solution is a layer-2 which is EVM compatible/interoperable with existing blockchains — this will enhance ecosystem growth.

Sidechains enable the transfer of assets between the mainchain and the sidechain, mainly so more complex work can be done while drawing on the security of the underlying layer-1. But because its focus is on extending the functionality of the mainchain, this layer-2 solution is more accurately described as an extension chain.

ZNN (Zenon) may be bridged to become xZNN (extension Zenon) which will be the gas token for the extension chain. The backing may not be 1:1 because in the extension chain xZNN will be partly burned. One idea for the fee distribution mechanism is 33% to builders/contract deployers, 33% to extension chain validators and 34% burned. ZNN was chosen because relative to QSR it has a high inflation rate and low burn rate. Furthermore, since validators produce ZNN, they can be validators for the extension chain as well and share their inflation to sustain the system subject to demand.

However, these details aren’t finalised. It may be that zBTC is bridged from the layer-1 to the extension chain where it will become xBTC and can be used for the fee system instead of xZNN.

## Idea #4: Layer-2 Solutions (Zero-knowledge proofs)

A layer-2 which is extremely scalable/fast — this will enable mass-adoption of Zenon as it proves to be practical and robust for real-world use. The design for this layer-2 is a Turing complete zero-knowledge general computation scaling solution that leverages unikernals. It would be written in a new programming language called Cairo, and the contracts would be called Starknet Contracts. To break down the components:

Turing complete means the computational system can perform any computation that can be described algorithmically; this means absolute competency in executing complex programs and solving a wide range of computational tasks/problems.

The inclusion of zero-knowledge proofs will bring security and privacy, because it allows for something to be verified without requiring the complete information set. The complete information set could include sensitive information that infringes on privacy.

Unikernals are lightweight and optimised for running a single type of program. Their simplicity means they are efficient and fast, and it also makes security easier as there is less of an attack surface to account for. Sometimes less is more.

The Taproot upgrade of November 2021 introduced a number of new features to the Bitcoin scripting language. Schnorr signatures and Script path spending allow for more efficient and complex transactions. Taproot outputs is also a key feature, as they can be used for a variety of purposes. Prior to Taproot, the only way to store data on Bitcoin was with a smart contract, but that is obviously expensive, slow and carries the risk of exploits. Now, Taproot outputs allow for the storage of data on Bitcoin without using smart contracts, meaning it is simple, efficient and secure.

Bitcoin could be used as a data availability layer for zero-knowledge smart contracts. The reference is on-chain on Bitcoin, but instead of referencing a JPEG it will be referencing data stored off-chain (off Bitcoin). For example, suppose a Zenon smart contract is used to store and manage medical records. The medical records could be encrypted using a zero-knowledge proof and stored off-chain. The smart contract could then reference the data on-chain (on Bitcoin) using a cryptographic hash. This would allow the smart contract to prove that it has access to the medical records without revealing the actual records themselves. This would provide an additional layer of privacy for patients.

Zenon could thus use Bitcoin as a data availability layer for smart contracts, meaning the layer-2 would be leveraging the most robust, secure and decentralised database in the world.

## Idea #5: Merged Mining

Mining in Bitcoin is the process of solving complex mathematical problems in order to confirm transactions and record them on the blockchain. Miners who successfully do this are rewarded with newly minted Bitcoin as well as with the transaction fees for that block. The intense competition between Miners has led to specialised hardware as well as the formation of mining pools. Essentially, multiple parties combine their computational power to increase their chances of being rewarded, and this reward is shared amongst individual members of the pool in proportion to the hash power they contributed.

Merged mining is a situation where miners can simultaneously mine multiple blockchains using the same hardware. The same hash puzzle is solved to validate both blockchains at the same time. The secondary blockchain (Zenon) would need to be designed to support merged mining. Zenon’s consensus would need to recognise and include the proof of work from Bitcoin — and if you read Zenon’s whitepaper, the fully realised vision for Zenon is a hybrid of proof of stake and proof of work. Furthermore, Zenon would need to entice the Bitcoin miners to want to merge mine it. The direct incentive for the Bitcoin miners would be the inflationary ZNN rewards and the overall value-add that Zenon brings to Bitcoin’s ecosystem. The incentive for Zenon validators is that they stay competitive with earning rewards and can draw from the security of Bitcoin’s tremendous hash power.

See [here](https://medium.com/iovlabs-innovation-stories/modern-merge-mining-f294e45101a0) for a more general and indepth discussion of modern merged mining. Rather than a traditional merge-mined sidechain, Zenon could be designed with a BTC relay such that it would be a merge-mined SyncChain. This is more flexible because if Zenon already has a Bitcoin relay, it is easy to transfer value from Bitcoin to Zenon by forwarding the Bitcoin headers and the Bitcoin peg-in transactions from Bitcoin to the Bitcoin relay contract as part of Zenon’s consensus.

## Idea #6: BRC-20 tokens

Bitcoin Ordinals are created by using the Taproot output to create a transaction that assigns a unique identifier to a satoshi. The identifier makes the satoshi distinguishable from others; it thus classifies as an NFT on Bitcoin. They are indivisible, non-fungible and are being used as NFTs.

BRC-20 tokens are built on Bitcoin. It utilises Ordinal inscriptions of JSON data to deploy token contracts, mint tokens, and transfer tokens. See [here](https://domo-2.gitbook.io/brc-20-experiment/) for in-depth information about BRC-20 tokens. They are divisible, fungible and are expected to be used in DeFi and in NFTs. They can represent a variety of assets such as Bitcoin, other cryptocurrencies or fiat.

The Zenon devs have suggested that BRC-20 tokens could be ported to become ZTS tokens (tokens issued on Zenon, analogous to erc-20 tokens on Ethereum) for feeless transactions.

## Parting Thoughts

This article has discussed a number of possibilities for integration with Bitcoin and what the future of DeFi with BTC could look like with Zenon. Some of these have already had significant progress made (atomic swaps) while others have only just started to be worked on (both layer-2 solutions). The other possibilities seem to be further down the roadmap (merged mining) or purely experimental in nature (integrations with BRC-20 tokens).

Notably, there are a lot of ‘if’s. If, if, if … does not exist. Network of Momentum? Network of Crazy Fantasies & Beautiful Promises more like. But it does present an intriguing opportunity to potentially be early in greatness. It’s an interesting risk-reward analysis. Learn as much as you can, analyse everything, DYOR (are there rumours it’s backed by OG Bitcoiners?), verify it all, talk to people.

Zenon will scale Bitcoin and give it wings. And as per game theory, the simple equation of BTC + ZNN \> BTC will onboard even the maxis one day. Do the maxis love Bitcoin, or do they love the Bitcoin Ethos? Perhaps one day the equation will simply become BTC = ZNN, and even further into the palantir the word money will just be replaced by sats and all of the infrastructure will be hidden and irrelevant to normies. We will see how it all unfolds …

## Thanks for reading!

– Zyler

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
