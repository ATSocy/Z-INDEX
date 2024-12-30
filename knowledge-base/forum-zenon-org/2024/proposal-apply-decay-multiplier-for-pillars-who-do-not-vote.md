Thread: proposal-apply-decay-multiplier-for-pillars-who-do-not-vote
0x3639 | 2024-03-27 15:20:05 UTC | #1

@sol recently mentioned (on TG) the idea of applying a decay multiplier for rewards paid to Pillars who do not vote on A Z proposals.  I think this is a great idea and wanted to discuss options here.  

Here are some thoughts:
- Decay multiplier gets applied after the expiration of the 14 day window to vote and no vote was cast
- Decay Multiplier should not be permanent.  Pillars should be able to earn back full rewards in the even they participate after getting “penalized”
- Decay Multiplier should persist and get larger for cumulative, non-votes.  
- Simple idea, for each no vote decay multiplier is 10% and grows with each additional missed vote.  10 missed votes makes decay multiplier 100%.  
- Once a decay multiplier is in place, a Pillar can remove it by voting on all active projects.
- Once a Pillar receives a Decay Multiplier once and then removes it, the Decay Multiplier increases by 2%.  Meaning, the next time they miss a vote the decay multiplier is set at 12%.  If they remove it and miss again, the multiplier is set at 14%.  

Thoughts?

-------------------------

cryptocheshire | 2022-05-14 09:41:28 UTC | #2

How to prevent pillars from being penalized for not voting on spam proposals?

-------------------------

0x3639 | 2022-05-14 09:55:51 UTC | #3

They just have to vote.  It does not take much time.  I’ve voted no all spam proposals and it take about 2 minutes to vote on 20 proposals.  you can see the funding address.  They are all the same and I robo click NO.

-------------------------

Ppaesch | 2022-05-14 10:21:00 UTC | #4

Reads like the mechanics of a magic card lmao.
How is it technically feasible and would it be somehow possible to redirect the missing rewards directly into the AZ fund? This way they would participate even if they don't.

-------------------------

Dumeril | 2022-05-14 10:31:02 UTC | #5

We have a parallel activity currently, that aims  to implement default hiding for proposals. The reasoning was that dealing with spam proposals is an ui issue. 
If we make voting mandatory, we engage in a conflict with this and future spammers that we cannot win.  Doing spam proposals from unique addresses is not difficult, it could even be scripted.

-------------------------

7nzalh | 2022-05-14 14:52:48 UTC | #6

Interesting idea but I think now is not the right time. I would suggest that community members first try undelegating to pillars that are not contributing and voting, observe the results and go from there. This needs to go on for a sufficient amount of time and over at least 10 or so valid proposals before evaluating the results.

-------------------------

cryptocheshire | 2022-05-14 16:48:17 UTC | #7

100% agree with @7nzalh . So far the voting quorum has been achieved for important initiatives and the economics of Zenon NoM were designed in a way so that delegators can express their support  by delegating to the pillars they like. It is up to the delegators to show first that they want to make a difference before taking drastic measures like penalizing pillars. 

The current system needs to be validated for a couple of months at least before making such fundamental changes. It was put in place this way for a reason.

Needless to say, it's an important discussion to have!

-------------------------

0x3639 | 2022-05-14 19:06:12 UTC | #8

I think part of the issue is many $ZNN holders are not actively involved, and delegate to the top 4 Pillars to generate max yields (understandable) but these top 4 pillars don’t vote.  

It’s unlikely community members will shift delegation in a significant way.  So I think we need to address this from the Pillar end.  Giving Decayed $ZNN back to the A Z Fund is a great idea.  So they are in effect helping the network.  

Voting on Spam Proposals is really not that hard.  Honestly guys it takes a few seconds.  And unless someone submits 1000 spam proposals I don’t think we need to worry about Pillars spending the time to hit NO.  We can still add a feature to hide spam. Pillars would need to hit NO and then mark as spam.  

![image|690x457](upload://eEoKIHlkhgOxNccQ5cPsOxtn1rT.jpeg)

-------------------------

TrevorLeahy3 | 2022-05-14 19:56:58 UTC | #9

Im not in favour of applying this sort of penalty to non voting pillars. As mentionned there havent been any hold ups from the pillar side so id argue were not really addressing a definitive problem. 

Id also argue that its general community participation that's holding the network back now. I include myself in this, talk is cheap.

-------------------------

0x3639 | 2022-05-15 11:54:12 UTC | #10

I guess another option would be to have a participation reward.  Not sure how to deal with rewarding Pillars for voting on spam proposals.  

By last count 37 Pillars are voting.  Less than half.  If Pillars are to become critical pieces of infrastructure in the network they need to participate IMO.  My closest experience with nodes that need to perform is THORChain (TC) and their reward mechanism can slash rewards down to zero if the node cannot perform.  

Node participation on TC are much more important than on NoM, but I feel like we need all hands on deck to push this project forward.  We want Pillars to vote and upgrade on a timely basis.  Last upgrade was a good example.  At the time of this post 4 nodes are still offline.

Maybe I’m coming from a different place.  I don’t have a legacy Pillar and had to spend a small fortune to get mine up.  So my incentives and desire to participate are different than those who earned their Pillar from easily participation.

-------------------------

Phuong | 2022-05-15 12:15:53 UTC | #11

I think a little tough love is needed. People want to build important components, but they need, what, 28 yes votes? The sooner contributors are able to get started on things beneficial to the network, the better. 

It's only for A-Z and eventually those funds will be depleted. Surely pillar operators can handle this temporary inconvenience.

-------------------------

DrD3 | 2022-05-15 13:59:18 UTC | #12

I like the idea of incentivizing pillars to participate through rewards but I'm not sure how exactly we'd implement this without the core team's assistance. 

I, however, do think that we should wait a couple more months since Accelerator Z just began. If we begin to observe that projects beneficial to our ecosystem are getting passed on due to a lack of a quorum only then do I believe we need to consider revamping the current structure.

Also, do you happen to have any resources on how TC's penalty scheme for non-participation?

-------------------------

0x3639 | 2022-05-15 16:57:33 UTC | #13

Here are the "risks" of running a node.  This is not really comparable, except from a concept standpoint.   Nodes in TC need to upgrade every week, and are required to sign transaction, keep chain state up to date constantly.  It's really a part time job.  

https://docs.thorchain.org/thornodes/overview#risk-of-running-a-node

-------------------------

sol | 2022-05-15 20:57:35 UTC | #14

Since I posted my yield decay suggestion, I've been reading the community's responses to gauge what problem we're trying to solve. Here are some more thoughts re: voting participation and incentives.

I found source material for the Zenon delegation/voting system [here](https://medium.com/@zenon.network/network-of-momentum-the-decentralized-self-evolving-superorganism-fad1de21868). There isn't much documentation for this topic.

> [Pillars] also represent the backbone of the network, having a governance role by voting community initiatives, Vested Pillars or the projects raising funds through Accelerator-Z.
>They can be seen as governors that have greatly contributed to the network and are the best to represent its delegators’ interests.

The community is meant to 'elect' thirty pillars that represent the best interests of the ecosystem. We vote with our funds and in return, the pillars enjoy greater yields.
Part of the pillars' responsibilities is to vote on community initiatives. It is their duty and as participants of the ecosystem, we have a fiduciary incentive (or obligation?) to elect those who represent us. 
If a pillar doesn't want to interact with the community, the least they can do is vote on the proposals.


[quote="0x3639, post:10, topic:504"]
I guess another option would be to have a participation reward. Not sure how to deal with rewarding Pillars for voting on spam proposals.
[/quote]

I was going to propose an alternate perspective, such as positive reinforcement.
Voting incentives can be positive or negative.
Negative: Yield **decay** increases with each missed vote
Positive: Yield **growth** increases with each cast vote
+/-: Total yield is impacted by community delegation

These are incentives to actually participate in the democratic process. Without these, we'd have a much harder time encouraging those in power to consider change.

> "...But what about the proposal spam?"

Obviously, the proposal mechanism isn't expensive to abuse. We've considered a few mitigation strategies to combat the spam but I may have a solution.
Similar to voting incentives, there are spam disincentives.

A negative disincentive could be burning the 1ZNN cost to submit a proposal. This applies a negative consequence on all who participate in the proposal submission process, also hurting those who are genuinely trying to help the project.
A positive disincentive could be locking the 1ZNN fee until it is deemed a valid/official proposal. 
Rewarding those who do well is positive reinforcement.

> "...But what's a valid/official proposal?"

Proposals must reach a floor of positive votes before they can be deemed official. Once they've achieved this status, they are subject to voting incentive strategies. Only official proposals are visible to all pillars in the Syrius wallet; the unofficial ones can be seen if a setting is toggled in the wallet.
Unofficial proposals must garner enough support via social mechanisms in order to achieve the floor required to become official.

We don't want to waste anyone's time with trying to decipher a legitimate proposal from spam. Spam in the future could appear more sophisticated, similar to phishing techniques. 

If there is something we can do to simplify the voting process and lower the time/mental burden on pillars, I think we should try.

-------------------------

Dumeril | 2022-05-15 21:11:40 UTC | #15

[quote="sol, post:14, topic:504"]
Proposals must reach a floor of positive votes before they can be deemed official. […]
[/quote]

I like that approach and it’s similar to what we discussed already, mainly in telegram. This is a solution that can be implemented in the ui, no protocol changes required. It also allows everyone to still get a list of all proposals via other clients.

-------------------------

romeo | 2022-05-15 22:04:40 UTC | #16

don't forget it's not just 28 votes for proposal quorum - there is also then a vote required for every phase the proposal submits (phase voting requires a little more effort as the pillar owner has to click into the project). If we want proper milestone based management of proposals (i.e. you get paid after you do the work) then we need the Pillars involved in the phase voting daily as well

-------------------------

dat_she_pepe | 2023-05-28 18:18:31 UTC | #17

I like the idea of positive incentives.

-------------------------

