Title: When machines come to an agreement: Evolution of classical consensus.

URL Source: https://medium.com/@zenon.network/when-machines-come-to-an-agreement-evolution-of-classical-consensus-3dc577fbd1bc

Published Time: 2019-11-02T09:54:35.181Z

Markdown Content:
[![Image 9: Zenon](https://miro.medium.com/v2/resize:fill:44:44/1*rFXGQl3tfmku28AMjfzlAQ.png)](https://medium.com/@zenon.network?source=post_page---byline--3dc577fbd1bc--------------------------------)

Part 2

![Image 10](https://miro.medium.com/v2/resize:fit:700/1*o3nfgDGeIIZ27rP2e-fU2A.png)

Consensus can take many different forms but has a clear goal: universal agreement. In case of an election algorithm, the goal is to pick a leader, for distributed transactions the goal is to decide whether to commit or abort a transaction and so on. Any distributed algorithm that employs a collection of processes that maintain a common state relies on solving the consensus problem.

Nowadays distributed systems are omnipresent, from distributed file systems like Colossus, globally distributed databases like Spanner or decentralized ledgers like Bitcoin, consensus is the key, keeping them running day by day.

Distributed consensus research spans over decades starting with the rise of the first distributed databases in the ’70. One of the earliest examples is the two-phase commit protocol that was designed to allow a transaction manager to atomically commit or abort a transaction. But what if the coordinator fails permanently? In that unfortunate case transactions will never be resolved, requiring manual intervention that is slow and costly — a major drawback for any live system.

Therefore, as distributed systems grew bigger and became more complex, more issues appeared: unexpected faults, poor scalability or performance. These determined the need for better protocols to provide tolerance against faults, greater scalability and speedup performance.

In 1989 Leslie Lamport introduced “Paxos”, the first practical fault tolerant (within the fail-stop model) consensus protocol. In Paxos, nodes are divided into three categories — proposers, acceptors and learners with two distinct phases — prepare-promise and propose-accept and the goal is to choose exactly one valid value in cases where multiple competing values may be proposed. Later on in 2004 Lamport published Paxos Commit, a non-blocking variant for the 2-PC protocol, based on the Paxos consensus algorithm.

A more robust consensus algorithm than Paxos is “Practical Byzantine Fault Tolerance” introduced in 1999 by Barbara Liskov and Miguel Castro and implements Lamport’s approach to the Byzantine Generals Problem by making the assumption that no more than 1/3 of the nodes are malicious. However pBFT incurs a quadratic message complexity, thus struggling to scale as more nodes are added to the set.

pBFT inspired the development of several other BFT protocols or BFT variants of classical protocols that were proposed mainly to improve scalability and performance. For example, Lamport published in 2010 “Byzantizing Paxos by Refinement” followed by a “Leaderless Byzantine Paxos” in 2011 to make it resilient against byzantine adversaries. Similarly, Tangaroa was proposed as a BFT implementation of the Raft consensus algorithm with many other protocols such as Zyzzyva or MinBFT addressing various issues such as robustness, efficiency or costs.

Classical protocols are the building blocks that lead to the development of decentralized protocols as we’ll see in the next article, where attributes like trustless and permissionless operation represent their “raison d’être”.
