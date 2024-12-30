Thread: wp1-governance-spec-feature-vote
georgezgeorgez | 2024-11-14 08:28:36 UTC | #1

Developers should serve the requirements of the community.
We cannot accept contributions to the codebase just because they exist or how much effort was spent.

There's been some ongoing discussion and debate regarding Governance:
https://forum.hypercore.one/t/wp1-governance-spec/545
https://forum.hypercore.one/t/universal-governance-module-proposal/544

Technical mechanisms must be comprehensible in the language of its users. In the case of governance, the users will be Pillars. The role of a protocol designer is to take the desires of the community, analyze them for cryptoeconomic security, and translate them into implementation-neutral instructions.

The role of a protocol developer will be to take a specification and implement it for a given platform. Currently we only have go-zenon, but in the future we may have rusty-zenon, so a clear spec will be required so that both implements perform the exact behavior.

**The following vote will serve as a guideline for spec definition. It is non-binding. The scope will be limited to what gets deployed onto hyperqube_z.** Factors such as deployment feasibility will impact what is actually delivered to hyperqube_z. Future work packages will include the deployment of governance onto mainnet with any lessons learned from testing on hyperqube_z.

For multiselect questions, choose as many options, including none, as desired.

In general, the options will go from more conservative to less conservative in terms of changes made.
Depending on scope, we may have additional follow-up questions in the future.

---

For the governance embedded contract on the hyperqube_z extension chain:

Q1: Should different voting requirements and thresholds apply to different types of governance actions? Specifically, should we classify different actions into [Type 1 and Type 2](https://www.theuncertaintyproject.org/tools/decision-types) decisions?
Options:
- A: No
- B: Yes
- C: Other (with explanation)

Q2: What should the default voting requirements be? If applicable: for Type 1 decisions, and starting requirements for dynamic quorums.
Options:
- A: Greater than 2/3 of all voting eligible pillars
- B: Greater than 1/2 of all voting eligible pillars
- C: Greater than 1/2 of votes with a 1/3 voting eligible pillar quorum (Same as AZ)
- D: Other (with explanation)

Q3: What should the default voting duration be? If applicable: for Type 1 decisions, and starting requirements for dynamic quorums.
Options:
- A: 15 Days
- B: 30 Days
- C: 45 Days
- D: 60 Days
- E: Unlimited
- F: Other (with explanation)

Q4: If applicable, what should the voting requirements be for Type 2 decisions?
Options:
- A: Greater than 2/3 of all voting eligible pillars
- B: Greater than 1/2 of all voting eligible pillars
- C: Greater than 1/2 of votes with a 1/3 voting eligible pillar quorum (Same as AZ)
- D: Other or N/A (with explanation)

Q5:If applicable, what should the voting duration be for Type 2 decisions?
Options:
- A: 15 Days
- B: 30 Days
- C: 45 Days
- D: 60 Days
- E: Unlimited
- F: Other or N/A (with explanation)

Q6: What should the requirement be for submitting governance proposal?
MULTISELECT: Options:
- A: ZNN Burn
- B: ZNN Deposit (returned upon passing vote)
- C: Must be Pillar
- D: Limited to 1 proposal per Epoch
- E: Other or N/A (with explanation)

Q7:  Should removing pillars from voting eligibility (caging) based on momentum production activity be part of scope for this work package?
MULTISELECT: Options:
- A: For Governance
- B: For Accelerator-Z
- C: For Momentum Production
- D: Other (with explanation)

Q8: Should we implement dynamic quorum requirements to eventually resolve votes that fail to get enough YES or NO votes?
- A: No
- B: Yes
- C: Other (with explanation)

-------------------------

georgezgeorgez | 2024-11-14 08:28:21 UTC | #2

Question| Answer| Notes |
|--- | --- | --- |
|Q1 |B | Yes to type1/type2 decisions|
|Q2|  A|  >2/3 should be required for sporks|
|Q3 | E|  For sporks creation, I would want to give either 45 or 60 days for pillars to decide. For spork activation however, I could see the merits of shortcutting the time once a certain amount of votes are achieved. For example, if >2/3 pillars (and likely other participants) signal they already have the new spork code running, then a speedy activation could be warranted with some possible buffer time. Getting READY signals from Sentinels is something we will have to tackle later if not now.
|Q4|  B| >1/2. Although I would be fine with what AZ has as well | 
|Q5|  B|  30 days|
|Q6|  BCD| 1 ZNN deposit, returned after passing a vote, limited to 1 proposal per pillar a day |
|Q7|  A| Caging governance voting pillars based on momentum production. Long term it should apply to AZ and momentum election too, so I'm ok adding the others into scope if it's easy. But it shouldn't be something that holds us up. |
|Q8|  C|  Dynamic Quorum is a potentially useful and potentially dangerous idea. It provides a disaster recovery mechanism that doesn't require hardforks. It would be interesting to test it on hyperqube_z but I don't think we should let it be something that delays us. I think we can probably suffice with high level pillar caging based on momentums. I would possibly want to revisit if we ever do hard fork or two on hyperqube_z or mainnet. |

-------------------------

SultanOfStaking | 2024-11-15 02:03:46 UTC | #3

MVP we can submit governance proposal to change later :) 

1 B
2 A
3 B
4 BC IDK...
5 A
6 ABD
7 ABC
8 A

-------------------------

nexuspillar | 2024-11-15 06:59:28 UTC | #4

Q1 B
Q2 A
Q3 C
Q4 B
Q5 B
Q6 BCD
Q7 ABC
Q8 C (not at this stage)

-------------------------

vilkris | 2024-11-15 15:14:47 UTC | #5

|Question|Answer|Notes|
|---|---|---|
|Q1|B|Yes to type1/type2 decisions|
|Q2|A||
|Q3|C||
|Q4|C|AZ style for familiarity|
|Q5|A|Same length as AZ for familiarity|
|Q6|BCD|1 ZNN deposit, returned after passing a vote, limited to 1 proposal per pillar a day|
|Q7|A/D|I would prefer keeping the scope on the governance contract in this WP. A caging mechanism could possibly be a completely separate WP, so that no caging mechanism is included in this governance WP.|
|Q8|C|We could explore this idea later.|

-------------------------

SultanOfStaking | 2024-11-16 00:46:01 UTC | #6

Context - Thinking burn 1 minimum then deposit ~4 you get back if you get approved

Also 30 days is more than enough IMO even for level 1. I think 15 days is a long time if you’re engaged. A lot can happen in 15 days

-------------------------

SultanOfStaking | 2024-11-16 00:51:57 UTC | #7

If I’m honest 30 days feels obscene

-------------------------

sugoibtc | 2024-11-16 02:02:43 UTC | #8

Q1: B
Q2: A
Q3: C
Q4: C 
Q5: B
Q6: BCD
Q7: ABC - Priority to A
Q8: C - currently N/A

-------------------------

coinselor | 2024-11-16 13:06:56 UTC | #9


|Question|Answer|Notes|
| --- | --- | --- |
|Q1|B||
|Q2|A||
|Q3|D|I'm going with 15 days for hyperqube_z. Probably 60 for Alphanet.|
|Q4|B||
|Q5|A||
|Q6|BC||
|Q7|ABCD|Given this is a resource intensive task it probably should be researched, developed, and tested in isolation|
|Q8|C|We could fake black swan events on hyperqube_z and consider the implications/improvements this feature might bring|

-------------------------

Stark | 2024-11-16 16:31:47 UTC | #10

@georgezgeorgez can you clarify:

Q7: Should removing pillars from voting eligibility (caging) based on momentum production activity be part of scope for this work package?

MULTISELECT: Options:

• A: For Governance
• B: For Accelerator-Z
• C: For Momentum Production
• 😧 Other (with explanation)

=================

...it looks like we're supposed vote on which activities a non-momentum-producing pillar would get prohibited/caged from.

In other words, a caged pillar would not be able to:

A. Vote for Governance
B. Vote for AZ
C. **Produce Momentums?**

This looks to me like voting pillars out of the network. Is that correct? I want to make sure we are all understanding this in the same way.

-------------------------

digitalSloth | 2024-11-17 09:08:10 UTC | #11

|Question|Answer|Notes|
| --- | --- | --- |
|Q1|B||
|Q2|A||
|Q3|B|Lower on HyperQube for testing|
|Q4|C||
|Q5|A||
|Q6|BCD|1 ZNN deposit, returned after passing a vote, limited to 1 proposal per pillar a day|
|Q7|AD|Focus should initially be for governance but with a mind to apply it to AZ & Momentum production. How would uncaging work? There needs to be a way for a pillar to signal they want to play an active role in the network again, maybe an uncage function on the pillar contract requiring a 1 ZNN burn for example |
|Q8|C||

-------------------------

Bzed | 2024-11-17 15:06:26 UTC | #12

|Question|Answer|Notes|
|---|---|---|
|Q1|B|
|Q2|A
|Q3|D| With voting to end once super majority is met. Activation based on signaling
|Q4|B|
|Q5|B|
|Q6|D|Limited to 1 proposal per epoch, pillars only|
|Q7|D|No, QSR burn equals one vote|
|Q8|C|Might be an important idea. Needs testing|

-------------------------

Stark | 2024-11-17 22:20:44 UTC | #13

Q1: B
Q2: A
Q3: B
Q4: C
Q5: A
Q6: B, C, D
Q7: A, B, C (provided that there is a permissionless way to uncage oneself)
Q8: A

-------------------------

georgezgeorgez | 2024-11-18 14:41:12 UTC | #14

If we actually implement caging, we will refine the details as a community.
But the way I would spec it out would be like:

If you don't produce any momentums for say a 3 days. Then you are caged.
You are token out of the eligible pillar set for governance, az, and pillar election for momentums.
After a period of 2 weeks, you can sign a message to uncage yourself.

The two weeks is the penalty, but a pillar can uncage itself anytime after it.
That's how I would approach it.

-------------------------

