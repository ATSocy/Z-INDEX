Thread: changing-the-minimum-amount-of-orchestrators-new-ceremony
dat_she_pepe | 2024-03-27 15:19:59 UTC | #1

As it is now, we clearly see that the bridge can't recover from a technical problem. Either orchestrators don't care or they don't have the technical capabilities to catch up.

We should discuss a new ceremony and a new way to calculate the minimum orchestrators needed to run the bridge. Something that's not a strict % could work if a similar situation happens again. 

Let's say we have 70 orchestrators then the minimum for the bridge to run could be 10. It's a lower percents than what's needed now and yet a higher amount of nodes. 

Anyway this gap between the needs for the bridge to be up and running and the seriousness and / or technical skills of the orchestrators should be addressed. Right now it just doesn't work. Good we could benchmark it when there's no real pressure to transact, capital wise.

-------------------------

0x3639 | 2023-08-18 20:54:15 UTC | #2

I think many orchestrators are proactively deciding NOT to turn their equipment back on.  The TSS Zero Day needs to be fixed.

I've very carefully looked at all the orchestrators, one by one.  And I've talked to many.  Here is why the bridge is down:

1)  Operators can be online, but they elect to be off because of the TSS Zero Day.
2)  One Operator has an issue with an IP address changing and can no longer join the pool.  However, his Orchestrator is online, it just cannot be reached.
3) Other operators are still syncing their pillars.  George has been syncing for 5 days (from scratch) and he is about 50% complete.  Pillars should not bootstrap from my backup and have elected to sync from scratch.

IMO, the real issue is we need to implement libp2p or an IBD solution to improve sync times.

-------------------------

dat_she_pepe | 2023-08-18 20:58:06 UTC | #3

This isn't exclusive to more orchestrators as described above though.

-------------------------

0x3639 | 2023-08-18 21:12:01 UTC | #4

[quote="dat_she_pepe, post:1, topic:1592"]
As it is now, we clearly see that the bridge can’t recover from a technical problem. Either orchestrators don’t care or they don’t have the technical capabilities to catch up.
[/quote]

I think I was referring to this.  Some of the Orchestrators that are down are very skilled software developers and they are offline for a reason, not because they do not care.  

My guess is the Orchestrators that are offline and also have an offline Pillars are still syncing (like 707).  But others that have Pillars that are up (Moonbazze for example) with an offline Orchestrator are off for a reason.  

I do think we will need a new ceremony after the sync is done.  Operators need to make sure they have a static IP that will not change.  Also, it's not easy to add orchestrators to the Keygen.  If you recall, we had about 35 eligible orchestrators but only 22 were able to stay in sync in order to perform the Keygen.  Many factors impact an Orchestrator's ability to participate.  So even if we had 50 Orchestrators trying to participate, my guess is 30 could be in sync for a keygen.

-------------------------

dat_she_pepe | 2023-08-18 22:17:48 UTC | #5

What makes the ceremony so hard to be in ? Alchemy does not support static IP I guess that made it an issue.

-------------------------

0x3639 | 2023-08-18 23:47:10 UTC | #6

[quote="dat_she_pepe, post:5, topic:1592"]
What makes the ceremony so hard to be in ?
[/quote]

I think early on we realized that many Operators were restarting their znnd node every few hours because of the memory leak.  On top of restarting, nodes should just restart themselves due to the memory issue.  The Orchestrator relies on the znnd node being up.  If the node goes down, the Orchestrator restarts causing it to be out of sync.  I think that was the largest issue.

Now that we've fixed the memory issue I am curious to see how many can stay in sync.  Maybe we can get a lot more in there.

Keep in mind the time to generate a key goes up exponentially with the number of participants.  Look at this study by THORChain.  Not sure how this translates to our situation, but directionally I think it's similar.  

![Screenshot 2023-08-18 at 6.30.48 PM|686x500](upload://pZmz8kaSm7dHI8r1r9aDdCb7dEG.jpeg)

https://medium.com/thorchain/thorchain-publish-tss-whitepapers-d3ea66913721

-------------------------

dat_she_pepe | 2023-08-19 12:35:57 UTC | #7

What makes it hard for an orchestrators to compute this ? It's highly CPU demanding ? Doesn't seem to be that long, unless there's a very short window for nodes to send the results. If yes, the window could be extended.

-------------------------

romeo | 2023-08-19 14:16:39 UTC | #8

I'm all for a new signing ceremony to allow new orchestrators to join - but I'd suggest it be aligned with the 0day patch and the majority of nodes being fully synched again 

lowering the threshold for number of online Orchs requirements I'm not sure about, I'd like to hear @sumamu thoughts on it as to why 66% +1 was chosen and what risk it attempts to mitigate - it does seem like a relatively high threshold to meet

-------------------------

TrevorLeahy3 | 2023-08-19 14:44:18 UTC | #9

If were talking about the risk of collusion between orchestrators how would anything other than majority or super majority % be secure?

-------------------------

dat_she_pepe | 2023-08-19 17:55:14 UTC | #10

We're so secure that we're not even live.

-------------------------

cryptocheshire | 2023-08-19 18:11:57 UTC | #11

Trading/bridging uptime is critical for adoption. Esp. Without Cefi listings

-------------------------

0x3639 | 2023-08-19 23:22:13 UTC | #12

I think the issue was staying in sync while performing the keygen.  The CPU necessary is low.  Last time we had two main issues:

1) Latency
2) Nodes going offline while performing the keygen

I think #2 is solved, so maybe that will improve #1.  I'm all for a new keygen.

-------------------------

mehowbrainz | 2023-08-20 16:03:13 UTC | #13

I'm down for a new keygen too.

-------------------------

TrevorLeahy3 | 2023-08-21 20:38:27 UTC | #14

@sumamu anything the community can do to prepare for a new keygen ceremony? Can we get the word out on a timeline for when it might happen?

-------------------------

