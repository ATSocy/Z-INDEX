Thread: bsc-liquidity-providers
mehowbrainz | 2023-02-09 18:10:34 UTC | #1

I think it's worthwhile for BSC wZNN Liquidity Providers to discuss and coordinate a date and time to remove their liquidity and bridge back to ZNN.

Track current LP's: https://bscscan.com/token/0xe6b03fcb16daf3462ddfb8b0afb3f0e87d38d884#balances

Let's also discuss about the potential volatility of ZNN's price as liquidity thins on BSC.

@0x3639 proposed to coordinate an effort on either January 21st, 22nd, 28th or 29th.

-------------------------

mehowbrainz | 2023-01-20 14:40:12 UTC | #2

ZenonOrg is okay with any of those dates.

-------------------------

ZNNAYIID | 2023-01-20 14:48:26 UTC | #3

I'm not sure, but I think wZNN contract will remain the same, only the bridge will deprecate, so keeping liquidity is okay.

-------------------------

mehowbrainz | 2023-01-20 14:57:08 UTC | #4

I don't quite follow how one would wanna keep it if there's no way to bridge back into ZNN after, other than selling and buying native ZNN elsewhere? Let's say the bridge is deprecated, and one LP wants to get back to ZNN, he'd have to sell his wZNN using Pancake, and then buy native ZNN elsewhere right? But what happens to the last few LPs when they also wanna get back to ZNN, what liquidity will they use to sell wZNN so they can get buy back into ZNN? The last LPs of a bridgeless BSC wZNN are gonna be in trouble, no?

IMO it's safer for LPs to swap back to native ZNN, and then reposition themselves into a new pool once @sumamu's interop solutions are rolled out.

-------------------------

ZNNAYIID | 2023-01-20 14:57:12 UTC | #5

the new bridge will support the current contract if I'm not mistaken, so as long as you'll get a way to get back to native ZNN in the next months, it's not worth removing all the liquidity we have now and try to build it again once the new bridge is live.

-------------------------

0x3639 | 2023-01-20 14:57:46 UTC | #6

any one of those dates work for me.  I have a block out from 11AM  to 3PM Central Standard Time on Jan 22 where I cannot access a computer.  All other times are good with me.

-------------------------

mehowbrainz | 2023-01-20 14:59:17 UTC | #7

I think we should confirm whether the new bridge will support the BSC wZNN contract, and whether we'll be able to bridge back to native ZNN using it. I wasn't aware of such capabilities until now.

-------------------------

ZNNAYIID | 2023-01-20 15:01:02 UTC | #8

yeah, we need to confirm with sumamu.

but this was sigli's response : https://discord.com/channels/920058192560533504/920068653330874398/1066007136833908747

-------------------------

mehowbrainz | 2023-01-20 15:04:09 UTC | #9

Yes some clarity would be nice from @sumamu 🙏🏼

![Screenshot 2023-01-20 at 10.02.09 AM|690x408](upload://ztu5A1dzKw1ejOrNqishK3KVaR6.png)

-------------------------

SugoiBTC | 2023-01-20 15:28:59 UTC | #10

Update:
![image|445x500](upload://upof4rnpKd8WE2zxChAwQBS3eU6.png)

-------------------------

coinselor | 2023-01-20 16:00:53 UTC | #11

Coordinating and bridging from BNB Chain to Zenon Network seems like the smart thing to do. I would vouch for that sensible approach and applaud aliens coordinating that effort. Advising bridge operators of the increase influx of transactions that day is also in order.

Disclaimer: I exited my LP position like a month or so ago, in a dump. Mostly to increase ZNN exposure and to avoid the (hopefully) impermanent loss on the way up. But I provided liquidity non-stop since day one, hack and all.

-------------------------

mehowbrainz | 2023-01-20 16:13:00 UTC | #12

There is a risk of confidence loss if ZenonOrg removes its 31% share position.

If it doesn't weight the risk of keeping the liquidity in BSC wZNN, it may have its position stuck there if no BSC wZNN to ETH wZNN bridge is made available. From what I understand, there is no guarantee when or if it'll happen.

-------------------------

mehowbrainz | 2023-01-20 16:22:08 UTC | #13

It would also make sense for LPs to wait for hummingbot to arrive on Stex or a new wZNN ETH pool to come around -- but if the legacy bridge is deprecated before the new bridge comes around, then the LP risks being stuck with potentially illiquid BSC wZNN.

-------------------------

0x3639 | 2023-01-20 16:41:29 UTC | #14

I'm going to ask this question in Twitter.  Sumamu is responsive there.

-------------------------

0x3639 | 2023-01-20 16:44:37 UTC | #15

Fired off the question.

![image|462x125](upload://bm0zxXDiDHbOesLAzYBTPaQYZ8q.png)

-------------------------

0x3639 | 2023-01-20 17:01:22 UTC | #16

Response.  I don't think we should NOT plan on the current bridge contract being transffered.  

![image|456x264](upload://8DTV9k8mVqnR7CeqwGdTcunzUow.png)

-------------------------

mehowbrainz | 2023-01-20 17:19:59 UTC | #17

[quote="0x3639, post:16, topic:1189"]
I don’t think we should NOT
[/quote]

Can you rephrase that haha though I get it, recommendation is to wait it out

-------------------------

0x3639 | 2023-01-20 17:23:18 UTC | #18

Sorry.  I'm all over the place.  Closing a loan right now.  

I do NOT think we should assume Kaine will transfer the existing BSC contract.

-------------------------

mehowbrainz | 2023-01-20 17:27:44 UTC | #19

With that assumption, BSC wZNN would not be bridgeable to ETH wZNN using @sumamu's new bridge, right?

-------------------------

0x3639 | 2023-01-20 17:38:27 UTC | #20

Correct.  Here is my logic.

Kaine told us to remove all wZNN from the BSC contract.  I can only assume that means it will be archived and taken down all together.

Then, the new bridge will launch a new BSC contract all together and the old BSC contract will not be usable.  This is entirely an assumption on my part reading between the lines.  

But keep in mind, as Sumamu said: "I think there’s still time and it’s probably best to just wait for more info." He thinks we should wait and see.

-------------------------

ZNNAYIID | 2023-01-20 18:01:05 UTC | #21

Best thing to do is to spam kaine on main chat before processing with removing liquidity, especially for large LPs.

-------------------------

mehowbrainz | 2023-01-20 18:03:51 UTC | #22

We could show a step forward in the right direction by first taking care of non-LP's (wZNN hodlers) via a push of the [Bridge Deprecation Campaign](https://twitter.com/ZenonOrg/status/1616143842134331392?s=20&t=RrB11TTDPKisNztX4OmMNw). I think Kaine will be more willing to share info then.

The best way to push the campaign: Create pressure in the Telegram / Discord channels. Create the trend.

-------------------------

0x3639 | 2023-01-20 20:30:10 UTC | #23

agree.

-------------------------

0x3639 | 2023-01-21 10:30:10 UTC | #24

Guys, I just realized that we need to coordinate this with people who have TXs stuck in the ZNN > wZNN direction.

I'm talking to a guy now who has about 1500 ZNN stuck.  If we pull all our liquidity before the ZNN > wZNN TXs are unstuck, these people will not be able to sell.  And, once the wZNN > ZNN bridge is removed these people will not be able to sell OTC either.  

@Sigli I think we need to explain this to Mr. Kaine and ask him to help.  How many other stuck TXs (ZNN to wZNN) are there?  

I'm also thinking about people selling wZNN OTC.  Once the old wZNN > ZNN bridge is expired, we need to be careful selling this OTC.  It's possible the wZNN will not be convertible to ZNN.

-------------------------

cryptocheshire | 2023-01-21 13:49:51 UTC | #25

They can just swap back though

-------------------------

mehowbrainz | 2023-01-21 14:47:28 UTC | #26

ZenonOrg's pool share increased from 31% to 34% today. Some LP's are swapping back to ZNN.

-------------------------

DrD3 | 2023-01-21 17:05:44 UTC | #27

I believe Kaine mentioned an article or for more info to be released for LP providers on tg. I don't see the need to rush and withdraw our liquidity until Team Sumamu's bridge alternative is up and running. Tho I won't mind if you guys wanna withdraw- that'll vastly increase my daily bread :grin:

-------------------------

DrD3 | 2023-01-21 17:07:13 UTC | #28

![Screenshot 2023-01-21 at 6.02.17 PM|690x414](upload://haiTbY1bzrwU5qy1tBFY4incaOd.jpeg)

-------------------------

0x3639 | 2023-01-21 17:07:16 UTC | #29

ya that's my thinking too.

-------------------------

0x3639 | 2023-01-21 17:07:39 UTC | #30

my rewards have gone up 2X since I started.

-------------------------

DrD3 | 2023-01-21 17:10:17 UTC | #31

Man I have to say I greatly admire ZenonOrg's commitment to the cause!

-------------------------

mehowbrainz | 2023-01-22 17:14:15 UTC | #33

[quote="Sigli, post:32, topic:1189"]
(bearing in mind that the bridge is still open at this time)
[/quote]

Yeah that's the key, hopefully they acknowledge LPs holding their position to help a gradual transition for everyone.

-------------------------

mehowbrainz | 2023-01-25 15:14:25 UTC | #34

Looking at [Liquidity Program Distributor address](https://zenonhub.io/explorer/account/z1qqw8f3qxx9zg92xgckqdpfws3dw07d26afsj74), it seems like it sent 1843.19 on Jan 25, 2023. There's 62,149.52501347 left in its balance. At this rate, we're looking at a depleted balance within 33.71845822 days, which is February 27, 2023.

Seems to match with other directives received recently in Telegram:

> Mr Kaine on Jan 18, 2023
> They should hurry up as we need to move on and make progress at a greater pace.
> All devs are invited to open PRs until the end of February or earlier. After review, they will be merged and the community will need to coordinate for upcoming network upgrades.

Does this mean that the Orbital Program (Protocol Level Liquidity) begins then?

Would they make it exactly 1 year after the liquidity program began, on March 1st, 2022?

-------------------------

DrD3 | 2023-02-22 15:40:02 UTC | #35

Sooo, what happens in 6 days guys? Do we finally start receiving some znn/qsr from orbital? Y'all withdrawing before that happens?

-------------------------

mehowbrainz | 2023-02-25 16:17:59 UTC | #36

Orbital rewards seem like they still have to be discussed with the community and implemented cc @sumamu

-------------------------

mehowbrainz | 2023-03-03 19:03:31 UTC | #37

To all major LP's, when do you guys think to remove your positions?

-------------------------

0x3639 | 2023-03-03 22:43:08 UTC | #38

I removed my liquidity from PCS and moved everything to Stex.  Kaine said they are not supporting the bridge so if that BSC node goes down or something happens we could be waiting a while.  

So after his notice this week I removed my liquidity and moved it to Stex.

-------------------------

