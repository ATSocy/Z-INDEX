Thread: bitcoin-interoperability
aliencoder | 2023-12-17 09:10:49 UTC | #1

# Enhancing Bitcoin's Capabilities with Zenon Network | The Network of Momentum (NoM)

*Still work in progress*

## Introduction

Bitcoin stands as a foundational pillar in the cryptocurrency revolution, known for its unparalleled security, decentralization, and widespread adoption. The emergence of altcoins was driven by a desire to either rival or enhance Bitcoin’s perceived limitations. These altcoins sought improvements in various domains:

- Programmability: Implementing Turing-complete smart contracts for enhanced functionality.
- Security: Developing innovative consensus protocols for robust network protection.
- Speed: Utilizing advanced cryptographic techniques for faster transaction processing.

In contrast, Zenon Network, the Network of Momentum (NoM), is designed not to compete with Bitcoin but to improve its capabilities by leveraging the strengths of both networks.

Since its inception, Bitcoin has seen many altcoins come and go. Among these, Ethereum stands out as a prominent cryptocurrency. However, Ethereum has made significant trade-offs, such as the shift to a proof-of-stake model. This shift has sparked concerns about Ethereum's long-term stability.

In this evolving landscape, the Network of Momentum (NoM) sets itself apart by aiming to enhance Bitcoin rather than compete against it. NoM is uniquely positioned as the first decentralized network to:

1. Trustless Bitcoin Acquisition: Utilize merge-mining to acquire Bitcoin in a secure, trustless manner.
2. Trustless Bitcoin Control: Employ advanced methods like Threshold Signature Scheme (TSS) and 3. Stake-Based Threshold Multi-Signatures (STM) for decentralized Bitcoin custody.
4. Programmability Enhancement: Integrate zero-knowledge rollups to improve Bitcoin’s programmability, using tapscripts for on-chain proof embedding.
5. Security Synergy: Leverage the robust security of Bitcoin to underpin NoM's own consensus protocol.

Crucially, NoM advocates for the growth of decentralized, peer-to-peer Bitcoin mining pools, essential for the diversification of Bitcoin's hashpower. This vision includes a symbiotic relationship with Bitcoin, contributing hashpower in return for block space. This block space is instrumental in securing highly scalable zk-rollups on Bitcoin, marking a significant step forward in blockchain interoperability and efficiency.

## Architecture and Design of the Network of Momentum

NoM features a distinctive dual-ledger system, comprising a meta-DAG for executing the consensus protocol and a block-lattice for transaction settlements. Utilizing Ed25519, a fast and secure deterministic signature scheme based on Curve25519, NoM ensures cryptographic robustness.
 
The block-lattice structure, composed of individual account-chains holding transactional data identified by public addresses, introduces a novel transaction mechanism with send-blocks and receive-blocks, marking transaction completion upon the send-block's publication.

NoM's development is phased. Phase 0 introduced Plasma, a fee abstraction mechanism allowing users to generate proof-of-work or lock QSR to process transactions. Phase 1, currently under design and development, will introduce dynamic plasma which removes the artificial cap on the transaction-per-second throughput (TPS). In addition, the network can incorporate a fee-based mechanism, akin to Ethereum's EIP-1559.

In Phase I transactions will be probabilistic, as they will be anchored on Bitcoin's blockchain. The block-lattice ledger will gain additional weight as it accumulates proof-of-work from both transactions and miners. 
 
Each account-chain stores account-blocks that are layered one on top of another in a similar way to which blocks within a blockchain are linked to each other. This is an important aspect for the merge-mining process that requires a dynamic difficulty adjustment mechanism. The mining difficulty will be automatically adjusted by implementing a dynamic difficulty targeting algorithm for the merge-mining account-chain.

Embedded contracts at the protocol level are the foundation of NoM. For instance, the Pillar embedded contract, which also has its own account-chain, oversees network emissions for Pillars and their delegators. 

Pillars represent the consensus nodes in NoM. Delegators stake ZNN to Pillars and are ordered by their total delegated stake. The top 30 Pillars produce more momentums per epoch. Pillars can adjust how much they want to share from their rewards with their delegators at the end of each epoch. The distribution of ZNN is handled automatically by the embedded contract and it represents the blueprint for the mining embedded contract.

To enable BTC and ZNN merge-mining, an on-chain network upgrade mechanism (spork) will deploy a specialized merge-mining embedded contract called the "share-chain". This necessitates Pillars and Sentinels to run Bitcoin full nodes, ensuring connection and block propagation within the Bitcoin network. Miners in NoM can join the network via Zenon full nodes ([znnd](https://github.com/zenon-network/go-zenon)) and participate in the construction of the share-chain, a blockchain-like structure within the embedded account-chain.

The share-chain will operate at a lower difficulty than Bitcoin's mainchain. The share-chain allows pool miners to collaborate in a decentralized pool by mining shares on the share chain at a rate of one share block every 10 seconds. Each of the blocks on the share chain records a proportionate share reward for the pool miners who contribute work, carrying the shares forward from the previous share block. When one of the share blocks also achieves the Bitcoin difficulty target, Pillars broadcast these valid blocks to the Bitcoin peer-to-peer network using bitcoind full node. Upon acceptance, the newly mined BTC from these transactions are deposited into a Threshold Signature Scheme (TSS) vault, controlled by the Pillars. Miners who contribute to the share-chain receive ZNN as a reward. This mined BTC is allocated for purchasing block space, facilitating the development of smart contract applications, details of which will be discussed later.

In Phase I NoM will incorporate advanced cryptographic techniques, like [FROST](https://github.com/ZcashFoundation/frost) (Flexible Round Optimized Schnorr Threshold Signatures) with a [ROAST wrapper](https://eprint.iacr.org/2022/550.pdf), for decentralized BTC custody, and we are exploring [Mithril](https://eprint.iacr.org/2021/916.pdf), a stake-based threshold multisignature scheme, to enhance network governance with a veto like process.
 
Ultimately, NoM aspires to be a decentralized network that not only coordinates BTC and ZNN merge-mining but also fortifies Bitcoin’s censorship-resistant properties. 

## Bitcoin Fractal Scaling with zk-Rollups

By utilizing BTC as a Data Availability layer, NoM will be able to incorporate zk-rollup data into Bitcoin blocks mined in order to bypass transaction censorship typically seen in centralized mining pools.

Example of a typical zk-Rollup architecture:
- L1 Smart Contract Management of L2:
  - Enables deposits and withdrawals.
  - Publishes new state roots ("assertions").
  - Publishes compressed transaction data batches for verification.

- L2 Operators (also called Validators/Aggregators/Sequencers):
  - Batch transactions, forming the basis of the rollup.

Zero-knowledge rollups, a Layer 2 scaling solution, use zero-knowledge proof systems to enhance blockchain throughput and computing capabilities. These rollups have distinct advantages:

- Security and Integrity: Validators can't corrupt the state or misappropriate funds.
- User Protection: In case validators act dishonestly, users can withdraw funds en masse.
- Fraud Prevention: Unlike optimistic rollups, continuous monitoring of blocks isn't needed.

Zk-rollups inherit the security guarantees of the underlying Layer 1, significantly enhancing scalability and transaction capabilities. In this architecture, a prover submits a "validity proof" (often using ZK-SNARKs or ZK-STARKs) of transaction batches. This proof is easier to verify than redoing the entire computation.

The smart contract on the Layer 1 validates these proofs despite limited computational ability. State transitions in zk-rollups are determined by applying a deterministic function which defines the rollup as a sequence of state transition steps, starting from a known initial state, similar to how blockchains start from a genesis block. This sequence is represented as a sequence of blocks, where each block consists of an ordered list of transactions. Validity proofs ensure correctness of off-chain transactions and prevent operators from executing invalid state transitions.

Thus, the security of zk-rollups is provided by the underlying blockchain. The underlying L1 enforces the correctness of every update on the zk-rollup's state and attests that the data that describes these updates is available. Another throughput enhancement technique is recursive proofs, where multiple block proofs are aggregated into one final proof, enabling the finalization of several blocks simultaneously.

### ZK Rollups on NoM with BTC Security

The goal is to achieve a trustless ZK-rollup solution that leverages Bitcoin's security and decentralization for data availability while leveraging NoM's computing, consensus and merge-mining layers to enhance the programmability and overall censorship resistance property of the rollup. NoM will post data proofs needed to recover the off-chain state on Bitcoin, which guarantees security, censorship-resistance, and decentralization. But due to the limited computing capabilities of Bitcoin, automatic user withdrawals are not possible. However, the embedded contract on NoM can verify the proofs on the Bitcoin network with its own data and can perform the required computations.
 
Transactions specific to the zk-rollup will be processed off-chain by special NoM nodes called executors that collect, process, and compile batches of transactions into a rollup. Once transactions are batched, executors will generate a zero-knowledge proof confirming the validity of all transactions in the batch. Rollup blocks will be published in the embedded contract and then inscribed onto the Bitcoin blockchain by leveraging Taproot techniques.
 
Ordinals inscribe data into the witness part of a Bitcoin transaction, and NoM will use a similar technique to embedded the rollup date into the witness part of a transaction. A standard Taproot transaction can include up to around 400KB of data in order to pass through the public mempool. By leveraging merge-mining, NoM is able to completely bypass the public mempool and create a non-standard coinbase transaction that can embed up to 4MB of arbitrary data into the blockchain. Merge-mining will make NoM immune to any form of censorship and enable it to store zk-rollup proofs in a way that is strictly tied to Bitcoin's security model.
 
The rollup will benefit from Bitcoin's security (re-organization-resistance, censorship-resistance) and decentralization and users will be always able to unilaterally withdraw their funds without the cooperation of executor nodes by posting the corresponding proofs to NoM's embedded contract.
 
In order to further enhance the operation of the zk-rollup, a security bond will be required for running executor nodes, similar to zk-sync's [instant confirmations proposal](https://docs.zksync.io/userdocs/tech/#instant-confirmations).
 
Another interesting topic of discussion is embedding the zk-circuits into the Bitcoin blockchain using the [pay-to-contract output](https://bitcoinops.org/en/topics/pay-to-contract-outputs/).

-------------------------

0x3639 | 2023-12-17 09:33:15 UTC | #2

Helpful article regarding Sovereign ZK Rollups.  

https://medium.com/@chainway_xyz/a-sovereign-zk-rollup-on-bitcoin-full-bitcoin-security-without-a-soft-fork-ca0389a0b658

-------------------------

Zyler | 2023-12-17 09:35:51 UTC | #3

Thank you for sharing your ideas with us sir. I will take the time to read this and probably come back later with a couple of questions. But two things I'd like to ask:

1. The people who are mining BTC for the NoM's TSS vault, you said they will be paid ZNN. Where does the ZNN come from? Would they be become a new "6th participant" of the network, to be allocated protocol emissions in the same way that applies for the existing 5 participants of Pillars, sentinels, stakers, delegators and Liquidity providers? 

2. So the mined BTC will sustain a program of paying for block space ... and the mined BTC is reserved for only one purpose, which is for that? What about BTC which is added to the TSS vault, but it didn't get there by mining? Can that be used for other things? Sorry if that question is outside the scope of the post you made, I know you said "work in progress" as well as "more to come later"

-------------------------

aliencoder | 2023-12-17 09:39:20 UTC | #4

[quote="0x3639, post:2, topic:283"]
Sovereign ZK Rollups
[/quote]

> A sovereign rollup is one that does not need a smart contract or use a settlement layer for validation—scalable and secure and with the "sovereignty" of a layer 1.

I believe NoM has stronger security guarantees than a sovereign rollup that is bootstrapped without a consensus protocol.

Check this article for more opinions on Bitcoin rollups: https://decrypt.co/122833/rollkit-pitches-second-layer-for-bitcoin-sovereign-rollup

-------------------------

aliencoder | 2023-12-17 09:41:10 UTC | #5

[quote="Zyler, post:3, topic:283"]
Would they be become a new “6th participant” of the network
[/quote]

Yes. Miners will become first class citizens in NoM.

[quote="Zyler, post:3, topic:283"]
What about BTC which is added to the TSS vault, but it didn’t get there by mining?
[/quote]

This is an open question for everybody.

-------------------------

coinselor | 2023-12-17 11:53:54 UTC | #6

Thanks for the great post, a lot of new pieces. 

[quote="aliencoder, post:1, topic:283"]
But due to the limited computing capabilities of Bitcoin, automatic user withdrawals are not possible.
[/quote]

I'm assuming every time you mention deposits/withdrawals you are specifically referring to BTC deposits and withdrawals onto NoM, is this a fair assessment? 

This seems to be a recent idea, dropping here in case it might be useful:

https://delvingbitcoin.org/t/aggregate-delegated-exit-for-l2-pools/297

does this mean on/off boarding could be done without submitting a single on-chain BTC transaction?

Brb, gonna RBF stop minting ordinals since it's counterproductive for me to bloat BTC's chain now that we are gonna need to run full bitcoind nodes. :sweat_smile:

-------------------------

Chadass | 2023-12-17 14:09:30 UTC | #7

[quote="aliencoder, post:1, topic:283"]
But due to the limited computing capabilities of Bitcoin, automatic user withdrawals are not possible.
[/quote]

Can this help? https://docs.brc100.org/ 

The NoM could act as a decentralized indexer that verify the inscriptions inputs for more complex operations if I get it right.

-------------------------

Chadass | 2023-12-17 16:21:14 UTC | #8

[quote="aliencoder, post:1, topic:283"]
In addition, the network can incorporate a fee-based mechanism, akin to Ethereum’s EIP-1559.
[/quote]

Dude, forget about your fee, seriously.

-------------------------

0x3639 | 2023-12-17 16:43:30 UTC | #9

[quote="Chadass, post:8, topic:283"]
Dude, forget about your fee, seriously.
[/quote]

This statement is consistent with this: https://forum.hypercore.one/t/ideas-for-dynamic-plasma/233

-------------------------

Chadass | 2023-12-17 17:08:53 UTC | #10

Of course it's consistent. At this point of consistency it's dogmatism.

-------------------------

aliencoder | 2023-12-18 09:36:14 UTC | #11

[quote="coinselor, post:6, topic:283"]
I’m assuming every time you mention deposits/withdrawals you are specifically referring to BTC deposits and withdrawals onto NoM, is this a fair assessment?
[/quote]

Yes, BTC will be deposited into the contract address that will be used by the rollup and NoM.

[quote="coinselor, post:6, topic:283"]
This seems to be a recent idea, dropping here in case it might be useful:

https://delvingbitcoin.org/t/aggregate-delegated-exit-for-l2-pools/297
[/quote]

Very useful: 

- "the operator (or a Musig2 of all the participants) publishes new states according to some rules.""

The Pillar's TSS (FROST, as Musig2 is n-out-of-n) will publish each new state.

- "If the operator messes up (for example, fraud is proven, or the operator becomes unresponsive and does not publish the next state), then the UTXO can be spent towards an unwinding state, where the only action allowed is getting your money out of the pool."
- "There are multiple constructions that might fit this model (rollups, coinpools, etc.)."

The operator in this case is the Pillar TSS (reading from the embedded contract) and its job is to publish the next valid state transition of the rollup to the DA layer (Bitcoin).

[quote="coinselor, post:6, topic:283"]
does this mean on/off boarding could be done without submitting a single on-chain BTC transaction?
[/quote]

I don't understand your question.

-------------------------

