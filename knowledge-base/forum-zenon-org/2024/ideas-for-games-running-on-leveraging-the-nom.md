Thread: ideas-for-games-running-on-leveraging-the-nom
dat_she_pepe | 2023-06-16 14:41:02 UTC | #1

As we discussed marketing ideas here https://forum2.zenon.org/t/self-sustaining-accelerator-z/1462/17 we came up with the idea of a game as mentioned in the message below:


> There's only two marketing ideas that I see working in this market right now:
> 
> - One is to attract new devs with funding or great features they can build on.
> - Two is to build something people actually use. For now we only click "collect rewards" and that's it. Build a SIMPLE cool game on top of the FEELESS network we have and normies would realize the advantage of the NoM over others. A simple game can be built within a few days in a gamejam (agar.io is (was?) a good exemple). It can be incentived with player's money; people putting money in a PvP, earning whatever others lose and you build a userbase with an actual product. Bam, marketing on without the cringe of "my coin's better [insert_buzzwords]
> 
> Food for thoughts. I'd vote an absolute yes to any good game idea that can actually be built and is fun. BTC Machine got a simple game the community is having fun on and their community is almost 40k people. We could learn from that.


To extend the conversation further and allow more in-depth discussions, I will present a few SIMPLE games that I think are relatively easy to fork, sometimes with a few improvements compared to what the NoM can do for players.

I will assume our games need a few things to be interesting:
**- Good gameplay loops**. A good gameplay loop should be simple, fun and rewarding.
**- Interesting learning curve.** The learning curve should allow anyone to progress with practice without getting stuck on impossible tasks for too long, which would hurt the gameplay.
**- Good for ZNN or QSR** The gameplay should allow us to think of an interesting economy that benefits the NoM, within the game.
**- Easy to build.** This recoup a few sub considerations; do we need a top designer to make it works? Does it needs a well balanced complex gameplay with different kind of characters? Does it needs a sound engineer to be fun? Does it needs original musics? etc.

Therefore, the perfect fit should be fun, shouldn't need an army of designers, should be tokenomics-compatible, and shouldn't need GBs of content to be fun.


I already have a few candidate in mind:
**- https://agar.io :** This one is almost a perfect fit. It's an old PvP game where you play a sort of cell that needs to eat smaller cells (players) to grow. We can imagine that to play, one must drop 1 ZNN in; eating other players is literally eating their ZNN. It doesn't need fancy design, complex graphics, and if well done, it can be immediately fun. I have no idea if it's still trendy, but this is a good analogy of trading to anyone who has been liquidated by Sam Bankman at least once.
**- Any chess game :** I see you're a boomer.  
**https://playbtcwar.com :** This one is a good fit, but it needs more work on the design side. Graphics and music should be good to make it worthwhile. The player can send 1 ZNN per game, the good old arcade game style. At the end of a given timeframe, the best player wins it all.
**- https://store.steampowered.com/app/674940/Stick_Fight_The_Game/** This one could be fun too. Stickman battle style, it doesn't need a complex balance between characters as we all play the same. Enter with x ZNN and earn the ZNN of players who lost.

You get the idea. Each of those examples is just an example, and each of those can be tweaked so a small fee goes back toward A.Z or whatever. I strongly believe we should avoid the easy way, the dull way, and the boring way if we want to make some noise. We need something catchy.

There might be way more interesting games for us to look at and if I've been a player for a long time I might not know them all so feel free to share and let's discuss the what and how.


Some good games can be built in a week. Any kind of DeFi product would take months and age to review. Most chain simply can't allow gaming to exist, this could be a way to communicate better. Better than a thousand words.

-------------------------

aliencoder | 2023-06-15 21:41:05 UTC | #2

[quote="dat_she_pepe, post:1, topic:1487"]
**- [https://agar.io ](https://agar.io) :** This one is almost a perfect fit.
[/quote]

I think this is a great idea. You can start from literally 0 (to highlight the feeless property of NoM). If you die and want to try again, you'll need to pay 1 ZNN or an equivalent in QSR. If you get bigger and win, you'll get all the ZNN from that round (I don't know what's the endgame).

[quote="dat_she_pepe, post:1, topic:1487"]
https://playbtcwar.com
[/quote]

Games in Unity can be connected to Syrius via [WalletConnect for Unity](https://docs.walletconnect.com/2.0/unity/sign/installation).

Other [gaming ideas](https://www.crazygames.com/t/space)

-------------------------

romeo | 2023-06-15 21:38:26 UTC | #3

The team that performed the bridge audit have a Discord for game developers and their SDK, they suggested that when we are ready to reach out in that discord to canvas ideas or look for Devs to build a game. The SDK is EVM compatible out of the box - so not exactly usable for us yet but there's no reason why we couldn't look for developers or try to sell the project to some:

Info:
https://gaming.chainsafe.io/
https://docs.gaming.chainsafe.io/

Discord: 
http://discord.gg/n2U6x9c

-------------------------

bayrum | 2023-06-15 21:42:14 UTC | #4

My idea can be hard to implement but I think the future is competing in esports for real money. I always dreamt to play cs:go for money. Making money on pure skill. Maybe this idea can inspire someone, 5vs5 matches and you pay entry 1znn each person, you win 2znn each or tournaments . Good luck. The idea has huge potential, one website gathering dota 2,cs:go etc... playing for znn.

-------------------------

dat_she_pepe | 2023-06-15 21:42:26 UTC | #5

Easy to implement should be a criteria. Mandatory not to make a bad game imo.

-------------------------

aliencoder | 2023-06-15 21:45:04 UTC | #6

[quote="romeo, post:3, topic:1487"]
so not exactly usable for us yet
[/quote]

It will be usable once we have the extension chain live.

-------------------------

dat_she_pepe | 2023-06-15 21:48:20 UTC | #7

Why do we need extension chain first ? Could we have simple tokens mechanics with the actual L1?

-------------------------

sol | 2023-06-15 21:51:53 UTC | #8

Keep in mind, I do not have a trustless solution for any games/services that involve earnings. We don't have smart contract that can facilitate the redirection of funds to a winner.

https://t.me/zenonnetwork/190785

If we are willing to trust people not to rug their users, then these kinds of services can be built today. 
I'm prepared to assist any gamedevs if they want to plug into NoM.

-------------------------

aliencoder | 2023-06-15 22:04:14 UTC | #9

We can, but the extension chain will be EVM-compatible out of the box.

Web page with games <-> WalletConnect <-> Syrius

Game outcome (win/loss) <-> Oracle <-> Conditional payment

-------------------------

aliencoder | 2023-06-15 22:04:50 UTC | #10

For oracle based conditional payments I mean [DLCs](https://dci.mit.edu/smart-contracts)

@georgezgeorgez already implemented PTLCs, right?

-------------------------

sol | 2023-06-15 22:13:56 UTC | #11

I'm aware of DLCs, but I don't know how we can execute/enforce them on NoM with our current utility.

-------------------------

aliencoder | 2023-06-15 22:16:23 UTC | #12

The DLC is "executed" by the oracle. The enforcement is done by the underlying cryptography (the signed tx is broadcasted into the network and included into an account-block).

More info [here](https://suredbits.com/schnorr-applications-scriptless-scripts/).

-------------------------

crack | 2023-06-15 22:16:46 UTC | #13

So when extension chain? We need to wait it before we built the game,
Do you have the estimate for this stuff done?

-------------------------

aliencoder | 2023-06-15 22:20:01 UTC | #14

[quote="crack, post:13, topic:1487"]
So when extension chain?
[/quote]

Already working on it. 

[quote="crack, post:13, topic:1487"]
We need to wait it before we built the game
[/quote]

No, go ahead with the game.

[quote="crack, post:13, topic:1487"]
Do you have the estimate for this stuff done?
[/quote]

I'm finishing Syrius v0.0.7 now and I'll focus 100% on extension chains next. A devnet is achievable before August.

-------------------------

sol | 2023-06-16 02:51:09 UTC | #15

Right, but none of us have attempted to run DLC oracle software on NoM yet. Anyone is welcome to try, I think it's a good idea.

Wouldn't we still be trusting the game provider to be honest, though?

-------------------------

NeoShredder | 2023-06-16 01:52:43 UTC | #16

Any details regarding this extension chain? Evm based or a L2 for BTC?

-------------------------

crack | 2023-06-16 02:48:06 UTC | #17

[quote="aliencoder, post:14, topic:1487"]
No, go ahead with the game.
[/quote]

can you @sumamu handle the DLC since Sidechain will be handled by aliencoder ?

-------------------------

aliencoder | 2023-06-16 08:05:38 UTC | #18

[quote="sol, post:15, topic:1487"]
Wouldn’t we still be trusting the game provider to be honest, though?
[/quote]

From what I see most of the games are client side. Multiplayer games can be hosted by a "trusted" provider with good ratings/reviews.

-------------------------

aliencoder | 2023-06-16 08:06:41 UTC | #19

[quote="NeoShredder, post:16, topic:1487"]
Any details regarding this extension chain
[/quote]

EVM based. It looks more like a sidechain than an L2.

-------------------------

aliencoder | 2023-06-16 08:08:14 UTC | #20

[quote="crack, post:17, topic:1487"]
can you @sumamu handle the DLC
[/quote]

I think @georgezgeorgez can do it faster. He already has experience with PTLCs and adaptor signatures.

-------------------------

aliencoder | 2023-06-16 08:15:37 UTC | #21

I've discussed with @zyler9985 and we need someone to start reskinning popular & open source HTML5 games:

https://github.com/topics/html5-games

-------------------------

ImperiumBNC | 2023-06-16 08:16:33 UTC | #22

I have a friends who’s a video game engineer and he is currently building and developing a game. I think it could fit with what’s been shared here. I’m going to suggest the idea to him and I’ll let you know what he thinks soon.

-------------------------

romeo | 2023-06-16 10:56:52 UTC | #23

Any game at this stage needs to bring in new users, no point just being a proof of concept or Chess clone etc 

Things that will bring in new people:

- addictive gameplay
- gambling aspects (loot boxes, NFTs, RND rolls/drops, unique items)
- competitiveness/leaderboards/progression 
- rewards (monetary or otherwise)

Doesn't have to be graphically impressive, just needs to hit a couple of these aspects well

-------------------------

angelo_a_jr | 2023-06-16 13:37:29 UTC | #24

Also wondering if these types of NoM equivalent tools could be built to send ZNN/QSR/ZTS to everyday handles like e-mail, telephone number, etc.

https://www.privy.io/
https://www.usekeyp.com/
https://magic.link/

-------------------------

dat_she_pepe | 2023-06-16 13:41:12 UTC | #25

Make it money + pvp and you'll hit the jackpot imo. People love gambling and a lot of crypto people love games

-------------------------

zyler9985 | 2023-06-16 13:50:59 UTC | #26

My vote is for a racing game. People would love to race their friends. Like a mario cart clone. I personally don't mind shitty graphics, as long as its fun to play and simple. Can do free races or can spice it up by waging ZTS tokens on it (znn/qsr or inches or another one ... )

-------------------------

sol | 2023-06-16 14:06:13 UTC | #27

[quote="dat_she_pepe, post:25, topic:1487"]
People love gambling
[/quote]

I am fully aware that this is a killer use case.
My issue is: will anyone use my game/platform if they need to trust me with their funds?

I guess the only way to know is to build it and see. 
I don't have a ton of spare time, though.

-------------------------

mehowbrainz | 2023-06-16 14:41:21 UTC | #28

Topic moved to #marketing:funding-staging.

-------------------------

dat_she_pepe | 2023-06-16 14:55:23 UTC | #29

With sidechain we can distribute the trust no ? So it can start a bit centralized during a testing stage and move forward to a better product. The recent Ordinal run is an interesting case study : centralized sometimes closed sources online wallets won by far by being simple and easy to use, with good UI and good UX over fully decentralized self custodian ones.

-------------------------

