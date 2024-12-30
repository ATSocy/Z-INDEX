Thread: the-p2p-revolution-decentralizing-decision-making
aliencoder | 2023-12-09 09:06:42 UTC | #1

I've conducted additional research and found [Mithril](https://mithril.network/doc/), a stake-based threshold multi-signatures protocol designed by the Cardano team: "We also showcase that STMs are eminently useful in the cryptocurrency setting by providing two applications: (i) stakeholder decision-making for Proof of Work (PoW) blockchains, specifically, Bitcoin, and (ii) fast bootstrapping for Proof of Stake (PoS) blockchains.".

NoM uses the same [cryptography](https://github.com/input-output-hk/mithril/blob/bcf34bb02a49c025123407c959b852ba33516a3d/mithril-common/Cargo.toml#L26C1-L27C1) as Cardano, so Mithril would be compatible out of the box.

Use case: we can use this stake-based threshold multisignature scheme to empower other NoM actors to participate in important decision making processes within the network.

-------------------------

coinselor | 2023-12-09 09:23:51 UTC | #2

What specific use-case are you thinking about? 

Something like allowing ZNN stakers to participate in A-Z ?

-------------------------

aliencoder | 2023-12-09 09:40:52 UTC | #3

[quote="coinselor, post:2, topic:267"]
What specific use-case are you thinking about?
[/quote]

- Light clients
- Decision-making: according to the [paper](https://eprint.iacr.org/2021/916.pdf), "... it is possible for all Bitcoin holders to ratify a particular software upgrade"
- Even more decentralized custody (extending the capabilities of a TSS)

-------------------------

