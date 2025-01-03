Title: III. When machines come to an agreement: The endeavor for the ultimate decentralized consensus

URL Source: https://medium.com/@zenon.network/iii-when-machines-come-to-an-agreement-the-endeavor-for-the-ultimate-decentralized-consensus-98da3bc5254a

Published Time: 2019-12-17T11:29:44.983Z

Markdown Content:
Part 3
------

[![Image 7: Zenon](https://miro.medium.com/v2/resize:fill:44:44/1*rFXGQl3tfmku28AMjfzlAQ.png)](https://medium.com/@zenon.network?source=post_page---byline--98da3bc5254a--------------------------------)

The first two parts represent a brief introduction into the history, evolution and importance of consensus algorithms and protocols. In this final part we’ll explore different consensus protocols in the context of decentralized systems and how they evolved since the inception of Bitcoin. Their core objective is to maintain a distributed ledger by determining the order of transactions to prevent double spending.

Bitcoin is the first decentralized cryptocurrency working at global scale, enabled by multiple technologies linked together into a blockchain of innovation. The consensus protocol that underpins Bitcoin is simple enough to be stated in a single phrase: the longest chain with most accumulated proof of work.

Proof of work was initially developed in the ’90 as a spam mitigation solution that Satoshi brilliantly blended with a cryptographically linked list data structure and the longest chain selection rule. Together with an adaptive difficulty targeting mechanism, it creates a triple entry ledger that solves the double spending problem in a trustless and permissionless environment.

Bitcoin design is simple, yet robust: nodes are participating in a peer to peer network, joining and leaving at will. They verify the ledger state and compete with one another to create blocks of transactions every 10 minutes. The parameters employed by the Bitcoin protocol seem heuristic at first look — the 1MB block size, 10 minutes block interval and the 2016 blocks difficulty adjustment period, yet the Bitcoin network is running like clockwork under real-world conditions for more than a decade. An achievement tough to dismiss.

Network participants following the protocol must solve a specific cryptographic puzzle that requires raw computational power and depends on an auto-adjustable difficulty parameter — this represents the Proof of Work part of the protocol. They then broadcast the newly created block across the peer to peer network and, if found valid, the block will be accepted and appended as the new tip of the timechain. The block creator will get rewarded for the effort with a block subsidy. In case of a fork, nodes will observe incoming blocks and migrate to the longest chain with the most proof of work invested in it. Starting with the assumption that the majority of hashing power is controlled by honest nodes, double spends are trivially detected and discarded. We’ll not focus on attack vectors as we’ll cover them later in a separate set of articles.

PoW consensus protocol, as it’s most commonly known, stood the test of time and represents the foundation of several prominent cryptocurrencies. PoW comes under many different shapes and flavors, but the core principles remain the same.

For example, the second cryptocurrency by market cap currently after Bitcoin, Ethereum also uses PoW, but with some minor modifications in order to adapt for the lower 15 seconds block interval that causes forks more frequently. Their specific implementation is called “Greedy Heaviest Observed Subtree”, or GHOST for short and is used to optimally determine the path that has the most computation done upon it.

Most of the cryptocurrencies using PoW employ different cryptographic hashing functions, other than Bitcoin’s SHA-256d, sometimes even combined — for instance Monero’s ASIC-resistant, CPU-friendly RandomX algorithm, in order to overcome the problem posed by large mining pools that can lead to excessive centralization.

Proof of Stake was envisioned as a superior consensus protocol aiming to solve several potential shortcomings of the proof of work consensus and is mainly addressing energy consumption and miner centralization issues.

It still uses the same underlying data structure, a linked list of blocks, but generally has a weaker security model in comparison with PoW. In PoS blocks are created by nodes proportional to their current stake in the network.

This can, on paper, solve some of the deficiencies of mining, but introduces other potentially catastrophic flaws, especially in the context of a decentralized system, for example even more destructive forms of centralization due to stake concentration and collusion and paves the way for new issues such as the Nothing at Stake problem, long range attacks and more; some cryptocurrencies already have implemented practical, feasible solutions in the form of “security deposits” and slashing, but those tend to overcomplicate the design of the protocol and potentially open it up to new attack vectors.

Some variations of PoS were later proposed in the form of Delegated Proof of Stake mainly to improve scalability, however they favor centralization due to a smaller set of validators. Other forms of delegation such as Leasing PoS (LPoS), Trustless PoS or Baking were introduced as enhancements of the DPoS consensus protocol in order to stimulate the participation of smaller nodes and energizing the delegation process, however they are still incurring overhead and add further complexity within the protocol.

Algorand employs a byzantine agreement protocol based on pure PoS: nodes are registering with participating keys to engage in a three stage protocol enabled by a verifiable random function; the underlying structure is still a blockchain, but with a mathematically verified safety guarantee that prevents forks from occurring.

Another interesting concept for approaching the consensus problem comes from NKN and is based on the Cellular Automata concept. The peer to peer network operates on a custom Cellular Automata framework with specific local rules that globally converges and reaches consensus by adopting a proven mathematical model based on a well researched physical phenomenon. The protocol is highly scalable and uses a Proof of Relay mechanism for efficient routing within the network, but still relies on a blockchain ledger to store transactions.

A new wave of consensus protocols emerged together with the apparition of DAG based cryptocurrencies such as Nano, IOTA, Hashgraph or AVA. They try to leverage some useful properties of directed acyclic graphs in order to overcome blockchain’s limitations. Nano uses a block-lattice data structure coupled with a custom DPoS to achieve consensus on transactions, while IOTA uses the Tangle to append and record transactions through a process known as “network spamming”, but has yet implemented a consensus protocol that can operate in a decentralized environment.

Hedera Hashgraph employs a novel byzantine fault tolerant consensus called gossip about gossip, where nodes don’t gossip just transactions throughout the network, but also the gossip they receive from other nodes (hence the naming) and using a virtual voting scheme that is very fast; however this consensus incurs a high message complexity that reflects into an inability to scale to larger set of nodes participating in the consensus.

Upcoming AVA also proposes a highly scalable leaderless byzantine fault tolerant consensus protocol called Avalanche that leverages the meta-stability property to converge and reach consensus and is based on a dynamic append-only DAG relying on a singular genesis vertex to embed transactions into the ledger.

There are also other types of DLTs such as Radix that are borrowing different concepts from distributed computing to solve the scalability trilemma, but they are currently lacking a concrete protocol or implementation, being under development.

We’ll just mention some consensus protocols that are viable only within a permissioned environment such as Proof of Elapsed Time that uses specialized processor hardware or Proof of Authority and its derivatives.

Although there are many consensus protocols available some just recently proposed, some being actively developed, while others completely abandoned, researchers and developers will continue their work to formulate, design, refine and innovate in order to obtain superior properties or to avoid disadvantages of current implementations — in the end, it is not a winner takes all game.
