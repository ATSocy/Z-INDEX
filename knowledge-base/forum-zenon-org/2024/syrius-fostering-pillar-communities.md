Thread: syrius-fostering-pillar-communities
sol | 2023-02-08 22:34:54 UTC | #1

I want to start a thread where we discuss the possibility of fostering Pillar-centric communities that are accessible to all participants in the network.

The idea is to encourage pillar-delegate interactions by reducing any friction around accessing communication channels. 
The common ground we all have is the network and desktop wallet; why not leverage those to enable bi-directional communication with pillars?

Think of a Telegram or Discord channel:
- users read/write messages
- users can react to other messages
- users can submit/respond to polls
- users can have handles/profiles

> **Pillar-centric social media\*, hosted on NoM, accessible via Syrius.**

I envision two ways to achieve this objective: 
1. an embedded smart contract could facilitate the tracking of all messages and interactions
    - a spork will be required
    - rules can be enforced, such as:
         - only active delegators have the ability to submit interactions
         - messages have a character limit
2. delegates and pillars can craft transactions that contain messages in the `data` field and send them to the pillar
    - a spork is not required
    - may be more challenging to parse the entire interaction history as the network evolves
    - anyone can submit interactions to a pillar community

Some community members could cache the interactions on their own infrastructure to make these accessible for others to read.

\* I think any non-text content will have to be hosted off-chain.

Other considerations:
1. https://t.me/zenonnetwork/266443
2. https://forum2.zenon.org/t/secret-messages-poc/1183
3. ![image|620x332, 50%](upload://aHqJSFpWz4aWcEYvwS4IKZlDmlv.png)

----
I would like to hear the community's thoughts about this. 
Suggestions and criticism are welcome. :)

-------------------------

DrD3 | 2023-01-30 20:37:57 UTC | #2

I like the idea of maintaining pillar channels where delegators can communicate with their Pillar (and vice-versa) within Syrius itself. Currently, 0x has a rocketchat for his delegators where they first gotta verify themselves with their delegating address and through signing a message using Syrius. Only the most devout of deeznnuts delegator's have joined this chat- something that'll only exacerbate as NoM grows larger.

I like the first option though that sounds like more work for you haha. 

For the second alternative- would the crafting of transactions that contain messages require plasma to be fused by the user?

-------------------------

sol | 2023-01-30 20:42:02 UTC | #3

[quote="DrD3, post:2, topic:1210"]
I like the first option though that sounds like more work for you
[/quote]
More work but probably a better result.

[quote="DrD3, post:2, topic:1210"]
would the crafting of transactions that contain messages require plasma to be fused by the user?
[/quote]
Plasma is required for all transactions, and even more than usual for any that include additional data.
Users can fuse QSR or do PoW, it doesn't matter.

-------------------------

DrD3 | 2023-01-30 20:45:54 UTC | #4

Will an embedded smart contract then free the user(s) from having to fuse QSR or perform a PoW?

-------------------------

aliencoder | 2023-01-30 21:03:34 UTC | #5

I like the idea and I would add the possibility of Pillars "sponsoring" projects that add value for the ecosystem beyond Accelerator-Z.

This process would be frictionless (e.g. no voting process, etc.) and will enable smaller contributors to engage and create value in the ecosystem. 

If contributors get rewarded faster for their work, they will remain in the community and potentially pursue more complex projects as the ecosystem expands.

-------------------------

sol | 2023-01-30 21:00:50 UTC | #6

No, I think those requirements will be roughly the same for both options I've proposed.

-------------------------

0x3639 | 2023-01-30 22:39:09 UTC | #7

I think this is a really good idea.  As we upgrade the network we need a way to communicate and coordinate with Pillars.  I like Option 1, but I do think we need to be careful embedding lots of smart contracts.  It could increase the attack surface and/or Pillars could get fatigue upgrading the node software. But embedding a SC that helps coordinate activities seems like a good reason to spork.  Maybe in the future this could move to the VM layer.

-------------------------

sol | 2023-01-30 22:44:08 UTC | #8

Valid concern. Perhaps this should wait until after unikernel integration. :thinking:

-------------------------

ZNNAYIID | 2023-01-31 09:45:59 UTC | #9

I agree with 0x, I also have some concerns regarding having embedded sc just for Pillars-Delegators communication, while we still have other high priority protocol upgrades that are worth developing and having their own embedded sc.

-------------------------

