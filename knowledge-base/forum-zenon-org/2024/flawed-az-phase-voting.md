Thread: flawed-az-phase-voting
sumamu | 2023-05-22 14:52:47 UTC | #1

The AZ funding process consists of 2 main subflows:

```
1. Creating a project
2. Creating a phase
```
___

> 1. Creating a project

I wouldn't change anything here since no funds are being released as a result.
___

> 2. Creating a phase

> Problem: The phase votes are counted too early, pillars don't have time for opposition.

With 86 pillars, the quorum is now 30 votes, which is calculated as the total amount of yes + no + abstain. 

For a phase to be funded, it needs to pass the following checks:

```
A. YES votes > NO votes
B. sum of YES + NO + ABSTAIN > quorum
```

This means that once a phase has 16 pillars supporting it, meaning 16 YES votes, there's no real way for others to stop it. 

If other pillars decide they don't want to fund this phase, intuitively they'd vote NO or ABSTAIN, but not enough NO votes could be casted (17 NO votes) to surpass the 16 YES votes before the quorum (31 votes) is reached.

Therefore once the pillars opposing this phase start voting NO or ABSTAIN, once they reach 15 NO votes, the quorum is reached and the phase gets funded automatically, at which point the voting stops.
___

> Solution: Count votes # days after phase is created

The best solution here is enforce a window of time before any phase can get funded regardless of the outcome, this way pillars have the change to oppose a phase by casting NO votes.

To sum it up, add condition C. to the ones above:

```
A. YES votes > NO votes
B. sum of YES + NO + ABSTAIN > quorum
C. phase created at least # days ago
```

The number of days should be enough for pillars to vote, but not so much that it would discourage spontaneity. 

For simplicity, considering that the projects have a maximum of 2 weeks before they are considered expired if they don't get enough votes, phases could get a minimum of 2 weeks before the votes are counted.

-------------------------

0x3639 | 2023-05-22 11:54:42 UTC | #2

this is a good idea.

-------------------------

ZNNAYIID | 2023-05-22 12:16:32 UTC | #3

Maybe instead of having an expiration date, we can have a 1 week window after the quorum is reached so other pillars can vote/change their votes instead of instantly paying out.

-------------------------

sumamu | 2023-05-22 12:23:54 UTC | #4

[quote="ZNNAYIID, post:3, topic:1449, full:true"]
Maybe instead of having an expiration date, we can have a 1 week window after the quorum is reached so other pillars can vote/change their votes instead of instantly paying out.
[/quote]

Projects already have an expiration date.

The issue is with phases, which don't have an expiration date and the proposed solution doesn't add an expiration date, but rather a minimum time before the votes are counted. 
___

Imagine that during a political election, the votes would be counted after each vote is casted and the same moment vote number 1 million is casted, whoever has more votes, wins.

That wouldn't work, the votes are only counted at the end of the election.
___

That's happening with phases right now, the votes are counted after each vote is casted by a pillar and once the 31st vote (quorum) is reached, the voting ends.

There should be a dedicated window for casting votes and the votes should only be counted after the voting window ends.

-------------------------

ZNNAYIID | 2023-05-22 12:24:19 UTC | #5

I was referring to the phases in my comment, having a 1-2 weeks window after the quorum is reached is better than a 2 weeks expiration date starting from the submission date, that way pillars and community will have enough time to discuss the delivered project without having a deadline. There was some projects where they had to resubmit because of the expiration date and start all over again.

-------------------------

Zashounet | 2023-05-22 12:25:00 UTC | #6

[quote="sumamu, post:4, topic:1449"]
There should be a dedicated window for casting votes and the votes should only be counted after the voting window ends.
[/quote]
Agreed. 
Also how do we prevent pillars from voting yes just because others did ?

-------------------------

sumamu | 2023-05-22 12:29:32 UTC | #7

[quote="ZNNAYIID, post:5, topic:1449, full:true"]
I was referring to the phases in my comment, having a 1-2 weeks window after the quorum is reached is better than a 2 weeks expiration date starting from the submission date, that way pillars and community will have enough time to discuss the delivered project without having a deadline. There was some projects where they had to resubmit because of the expiration date and start all over again.
[/quote]

Technically this would more complex to implement compared to the proposed solution. 

And the community would still have the chance to discuss during the 2 weeks. Pillars could also change their vote during that time.

The solution you're proposing sounds like adding another voting window after the voting ends.

That accomplishes the same: giving pillars time to oppose a phase, but with extra steps.

-------------------------

Asgardians-Pillar | 2023-05-22 12:31:49 UTC | #8

Do we have a TG channel that shows every project and phase once proposed? If not it might be a good idea to set 1 up so all the Pillar owners can subscribe and vote pretty quickly. Or an email, just need a notification really. 
I think this could really help our voting behavior be more efficient. 

I support the new model you are suggesting here 👍

-------------------------

sumamu | 2023-05-22 12:31:57 UTC | #9

[quote="Zashounet, post:6, topic:1449"]
Also how do we prevent pillars from voting yes just because others did ?
[/quote]

The only way would be a secret vote.

-------------------------

sumamu | 2023-05-22 12:33:36 UTC | #10

[quote="Asgardians-Pillar, post:8, topic:1449"]
Do we have a TG channel that shows every project and phase once proposed? If not it might be a good idea to set 1 up so all the Pillar owners can subscribe and vote pretty quickly. Or an email, just need a notification really.
[/quote]

I'm not sure. But good idea, new projects/phases should be advertised on all main communication channels: TG, Discord, Twitter, Forum.

-------------------------

ZNNAYIID | 2023-05-22 12:33:36 UTC | #11

Adding a voting window after the quorum is reached, not after the voting ends. It doesn’t accomplish the same as what you proposed, maybe I didn’t explain it well, but having a 2 weeks window to vote (not reaching the quorum during this time means they need to resubmit and pillars need to vote again) is not the same as having the current implementation where there is no voting window but once quorum is reached we start the 1-2 weeks voting window ( that way we can be sure the proposal will get through and we don’t have to resubmit because of the lack of voting from lazy pillars).

-------------------------

ZNNAYIID | 2023-05-22 12:35:48 UTC | #12

We already have an A Z tracker on both tg and discord.

Tg : https://t.me/az_tracker
Discord : https://discord.gg/dANhVxvr

-------------------------

sumamu | 2023-05-22 12:45:43 UTC | #13

[quote="ZNNAYIID, post:11, topic:1449, full:true"]
Adding a voting window after the quorum is reached, not after the voting ends. It doesn’t accomplish the same as what you proposed, maybe I didn’t explain it well, but having a 2 weeks window to vote (not reaching the quorum during this time means they need to resubmit and pillars need to vote again) is not the same as having the current implementation where there is no voting window but once quorum is reached we start the 1-2 weeks voting window ( that way we can be sure the proposal will get through and we don’t have to resubmit because of the lack of voting from lazy pillars).
[/quote]

Ok, now I'm starting to understand. 

That's the way projects work: they get 2 weeks to pass + reach quorum, otherwise the project expires and they need to submit a new one.

After the project passes, they can submit phases.

So you're saying the projects should have a minimum of 2 weeks instead of a maximum of 2 weeks?

Btw, @ZNNAYIID if you haven't done so yet, it might be a good idea to get some tZNN from the testnet faucet and see how AZ works.

-------------------------

sumamu | 2023-05-22 12:36:57 UTC | #15

[quote="ZNNAYIID, post:12, topic:1449, full:true"]
We already have an A Z tracker on both tg and discord.

Tg : [Telegram: Contact @az_tracker](https://t.me/az_tracker)
Discord : [Discord](https://discord.gg/dANhVxvr)
[/quote]

These need better exposure throughout the community.

-------------------------

Asgardians-Pillar | 2023-05-22 12:40:01 UTC | #16

Very nice must have missed that.
I think a lot of the lazy pillars could benefit from being in this channel. 😁

-------------------------

ZNNAYIID | 2023-05-22 12:49:57 UTC | #17

If we give a 1 week window after the quorum is reached it will be a minimum of 1 week, instead of having 2 weeks maximum, the reason for that again is what you said in your post, and also not making the pillars vote again if it doesn’t reach the quorum during the 2 weeks window you suggested because of 1 missing votes ( this already happened before). 
No need for that I already know how A Z currently works.

-------------------------

sumamu | 2023-05-22 12:58:25 UTC | #18

[quote="ZNNAYIID, post:17, topic:1449"]
If we give a 1 week window after the quorum is reached it will be a minimum of 1 week, instead of having 2 weeks maximum, the reason for that again is what you said in your post, and also not making the pillars vote again if it doesn’t reach the quorum during the 2 weeks window you suggested because of 1 missing votes ( this already happened before).
[/quote]

Could you rephrase it in this format, please? It would make it easier for me to understand what changes you're proposing.

```
For a phase to be funded, it needs to pass the following checks:
A. YES votes > NO votes
B. sum of YES + NO + ABSTAIN > quorum

To sum it up, add condition C. to the ones above:
C. phase created at least # days ago
```

Also, are you also proposing changes to the Project flow or just the Phase flow?

[quote="ZNNAYIID, post:17, topic:1449"]
No need for that I already know how A Z currently works.
[/quote]
Awesome!

-------------------------

ZNNAYIID | 2023-05-22 13:06:42 UTC | #19


A. YES votes > NO votes
B. sum of YES + NO + ABSTAIN > quorum
C. Phase reached quorum x days ago

-------------------------

sumamu | 2023-05-22 13:08:24 UTC | #20

Thanks, now I understand exactly what you mean. 
It does sound like a great idea. 

Let me think about what it would take to implement this.

-------------------------

mehowbrainz | 2023-05-22 14:53:00 UTC | #21

Topic moved to #development:funding-staging

-------------------------

ToKR | 2023-05-22 15:13:31 UTC | #22

Happy that this is being discussed.  My understanding is that a quorum is meant to be a minimum number of votes but since a quorum of yes votes closes the voting, a quorum can also be the max.   And the vote can close rapidly.   Voting should remain open long enough for each pillar to have a chance to vote if pillar engagement is a goal.  What would happen if a quorum of no votes is reached just before a larger group of pillars were to vote yes?  Unlikely, I know but still a possibility.  Should a pillar owner rush to get a vote in or take some time to research?  Agree with having some minimum time frame.

-------------------------

sultanofstaking | 2023-05-24 01:46:36 UTC | #23

Either idea is an improvement. What is the quickest / most natural way to get this updated and how do we collectively determine what "this" is?

I like the addition of time, but I really think we should consider raising quorum to a higher number or more logically a percentage of total pillars. 

I for one am confident the 16 yes votes needed will come with or without me. My incentive to participate is very low. We could look at the number of pillars that made the hard fork on time and use that as an anchor to raise quorum.

-------------------------

sumamu | 2023-05-24 08:44:01 UTC | #24

The main objective is to give more pillars more time to react. 
We must achieve this without slowing things down too much and with minimal changes to the AZ logic.

These are the current options:

[quote="sumamu, post:1, topic:1449"]
Current conditions for approving an AZ phase:
A. YES votes > NO votes
B. sum of YES + NO + ABSTAIN > quorum

Extra condition to be added:
C. phase created at least # days ago
[/quote]

OR

[quote="ZNNAYIID, post:19, topic:1449, full:true"]
Current conditions for approving an AZ phase:
A. YES votes > NO votes
B. sum of YES + NO + ABSTAIN > quorum

Extra condition to be added:
C. Phase reached quorum x days ago
[/quote]

-------------------------

ToKR | 2023-05-24 13:41:47 UTC | #25

I like option A.  I don't think it's important when the quorum is reached, just that pillars have had enough time to assess and vote.  10 days maybe?  But for major votes or for projects requesting large sums I think quorum size needs to be larger.  At least half of the "active" pillars?

-------------------------

0x3639 | 2023-05-24 14:22:07 UTC | #26

[quote="sumamu, post:1, topic:1449"]
C. phase created at least # days ago
[/quote]

I think I like Option A because no one will be surprised.  Pillars would know they ALWAYS have X days for a vote, regardless of how popular it is.

-------------------------

vilkris | 2023-05-24 14:12:00 UTC | #27

I like option A as well. This would be a good improvement.

-------------------------

sumamu | 2023-05-24 14:24:32 UTC | #28

[quote="0x3639, post:26, topic:1449"]
I think I like Option A because no one will be surprised. Pillars would know they ALWAYS have X days for a vote, regardless of how popular it is.
[/quote]

Both options would give pillars a minimum time to vote.

-------------------------

0x3639 | 2023-05-24 14:37:39 UTC | #29

Yes, but the total time to vote in Option B is unknown.

Option A = Time is X
Option B = Time to achieve quorum (unknown) + Y

-------------------------

sultanofstaking | 2023-05-24 19:52:35 UTC | #30

Maybe 7 or 14 days then set a weekly reminder to check makes it simple

-------------------------

sol | 2023-05-28 18:08:29 UTC | #31

I like your proposal, sumamu.

Please consider positive/negative incentives for pillar votes: https://forum2.zenon.org/t/proposal-apply-decay-multiplier-for-pillars-who-do-not-vote/504/14?u=sol_sanctum

-------------------------

