Thread: nfts-on-nom-fr
sumamu | 2023-08-02 19:21:31 UTC | #1

Man, am I excited about this one.

I've spotted some ZTS' in the wild that are strikingly similar to what a NFT would resemble and it got me thinking: if Ordinals were possible on BTC, then NFTs must be possible on NoM too, right?

Check these out:
https://zenonhub.io/explorer/token/zts1t9ttvamu9zvczwz2t352x8
https://zenonhub.io/explorer/token/zts1xdrr952z5zmz5ea7cex0x4

Clearly someone's been thinking about it since May and even issued 2 ZTS', guessing that's @georgezgeorgez (as pointed out by @digitalSloth)

So today, I've acted on it and reached out to @digitalSloth to see if he'd be willing to add this feature in ZenonHub, since it already has most of the infrastructure in place.

To no surprise, as a true alien, he's happy to get onboard and I've offered to handle the discussions about how the standard should look like.

So for a ZTS to qualify as a NFT it would need to have the following properties:
- domain points to ipfs where the metadata and media are stored
- totalSupply = 1
- maxSupply = 1
- decimals = 0

This part is easy and inspired by the examples above.

Since the domain is pointing to ipfs, anything can be stored there in any format. But we need a standard format for apps and website to be able to read it and display the NFT's content correctly.

Before @digitalSloth can start implementing this feature into ZenonHub and other devs (@aliencoder @sol @vilkris) hopefully implement related features in syrius, we need to figure out what goes into that ipfs link.

We don't have to reinvent the wheel here, let's start by looking into how others are doing it already (eg.: Ethereum NFTs, Bitcoin Orginals)

For storage, I've found the following service used by OpenSea any many others:
https://nft.storage

LFG!!!

-------------------------

0x3639 | 2023-08-02 19:44:59 UTC | #2

I want my ballz on there.

-------------------------

sol | 2023-08-02 19:45:04 UTC | #3

There are several ways to inscribe data on NoM, each with their own tradeoffs.

While these are indeed non-fungible tokens, I would caution against this approach for large collections since you need to burn 1 ZNN per token.

In the future, the Zenon Asset Standard will be used to deploy an assortment of assets on NoM without this cost.

Until then, users are free to adapt the ZTS in unconventional ways to trade NFTs.
In fact, it's inevitable.

-------------------------

0x3639 | 2023-08-02 19:45:47 UTC | #4

I need a nut collection.

-------------------------

coinselor | 2023-08-02 19:54:39 UTC | #5

We better start minting them NoM NFTs when the minting fee is below $1 :laughing:

ipfs is ruggable right? Like I could mint a ZTS pointing to a ipfs URL and change what's stored in that address in the future?

-------------------------

0x3639 | 2023-08-02 20:02:37 UTC | #6

[quote="sol, post:3, topic:1571"]
While these are indeed non-fungible tokens, I would caution against this approach for large collections since you need to burn 1 ZNN per token.
[/quote]

If someone want to work with me on a nut collection, I'll front 100 znn to mint 100 sets of ballz.  It would be awesome to run this through the noun algo.  @sol let's do it!!!

What are the ballz characteristics???  Classic.  I refuse to act my age. 

https://nouns.wtf/

![image|470x500](upload://6sryOfbYIBVkQ0rSIyvGxYSZDGj.png)

-------------------------

dat_she_pepe | 2023-08-02 20:04:14 UTC | #7

I'd prefer having things onchain and not mimicking ETH on this question. Or stored on BTC. Maybe some thinking about Ordinals bridging could be interesting?

-------------------------

dat_she_pepe | 2023-08-02 20:04:38 UTC | #8

What make Nouns unique is their fully onchain nature though

-------------------------

dat_she_pepe | 2023-08-02 20:06:57 UTC | #9

To clarify I find kinda meh the idea of having an onchain object acting as an authenticity certificate pointing to a non onchain content. You just own a certificate. It's interesting but not really cool to me, personal opinion. Beside the BTC narrative is about Ordinals VS BTC with this kind of reflection about what NFTs are.

-------------------------

sol | 2023-08-02 20:08:34 UTC | #10

[quote="coinselor, post:5, topic:1571"]
ipfs is ruggable right?
[/quote]

I'm not certain of IPFS immutability and permanence.
Check out [this thread](https://www.reddit.com/r/ipfs/comments/u2hvmr/what_happens_to_the_content_when_i_stop_paying/) about pinning.

IMO the best options for those criteria are:
- Zenon (on-chain)
- Bitcoin (off-chain)
- Arweave (off-chain)

[quote="0x3639, post:6, topic:1571"]
If someone want to work with me
[/quote]

We need some sort of standard that indexers can use to validate (and maybe even authenticate) NFTs. We can look to other platforms for inspiration, like brc-20, src-20, xcp...

If anyone else wants to jump in and volunteer for this part, by all means. Otherwise, I can whip up a framework and tooling to generate collections.

-------------------------

dat_she_pepe | 2023-08-02 20:07:46 UTC | #11

I can make you pixel balls.

-------------------------

sumamu | 2023-08-02 20:08:47 UTC | #12

[quote="coinselor, post:5, topic:1571"]
ipfs is ruggable right? Like I could mint a ZTS pointing to a ipfs URL and change what’s stored in that address in the future?
[/quote]

There are immutable options too.

[quote="dat_she_pepe, post:7, topic:1571"]
Or stored on BTC
[/quote]

Bitcoin does benefit from having content stored onchain because the minter pays for storage fees.

However, in our case, it's more advantageous to store the content offchain.

-------------------------

dat_she_pepe | 2023-08-02 20:10:06 UTC | #13

Can a standard allow storing on IPFS and BTC, letting people decide what to do ? There must be way to retrieve BTC ordinals content through URLs or something. Storing on IPFS is really ETH ethos.

-------------------------

sumamu | 2023-08-02 20:09:38 UTC | #14

Technically, yes.

-------------------------

sol | 2023-08-02 20:09:57 UTC | #15

[quote="dat_she_pepe, post:13, topic:1571, full:true"]
Can a standard allow storing on IPFS and BTC, letting people decide what to do ?
[/quote]

Like I said here
[quote="sol, post:3, topic:1571"]
There are several ways to inscribe data on NoM, each with their own tradeoffs.
[/quote]

-------------------------

dat_she_pepe | 2023-08-02 20:10:29 UTC | #16

People could pay with plasma though.

-------------------------

dat_she_pepe | 2023-08-02 20:11:36 UTC | #17

This could be an opportunity to tackle on the Ordinal market and bring new users in rather than letting us having fun with NFTs in our own bubble. Bitcoin it.

-------------------------

sol | 2023-08-02 20:11:32 UTC | #18

[quote="dat_she_pepe, post:16, topic:1571, full:true"]
People could pay with plasma though.
[/quote]

Indeed, we must limit this capability. Once we start down this path, dynamic plasma will be required to keep the network stable.

-------------------------

sumamu | 2023-08-02 20:14:16 UTC | #19

[quote="sumamu, post:1, topic:1571"]
we need to figure out what goes into that ipfs link.
[/quote]

[quote="sumamu, post:1, topic:1571"]
a standard format for apps and website to be able to read it and display the NFT’s content correctly.
[/quote]

This is our mission here.

-------------------------

dat_she_pepe | 2023-08-02 20:18:27 UTC | #20

What would make the NFTs experience and nature unique on the NoM could be an interesting question. ETH NFTs on other chains pathetically failed to get any traction or interesting development, except for SOL at the bullrun peak.

(Here I am, your good old party pooper)

-------------------------

sol | 2023-08-02 20:23:20 UTC | #21

This is Counterparty, on NoM.

Check out their dispensers. I think we can do something similar.

-------------------------

sumamu | 2023-08-02 20:24:47 UTC | #22

[quote="sol, post:21, topic:1571"]
This is Counterparty, on NoM.
[/quote]

Where do I find it?

-------------------------

sol | 2023-08-02 20:26:10 UTC | #23

https://counterparty.io/

https://www.xchain.io/

-------------------------

sumamu | 2023-08-02 20:30:38 UTC | #24

[quote="sol, post:23, topic:1571"]
https://www.xchain.io/
[/quote]

I don't understand it yet, but I'm reading about it.

-------------------------

sol | 2023-08-02 20:42:39 UTC | #25

You don't need to know everything about XCP but 5-10 mins of research should be enough to understand what I mean.

Users can set a max supply greater than 1 if they want duplicates of the same token. I was surprised to see this is still a popular concept for Bitcoiners.

Ideas for collection sizes:
- max supply 1 per individual NFT (cost 1 ZNN)
- max supply >1 per individual NFT -- no longer "non-fungible" (cost 1 ZNN but your collection is much larger)


For distribution, collection owners can do any of the following:
- mint the max supply
   - distribute manually (p2p payment or free)
   - distribute automatically (airdrop)
- create the collection with a throwaway address (the dispenser) and configure a non-standard minting and distribution mechanism
  - the mint and distribution could be limited by a fee
  - this is what xchain does

-------------------------

aliencoder | 2023-08-03 12:36:01 UTC | #26

Additional resources:

- [Ordinal Theory](https://docs.ordinals.com/)
- [ORC-20](https://docs.orc20.org/)
- [ERC-721](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/)
- [ERC-1155](https://ethereum.org/en/developers/docs/standards/tokens/erc-1155/)

-------------------------

dat_she_pepe | 2023-08-03 12:56:25 UTC | #27

What is the goal, strategically, of mimicking an old protocol on the NoM? Would it bring more users? Is the tech they built relevant today and how? For which usecases? Which narrative does it help us market?

-------------------------

aliencoder | 2023-08-03 13:09:19 UTC | #28

Anything that will attract more users is worth pursuing. As a L1 network, one must be able to create non-fungible tokens. It's a requirement and we're here to define the spec.

-------------------------

sol | 2023-08-03 18:13:14 UTC | #29

[quote="aliencoder, post:28, topic:1571"]
we’re here to define the spec.
[/quote]

To be clear, this is the spec for one of potentially several NFT protocols on NoM that are limited by the constraints of ZTS.
ZAS isn't even part of this discussion.

[quote="dat_she_pepe, post:27, topic:1571"]
What is the goal
[/quote]

I'll say this should be seen more as an interesting, fun experiment. Maybe it gains user adoption over time, maybe not.

The XCP crowd thinks their protocol is still relevant and useful, so I'd say that beauty is in the eye of the beholder.

-------------------------

zyler9985 | 2023-08-03 14:48:08 UTC | #30

ETH itself is a scam because it's centralised garbage, and its NFTs are giga scams because you're just buying a reciept that points to some random place where the jpeg is actually stored. That jpeg can be rugged. The jpeg can also be screenshotted.

The only NFTs worthy of zenon's brand and ethos is on-chain storage/ decentralised storage and also steganography capacity with easy UX to have hidden signatures and things inside of it

If we copy ETH and make shitty NFTs ... not gonna help us win over hardcore bitcoiners. it'd be a misuse of the NoM and I don't think prominent people in our community should be advocating for this. do what you want, but that's my 2 cents.

-------------------------

0x3639 | 2023-08-03 16:23:15 UTC | #31

[quote="sol, post:29, topic:1571"]
I’ll say this should be seen more as an interesting, fun experiment. Maybe it gains user adoption over time, maybe not.
[/quote]

Agree.  IMO it's more about FAFO.  If we don't fuck around, we will never find out.  Let's try some stuff and have fun.

-------------------------

Stark | 2023-08-03 17:08:50 UTC | #32

I'm cooking. @sol please check dms on HC1.

-------------------------

sumamu | 2023-08-08 17:52:02 UTC | #33

[quote="aliencoder, post:26, topic:1571, full:true"]
Additional resources:

* [Ordinal Theory ](https://docs.ordinals.com/)
* [ORC-20](https://docs.orc20.org/)
* [ERC-721](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/)
* [ERC-1155](https://ethereum.org/en/developers/docs/standards/tokens/erc-1155/)
[/quote]

Thank you for the resources!

[quote="zyler9985, post:30, topic:1571"]
The only NFTs worthy of zenon’s brand and ethos is on-chain storage/ decentralised storage and also steganography capacity with easy UX to have hidden signatures and things inside of it
[/quote]

Storing data onchain is advantageous for Bitcoin, because fees are paid based on how much data is included in the transaction.

Unlike Bitcoin, NoM fees are limited to 1 ZNN. Also, the stored data is limited to ~17kb on NoM, which is rather low.

[quote="aliencoder, post:28, topic:1571, full:true"]
Anything that will attract more users is worth pursuing. As a L1 network, one must be able to create non-fungible tokens. It’s a requirement and we’re here to define the spec.
[/quote]

NFTs are already possible on NoM, but right now they're not referencing any data (images, videos).

[quote="sol, post:29, topic:1571"]
I’ll say this should be seen more as an interesting, fun experiment. Maybe it gains user adoption over time, maybe not.
[/quote]

Yes, that's pretty much the purpose here, doing something fun. Down the road we could migrate to NFTs storing the data onchain.

-------------------------

dat_she_pepe | 2023-08-09 00:23:22 UTC | #34

We should be something fun BUT that makes sense VS the NoM. Not copying ETH NFTs.

-------------------------

romeo | 2023-08-10 08:45:17 UTC | #35

Copying Eth's NFTs isn't a bad thing, particularly because we could mint and transact them without fee's

It's also the most popular NFT standard by far - and would tie in nicely with web3 and games

I don't see why we can pursue more than 1 solution in the short and long term

-------------------------

Stark | 2023-08-10 18:52:24 UTC | #36

I don't necessarily "like" it, but what you have spoken, is the truth.

-------------------------

dat_she_pepe | 2023-08-10 20:31:12 UTC | #37

Nobody cares about fee when it comes to NFTs. Let's see beyond that. Don't go the easy way. How did SOL NFTs work and are they still interesting now ? Rethorical question, there's no volume to be seen. On ETH there is still activity. Why? Fee doesn't matter.

-------------------------

cryptocheshire | 2023-08-10 21:57:37 UTC | #38

![image|268x200](upload://8vtgIRUmQj4iWAKy9IZq2uaKlBX.jpeg)

-------------------------

coinselor | 2023-08-10 23:26:00 UTC | #39

Seems to me decentralization might be top-of-mind for a lot of NFT holders, otherwise why is there a slight trend of ETH NFTs being converted to ordinals/brc20's? Clearly, fees are not the reason, lol. A lot of this ETH centralization FUD might be working.

We can leverage that ETH NFT exodus and be like: why go to BTC for NFTs when there is a better alternative? We got cool tech that improves decentralization and scalability over time, plus we are feeless and can provide smart contract capabilities, join the cool-looking aliens and forget about moving your NFTs ever again.

-------------------------

romeo | 2023-08-11 11:46:29 UTC | #40

of course fees matter - activity doesn't equal happiness with the situation, merely acceptance likely due to lack of comparable/convenient alternatives

Like I said, if we can get Eth style NFTs up and running quickly and pain free it's a no brainer to me. Aspirational endeavors can still be worked on in unison and be delivered down the line

-------------------------

aliencoder | 2023-08-11 15:24:01 UTC | #41

Look. If we're doing nothing, we're going nowhere. Simple as that. Too much debate means less actual work.

-------------------------

zyler9985 | 2023-08-11 16:11:23 UTC | #42

The Plan:
1) Teaser NFTs: Do some ETH style NFTs, because it's a clown market anyway and it might help get more clown users to join
2) Hardcore NFTs: Make it clear we are also eventually working on NFTs actually worthy of our brand; that is to say, doing everything better than ETH does. This could mean decentralised storage solutions or steganography etc. 

At minimum, even our Teaser style ones are superior in that they are feeless, decentralised and secure.

-------------------------

cryptocheshire | 2023-08-11 17:09:02 UTC | #43

Tezos, Algorand and so many others had that too at marginal fees, yet nobody cares or uses it.

-------------------------

dat_she_pepe | 2023-08-12 13:12:43 UTC | #44

Ok ok. Let's make NFTs A. And let's make NFTs B. A represents shares of smart contracts on the ext chain. B are jpegs or whatever. Allow users to add IPFS images they bought as B to their A NFTs. Bam. DeFi with cartoons. Anime DeFi. The smart contract war. Own the ecosystem. Bam Bam says bam.

-------------------------

dat_she_pepe | 2023-08-15 21:29:48 UTC | #45

![Screenshot_2023-08-15-23-29-26-95_0b2fce7a16bf2b728d6ffa28c8d60efb|223x500](upload://wsIRt4jbvGHb280IBM6PF4OCQOY.jpeg)

-------------------------

tapwoot | 2023-08-17 11:20:45 UTC | #46

I made 50 teaser NFTs ready to deploy, problem is how do I distribute them?
![image|690x173](upload://a0De4dVUCkGgbk2xwIidcxXt7Zq.jpeg)
![image|690x169](upload://utKqCypFQzcWaC3plLPcEggZeAs.jpeg)

-------------------------

zyler9985 | 2023-08-17 11:28:00 UTC | #47

Yas king!!! Well, I'd like to make a claim on one which has a prominent bulge below his extraterrestrial belt. Unless you gifted them like how hewwo marketed his lone aliens? Have competition for it.

-------------------------

tapwoot | 2023-08-17 11:32:06 UTC | #48

lol ok sure this one has a third leg its yours ![artbreeder-image (50)|500x500](upload://k2WzJH2ZArlPnnGWVqeuAJrDwGV.jpeg)

-------------------------

zyler9985 | 2023-08-17 11:34:16 UTC | #49

CLAIMED. If anyone screenshots this ill be calling local law enforcement.

-------------------------

0x3639 | 2023-08-17 11:50:53 UTC | #50

do stuff to help the project to earn them??

-------------------------

sol | 2023-08-17 12:52:29 UTC | #51

How do you want to distribute them? 
Where do you want to issue them?

I don't have any tools to facilitate these actions on NoM yet, but I may be able to help you.

-------------------------

tapwoot | 2023-08-17 18:00:06 UTC | #52

I will use the pre-existing tools after you work through some of the kinks with others first

-------------------------

0x3639 | 2023-08-17 18:10:52 UTC | #53

do any of them have alien ballz?

-------------------------

0x3639 | 2023-08-17 18:19:17 UTC | #54

![IMG_6129|501x500](upload://5VHJKDIEyCSpTdrhRxWHZVvXV6k.jpeg)

-------------------------

TThanos | 2023-08-17 19:49:09 UTC | #55

Give me the one with the big alien cock plz

-------------------------

dat_she_pepe | 2023-08-18 10:26:22 UTC | #56

Can you give me the one you think fits my gentleness ser?

-------------------------

angelo_a_jr | 2023-08-18 19:12:30 UTC | #57

This would be a great collection to get on NoM instead of Ordinals. https://twitter.com/TheDevsNFT/status/1690106975617482752?s=20

@sumamu did you mention the bridge should theoretically work for ERC721s?

-------------------------

sumamu | 2023-10-10 13:35:03 UTC | #58

[quote="angelo_a_jr, post:57, topic:1571"]
@sumamu did you mention the bridge should theoretically work for ERC721s?
[/quote]

Yes, it should. We should first have an NFT standard on NoM before attempting to bridge other NFTs over.

-------------------------

DyDDy | 2024-02-20 23:46:39 UTC | #59

willing to support in any way possible to make this happen - whether its ZNN payment or art please hit me up

-------------------------

DyDDy | 2024-02-20 23:49:20 UTC | #60

on the same topic, having a separate tab that could identify ZTS tokens with a link attached to them to display potential PFP's would be a good way to get integrated support for viewing the NFTs you own.

-------------------------

baggot | 2024-02-28 20:30:04 UTC | #61

can i has? am dewegated to tapwoot pweeze reward wiff awien nft

-------------------------

baggot | 2024-02-28 20:29:46 UTC | #62

i literally came up with this entire idea ages ago. nobody listened to lil ol baggy

-------------------------

tapwoot | 2024-04-01 16:19:08 UTC | #63

ok bro, feeling bloated

-------------------------

DyDDy | 2024-04-20 22:44:01 UTC | #64

just checkin in on this progress.

please again reach out to me for anything needed

-------------------------

SugoiBTC | 2024-04-21 00:02:18 UTC | #65

Hey man, yeah! We're getting closer. So the Supernova testnet is live and we should be able to start on it.

Follow the discussion here: https://forum.hypercore.one/t/supernova-zapps/437/6?u=sugoibtc
![image|598x500](upload://zVnygiYieDMjxwFMvFw4GvniSMK.png)

-------------------------

DyDDy | 2024-04-26 11:41:25 UTC | #66

this is good news. 

I actually came here to suggest putting Cryto Hales into Ordinals (pretty cheap inscription fee since the art is 24x24) to try to give more exposure to ZNN as a marketing strategy, but it seems people want the Hales on NoM respectfully so I'll continue to wait.

-------------------------

baggot | 2024-04-29 03:16:28 UTC | #67

ordinal hales sound based and greenpilled and exposes the broaded ordinal community to NoM

-------------------------

cryptocheshire | 2024-05-04 21:29:05 UTC | #68

You could launch them as ordinals and mirrored on NoM later

-------------------------

