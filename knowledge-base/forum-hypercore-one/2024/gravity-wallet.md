Thread: gravity-wallet
Nostromo | 2023-12-10 07:32:15 UTC | #1

I have been contemplating an idea. It’s a very simple concept, essentially a mobile wallet that is streamlined.

I have seen the Figma design for the Sirius mobile app, and it’s beautiful. I look forward to using it. However, I believe that Sirius might be overwhelming for new users as it introduces too many concepts that are irrelevant to most users.

I propose a basic wallet called “Gravity.”

The focus and narrative around Gravity are straightforward. It strips away all the complexities of the Network of Momentum. The message of the Gravity wallet is zero transaction fees for tokens with an emphasis on fiat-backed stablecoins.

The wallet will be very simple, and the design should be neutral but elegant. The main screen will have an account overview and a token list. Users will have the ability to send and receive funds, made easy with QR codes and an address book. That’s it—very simple.

There is only one thing the user needs to learn about this wallet: there are two states, the default Gravity state and the Zero Gravity state. When the Gravity wallet holds a QSR balance, it turns into Zero Gravity. Behind the scenes, the wallet automatically fuses QSR; the user doesn’t need to do anything. When the wallet is in Zero Gravity, the UI changes, is lifted, and the logo transforms.

The marketing and communication to new users are simple: Buy QSR and keep it in the wallet for Zero Gravity.

The initial market for this could be people in countries like Turkey, Venezuela, Argentina, Nigeria, etc., who transact a lot in stablecoins via EVM chains and tend towards those with the lowest fees. Ultimately, the target audience for this app is literally everybody in the world.

An appealing narrative could be the free and uncensorable nature of the wallet. I want the user to be able to download the app, open it, and be in it immediately. Unlike Metamask, where a user downloads the app and is greeted with terms of service agreements. Gravity has no terms of service, it provides egalitarian, free, and uncensorable access to the network.

What are some drawbacks or pain points of this idea?

* There are currently no stablecoins on the Network of Momentum, and bridged EVM coins provide a poor user experience. If users can’t buy ZTS stablecoins on exchanges and send them to their Gravity wallet via an address or QR code, then this wallet will struggle to find users.
* A QSR market. The point here is nearly the same as with the previous one. The user needs to be able to easily get QSR into their wallet.
* A embedded node. It would be most ideal if the app runs a light node that syncs with the zk proof in a matter of seconds. Connecting to public nodes will add a layer of complexity that this app is trying to remove.

I’m under a time constraint at the moment, so I’m not sure if I did a good job putting the idea to paper. But that is the basic idea of the Gravity wallet. Let me know what you guys think of it. Any ideas are welcome.

-------------------------

Zyler | 2023-12-10 08:10:47 UTC | #2

This is a really smart and elegant idea. Rather than try to make the existing hardcore wallet super simple and noob-friendly, simply have a separate light wallet which is easy for mass-appeal/mass-use. Those actually interested can find the hardcore wallet and follow guides/ask Qs.

On Zenocratez account I shared some alternative designs for SYRIUS to consolidate functionality onto the main tab/dashboard, which I still think should be done, but maybe SYRIUS can have a light wallet equivalent too. One which is just for delegating and staking, but doesn't have any pillar/sentinel/zts creation stuff for example.

-------------------------

Zyler | 2023-12-10 08:25:56 UTC | #3

My only contrarian point is that if we are going for maximum clarity, then Gravity/Zero gravity and any space-terms are too complex. Even though it's really cool, I think it's too hard for mass-appeal.
In my work I meet a dozen or more people every day in an intimate setting, so I feel I know first-hand how simple you need to make things such that the majority of people will understand intuitively. 

An alternative?
Call it a Q-name to make people realise you need QSR. Make a display of a QSR tank similar to a fuel tank, where it's red, empty and unhappy with no QSR, but with QSR it becomes green, full and happy (and automatically fused). A "QSR tank" rather than the zero-gravity thing. Wallet could literally be called the Q Wallet.

For the record – your idea is way cooler. My suggestion is just to dumb things down significantly, as people already understand fuel tanks and your target is the whole world? My 2 cents

-------------------------

Nostromo | 2023-12-10 11:10:26 UTC | #4

Thanks for your input; that is worth considering.

The reason why I went with the Gravity and Zero Gravity terminology and symbolism is because I was looking for something thematic that embodies the technological aspect in a metaphorical context that makes it easier to understand. It's challenging to explain to somebody that they can make a free transaction, but their device will need to perform a POW calculation.

However, to say 'yes, it's free, but there is a gravity to this transaction', makes it more tangible. It is heavy; it may take longer and use more battery. Put QSR in the wallet, and the transaction becomes lighter and moves with zero gravity.

This is easy to understand and makes sense to people as they have an intuitive understanding that nothing is free, and they come to reconcile this understanding without the need for explaining proof of work, plasma, and all that jargon that goes along with crypto.

Ultimately, it comes down to testing and seeing how POW works on a phone. This really depends on how Phase 1 is implemented and what the performance metrics are.

-------------------------

0x3639 | 2023-12-10 11:15:16 UTC | #5

@Nostromo do you have the URL?  I like the name, but let's make sure you can get a good URL.  Looks like there are several other options... .xyz, .ai, etc...

![Screenshot 2023-12-10 at 5.11.30 AM|678x500](upload://2zDQyiFNMMD1QDZCagfzZT0RlgE.png)

-------------------------

0x3639 | 2023-12-10 11:26:39 UTC | #6

[quote="Nostromo, post:1, topic:270"]
The marketing and communication to new users are simple: Buy QSR and keep it in the wallet for Zero Gravity.
[/quote]

Love this idea.  Super simple.  No staking, delegating, nodes, TOS, just send and receive.  

[quote="Nostromo, post:1, topic:270"]
Gravity has no terms of service, it provides egalitarian, free, and uncensorable access to the network.
[/quote]
Remember @georgezgeorgez's P2P Revolution?  It's coming.  We are setting new standards.

[quote="Nostromo, post:1, topic:270"]
There are currently no stablecoins on the Network of Momentum, and bridged EVM coins provide a poor user experience. If users can’t buy ZTS stablecoins on exchanges and send them to their Gravity wallet via an address or QR code, then this wallet will struggle to find users.
[/quote]

Build it and they will come.  It's like everything in this project.  FAFO.  What comes first, stable coins on exchanges or a wallet to use them?  

[quote="Nostromo, post:1, topic:270"]
A QSR market. The point here is nearly the same as with the previous one. The user needs to be able to easily get QSR into their wallet.
[/quote]

We do have QSR whales where it's highly concentrated.  But they are redistributing it.  I think this gets solved over time.  Whales know QSR needs to get out into the wild for the network to function.  I believe they will part with it. 

[quote="Nostromo, post:1, topic:270"]
A embedded node. It would be most ideal if the app runs a light node that syncs with the zk proof in a matter of seconds. Connecting to public nodes will add a layer of complexity that this app is trying to remove.
[/quote]

Is this where a Sentry comes into play with something like zerosync?

[quote="Nostromo, post:1, topic:270"]
There is only one thing the user needs to learn about this wallet: there are two states, the default Gravity state and the Zero Gravity state. When the Gravity wallet holds a QSR balance, it turns into Zero Gravity. Behind the scenes, the wallet automatically fuses QSR; the user doesn’t need to do anything. When the wallet is in Zero Gravity, the UI changes, is lifted, and the logo transforms.
[/quote]

Love this concept.  Most people know what gravity is.  We don't need to explain it.  Introducing a new term to describe the wallet that people don't understand will just be another hurdle.

-------------------------

Nostromo | 2023-12-10 11:35:44 UTC | #7

I haven't put much thought into this yet. I just searched for gravity-related terms in the cryptosphere and found some projects which makes sense given the seemingly generic name. Upon checking, it appears that [https://gravity.wallet](https://gravity.wallet/) yields no results. What are your thoughts on this URL?

-------------------------

0x3639 | 2023-12-10 11:45:13 UTC | #8

Are you thinking unstoppable domain? Taken.  I'll investigate more.  

![Screenshot 2023-12-10 at 5.41.05 AM|690x409](upload://ixDz5Um9sIfyHemJDaxdC6BNi1p.png)

![Screenshot 2023-12-10 at 5.44.39 AM|690x299](upload://qRTbELvDMiXwJ6XpiXSNZcB1lbw.png)

-------------------------

Blueginger | 2023-12-10 12:11:36 UTC | #9

@Nostromo Are you a developer? If not who will develop this wallet?

Is it possible to fork an open source wallet code?

-------------------------

Blueginger | 2023-12-10 12:17:54 UTC | #10

gravity-wallet.com
gravitywallet.app
gravitywallet.network

These are available. But I think url shud be shorter .

-------------------------

Shazz | 2023-12-10 12:21:06 UTC | #11

It's a great concept / metaphor. Please keep it.

-------------------------

Nostromo | 2023-12-10 12:37:08 UTC | #12

Yes, that said, I am not very experienced, and I am currently learning Flutter.
The wallet will be open source, of course, and anybody willing to contribute is more than welcome to once I get the repo online.

-------------------------

coinselor | 2023-12-10 17:57:31 UTC | #13

I think the concept is great and well thought-out.

Instead of just relying on bridged USDT, I believe we can do better than that. We should start looking into over collateralized stablecoin protocols. Once NoM owns BTC, we could create a NoM-native synthethic asset pegged to a basket of currencies that behaves as a stablecoin and is overcollaterized by BTC. 

Clearly this requires in-depth R&D, but can also become a significant piece of the holy grail of BTC DeFi.

-------------------------

0x3639 | 2023-12-10 17:58:06 UTC | #14

@Nostromo have you looked at the new coinbase [send with link](https://www.coinbase.com/blog/with-coinbase-wallet-sending-money-is-now-as-easy-as-sending-a-text)?  

This must have centralized features, so not part of the P2P Revolution. But if we can be this simple without central actors, it could be pretty interesting.  

https://youtu.be/MqDmXdibCM4

-------------------------

1776 | 2023-12-10 19:54:28 UTC | #15

Second this.

Also Strike.me is pretty elegant/simple design.

Would this be a native Apple/Android app wallet or are you thinking PWA app?

-------------------------

0x3639 | 2023-12-22 11:03:28 UTC | #16

@Nostromo I'm curious why you are interested in developing the Gravity Wallet, which I like a lot, over some of the important plumbing in the network.  Based on our conversation about Dynamic Plasma you seem to be interested in the network architecture too.  

We have important network upgrades to consider too:
- libp2p
- Sentinels / PoW links
- IBD

I personally think `libp2p` is very important given some of the issues we have with syncing nodes.  It's possible George is working on this, but it's also possible he is focused on something else.... in true alien style.

![Screenshot 2023-12-22 at 4.15.19 AM|690x293](upload://4GBBEYchqJYQDEezKHKXx6uf7cD.jpeg)

There is an issue with scheduling downloads in the existing p2p code.  And if you recall during the `fork era` and this last surge of users syncing `s y r i u s` it takes for ever and requires a restart of `go-zenon` every hour or so.

-------------------------

Nostromo | 2023-12-22 10:51:16 UTC | #17

Yes, syncing a node is an absolute mess right now.

While I appreciate your vote of confidence a lot, implementing libp2p or IBD takes a significant amount of expertise, which I definitely don't have.

Gravity is an ideal project for me for the time being. I'm hoping to get the code on GitHub in a few months. The alpha version will be for Android, Windows desktop, and Web.

-------------------------

cagri | 2023-12-27 00:50:19 UTC | #18

I'd like to contribute to the project, can you share repo?

-------------------------

0x3639 | 2023-12-27 11:11:14 UTC | #19

I found this image interesting given the goals of the Gravity Wallet.

![Screenshot 2023-12-27 at 5.09.59 AM|480x500](upload://3mgo5aUuUYAnXHy8U5M5hDzmzJY.jpeg)

-------------------------

Nostromo | 2023-12-27 14:10:56 UTC | #20

Hello, sir. Currently, there is no repository as I am still in the conceptual phase. I have expanded the scope a bit. I have decided to abandon Flutter in favor of a React Native mobile app and a React web app.

The web app will share the design of the mobile app but will also have the same functionality as MetaMask, including the ability to connect to websites. This approach should enable interactions with the main chain and any extension chains for web3.

-------------------------

0x3639 | 2023-12-27 19:38:11 UTC | #21

Have you read the discussion about [Metamask Snaps](https://forum.hypercore.one/t/metamask-snaps-for-zenon/209)?   Have you thought about how the app will generate PoW?

-------------------------

Nostromo | 2023-12-28 02:06:23 UTC | #22

Thank you; I just read through that discussion. Some good points were raised by Vilkris.

Regarding conducting Proof of Work from a web app, I believe it's possible with RandomX. In the FAQ, it states: 'Web mining is infeasible due to the large memory requirement and the lack of directed rounding support for floating-point operations in both Javascript and WebAssembly.'

Here are two points to consider:

1. We are not aiming to conduct mining.
2. Rounding can be emulated in software but will be very inefficient.

For economically feasible mining, efficiency is a crucial consideration. However, when using PoW against transaction spam and as a proxy for network utilization, the efficiency of the hashing calculations is not as important. Additionally, the difficulty adjustment dynamic is also different.

In Monero, for example, the hash rate of the network determines the difficulty, and miners are incentivized to add hash rate by being able to mint coins.
In Zenon, however, network utilization determines the difficulty. Transactors are disincentivized to use PoW by longer wait times as network utilization increases and are instead incentivized to fuse QSR for plasma.

I would estimate that the PoW calculations on the web app would take something like 10 - 20x longer than in Syrius. So maybe a transaction that would require 30 seconds of hashing with Syrius might take 7 minutes with the web app.

This is where the Gravity | Zero-Gravity UI guides the user towards holding QSR. I think adding a staking function into the web app will be useful too, especially considering there is no easy way to buy QSR.

If someday we can make QSR dynamic as well, this will work out very well for all fusers.

-------------------------

Chadass | 2023-12-28 11:11:13 UTC | #23

Regarding RandomX I remember a crypto rave project organised in Geneva and you had to mine XMR to get your tickets. It was years ago though, can't find the website back.

-------------------------

vilkris | 2023-12-28 11:33:39 UTC | #24

[quote="Nostromo, post:22, topic:270"]
I would estimate that the PoW calculations on the web app would take something like 10 - 20x longer than in Syrius. So maybe a transaction that would require 30 seconds of hashing with Syrius might take 7 minutes with the web app.
[/quote]
You also need to take [light mode and fast mode](https://forum.hypercore.one/t/plasma-pow-with-randomx/224#downsides-and-potential-issues-with-randomx-2) into consideration. Fast mode requires at least 2 GiB RAM which is not possible in a browser. There's around a 5x difference between the modes based on my testing. If Syrius is running in fast mode, then the difference in speed becomes 50-100x, assuming your estimation of 10-20x is correct.

I would start with a PoC to prove that RandomX plasma PoW can be computed within a reasonable time in a browser before basing any decisions on that assumption. I doubt it will be fast enough to be a viable option and not worth the additional complexity it introduces.

-------------------------

Nostromo | 2023-12-28 14:01:04 UTC | #25

[quote="vilkris, post:24, topic:270"]
assuming your estimation of 10-20x is correct
[/quote]

That estimation was based on one Reddit comment I read, but I have since read more about it and seen reports of it being significantly slower than that.

I guess it depends on the difficulty, what the baseline is, and how it ramps up with demand. But either way, it seems like it may be a pain to run in the browser if a transaction could take hours when the difficulty even slightly ramps.

Maybe @1776's suggestion of a PWA could be a better solution, as they have more access to hardware, I think. Not too sure, will look into it and do some testing.

-------------------------

0x3639 | 2023-12-28 19:45:59 UTC | #26

["first store" in Kenya](https://www.youtube.com/watch?v=JRxUR_UJk6I) accepting $kas.  You should check out their mobile wallet.  It's not very good.

-------------------------

