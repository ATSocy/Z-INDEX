Thread: syrius-v0-2-0-rc-2-3
CryptoFish | 2024-03-15 07:04:08 UTC | #1

This post will be used to collect issues for test round #3.

Download: [Syrius v0.2.0-rc.2](https://github.com/zenon-network/syrius/releases/tag/v0.2.0-rc.2)

Read [this ](https://forum.hypercore.one/t/syrius-v0-2-0/328/7) post for more information about how to test.

-------------------------

coinselor | 2024-03-12 12:11:00 UTC | #2

It wasn't my best start, failed at the second row. See [issue](https://github.com/zenon-network/syrius/issues/85). Turns out it is not a big deal, just a chain id mismatch, but this took me 20 minutes to figure out. I realized what was going on thanks to this detailed notification, when trying to fuse plasma to the original wallet from another one:

![image|690x95](upload://qQE18UH0uOrvsyufRlOqRGovyfN.png)

Would it be possible to enhance this one with a similar error message, in this particular case?:

![image|682x116](upload://xxKcWPXh9Pjd7FbmoLXRWODE1fR.png)

Edit: I guess the issue is not the notification above, but that it's silently failing without an "Error while generating Plasma" notification error. 

Edit2: I also wanted to mention a small UI/UX improvement. During the Node Management on boarding flow, the default window size does not accommodate enough space to show the "Wallet options" and "Continue" button sections, and there is no scroll bar indicating the user there is more content hidden from view.

Anyway... will proceed to try to get more PASSes!

-------------------------

CryptoFish | 2024-03-12 15:39:00 UTC | #3

Thank you for your submission.

Coincidentally, two issues have been recently picked up that are somewhat related to your issue. These are:

- https://github.com/zenon-network/syrius/pull/82
- https://github.com/zenon-network/syrius/pull/83

I believe this will solve the small UI/UX improvement you mentioned.

Concerning the issue, I was not able to reproduce the problem exactly as mentioned. The plasma generation loop is by design, because the auto-receiver will try to receive the tx until success.

The difference is that I'm getting an error notification after the plasma generation notification wereas in your case you keep getting only plasma generation notifications. This is the part I cannot seem to reproduce.

![errors|690x373](upload://791uu0qvs1wdhBJoOUpVfZ3o4tT.png)

-------------------------

coinselor | 2024-03-12 15:41:58 UTC | #4

That's interesting. Ok, I will try again in another machine or in another OS and report back or try to reproduce it.

-------------------------

coinselor | 2024-03-12 15:46:02 UTC | #5

Should the client chain id be automatically set by syrius after the user clicks "proceed anyway" ?

In Metamask, it's expected behavior when I get a popup to "change networks/RPC" and I accept, that it automatically changes the chain id, explorer, and everything MM requires to function properly. Should this not be the case in syrius?

Maybe a slight modification of the Popup that reflects the changes that will happen when "proceeding".

-------------------------

CryptoFish | 2024-03-12 20:37:14 UTC | #6

[quote="coinselor, post:5, topic:406"]
In Metamask, it’s expected behavior when I get a popup to “change networks/RPC” and I accept, that it automatically changes the chain id, explorer, and everything MM requires to function properly. Should this not be the case in syrius?
[/quote]

Currently the chain id mismatch only warns the user. It is assumed the user knows what he's doing.
Metamask works differently because it has predefined networks to choose from. They have to be configured explicitly beforehand.
Syrius allows both the node url and chain id to be used interchangeable. Which is not necessarily a good thing.

The chain id and node url are to my knowledge bound to eachother. Meaning you cannot connect the hc1 node with chain id other than 1. While other nodes are specifically meant for testing. So it makes sense to combine both the node url and chain id in one single configration.

One other limitation of the node management screen while onboarding is that you cannot specify the chain id. So for example, if you want to create a new wallet and connect a testnet. You first have to connect to the testnet node using chain id 1 while onboarding and later goto settings and change the chain id.

In general changing the chain id only has to done for testnets or devnets. The average user should not directly be bothered.

I think the node management needs to be redesigned, but later for another future release.

-------------------------

CryptoFish | 2024-03-13 17:06:42 UTC | #7

These issues have been resolved in the following PRs:

- https://github.com/zenon-network/syrius/pull/82
- https://github.com/zenon-network/syrius/pull/83
- https://github.com/zenon-network/syrius/pull/84
- https://github.com/zenon-network/syrius/pull/88
- https://github.com/zenon-network/syrius/pull/89

A new release candidate will be made available.

-------------------------

0x3639 | 2024-03-13 17:33:30 UTC | #8



-------------------------

