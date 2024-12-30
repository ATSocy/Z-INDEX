Thread: welcome-to-the-multiverse-bridging-the-zenon-ecosystem
sumamu | 2022-08-11 18:36:55 UTC | #1

This article has been in the writing for some time and we approached it by asking ourselves questions that we though a community member would have asked in the first place. Below you will find a list with those questions. There's a lot of information, so you can skip to the ones that spark your interest if you want a quick read.

## Who are you?
We are a team of rockstar engineers that tackle complex software projects and strive to deliver comprehensive solutions.

## Are you part of the community?
If you want us to take you to our leader, then that’s sumamu.

## How did you find out about Zenon?
While looking to fund our work on similar projects by reaching out to other cryptocurrency communities such as Thorchain, we found out about Zenon's Accelerator-Z funding program and started learning more about it. We decided to participate into the Hyperspace program that has a specific call to action for interoperability solutions.

## What did you like about Zenon?
It gives us the opportunity to build on a promising network, while being rewarded for our efforts.

## Why are you building on Zenon?
We've been working with similar tech before and we believe Zenon has huge growth potential in the  mid and long-run.

## What are you building on Zenon?
Basically a full-stack cross-chain solution that will enable the flow of assets between Zenon and other blockchains.

## What will the bridge do?
The bridge will be based on a lock-and-release mechanism that will allow users to transfer assets to and from Zenon (swap ZNN to wrapped ZNN on other chains and vice-versa).

## How are you building it?
By coding it, of  course. But before that, there's a lot of research that we've done and a lot more still to be done.

We've delegated members of our team for the following tasks: researching existing bridging solutions, learning their faults, assessing their limitations, learning the go-zenon codebase, and also keeping in touch with the community (we know, that can be improved).

With what we've learned so far, we're able to give you some of the details that we're fairly certain of.

**The bridge will have the following components:**
### 1. Bridge Embedded Contract
A new embedded contract is needed  in order to allow the secure storage of funds. Our first approach was creating a Zenon address based on a EdDSA pubkey, which we successfully accomplished (including all the necessary unit testing). This work was not in vain since it will later enable us to develop custom multisig tech compatible with Zenon. However upon further research, better ways to design the bridge architecture have been discovered: via the embedded contracts. Although it will be a challenge to get them included into go-zenon, we are confident that the community will support us in this endeavor.

### 2. EVM Contracts
EVM blockchains will store the funds in smart contracts. To swap assets to Zenon, users will simply need to send them to the smart contract specifying the Zenon address where the funds will be released to. Users will also be able to redeem funds by providing a valid TSS signature when calling the smart contract.

### 3. The TSS module
TSS is state-of-the-art cryptography that enables distributing access to an address between multiple parties. Just like multisig, TSS allows signing a message with a threshold of M out of N, but unlike multisig addresses, it looks and behaves much like a regular address. This also means that no information about the co-signers is published on-chain.

### 4. The bridge participants
The participating nodes will provide the infrastructure needed to run the bridge components. They will be running the bridge logic, the go-zenon node (znnd) and the corresponding nodes for each supported network (geth for ETH/BNB Smart Chain, bitcoind for BTC, etc). They will also store and secure the secret shares used to generate the TSS pubkeys.

## What about security?
We are aware of the exploits happening right now in the cross-chain bridges space. That’s exactly why we will employ a multi-layered security approach and we'll get into the details in a dedicated post. One security layer that we’re testing is an innovative delay mechanism, which will allow additional security measures to kick-in and halt operations if abnormal activity is detected.

## Will the bridge be audited?
Internal audits will be the first ones to be performed. The community will also have the opportunity to audit the entire code and efforts will be made to engage external parties to perform extensive security audits after the code is open sourced.


## What blockchains will the bridge support?
The architecture is designed with support for EVM chains such as Ethereum, BNB Smart Chain and at a later time it will be possible to offer support for Bitcoin.

## What assets will be supported?
Any ERC-20/BEP-20 token can be integrated as long as a ZTS counterpart exists. Supporting wZNN and later on wQSR is the primary objective.

## Who will be able to participate?
The first iteration will run on Pillars, since they already fulfill most of the requirements for running the entire stack and are most invested into the ecosystem. For the next iteration we are taking into consideration running the entire stack on Sentinels, since there's already an incentivization mechanism present, and that mechanism can be used to incentivize bridge participants.

## What about fees?
There will be fees as they are necessary for preventing spam and as a way to incentivize nodes participating in the bridge.

## How will participants be incentivized?
During the first iteration, participants will be incentivized via fees. In the next iteration rewards will be distributed based on participation.

## What is the current status of the project?
There wasn't much public activity on this topic, but internally we've been very busy. At this point we've been able to fulfill all technical requirements for on-ramp and off-ramp.

## How will users be able to interact with the bridge?
Users will be able to interact with the bridge using any means accessible to them. Most users will likely use Web3 apps, since these are already being developed. At a later time, more ways to interact with the bridge will become available. Ideally the bridge will also be directly integrated into the Syrius wallets.

## Where can I test it?
All testing is currently being performed internally. As we make additional progress we'll also be looking into ways to open public beta testing.

## When will the bridge open?
We're expecting to be able to deliver publicly accessible infrastructure by November.

## How will you integrate the bridge with go-zenon?
We’ll leverage the already present spork system and create a pull request for the project.

## When will it be ready?
By the end of the year, but even earlier if everything goes as expected.

## How much will it cost?
It's difficult to make an estimation at this point, but one thing is for sure: it will be outweighed by the amount of time and energy required by this kind of project (in terms of complexity) and the value that it will provide to the entire ecosystem both in the short and long term. We'll be posting updates as we make progress and follow-up milestones with Accelerator projects to cover R&D costs. Starting with this post we'll also be creating the first A-Z project and phase for covering the research we've done so far.

## What do you intend to do with the funds?
We intend to become a major contributor to the ecosystem and use most of the funds to establish our presence into the network.

## Will you develop other projects?
We'll assess the needs of the ecosystem together with the community and do our best to deliver where our skills meet the demand.

We understand that taking the time to read this post means you are also part of the ecosystem and/or interested in growing it, so we invite you to follow the progress and support our efforts.

-------------------------

0x3639 | 2022-08-11 18:26:48 UTC | #3

LETS FUCKING GO!!!  This is really exciting to read.  I'm happy to help with any and all testing.

-------------------------

ZNNAYIID | 2022-08-11 18:31:20 UTC | #4

This is awesome! I’m not so tech savy but my only concern is the fees system, I know it’s meant to prevent spamming and incentives nodes participants, but since the NoM is known for its feeless feature, it would be ideal to have this feature on our crosschain solution, is it possible to make the bridge feeless while preventing spam?

-------------------------

Zashounet | 2022-08-11 18:34:46 UTC | #5

Brillant! Can’t wait to test it

-------------------------

sumamu | 2022-08-11 19:10:13 UTC | #6

The fees are most useful for spam prevention when swapping from NoM (which is feeless by design) to other chains. So the other way around could be feeless. 

However, when it comes to incentivizing the nodes that participate in the bridge, it's too early to tell how much will be enough to cover the costs and also maintain interest.

Switching from Pillars to Sentinels could be the move that enables the bridge to be completely feeless.

-------------------------

Dumeril | 2022-08-11 19:22:24 UTC | #7

Sounds great! Looking forward to learn more about it.

-------------------------

coinselor | 2022-08-11 19:23:01 UTC | #8

Welcome to our community, grandiose entrance, way to go. Looking forward to eating Chankonabe with sumamu in space sometime ;)

I'm particularly looking forward to the TSS implementation as a fundamental building block that allows other applications to be built on top of NoM with a higher degree of security and decentralization.

Just read a [medium](https://medium.com/zengo/threshold-signatures-private-key-the-next-generation-f27b30793b) to inform myself in the fundamental differences between multisig and tss.

-------------------------

kw1da1 | 2022-08-11 20:07:23 UTC | #9

Welcome to the community

-------------------------

romeo | 2022-08-11 23:20:14 UTC | #10

Worth noting the core team set the precedent for submitting multiple AZ proposals if the current max (5000znn) grant isn't sufficient for the work being undertaken

-------------------------

sumamu | 2022-08-12 08:31:08 UTC | #11

Thank you all for the warm welcome!

-------------------------

shaimo | 2022-09-02 22:21:18 UTC | #12

Who creates and owns the wrapped token contract on the EVM side? With wZNN/BSC it is the Zenon team. But if the team is not involved in the new bridge(s) then who owns it?
Also, how do we manage the minting and burning of the wrapped tokens on the EVM chain side? Today this is done either centrally (eg in wZNN/BSC, and also on bridges such as chainport) or by a smartcontract (which often leads to these terrible hacks which we saw happening again and again).

-------------------------

Phuong | 2022-09-03 08:24:04 UTC | #13

Good questions, especially with regard to avoiding hacks.

-------------------------

0x3639 | 2022-09-03 21:45:41 UTC | #14

Sir, would you be willing to have a twitter spaces to discuss your AZ Proposal?

-------------------------

cryptocheshire | 2022-09-03 21:50:23 UTC | #15

Great idea

-------------------------

0x3639 | 2022-09-05 21:15:21 UTC | #16

@sumamu can we have you join a twitter spaces for the community to ask some questions?  Or a scheduled TG chat?

-------------------------

cryptocheshire | 2022-09-07 07:35:23 UTC | #17

@sumamu any chance you can address the following thoughts shared by another member? 

"So the only details we have from the bridge proposal are that it will use TSS and that pillars will run it first, then maybe sentinels.

How does a bridge work? Someone has to run a node for the other blockchain. And watch for transactions there. Are all pillars/sentinels going to run a node for every bridged network? If not all of them, then which ones? This determines how many people have to sign for the threshold signature.

The proposal kinda seems to want to blindly copy the Thorchain model. But Thorchain is a purpose built chain for swaps with the RUNE token providing cryptoeconomic security and incentives.

The proposal suggests that people are going to want to run the nodes for other networks without providing any information about what incentives will exist to run them."

-------------------------

sumamu | 2022-09-07 09:08:05 UTC | #18

Wow, there's lot of activity here. I've been watching this thread for a few days after the initial post, but there wasn't anything new, so I stopped refreshing it so often. I guess the extra exposure and awareness generated by Accelerator-Z have drawn more [spoiler]people[/spoiler] alienz here.

-------------------------

sumamu | 2022-09-07 09:57:58 UTC | #19

Well, there are 2 mechanisms that can be used:
A. lock and release
B. burn and mint

Mechanism A is used when the EVM side of the bridge doesn't have minting privileges for the token.
Mechanism B is used when the EVM side of the bridge DOES have minting privileges for the token.

In case of a vulnerability, both mechanism are affected. The main difference is that in case of mechanism A, the damage is limited by the amount of tokens locked in the EVM bridge contracts.

In the case of bridging a ZTS to ERC, which applies to both ZNN and QSR, if the EVM bridge is unable to mint the ZTS' counterpart on the EVM side, then bridge's usability is limited by the token's circulating supply on that specific EVM network, which can cause a complete halt of that ZTS' ability to be bridged to a specific EVM network.

Therefore, mechanism B would be more appropriate for ZTS', meaning that the EVM bridge should have minting privileges for the ERC okens that only existed as ZTS' before being bridged.

Pretty much the same applies for ERC tokens that didn't have a ZTS counterpart before being bridged.

In conclusion, in the case of any token (ZTS of ERC), that didn't have a counterpart on the other side, unless there is a third party making sure the bridge has enough liquidity, then the bridge should have minting privileges (mechanism B). 

The issues you are concerned with actually rise from the lack of other security measures (which are considered in the bridge's design already), not from the the choice of using one mechanism or the other.

-------------------------

sumamu | 2022-09-07 10:01:38 UTC | #20

This forum is a great place for discussions because it's well organized and the content will remain easily accessible for anyone interested in the topic.

-------------------------

sumamu | 2022-09-07 10:28:10 UTC | #21

> How does a bridge work? Someone has to run a node for the other blockchain. And watch for transactions there. Are all pillars/sentinels going to run a node for every bridged network? If not all of them, then which ones? This determines how many people have to sign for the threshold signature.

Like any other bridge, it lets users transfer assets across chains. Yes, node operators will need to provide a full node/light node/3rd party node for every other bridged network. It will be run by Pillars at first because they are the most invested in the network, they most likely have the technical skills necessary to participate in the bridge. They also likely understand the value this bridge can bring to the ecosystem and have the potential to benefit from it. Any active pillar that produces momentums will be able to become a bridge participant. A minimum number of pillars is to be set in order to ensure a higher degree of decentralization and security. The threshold will likely be 2/3 of the participants. 
___

> The proposal kinda seems to want to blindly copy the Thorchain model. But Thorchain is a purpose built chain for swaps with the RUNE token providing cryptoeconomic security and incentives.

The same TSS technology is used, however pretty much everything else is different. Just like you said, Thorchain is a purpose build chain for swaps, which provides cross-chain native swaps. That's the main reason it needs liquidity to run and a very delicate system to secure that TVL. This bridge's main objective is to allow the bridging of ZTS' to ERCs and the other way around, which requires a fraction of Thorchain's TVL.
___

> The proposal suggests that people are going to want to run the nodes for other networks without providing any information about what incentives will exist to run them."

Participants will be incentivized using the fees at first. There is also the Orbital program which could provide a source of incentives. However, in the next phase we'll be looking into how Sentinels could become bridge participants and how the current incentives model can be changed in order to reward those Sentinels who are active and hones bridge participants.

-------------------------

romeo | 2022-09-07 11:18:13 UTC | #22

Are you able to provide a break down of the high level tasks to completion, and how many AZ submissions/phases you anticipate you will need?

Would love to see this proposal get up

-------------------------

sumamu | 2022-09-07 12:16:24 UTC | #23

It's difficult to answer this because the price keeps going down and the costs keep going up. Honestly we stopped looking at the hours we're putting in because it was becoming a bit disturbing. Like it seemed irrational to keep doing things.

-------------------------

cryptocheshire | 2022-09-07 12:25:48 UTC | #24

Imo for such a critical piece of infra its fair to ask for multiple grants à 5k ZNN / 50k QSR, especially at these prices. 

I guess what the community would appreciate is to get a rough understanding for how many of these full grants you're gonna ask. 

Maybe it could make sense to say e.g. 2 for the first bridge implementation, and then maybe 1 for the next 2 additional bridges, and 0.5 for every subsequent ones. Up to you to define what would feel "fair" for you guys considering what counts are solutions rather than hours. 

This would allow the community to give you grants for clear deliverables instead of work in progress.

Just an idea

-------------------------

sumamu | 2022-09-07 12:35:48 UTC | #25

There will certainly be clear deliverables starting with the next phase.

-------------------------

cryptocheshire | 2022-09-07 12:46:53 UTC | #26

Can you already post a list? This would help lobby for your current AZ proposal

-------------------------

0x3639 | 2022-09-07 14:42:40 UTC | #27

Sir, my question is similar to @cryptocheshire's in that I'm just wondering how many phases we can expect and the approximate timeframe.  I know that is hard to predict now.  But we had a wallet project presented, approved, completed, and funded without a clear path to full completion.  The wallet needs multiple full submissions, but that was not 100% clear initially.

Maybe as Shazz discussed, you can break things into 2 to 4 milestones that could fit nicely into AZ submissions.  Just a 30,000' roadmap in a few words each. 

Are you involved with THORchain in any way?  

How many bridges have you developed?

Thank you sir for you submission and time!

-------------------------

sumamu | 2022-09-08 16:20:11 UTC | #28

We're still in discovery mode with the roadmap and the deliverables, but we're hoping to clarify most of them this month. As soon as we have more to share we're going to publish an update.

-------------------------

0x3639 | 2022-09-08 16:31:02 UTC | #29

OK.  I will vote yes on this proposal.  Just please understand that we are sensitive to developers requesting funds for projects that do not have a clear path to deliver the entire project.

thank you!

-------------------------

sumamu | 2022-09-08 17:29:27 UTC | #30

Like you should. 
Thank you for your vote!

-------------------------

dat_she_pepe | 2022-09-08 18:08:26 UTC | #31

I voted yes because of your pfp

-------------------------

coinselor | 2022-09-09 01:33:42 UTC | #32

Actually fair game. A nicely branded anon dev probably delivers a nicely branded cross-chain bridge.

-------------------------

bytecode | 2022-10-22 13:07:53 UTC | #33

Sounds very promising, hopefully this project sees fruition. If you need testers i'll gladly QA it.

-------------------------

sumamu | 2022-10-27 14:25:53 UTC | #34

Hello Aliens,

Reporting to the Mothership: 
I'm excited to announce that the Multiverse project is hitting an important milestone: the release of the open beta.

The community is invited to test the bridge that is currently setup to support bidirectional swaps between Zenon Testnet and Ethereum's Goerli Testnet.

For more transparency requested by community members, I've also compiled a short FAQ regarding the current status of the project.

How can I test the bridge?
Thanks to @dexZNNter, the bridge frontend is available here:
https://bridge.testnet.zenon.community

Where can I get tokens to test it?
You can get testnet tokens from the following sources:

Zenon Public Testnet faucet: 
@znn_faucet_bot

ETH Goerli faucet: 
https://faucetlink.to/goerli

Where can I report an issue?
You can report issues in this thread.

What about the security of this bridge?
The bridge is designed with a multi-layer security architecture in mind and additional security modules for the bridge are currently in development. Although we make huge efforts, there are always ways to enhance the security. We will perform internal security reviews, but an external security audit should be conducted before the official launch. The bridge has 3 main components that will require to be audited: the Solidity smart contracts, the core module and the Zenon embedded contract.

What else can I do to help?
Beside testing it, spreading the word about this project beyond Zenon's community is also equally important. In this way, other projects can hear about it and provide additional support.

Please consider that this project is still under heavy development, so expect things to break and kindly report only valid and reproducible issues.

We will keep you updated with the progress. 
Buckle up for the official launch!

-------------------------

0x3639 | 2022-10-27 18:49:36 UTC | #35

Brave Browser, Ubuntu 22.04

Refreshed 3x.  It finally worked.  I was not able to inspect fast enough to see any issues.

My computer is doing PoW to get more test ETH, so that could be the issue.

![image|563x500](upload://uWv0ykNtxv9lC57AOdMRHLeLPvG.png)

-------------------------

0x3639 | 2022-10-27 18:51:41 UTC | #36

How long does it normally take to do the bridge?  Does the computer need to do PoW to complete the TX?

![image|577x499](upload://2xCdjSYFgdCcbHFMMLt4uTTEjyf.jpeg)

-------------------------

0x3639 | 2022-10-27 18:59:55 UTC | #37

On first attempt, the bridge worked exactly as expected.  I need more testETH.  Will keep playing with it and report back.  

![image|425x499](upload://myBHfNcGJXjDWkE7zOQueQHOTzH.jpeg)

-------------------------

0x3639 | 2022-10-28 00:30:16 UTC | #39

what is happening when it says "Signing"

![image|690x409](upload://nba8rklhCJ7anmlMa8Qr7BdlnG0.jpeg)

-------------------------

0x3639 | 2022-10-28 00:38:11 UTC | #40

I wonder if we can improve the appearance of this page.  The transaction looks strange in that window.


![image|268x500](upload://hjuTXRiRHK5hq08QlwkWvnkTR04.png)

-------------------------

0x3639 | 2022-10-28 00:43:02 UTC | #41

I tried to unwrap wZNN to ZNN.  While the "Signing" process was taking place (to unwrap the token), I tried to wrap ZNN to wZNN.  That seemed to remove the Unwrap Request all together and execute the ZNN to wZNN request only. 

After making the request to Unwrap the wZNN

![image|690x409](upload://6nSs2QFJcmknuKqOdkC6GaDmbPU.jpeg)

After making the request to wrap ZNN to wZNN

![image|666x500](upload://gygTBU68GEnTXO8rhxyFWVhwLsV.jpeg)

After 90 seconds or so this reappeared

![image|690x423](upload://sBWAVMehSyyyO8PzfQYqjORkW8F.jpeg)

Is this behavior expected?

-------------------------

0x3639 | 2022-10-28 09:56:40 UTC | #42

I just converted wZNN to ZNN

![image|462x500](upload://b7JyWsDuOSVGgSGu2MJwDZGvyJA.jpeg)
https://goerli.etherscan.io/tx/0x492d2343c29705c968cf05a5900cb1dc7769f8304e5063bf95ddcca954469aa7

![image|380x500](upload://a5WPXqoql8b3F89raI1uLcqKPqy.png)
https://explorer.zenon.org/transaction/7261bb455a94be35c768bce722b43bc09a5f5ab3d1fe44f7b13037cfdcb18258

The wZNN was removed from my wallet and hit syrius, but it's still showing up as a redeemable asset a few minutes after the tx in the bridge

![image|690x402](upload://3aOsBKs8drOZiY9czbSiNvg4hyq.jpeg)

I tried to redeem the 69 a second time (an attempted double redeem) and now  syrius is stuck "Sending" the TX for a few minutes.  I will let it run to see if it times out.  

![image|690x346](upload://tdCKfvDHeOf7EAVS5SCpOjvwsdz.jpeg)

-------------------------

0x3639 | 2022-10-28 01:44:15 UTC | #43

Notice the addresses for ZNN and wZNN in the image.  They look reversed.  

![image|462x500](upload://5kAwN5Ncz6sDxNsbr0j7zFq5twM.jpeg)

-------------------------

CryptoFish | 2022-11-04 08:36:20 UTC | #44

Below are a couple of issues I noticed when entering a ZNN amount for a new swap to WZNN.

**Issue 1**
Waiting for approval from extension stays when the approval is declined.

**Issue 2**
Entering a ZNN amount with more than 8 decimals causes the approval not to appear and the website stays waiting for approval from extension.

**Issue 3**
Sometimes the approval popup just opens up the Zenon Wallet but not showing the tx to approve. I haven't been able to reproduce the exact conditions that causes the issue.

**Issue 4**
When choosing "Existing swap" there is no way to start a "New swap". You have to refresh the page and go through the approvals, reconnect the wallets to be able to choose a new swap.

-------------------------

DrD3 | 2022-11-02 17:48:30 UTC | #45

Hey @sumamu bumped into a slight problem while tryna play with the TestNet bridge. I managed to install version 0.1.2 of Dexter's browser extension and create a wallet. Following this I texted /faucet alongide my addy to @znn_faucet_bot and received the following confirmation.

![Screenshot 2022-11-02 at 6.35.17 PM|690x355](upload://4fHt2QYZsfv4lZ9o7C8ZPD0WxiY.png)

However, I still haven't received any of the test znn & qsr. I also attempted to create a new wallet and texted the bot through another tg account to no avail.

-------------------------

DrD3 | 2022-11-03 08:27:23 UTC | #46

I also got @0x3639 to send my test wallet some znn & qsr 
![Screenshot 2022-11-03 at 9.22.04 AM|335x499](upload://3jgHMPCXQ4Saj1w47yZcZqEpBUr.jpeg)

but my wallet is still empty. 
![Screenshot 2022-11-03 at 9.24.01 AM|301x500](upload://pSj1cPZTUg4XJrCon1zlxrNB2GO.png)

I attempted switching my browser from Brave to Chrome and also attempted installing Alpha version 0.1.1 but I can't see any znn/qsr sent from 0x or from the faucet bot.

-------------------------

0x3639 | 2022-11-03 08:48:07 UTC | #47

is your wallet using the correct testnet node?  it should be on

wss://syrius-testnet.zenon.community:35998

-------------------------

DrD3 | 2022-11-03 12:11:15 UTC | #48

[quote="0x3639, post:47, topic:932"]
wss://syrius-testnet.zenon.community:35998
[/quote]

wow, can't believe it was because I was connected to the wrong node :C. Everything came through all at once after I connected to wss://syrius-testnet.zenon.community

-------------------------

DrD3 | 2022-11-03 13:33:18 UTC | #49

**Observations from using the test bridge:**

1.  25tznn -> twznn (Wrapping)
Waiting time for receiving approval from extension= 1:23 mins
Waiting time for the transaction to complete "signing"= over 4 mins
Redeeming the znn to twznn within MM consisted of two stages with the first taking 2 mins and the second being more immediate.

2. 50tznn -> twznn
Receiving approval from extension= 1:44 mins
Signing= 0:59 mins
Redeeming= 2 mins then instant.

3. 75tznn -> twznn
Receiving approval from extension= 3:13 mins
Signing= 0:47 mins
Redeeming= 2 mins then instant.

![Wrapping|690x392](upload://bswDsCMDzMsRb7HiK93wyPkecfn.png)

4. 75twznn -> tznn (Unwrapping)
Receiving approval from extension= 0:45 mins
Signing= 2:25 mins
Redeeming= 2:56 mins

5. 50twznn -> tznn
Receiving approval from extension= 0:47 mins
Signing= 2:58 mins
Redeeming= 1:28 mins

![Unwrapping|690x301](upload://nYINuy02LkWjIR1DuQXE5OHBp9D.png)

**Issues identified:**
1. Clicking on 'Connect Syrius Extension' sometimes results in a "socket not approved" popup.
2. After completing a transaction and attempting to begin another one- clicking on the extension results in the wallet opening up but the approval popup not appearing. This happened 2/4 times and was resolved by refreshing the bridge. 

* Outta gETH for now so I'll have to try again later

-------------------------

sumamu | 2023-03-07 16:40:15 UTC | #50

After 9 months of high-paced development, the NoM Multichain infrastructure is finally ready for release: https://forum2.zenon.org/t/zip-sumamu-0002-final/1327

We are also preparing in parallel the applications to Accelerator-Z and pull requests for the go-zenon codebase.

-------------------------

aliencoder | 2023-03-07 20:28:10 UTC | #51

Finally we'll have both a decentralized bridge *and* the Orbital Program. It's safe to say it's a very important milestone for NoM. Good work, guys!

-------------------------

sumamu | 2023-03-20 12:29:32 UTC | #52

The NoM Multi-chain Infrastructure documentation:

https://github.com/HyperCore-Team/nom-multichain-docs

-------------------------

cryptocheshire | 2023-03-21 05:00:20 UTC | #53

You might want to join the convo on the main telegram

-------------------------

sumamu | 2023-03-21 10:30:57 UTC | #54

The docs are now available in web format here:

https://hypercore-team.github.io/

A lot of effort was invested into this documentation. Constructive feedback is appreciated!

-------------------------

cryptocheshire | 2023-03-21 11:46:51 UTC | #55

Raising some points that have been addressed in the Zenon TG here:

Re: Orchestrator Nodes

> "This design decision is based on the consideration that the security of the whole network depends on NoM consensus running nodes."

How/why does this translate into the security of the bridge?

> "Pillar operators already have both the technical background and know-how to operate nodes and a sufficient stake in the network to responsibly manage this critical piece of infrastructure."

How do you measure "Responsible Management"? 
How does the fact that someone runs a pillar mean they can maintain nodes of other other networks? 
What is the incentive for them to do so?
Why did you not go for sentinel implementation which, [according to Kaine](https://t.me/zenonnetwork/265300) are the right network participant to act as protocol level oracles (instead of having Pillar operators do this).

Re: Guardians
> "Guardians will be elected from prominent members of the community. Their main responsibility is to safeguard the infrastructure in case of an emergency. They will act as judges in case of a major failure of the infrastructure and they are responsible to appoint a new admin."

Why would "prominence" qualify for participation in a trusted setup?
How is "prominence" measured and who will be the judge of who is eligible?

Can you please show which other possible solutions you've exhausted?

-------------------------

sumamu | 2023-03-22 21:37:20 UTC | #56

[quote="cryptocheshire, post:55, topic:932"]
How/why does this translate into the security of the bridge?
[/quote]

The `orchestrator` has built-in authentication using `libp2p` and each Pillar already has an "identity", namely a `producer` key that has implications for the security of the consensus protocol.

[quote="cryptocheshire, post:55, topic:932"]
How do you measure “Responsible Management”?
[/quote]

They already have a huge responsibility to maintain the security of the whole network by running consensus nodes.

[quote="cryptocheshire, post:55, topic:932"]
How does the fact that someone runs a pillar mean they can maintain nodes of other other networks?
[/quote]

As I've already stated, they have the technical background to run full nodes. Pillars are basically `znnd` full nodes. Running connectors/relayers for connected networks is an easy task given that the `orchestrator` supports light nodes and 3rd parties (that are good enough).

[quote="cryptocheshire, post:55, topic:932"]
What is the incentive for them to do so?
[/quote]

An obvious answer: Pillars heavily invested into this ecosystem. It is in **their best interest** to expand the ecosystem and tap into bigger markets (worth billions of $ combined). Plus the legacy bridge is closing and the remaining markets are either illiquid or centralized.

[quote="cryptocheshire, post:55, topic:932"]
Why did you not go for sentinel implementation which, [according to Kaine](https://t.me/zenonnetwork/265300) are the right network participant to act as protocol level oracles (instead of having Pillar operators do this).
[/quote]

We like to take everything step by step. We've **shipped a ton** already. And some of you are still questioning us.

If everything goes smooth from now on, we'll move on to tackle the Sentinels as well. We have many plans for the future.

[quote="cryptocheshire, post:55, topic:932"]
Why would “prominence” qualify for participation in a trusted setup?
[/quote]

Because several OG members have a very good track record. You can literally trust them with your funds (for example OTC trades).

[quote="cryptocheshire, post:55, topic:932"]
How is “prominence” measured and who will be the judge of who is eligible?
[/quote]

We can propose some members and decide together with the community.

[quote="cryptocheshire, post:55, topic:932"]
Can you please show which other possible solutions you’ve exhausted?
[/quote]

I think that what we try to deliver is vital for any young ecosystem. It's up to every community member to support us or not.

I also think that the **code alone speaks for itself** and we are literally **exhausted** at this point. Only the documentation took us 7 days to finish... over 25 pages in total... I think many of you **grossly underestimate the tremendous amount of time and resources** we've already committed to this project.

-------------------------

cryptocheshire | 2023-03-23 05:33:39 UTC | #57

Thank you for the answers.

I don't believe anyone doubts the amount of work you have put into this. Yet, this is an open source community and you chose to implement design choices without really entering an open dialogue about them in the first place (despite continuous attempts by community members to engage you in one for months). 

It may well be that you preferred focusing on delivering code you felt confident to be the best possible solution for a pragmatic and a fast time to market, rather than engaging in lengthy discussions, that's fair enough.

But in that case it shouldn't come to a surprise to you that some people will question your design choices until they fully understand why you made them. 

Given that a supermajority of Pillars will need to run your code for it to be useful, educating the community about why you built this the way you did could be critical. 

In politics, your loudest critics sometimes turn out to be your most useful allies.

Good luck!

-------------------------

dat_she_pepe | 2023-03-24 04:07:18 UTC | #58

Kuddos to sumamu and his team for the work.

-------------------------

zyler9985 | 2023-03-24 12:57:19 UTC | #59

I can't wait to use the bridge, I'm gonna make a step-by-step guide like the one I did for the BSC bridge, it'll be the same noob-friendly style. I reckon I'll LP a small amount as well to be part of the orbital program party.

Love to see your dedication to zenon as well as your dedication to excellence (Mr Kaine is still reviewing, but he mentioned in telegram that he was really impressed by your coding skills!!)

-------------------------

dat_she_pepe | 2023-03-26 14:33:24 UTC | #60

I'm keen to provide some liquidity to the bridge. Can't wait.

-------------------------

0x3639 | 2023-03-31 10:25:17 UTC | #61

Adding this here

Web
bridge.testnet.zenon.community

Faucets
$ZNN: t.me/znn_faucet_bot
$ETH: sepolia-faucet.pk910.de

Feedback
t.me/nom_mt

Source: 
https://twitter.com/su_mamu_/status/1641682526727962624?s=61&t=PrMsEcDqxdl6bt-Wi7ygFQ

-------------------------

sumamu | 2023-04-10 10:27:13 UTC | #62

The upcoming bridge to Ethereum is set to open new markets and opportunities, creating an exciting space for users and developers. To prepare for this change and address concerns from the community and Mr. Kaine, a well-structured plan called the Liquidity Bootstrap & Provisioning campaign has been developed.

The timeline for the campaign is as follows:
1. Activate upgrades
2. Activate bridge
3. Create pools
4. Bootstrap liquidity
5. Start Orbital Program
6. Provision liquidity
7. Increase Orbital incentives
8. Remove limits
9. Finish campaign

> Mr.K: Is there a dedicated window of time for bootstrapping the liquidity pools? How will you avoid unfair participation at the start of the Orbital Program?

Before starting the Orbital program, we need to give some time for early participants to transfer their assets, add them to the pool, and then move the pool tokens back to NoM to stake them in the Orbital program. This ensures they have a fair chance to participate. Daily rewards are 561.6 ZNN and 1,250 QSR. During the "Liquidity Bootstrap and provisioning" campaign, up to 250k ZNN and up to 600k QSR extra rewards may be given out based on the campaign results.


> Mr.K: Do you have a plan to limit the risk exposure for the liquidity pool?

We have taken many steps to ensure the safety of the bridge contracts and the Orbital contract. These steps include unit-tests, static analysis, internal audits, community audits, and manual testing. Additionally, we will limit the maximum amount of wZNN in the pool to 100k at first to lower risk exposure and provide better incentives for early participants, making it more attractive to add liquidity.


> Mr.K: Are there any mechanisms to avoid a liquidity implosion? (LPs swapping the wrapped tokens for the other tokens in the pool in order to provide liquidity)? Opening new market will generate activity which could, in turn, attract front running bots. Is there a way to protect users against this or leverage it to their advantage?

The campaign's goal is to set up and add funds to the liquidity pools. To lower the risk of liquidity implosion, we will restrict swapping wrapped assets for their counterparts in the pools during the "Liquidity Bootstrap & Provisioning" campaign. This also protects participants and users from front-running during the campaign because a bot would only be able to execute a partial swap.

Overall, the Liquidity Bootstrap & Provisioning campaign has been designed with the best interests of the community in mind. It aims to create a fair, stable, and secure environment for users as they navigate the new opportunities presented by the Ethereum bridge. By implementing these measures, we hope to foster a thriving ecosystem that benefits all parties involved.

-------------------------

0x3639 | 2023-04-10 11:04:43 UTC | #63

[quote="sumamu, post:62, topic:932"]
“Liquidity Bootstrap & Provisioning” campaign
[/quote]

How long will this period be?

-------------------------

sumamu | 2023-04-10 11:15:58 UTC | #65

[quote="0x3639, post:63, topic:932"]
How long will this period be?
[/quote]

At least 1 month and likely up to 3 months, but the final period will have to be adjusted based on results.

[quote="0x3639, post:64, topic:932"]
Just wanted to confirm this period will be approximately 445 days (250,000/561). Meaning the distributions are equal every day regardless of the depth of the market.
[/quote]

Not entirely correct. What it actually means is that there will be a certain amount of rewards that will be distributed daily (561.6 ZNN and 1,250 QSR) and in the orbital contract there is an extra amount of rewards (250k ZNN and 600k QSR) out of which an optional amount can be distributed daily until it reaches zero.

-------------------------

0x3639 | 2023-04-10 11:21:38 UTC | #66

[quote="sumamu, post:62, topic:932"]
The campaign’s goal is to set up and add funds to the liquidity pools. To lower the risk of liquidity implosion, we will restrict swapping wrapped assets for their counterparts in the pools during the “Liquidity Bootstrap & Provisioning” campaign.
[/quote]

Is it accurate to then say during the first 1 to 3 months community members will be adding liquidity to the wZNN / ETH pair however NO trading will be allowed in that pair.  We will spend that time adding liquidity and moving the LP tokens back to ZNN?  

Do we need to make any changes to SYRIUS to allow for LP rewards of the LP Tokens?  Or will we use the Staking function in SYRIUS that exists today?

-------------------------

sumamu | 2023-04-10 11:25:13 UTC | #67

[quote="0x3639, post:66, topic:932"]
Is it accurate to then say during the first 1 to 3 months community members will be adding liquidity to the wZNN / ETH pair however NO trading will be allowed in that pair. We will spend that time adding liquidity and moving the LP tokens back to ZNN?
[/quote]

Swapping ETH/WETH to wZNN/wQSR and adding liquidity will be possible.

[quote="0x3639, post:66, topic:932"]
Do we need to make any changes to SYRIUS to allow for LP rewards of the LP Tokens? Or will we use the Staking function in SYRIUS that exists today?
[/quote]

At the moment everything related to the bridge + liquidity UIs is implemented as Web Apps and it's only possible to interact with the Web App using syrius extension, but as soon as Wallet Connect is integrated into syrius desktop, the UIs will be updated to work with syrius desktop as well.

-------------------------

0x3639 | 2023-04-10 11:32:49 UTC | #68

So we need a good video on how to install the Syrius Extension.  I can help with that.

-------------------------

0x3639 | 2023-04-10 11:39:00 UTC | #69

@dexter703 would it be possible to submit the syrius wallet extension to the Chrome Web Store?  That way we can avoid the step of downloading, extracting, putting chrome in dev mode, etc...

https://developer.chrome.com/docs/webstore/publish/

-------------------------

0x3639 | 2023-04-10 11:43:57 UTC | #70

[quote="sumamu, post:62, topic:932"]
we will restrict swapping wrapped assets for their counterparts in the pools during the “Liquidity Bootstrap & Provisioning” campaign.
[/quote]

Got it.  So does this means we cannot swap wZNN for ZNN and wQSR for QSR during the first 1 to 3 months?

-------------------------

sumamu | 2023-04-10 16:45:50 UTC | #71

[quote="0x3639, post:70, topic:932"]
Got it. So does this means we cannot swap wZNN for ZNN and wQSR for QSR during the first 1 to 3 months?
[/quote]

No, only swapping wZNN/wQSR to ETH/WETH will be limited during the campaign. Everything else will be possible:

[quote="sumamu, post:67, topic:932"]
Swapping ETH/WETH to wZNN/wQSR and adding liquidity will be possible.
[/quote]

-------------------------

0x3639 | 2023-04-10 16:48:00 UTC | #72

Got it. I see now

-------------------------

vibe.znn | 2023-04-14 10:21:45 UTC | #73

Does this make sense? Slippage is already a penalty for big sales right? Only allowing buying but not selling of wZNN/wQSR might give honeypot vibes?

edit: probably also being asked/answered already, but who will be the owner of the erc20 contract?

-------------------------

DrD3 | 2023-04-14 11:23:04 UTC | #74

What are the conditions necessary for utilizing the additional rewards accruing within the Oribital Contract? Do we have a certain amount of ZNN/ETH that needs to be provided to trigger a daily multiplier- something akin to the wZNN liquidity program?

![image|690x388](upload://yH8ZZ97DoY5zJnxZ5fWb02w2LHX.jpeg)

-------------------------

sumamu | 2023-04-14 11:44:24 UTC | #75

[quote="vibe.znn, post:73, topic:932"]
Does this make sense? Slippage is already a penalty for big sales right? Only allowing buying but not selling of wZNN/wQSR might give honeypot vibes?
[/quote]

It's only during the liquidity campaign and considering the potentially high incentives, without the limitation liquidity implosion is bound to happen.

[quote="vibe.znn, post:73, topic:932"]
edit: probably also being asked/answered already, but who will be the owner of the erc20 contract?
[/quote]

Only the bridge contracts will have minting rights over the Wrapped ERC-20 tokens.

[quote="DrD3, post:74, topic:932"]
What are the conditions necessary for utilizing the additional rewards accruing within the Oribital Contract? Do we have a certain amount of ZNN/ETH that needs to be provided to trigger a daily multiplier- something akin to the wZNN liquidity program?
[/quote]

The daily rewards shared between liquidity providers will be 561.6 ZNN and 1,250 QSR, with a multiplier of 1X-12X for locking the LP tokens 1-12 months. During the campaign, extra rewards of up to 250,000 ZNN and up to 600,000 QSR will be dynamically adjusted based on campaign performance. A more detailed plan will be outlined by the time the campaign starts.

-------------------------

bayrum | 2023-04-14 14:21:41 UTC | #76

If first provider brings 100k znn for liquidity program there will be no place for other people?

-------------------------

0x3639 | 2023-04-14 14:23:30 UTC | #77

now who would do that?  Maybe we have a gentlemans agreement to avoid that?

-------------------------

sumamu | 2023-04-14 14:25:06 UTC | #78

[quote="bayrum, post:76, topic:932, full:true"]
If first provider brings 100k znn for liquidity program there will be no place for other people?
[/quote]

Even if that would happen, every time someone swaps ETH/WETH to wZNN, the total wZNN in the pool will decrease and others will be able to join.

-------------------------

dat_she_pepe | 2023-04-15 15:54:25 UTC | #79

Okay I'll provide 100k ZNN thanks

-------------------------

aliencoder | 2023-04-15 20:17:27 UTC | #80

I've submitted a PR with `pprof`, versioning and the `cicd` pipeline and it was merged in the `orchestrator` repo:

https://github.com/HyperCore-Team/orchestrator/commit/8c46abae557d3ed91f692bfc659c7de6017e8e40

@sumamu thank you for merging my PR

-------------------------

vibe.znn | 2023-04-16 07:36:15 UTC | #81

One more question about the first point, just being able to buy for the first month. Wouldn't that trigger all kind of tokensniffers labeling it as a possible scam?

-------------------------

sumamu | 2023-04-21 10:55:23 UTC | #82

That shouldn't be the case, since only 1 pool is restricted. Anyone could create a 2nd pool and use that to do whatever.

-------------------------

sumamu | 2023-05-03 20:18:57 UTC | #83

The bridge upgrade has been activated last week, so it's going live soon. For that to happen, we've got some work to do as a community. 

@0x3639 has a headstart with the audit, so we're going have to pick up the pace and pick the initial guardians of the network.

___
> What is the role of the guardians?

In case the admin is compromised, before any administrative actions can be taken, the admin has the possibility to remove itself as admin. If this happens, the bridge goes into emergency mode, where all activity is halted and restricted. At this point, the guardians are responsible to coordinate and set a new, uncompromised address for the admin.
___
> Are the guardians permanent?

No, this is just the initial batch so the bridge can go live. The guardians can be changed by the admin at a later time if the timechallenge passes. In fact, the guardians should probably prove they still control their addresses and are still active in the community from time to time. If they don't the stale guardians should be changed with other members of the community.
___

> What must a guardian provide in order to become a guardian?

A valid NoM address, the associated ed25519 public key and a signed message to prove they actually own that address.
___

> How should they be chosen?

After debating the issue of choosing the guardians a bit internally, we came up with the following aspects to take in consideration:
- technical skills
- ecosystem involvement
- availability
- decentralization/distribution
___

> How do they vote?

The znn cli will be updated to provide a way for the guardians to cast votes. A new admin becomes active once it has 50%+1 votes.
___
In conclusion, we're proposing 10 devs + 5 pillars as the initial guardians. Remember, they are not permanent:
:white_check_mark: mr kaine `z1qpxswrfnlll355wrx868xh58j7e2gu2n2u5czv` `0xb13857a4F3bc3b8AB205e06FD8b874692451ADc0`
:white_check_mark: @Sigli `z1qr7urykpjth3w9lcl66atgvu5fc0ywawzha220` `0x671A0F784F4AfaCEC1701eA4B6Cc3FBB68a7ADE9`
:white_check_mark: sumamu `z1qphnq6jfaf82kmpyuuc88983ar66dmh7e59f67` `0x7AA4fa384B0499111DcDa4638718d744cDD1195D`
:white_check_mark: sumoshi `z1qrgh8w9q3xj5a2t2atnt3reqhh0akm4qae8ezk` `0x2F3410C62e1C2E4CEa3fB5Db1FAC196bfcAD54D7`
:white_check_mark: nomkamoto `z1qqeyp02thdets4k245fnnjpk764ls65gwsy0cg` `0xbD0189C4a9a64B8ee82928D002a86bd5eb2A5Ef6`
:white_check_mark: @georgezgeorgez `z1qrawthjzd95hcz73r3e5wd0xxzjmrt4vfqla0z` `0x456c5FCEA60dd5F4c1dcB485FA307A946E356456`
:white_check_mark: @aliencoder `z1qzup2zm6c9g68t085zjn5ycvdnr0u4pt0k4c80` `0xE34FB7aadc91f0d95757125F9FB546712846feeB`
:white_check_mark: @CryptoFish `z1qzjnnpmnqp6uqz2m9uet8l5e42ewwaty2mqcpy` `0xf2aA170dDe5319F03785C29f94f39510EE6345AA`
:white_check_mark: @dexter703 `z1qr6k9c0z73c2zx22grhcw702slyz0gelt2uwvd` `0xc91edA9Ba70EB09f5cc450A4dFA57D43fB590C3F`
:white_check_mark: @MoonBaZe `z1qprccs7kjvx9q78m5v5ghwwfvxr6py8rtwcfrd` `0xc752B223c87327A8A6e2CBE9D3A3E334F1a96fD3`
:white_check_mark: vilkris `z1qqcz0rmkz7f5442hjjr0thh2v6txu4875eyrkd` `0x30800A10128820D518997EC22201Df0f5b873712`
:white_check_mark: @mehowbrainz `z1qzymmtmfr3gxz3fr80cq94rgaefzkvst4e90lz` `0x061ACFb9F0151c3DB502d1320B70E1A894d25010`
:white_check_mark: 0x3639 `z1qrztagl9rukq3ltdflnvg4zrvpfp84mydfejk9` `0x559d33edB4bDE79A70bE70db77Bf27E7B86C5479`
:white_check_mark: @shaimo `z1qppk2p26xwwzu5w4zyzwknrx28whvjgy9ukc6h` `0x76B9b17cce584de58668b574474939C9e6FbAdb3`

### Legend
:white_check_mark: user agreed to participate and address, public key, signature are available
:ballot_box_with_check: address, public key, signature are available (onchain or offchain), waiting for user to agree
:black_large_square: waiting for user to submit address, public key, signature and agree to be a guardian

-------------------------

0x3639 | 2023-04-25 16:36:16 UTC | #84

I'm happy to participate.  I'm ready to sign a message any time.  

I recommend you include @vilkris.  He is a dev and Pillar operator.  Also wanted to point out @ZenonORG and @shaimo have a very large footprint in the community.  I think they should be here too.

-------------------------

shaimo | 2023-04-25 17:48:39 UTC | #85

Happy to participate 👍

-------------------------

ZNNAYIID | 2023-04-25 17:57:55 UTC | #87

I suggest removing QSR, ElderZ, and ZenDao since they are not that active in the community.
My suggestion : Zed, Anvil, ZenonORG, one of shai’s pillar.

Also since you are a team, wouldn’t it be better to only have one of you as a guardian instead of all the three? That’s like 20% of voting power… Or maybe add more guardians ( preferably pillars)

-------------------------

sumamu | 2023-04-25 18:06:17 UTC | #88

[quote="ZNNAYIID, post:87, topic:932"]
Or maybe add more guardians ( preferably pillars)
[/quote]

You're onto something here. The best guardians would be pillars and the most appropriate pillars are the ones who demonstrate they have the skills to set up the orchestrator and become TSS participants. 

We can only figure out which are those pillars after the TSS key generation event is complete. So for now, we'll have to go with a list of 15-20 guardians because they're required to get to the TSS key generation phase and after that's done, the guardians will be updated to the owner addresses of the pillars that participated in the bridge.

-------------------------

romeo | 2023-04-25 22:29:04 UTC | #89

another vote of confidence for considering sigli/zed, vilkris, shai and ZenonORG.

All have shown continued support and acted in the best interests for the NoM

-------------------------

DrD3 | 2023-04-26 10:16:29 UTC | #90

+1 for the suggestions 

* Zed- Sigli's been around from the start and as community prophet has onboarded/assisted most of us at some point or the other. 
* Anvil- Vilkris is both dev and pillar & has constantly proved his mettle by delivering projects/services before requesting any compensation from AZ.
* ZenonORG- I don't think anyone can really question their commitment to NoM.
* Shai- wrote the article that initially got me hooked, has multiple pillars, and is probably the most trusted community member operating the soon-to-be-defunct Shaiswap.

DeeZNNutz & SultanofStaking are both top-tier candidates but I agree with Layiid that the other three (QSR, ZenDAO & ElderZ) need to play a more active role all-in-all before we can trust them to play the role of Guardian in the event shit goes down.

-------------------------

sumamu | 2023-04-26 12:49:09 UTC | #92

@Sigli @georgezgeorgez @aliencoder @CryptoFish @sol @dexter703 @MoonBaZe  @vilkris @mehowbrainz @shaimo

Can everyone on the guardians list confirm they're ok with being nominated as a guardian and if so, please check your address is correct or provide an alternative address.

Please keep in mind that all guardians must also provide EVM addresses by Monday (May 1st 2023) to be used as guardians for the solidity contract which is currently being audited by ChainSafe.

-------------------------

ZNNAYIID | 2023-04-26 12:30:15 UTC | #93

Also for dexter he’s not really active, last seen here was in 2022, same on tg. We need active devs and pillars for this critical role.

-------------------------

sumamu | 2023-04-26 12:34:29 UTC | #94

@dexter703 developed the entire bridge web app so that kind of qualifies as active. Just because a dev isn't constantly communicating on the social channels, doesn't mean they're not actively building.

-------------------------

sumamu | 2023-04-26 12:47:45 UTC | #96

Awesome! Is the address correct and will you also be able to provide an EVM address by Monday?

-------------------------

aliencoder | 2023-04-26 12:54:30 UTC | #97

I also confirm my participation. Thank you for the nomination!

-------------------------

coinselor | 2023-04-26 13:20:31 UTC | #98

Acta, non verba.

As a mere alien, I feel well-represented by this proposed guardian set. 

Hopefully, in no time everyone on this list is not only a guardian but a pillar operator.

-------------------------

CryptoFish | 2023-04-26 13:57:23 UTC | #100

I can confirm my participation. The Zenon address is correct and below is my EVM address.

0xf2aA170dDe5319F03785C29f94f39510EE6345AA

-------------------------

0x3639 | 2023-04-26 14:47:52 UTC | #101

[quote="sumamu, post:83, topic:932"]
z1qrztagl9rukq3ltdflnvg4zrvpfp84mydfejk9
[/quote]

This address is correct.

-------------------------

shaimo | 2023-04-26 15:31:53 UTC | #102

How to submit the required info? DM you on TG @sumamu?

-------------------------

sumamu | 2023-04-26 17:59:24 UTC | #103

Sure, that'll work. If it's an address you've used onchain or is the owner of one of your pillars, just send it here, signature won't be needed.

-------------------------

mehowbrainz | 2023-04-26 17:19:07 UTC | #104

[quote="sumamu, post:83, topic:932"]
At this point, the guardians are responsible to coordinate and set a new, uncompromised address for the admin.
[/quote]

From a technical POV, what is required here?

[quote="sumamu, post:83, topic:932"]
The znn cli will be updated to provide a way for the guardians to cast votes.
[/quote]

What will votes be used for?

[quote="sumamu, post:88, topic:932"]
The best guardians would be pillars and the most appropriate pillars are the ones who demonstrate they have the skills to set up the orchestrator and become TSS participants.
[/quote]

What is the average infra consist-of for an orchestrator?

-------------------------

sumamu | 2023-04-26 18:39:44 UTC | #105

[quote="mehowbrainz, post:104, topic:932"]
From a technical POV, what is required here?
[/quote]

Basically you're just sending a transaction to the bridge contract originating from your guardian address and specifying the admin's new address.

[quote="mehowbrainz, post:104, topic:932"]
What will votes be used for?
[/quote]

Telling the bridge contract about the admin's new address.

[quote="mehowbrainz, post:104, topic:932"]
What is the average infra consist-of for an orchestrator?
[/quote]

Minimum: linux machine, 2 cores, 2gb ram, 50gb storage ssd/nvme, pillar producer keystore and password, reliable connection to go-zenon & ethereum nodes. However, this doesn't account for the resources required by the nodes, just the orchestrator.

-------------------------

mehowbrainz | 2023-04-28 22:59:51 UTC | #106

I confirm ZenonORG/mehowbrainz participation. The Zenon address is correct. The EVM address is: `0x061ACFb9F0151c3DB502d1320B70E1A894d25010`

Will appreciate documentation for any participation requirements, including the orchestrator.

-------------------------

vilkris | 2023-04-26 17:53:41 UTC | #107

I also confirm my participation. Thank you for the trust. The NoM address is correct.

EVM address:

0x30800A10128820D518997EC22201Df0f5b873712

-------------------------

