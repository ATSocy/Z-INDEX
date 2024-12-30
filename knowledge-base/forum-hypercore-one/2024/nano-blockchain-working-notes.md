Thread: nano-blockchain-working-notes
0x3639 | 2024-03-03 14:44:43 UTC | #1

## Placeholder for Nano vs NoM Analysis

zoon(tm) 

wiki enabled.

## Nano References in NoM Whitepaper
![Screenshot 2024-03-01 at 7.39.15 AM|690x421](upload://aRxauYAcLI86efJjBd04H2EKmmr.png)

## Nano Consensus

Consensus is maintained by [Open Representative Voting (ORV)](https://docs.nano.org/protocol-design/orv-consensus/), which facilitates irreversible finality (full-settlement). User-selected representative nodes vote on each transaction, and every node independently [cements](https://docs.nano.org/glossary/#cementing) each transaction after seeing enough representative votes to achieve [quorum](https://docs.nano.org/glossary/#quorum).

While Nano uses a weighted-voting system that can be compared to PoS, it differs significantly from traditional PoS. See the [Open Representative Voting (ORV)](https://docs.nano.org/protocol-design/orv-consensus/) page for more details.

Nano achieves consensus via a balance-weighted vote on conflicting transactions. This consensus system provides quicker, more deterministic transactions while still maintaining a strong, decentralized system. Nano continues this development and has positioned itself as one of the highest performing cryptocurrencies.

---

# Protocol Design - Ledger

## Ledger Design

The Nano ledger is the global set of accounts where each account has its own chain of transactions ([Figure 1](https://docs.nano.org/protocol-design/ledger/#account-chains-diagram)). This is a key design component that falls under the category of replacing a run-time agreement with a design-time agreement - everyone agrees via signature checking that only an account owner can modify the balance and representative on their own chain. This converts a seemingly shared data structure (a global blockchain) into a set of non-shared ones (individual account-chains).

Each Nano node determines for itself whether or not to add a valid transaction to its local ledger. This means that there is no waiting for leader-selection as there is in single-blockchain cryptocurrencies like Bitcoin, where a single miner or staker extends the global blockchain with a new block (group of transactions) after solving a Proof-of-Work or being chosen through random selection. The block lattice ledger design removes this bottleneck, drastically decreasing transaction latency, improving decentralization, and simplifying transaction validation. Nano has no concept of block sizes or block times that arbitrarily limit the number of transactions that can be processed - the network will confirm as many transactions as current network conditions allow.

![image|533x500](upload://qggyJUas4T9Hk3N8aEI38zNDptv.png)

### Accounts
Account owners are the only ones who can modify the balance and representative on their own account chains and thus contention only happens on a per-account basis or in relation to epoch distributions[1](https://docs.nano.org/protocol-design/ledger/#fn:1).

For example, if account A attempts a double spend that must be resolved by the network, account B can still make transactions as normal. Transactions are processed independently and asynchronously.

### Blocks
In Nano, a block contains the details of a single transaction. There are four different transaction types in Nano (send, receive, change representative and epoch) and in order to transfer funds, two transactions are required - a send transaction and a receive transaction.

#### Why require two transactions to transfer

* Sending of funds can be performed while the receiver is offline
* Account owners are the only ones who are allowed to modify the balance and representative on their accounts
* Allows account owners to ignore transactions, which prevents continuous sending of tiny amounts in an attempt to prevent use of the account

### Block Latice
The lattice structure of the ledger arises from blocks connecting across account-chains. All block types use the `previous` field to vertically extend the account-chain. In addition, send and receive blocks also use the `link` field to connect across account-chains. [Figure 3](https://docs.nano.org/protocol-design/ledger/#block-lattice-diagram) below illustrates the lattice structure at a high level with additional details about blocks available on the [blocks](https://docs.nano.org/protocol-design/blocks/) page.

![image|690x435](upload://eBUw8qsfELX9Wv5Pr9NlogDkD27.png)

### Ledger Pruning
Since every transaction in Nano includes a block with the complete current state of an account, the ledger can be significantly pruned. While there are a few exceptions (e.g. pending transactions), Nano's ledger design could be pruned down to one block per account (plus pending), regardless of how many transactions the account has sent or received. 

# Protocol Design - Blocks

## State Blocks
All new transactions on the Nano Protocol are communicated via blocks. The account's entire state, including the balance after each transaction, is recorded in every block. Transaction amounts are interpreted as the difference in balance between consecutive blocks.

### Account Balance
If an account balance decreases, the transaction that caused the decrease is considered a send. Similarly, if an account balance increases, the transaction that caused the increase is considered a receive.

### Block vs transaction
In traditional blockchain-based cryptocurrencies like Bitcoin, a block is a group of transactions. In Nano, a block is a single transaction, so the term “block” and “transaction” are often used interchangeably. "Transaction" specifically refers to the action, while block refers to the digital encoding of the transaction. Transactions are signed by the private-key belonging to the account on which the transaction is performed.

## Creating transactions

### Open (receive)
To create an account, an open transaction must be issued first. This is always the first transaction (block height 1) of every account-chain and can be created upon the first receipt of funds. To open an account, you must have sent some funds to it with a send transaction from another account. The funds will be pending on the receiving account. The account field stores the public-key (address) derived from the private-key that is used for signing. The link field contains the hash of the transaction that sent the funds. On account creation, a representative must be chosen to vote on your behalf; this can be changed later. The account can declare itself as its own representative.

### Send
A send transaction is one that decreases the sender's account balance by the amount they intend to send. To send from an address, the address must already have been opened with an open (receive) block and therefore will have a balance. The previous field contains the hash of the previous block in the account-chain. The link field contains the account for funds to be sent to. A send block is immutable once confirmed by the network. This means the funds are deducted from the balance of the sender's account and wait as pending until the receiving party signs a block to accept these funds.

### Receive
A receive block is very similar to the send block mentioned above, except the account balance is increasing and the link field contains the send block's hash. To complete a transaction, the recipient of sent funds must create a receive block on their own account-chain. The source field references the hash of the associated send transaction. Once this block is created and broadcasted, the account's balance is updated and the funds have officially moved into their account.

### Change rep
Nano account holders have the ability to choose a representative to vote on their behalf. This can be done any time (i.e. in an open, send, or receive transaction) by changing the representative field. In conventional PoS systems, the account owner’s node must be continuously running to participate in voting. This is impractical for many users, so to remove this requirement Nano was designed to give a representative the power to vote on an account’s behalf. A change transaction is what changes the representative of an account by subtracting the vote weight from the old representative and adding the weight to the new representative. No funds are moved in this transaction, and the representative does not have spending power of the account’s funds.

### Epoch blocks
Since all accounts on the Nano network are asynchronous, an asynchronous form of chain upgrades is needed. Unlike Bitcoin and other traditional blockchains, Nano is not able to say “upgrade at block X”, so Epoch blocks were one of the approaches developed to solve this problem.

Epoch blocks are a special block type that can only be generated using a pre-determined private key currently owned by the [Nano Foundation](https://nano.org/foundation). These blocks will be accepted by nodes and be attached as the frontier blocks on each account-chain on the network. This feature was built to allow very limited controls using these blocks: they cannot change account balances or representatives, only upgrade the account versions to allow new block structures. Furthermore, if the majority of the network does not upgrade to a new node version that enables a particular epoch block, then the epoch block will have minimal or no effect.

# Protocol Design - Spam, Work and Prioritization 

## Spam resistance
A spam transaction is loosely defined as a block broadcasted with the intent to saturate the network, reduce network availability, or increase the size of the ledger. In order to make spam more costly, each valid block in Nano requires a proof-of-work (PoW) solution to be attached to it - similar to the original Hashcash proposition[1](https://docs.nano.org/protocol-design/spam-work-and-prioritization/#fn:1). Participants can compute the required work in a few seconds, and verification time for this work is negligible (to prevent invalid blocks, large work, and/or invalid work from becoming a denial-of-service attack vector). The cost of spamming the network then increases linearly with the number of spam transactions, reducing the impact of spam from theoretically infinite to a manageable amount.

In addition to proof-of-work, another key component of Nano's defense against spam is transaction prioritization using a round-robin balance-bucket system, combined with least-recently-used (LRU) prioritization within those buckets. This system ensures that spam does not prevent legitimate users from making transactions & achieving fast confirmation, which in turn removes some of the incentives to spam (e.g. network disruption). 

Read more about their upgraded [anti-spam mechanism](https://open.substack.com/pub/senatus/p/the-bucketing-system-prioritizing?utm_campaign=post&utm_medium=web).  

Nano is under attack again.  Read more about it in Reddit. https://www.reddit.com/r/CryptoCurrency/comments/1b3v804/nano_is_under_spam_attack_days_after_anti_spam/

# Protocol Design - ORV Consensus

## Overview
In order to protect against [double spending](https://docs.nano.org/protocol-design/attack-vectors/#50-attack) and [Sybil attacks](https://docs.nano.org/protocol-design/attack-vectors/#sybil-attack-to-change-ledger-entries), Nano uses a unique consensus mechanism called Open Representative Voting (ORV). In ORV, user-selected representative nodes vote on each transaction, and every node (representative or not) independently [cements](https://docs.nano.org/glossary/#cementing) each transaction after seeing enough representative votes to achieve [quorum](https://docs.nano.org/protocol-design/orv-consensus/#quorum). Since Nano transactions are processed individually and asynchronously, deterministic finality (irreversible, full-settlement) is achieved in a short period of time, typically less than 1 second.

Due to Nano's [block-lattice ledger design](https://docs.nano.org/protocol-design/ledger/), only account owners have the ability to sign blocks into their account-chains, so all forks must be the result of poor programming or malicious intent (double-spend) by the account owner, which means that nodes can easily make policy decisions on how to handle forks without affecting legitimate transactions.

Because Nano accounts can freely delegate their voting weight to representatives at any time, the users have more control over who has power with consensus and how decentralized the network is. Also note that delegation of voting weight does not mean staking of any funds - the account delegating can still spend all their available funds at any time without restrictions. This is a key advantage to the design of [Open Representative Voting (ORV)](https://docs.nano.org/glossary/#open-representative-voting-orv). With no direct monetary incentive for nodes, this removes emergent centralization forces for longer-term trending toward decentralization of the network.

While Nano uses a weighted-voting system ([ORV](https://docs.nano.org/protocol-design#orv-consensus)) that can be compared to PoS, it differs from traditional PoS because:

* There is not one monolithic blockchain that requires leader selection (i.e. a staker or a miner) to extend
* Representatives do not create or produce shared blocks (groups of transactions)
* Each Nano account has its own blockchain that only the owner can modify (representatives can only modify their own blockchain)
* In Nano, a block is a single transaction (not a group of transactions). Transactions are evaluated individually and asynchronously
* Users can remotely re-delegate their voting weight to anyone at any time
* Anyone can be a representative
* No funds are staked or locked up
* Representatives do not earn transaction fees - see discussion here: https://blog.nano.org/the-incentives-to-run-a-node-ccc3510c2562
* Representatives cannot reverse transactions that nodes have locally confirmed (due to [block cementing](https://docs.nano.org/glossary#cementing)).

# Protocol Design - Distribution and Units

## Distribution
The distribution of Nano (formerly RaiBlocks) was performed through solving manual captchas starting in late 2015 and ending in October 2017. Distribution stopped after ~39% of the [Genesis](https://docs.nano.org/glossary#genesis) amount was distributed and the rest of the supply was burnt.

# Nano v NoM Notes

- Both have account chains and can process TXs asynchronously (both are fast)
- Nano has capped (limited) supply and NoM is inflationary to allow for incentivized consensus
- Nano has one "native" token and NoM currently has two (ZNN & QSR).  However, NoM has the ability to issue tokens natively.  There are no limits to the number of tokens that can be issued.  
- Both are feeless
- Nano uses PoW and buckets to prevent spam.  NoM uses dynamic plasma (PoW and QSR the second asset) to prevent it.  
- Nano uses a weighted votings system (like PoS but different) for consensus and NoM uses [INSERT].
- Nano does not incentivize nodes and can't.  Its supply is capped.  NoM is inflationary and incentivizes nodes.
- Nano is primarily designed to be digital cash, focusing on sending and receiving transactions only.   In contrast, NoM has embedded contracts / functions which allows for diverse behaviors on the NoM platform. This includes Zts, Zats, NFTs, staking, delegating, and any other kind of functionality that can be embedded in the network.
- NoM will have higher layers (L2s & L3s) that enable EVM and WASM functionality.  
- NoM uses Plasma as a network resource asset to manage spam, congestion, transaction ordering, storage, etc.
- Nano has only send and receive blocks. NoM can have many different types of blocks, allocating tiers of expense to their usage.
- NoM also features a spork that allows for the incorporation of new functionalities.
- NoM is community run and funded through on-chain funding framework called AZ.  Nano recently moved to a community funded model with no on-chain funding.  
- NoM has a field for arbitrary data, while Nano does not.

## Major Issues with Nano
- Anti-spam does not appear to be effective.
- Capped supply (no more issuance)
- Validator nodes are not incentivized 
- Medium of exchange only with no additional functionality

## Benefits of Nano
- Block-lattice account chains process transactions asynchronously (fast)

## Useful Links
- Nano Website - https://nano.org/en
- Nano Wikipedia - https://en.wikipedia.org/wiki/Nano
- Living White Paper - https://docs.nano.org/living-whitepaper/
- Foundation Funding - https://nano.org/en/blog/the-nano-foundation-takes-a-step-forward-on-its-open-source-journey--420eae42

-------------------------

Nostromo | 2024-03-03 11:16:38 UTC | #2

That is a fairly interesting summary of Nano. We can learn a lot from it, but the interesting part is where Zenon and Nano differ.

"Nano has one token and NoM has two." This is not correct; NoM has the ability to issue tokens, so there is no limit to how many tokens we can have. This leads into a major advantage Zenon has over Nano: the embedded contracts/functions. Nano is primarily designed to be digital cash, focusing on sending and receiving transactions. In contrast, embedded functions allow diverse behaviors on the NoM platform. This includes Zts, Zats, NFTs, staking, delegating, and any other kind of functionality that can be embedded in the network.

"Nano uses a weighted voting system (like PoS but different) for consensus, and NoM uses PoW links + PoW and PoS + virtual voting (or will eventually)." If we want to compare Nano with Zenon, it's best to compare Nano with the alphanet as it currently is, to compare apples to apples. NoM does not use PoW links, PoW, POS, or virtual voting. What does it use? I'm not entirely sure; it must be some sort of voting mechanism similar to Nano's, along with something to publish the momentums. Perhaps someone else could provide more insight into how exactly the consensus works.

Another advantage that Zenon has over Nano is its use of Plasma as a network resource asset to manage spam, congestion, transaction ordering, storage, etc.

While Nano has only send and receive blocks, Zenon can have many different types of blocks, allocating tiers of expense to their usage.

Zenon also features a spork that allows for the incorporation of new functionalities.

And there are probably more things too that I can't think of right now.

-------------------------

coinselor | 2024-03-03 12:58:58 UTC | #4

[quote="Nostromo, post:2, topic:391"]
Nano uses a weighted voting system (like PoS but different) for consensus, and NoM uses PoW links + PoW and PoS + virtual voting (or will eventually).” If we want to compare Nano with Zenon, it’s best to compare Nano with the alphanet as it currently is, to compare apples to apples. NoM does not use PoW links, PoW, POS, or virtual voting. What does it use?
[/quote]

@georgezgeorgez @sumamu ?? what do we use? :joy:

Great point. Alphanet seems to be appropiately named, after all. I would focus the article around the current Alphanet implementation. 

Maybe just add a reference to future network updates that address consensus, scalability, etc and link to the roadmap/N&T articles.

-------------------------

