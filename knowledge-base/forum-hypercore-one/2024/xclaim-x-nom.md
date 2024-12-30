Thread: xclaim-x-nom
coinselor | 2024-03-07 14:09:41 UTC | #1

The [XCLAIM](https://eprint.iacr.org/2018/643.pdf) whitepaper was released in 2018.

The Taproot upgrade occurred in November 2021.

I've researched the Polkadot implementation of XCLAIM and considered the potential improvements resulting from the unique architecture (including a node decoupled from consensus) of NoM and the advent of the Bitcoin Taproot upgrade. This exploration speculates on how these advancements could enhance the protocol for cryptocurrency-backed assets.

*disclaimer: I have no idea what I'm talking about. This is all based on a video of a 3D redendering of a sentinel eating a BTC.*

## XCLAIM
[XCLAIM](https://xclaim.io/) comprises three main protocol ideas: Issue, Use, and Redeem.

### Issue
Users mint BTC in NoM by locking BTC with Sentinels  — non-trusted intermediaries.

### Use
Enjoy feeless and smart BTC transactions, powered by alien technology.

### Redeem
Users burn BTC on NoM to unlock their corresponding BTC from Sentinels on Bitcoin.

**BTC on NoM can indefinitely enjoy all the benefits, including feeless transactions, like any other ZTS.**

## Secure, Open, Efficient
XCLAIM ensures users can redeem their BTC back on Bitcoin at any time. How? Taproot.

(Tap)Rooted in a financially secure design, intermediaries (Sentinels) do not need to pledge collateral or prove correct behavior, thanks to Taproot. It's enforced on the Bitcoin side by default, eliminating any theft attempts.

### Dynamic and Permissionless
Any user can become their own intermediary by deploying a Sentinel, simply, anytime, and without asking for permission. 

*Note: in XCLAIM, any user can become a vault. It's an open system. I'm speculating we want to only allow sentinels to behave as BTC vaults. This might not be the case.*

### Censorship Resistant
By design, Sentinels have no influence over the issuance process. An embedded NoM contract controls the issuance of BTC on NoM, ensuring no Sentinel can prevent a user from obtaining BTC on NoM.

### Fast and Efficient
Thanks to the XCLAIM protocol, the system is 95% more efficient than traditional HTLC atomic swaps. With NoM feeless properties, I'm gonna go with 99.9% efficiency.

### Now... let's dig deeper into the Blackhole.
Now, let's delve deeper into the concept of a "Liquidity Blackhole" and piece the whole system together in NoM.

XCLAIM is designed to be open and permissionless. For this reason, any user can assume multiple roles simultaneously or leave the system whenever they wish. Choose your preferred role from:

## Users
There are two types of XCLAIM users on NoM:
- **End-users** obtain BTC on NoM from LPs and enjoy feeless and smart BTC. Requirements: (1) s y r i u s wallet.

- **Liquidity Providers (LPs):** Lock BTC with Sentinels to mint the equivalent counterpart on NoM through an embedded contract. Requirements: (1) BTC wallet and (2) s y r i u s wallet.

**Both can redeem BTC natively on Bitcoin at any time (requires a BTC wallet)**.

### Sentinels
Sentinels are XCLAIM enablers who hold BTC locked on Bitcoin in a Taproot Script. Owing to their unique characteristics within NoM, they perform two critical roles within the XCLAIM system:

- **Validators:** By having direct access to the NoM consensus, any sentinel can verify it. Requirement: (1) a znnd full node.

- **Relayers:** Ensure NoM is up-to-date with Bitcoin's state by submitting block headers to an embedded contract, acting as an on-chain SPV client. Relayers also flag potentially invalid blocks and transactions. Requirements: (1) a Bitcoin Full Node and (2) a NoM embedded contract implementation. This functionality can potentially be delegated to @MoonBaze's [haulers](https://forum.hypercore.one/t/merge-mining-feasiblity/381). 

Requirement: TBD (1) BTC wallet

All roles are coordinated using NoM embedded contracts, which include the functionality for issuing and redeeming BTC. This takes advantage of the decentralized and feeless properties of the network. One of the original concerns of XCLAIM was the cost of transactions as volume increases.

## From BTC to NoM, Step by Step
Leveraging the work done by XCLAIM, the system has two main functions: Issue and Redeem.

### Issue
A user mints BTC on NoM by following these steps:
1. Submit an on-chain issue request with a Sentinel of their choosing.
2. Send the BTC to the Sentinel.
3. Submit a transaction proof to the BTC SPV embedded contract.
4. The SPV embedded contract verifies the Bitcoin transaction.
5. The user is allocated the equivalent amount of newly minted BTC on NoM.

### Redeem
A user redeems BTC on NoM for the equivalent BTC on Bitcoin through the following process:
1. To initiate a redemption, a user locks (or burns?) BTC on NoM with an embedded contract.
2. The embedded contract instructs a Sentinel to execute the redemption on Bitcoin.
3. The Sentinel releases the correct amount of BTC to the user.

Thanks to Taproot, there is no need to manage the redeem transaction proof explicitly.

And enabling...

## A Liquidity Blackhole Powered by Orbital Program

Generalizing the idea above, any token on any chain can be locked within a Sentinel vault. This approach incentivizes cross-chain swaps with the same guarantees and user experience provided by XCLAIM, without the inconveniences of traditional atomic swap-based systems. 

By incentivizing Liquidity Providers (LPs) with real yield at the protocol level, and offering a feeless, smart, and scalable protocol that builds on the shoulders of giants—open and permissionless systems like Bitcoin and XCLAIM—the system will absorb all cryptocurrency liquidity into what can aptly be described as the **Network of Momentum Liquidity Blackhole**.

-------------------------

Chadass | 2024-03-07 15:13:27 UTC | #2

This seems more elegant than copying Thorchain distributed trust. This isn't using TSS at all, right? What are the pros and cons VS TSS solutions? I like the liquidity idea, new flavor of incentivized liquidity is a very good and smart way to attract newcomers.

-------------------------

coinselor | 2024-03-07 16:16:59 UTC | #3

Indeed, nice observation. I can't speak to the pros and cons VS TSS solutions, but I could see some efficiency improvements from less complex signature schemes. I believe the bigger improvement, particularly in terms of capital efficiency, comes from the lack of collateral needed by the system to maintain security.

-------------------------

