Thread: metamask-snaps-for-zenon
aliencoder | 2023-09-13 20:09:47 UTC | #1

Developing a new browser extension is now obsolete since Metamask released snaps.

https://metamask.io/snaps/

Let's discuss about integrating Zenon into Metamask directly.

-------------------------

aliencoder | 2023-09-13 20:02:17 UTC | #2

Some Metamask Snaps examples:

[Bitcoin in Metamask](https://snaps.metamask.io/snap/npm/btcsnap/)

[Shapeshift multichain Snap](https://snaps.metamask.io/snap/npm/shapeshiftoss/metamask-snaps/)

[Cosmos Snap](https://snaps.metamask.io/snap/npm/cosmsnap/snap/)

-------------------------

vilkris | 2023-09-13 20:04:24 UTC | #3

Interesting. I'll definitely investigate this. Thanks for sharing.

-------------------------

aliencoder | 2023-09-13 20:15:55 UTC | #4

What's the best part?

- No more dev work on our own browser extension
- Access instantly >10M Metamask users
- More focus on Syrius desktop & mobile

-------------------------

Chadass | 2023-09-13 20:27:52 UTC | #5

Let's also address the elephant in the room: users can now easily swap anything to BTC and I doubt the average user even know or even care (unfortunately) about the difference between P2P swaps native BTC to USDT or anything and this solution where they can keep using Metamask. 

This can be an issue heavily undermining the narrative we're trying to play with BTC.

-------------------------

aliencoder | 2023-09-13 20:37:10 UTC | #6

Some people come with solutions, others with problems.

This was about bringing Zenon closer to ordinary users.

[quote="Chadass, post:5, topic:209"]
This can be an issue heavily undermining the narrative we’re trying to play with BTC.
[/quote]

There are multiple narratives in Zenon, go with the one that suits your vision/goals/expectations.

-------------------------

Chadass | 2023-09-13 20:59:08 UTC | #7

Both aren't exclusive and I'm not attacking your proposal nor your work. So get down of your high horse. There aren't 1000 narratives and this need to be at least discussed. Maybe not in this thread though.

The question would be : is this change other aspect of ZNN development or make those irrelevant? If yes how and if no why. The field is evolving and this tends to reformulate problems and how to fill gaps.

-------------------------

sol | 2023-09-13 20:58:32 UTC | #8

I think MM Snaps are worth considering, though we may not have many devs that can/will work on this.

Any volunteers?

-------------------------

0x3639 | 2023-09-13 21:05:48 UTC | #9

Maybe Dexter has bandwidth?

-------------------------

vilkris | 2023-09-13 21:22:42 UTC | #10

I'd need to research what possibilities Snaps could offer us but I might consider working on this. I'm interested in how this could improve the ETH bridge experience (and maybe the extension chain experience?) to make the onboarding into Zenon smoother.

I'm finishing up the ZTS<>ZTS P2P swaps project so I should have more bandwidth soon.

BTC<>ZTS P2P swaps are another possibility, so depends on what makes more sense for us now.

-------------------------

aliencoder | 2023-09-14 07:49:05 UTC | #11

I see another benefit of Metamask Snaps:

Users will be able to easily swap `ZNN` to `XZNN` directly inside Metamask.

We will need to replicate this flow inside Syrius desktop and mobile as well.

-------------------------

vilkris | 2023-09-14 08:43:04 UTC | #12

After a quick dive into these snaps they seem pretty cool.

The snaps are completely open and permissionless, meaning that we don't need to worry about having to publish anything to an "app store". We just publish an npm package.

I suspect there will be a ton of development & hype happening around snaps in the near future since the barrier for devs to start building is very low, and you don't have to worry about lots of the annoying complexities of building a complex extension because MetaMask handles that for you.
And like Aliencoder said, you get access to the MetaMask userbase of millions of people so you don't need to onboard them into your own extension.

EVM <> Zenon dapps like the bridge can build a full experience for the user, only requiring MetaMask to be installed. Nothing stopping us from adding Bitcoin functionality into the snap as well.

For the purpose of allowing low effort, maximally easy onboarding into our network, I think this is a good option for that.

Some technical aspects and ideas to consider:
* I think being able to send PoW transactions with the snap is crucial for an easy onboarding experience. The need for gas in EVM networks is such a UX painpoint.
Apparently WASM can be used with snaps, but there seem to be limitations to how long a background process can be executed for on the snap: https://docs.metamask.io/snaps/concepts/lifecycle/ 
60 seconds may not be enough to send a PoW TX but we'll need to investigate this some more.

* It would be nice to allow the user to use a local node with the snap. The snap could work as a proxy between a webapp and a local node. We would have to define an RPC interface that webapps could use to make RPC calls to the node through the snap.

* Cron jobs could possibly be used to automate the receiving of TXs in the background (among other stuff): https://docs.metamask.io/snaps/reference/exports/#oncronjob

* The snap could be used as just a simple keystore & node provider for dapps. UIs for basic NoM functionality (like staking, delegating, etc.) and the EVM bridge could be provided by webapps (that anyone can build) and the snap would just be used to sign & send transactions and provide a node connection. Of course all this functionality could be built directly into the snap as well.

I'm impressed at what MetaMask is doing here.

[quote="aliencoder, post:11, topic:209"]
Users will be able to easily swap `ZNN` to `XZNN` directly inside Metamask.
[/quote]
Yes exactly. Could probably make a smooth experience between ETH <> ZNN <> XZNN.

-------------------------

Stark | 2023-09-15 04:59:09 UTC | #13

Whereas Bitcoin is the lesser volatile and less moonboi-ish asset, I think people who buy BTC are generally more aware of what they are buying.

I still think that decentralization will be the core theme of the next bull run, and the task of educating the market will not rest solely on our shoulders. The market will be looking for a solution like Zenon.

SEC and FEDNOW may turn out to be some of our best advertising.

We don't chase, we attract.

-------------------------

0x3639 | 2023-09-15 21:42:12 UTC | #14

https://www.youtube.com/watch?v=lv8A6yeIqkI

-------------------------

aliencoder | 2023-09-16 10:24:16 UTC | #15

[quote="vilkris, post:12, topic:209"]
* 60 seconds may not be enough to send a PoW TX but we’ll need to investigate this some more.
[/quote]

For the moment it's enough, but I'm not sure when dynamic Plasma gets integrated.

[quote="vilkris, post:12, topic:209"]
* It would be nice to allow the user to use a local node with the snap. The snap could work as a proxy between a webapp and a local node. We would have to define an RPC interface that webapps could use to make RPC calls to the node through the snap.
[/quote]

This way we can offload the PoW creation to the node.

-------------------------

vilkris | 2023-09-26 07:36:15 UTC | #16

I spent some more time testing and researching the snaps platform and made the following findings:

* Keystore generation works - a zenon keystore can be derived from the metamask account. This means that the zenon keystore is tied to your metamask account. It should not be possible for anyone to link your EVM accounts to the zenon account.

* The snap can indeed be used as a relay between a webapp and a local node, meaning that dapps can be used with a local node.

PoW generation:
* The 60 second timeout is still a problem. There is currently a feature in the snap environment that allows for long running processes to be executed, but unfortunately this feature is deprecated and will be removed soon. On the bright side the snaps team is actively working on providing a new solution for long running tasks: https://github.com/MetaMask/snaps/issues/1604

* Using the current C++ implementation for PoW generation via WASM isn't really feasible in a snap. The snap runs in a [secure execution environment](https://docs.metamask.io/snaps/concepts/execution-environment/) that has limitations that complicate the usage of WASM in a snap. There have also been reports of issues with WASM performance: https://github.com/MetaMask/snaps/issues/1422

* I overcame the WASM issues by rewriting the PoW algorithm to work with Typescript directly which allows it to be run inside the snap.

#### PoW generation feasibility with dynamic plasma and RandomX

A new problem that came up in regards to PoW generation within browser environments is that if we change the PoW algorithm to RandomX, like has been suggested, then browser-only onboarding into our network will not be possible. It is not viable to compute RandomX in browser environments: https://github.com/tevador/RandomX/blob/master/README.md#does-randomx-facilitate-botnetsmalware-mining-or-web-mining

This means that browser based wallets, like the snap wallet, will have to rely on either a separate locally run program that can do the PoW generation, or on external services that provide PoW or Plasma as a service. Currently the only way to onboard onto our network without external services is by doing PoW transactions.

If the snap wallet requires the user to install a separate program on their computer to be able to use the wallet, it interferes with the idea of using browser wallets to allow for a very low effort onboarding experience. Getting the user to install and trust the program is a UX challenge.

Another option is to build external PoW and Plasma services that can be used by wallets, but how are such services incentivized?

#### High level view of a snap wallet and the related components
![snap|690x333](upload://wsjcN76M4esV49WabeXexHkfLdS.png)

-------------------------

0x3639 | 2023-09-26 09:48:12 UTC | #17

We need a good web wallet IMO that is easy to use and install with no "special" steps. I guess the desire to move to RandomX is to prevent an ASIC style attack on the account blocks? 

We need ease of use but want to prevent spam attacks.  Incentivized PoW seems like another step that we are too young (small) for.  Curious what others think.  

![Nervous Ted Striker GIF by filmeditor|480x270](upload://2CDy56M5L6djwGg11vDXhaVnwGk.webp)

-------------------------

digitalSloth | 2023-09-26 10:43:10 UTC | #18

If it helps initially until a more viable solution can be found I could setup an API route for the plasma bot which the snap could use? 

We can adjust the parameters of how much and for how long QSR is fused for this specific application. The bot has 70k QSR available and only a tiny fraction is ever in use at the moment

-------------------------

0x3639 | 2023-09-26 12:54:02 UTC | #19

Maybe there is a market to process PoW.  Users could either fuse QSR or pay a 3rd party for PoW (right in the app).

-------------------------

0x3639 | 2023-09-26 13:00:44 UTC | #20

I might be interesting in offering a PoW service.  I have a location where I use to mine.  I have a utility contract in place for $0.05/kwh.

-------------------------

vilkris | 2023-09-27 11:19:53 UTC | #21

[quote="digitalSloth, post:18, topic:209"]
If it helps initially until a more viable solution can be found I could setup an API route for the plasma bot which the snap could use?
[/quote]
Thanks. That could be used as a temporary solution to get things started. It would work as long as it's not abused and the network's utilization is small.

But we may have to think about this problem a bit more, because in the long run without the user being able to generate PoW they cannot onboard onto the network.

[quote="0x3639, post:19, topic:209, full:true"]
Maybe there is a market to process PoW. Users could either fuse QSR or pay a 3rd party for PoW (right in the app).
[/quote]

The problem these services have is that the user cannot pay for the services because they can't interact with the network if they can't generate PoW. They can't receive their funds from the bridge nor can they fuse plasma for their account if they can't generate PoW.

Maybe the services could be paid for with other cryptocurrencies/fiat but I think that might create a confusing UX and of course introduce trust issues.

-------------------------

0x3639 | 2023-09-27 12:23:19 UTC | #22

Wonder if there another CPU algo that can be run in the browser?

From link above regarding RandomX:

> Web mining is infeasible due to the large memory requirement and the lack of directed rounding support for floating point operations in both Javascript and WebAssembly.

-------------------------

coinselor | 2023-09-29 16:55:45 UTC | #23

[quote="vilkris, post:21, topic:209"]
They can’t receive their funds from the bridge nor can they fuse plasma for their account if they can’t generate PoW.
[/quote]

Maybe this is a good point to bring up in the Dynamic Plasma discussion. Before RandomX is implemented, we could explore the option of leaving an "incorporation lane" to the highway that can be exclusively used by "new" accounts running a browser wallet. This is just another random idea, but hopefully gets the brains working :)

-------------------------

vilkris | 2023-10-02 20:42:35 UTC | #24

[quote="0x3639, post:22, topic:209"]
Wonder if there another CPU algo that can be run in the browser?
[/quote]
Based on some research I did the options are pretty limited. One alternative "ASIC resistant" algorithm is Dero's novel [AstroBWT algorithm](https://github.com/deroproject/astrobwt) that is claimed to be FPGA, ASIC, and GPU resistant but it would need more research to determine if it's otherwise suitable for us.

But even if we had a browser friendly PoW algorithm, I'm not sure if it's a long term scalable solution to generate PoW in browser environments (or on mobile phones for that matter), because once the network usage picks up, the PoW difficulty will rise and generating PoW in a browser will be slow. People hate slow.

One idea of how these PoW/Plasma services could work is to get pillars to operate a kind of "wallet provider" service, in exchange for the user's delegation. The wallet's UX would have to be tightly coupled with the "wallet provider" service. The wallet provider would be responsible for generating PoW/fusing Plasma for the user, and these concepts could then even be abstracted away from the user. Ideally the wallet provider will have the resources to provide fast transactions to the user. If the user is not satisfied with the provider, they can always change it by delegating to another pillar that offers the service.

When onboarding a new user the wallet provider could check that the user actually has a pending transaction in the bridge and it will only generate PoW for that transaction. The wallet's onboarding flow could be made in such a way that after the user has selected the wallet provider that onboarded the user, the user will have to delegate to that pillar. Referral links would ideally be integrated also, so that pillars could advertise themselves as wallet providers and the wallet would onboard the user directly as a delegator to that pillar.

It's hard to make such a service unabusable but wallet providers could limit how many transactions the delegator can send within a time period and if the user is not a delegator they might only generate PoW for a transaction that is a delegation transaction to the pillar.

-------------------------

0x3639 | 2023-10-02 20:56:50 UTC | #25

This is interesting.  I assume the wallet "service" offered by Pillars could be run on specialized hardware, especially since this will be CPU intensive.  Pillars will potntially need to run CPU farms.

-------------------------

vilkris | 2023-10-03 06:42:21 UTC | #26

I suspect that a decent VPS would be enough at the start, especially if it's combined with fusing some plasma to the delegator but yes, with sufficient network utilization the providers would need specialized hardware. Maybe there could be a separate market for PoW generation where pillar operators can make deals with PoW providers. Lot's of people have Monero mining rigs that aren't all that profitable at mining Monero for example.

From the user's perspective the goal is that they get free, fast, and effortless transactions and I think if we're looking to maximize user friendliness and achieve "global adoption", the key is to abstract away as much as possible. The user doesn't need to now what PoW is, or what Plasma is to use the network. They don't need to select what pillar to delegate to from 100 options, since the wallet can onboard them as a delegator to a specific pillar and advertise the fact that they get free transactions and x% APR for their funds while doing so.

In the future we'll probably have DeFi services, NFT marketplaces, etc. built on sidechains and L2 solutions and we'll want to abstract away the boundary between these different layers.

The same goes for BTC and zBTC and ideally the user can send native Bitcoin to a Zenon address for example. The wallet will automatically bridge the BTC to zBTC, and the recipient will receive zBTC, but the complexity is abstracted away from the users. From their perspective they're sending native BTC to a Zenon address.

-------------------------

0x3639 | 2023-10-03 15:39:04 UTC | #27

I like this idea a lot for the following reasons:

1) We need a browser wallet. I suspect developing a snap is faster and will be more secure than building a wallet from the ground up or rebuilding what Dexter prepared.
2) Metamask has wide adoption.  I believe people will feel more comfortable interacting with NoM over Metamask + a snap.  
3) I like the idea of abstracting away the PoW / Plasma fusing to Pillars.  Initial the PoW required by Pillars will be low, and as it grows so will that market place.  it will evolve.  You can count on me to provide a PoW service to my delegators.

Question: will we offer "Advanced" user the ability to run RandomX on their local PC to make their own PoW if they are technically capable?

-------------------------

vilkris | 2023-10-04 08:28:58 UTC | #28

[quote="0x3639, post:27, topic:209"]
Question: will we offer “Advanced” user the ability to run RandomX on their local PC to make their own PoW if they are technically capable?
[/quote]
Ideally we want to offer the option to use the wallet without a wallet provider. Meaning you can run your own node and do pow generation.

But if the user is someone who absolutely does not want to connect to any third party services, I'm not sure how well we can cater to that user group in the long run. Once we have the extension chain, the wallet will need a connection to an EVM node. If we integrate a Bitcoin wallet into the snap, it will need a Bitcoin node. Maybe we want to add support for ordinals and BRC20 tokens, then it will need a connection to Unisat's API for example.

I think it's possible that the user can provide their own infra for the wallet but eventually it will get more complicated. Most extension wallets/mobile wallets rely on a centralized backend, so having multiple pillars provide the backend separately is still an improvement to that, with a negligible effect on ease of use.

-------------------------

0x3639 | 2023-10-04 13:21:05 UTC | #29

makes sense.

-------------------------

coinselor | 2023-10-04 16:07:39 UTC | #30

There's a reason why the most used LN wallets are custodial, a better UX ends up winning over the users. Most people don't have their BTC life savings in them, so I think that's a reasonable compromise people are willing to take for convenience. 

I like the wallet provider idea, and we don't seem to be compromising much at a glance. 

Regarding the more knowledgeable/hardcore user group, I think we are already offering best-in-class UX in syrius, while being cross-platform, and we should just maintain the standard moving forward as we increase the capabilities of the wallet/network. I don't see a good reason to "stay" in the browser for such an user unless a mobile device is being used.

-------------------------

vilkris | 2023-10-04 19:17:30 UTC | #31

[quote="coinselor, post:30, topic:209"]
There’s a reason why the most used LN wallets are custodial, a better UX ends up winning over the users. Most people don’t have their BTC life savings in them, so I think that’s a reasonable compromise people are willing to take for convenience.
[/quote]
I agree, but I want to highlight that even with the wallet providers the snap wallet would be non-custodial and only the user can access the keys. The keys never leave the metamask extension.

[quote="coinselor, post:30, topic:209"]
Regarding the more knowledgeable/hardcore user group, I think we are already offering best-in-class UX in syrius, while being cross-platform, and we should just maintain the standard moving forward as we increase the capabilities of the wallet/network. I don’t see a good reason to “stay” in the browser for such an user unless a mobile device is being used.
[/quote]
Syrius is definitely best-in-class when it comes to "core" network wallets. It has its role as our core wallet, catering to power users. I think syrius should continue to focus on stability, security and minimizing its dependency on external services and new features should be added when necessary. On the other hand a browser based wallet could focus more on experimentation, ease of use and cater to a different set of user needs.

-------------------------

vilkris | 2023-10-05 12:05:43 UTC | #32

So how would this project move forward.

I would have to make a proper description of the architecture, of the different components, and of the potential risks, so that the community could better evaluate and discuss the idea.

But before that, how high of a priority would this kind of a project be? Community members have voiced their opinion that developer resources should be focused on critical tasks only. I understand that protocol upgrades are top priority right now, but I don't consider myself a protocol developer, so network upgrades aren't really in my comfort zone.

Another area I've researched is how Bitcoin P2P swaps could be implemented in syrius, and while the community is expecting that feature, I'm not sure which of these projects (snaps wallet or BTC P2P swaps) would drive more adoption to our network in the short term. I can't really focus on both projects at the same time.

I've also volunteered to develop the syrius UI for the governance module that @georgezgeorgez has been working on, but I don't expect that to be too big of a task.

If we can get the extension chain that @aliencoder is working on into use in the coming months, then I think the snap wallet would make onboarding users onto the extension chain much easier, driving new users into our ecosystem. The possibility of adding Bitcoin integrations into the snap is also intriguing, although it would take some time to get there. Ultimately I believe that sooner or later we will need to start tapping into the vast user base that exclusively uses simple-to-use extension and mobile wallets.

Then again Bitcoin P2P swaps in syrius would be good PR for us, allow for more cross-chain liquidity, and could get more Bitcoin people interested in our network.

-------------------------

0x3639 | 2023-10-05 12:31:01 UTC | #33

We plan to hold the dev meeting tomorrow (Friday @ 12 PM UTC) and hopefully we can dive into this discussion in more detail then.  

In the meantime, I think the fastest path to onboard more users and increase adoption is a simple, secure, and reliable web wallet.  Metamask is best in class and leveraging their platform will help our users feel safe.

I also think native P2P swaps with BTC is an important use case.  However, the number of people that will use such a feature will be much less than people wanting to use a web wallet.  Also, once the EVM side chain is up, and the web wallet is bringing in new people, it's possible (likely) some BTC devs will get interested in what we are doing.  Maybe these new devs can help architect and implement native P2P swaps with BTC.  Or at a minimum, they can join forces with @vilkris @sol @CryptoFish and @aliencoder to work on the feature.  

In summary, I think implementing a NoM snap for Metamask is an A+ priority for stimulating adoption, especially once the side chain is available.

-------------------------

0x3639 | 2023-10-14 15:47:25 UTC | #34

Wow if this is true

https://watcher.guru/news/metamask-removed-from-apple-app-store?c=76

![Screenshot 2023-10-14 at 10.46.52 AM|690x167](upload://x6K0gla5FxakVoa5PRvit0DBg7p.png)

-------------------------

0x3639 | 2023-10-14 17:18:58 UTC | #35

it's back

https://twitter.com/WatcherGuru/status/1713234587365593099

-------------------------

