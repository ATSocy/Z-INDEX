Thread: nom-developer-coordination-meeting-5-9-feb-12-pm-utc-draft
0x3639 | 2024-02-09 11:04:40 UTC | #1

**What:** NoM Developer Coordination Meeting #5
**When:** [Friday 9 Feb @ 12 PM UTC](https://www.worldtimebuddy.com/?qm=1&lid=6,5128581,2643743,100&h=5128581&date=2024-2-9&sln=7-8&hf=1)
**Where:** [Discord Channel - #dev-meeting ](https://znn.link/discord)  If you need the Discord Sever => [https://discord.gg/a8mky5DA ](https://znn.link/discord)
**Duration:** 2 Hours
**Purpose:** Discuss Open PRs, Status of Open Work, Phase I Roadmap
**Agenda:** TBD

Note: This post is a wiki. Anyone can edit it to add / change items to the agenda.

## DRAFT AGENDA

1. Discuss Open PRs
* [PLTCs](https://github.com/zenon-network/go-zenon/pulls)
* [znn_cli_dart](https://github.com/zenon-network/znn_cli_dart/pulls)
* [znn_sdk_dart](https://github.com/zenon-network/znn_sdk_dart/pulls)
* [znn_ledger_dart](https://github.com/hypercore-one/znn_ledger_dart/pulls)
* [syrius](https://github.com/zenon-network/syrius/pulls) - ledger support, alienc0der's v0.0.7 changes and bug fixes
* [zenon.network](https://github.com/zenon-network/zenon.network)

2. Discuss Open Development
* Ledger Integration
* Extension Chain
* Dynamic Plasma

3. Discuss Roadmap to Phase I

Please let me know if you can attend.  If this date does not work how about the following Friday?  

@georgezgeorgez @vilkris @CryptoFish @sol @digitalSloth @aliencoder @sumamu @cagri @Nostromo @MoonBaze

-------------------------

aliencoder | 2024-01-21 22:05:43 UTC | #2

[quote="0x3639, post:1, topic:316"]
* syrius upgrade (dust attacks)
[/quote]

@CryptoFish is on it, so it will be ready by then :smiley: 

[quote="0x3639, post:1, topic:316"]
* Extension Chain
[/quote]

Hope I make good progress next week.

-------------------------

cagri | 2024-01-22 08:00:54 UTC | #3

It'll be my first meeting, thank you for inviting :v:

-------------------------

vilkris | 2024-01-23 07:18:37 UTC | #4

I'm not sure yet if I can attend on the 2nd but I'll try.

-------------------------

0x3639 | 2024-02-01 23:19:48 UTC | #5

Guys, we've changed this meeting to 9 Feb at the same time.  A few devs were not able to join.  I hope this time works for everyone.

https://www.worldtimebuddy.com/?qm=1&lid=6,5128581,2643743,100&h=5128581&date=2024-2-9&sln=7-8&hf=1

-------------------------

0x3639 | 2024-02-09 11:20:21 UTC | #6

## Open PRs for Dev Meeting

### Syrius
![Screenshot 2024-02-09 at 4.56.16 AM|690x359](upload://pDtfEj2JQGnz0dPNpGz4LwsyWCu.png)
@vilkris and @aliencoder reviews needed

### znn_sdk_dart
![Screenshot 2024-02-09 at 5.00.32 AM|690x140](upload://yc68qbA2g4gMwaWU9zM53qfF8hH.png)
@vilkris and @aliencoder reviews needed

### znn_cli_dart
![Screenshot 2024-02-09 at 5.01.29 AM|690x141](upload://4mAELuxRkVPiAJDnho46GpPo1KW.png)
@vilkris and @aliencoder reviews needed

### znn_ledger_dart
![Screenshot 2024-02-09 at 5.19.57 AM|690x111](upload://fMuXS9rtlXifOwt5PImIkRK96qo.png)
@vilkris 

### zenon.network
![Screenshot 2024-02-09 at 4.57.36 AM|690x108](upload://3MP4zEpkfjoaczSXWaiTlpXLGe.png)
@vilkris review needed.  Simple mixed-content error in css.

### go-zenon
![Screenshot 2024-02-09 at 4.58.31 AM|690x104](upload://f2ncvvfdZjz9bVytT5wVKFibXRV.png)
@vilkris @aliencoder @sumamu Review needed.  @aliencoder asked for a working session with @georgezgeorgez before performing the review.

-------------------------

0x3639 | 2024-02-09 11:10:29 UTC | #7

## Potential Roadmap Discussion Items

- Dynamic Plasma @vilkris 
- Extension Chain @aliencoder 
- [Bitcoin Interoperability / Integration: Merge Mining](https://forum.hypercore.one/t/bitcoin-interoperability/283) @aliencoder 
- libp2p upgrade (will this impact the extension chain or it's function and how important is this?  Is this more important than BTC interoperability solutions?) #TBD
- Sentinels #TBD
- N&T, zK solutions and others #TBD

-------------------------

