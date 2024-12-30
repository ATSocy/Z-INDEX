Thread: what-can-we-do
sol | 2023-07-04 14:13:59 UTC | #1

Most new participants will be attracted by the applications built on top of NoM. We don't have any at the moment.

So what can we do on NoM?

The goal of this thread is to surface interesting ideas, discuss capabilities/limitations, and find devs that can build them.

Please don't focus too much on Syrius' current functionality unless you have a way to leverage it to do something new.

Examples
- Damus clone with ZNN zaps
- Encrypted messaging protocol on NoM
- ztamps / [znnscriptions](https://ethscriptions.com/) / zrc-20 (external indexing/consensus)
- [Games on the blockchain](https://twitter.com/NewBitcoinCity/status/1669562178284982272?s=19) (external indexing/consensus)

There are plenty of other ideas.

-------------------------

0x3639 | 2023-07-04 15:07:04 UTC | #2

I personally think we should do the most retarded and degenerate gambling game know to man. This sort of game could become catchy and could generate public interest.  It will be "easy" to code and will test NoM on a small scale.  

We have some degenerate community members here who will be good and designing such a game.

-------------------------

dat_she_pepe | 2023-07-04 15:14:13 UTC | #3

- It there a way to use the Pillars / Sentinels for a better version of TOR? It's niche though.
- DeFi but feeless. 
- Gaming, as it makes sense with little fee or feeless. Gaming in crypto is still something to be seen. There's only craps so far: see https://forum2.zenon.org/t/what-if-i-told-you-nom-game-edition/1490/11
- Real crosschain bridge with BTC and native BTC DeFi products.
- NFTs as DeFi legos.

See this for more narratives : 
![image|594x500](upload://hGbdzQifx31kUDxUaCdmc9zuSRY.jpeg)

-------------------------

0x3639 | 2023-07-04 15:19:12 UTC | #4

I also think rolling out a "game changer" like the [New NFT Standard](https://medium.com/@zenon.network/the-new-nft-standard-when-cryptography-meets-steganography-9e356007dcaa) could develop interest.  Just not sure how long it would take to implement and I think getting a "small win" with an easy degenerate game would be helpful.

-------------------------

dat_she_pepe | 2023-07-04 15:32:02 UTC | #5

If you want a game that works, and attract people it has to be good even WITHOUT ZNN. Chess games are giga niche. This will never thrive.

-------------------------

SugoiBTC | 2023-07-04 15:35:35 UTC | #6

I agree with @0x3639, a simple game where you're able to gamble for profits could be very effective and attract degenerates.

The game [SatoshiDice](https://satoshidice.com/) has been mentioned a few times in the community already and demonstrates the feeless properties of NoM.

Would a game like this be possible to build?

-------------------------

dat_she_pepe | 2023-07-04 15:41:20 UTC | #7

[quote="SugoiBTC, post:6, topic:1537"]
I agree with @0x3639, a simple game where you’re able to gamble for profits could be very effective and attract degenerates.
[/quote]

Yes, a gambling game with an AMAZING UI & UX would be so damn good. Need to be able to bet BTC though.

-------------------------

0x3639 | 2023-07-04 16:03:22 UTC | #8

It could be as simple as a lottery where you can increase your odds by interacting with the network in some say.  Or, in order to participate in the lottery you need to Fuse 120 QSR and and stake 10 ZNN.  

We should research casino games.

-------------------------

dat_she_pepe | 2023-07-04 16:15:36 UTC | #9

Bring BTC but don't make it a pay to win. Increase your gains by betting more, not your odds to win. Bustadice was good for that. Check https://bustadice.com/ & https://www.bustabit.com/

-------------------------

aliencoder | 2023-07-04 16:22:47 UTC | #10

[quote="sol, post:1, topic:1537"]
* Damus clone with ZNN zaps
[/quote]

https://github.com/ethicnology/dart-nostr

https://github.com/anasfik/nostr/

[quote="sol, post:1, topic:1537"]
* Encrypted messaging protocol on NoM
[/quote]

https://pub.dev/packages/libsignal_protocol_dart

[quote="sol, post:1, topic:1537"]
* ztamps / [znnscriptions ](https://ethscriptions.com/) / zrc-20 (external indexing/consensus)
[/quote]

Inscriptionz*

[quote="sol, post:1, topic:1537"]
Games on the blockchain
[/quote]

TBA


**I would focus on the docs to be able to seamlessly onboard all the devs & users that will come in the very near future.**

-------------------------

sol | 2023-07-04 19:54:43 UTC | #11

[quote="0x3639, post:2, topic:1537"]
gambling game
[/quote]

Gambling, lotteries, anything involving the automation of asset transfers (incl. 2-player PVP winner-takes-all) requires **trust** at this time. 
Sumamu stated he can leverage compute on an external chain to solve this but I don't know how.

George has mentioned this in the past: [1](https://t.me/zenonnetwork/190779) and [2](https://t.me/zenonnetwork/190785)

The early services running on Bitcoin, potentially even some that are operating today, have a risk of rugging. You must deposit coins with the service provider and trust that they will pay out the winnings and deposit back to you in a timely manner.

This can be achieved today on NoM but we carry the same risk.
If that isn't an issue for the degens among us, then anyone can clone any of the hundreds of gambling sites and hook it up to NoM. 
I'll even help with the backend, but I don't want to operate the platform.

Sidebar: wen bustabit clone on NoM?

---------

[quote="dat_she_pepe, post:3, topic:1537"]
use the Pillars / Sentinels for a better version of TOR
[/quote]

I don't think we should allow our core infra to host Tor exit nodes. They're high profile targets, likely to be subpoenaed by their local jurisdictions and subjected to DOS attacks. I guess we could try to limit their exposure to the wider web, only permitting specific clients to connect to them, but this is probably not going to garner much interest.

I have a different idea related to content-hosting -- recursive inscriptions on NoM, accessible via a custom client. Honestly, it's inevitable if this network grows beyond our little group.

[quote="dat_she_pepe, post:3, topic:1537"]
DeFi but feeless.
[/quote]

This is potentially a killer app of our platform. George has worked on an AMM.
We can even setup [Expiring Offer Contracts (EOC)](https://github.com/orgs/Big-Inches-Club-House/discussions/1#discussioncomment-4824577) for buy/sell orderbooks.

What sets us apart is feeless high-frequency trading of wrapped assets.
Unfortunately, Mr Kaine doesn't support this idea and didn't elaborate. 
#decentralized #MrKaineWontCreateTheSpork


[quote="dat_she_pepe, post:3, topic:1537"]
* Gaming
* BTC DeFi products.
* NFTs as DeFi legos.
[/quote]

I think these fall under the Zenon Asset Standard category. I'm trying to design a flexible system that can support a variety of use cases.
This ties in to my "data storage is Zenon's killer use case" argument, by the way.

------------

[quote="aliencoder, post:10, topic:1537"]
focus on the docs
[/quote]

This should be one of our top priorities. I'm hoping we can automate most of it, though.

This thread is more of a thought experiment to see what we all value. 
Prospective devs can find this thread and start building things that we think are important.

------------

Good ideas so far! What else can we do on NoM?

-------------------------

cryptocheshire | 2023-07-04 19:42:27 UTC | #12

I second this

-------------------------

cryptocheshire | 2023-07-04 20:01:26 UTC | #13

What about a quiz?

- X players throw ZNN in a pot in the same principle as a pre-flop texas holdem round. People can do blind raises and fold if they chicken out.
- once everyone has entered the equal amount into the pot, GPT generates a random question about anything
- first player to answer correctly wins the pot.

Extensions:
- add questions about btc/zenon/satoshi
- enable sats and zats to be put in the pot at the current exchange rate
- auto generate badges/nfts/pfps on nom for winners of big pots to brag with

-------------------------

mehowbrainz | 2023-07-04 20:02:02 UTC | #14

In its current stage, what can NoM support? What are we missing?

-------------------------

Dr.GreenThumb | 2023-07-04 20:16:44 UTC | #15

[quote="sol, post:11, topic:1537"]
Gambling, lotteries
[/quote]

How about the legal status of web3 gambling  that varies depending on the jurisdiction, but it's basically the same as the online gambling.
These regulations aim to ensure fairness, protection, and responsible gambling. In regions with strict gambling regulations web3 gambling may face legal restrictions or prohibitions.

-------------------------

sol | 2023-07-04 20:22:48 UTC | #16

[quote="cryptocheshire, post:13, topic:1537"]
What about a quiz?
[/quote]

Okay, so is it a quiz or closest guess to a random number generated by an external party?
Quizzes probably need predetermined answers. ChatGPT is still a wildcard these days.

If you're looking for RNG on NoM, I found an interesting way to achieve this.
Users can speculate on momentum hashes at specific heights.

[quote="mehowbrainz, post:14, topic:1537"]
In its current stage, what can NoM support?
[/quote]

I like to pretend we're around the same stage of development as early Bitcoin.
Whatever they could do back then, we can probably do now.

I draw a lot of inspiration from other projects that have similar constraints as us.

[quote="Dr.GreenThumb, post:15, topic:1537"]
In regions with strict gambling regulations web3 gambling may face legal restrictions or prohibitions.
[/quote]

Anyone is welcome to run their own trusted casino platform. 
I don't want to be entangled with this kind of legal liability.

-------------------------

dat_she_pepe | 2023-07-04 20:28:50 UTC | #17

[quote="sol, post:11, topic:1537"]
Gambling, lotteries, anything involving the automation of asset transfers (incl. 2-player PVP winner-takes-all) requires **trust** at this time.
[/quote]

Can it be fully smart contract on L2?

-------------------------

sol | 2023-07-04 20:36:20 UTC | #18

[quote="dat_she_pepe, post:17, topic:1537"]
Can it be fully smart contract on L2?
[/quote]

Yeah, we can off-load a lot of utility on an EVM side-chain, though there will be gas fees.

I'm still convinced that feeless (increased operating margins) will be enticing to some people.

-------------------------

dat_she_pepe | 2023-07-04 20:53:49 UTC | #19

Embedded BetGPT

-------------------------

aliencoder | 2023-07-04 21:44:27 UTC | #20

[quote="sol, post:11, topic:1537"]
Gambling, lotteries, anything involving the automation of asset transfers (incl. 2-player PVP winner-takes-all) requires **trust** at this time.
[/quote]

[This sample code](https://github.com/p2pderivatives/dlc/blob/master/test/integration/dlc_test.go) demonstrates how 3 parties communicate. An oracle Olivia publishes a n-digit number lottery result everyday, and Alice and Bob bet on the lottery.

In the tese, the following scenarios are tested.

* Alice and Bob make contracts and execute a fixed one.
* Oracle does't publish a valid message and sign, and contractors refund their funding transactions.

[quote="sol, post:11, topic:1537"]
Unfortunately, Mr Kaine doesn’t support this idea and didn’t elaborate.
[/quote]

I remember he said that we should keep the base layer minimal & robust. High-frequency stuff can be moved off-chain.

[quote="sol, post:11, topic:1537"]
#MrKaineWontCreateTheSpork
[/quote]

#GovernanceEmbedded

[quote="sol, post:11, topic:1537"]
What else can we do on NoM?
[/quote]

- DLC
- Extension chains for user smart contracts
- zk-powered L2s

-------------------------

sol | 2023-07-04 22:13:44 UTC | #21

[quote="aliencoder, post:20, topic:1537"]
An oracle / DLC
[/quote]

Do you know who would run the oracle software in our network? I think there's still an element of trust here but it's still worth exploring.

[quote="aliencoder, post:20, topic:1537"]
he said that we should keep the base layer minimal & robust. High-frequency stuff can be moved off-chain.
[/quote]

"Minimal and robust" are evaluated subjectively and the architect refuses to elaborate.
I could debate that a base-layer AMM wouldn't be any more complex than the Bridge while greatly benefiting all participants in the ecosystem.
Just because we can offload this to a side-chain doesn't mean a base-layer implementation is a bad idea.

-------------------------

coinselor | 2023-07-04 23:36:31 UTC | #22

Chatgpt or alien?

1. Pool of aliens
2. sign up phase (buy-in cost)
2. Algo selects a random alien alice and gives her chatting permission
3. Algo selects either another random alien bob or chatgpt
4. Alien alice can ask up to 5 questions
5. Round of betting, double or nothing. Is it bob or chatgpt? alien or ai? 
6. If bob sucessfully pretends to be chatgpt he gets a % of the total amount wagered. 

Inspired by https://www.reddit.com/r/ChatGPT/comments/12s6de9/obsessed_with_this_game_right_now_you_chat_with_a/

more info: https://www.ai21.com/blog/human-or-not-results

-------------------------

cryptocheshire | 2023-07-05 08:16:46 UTC | #23

combine it with onlyfans and AI image generation and call it "bot or thot" to onboard a few million dudes

-------------------------

0x3639 | 2023-07-05 09:21:48 UTC | #24

Interesting idea. Can this idea scale?  Can we get thousands of people to play it?

Would autonomous games scale better?    

This plinko game looks pretty cool.  But I don't think anyone should run infra that centralizes running any betting game.

https://github.com/kayooliveira/plinko-game

-------------------------

