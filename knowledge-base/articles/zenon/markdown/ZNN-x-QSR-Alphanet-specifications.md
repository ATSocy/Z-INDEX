Title: ZNN x QSR Alphanet specifications - Zenon - Medium

URL Source: https://medium.com/@zenon.network/znn-x-qsr-alphanet-specifications-83d27c005c09

Published Time: 2020-09-14T19:44:45.405Z

Markdown Content:
[![Image 15: Zenon](https://miro.medium.com/v2/resize:fill:44:44/1*rFXGQl3tfmku28AMjfzlAQ.png)](https://medium.com/@zenon.network?source=post_page---byline--83d27c005c09--------------------------------)

![Image 16](https://miro.medium.com/v2/resize:fit:700/1*X4J_Hmk1sbpJ4Ukl5rOBWg.png)

As the Network of Momentum Alphanet is nearing its release, a series of articles will be published to clarify some major aspects, such as use cases and strategic partnerships. This article approaches the following subjects: the refreshed coinmetrics, the roles of the network actors and their importance within the Zenon ecosystem.

## **PILLARS**

During Phase 0 of NoM, Pillars participate in the consensus protocol by producing and validating Momentum Intervals (blocks), thus being rewarded for securing the network. As full nodes, they also retain and archive the entire ledger history.

Pillars Requirements:
\- 15000 ZNN
\- 150000 QSR for Legacy Pillars
\- 160000 QSR or more for Regular Pillars, the calculation can be exemplified by using the formula: max(0, (number_of_pillars — 136 + 1)) \* 10000 + 150000 QSR to create the Pillar slot(\*).

Refund:
If a Pillar is disassembled, the 15000 ZNNs will be refunded to the original address that deployed it.
The QSR amount is burned in order to create the Pillar slot, so it is not refundable.

Revoke window:
\- After the initial registration of a Pillar, a cooldown period of 83 days begins
\- At the end of the cooldown period, there is a window of 7 days during which the Pillar can be revoked and disassembled upon user request.
\- This cycle repeats until the Pillar is revoked.

## **Pillar Categories**

_A. Legacy Pillars(\*)_
Pillars that were deployed prior to the Alphanet release can create the slot necessary for the Pillar burning for a fixed amount of 150000 QSR at any time, but only once. If the Legacy Pillar is revoked, it loses the Legacy Pillar status and will need to pay for the slot according to the formula above.

The Legacy Pillar slot is assigned to the public address used at the swap.

_B. Vested Pillars_
Granted to strategic partners.

_C. Pillars_
There can be an unlimited number of Pillars, which will require an additional 10000 QSR for each new Pillar slot in the network.

**Pillar Rankings**
Rankings are calculated based on the amount of ZNN delegated to each Pillar. Its position influences the number of Momentum Intervals a Pillar produces.

30 Pillars are chosen pseudo-randomly to produce the next 30 Momentums Intervals as follows:
\- 15 Pillars out of the top 30.
\- 15 Pillars out of all the Pillars that are not part of the previous lot.

**Pillar Reward**
The Pillar rewards are divided into two categories:
\- Momentum Interval rewards, distributed based on the number of Momentums a Pillar produced.
\- Delegating rewards, distributed proportionally to the amount of ZNN that was delegated to the each Pillar.

_\*\*Note: Pillar rewards are affected by the Pillars uptime. If a Pillar is assigned to produce 10 Momentums, but only produces half, it receives 50% of the rewards._

For example, assuming there are 100 Pillars in the network, the next results are expected:
\- Each Pillar ranking in the top 30 is expected to produce 169 Momentums daily.
\- Each Pillar ranking in the bottom 31–100 positions is expected to produce 50 Momentums daily.

## STAKERS

During Phase 0 of NoM, stakers will cease to participate in the consensus protocol but will still have the possibility to accumulate rewards.

**A. Delegating to a Pillar to obtain ZNN**

30% of the ZNN amount minted daily will be distributed as voting rewards to Pillars. Each account can delegate its balance to a Pillar, which in turn increases the Pillar’s voting power and the percentage of voting rewards that it will receive. This action neither locks nor transfers the balance of the delegating account.

Any Pillar can distribute a part or all of its rewards to the delegators to attract more votes and increase its ranking. This mechanism creates a free market that encourages engagement and fosters community growth.

**B. Staking to obtain QSR**

Requirements:
Staking for QSR requires ZNN which will be locked in a smart contract for a predefined amount of time (multiples of 30 days).

Refund:
After the locking period has ended, the staked amount can be refunded without any costs.

Rewards:
The daily QSR amount assigned to stakers is distributed based on the staked amount of ZNN and the locking period. The QSR amount for each staker is relative to the network’s conditions, and the daily calculations can be exemplified using the following formula:
weightedAmount = znnAmounnt \* (1 + (lockingPeriodInMonths — 1) / 12)

For example, assuming the following conditions:
\- Account A stakes 100 ZNN for a locking period of 1 month
\- Account B stakes 100 ZNN for a locking period of 11 months
\- Daily QSR amount assigned for stakers of 300 QSR
At the end of the day, the following results are expected:
\- Account A receives 100 QSR
\- Account B receives 200 QSR

## NODES

Nodes are also full archival nodes; they store, share and passively validate the ledger. They are rewarded with both ZNN and QSR.

_Requirements:
\- 5000 ZNN
\- 50000 QSR_

Eligibility:
To be eligible, a Node must meet the following conditions:
\- Be an up-to-date source of information regarding the network’s current state
\- Have a daily uptime \>90%

Refund:
If a Node is disassembled, both the ZNN and the QSR will be refunded to the original address used to deploy it.

Revoke window:
\- After registration of a Node, a cooldown period of 27 days commences.
\- At the end of the cooldown period, there is a window of 3 days during which the Node can be revoked upon user request.
\- This cycle repeats until the Node is revoked.

Rewards:
\- QSR and ZNN are equally distributed among eligible Nodes daily.

For example, during the first month, a bulk amount of 1960 ZNN/day will be distributed equally among eligible Nodes. If there are 100 Nodes in the network, at the end of the day, each Node will receive 19,6 ZNN.

![Image 17](https://miro.medium.com/v2/resize:fit:700/1*GqXBE27YFv2UGX1o5S2vFA.png)

_\*\*Note that the target Momentum Interval is 10 seconds, but the rewards are displayed per minute._

## **Zenon & Quasar Allocation Pool**

![Image 18](https://miro.medium.com/v2/resize:fit:700/1*dCSZ_ZxaH_I1sLLr08uL8Q.png)

## **QSR rewards structure**

![Image 19](https://miro.medium.com/v2/resize:fit:700/1*39_GdwH9W1Zk2JbIjqcbjw.png)

## Conclusion,

We hope this article clarifies aspects of Network of Momentum and ZNN-QSR coinmetrics. This is the first of articles series delivered in the following weeks as we proceed to follow the path of developing an ecosystem for decentralized applications to thrive.

Welcome to NoM Phase 0, Zenon Alphanet.
