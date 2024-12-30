Thread: universal-governance-module-proposal
sumoshi21 | 2024-11-05 11:39:55 UTC | #1

Hello!

I'm proposing a flexible governance embedded that will fulfill all of our current necessities and even beyond.

The governance embedded contract will be able to:

1. Create sporks to upgrade the network codebase
2. Change network parameters that were previously only accessible to admins


We are basically solving 2 problems at once with my proposed architecture for the embedded contract.

The process goes as follows:

One must spend 1 ZNN in order to make a governance proposal. This anti-spam mechanism is also implemented for ZTS creation or AZ proposals.

Once the account-block is sent to the governance embeded, the Pillars can start voting on the proposal.

The threshold to pass this proposal is 51% of registered Pillars. I've chosen a bigger threshold because network governance needs wider Pillar participation and support to implement changes that will impact everyone.

Point 1 is pretty self-explainatory: instead of the current hardcoded spork address to create a spork block and active the spork, we'll be able to activate network upgrades if the proposal has enough votes and passes.

Point 2 is more interesting: we will be able to change network parameters that were reserved only for centralized admins like adding new networks in the bridge or modifying params in the liquidity contract.

I've managed to make a working implementation and I'll release the source-code zoon. 

In technical terms, a proposal is a custom account block that will be sent from the governance embedded to the other embedded contracts. We will add permission for the governance to all embedded contracts so for example, not only the bridge administrator could call "SetNetwork" but also the governance.

-------------------------

sumoshi21 | 2024-11-05 13:35:46 UTC | #2

https://github.com/sumoshi21/go-zenon-governance

-------------------------

georgezgeorgez | 2024-11-05 16:53:46 UTC | #3

https://forum.hypercore.one/t/wp1-governance-spec/545

-------------------------

sugoibtc | 2024-11-05 23:10:09 UTC | #4

Thank you for initiating this initiative zir. A governance module is much needed in order to move NoM forward. That said, I’m a bit concerned that we may struggle to reach the 51% pass rate in most cases, especially since some Pillars either don’t vote at all (with less than a 10% voting rate) or have been offline for a long time (not producing momentums). Could we consider adding additional rules for the pass rate? With a 51% threshold, achieving quorum could be challenging.

Also as @georgezgeorgez mentioned, for HyperQube_z's (hq_z) first Work Package (WP), we’re aiming to stimulate as much open collaboration as possible and involve the community. I’d like to invite you to join us in developing the specs for hq_z before implementing it on mainnet. This work will of course, be incentivized.

-------------------------

aliencoder | 2024-11-05 21:52:19 UTC | #5

Great work @sumoshi21! A much needed upgrade to NoM.

[quote="sugoibtc, post:4, topic:544"]
I’m a bit concerned that we may struggle to reach the 51% pass rate in most cases
[/quote]

I think the threshold is simple and fair. 51% consensus is really important for network wide upgrades. AZ quorum has a lower threshold because it doesn't impact the network as a whole, just the AZ treasury. Plus it's only limited to 5k ZNN 50K QSR so little "damage" can be caused.

We can't go with lower values for this threshold and also we can't get higher either. 51% is the sweet spot for security and participation.

-------------------------

Chuckerboy | 2024-11-05 22:49:27 UTC | #6

51% of pillars, it will be stuck for waiting pillar to reach quorum vote. 

51% of active (creating momentum) pillars or
even 51% of active pillar that more than 33% vote rate is good imo

-------------------------

sugoibtc | 2024-11-05 23:10:53 UTC | #7

Hmm.. I just checked the numbers and 31/95 pillars have <10% voting rate. 7 of these pillars are offline, 51% quorum could work. Especially if the goal is upgrading the network.

-------------------------

sumoshi21 | 2024-11-06 09:16:05 UTC | #8

For the issue of 50% + 1: If you can't count on them to vote, then you can't count on them to upgrade the node, and then we've got bigger problems.
There's no need to overthink it. The embedded contracts that will be governable need to define dedicated functions accessible only to the governance module. It's not mean to govern the ungovernable and over complicate it. If we'll want to govern certain aspects of the network, new embeddeds will need to be deployed for those specific needs and we can now achieve it by vote.

-------------------------

sumoshi21 | 2024-11-06 16:46:04 UTC | #9

I like the idea of type 1 and type 2. For now, type 1 is just creating and activating a spork. Others would be type2. Type1 should be at least the majority required for consensus which 66% + 1 for NoM. Type2 like adding networks to the bridge could remain 50% + 1.

 I don't think we need to implement the logic in order to send ZNN or QSR, we just don't need it now, there is no functionality for it, just create an accelerator proposal insead of a type1/2 that would transfer. Handling ZTS transfers is purely beyond the scope of a governance embedded contract.

I also don't think we need a dynamic quorum for now. One pillar, one vote for all the remaining time. If pillars don't vote, there is no interest in the proposed change. Why should the quorum lower?

We might need to increase the period from one month for type1.

-------------------------

aliencoder | 2024-11-07 11:30:47 UTC | #10

I agree with the fact that handling ZTS is both beyond the scope of a Governance embedded and also potentially dangerous.

Dynamic quorum is also very dangerous: you'll be able to pass proposals impacting everyone with a minority.

Let's not overthink and underdeliver. I strongly suggest we deploy this Governance Module asap.

-------------------------

edgepillar | 2024-11-07 16:57:00 UTC | #11

Why don't we consider including Sentinels in the voting? Wouldn't it be better for diversity of opinion and consensus?

-------------------------

0x3639 | 2024-11-08 01:52:39 UTC | #12

[quote="aliencoder, post:10, topic:544"]
Dynamic quorum is also very dangerous: you’ll be able to pass proposals impacting everyone with a minority.
[/quote]

agree.  I listen to many pods where strange blockchain proposals get approved when people are not watching.  It's a real risk.

-------------------------

aliencoder | 2024-11-10 14:30:23 UTC | #13

[quote="edgepillar, post:11, topic:544"]
Why don’t we consider including Sentinels in the voting
[/quote]

We currently don't have a well defined Sentinel participant yet.

Let's stick with battle tested setups and we have plenty of time to refine the Governance Module in the future.

We need it asap to be able to:

1. Change the network emission
2. Integrate the new extension-chains embedded
3. Perform admin tasks for the bridge

-------------------------

sugoibtc | 2024-11-10 23:57:27 UTC | #14

Zend it

-------------------------

coinselor | 2024-11-13 11:29:07 UTC | #15

First, I want to thank @sumoshi21 for taking the initiative to draft an implementation for the governance module. This has been long overdue and is a crucial step for the future of our network.

I appreciate how quickly Sumoshi integrated feedback and made changes. However, George’s insights present a compelling argument against the current approach, which we should carefully consider.

[quote="georgezgeorgez, post:5, topic:545"]
The suggestion for dynamic quorum would be for robustness. It’s very likely that over the years pillars will stop functioning but not deconstruct (if people die without succession plans). Likely we will need a consistent mechanism to take them out of the pillar pool for both momentum creation and voting quorums, with a way to get back in (e.g. a signature of liveliness).

Consider the following:

Let’s say we get a bunch of pillars in China. 40%. But then China decides to completely cut off outside internet access. We can’t reach 66% + 1 for an upgrade. We can’t spork to lower the threshold since that would require the same threshold. Without a dynamic quorum, a hardfork would be required. And that could be acceptable given the circumstances. I am providing a possible solution for network survivability without hardforks.

Dynamic quorum also means people need to either vote NO for changes or get out of the way for progress. Someone who can’t be bothered to vote may be bothered to upgrade if they see everyone else is. Greater momentum. Enough time would need to be given however.
[/quote]


It’s encouraging to see @aliencoder and @georgezgeorgez, along with other network developers, joining the discussion. I’d love to hear from even more voices, as this change deserves thorough review and due process.

While I recognize different preferences for pace, I tend to favor caution with significant changes like this. If speed had been a priority, I would have recommended drafting the implementation a year ago, during the initial discussions. We had the time, so there’s no need to rush now.

At this point, I support testing the governance module in a live production environment, such as hyperqube_z. It seems it will be live soon, and I can’t think of a better way to stress-test it.

On this note, I’d also like to see other developers receive compensation for their work on the Governance Module AZ—especially contributors like George, who have invested substantial time and thought and will be involved in testing the module. It would reflect well on our network if this effort is a collective achievement by a majority of our developers.

-------------------------

SultanOfStaking | 2024-11-13 13:19:51 UTC | #16

I read coins post and wasnt sure what to make of it but after letting it sit for a minute I am aligned. Maybe this is our chance to turn AZ from a spray and pray (not saying this is... but many are) to a process that gets the attention it deserves. Not saying anything everyone here doesnt know but governance is a unique animal and can have disproportionate impact compared to most of what goes through here.

I would be in favor of having a twitter spaces discussion (or similar) with sumoshi, alien, and george (since they are all actively working on this topic) plus other devs / pillars / community members. 

I dont want us to slow down or get to a point where there are so many stage gates to funding that people are not motivated to build, but I think some of the things we are discussing deserve more than a few responses in a forum every day or two.

I can make time Friday / this weekend if we were to actually do this - not that I am key to this discussion, but I would like to practice what I preach :)

-------------------------

sumoshi21 | 2024-11-13 16:00:29 UTC | #17

As I said, even if China cuts the connection to the Internet and 50% e.g. of pillars can't connect, having a quorum that decreases over time means that all proposals will be accepted, even proposals that are a joke, or the community and pillars disagree with, in case of pillar inactivity. An analogy for the accelerator contract means that all proposals will be accepted (and funds released) with a few yes votes on the long term if other pillars don't vote. And we have a solution for that edge case of blackout, as george said, hard fork or the spork address.

On the implementation side, these are the methods that the governance contract will be able to call:
**Spork**:
* 	CreateSporkMethod
* 	ActivateSporkMethod

**Bridge**:
	* SetNetworkMethod
* 	RemoveNetworkMethod
* 	SetNetworkMetadataMethod
* 	SetTokenPairMethod
* 	RemoveTokenPairMethod
* 	HaltMethod
* 	UnhaltMethod
* 	EmergencyMethod
* 	ChangeTssEcdsaPubKeyMethod
* 	ChangeAdministratorMethod
* 	SetAllowKeyGenMethod
* 	SetOrchestratorInfoMethod
* 	SetBridgeMetadataMethod
* 	RevokeUnwrapRequestMethod
* 	NominateGuardiansMethod

**Liquidity**:
	* FundMethod
* 	BurnZnnMethod
* 	SetTokenTupleMethod
* 	SetIsHalted
* 	UnlockLiquidityStakeEntries
* 	SetAdditionalReward
* 	ChangeAdministratorLiquidity
* 	NominateGuardiansLiquidity
* 	EmergencyLiquidity

Type1 proposals are the ones that have the destination the spork contract, the voting period is 45 days and the threshold is 66%.
Type2 proposals are all other one, the voting period is 30 days and the threshold is 50%.
We could discuss these variables.
The cost of creating a proposal is 1 ZNN. Personally I would increase it to 5 ZNN, even if the price goes up and the proposal is accepted, one could get them back from the accelerator if he really needs them. I saw there is also some spam with 1 ZNN for accelerator projects and we need to make it as easy as possible for pillars to vote only on serious proposals, not scroll on all.

I believe this is a good version for V1, if we decide in the future that we should add dynamic quorum or any other functionality, one should implement it, test it, audit it and could propose it and see if pillars agree and vote. Otherwise, we will just spend another year discussing once in a while on the forum about impact, possibilities and nothing will be practically achieved.

-------------------------

sumoshi21 | 2024-11-13 16:04:41 UTC | #18

[quote="coinselor, post:15, topic:544"]
On this note, I’d also like to see other developers receive compensation for their work on the Governance Module AZ—especially contributors like George, who have invested substantial time and thought and will be involved in testing the module. It would reflect well on our network if this effort is a collective achievement by a majority of our developers.
[/quote]

I totally agree that testing and auditing each other's code should not be done for free. We should encourage that and speed up the acceptance or denial of PR.

-------------------------

aliencoder | 2024-11-13 16:10:53 UTC | #19

[quote="coinselor, post:15, topic:544"]
This has been long overdue and is a crucial step for the future of our network.
[/quote]

Totally agree.

[quote="coinselor, post:15, topic:544"]
George’s insights present a compelling argument against the current approach, which we should carefully consider.
[/quote]

Dynamic quorum is a trojan horse for the Gov module. It introduces potential weaknesses and vulnerabilities that can be exploited by malicious actors. I'm agaist it because in the case of a network partition the CAP theorem states that the consensus will always favor consistency. It's the same trade-off between safety and liveness. The consensus must always favor safety over liveness (better stop the chain than making progress with incorrect state transitions).

-------------------------

0x3639 | 2024-11-13 18:23:11 UTC | #20

As part of this AZ would you be willing to prepare a ZIP - Zenon Improvement Proposal and test the deployment on Hyperqube before pushing to mainnet?

The governance module is core to the inner workings of NoM.  I look at all the testing that @vilkris @georgezgeorgez and @CryptoFish do for protocol level work and it's extensive: months of testing.  DP has been in design and testing for what seems like a year.  

I think it's really important that we test this work extensively before bringing it to mainnet.  Hyperqube seems like a good place to test it.  Also, we can iterate quickly on hyperqube if we find an issue.  Pillars will be active and many devs are looking at this work.

Also if we test on Hyperqube I think we will engage with more devs, more will look at the code, and we will have a public testing process that pillars can see and monitor.

-------------------------

Stark | 2024-11-13 21:53:05 UTC | #21

![Screenshot 2024-11-13 at 4.52.45 PM|690x390](upload://8jvX3bhZ3MXBqGuXyVgWSDL6t23.jpeg)

-------------------------

aliencoder | 2024-11-14 08:58:06 UTC | #22

[quote="0x3639, post:20, topic:544"]
protocol level work and it’s extensive: months of testing
[/quote]

The only production embedded contracts were designed, developed and deployed by @sumamu & co team. And I remember that the audit results for their Solidity contracts were flawless.

[quote="0x3639, post:20, topic:544"]
I think it’s really important that we test this work extensively before bringing it to mainnet.
[/quote]

I agree. But maybe they've already tested everything in the meanwhile.

-------------------------

sumoshi21 | 2024-11-14 09:22:00 UTC | #23

I agree with testing the code anywhere you want, my intention is not to work alone in this community and I am always teamed up with sumamu. I just hope there will be pillar activity on this testnet, explorer that can interpret the account block data, available RPC, faucets so that we could stress test the contract.

-------------------------

sumoshi21 | 2024-11-14 09:25:16 UTC | #24

@georgezgeorgez I am unable to follow your replies, could you please respond here? Why would you open another thread?

-------------------------

sumoshi21 | 2024-11-14 10:08:21 UTC | #25

As an asnwer to geroge's questions, I believe it's important that I answer, even though I am not a pillar. I cannot reply on that post. 
https://forum.hypercore.one/t/wp1-governance-spec-feature-vote/554

|Question |Answer |Notes|
|---|---|---|
|Q1 |B |Yes to type1/type2 decisions|
|Q2 |A | The minimum requirement for sporks must be the consensus requirement, which I believe is 66%|
|Q3 |C |I think 45 days at most is enough so that all pillars can see the proposal and understand it. I would not let it unlimited, if there is no interest in it, there is no vote, simple. If pillars change their minds, just create the proposal again. |
|Q4 |B | I think 50% is fine, altough, **very important**, some changes for the bridge (and in the future other embeddeds) like `orchestratorInfo` should be made with someone that understands the implications for the orchestrator operators |
|Q5 |B |30 days|
|Q6 |B |I like the idea of depositing and getting the ZNN back if the proposal is accepted, otherwise it's just like burning them, because the ZNN will be stuck in the embedded. My choice is 5/10 ZNN. The only problem I see is: with 1 ZNN, one could replicate a proposal 100 times, same name, description, etc but other data and pillars won't know what to vote. The original owner must come in the community and tell pillars what is his address so they know what to vote, meaning also pillar responsibility. The idea with only a pillar creating it could be good, as it decreases the chance of a malicious actor and everyone that creates a project here must should some people from the community, should create a forum post, ask for opinions, no one will just come and post a github link and create the proposal.
|Q7 |ABC | I would exclude them from all voting in the future if they don't produce for a long period of time. The only problem here is when do we start looking if the hasn't produced lately? At the moment of the count? When the proposal was created? What interval? 1 day / week / month? It is also resource intensive to look up this much I believe|
|Q8 |B | Dynamic forum in this form no, as it means that proposals with no interest from the pillars have a high chance of being accepted after a few months. I agree that we need some kind of mechanism for black swans and for now we do, the spork address or hard fork.|

-------------------------

0x3639 | 2024-11-14 17:45:18 UTC | #26

[quote="aliencoder, post:22, topic:544"]
The only production embedded contracts were designed, developed and deployed by @sumamu & co team.
[/quote]

I think we also have the HTLC and PTLC embedded contracts.  The HTLC code was tested for many months (maybe a year) and was adopted into `go-zenon`.  The PTLC contract has been out there for more than a year and I think some devs have been reviewing it and testing it for a long time.  

I'm in full support of a governance module.  I just want to make sure we have enough testing and review before it gets adopted.

-------------------------

edgepillar | 2024-11-15 04:49:47 UTC | #27

[quote="0x3639, post:26, topic:544, full:true"]
I'm in full support of a governance module.  I just want to make sure we have enough testing and review before it gets adopted.
[/quote]

+1

-------------------------

georgezgeorgez | 2024-11-16 00:02:18 UTC | #28

Thank you, I value your input.

-------------------------

georgezgeorgez | 2024-11-16 00:20:51 UTC | #29

No matter what we talk about, things need to pass governance and AZ.
The Hyperqube incubator and forum category is restricted to the pillars to get a good sense of what is passable.
If it was easy to have one thread, but filter out non-pillars when it came to voting, I would do it.

The process is not meant to be exclusive for the sake of being exclusive.
Rather it is meant to be indicative.

-------------------------

Stark | 2024-11-20 18:28:05 UTC | #30

@sumoshi21 ,

Can you let sumamu know that his engagement is requested, please? His opinion as well as technical insights will be valued, as well as yours.

https://forum.zenon.org/t/serious-about-adding-znn-markets/1964/14

Regards,
Stark

-------------------------

vilkris | 2024-12-05 09:43:26 UTC | #31

Since the advent of NoM it has been discussed many times that protocol changes should be accompanied by a ZIP. Is there a ZIP in the works?

Regarding the [proposed implementation](https://github.com/zenon-network/go-zenon/pull/47), it more or less adheres to this: https://forum.hypercore.one/t/universal-governance-module-proposal/544/25

Personally I'd want some changes to the implementation but it's not just up to me.

I don't want to be too idealistic in terms of reaching a supermajority consensus off-chain regarding a specification but we should at least give pillars the chance to voice their opinion on the specification.

One way to do this could be to ask pillars a set of questions about the specification similar to how the hyperqube spec voting is being carried out: https://forum.hypercore.one/t/wp1-governance-spec-feature-vote/554/1

And ask pillars to include a signature in their reply. Of course not all pillars will reply but at least it would give developers a lot more confidence in what to implement and approve into the codebase.

The community can help spread the word so that pillars will hopefully respond in a timely manner. A pillar can also say that they are indifferent to the details of the specification delegating the responsibility to the pillars that do have an opinion.

The only developers who have approval rights into the go-zenon codebase right now are: 0x3639, George, MoonBaZZe and sumamu.

Other questions:

How are others supposed to test the implementation?

What is the course of action if MrK doesn't create a spork? How long do we wait for him?

-------------------------

vilkris | 2024-12-05 11:15:33 UTC | #32

I want to clarify that I believe there's two parts to reaching consensus for a protocol change:

The first one is pillars voting on the details of the change. I expect that only a smaller subset of pillars have interest in participating in this vote and that's fine.

The second one is pillars voting on accepting the proposed changes that are based on the first vote. This part should require a supermajority.

-------------------------

sumoshi21 | 2024-12-05 18:28:00 UTC | #33

Make Governance Great Again

I've come up with a way to prove the supermajority of Pillars support the integration of the Governance module.

Basically I will keep creating phases until more than 66% of Pillars (distinct Pillars) have voted on the Project and its Phases.

This is a simple and straightforward way to gather distinct votes using AZ proposals without using any off-chain mechanisms.

-------------------------

georgezgeorgez | 2024-12-06 00:20:46 UTC | #34

I have voted NO on the phase for now because there is no ZIP.

Edit: To elaborate further, an implementation neutral spec (ie a ZIP) and pillar supermajority consensus are a subset of my maintainer criteria for go-zenon which I have published here: https://zenon.wiki/index.php/User:George

-------------------------

0x3639 | 2024-12-06 02:43:09 UTC | #35

I support the idea of a governance module, but with testing, review, and meeting the criteria of the `go-zenon` maintainers.  I also think any changes to `go-zenon` should require a ZIP.

I don't understand what we are voting on TBH.  The AZ passed.  The next phase is to get adoption.  The Pillars cannot merge the code, and we don't want that.

So are we asking the Pillars to "force" the maintainers to accept the code without review and testing?  Or are we asking Pillars to approve the AZ again, but with more votes this time?

-------------------------

tapwoot | 2024-12-06 05:07:50 UTC | #36

Hi all, seems like if i vote yes then I'm a sheep and if I vote no then I'm against making Zenon Governance great again

-------------------------

coinselor | 2024-12-09 20:29:55 UTC | #37

What if you vote Absent? Asking for a friend.

-------------------------

