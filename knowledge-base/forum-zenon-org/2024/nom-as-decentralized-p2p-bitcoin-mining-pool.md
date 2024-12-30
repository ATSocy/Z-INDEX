Thread: nom-as-decentralized-p2p-bitcoin-mining-pool
aliencoder | 2024-03-27 15:19:50 UTC | #1

Motivated by the discussions around dynamic Plasma, I’m coming up with a brand new development that seeks to decentralize the mining pools found in Bitcoin, while enhancing NoM ecosystem creating a symbiotic relationship to strengthen both networks.

Inspired by [Braidpool](https://blog.opdup.com/2021/06/30/can-braidpool-reuse-p2pool-components.html) proposal, NoM seems to check all the boxes:

1. A peer to peer network of miners to disseminate shares:
We already have a p2p network of “miners”: they are the users of NoM that generate PoW for Plasma.

2. A rewards calculation algorithm that incentivizes miners to disseminate them at the earliest.
Very interesting because we already have this mechanism: you want your transaction to be issued as soon as possible.

3. Payment channels to make payouts to miners so that a constant amount of blockspace is required, independent of the number of participating miners.
We can redirect those payouts to a TSS controlled by Pillars/Sentinels.

4. An anonymous hub that can’t deny rewards payouts to miners.
Can Pillars be those anonymous hubs? They already issue payouts for hundreds of delegators.

I’m remembering some parts of the whitepaper that compares Pillars to mining pools. Is the whitepaper so forward thinking? The more I read, the more interesting those ideas become… I’m trying to connect some dots here.

How does it work?

Replace SHA-3 with SHA-256d PoW to mine Bitcoin while it is being used for feeless txs. Basically merge-mine Bitcoin while generating Plasma for feeless txs.

Additional resources we would need:

- Bitcoin full nodes or light clients such as [Neutrino](https://github.com/lightninglabs/neutrino) or [nakamoto](https://github.com/cloudhead/nakamoto)
- [FROST](https://github.com/ZcashFoundation/frost) with ROAST [wrapper](https://github.com/nickfarrow/roast) (more about ROAST [here](https://blog.blockstream.com/roast-robust-asynchronous-schnorr-threshold-signatures/), paper [here](https://eprint.iacr.org/2022/550.pdf))

Why?

* NoM can become the first decentralized mining pool for Bitcoin, strengthening the hashrate, while increasing the number of mining peers (more users on NoM => more hashrate => more BTC mined => more TVL => more users, positive feedback loop)
* it can become the first network to acquire Bitcoins by mining them in a trustless way
* it can use mined BTC to embed information into the Bitcoin blockchain (tapscripts) by paying fees and unlock a myriad of use cases (including the “Holy Grail” aka Bitcoin DeFi)
* it can become the first decentralized network to simultaneously mine, hold and use on-chain BTC trustlessly, providing added value and acting as a Bitcoin L2
* creates a symbiotic relationship with Bitcoin by providing hashrate in exchange for block space (mine & pay sats/vbyte)

More information [here](https://forum.hypercore.one/t/nom-as-p2p-mining-infrastructure-for-bitcoin/239/1).

-------------------------

cryptocheshire | 2023-11-21 22:24:18 UTC | #2

Yes pls

-------------------------

0x3639 | 2023-11-21 22:31:18 UTC | #3

Did Kaine envision all this when he wrote the white paper?

-------------------------

DrD3 | 2023-11-21 22:49:44 UTC | #4

![2023-11-21 23.48.50|690x383](upload://jJDjkpQCEB5NxFkHl2YJr5UXd7u.jpeg)

-------------------------

romeo | 2023-11-22 00:21:07 UTC | #5

thanks for the insight @aliencoder - you listed what's needed in relation to FROST, but what I'm not sure of is what changes are needed at protocol level for this implementation. Is it a change to the current proposed PTLC deployment or something new entirely and if so does it impact existing NoM functionality?

-------------------------

aliencoder | 2023-11-22 09:18:55 UTC | #6

[quote="0x3639, post:3, topic:1685, full:true"]
Did Kaine envision all this when he wrote the white paper?
[/quote]

I think that ProfessorZ envisioned all of this, but it's all speculation.. That's why I'm trying to connect the dots and see what is feasible and what is not.. Seems that many things written both in the whitepaper and in the code are hints for us.

In my opinion we must do our best to analyze everything and deliver Phase 1 to the best of our knowledge.

[quote="romeo, post:5, topic:1685"]
Is it a change to the current proposed PTLC deployment
[/quote]

Absolutely not. PTLC is a "standard" and straightforward implementation. They're like HTLCs that we already have, but better.

[quote="romeo, post:5, topic:1685"]
what changes are needed at protocol level for this implementation
[/quote]

No protocol changes to support FROST. *Flexible Round-Optimised Schnorr Threshold Signatures*, more specifically [frost-secp256k1](https://crates.io/crates/frost-secp256k1) is TSS for Bitcoin using Schnorr signatures. We'll use [frost-ed25519](https://crates.io/crates/frost-ed25519) for NoM.

What we need to do is adapt Braidpool's P2P mining pool proposal and tweak it to be compatible with NoM.

-------------------------

romeo | 2023-11-22 11:20:53 UTC | #7

[quote="aliencoder, post:6, topic:1685"]
Absolutely not. PTLC is a “standard” and straightforward implementation. They’re like HTLCs that we already have, but better.
[/quote]

Sorry - I meant to ask any changes to the signature algorithms that were chosen for the PTLC noting that FROST specifies it, but you answered that in the next part

-------------------------

aliencoder | 2023-11-22 17:37:52 UTC | #8

Another interesting idea that can be derived from this post is that ZNN can be backed in the future by actual Bitcoin (not some wrapped representations).

-------------------------

aliencoder | 2023-11-24 16:22:44 UTC | #9

The future of Bitcoin mining is peer-to-peer.

https://ocean.xyz/event

https://twitter.com/ocean_mining/status/1726740971461767401

> One small step for miners, a giant leap for decentralization!

-------------------------

Stark | 2024-01-14 05:50:27 UTC | #10

The underlying commodity of crypto is proof of work. The various projects just monetize PoW on different ledgers.

-------------------------

cryptocheshire | 2024-01-14 10:09:22 UTC | #11

This will be the main driving narrative for Zenon in 2024

-------------------------

Stark | 2024-01-21 22:17:49 UTC | #12

I want to suggest researching Kaspa to see how their mining works. Perhaps NoM decentralized mining pools can serve Kaspa as well. 

Amongst many things, NoM can be the decentralized PoW market aggregator. PoW is the overarching theme that is greater than the sum of all the chains. 

Zenon eyes.

-------------------------

aliencoder | 2024-01-21 22:09:25 UTC | #13

[quote="Stark, post:12, topic:1685"]
Perhaps NoM decentralized mining pools can serve Kaspa as well.
[/quote]

It will surely serve Bitcoin `SHA-256d` algo (merge-mining) and XMR `RandomX` algo (Plasma PoW difficulty adjustment).

-------------------------

