Thread: what-are-the-communities-priorities-for-accelerator-z-and-hyperspace
romeo | 2024-03-27 15:20:21 UTC | #1

Byzentined made a good point earlier on the Telegram about mapping out a high level roadmap and budget  for what we would like built on the NoM as a priority - and what value we would assign such tasks. Let's start a discussion here about tasks and estimated payments.

Some ideas: 

- CEX/DEX listings, bridges to specific Crypto chains for hyperspace.
- Key SDKs, Syrius enhancements (skins, lightweight mode, interface improvements), NFTs, BTC interop for A-Z

-------------------------

vibe.znn | 2022-04-23 12:28:08 UTC | #2

Bridges to other chains and atomic swaps (or any other kind) with BTC seems the most important if you omit VM functionality. 

So VM/wasm otherwise above. 

I think SDKs are a must also but nowhere near as useful as smart contracts at this point. Good SDKs allow easier implementation for exchanges tho and interaction with the chain.

-------------------------

Byzentined | 2022-04-23 12:51:03 UTC | #3

As we go I hope this conversation begins to build out a pie chart of how the A-Z pool gets allocated. This can also tie into other conversations (like the Fiverr meets Github idea)

What are the various areas of the NoM that need to be built out?

Bridges
BTC interop
Wallets
Exchanges / ways to trade
NFT platform
ZTS platform
Central info resources / wiki / gitBook
Competitions and incentives
Marketing
Graphic Design and Brand

Maybe list everything we can possibly think of and then do a Phase One poll were we vote on what is most important?

-------------------------

Jeron | 2022-04-23 20:38:57 UTC | #4

I fully agree with this. Adding smart contracts will unlock so much functionality. It seems like it should be the highest priority.

We should clarify with Mr Kaine if 'zApps' on the roadmap means the team is going to do this, or whether it should be done under AZ/hyperspace. He has said AZ/hyperspace in chat before.

I'm still not clear whether the core dev team are going to be submitting proposals via AZ/hyper or are continuing to work on the network design separately.

I'm not sure if there is anyone in the community capable of implementing the VM for SCs.

-------------------------

Byzentined | 2022-04-23 21:18:15 UTC | #5

Good point - it’s fundamental. Previous mentions by the team was Smart contracts for NoM 1, but that may have shifted with AZ. We do need need clarity on who’s lifting what.

The AZ webpage shares some things…

Under Zenon Fabric
Governance, Blockchain based AI, IoT solutions, DEX, Defi, VM integrations, NFT Platforms, Mobile Apps, GameFi, DeSo, Decentralised storage, AMM.

Under HyperSpace
SDK ports, Multi-chain integrations, Interoperability solutions, Cross-Chain bridges, Atomic Swaps.

But a lot of this cannot occur until we have full Smart Contract abilities.

-------------------------

Dumeril | 2022-04-24 07:33:33 UTC | #6

I think getting transparency on role of the team and the features they are planning to implement is the most important issue we have, when we think about future directions. 
VM and non-embedded smart contracts. I wouldn’t be able to sit down right now and start implementing those. But I’m confident that I’d be able to figure it out. But then there’s things that I’m able to do right now, so why would I spend time to understand and work on stuff that’s (a) potentially being developed already and (b) already thought through and understood by others, that also should have the proper infrastructure in place to test and validate core changes. 
That’s just sane behavior I guess. 
So until the team steps up makes a commitment in either direction we’re probably locked in a vacuum. It wouldn’t even make sense to ask go/blockchain/wasm experts if they want to earn az funds in that situation.

-------------------------

Jeron | 2022-04-24 07:49:18 UTC | #7

Very true. I've pinged MK on this matter a couple of times already but am not getting any response. 

Now that AZ is out, we should have the AMA soon and pose this as a question with a more detailed rationale along the lines of your post. 

I've been busy with a few things lately but might give the questions a final review and see if we can set something up soon.

-------------------------

zyler9985 | 2022-04-24 09:46:47 UTC | #8

Apart from estimated costs, we could also try to ascertain the the order of things generally.
For example, listing on a tier 1 CEX is de facto marketing because of the exposure, visibility and perceived legitimacy, so what do we want those people to see when they check us out? What is the minimum a prospective builder/retail would like to see when they come across us via a new exchange listing?

-------------------------

7nzalh | 2022-04-24 10:37:19 UTC | #9

Short term wise and before we dive into NoM's "mega-projects", I think we should give some attention to the little bugs in Syrius. Many of the users are reporting several issues that seem to be reoccurring. Syrius is the gate and entry point to the NoM and I think it should provide an ideal experience for the participants. Next inline I think should be smart contracts > VM/Wasm > bridges/atomic swaps > SDKs. Goes without saying that BTC interop is on the top of the list but I'm still not quite sure how it's envisioned.

-------------------------

Dumeril | 2022-04-24 13:05:54 UTC | #10

I want to push sentinels to the front of that list. We’re always talking about smart contracts and such, but sentinels already exist as a placeholder and from the initial architecture description they seem to play a vital role. Maybe they are even necessary for sc execution.

-------------------------

Byzentined | 2022-04-24 15:38:41 UTC | #11

Do we have an idea of the SDK's which we should build, and which have been built? If I understand this, it is something which can be done now and can be allocated for.

If we create the broad outlines of the Zenosphere then we will know what parts of the picture to colour in - and having the outline will help others spot pieces of the picture they can colour in.

-------------------------

Byzentined | 2022-04-24 16:52:57 UTC | #12

![2022-04-24 16.25.00|690x428](upload://sFMKMsWFVCaxr0El3UaOgI1KO1k.jpeg)
 Mr Ztark made this as a quick idea of how allocation could be visualised.

-------------------------

romeo | 2022-04-25 22:16:10 UTC | #13

Noting the teams Tweet today - are we confident that we should be submitting non-hyperspace related proposals now? It seems that Hyperspace is meant to go first (cross-chain bridges etc.)

-------------------------

Dumeril | 2022-04-26 04:10:34 UTC | #14

I wondered that too. It’sa bit weird that they make this artificial separation but no way to enforce it. If people can submit anything and pillars can vote on it, it will happen and why not

-------------------------

Jeron | 2022-04-26 07:41:17 UTC | #15

Yes I'm not clear on how the funds would be depleted from the orbital address for hyperspace.

I think the AZ funds are distributed by the SC from the AZ address based on the pillar votes in a trustless manner.

Maybe the team will transfer them from the Orbital fund to the AZ fund after the fact?

-------------------------

Phuong | 2022-04-26 08:30:52 UTC | #16

Totally forgot about the ama - i bet people have new questions to ask

-------------------------

Dumeril | 2022-04-26 08:44:31 UTC | #17

Are these funds actually separate?

-------------------------

Jeron | 2022-04-26 09:04:07 UTC | #18

Yes i believe the orbital funds are being accrued in a separate address to the Fabric funds (AZ and vested pillars)

-------------------------

Jeron | 2022-04-26 09:05:36 UTC | #19

If you have any further suggestions, please add them here: https://docs.google.com/document/d/1T1CmXi-qwEILRb60WaUhkzPrPe8kx3EwR3tLtlpk76s/edit

-------------------------

TrevorLeahy3 | 2022-04-26 23:19:36 UTC | #20

Not that it would be number one on the list but i think some sort of multi sig function would add a lot of value for the community. There seems so be interest in pooling funds for infrastructure and other things.

The wallet already has something to sign/verify files but i havent heard anyone use it. I see this as seperate from the implementation of runtime environment but maybe doesnt have to be.

-------------------------

TrevorLeahy3 | 2022-04-27 01:00:44 UTC | #21

After reading the medium article from georg i think we should add decentralized storage to the priority list too. It sounds like the tech is destined to solve some problems in this area so could be big for future development to have some groundwork done.

-------------------------

Byzentined | 2022-04-27 13:39:44 UTC | #22

I’m not that focussed on Zenon atm and I’m confused between 
- Orbital
- HyperSpace
- Accelerator Z

Are all of these funding mechanisms coming from 1 pool?

-------------------------

ZNNAYIID | 2022-04-27 13:46:43 UTC | #23

actually, they sent orbital funds to Accelerator Z address to fund hyperspace projects, that's why we have 900k ZNN now.

-------------------------

Jeron | 2022-04-27 21:20:27 UTC | #24

Ah I see. So there really isn't any distinction to seperate hyperspace from AZ in terms of the distribution of  funds.

-------------------------

romeo | 2022-04-27 22:35:01 UTC | #25

that's correct - but there's still the timing aspect (as in are they not wanting A-Z proposals yet?)

-------------------------

Byzentined | 2022-04-27 23:46:11 UTC | #26

So this is basically the ‘Fabric fund’ split between 
- Funding for interoperability (Hyperspace)
- Everything else the team isn’t building (Accelerator Z)

And Orbital is gone?

-------------------------

Jeron | 2022-04-28 01:10:41 UTC | #27

Correct as i understand it. However, Orbital still exists standalone and continues to accrue a share of ZNN and QSR emissions. We need interoperability to make use of the Orbital funds for liquidity provision

-------------------------

DrD3 | 2022-04-28 19:11:58 UTC | #28

correct me if I'm mistaken Jeron but I was under the impression that Orbital was accruing a share of ZNN and QSR emissions to reward liquidity providers at some point. Is this no longer the case? I'd probably extract my meagre % from there then

-------------------------

Jeron | 2022-04-28 20:31:29 UTC | #29

As I understand it, that is still happening but some of the accrued funds have been channeled into AZ. 

@ZNNAYIID is on top of the on-chain data so maybe he can confim that the Orbital funds are still being accrued seperately and that only some of them were transferred?

-------------------------

ZNNAYIID | 2022-04-29 02:08:29 UTC | #30

Yes, actually they transferred all the fund from the orbital address (129,583 ZNN and 701,250 QSR) to A Z address, but the funds are still being accrued separately as you said, 936 ZNN and  3,750 QSR are being sent to the orbital address every day, you can check it out : z1qxemdeddedxlyquydytyxxxxxxxxxxxxflaaae .

-------------------------

Phuong | 2022-04-29 10:30:20 UTC | #31

Whatever moves the price up should be near the top. Otherwise, the developer funds aren't much of an incentive compared to other L1s. Seems like a Catch-22 right now.

-------------------------

Phuong | 2022-04-29 10:36:11 UTC | #32

Substantial projects like a CEX would require a team, right? We're bleeding down to $5 and need resuscitation or good luck attracting talent. No money, no honey.

-------------------------

vibe.znn | 2022-04-30 08:35:53 UTC | #33

![Screenshot_20220430-103524_Telegram|225x500](upload://eDcXXjYqjkbV2xc1OGF4VWFlt3v.jpeg)

-------------------------

romeo | 2022-05-01 00:46:29 UTC | #34

They still haven't clarified if non hyperspace proposals are allowed now? I guess it's what the community wants in the end. For example I feel the forum proposal is valid now as it's needed for Hyperspace/A-Z discussion of proposals, but there definitely needs to be a focus on getting cross-chain and SDK proposals up and running. 
- Should we start looking external for devs to develop cross-chain solutions?
- How would we validate their work?
- What recruitment mechanisms exist for finding quality devs  now?
- Can we afford to pay for these works with ~$25k worth of znn (we would likely have to submit a proposal, sell the znn and pay the dev/entity in USD or another coin if they don't want to accept ZNN as payment) 
- Is MrK and co working on any of these themselves?
- How do we avoid double-ups
- Do we have any skilled project managers or DevOps guys that can help run such initiatives

-------------------------

ZNNAYIID | 2022-05-01 01:31:00 UTC | #35

Another question regarding hyperspace is how are they going to separate it from A Z, since both funds are in 1 address, I mean someone can come up and propose an SDK port after 100 days  and pillars can still vote for it. Even if they remove hyperspace funds back to orbital address.

-------------------------

Jeron | 2022-05-02 10:25:45 UTC | #36

I don't think they can.

The funds distribution is automatic so if pillars all vote to release the funds it just happens via the embedded SC

-------------------------

Jeron | 2022-05-02 10:28:59 UTC | #37

Given the release of funds is automated via the embedded SC, i assume people can submit proposals on whatever they want and if the pillars support it, the funds will flow.

I'm also concerned about double up with the core team. There are questions in the AMA on this. Lets see if we get answers.

I'm really hoping the core team starts submitting proposals as community members. Seems much more sustainable.

-------------------------

