Thread: code-consensus
sol | 2023-07-09 19:33:13 UTC | #1

I'll briefly summarize the topic and request everyone to express their opinions.

Mr Kaine is the sole maintainer of the [de-facto](https://github.com/zenon-network) Zenon codebase, yet he ignores ([1](https://github.com/zenon-network/go-zenon/pulls), [2](https://github.com/zenon-network/znn_sdk_dart/pulls), [3](https://github.com/zenon-network/syrius/pulls)) our pull requests or silently accepts them without any comment.  
His review process is opaque, his inactivity has stalled this project on several occasions, and the need for his involvement is questionable. 

George has summarized most of the concerns in these posts: [1](https://www.zenonzealot.xyz/9/), [2](https://www.zenonzealot.xyz/10/)

I propose that we, the active developers of the Zenon project, reach a consensus about how "official" code should be maintained, reviewed, tested, and distributed. Feel free to suggest solutions in this thread.

HyperCore One was formed to handle these objectives, but Mr Kaine continues to undermine our efforts.

I believe it would be in our best interest, as a community, to proceed without Mr Kaine's explicit involvement.

-------------------------

0x3639 | 2023-07-10 10:15:21 UTC | #2

I was recently watching this long podcast with Jack Dorsey.  Some of the things he talks about are relevant to our discussion here.  

Dorsey: if you don't like the architecture of the public square, change it.  He also talks about how Satoshi started bitcoin and turned it over and vanished.  And how elegant that was.  I don't recommend listening to this unless you have 3 hours to burn in a car or plane.    

Here are my general thoughts.  I think Kaine is far more active than we know or think. Kaine's inaction in /zenon-network is on purpose.  It must be hard for him to see code sitting there that needs to be reviewed and merged.  And yet he lets it sit there.  I do not think he is lazy or does not care.  He is doing this on purpose.  He wants the community to take over.  He wants the /zenon-network repo to go away.  He wants us to fork him out and/or take over spork production.  He wants to vanish. 

And once we deliver Phase 1 my bet is he is gone forever.  We all know it's going to happen.  It's just a question of when. So the sooner we move in this direction the better.  However, I don't want to do anything stupid or too quickly that puts the network at risk.

In summary, I am for an orderly transition away from Mr. Kaine and the /zenon-network repo.  I think this must be 100% complete by the time we deliver Phase 1 but hopefully before that.  I think we can start building trust with the community by asking the community to use our repos for critical infrastructure.

Pillars are trusting the HCT repo for the Orchestrator.  HC1 can offer the znn_controller_dart software to upgrade go-zenon to v0.0.6 by fixing big int support.  I'm going out for a walk.  I'll post more later.    

https://www.youtube.com/watch?v=Nzvh4AODtWc

-------------------------

CryptoFish | 2023-07-10 07:37:07 UTC | #3

I don't know what Mr. Khaine thinks and if there's no clear communication about it, it doesn't matter.

It is important that we can move forward as a community. The government module is a crucial part of it. The umbilical cord can be cut with this.

As for the repositories, I think it's a lot simpler. If we agree today that repo X is leading, we'll make it leading. No one is stopping us, especially if it means we can move forward faster.

For this we can create a new organization e.g. Zenon-Community where all crucial repos will be stored and Team organizations fork from there. Actually the same as we now only work under our own management. If Zenon-Network wants, it can always synchronize to stay up to date with the community.

-------------------------

0x3639 | 2023-07-10 12:41:54 UTC | #4

This is the /zenon-network repo.  When I look at this all I can think about is the SEC trying to make a case that the community is relying on a central entity.  That will be an impossible case to make with this level of activity.   

![Screenshot 2023-07-10 at 7.32.06 AM|690x178](upload://eaDANNvttHGcPPLagaq0GoSpvpu.png)

When I look at this it makes me think we are (1) winning, and (2) we need to take over.  It's a very clear message to us.  So let's do it.  

Should we focus on HC1 and HCT repos...  Or should they roll up to a zenon-community repo?  Early on when we debated the ZIP process we tried to avoid centralizing the repos into one gate keeper.  We envisioned having many repos that the community started to trust over time.  That way one "entity" or group of devs cannot gate keep one repo.  Sounds like Bitcoin is starting to think in this direction too.  @georgezgeorgez found some nice articles about it at the time.  

My preference is to release code from HC1, HCT, and maybe even some individual repos that people trust over time.  I guess the question then becomes, how do we do code review / audits?

-------------------------

digitalSloth | 2023-07-10 19:27:54 UTC | #5

I agree it is crucial for the community to move forward without waiting for Mr. Kaine to approve code, as already stated he is slow at approving and bad a communicating so if this is holding back progress its time to move on. 

HC1 and HCT have both delivered code that the community is running so there is already a level of trust built and with the governance module the pillars will have final say as to what gets approved via a spork. 

While I agree its good to avoid centralised control over the repos I also think from an onboarding point of view its more confusing if you have code located in different repos as you have to remember X manages XX repo , while Y manages YY repo etc.. so to me having a zenon-community org makes sense. But like 0x says then the issue of code reviews/audits comes into play. Maybe community org could host "core" repos like go-zenon, orchestrator, syrius, etc and fork others like SDKs etc with the emphasis on the original devs to maintain the forks and submit PRs back to community org. Not sure if this is feasible just thinking aloud.

-------------------------

sumamu | 2023-07-11 13:43:22 UTC | #6

[quote="0x3639, post:2, topic:153"]
I’m going out for a walk. I’ll post more later.
[/quote]

I like the way you so suddenly ended the post.

-------------------------

sumamu | 2023-07-11 14:10:49 UTC | #7

So our options are:
- separate githubs for all teams
- all teams join under the same github organization and transfer repos to it
- keep creating PRs for the official repos

What if we proposed to Mr Kaine to give us, the contributors, maintainer roles? And maybe even convert the account to an organization and transfer ownership of it to one of the more trusted community members?

-------------------------

sumamu | 2023-07-14 15:51:56 UTC | #8

Where are we on this? Has anyone proposed to Mr Kaine to give the devs maintainer roles?

-------------------------

sol | 2023-07-14 23:54:46 UTC | #9

[Everything belongs to the community. Patience.](https://t.me/zenonnetwork/302298)

-------------------------

CryptoFish | 2023-07-15 09:03:10 UTC | #10

The way he just disappear in the middle of a conversation. And, he's gone...

-------------------------

sol | 2023-07-17 15:53:07 UTC | #11

It's obvious to me that Mr Kaine doesn't want to maintain the zenon-network Github account.
Why are we still submitting PRs there?

-------------------------

0x3639 | 2023-07-17 18:37:01 UTC | #12

Because we have not agreed on a different process?

-------------------------

sumamu | 2023-07-17 18:56:57 UTC | #13

I vote for converting the zenon-network github to an organization and giving all (or at least some) of the contributors maintainer roles and maybe even appointing a trusted member of the community as owner of the organization somewhere down the road.

This will give the contributors more flexibility and it will certainly increase github activity.

But for this to happen it has to be supported by a majority of the community devs. We must prove that we can coordinate.

-------------------------

sol | 2023-07-17 18:58:31 UTC | #14

Mr Kaine has not indicated that he would respect the result of such a vote. I don't particularly care to have access to that account.

I vote in favor as well, albeit only for the sake of progress.
Fully aware this can lead to a power stuggle in the future.

I would prefer we abandon that account entirely.

-------------------------

aliencoder | 2023-07-17 21:25:25 UTC | #15

[quote="sol, post:9, topic:153"]
Everything belongs to the community. Patience.
[/quote]

[quote="sol, post:11, topic:153"]
It’s obvious to me that Mr Kaine doesn’t want to maintain the zenon-network Github account
[/quote]

I guess we'll get the answer until the end of this month.

-------------------------

sol | 2023-07-18 21:37:08 UTC | #16

Mr Kaine visited us on Telegram today and wrote the following:

[Let's finish the community review for the PTLC embedded: if a majority of devs approve it, it will get merged. Same principle will apply for the rest of the changes: BigInt, p2p fix, etc. Once everything is merged, every dev that contributed will get a maintainer role.](https://t.me/zenonnetwork/303966)

-----------

Seems like this thread is no longer required, though we should probably still come to an agreement re: code review and testing practices. 

Should I start a new thread?

-------------------------

0x3639 | 2023-07-19 14:41:17 UTC | #17

[quote="sol, post:16, topic:153"]
Should I start a new thread?
[/quote]

Please do.

-------------------------

