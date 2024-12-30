Thread: nostr-nom
angelo_a_jr | 2024-03-27 15:19:50 UTC | #1

At build_republic (ideally one of NoMs first zApps) we're reaching a decision point for which decentralized social stack to use.  Obviously Nostr is top of mind but was curious to know more about what capabilities Nostr would have with NoM both right of the bat and over time given its BTC relationship.

On the ETH side there are clients like Farcaster which have a very active community and a seamless onboarding UX.

Would be great to get both technical perspectives and ELI5 explanations.

-------------------------

sol | 2023-10-25 15:59:43 UTC | #2

Glad to see you're interested in Nostr! At this time, the Nostr tooling ecosystem is growing at a healthy pace, so there should be something out there that fits into your stack.

Unfortunately, there aren't any plug-and-play libraries for NoM. HC1 is planning to develop a matchmaking system to facilitate PTLC transactions [[1](https://t.me/zenonnetwork/285658), [2](https://t.me/zenonnetwork/300348)], but nothing has been published yet.

If anyone wants to learn more about Nostr development, check out supertestnet's [workshop](https://github.com/supertestnet/nostr-workshop-demo) and the [NIPS](https://github.com/nostr-protocol/nips#list).

-------------------------

angelo_a_jr | 2023-10-25 16:28:31 UTC | #3

Thank you, will take a look through.

I figured there's not and plug-and-play libraries for NoM nor was I expecting any at this stage.

Was mainly trying to figure out how the pub key could, if at all, work with NoM given the BTC interop.

Given Nostr has the same level of cultural acceptance by BTC community as lightning, what could/would the relationship look like between BTC <> Nostr <> NoM.  

I guess a prereq would be better understanding how BTC <> NoM are supposed to function before answering how Nostr would fit into the picture.

Good read on Nostr <> BTC relationship here:  https://protos.com/what-is-nostr-and-why-do-bitcoiners-love-it/

-------------------------

Stark | 2023-10-25 23:15:28 UTC | #4

[Can NoM serve a mega relay?](https://bitcoinmagazine.com/culture/can-nostr-grow-to-twitter-size)

A federated super relay operated by the Network of Momentum? 

Can someone with more technical knowledge chime in?

1. How far away are we from being capable of such a thing?

2. What kind of cost would this impose to pillars / participants?

If the operating cost isn't too high, and it's technically feasible, there is a case to be made for showing up with a big egalitarian show of force.



Other Nostr reading:
[Overview of Nostr](https://bitcoinmagazine.com/technical/what-makes-nostr-a-different-social-platform)

[Key Management](https://bitcoinmagazine.com/technical/solving-nostr-key-management-issues)

-------------------------

cryptocheshire | 2023-10-26 04:32:31 UTC | #5

I suggest we focus on growing the community first by tapping into known watering holes. We have few dev resources, they  focus on critical stuff. New joiners from Nostr can build these things if they want it.

-------------------------

