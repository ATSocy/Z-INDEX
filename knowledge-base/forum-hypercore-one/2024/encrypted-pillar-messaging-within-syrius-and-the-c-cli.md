Thread: encrypted-pillar-messaging-within-syrius-and-the-c-cli
0x3639 | 2024-02-29 19:29:56 UTC | #1


## Issue
Pillar voting is very low.  We generally have 30 Pillars consistently voting which is barely enough to approve AZs and funding requests.  In addition, Pillars who control more than one can single handedly kill a vote by simply not voting.  Our system was designed to promote a democracy with decentralization, not a monopoly with centralization.  

How can we improve voting and engagement by Pillars?

## Proposed Solution
Encrypted messaging in syrius.  If we can send messages to Pillars they might read them and consider voting.  

## Background
@sol @vilkris and @aliencoder have investigated messaging solutions.  We have also discussed this topic with Mr. Kaine in TG.  
- @vilkris developed a [PoC Encrypted Messaging Solution](https://forum.zenon.org/t/secret-messages-poc/1183)
- @aliencoder found a [Dart Implementation of the Signal Protocol](https://forum.zenon.org/t/secret-messages-poc/1183/6?u=0x3639)
- @sol  Came up with a [message field in the transfer agent.](https://forum.zenon.org/t/rfc-syrius-message-field-in-transfer-widget/864)

Pillars do yield farm even if they don't vote.  If we can send them encrypted messages and show a notification it's possible they will look at a message. If they will look at a message, we can ask them to look at and/or vote on an AZ or funding request. 

## Proposal
- Add messaging functionality to the C# cli that leverage the work that @vilkris did on messaging.  
- Use the cli to send encrypted messages to addresses in NoM. By limiting the message generation to the cli it's possible we can reduce spam.  Barriers to create messages are higher.
- Add a notification in syrius when an address receives an encrypted message
- Add a display window to read the message.
- Consider adding a fee to see a message in syrius.  Meaning, for a user to send a message they must pay x znn for that message to appear in the users wallet.  If no fee is paid, the message will not appear.  This will be enforced in syrius, and not the L1.
- We could also consider creating a messaging token that is used to send messages.  And that token must be purchased.  Maybe the dev who codes this could benefit from selling that token.  This is not necessary.  It's just an idea.  

## Issues
- Mr Kaine encouraged us to reduce chain bloat.  And this could encourage spam. However, users will not see messages unless a fee is paid.  We could also deposit this fee into AZ.  
- Can we limit message size?  Maybe we can enforce the message size at the cli level.

-------------------------

0x3639 | 2024-02-29 19:41:51 UTC | #2

I received the following idea from a DM in response to this post.  

> I think it'd be more efficient to have a feature that allows pillars to delegate their votes.
> 
> Either a separate binary that runs on pillars along znnd, or as a new feature for znnd

-------------------------

Chadass | 2024-02-29 22:05:56 UTC | #3

The only option you have is to rewards vote or reduce rewards of non voters. I highly doubt spamming an onchain mailbox will change the trend. This solution don't change the amount of ZNN earned by the pillars pack, it simply adjusts the % you get according to your activity. You want 100% of your current rewards? Vote. Or else, these ZNN will get distributed to active Pillars.

-------------------------

aliencoder | 2024-03-01 07:16:32 UTC | #4

[quote="Chadass, post:3, topic:389"]
I highly doubt spamming an onchain mailbox will change the trend
[/quote]

I have to agree with @Chadass here. We don't want on-chain messaging bloat.

We can implement [Web3Inbox](https://docs.walletconnect.com/web3inbox/about) from WalletConnect and create a dApp dedicated to Pillar owners where they can post announcements or engage with their delegators.

-------------------------

DrD3 | 2024-03-01 08:58:01 UTC | #5

Or perhaps even redirected to Accelerator-Z? Especially giving consideration to how the community's been looking for ways to make AZ more self-sustaining.

-------------------------

0x3639 | 2024-03-01 11:51:43 UTC | #6

I guess we have two problems:

1) Low pillar participation
2) Active pillars who do not vote at all (on purpose) to torpedo votes

It's possible we can solve #2 by changing the way the quorum is established.  I think the quorum is 33% of all active Pillars?  Maybe the calculation excludes inactive pillars from the quorum.  That way Pillars who do vote usually are incentives to actually vote if they want to be considered in a quorum.  

I do find it curious that 2 Pillars who never vote actually run Orchestrators.  At a minimum, why include Pillars with zero votes in the quorum?  

We currently have 23 pillars who have never voted.  If we remove them from the quorum (99 - 23 = 76 x .33 = 25).  That would reduce the quorum to 25 pillars.  

![Screenshot 2024-03-01 at 5.40.00 AM|689x420](upload://n9aj3MhmHwMKT54FzSz4jlzopp4.png)

-------------------------

