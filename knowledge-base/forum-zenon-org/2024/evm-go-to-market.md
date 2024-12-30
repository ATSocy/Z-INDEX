Thread: evm-go-to-market
angelo_a_jr | 2023-06-29 23:19:27 UTC | #1

Perhaps this has been discussed somewhere or more internally planned with some of the development teams (CC: @sumamu) and there is reference on the Zenon website but it would be great to start publicly planning the next EVM-NoM compatibility rollouts.

Currently on the main website it lists the following:

Ethereum mainnet (Uniswap) (COMPLETED)
Polygon (Quickswap)
BNB Smart Chain (PancakeSwap)
Fantom (SpiritSwap)
Avalanche (TraderJoe)


IMO this still leaves out some very promising EVM chains such as Optimism (Velodrome, Uni on Optimism, etc.) and Arbitrum (Uniswap v3 on Arbi, Zyberswap, etc.) and there is probably some solid arguments to be made for even going after much more niche but engaged EVM communities. Heck, even Tron is #2 in TVL according to [DeFiLlama](https://defillama.com/chains/EVM) but not quite sure how compatible it actually is.

Would be great to start canvassing all the considerations, tradeoffs, etc. about the multichain rollout.  Some factors to consider:

-Technical implementation differences between each new EVM chain activation on the multichain bridge
-DEX availability and volume for different EVM chains
-Marketability
-LP rewards distribution
-Ecosystem compatibility (what dApps exist in each that might align with NoM?)
-???

By the end of July let's aim to have a solid rank-order plan in place for the rollout that ideally includes the following (at minimum) for each EVM chain: 
1. Timeline 
2. Technical Notes 
3. LP considerations 
4. Points of Contact to help publicity

I can help synthesize all points surfaced in this thread until mid-July and then start formatting a plan for the above.

-------------------------

aliencoder | 2023-06-29 13:54:07 UTC | #2

I would go with the networks that have the biggest `24h volume` in descending order:

1. [Arbitrum](https://defillama.com/chain/Arbitrum)
2. [BSC](https://defillama.com/chain/BSC)
3. [Polygon](https://defillama.com/chain/Polygon)
4. [Avalanche](https://defillama.com/chain/Avalanche)
5. [Optimism](https://defillama.com/chain/Optimism)

Why? Because they are the most liquid and have "real world" usage (best to be weighted over a period of 1 month).

-------------------------

mehowbrainz | 2023-06-29 23:19:36 UTC | #3

Topic moved to #development

-------------------------

