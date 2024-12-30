Thread: serious-about-adding-znn-markets
Stark | 2024-11-20 18:09:07 UTC | #1

Ethereum fees are already getting very high, in excess of $50 for a swap. High ETH fees are reportedly hindering new participants. 

As it stands, ZNN is primarily traded on Uniswap, but it’s time to expand to other markets.

There are many active traders in the community, and there are dev considerations. What are everyone’s thoughts on this?

-------------------------

aliencoder | 2024-11-14 09:14:01 UTC | #2

We need `ZNN` and `QSR` (and their wrapped counterparts) on as many chains, DEXs and bridges as possible to increase adoption.

-------------------------

john.maxwell | 2024-11-14 10:24:20 UTC | #3

You actually read my mind with this post. I also saw that swapping would cost someone even over 100$ when the gas fees are high. 

Just a couple of minutes ago I did some basic research and I can say that there are some libraries for Flutter build for Solana support.

Adding Solana for mobile and desktop wallet wouldn't be a problem, if it's desired.

-------------------------

TrevorLeahy3 | 2024-11-14 21:08:14 UTC | #4

1. Id say yes we should prioritize Sol. 

2. We could split the current rewards from wznn/eth and use half for new wznn/sol and then add some for wqsr/sol incentives. Both only need to be for a window of time months up to a year and then should re-assess.

-------------------------

Stark | 2024-11-15 00:13:09 UTC | #5

Regarding QSR, I don't think we should spread our resources/rewards. If anything, I'd say allocate a VERY small amount of rewards for a SOL/wQSR pool in order to support swaps of 150 QSR with minor slippage.

I will also refer to this previous post on the topic:
https://forum.zenon.org/t/discuss-opening-new-liquidity-pools-continue-orbital-campaign/1933/37

-------------------------

SugoiBTC | 2024-11-16 02:12:43 UTC | #6

1. Yes. Solana is growing at a fast pace and is much cheaper as opposed to Ethereum.

2. wZNN/SOL needs to be incentivized. Agreeing with @TrevorLeahy3 on his statement of splitting it 50/50 + Orbital campaign on SOL.

3. A bigger market for wQSR would be nice, but no priority. Ideally I would like to see it to become tradeable on a reputable CEX (T1)

-------------------------

coinselor | 2024-11-16 14:35:06 UTC | #7

In favor.

Let's make multi-chain multi again!

-------------------------

Samwinter1888 | 2024-11-16 15:42:53 UTC | #8

Sounds like a good idea, paying 100$ for swaps is a lot and if the price of ETH goes up so will the fees.

-------------------------

Stark | 2024-11-17 16:39:45 UTC | #9

base is another option. A reputable source weighed in saying SOL is overwhelmingly memes -which can be used as an argument in favor or against it.

I'm seeing BASE come up in my feed now.

My general sense is that people who favor base would be more amicable to going over to SOL if they want to buy wZNN, in contrast to SOL users who would see porting over to base as more high friction.

I also tend to see more people speaking in term of SOL on my feed. 

This is my subjective sense but the stats do support sol being where the action is. I hope to hear more opinions.

Option C would be to get more aggressive and go for both base and sol.

-------------------------

coinselor | 2024-11-17 20:33:01 UTC | #10

Let's add more chains. Our website has placeholders for literally every dex in existence including fantom, avalanche, polygon, etc. We are smart enough to realize base/solana are taking market share over those, so we pivot, but no reason to be single chain bridge especially when ETH fees are ridiculous.

-------------------------

WAGMI | 2024-11-18 17:11:13 UTC | #11

Yes, let's add solana

-------------------------

EovE7Kj | 2024-11-18 18:37:35 UTC | #12

I would also recommend that we deploy wZNN to TRON. I think TRC-20 is poised to see a huge growth in the near future, given the recent tether mint on TRX.

-------------------------

TheDev1776 | 2024-11-18 19:38:11 UTC | #13

Solana or Base/Arbitrum, whichever is faster to get up and running is paramount.

Cc: @sumamu

-------------------------

Stark | 2024-11-20 18:24:07 UTC | #14

1. Let's get a sense for which chains have the most support.

[poll type=multiple results=always min=1 max=6 public=true chartType=bar]
# Which chains? (Multiple select)
* Solana
* Base
* Tron
* Arbitrum
* Avax
* Polygon
[/poll]

2. How many chains do you think we should add? How to incentivize the pools, is a factor here. The more chains we add, the more spread out the LP rewards will be. Therefore the LP pools are likely to be more thin / volatile / potentially discouraging to large trades. Please comment to provide additional opinions on this factor.
[poll name=poll2 type=regular results=always public=true chartType=bar]
* Add 1 new LP incentivized chain.
* Add 2 new LP incentivized chains.
* Add 3 or more new LP incentivized chains.
[/poll]
3. How soon should we aim to achieve this?
[poll name=poll3 type=regular results=always public=true chartType=bar]
* Last week.
* ASAP.
* Zoon (some day in the future).
[/poll]

-------------------------

sumamu | 2024-11-21 11:56:52 UTC | #15

I am happy to see this initiative. 

Any member of the community can easily list wZNN and wQSR on all chains supported by the wormhole bridge.

However there are some minor disadvantages:
- token is owned by the wormhole bridge, which means we'd have to get in touch with most platforms to update the details of the token since we can't prove ownership. However some accept the deployed address for making changes
- bridging back to native ZNN and QSR will require going thru 2 bridges, so the UX might suck
- adding a new pair to the liquidity staking will require bridging the LP token thru 2 bridges
- if we ever want to bridge directly to any of the networks we might end up with 2 tokens
- relying on the security of wormhole

And the advantages
- very fast listing (1 hour)
- no extra efforts for orchestrators
- no extra development required
- absolutely anyone can do this, there's no need to wait for HCT to do it

-------------------------

TrevorLeahy3 | 2024-11-21 12:59:38 UTC | #16

A wrapped stablecoin ZTS from any network could be helpful.

-------------------------

aliencoder | 2024-11-27 16:01:39 UTC | #17

What's the status?

-------------------------

aliencoder | 2024-12-04 13:51:02 UTC | #18

Ping

-------------------------

SugoiBTC | 2024-12-04 18:57:14 UTC | #20

I'd like to see Base as our source chain, but from what @sumamu said, his team has already prepared the launch for BNB

-------------------------

shaimo | 2024-12-04 19:00:15 UTC | #21

I think going with BSC also gives us the chance to make people with old deprecated znn on it whole again. Disclaimer: I don’t own any so I don’t have any personal interest in it…

-------------------------

SugoiBTC | 2024-12-04 19:02:11 UTC | #22

I believe bridging to BSC will be another contract, not the same one that was used in the old pool. Need sumamu to confirm this though

-------------------------

shaimo | 2024-12-04 19:41:31 UTC | #23

Yes, of course. But will make it easy to come up with a simple dapp for 1:1 token exchange from the old contract to the new one

-------------------------

