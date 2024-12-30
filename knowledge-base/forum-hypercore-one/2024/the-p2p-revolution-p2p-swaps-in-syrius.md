Thread: the-p2p-revolution-p2p-swaps-in-syrius
vilkris | 2023-06-07 08:03:49 UTC | #1

The P2P Swap feature in Syrius offers users an easy and censorship resistant way of exchanging value, peer-to-peer, without intermediaries on Network of Momentum.

This funding request is meant to cover the development costs related to the Syrius P2P Swap feature and the additional tooling and services related to it.

## Impact

Being able to trustlessly exchange value between individuals in a censorship resistant way over the internet without intermediaries and other third parties is one of the cornerstones on which the cryptocurrency revolution is being built upon. Currently there is no user friendly way to trustlessly trade on Network of Momentum.

P2P Swaps are not a replacement for an AMM or an orderbook based DEX, but the P2P Swap feature will offer a way for all users to conduct feeless OTC swaps with ZTS tokens, allowing for more economic activity to start taking place on Network of Momentum. The need for trustless ways of trading was once again highlighted by the recent unfortunate demise of the only CEX that ZNN and QSR were trading on.

The Zenon community has always had an active OTC market and large OTC trades are conducted regularly. A safe and liquid OTC market is especially useful when conducting large trades. Traditionally the downside of OTC trading is that the trading parties have to either trust each other or use a third party escrow that usually requires a fee to conduct the trade. With P2P Swaps in Syrius, there is no need to trust the trading partner or pay an escrow for their services.

## Team

[HyperCore One](https://github.com/hypercore-one), with two members as the primary contributors (@vilkris, @sol), and three other members supporting with testing, reviews and user guidance.

## Breakdown of work items

A breakdown of what this proposal covers:

* UI/UX design, research and iteration => 160 hours

* Prototyping, implementation and testing => 440 hours

* Writing manual test cases and doing a write-up of the implementation => 40 hours

* Incentivized peer review and testing => 30 hours

* HTLC Watchtower: design, implementation and testing => 120 hours

* Fixing potential bugs post release

* A tutorial in written format

## Areas of interest not in the scope of this proposal

Currently the P2P Swap feature does not have an automatic matchmaking system, which means that users have to find a trading partner themselves. A straightforward way to find a trading partner is to use OTC chat rooms for example. Automatic matchmaking/an orderbook would have to be considered in a separate proposal.

### What about cross-chain swaps?

HTLCs can be used to facilitate cross-chain swaps and initially, when the P2P Swap project was started, the idea was to integrate a user interface for cross-chain swaps into Syrius. After a decent amount of time spent on researching and designing a solution for this, we have decided not to include the cross-chain swap feature into the scope of this proposal.

**Reasoning**

We could provide a relatively user friendly interface for the NoM side of the swap, but since there are basically no wallets on other chains that support HTLC-based cross-chain swaps, it would mean that the swap would have to be done via rudimentary command line tools on the other chains. Based on our testing, doing cross-chain swaps with Bitcoin using a command line tool is hard and error prone. So, even if there was a user friendly interface for the NoM side of the swap, the purpose is defeated when the user has to use rudimentary tooling on other chains.

Another option would be to attempt to integrate the full cross-chain swap flow into Syrius for some chains, like Bitcoin, but this will require a significant amount of research and effort to do and will have to be considered in a separate proposal, if there is enough demand for such a feature.

We are still actively continuing the testing of cross-chain swaps to see what is technically feasible and what makes sense from a user experience point of view.

## What has already been delivered

The [first iteration](https://forum.zenon.org/t/p2p-atomic-swaps-in-syrius/1165) of the UI design was presented to the community in November 2022. After feedback from the community and prototyping of the UI, more iterations of the UI design were made until the [final version](https://forum.zenon.org/t/p2p-atomic-swaps-in-syrius/1165/47) of the UI design was presented to the community in March 2023.

After iteration and prototyping, the first version of Syrius with the P2P Swap feature ready for public testing was released a while ago. Instructions on how to try out the P2P Swap feature on the HyperCore One testnet can be found [here](https://forum.hypercore.one/t/syrius-v0-1-0-release-candidate-1-ready-for-community-testing/72).

Please note that the P2P Swap feature is only usable on testnet for now.

## What is still to come

The P2P Swap feature has not yet been enabled on mainnet. We are close to having a release candidate of Syrius available for public testing that has mainnet support for P2P Swaps.

A deposit recovery feature is still pending development. This feature will allow a user to recover their deposited swap funds in the unlikely event that they completely lose access to the machine they started the swap on.

Further testing and code review is also needed and the tutorial has to be made.

### Additional safety measures: HTLC Watchtower

Work on a watchtower service has been started. In short, the watchtower is a service that anyone can run to improve the safety of P2P swaps. Its purpose is to watch over the swaps that are being conducted on the network to make sure that swap participants receive their funds as expected in situations where Syrius fails to do so for whatever reason. The watchtower utilizes the proxy unlocking feature of the embedded HTLC contract.

A more detailed write-up of the watchtower can be found [here](https://forum.hypercore.one/t/htlc-watchtower/50).

HyperCore One is already running an MVP version of the watchtower on both testnet and on mainnet. Hopefully, in the future more watchtowers will be launched by the community to further improve swap safety.

## Timeline

If nothing unexpected happens, fully featured releases of Syrius and the HTLC watchtower should be available in Q3.

## Funding request

Total: 13,000 ZNN + 130,000 QSR

Total hours put in/allocated: 790h

If this proposal is accepted, a payout request will be made for the `UI/UX design, research and iteration` phase and for 1/4th of the `Prototyping, implementation and testing` phase.

This means a payout request of approximately 35% of the total requested funds, which will be rounded to 4,300 ZNN + 43,000 QSR.

If this proposal is accepted, work on the remaining items will be continued. The rest of the funds will be requested in batches, according to the following milestones:

* 1,700 ZNN + 17,000 QSR once a test version of the P2P swap feature that can be used on mainnet is available for public testing.

* 2,000 ZNN + 20,000 QSR once the swap recovery feature has been implemented and is available for public testing, the manual test cases have been written and the tutorial has been made.

* 5,000 ZNN + 50,000 QSR once the fully featured Syrius release and the HTLC watchtower are available and the work items have been completed.

We will wait for a couple of days to respond to feedback and gauge the general sentiment and amount of support for this proposal, until deciding whether to submit it on chain.

-------------------------

Chadass | 2023-06-07 13:38:08 UTC | #2

Could you give a few examples on what could be built down the road using P2P / HTLC / PTLC contracts ? Realistic imagination here could help us to get a view on where Zenon is going.

-------------------------

vilkris | 2023-06-07 18:13:32 UTC | #3

A lot of things are possible with the technologies you mentioned, but we have to keep in mind that they are only one piece of the puzzle - even if HTLCs and PTLCs can be used for cross-chain swaps, P2P trading, bridges and more, there are a lot of other components that have to be built to actually deliver an end-to-end service or product that solves an end user problem.

You may have already used services that use HTLCs under the hood without even knowing it. Some examples are the [Orion Bridge](https://www.orionprotocol.io/bridge) and the [Magic Protocol Bridge](https://magicstx.gitbook.io/magic-protocol/overview/magic-protocol).

Since we, HC1, are only one team with limited resources, we need to use our time effectively. This is why we will be actively engaging with Pillars to help define our roadmap for what problems we should be solving to allow for real economic activity to start taking place on NoM.

Ultimately HTLCs and PTLCs are just tools to solve problems. The P2P swaps use HTLCs to facilitate the swaps but nothing is stopping us from using some other technology for them in the future if it makes more sense. The end user doesn't care about that as long as they achieve their goal.

-------------------------

Chadass | 2023-06-07 19:01:42 UTC | #4

Do you see something like https://app.multichain.org/#/router doable with PTLC or HTLC ? This would be a kickass dapp.

The way I think it works is by leveraging what Fusion developped back in 2018 and a bunch of liquidity pools. Could PTLC be used me along with a liquidity contract owned by a bunch of pillars multisigning operations ?

-------------------------

aliencoder | 2023-06-07 20:59:09 UTC | #5

[quote="Chadass, post:4, topic:108"]
like [Multichain - Cross Chain Router Protocol ](https://app.multichain.org/#/router) doable with PTLC or HTLC
[/quote]

They share the same architecture developed by @sumamu and his team.

https://docs.multichain.org/getting-started/introduction

HTLCs and PTLCs are just primitives. PCNs (Payment Channel Networks) like BTC/LN are based on HTLC/PTLC primitives.

-------------------------

Chadass | 2023-06-07 22:16:27 UTC | #6

[quote="aliencoder, post:5, topic:108"]
d PTLCs are just primitives. PCNs (Payment Chan
[/quote]

It'd be great to see this being used to leverage crosschain massive liquidity markets.

-------------------------

vilkris | 2023-06-08 06:23:48 UTC | #7

The Orion Bridge I posted earlier is an example that basically does the same thing as Multichain. Another example of a cross-chain bridge that uses HTLCs under the hood is [Meson](https://docs.meson.fi/protocol/system-design).

So technically it should be possible to use HTLCs to solve the same problem that the Multichain bridge solves for an end user. But like Aliencoder said, HTLCs/PTLCs are just primitives. For example the Meson protocol uses their own modified HTLC scheme but is also has several other components that are needed to provide the service, such as relayers, LP servers and smart contracts on all the supported chains.

-------------------------

vilkris | 2023-09-18 09:11:43 UTC | #8

**Project update**

**Phase 1: Done**
The UI design has been delivered.

**Phase 2: Done**
A public test version of P2P Swaps has been available for a while now.

**Phase 3: Done**
* The written tutorial for P2P Swaps has been published here: https://medium.com/@vilkris/p2p-swap-tutorial-3805f10d2d21

* A more technical documentation of how P2P Swaps work can be found in Syrius' repository: https://github.com/hypercore-one/syrius/blob/develop/docs/p2p_swaps.md

* A release candidate for the HTLC Watchtower can be found here: https://github.com/hypercore-one/htlc-watchtower/releases/tag/v0.1.0-rc.2

* The manual test cases are completed and the latest Syrius release candidate passes the tests: https://github.com/hypercore-one/syrius-manual-tests/blob/main/test-runs/v0.1.0-rc.8/p2p-swap/p2p-swap-2023-09-17-windows-10.csv

**Phase 4: In progress**
We are preparing a pull request into the Zenon Network repository. After the pull request is accepted the P2P Swap feature will be available in the next Syrius release made from the Zenon Network repository.

A payout request will now be made for milestones 1, 2 and 3.

-------------------------

0x3639 | 2023-09-18 10:13:42 UTC | #9

Great work!!  I could not be more happy with the outcome of the P2P swap UI/UX.  I think this swap experience is best in class.

-------------------------

sol | 2023-09-18 13:55:26 UTC | #10

Excellent work, Vilkris! Absolutely love what you've built and community feedback has been overwhelmingly positive.

-------------------------

coinselor | 2023-09-18 17:06:43 UTC | #11

Vilkris might have to consider changing profile picture to a goat :wink:

-------------------------

aliencoder | 2023-09-18 20:35:47 UTC | #12

Amazing Vilkris :alien:

-------------------------

CryptoFish | 2023-09-20 07:30:59 UTC | #13

I admire your work, something to live up to :clap:

-------------------------

vilkris | 2023-11-19 21:54:35 UTC | #14

I'm requesting the final payout for this project (Phase 4). A release of Syrius containing the P2P swap feature was [published](https://github.com/zenon-network/syrius/releases/tag/v0.1.0-alphanet) over a month ago and the feature has been working as expected.

The [HTLC watchtower](https://github.com/hypercore-one/htlc-watchtower) has also been running without issues.

-------------------------

Blueginger | 2023-11-21 09:30:58 UTC | #15

I support

-------------------------

Zyler | 2023-11-21 15:39:19 UTC | #16

I used the P2P swap recently, it was so easy and fast. Awesome experience. NoM devs rock!

-------------------------

aliencoder | 2023-11-23 20:40:30 UTC | #17

The P2P Revolution is more than just swaps. Another post coming zoon :tm:

-------------------------

