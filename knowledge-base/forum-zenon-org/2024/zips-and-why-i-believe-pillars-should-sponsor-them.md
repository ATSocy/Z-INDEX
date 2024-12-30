Thread: zips-and-why-i-believe-pillars-should-sponsor-them
0x3639 | 2024-03-27 15:20:12 UTC | #1

**Background:**  ZIPs are Zenon Improvement Proposals.  They are a document for introducing features or information to the NoM. The ZIP framework should become the standard way of formally communicating ideas about potential Zenon improvements.

Most projects maintain some central repository for improvement proposals.  Editors review proposals based on established standards and publish those proposals after community engagement and debate. After an improvement proposal is published, developers can chose to write code to implement the proposal.  And node operators are expected to upgrade.  

**NoM Zips:** I believe that NoM should take a different approach to ZIPs. To understand why, let's review how NoM sporks (upgrades) happen.  But first, what is a spork?  A spork is a mechanism used to safely deploy new features to the network through network-level variables to avoid the risk of unintended network forking during upgrades.

Today, Mr. Kaine holds the only address that is hard coded to accept sporks.  Meaning, only the core team can activate a network upgrade. For example, the AZ framework was enabled by Pillars upgrading their node software and the core developers activating it.  But in the future, that will change.  The Pillar community will remove the hard coded address and enable on-chain Pillar voting to activate a spork.

Why create a ZIP framework that vests any control in central editors or the core team if that will need to change in the near future?  Pillars will be responsible for upgrading and activating sporks.  And it's possible that delegators will come into play in sporks too.  What if the threshold to activate a spork required 2/3 of Pillar vote by delegator weight?

Active Pillars will need to work with the community to hear, debate, and publish ZIPs they support.  And once they support a ZIP, Pillars and the community will need to spread the word to garner additional network support.  

In my opinion, if Pillars are responsible for upgrading the network, they should be responsible for managing ZIPs.  We just need a few Pillars to engage in the process.  Some might even delegate the responsibility to engaged community members.  deeZNNutz.com is willing to participate.  And I know others will too.  

**Potential ZIP Process:**

Community Proposes ZIP in a public channel > Community debates and revises > Community finds a Pillar to sponsor the ZIP > Pillar publishes ZIP in repo > Pillar and community gets support of other Pillars > Pillars vote on ZIP with some on or off chain tool that "settles" results to the blockchain > If approved by some TDB metric official support is signaled > community then knows Pillars support the ZIP and can spend time to implement it > if code is necessary, the community creates code and audits > Pillars upgrade their node software > Pillars then vote to enable to spork based on TBD metric > if approved upgrade goes live

Pillars that do not upgrade after a spork will get forked away into a second chain.  They can either run the second, smaller chain, or upgrade.  

Note:  I think we should try a spork ourselves.  Some people have made changes to Syrius.  Someone added a message field I believe.  We can run through the ZIP process, upgrade our node software, and ask the devs to enable it.  We need to accept the fact the core devs are not going to be here forever.  I think they are withholding  LP rewards as a message to us.  GET THE ZIP FRAMEWORK DONE.  They released one day of rewards and then stopped, so as to say, we are still here dumb asses.  Do you job and we will release LP rewards.  

I tried to synthesize these thoughts from George's post on Github and me asking lots of questions about how this stuff works.  I hope I have not made a super stupid mistake in all this.  If so, I'm learning so please excuse me.  

Thoughts?

-------------------------

georgezgeorgez | 2022-08-30 13:16:21 UTC | #2

At some point, I would like to work with a Pillar to go over the htlc work I’ve been doing and properly define it as a zip.

-------------------------

0x3639 | 2022-08-30 13:22:15 UTC | #3

I would do that.  I've run and tested the code, so this is something I would like to participate in for sure.

-------------------------

coinselor | 2022-08-30 16:58:22 UTC | #4

Most of it sounds reasonable to me, except afaik updating the s y r i u s codebase will only require core team to merge a PR in the official syrius codebase. Like you explained, sporks are intended for protocol upgrades so we would need a different community led spork example. 

Ideally we would add something meaningful like an embedded contract required for HLTC, TSS implementations, etc but if we can find something simpler like what george mentioned about defining network constants for easy on-chain upgrade later on could also work as a test run.

It can also set the tone for Phase 1 'tokenomics' discussion as we would have some set variables we would need to agree on and set as a community.

-------------------------

0x3639 | 2022-08-30 19:34:57 UTC | #5

Feel free to continue the discussion on Github too.  George made a relevant post over there regarding the topic. https://github.com/orgs/Big-Inches-Club-House/discussions/4#discussioncomment-3511501

-------------------------

Phuong | 2022-08-31 03:15:23 UTC | #6

I don't know if every detail you have here is right or not, but there's no doubt that it's directionally correct at a minimum. Thank you for putting your time and thought into this.

-------------------------

cryptocheshire | 2022-08-31 18:37:53 UTC | #7

I have a question: For the AZ spork the key requirement for a successful lock-in was a supermajority of public nodes running v0.0.4

The above ideas revolve exclusively around Pillars being the determining factor for a spork activation. With NoM phase 1 we will have Sentinels who each will act as public nodes. 

Therefore, shouldn't a ZIP framework specify that the support for a protocol upgrade requires approval by a supermajority of public nodes (rather than just pillars)?

While I agree the Pillar sponsorship is a good way to get public endorsement by a validating network participant, I believe that if the quorum threshold is based on public nodes in general, Pillars might never be able to achieve supermajority since there will be many more Sentinels in the network.

Unless this depends on the type of the upgrade? Are there different types apart from sporks for which it would make sense to just require Pillar support?

-------------------------

georgezgeorgez | 2022-08-31 19:23:09 UTC | #8

That’s a great point.

So there’s two concepts I mention in my original post on GitHub.

Acceptance
Activation 

Acceptance is really just having the confidence to force the issue. People are committed to activation, start planning for it, accept that people who don’t follow will be forked out etc.

We need to do some research on what soft forks vs hard forks looks like on our network.

The network cannot run without infra but the network is worthless without users. So it’s a symbiotic relationship. Besides price, delegation helps drive the pillar user alignment.

For acceptance, getting the feedback of all network participants is critical. Another reason why AZ isn’t a good polling mechanism. 
We’ll want mechanisms where anyone can vote and we can see it weighted by capital. 

That being said, only pillars have done the burn, while the others are free to leave the network without guaranteed loss. Other participants don’t have the same skin in the game.

Activation is the process of actually making the change. If it’s a protocol change, anyone who doesn’t make the change simultaneously will get forked out. 

So this can be set to some predetermined height or on-chain signal. Eg in bitcoin 90% of recent mined blocks are in support, everyone in support activates
For us, we have the spork objects.

We can make spork object creation depend on on-chain votes. That might actually be the first protocol change we have to do…

Whether to include sentinels voting is a debate to be had.
Personally I think it would be okay just to consider sentinels and other participants for acceptance, and rely on pillars for activation

-------------------------

ZNNAYIID | 2022-08-31 20:13:59 UTC | #9

[quote="georgezgeorgez, post:8, topic:984"]
only pillars have done the burn, while the others are free to leave the network without guaranteed loss. Other participants don’t have the same skin in the game.
[/quote]

[quote="georgezgeorgez, post:8, topic:984"]
Personally I think it would be okay just to consider sentinels and other participants for acceptance, and rely on pillars for activation
[/quote]

100% agree on this.

-------------------------

romeo | 2022-09-05 01:05:16 UTC | #10

Adding some thoughts here:

> "Why create a ZIP framework that vests any control in central editors or the core team if that will need to change in the near future? Pillars will be responsible for upgrading and activating sporks"

Because we have limited buy in from Pillars currently, we've only validated 6 on the forum, and know the identity of maybe 10 others. Reliance on Pillar operators is no different to that of a Editor/s - other than skin in the game

> "We just need a few Pillars to engage in the process. Some might even delegate the responsibility to engaged community members"

What's the point of a decentralized repo if only a few Pillars participate in the hosting? I would argue it needs a strong footprint to be beneficial, otherwise just use GitHub and save the hassle initially

> "Community Proposes ZIP in a public channel > Community debates and revises > Community finds a Pillar to sponsor the ZIP > Pillar publishes ZIP in repo > Pillar and community gets support of other Pillars > Pillars vote on ZIP with some on or off chain tool that “settles” results to the blockchain > If approved by some TDB metric official support is signaled > community then knows Pillars support the ZIP and can spend time to implement it > if code is necessary, the community creates code and audits > Pillars upgrade their node software > Pillars then vote to enable to spork based on TBD metric > if approved upgrade goes live"

This flow is too convoluted imo, too many steps that require human intervention and input which goes against the decentralized goal. I do like the Pillar support aspect, but do not think its neccesary for an initial ZIP implementation.

A more streamlined process of "proposal>identify sponsor>on-chain vote>ZIP submission and code review>implementation" simplifies matters significantly.

> "with some on or off chain tool that “settles” results to the blockchain"

why an off chain tool when we have an on-chain voting protocol already? Who runs the tool? Who ensures the vote is fair and accurate? who supports it?

Are we confident removing the embedded upgrade contract doesn't have any other impact? Is it appropriate to be threatening with a fork to remove the currently available method to upgrade the protocol?

The framework I drafted aimed to avoid these unknowns and limit risk exposure by not pushing any significant change early on - with a view to grow and evolve as we A) Learn more about the network and B) See what the next protocol upgrade includes. I feel the approach you're taking whilst introducing benefits and improvements also adds unnecessary risk and time delay

-------------------------

0x3639 | 2022-09-05 01:53:24 UTC | #11

thank you for that feedback.  Let me sleep on it and respond.  You make some good points.  I want to consider them carefully.

-------------------------

coinselor | 2022-09-05 02:46:06 UTC | #12

[quote="0x3639, post:1, topic:984"]
Community Proposes ZIP in a public channel > Community debates and revises > Community finds a Pillar to sponsor the ZIP > Pillar publishes ZIP in repo > Pillar and community gets support of other Pillars > Pillars vote on ZIP with some on or off chain tool that “settles” results to the blockchain > If approved by some TDB metric official support is signaled > community then knows Pillars support the ZIP and can spend time to implement it > if code is necessary, the community creates code and audits > Pillars upgrade their node software > Pillars then vote to enable to spork based on TBD metric > if approved upgrade goes live
[/quote]

I kinda agree with Romeo this can be simplified. Here are my thoughts. I don't think the people that worked on the Taproot implementation of Bitcoin waited for the consensus of miners to fully flesh out the code/implementation of it. Rather, they worked on a Taproot implementation because they truly believed in the benefits it will bring to the Bitcoin network, and that the consensus from the miners will come eventually. I like this approach for NoM, as george said, it's an opt-in network.

Random thought... can you create an AZ proposal from a Pillar address? It would be nice for that to be the official way for a pillar to sponsor a ZIP, while also getting the initial signal of support from other pilars. Two birds, one stone. We could even tweak syrius/zenon.tools ui's to show them as different and even be able to filter them.

"When miners “signal” support for any Bitcoin protocol update, they are essentially saying that they are prepared to run a certain version of the Bitcoin node software which implements the updated code. In the case of Taproot, we signaled our support by putting a “4” at the end of the version bits (0x2f900004) in the block that we mined."

Would you say a simple AZ 'yes' vote from a pillar would suffice to signal support for a protocol upgrade? Seems like a good alternative since we can see exactly who voted yes/no or abstained. However, mined blocks seem to be like a more real-time metric of support.

-------------------------

cryptocheshire | 2022-09-05 05:03:46 UTC | #13

Acceptance signaling is probably optional anyway. Its goal is to gauge community support for a proposed change, but it's not required by a ZIP initiator to build and release an implementation Pillars / node operators can activate.

-------------------------

0x3639 | 2022-09-05 11:39:40 UTC | #14

I think we are seeing the longest running crypto project with a central editor system rethink how they manage the repo.  Read this article George shared.

https://protos.com/bitcoins-longest-serving-lead-maintainer-calls-it-quits-names-no-successor/

We know the core devs will not engage.  We are seeing the BTC central editor system unravel and their own devs are questioning the structure.  I believe we should take note of these signals when designing our system.  Who from the community would even take on the roll of central editor?  And why would they do it?

I assume a few Pillars will engage in the proposed process initially.  If we are successful in growing the network, and the cost of Pillars goes up, the new entrants will engage.  I've seen this in THORChain.  Even if we have 2 to 5 Pillars willing to use the process initially, I believe that is better than 1 central editor.  

I agree the process is messy.  And @coinselor pointed that out too.  I think the initial vote is optional and only a signal.  We will highlight that in the draft.  It can be bypassed for sure, but for someone who is debating spending time on writing code, it's a good signal the community supports the initiative.  

Not sure about the off/on chain tool.  I think we need a way to vote.  We can sign messages, embed in Syrius, or some other way.  

Regarding the spork object for activating code, I think we need to be ready for the training wheels to come off.  The core team will not be around for ever.  I believe they will disband and become community members with no control to activate sporks.  I'm very confident that will happen.  Just not sure when.  I absolutely do not think we should threaten that.  We are not ready.  But I do think that day is coming in a year or two.  

They are asking the community to develop the ZIP framework with no input from the core team.  This is an important piece of the network and we are designing it.  Seems crazy TBH.  I'm a real estate developer, not a blockchain expert!!!  WTF do I know.  The point is, if they want us to design the ZIP upgrade process they will hand over the keys to spork the network.

-------------------------

romeo | 2022-09-05 12:39:34 UTC | #15

[quote="0x3639, post:14, topic:984"]
I think we are seeing the longest running crypto project with a central editor system rethink how they manage the repo. Read this article George shared.
[/quote]

I spoke with the current Bitcoin BIP editors when I wrote the framework, they didn't raise any issues or concerns over the use or role of an editor in their process for what it's worth - see https://github.com/bitcoin/bips/wiki/BIP-Process-wishlist for their current issues list. That's not to say it's ideal having an editor (I'd like to see no manual or human involvement in the progression of the process at all if possible) but again to get the ball rolling early and quickly I think it's necessary

-------------------------

