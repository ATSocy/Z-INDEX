Thread: taproot-bridge-discussion
Stark | 2024-12-04 15:00:40 UTC | #1

This is an outline summary of key points from discussions with @aliencoder 

Outline of the Taproot Bridge:

**I. Introduction**

* The Taproot Bridge is a proposed infrastructure upgrade for the Zenon Network (NoM) that enables interoperability with Bitcoin.
* It allows for the transfer of BTC, Ordinals, and Runes between the Bitcoin network and NoM.

**II. Key Benefits**

* Transforms NoM into a Bitcoin layer-2 infrastructure, providing a gateway for BTC, Ordinals, and Runes.
* Enables the creation of a Bitcoin vault on NoM for merge-mining, allowing miners to use the TSS vault as a coinbase address.
* Allows for the accumulation of Bitcoin in a decentralized treasury.

**III. Technical Details**

* Utilizes Taproot TSS (Threshold Signature Scheme) with Schnorr signatures, which is more secure and scalable than traditional ECDSA TSS.
* Employs MPC to secure funds, ensuring decentralization and security.
* Compatible with NoM's existing architecture, with plans to integrate with future extension-chains.

**IV. Prerequisites**

* The Governance Module must be implemented and activated on the Zenon Network before development of the Taproot Bridge can begin.

**V. Novelty and Competitive Advantage**

* The Taproot Bridge's use of Schnorr signatures and Taproot TSS makes it a novel approach to Bitcoin interoperability.
* This technology has the potential to position Zenon Network as a leader in BTC interoperability and layer-2 infrastructure.

**VI. Next Steps**

* Community discussion and approval of the Governance Module and Taproot Bridge proposals.
* Implementation the Governance Module on Zenon Network.
* Development and deployment of the Taproot Bridge, pending successful implementation of the Governance Module.

---

https://github.com/zenon-network/go-zenon/pull/47

![Screenshot 2024-12-04 at 9.57.51 AM|690x337](upload://99OMZGvl8V9TpF4HohoDjUREAEq.png)

-------------------------

Stark | 2024-12-04 15:27:06 UTC | #2

The governance module is key to this discussion. The Taproot Bridge team wants to start this month and that adds a critical time element to the governance module. I think there is a good argument for testing the governance module on Hyperqube_Z, but a key point of discussion is the potential opportunity loss of delaying the governance module, and therefore missing the window of opportunity for this team to move forward with the Taproot Bridge. 

Nobody likes feeling rushed. We have to try to be as objective as possible from a number of perspectives. I look forward to learning more points of view.

-------------------------

0x3639 | 2024-12-04 17:37:16 UTC | #3

We are not going to rush the implementation of the governance module.  It will be tested and reviewed extensively before being considered for `go-zenon`.  I am confident it will take more than 30 days.  

Can you please explain how this work is consistent with Mr. Kaine's vision for BTC integration?  In the past he mentioned xClaim as a basis for BTC interoperability.  

Why are you making this proposal and not the developers who are behind this work?  Something this expansive and important should be proposed by the people doing the work. 

How does this work integrate with Sentinels and the work of the professor?  

My general reaction is this implementation is not consistent with Kaine's limited explanations of how he envisioned the BTC integration and if these devs are serious they need to make a very comprehensive proposal and have an active discussion with the developers here.

-------------------------

Stark | 2024-12-04 15:42:30 UTC | #4

Thank you for furthering the discussion. My goal is to move several presently ongoing issues in the NoM, forward. Whether they are approved or not is not my primary concern, but we need to come to some kind of resolution on several matters, rather than wasting away. 

*Disclosure: I do not have any investment in these proposals.*

-------------------------

aliencoder | 2024-12-05 11:40:41 UTC | #5

[quote="0x3639, post:3, topic:565"]
Can you please explain how this work is consistent with Mr. Kaine’s vision for BTC integration? In the past he mentioned xClaim as a basis for BTC interoperability.
[/quote]

This is a complementary interoperability solution. It builds on the TSS approach using Schnorr. It's needed to create vaults on Bitcoin for different purposes: bridging, merge-mining, etc. It's a proven method to control BTC, Ordinals and Runes on Bitcoin.

[quote="0x3639, post:3, topic:565"]
Why are you making this proposal and not the developers who are behind this work? Something this expansive and important should be proposed by the people doing the work.
[/quote]

I'm going to take the lead in this direction because they prefer to code and not bother with anything else (that's how we worked for Bitcoin Account Abstraction on Supernova too).

[quote="0x3639, post:3, topic:565"]
How does this work integrate with Sentinels and the work of the professor?
[/quote]

The Bitcoin full nodes `bitcoind` can run on Sentinels. We need reliable RPC connections to Bitcoin full nodes and Sentinels are already incentivized by the protocol.

-------------------------

0x3639 | 2024-12-05 15:18:53 UTC | #6

[quote="aliencoder, post:5, topic:565"]
TSS approach using Schnorr.
[/quote]

who signs messages?  Pillars?  How do you deal with a changing signature set?

[quote="aliencoder, post:5, topic:565"]
The Bitcoin full nodes `bitcoind` can run on Sentinels. We need reliable RPC connections to Bitcoin full nodes and Sentinels are already incentivized by the protocol.
[/quote]

Does this mean you propose the work will include the deployment of sentinels?  How do you coordinate this with Prof's work on UnikernelZ which is intended to run on sentinels also (as outlined in the WP)?  And will the sentinel design take into account PoW links?

I think the deployment of sentinels needs to be coordinated with the core developers of the project.  Sentinels encompass PoW links, N&T potentially, and UnikernelZ.  

How do you bring all these ideas together so the deployment of a sentinel meets the intended design objective?

-------------------------

aliencoder | 2024-12-07 14:03:46 UTC | #7

[quote="0x3639, post:6, topic:565"]
who signs messages? Pillars? How do you deal with a changing signature set?
[/quote]

The team will work on @sumamu's orchestrator and integrate Bitcoin Taproot support for it. The only thing to add is that we'll need more than 1/3 of Pillars to secure the Bitcoin TSS vault(s). We can add a few cool things to the orchestrator, too.

[quote="0x3639, post:6, topic:565"]
Does this mean you propose the work will include the deployment of sentinels?
[/quote]

I don't know. We can integrate `bitcoind` into Sentinels, but we need to figure out how to do that. 

[quote="0x3639, post:6, topic:565"]
Sentinels encompass PoW links, N&T potentially, and UnikernelZ.
[/quote]

N&T is at the consensus layer (Pillars). UnikernelZ is complementary.

 [quote="0x3639, post:6, topic:565"]
How do you bring all these ideas together so the deployment of a sentinel meets the intended design objective?
[/quote]

A Sentinel specific implementation is currently out of scope for the Bitcoin Taproot bridge.

-------------------------

0x3639 | 2024-12-06 23:25:13 UTC | #8

Thank you for that clarification.  My recommendation is that before we add any functionality to the bridge, we improve the existing UI / UX experience.  Every new user that joins the project experiences an issue with bridging assets and they each require help in Telegram.  

I also experience issues and have reported them in Github.  

[quote="aliencoder, post:7, topic:565"]
N&T is at the consensus layer (Pillars). UnikernelZ is complementary.
[/quote]
From my research of N&T it separates transaction dissemination from consensus ordering. Being that Sentinels are the networking layer of the project I assumed they would be involved with transaction dissemination (the Narwhal portion of N&T).  But that is a guess at this point.

I think we need to have a deep understanding of how sentinels will work before we assume they take on new network rolls.

-------------------------

aliencoder | 2024-12-07 18:18:50 UTC | #9

[quote="0x3639, post:8, topic:565"]
My recommendation is that before we add any functionality to the bridge, we improve the existing UI / UX experience.
[/quote]

This is out of scope for the Bitcoin Taproot bridge project. They can deliver the bridge integration, and they can also cover the frontend required for the bridge interface, so we can parallelize work.

[quote="0x3639, post:8, topic:565"]
Every new user that joins the project experiences an issue with bridging assets and they each require help in Telegram.
[/quote]

I agree, but again, it's out of scope for the Bitcoin Taproot bridge proposal. We need a separate discussion to find ways to improve the current bridge UX.

[quote="0x3639, post:8, topic:565"]
From my research of N&T it separates transaction dissemination from consensus ordering. Being that Sentinels are the networking layer of the project I assumed they would be involved with transaction dissemination (the Narwhal portion of N&T). But that is a guess at this point.
[/quote]

Every NoM node is part of the peer-to-peer layer. Sentinels are just a special type of node.

[quote="0x3639, post:8, topic:565"]
I think we need to have a deep understanding of how sentinels will work before we assume they take on new network rolls.
[/quote]

For the purpose of this integration, they can host `bitcoind` full nodes. But other than that, the Sentinel implementation is out of scope for this discussion

-------------------------

aliencoder | 2024-12-21 17:21:39 UTC | #10

I've discussed with the AA team and we decided to not touch Sentinels for this implementation.

`orchestrators` will either need to rely on [3rd party RPC providers](https://www.comparenodes.com/protocols/bitcoin/) or run a dedicated full/light node or a combination of both:

- Centralized Bitcoin RPC providers in conjunction with a light client like [Neutrino](https://github.com/lightninglabs/neutrino) or [Nakamoto](https://github.com/cloudhead/nakamoto)
- Semi-centralized RPC like [dRPC](https://drpc.org/chainlist/bitcoin)
- Running [Bitcoin full nodes](https://github.com/bitcoin/bitcoin/releases)
- Running an Electrum server like [Electrs](https://github.com/romanz/electrs)

We have plenty of options and we can defer the Sentinel implementation for a later date.

-------------------------

0x3639 | 2024-12-30 13:05:14 UTC | #11

I've been a little less interested in this work because I guess I assumed it was more focused on BTC integration with Supernova to enable runes and ordinals, both of which I know nothing about.  

However, when I asked chatGPT "What is a Taproot Bridge?" it explained a more interesting concept: fungible vaults on BTC.  This is a concept we have all been talking about. How does NoM create a fungible vault on BTC to represent zBTC on NoM?  This vault concept is discussed in the xClaim whitepaper which Kaine referenced.  And several knowledgable devs have discussed the vault concept in Telegram.

Maybe the first step in deploying BTC vaults on NoM is to test them on Supernova.  Have pillars sign TXs in a TSS scheme.  Prove the vault, bridge, and concept.  Then flip the script when sentinels are introduced.  Maybe Sentinels become observers and relay BTC transactions to Pillars to sign and that is what enables zBTC on NoM ?  IDK...  

Does anyone know of a working taproot vault on Bitcoin yet?  

---

A **Bitcoin Taproot Bridge** is a conceptual mechanism or design that uses Bitcoin's Taproot upgrade to facilitate interactions between the Bitcoin network and other blockchain ecosystems, such as for creating tokenized representations of Bitcoin (e.g., wrapped Bitcoin or synthetic Bitcoin) or enabling cross-chain interoperability.

### Core Features of a Bitcoin Taproot Bridge

1. **Taproot Upgrade**:
   - Taproot is a Bitcoin protocol upgrade that enhances privacy, efficiency, and flexibility by combining Schnorr signatures and Merkelized Abstract Syntax Trees (MAST).
   - It allows Bitcoin to support more complex transactions with reduced on-chain data and better privacy, making it suitable for bridges.

2. **Vaults for Tokenization**:
   - Bitcoin can be locked in a "vault" using a Taproot script. This vault secures the Bitcoin while representing its value on another blockchain.
   - For example, Bitcoin locked in a Taproot vault on the Bitcoin blockchain can be represented as a token like `zBTC` on the Zenon Network.

3. **Partial Redemption**:
   - Taproot enables the creation of scripts that allow partial unlocking of funds. This means the vault could allow for partial redemptions corresponding to fractional amounts of Bitcoin, improving fungibility and flexibility.

4. **Inclusion Proofs**:
   - Transactions on the Bitcoin blockchain can generate cryptographic proofs (e.g., Merkle proofs) to verify on the target blockchain that Bitcoin has been locked.
   - These proofs are essential for trustless cross-chain interactions.

5. **Enhanced Privacy**:
   - Taproot transactions look identical to regular Bitcoin transactions unless specific conditions are met, which helps preserve user privacy when locking/unlocking Bitcoin for bridging purposes.

6. **Reduced Costs**:
   - Taproot's efficiency reduces transaction sizes, making it less expensive to create and manage bridges.

### Applications of a Bitcoin Taproot Bridge
- **Cross-Chain Liquidity**: Allowing Bitcoin holders to use their assets in DeFi or other blockchain applications without needing centralized custodians.
- **Decentralized Exchanges (DEXs)**: Facilitating swaps between Bitcoin and assets on other networks.
- **Improved Fungibility**: Taproot-based vaults can enable fungible representations of Bitcoin with flexible redemption rules.

### Example: Bitcoin to Zenon Network Bridge
1. A user locks Bitcoin in a Taproot vault.
2. The bridge generates a tokenized representation of Bitcoin (`zBTC`) on the Zenon Network.
3. `zBTC` can be used in Zenon applications or sent to other users.
4. When redeeming `zBTC`, the vault releases the corresponding Bitcoin on the Bitcoin blockchain.

This design leverages Taproot's privacy and scripting capabilities to make the process more secure, cost-effective, and decentralized than older methods.

-------------------------

