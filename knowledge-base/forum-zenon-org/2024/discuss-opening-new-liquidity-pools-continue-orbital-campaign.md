Thread: discuss-opening-new-liquidity-pools-continue-orbital-campaign
SugoiBTC | 2024-09-04 20:40:21 UTC | #1

Dear Zenon community,

There have been requests to start additional liquidity pools to enhance our ecosystem's liquidity. Additionally, we have a new opportunity to leverage the launch of the Supernova EVM and drive traffic to it. Building on @sumamu's [previous discussion](https://forum.zenon.org/t/wqsr-liquidity-pools-and-orbital/1545) and considering our previous Orbital campaign has [ended]((https://forum.zenon.org/t/liquidity-provisioning-campaign/1544) ), I'd like to reopen the discussion on the various options available, including the possibility of starting a new [Orbital Campaign](https://forum.zenon.org/t/road-to-100x/1484) specifically designed to promote Supernova.

Furthermore, we should consider incentivizing the ZNN/QSR pool on Ethereum. This could make it easier for individuals interested in spawning infrastructure to buy and sell through Uniswap, potentially lowering barriers to entry for new network participants and fostering greater decentralization. Another benefit of incentivizing the ZNN/QSR pool is the ability to get relisted on CG/CMC and visibility on Dexscreener, as tokens that don't have any transactions in the past 24 hours won't be visible and may not appear in search results.

## Proposed Options

1. **Incentivize:** wZNN/wQSR (ERC-20) Liquidity pool
2. **Add:** xETH/xZNN or xUSDT/xZNN (Supernova) Liquidity pool

## Funding Considerations

We have several options for funding these new LPs:

1. **Use Orbital reserves**
   * Current reserves: 254k ZNN / 596k QSR - https://zenon.tools/accounts/z1qxemdeddedxlyquydytyxxxxxxxxxxxxflaaae
   * Pros: Doesn't affect current LP rewards
   * Cons: Depletes our reserves

2. **Split current Orbital emissions**
   * Pros: Sustainable long-term solution
   * Cons: May reduce rewards for existing ERC-20 ETH/ZNN LP providers

### Which LP should we add?
[poll name=poll3 type=multiple results=always min=1 max=3 public=true chartType=bar]
* Incentivize wQSR/wZNN
* Add xETH/xZNN
* Add xUSDT/xZNN
* All above
[/poll]


### How should it be funded?
[poll name=poll4 type=regular results=always public=true chartType=bar]
* Use Orbital reserves
* Split current Orbital emissions
* Both (suggestions on how to implement are welcome)
[/poll]




Please share your thoughts and suggestions below!

-------------------------

cryptocheshire | 2024-09-04 20:21:27 UTC | #2

Why are these options all mutually exclusive?

-------------------------

coinselor | 2024-09-04 20:25:16 UTC | #3

Agree with Shazz, I think we should both split orbital emissions with however many more pools we want, plus add the multiplier bonus to kick off the initial liquidity campaign. It's not like we have enough liquidity to spread out over multiple chains/LPs. I wouldn't go with more than 3 incentivized pools.

Eventually, we'll probably split orbital emissions throughout LPs on all major EVM chains we support, but we're not there yet.

-------------------------

SugoiBTC | 2024-09-04 20:36:50 UTC | #4

I thought maybe we should start with adding one pool first or incentivizing wQSR/ZNN, but would mainly just want to reopen the discussion.

Unfortunately I'm unable to edit the existing polls, we can start a new one after we gained some more input from the community.

EDIT: remade the polls in the original post.

-------------------------

shaimo | 2024-09-05 01:13:32 UTC | #5

I’m not sure liquidity for xZNN is important for the time being. While I do hope we see growing activity on Supernova, I doubt it would be in the form of people bridging there usdt or ETH to buy xznn with it. And since our liquidity depth was always a challenge, I think we should focus it on a single network for the time being. If it’s Ethereum then let’s just do it there, so just incentivize wQSR/wznn for now.
We can always revisit this decision if/when needed.

-------------------------

DrD3 | 2024-09-05 05:36:43 UTC | #6

I'm with Shai on this one. Better to deepen the existing liquidity of the wQSR/wZNN pair rather than create a new one. 

A larger problem new/existing network participants face is the inability to acquire $QSR and set up infrastructure.

I'd just split orbital emissions between the two Pools- though maybe incentivize initial wZNN/wQSR LP'ers with a fraction of orbital reserves to get the ball rolling.

-------------------------

SugoiBTC | 2024-09-05 11:29:04 UTC | #7

The reason why I think starting a pool on xZNN would be beneficial is because we have https://alienswap.fun/ and Bagswap in the making. If we want to push our DEX's it would come in handy to have at least one pool on Supernova for people to trade on / enter the ecosystem from there.

It also helps with onboarding new folks and potentially converting back to native ZNN.

But I 100% agree with incentivizing the wQSR/wZNN pool.

-------------------------

shaimo | 2024-09-05 13:51:11 UTC | #8

I think alienswap and bagswap would mostly be used to swap between xznn and zts tokens. I don’t see many bridging eth or usdt to supernova, at least not right away.

-------------------------

coinselor | 2024-09-05 17:21:13 UTC | #9

Yeah, good point about Supernova. We can expect most pairs on bagswap/alienswap to be token/xZNN.

However, there's a case to be made to incentivize ETH/wQSR instead of wZNN/wQSR. The higher perceived impermanent loss of the ETH/wQSR might detract LPers, therefore a higher incentive is needed, imo. 

But maybe we could do all 3: ETH/wZNN (40%), ETH/wQSR (40%), wZNN/wQSR (20%) ?

-------------------------

SugoiBTC | 2024-09-05 21:37:26 UTC | #10

Yes that's a good point, if there are dApps built on Supernova I'd assume they'd launch their own token against xZNN. In that case it might be better to hold off with the xETH/xZNN pool and waste resources.

> But maybe we could do all 3: ETH/wZNN (40%), ETH/wQSR (40%), wZNN/wQSR (20%) ?

Dividing it over these three pools is also a nice option. However, how would we agree on the emission split between the pools? I'm worried that current LP stakers in the ETH/wZNN pool will be held hostage if we decide to fracture the Orbital emissions.

-------------------------

coinselor | 2024-09-06 17:05:01 UTC | #11

I assume most LPers are currently not locked, so our timing (Over 12 months after LP launch) would make that a non-issue for the most part, I think.

Regarding choosing the split probably what we are doing right now, debating to narrow down the best options. After that, who knows, AZ is probably not the right tool.

-------------------------

bayrum | 2024-09-08 00:10:24 UTC | #12

- Most of LPers are locked in for 12 months and will be held hostage. Can you get high ROI without locking in? I assume if you get rewards it's so small that it's not worth providing liquidity that's why I think most of them are locked in.
- Splitting can be counter intuitive if we need more liquidity depth when zenon will reach 10$+
- QSR can simply be added to Xeggex, wasn't this in their plan? 
- I think we should list QSR on Xeggex wait until we reach a higher price, attract more wznn/eth liquidity and see If we can fracture the orbital emission after enough liquidity is provided to sustain a good volume.

-------------------------

Stark | 2024-09-09 04:12:56 UTC | #13

wQSR/wZNN does not pose the same kind of risk of impermanent loss, as ETH or USDT pairs.

Therefore, the wZNN/wQSR Orbital rewards should be considerably smaller.

A plausibly bullish scenario on ETH/ZNN is 100X and beyond
A plausibly bullish scenario on wZNN/wQSR is 3X (maybe 10X if ZNN:QSR some day reaches 1:1)

-------------------------

shaimo | 2024-09-09 09:05:27 UTC | #14

They should be smaller than what? They are 0 now…

-------------------------

crack | 2024-09-09 10:10:29 UTC | #15

[quote="Stark, post:13, topic:1933"]
herefore, the wZNN/wQSR Orbital rewards should be considerably smaller.
[/quote]

competitive with sentinel reward, maybe lower is good since no minimum required to stake the LP

-------------------------

Stark | 2024-09-09 13:58:09 UTC | #16

Sorry that might have been confusing because I inadvertently replied to you, rather than the thread. 

I meant that there are enough rewards allocated to the ETH pool such that the liquidity provider market has found the APY at 70%. So I think we'd want to figure out roughly how deep we want the znn/qsr pool to be, and then set the portion of orbital rewards so that the market would find 10-15% APY.

I believe I've seen some comments about splitting the ETH Orbital rewards 50/50, with the znn/qsr pool. That would be too much. But moreover, please see below:

-------------------------

Stark | 2024-09-09 13:54:25 UTC | #17

Should we consider using orbital funds to directly fund the pool, rather than incentivizing LP'ers? ZNN and QSR will appreciate in value with a reasonable degree of parity. 

We could rebase the ratio to 5:1 or whatever we want, before depositing the ZNN/QSR into the pool, and then let the market do its thing.

This way, the orbital funds are not spent / distributed to LP'ers. The ZNN/QSR could later be withdrawn and put back into Orbital or used for some other purpose.

-------------------------

SugoiBTC | 2024-09-10 08:51:08 UTC | #18

I think reserving a small portion of the Orbital emissions for LP'ers of the wQSR pool is good, as they could put their QSR to work rather than keeping it idle in their wallet.

Maybe a percentage between 10%-20% would suffice, as IL on the ETH pairs could be a lot higher in the future.

-------------------------

coinselor | 2024-09-10 17:10:08 UTC | #19

[quote="bayrum, post:12, topic:1933"]
I think most of them are locked in.
[/quote]

Were locked in. It's been like ~14 months since the LP+Orbital campaing started. Most of the LPers are unlocked and earning max multiplier rewards and will continue to do so until they unstake.

-------------------------

crack | 2024-09-10 23:09:52 UTC | #20

I disagree ETH pair

Should rewarding wQSR/wZNN first, low IL, more confident for LPers, and more ZNN locked

-------------------------

SugoiBTC | 2024-09-11 00:24:10 UTC | #21

Yes, for now, the majority seems to be in favor of incentivizing the wZNN/wQSR pool.

The next thing we would need to agree on is whether to launch an ETH/wQSR pool, start a pool on Supernova, or do both. Based on the first poll, there appears to be interest in an LP on Supernova as well. However, considering the comments mentioned above, we might want to start with the wQSR pool first and reassess later when there's more demand for xETH/xUSDT/xZNN on Supernova.

I will start a new poll on Friday to gauge consensus. From there, we can think about the distribution of Orbital emissions, but suggestions are still welcome.

-------------------------

Stark | 2024-09-11 23:00:21 UTC | #22

If we directly use ZNN and QSR from the orbital fund to create the pool, (rather than community LP's) then the only "cost" to the orbital fund would be the impermanent loss between ZNN and QSR.

The liquidity could be pulled and returned to the orbital fund at any time.

-------------------------

SugoiBTC | 2024-09-12 01:14:45 UTC | #23

I still think it’s better to set aside a portion of the emissions for the pool, as it incentivizes users to put their spare QSR to work.

Impermanent loss will also be shared amongst liquidity providers, whereas if we use the reserves for the pool, the IL will hurt future Orbital campaigns, as it will create a discrepancy between ZNN and QSR in the fund.

-------------------------

TheDev1776 | 2024-09-12 15:17:50 UTC | #24

Seems like starting with wZNN/wQSR pool is the way to go, what are next steps?

-------------------------

Stark | 2024-09-12 20:29:21 UTC | #25

We can set the ratio to whatever we want before supplying the ZNN/QSR. So for example, the pool could be based at 1:5 ZNN:QSR if we think the relative value of qsr will rise, in order to mitigate IL.

We should run some numbers to see what the cost rewarding LPs is, vs the potential IL between ZNN/QSR if it is provided directly from orbital.

-------------------------

TheDev1776 | 2024-09-12 21:31:43 UTC | #26

I believe the 1:10 has always been the standard for this pair.  

Why not just keep start with that and keep it simple?

Question remains how much Orbital rewards to give...

-------------------------

NeoShredder | 2024-09-14 20:03:46 UTC | #27

Uniswap can route pairs with a common pair like ETH. A wQSR/eth pool is the best option. Uniswap will autoroute znn to qsr swaps. So we can have both znn/eth and znn/qsr swaps.

https://ethereum.stackexchange.com/questions/149403/uniswap-router-v2-pairing

-------------------------

Stark | 2024-09-15 09:27:55 UTC | #28

With a wZNN/wQSR pool, you won't have to insure the liquidity providers against potentially severe impermanent loss, like you would with an /ETH pool.

-------------------------

DrD3 | 2024-09-15 15:24:40 UTC | #29

I would rather we pair it at market rate which is currently 1:8. 

@SugoiBTC should we start a poll to gauge community sentiment on the ratio/distribution of orbital emissions?

-------------------------

SugoiBTC | 2024-09-16 15:46:12 UTC | #30

I believe that the ZNN/QSR pairing should be matched in terms of USD value, requiring a 50/50 split to contribute to the existing wZNN/wQSR pool.

I should have provided more detail in the initial polls, specifically in the poll titled **"How the LPs should be funded."** This was intended to propose launching a new Orbital Campaign on Supernova, utilizing our reserves to effectively kickstart it.

If we only look at incentivising the wQSR pool, I would refrain from using the reserves but allocate emissions to it with the following reasoning:

|**Factor**|**Using Orbital Emissions**|**Using Orbital Reserves**|
| --- | --- | --- |
|**Sustainability**|Continuous and long-term, as emissions are ongoing|Finite resource, once depleted cannot be replenished|
|**Impact**|Steady incentives, but emissions would need to be split between multiple pools, reducing per-pool rewards|Strong short-term boost, high-impact use|
|**Inclusivity**|Incentivizes users who don’t have enough QSR to spawn sentinels|Does not affect QSR requirements, but may not incentivize smaller participants effectively|
|**Impermanent Loss (IL)**|Encourages sharing of IL among participants|May place more burden of IL on the reserves|
|**Flexibility**|Tied to the ongoing emission schedule, less adjustable|Highly flexible in the short term, provides liquidity when needed|
|**Long-term Resource Preservation**|Preserves reserves for future use|Depletes finite reserves, limiting future flexibility|
|**Participation Barrier**|Lowers entry barriers, encouraging broader community participation|Does not stimulate community participation; fewer incentives for broader involvement|

**Summary**
* **Orbital emissions** encourage broader participation by incentivizing users without enough QSR to spawn sentinels and help share IL, making it more inclusive and community-driven.
* **Reserves** can be a powerful tool for targeted liquidity boosts but are finite, limiting long-term flexibility and inclusivity.

> @SugoiBTC should we start a poll to gauge community sentiment on the ratio/distribution of orbital emissions?

Yes, if there are no further objections we can start looking into the percentage of the Orbital emissions that we can allocate to the wQSR pool.

-------------------------

Stark | 2024-09-16 20:23:28 UTC | #31

Does the Orbital address receive ZNN/QSR token emissions?

-------------------------

SugoiBTC | 2024-09-16 22:43:10 UTC | #32

I'm not sure. From what I'm seeing is that the Orbital address only holds the reserves. I think the emissions are baked into the protocol and are being sent through [this address](https://zenonhub.io/explorer/account/z1qxemdeddedxt0kenxxxxxxxxxxxxxxxxh9amk0), but maybe someone in the community can check the code to verify this.

-------------------------

crack | 2024-09-17 05:28:22 UTC | #33

No, same case with AZ address afaik

-------------------------

SugoiBTC | 2024-09-17 20:12:13 UTC | #35

I ran some prompts in ChatGPT and came up with several scenarios to adjust the orbital emissions, aligning the APY of the wQSR pool with the current APR that sentinels provide (11.67%). These scenarios also consider the impact on the ETH/wZNN pool.

## Input Data
- Daily Orbital emissions: 561.6 ZNN + 1250 QSR

- Current Sentinel APR: 11.67%

- Current ETH/wZNN Pool APR: 72.4%
## Scenarios
### Scenario 1: 500k wQSR pooled
- Orbital Emissions Allocated: 12.79%
- Resulting APR for wZNN Pool: Decrease to 63.14%

- Resulting APY for wQSR Pool: 11.67% (target achieved)

### Scenario 2: 1m wQSR pooled
- Orbital Emissions Allocated: 25.58%

- Resulting APR for wZNN Pool: Decreases to 53.88%

- Resulting APY for wQSR Pool: 11.67% (target maintained).

### Hypothetical Scenario: 12.79% allocation with pool size increasing to 1m wQSR
- Orbital Emissions Allocated: Maintained at 12.79%

- Expected APR for wZNN Pool: Remains at 63.14% (no change in percentage allocation).

- Resulting APY for wQSR Pool: Decreases significantly to approximately 5.84%

## Impact on ETH/wZNN Pool
- Original APY with 100% Emissions: 72.4%

- New APY After 12.79% Reallocation (to match Sentinel APR at 500k wQSR pooled): Approx. 63.14%, reflecting a modest decrease but maintaining substantial rewards.

- New APY After 25.58% Reallocation (to match Sentinel APR at 1m wQSR pooled): Further reduced to approx. 53.88%, demonstrating a significant impact.

## wQSR Pool Analysis
- 500,000 QSR Pool: Allocating 12.79% of the total emissions achieves the target APY of 11.67%.
- 1,000,000 QSR Pool: To maintain the same APY for a larger pool, 25.58% of the total emissions is necessary. 

## Supporting Tables

### Main Scenarios
| Scenario | Pool Size (wQSR) | Orbital Emissions Allocated | Resulting APR for wZNN Pool | Resulting APY for wQSR Pool |
|----------|------------------|-----------------------------|-----------------------------|------------------------------|
| 1        | 500,000          | 12.79%                      | 63.14%                      | 11.67%                       |
| 2        | 1,000,000        | 25.58%                      | 53.88%                      | 11.67%                       |

### Hypothetical Scenario
| Scenario     | Pool Size (wQSR) | Orbital Emissions Allocated | Resulting APR for wZNN Pool | Resulting APY for wQSR Pool |
|--------------|------------------|-----------------------------|-----------------------------|------------------------------|
| Hypothetical | 1,000,000        | 12.79%                      | 63.14%                      | ~5.84%                       |

## Conclusion
In a hypothetical scenario where the wQSR pool size increases to 1 million QSR while the orbital emissions allocation remains at 12.79%, the APY for the wQSR pool would decrease significantly, approximately halving to about 5.84%.

Given that impermanent loss (IL) is considered less important in the wZNN/wQSR pool, should we consider a 5.84% APY sufficient enough for liquidity providers?

Please share your thoughts on this.

-------------------------

0x3639 | 2024-09-17 21:40:51 UTC | #36

[quote="SugoiBTC, post:35, topic:1933"]
Given that impermanent loss (IL) is considered less important in the wZNN/wQSR pool, should we consider a 5.84% APY sufficient enough for liquidity providers?
[/quote]

5.84% is too low IMO.  Impermanent Loss does not go away.  We just think the wZNN to wQSR ratio will remain 10:1.  But what if it goes to 3:1?

-------------------------

Stark | 2024-09-18 05:04:56 UTC | #37

Orbital is funded at 2:1 QSR:ZNN
Circulating supplies are 3:1 QSR:ZNN

There are still big bags of QSR being swapped p2p at 10:1 and 9:1. There hasn't been a situation where someone who wanted to purchase QSR, hasn't been readily able to.

The p2p market is still efficient and given the token supplies, orbital ratio, and the upcoming launch of utility on NoM, it would be wise to wait until QSR has more opportunity for price discovery. 10:1 references all the way back to the alphanet inception.

We don't even have decent volume on wZNN. I don't see the purpose of depleting or spreading Orbital reserves to incentive a market with so little use at this stage.

Furthermore, from a marketing perspective, we have so much jargon flying around for a network that is often described as "too confusing". I suggest we try to simply say "Zenon" and "ZNN" as much as possible until we gain more traction. We are already spread so thin.

p.s. The tiny QSR LP on ETH supports a QSR buy for max plasma. The only problem is that it's fee inefficient. Maybe we can get those LP's to move their liquidity over to xQSR/xZNN.

QSR is inherently a few levels deeper into the rabbit hole anyway. When a new person asks how to invest in Zenon, we don't want to be leading with, "Well the NoM has a dual token ec... 💀". 

Q) What is NoM?
A) Oh, it's this other name for Zenon. We also call it....

Q) You have two names? Ok, should I buy ZNN or NoM?
A) ACTUALLY, the other token is called QSR...

Q) What is NoM?
A) The Network of Momentum, which is also Zenon. But in the whitepaper it is sometimes called the momentum network.

Q) Have you heard of HBAR?

-------------------------

