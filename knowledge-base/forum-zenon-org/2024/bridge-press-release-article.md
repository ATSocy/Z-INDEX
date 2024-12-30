Thread: bridge-press-release-article
zyler9985 | 2024-03-27 15:20:06 UTC | #1

I've drafted an article covering the bridge, the audit, liquidity program and benefits to the ecosystem (including how NoM Multichain tech can be a foundation for other things such as L2 EVM and TSS).

I'm hoping for a collaborative approach. Points of discussion:
1) Is the content good, any suggestions to add or change?
2) Where to publish article, how to distribute it? 
3) I was thinking to ride the chainsafe audit momentum (if they tweet) this would be good, but maybe better to wait? Wait for mobile wallet and atomic swaps so that could be included in a larger article about updates in our ecosystem?

https://medium.com/@Zyler9985/zenon-network-building-bridges-draft-article-for-feedback-4bb2ef8af7eb

-------------------------

aliencoder | 2023-05-14 10:03:21 UTC | #2

[quote="zyler9985, post:1, topic:1435"]
* Is the content good, any suggestions to add or change?
[/quote]

Very good overall, congrats! 

Some minor suggestions:

> was reached with the release of an audited bridge to Ethereum,

From what I understood, the decentralized bridge is part of the NoM Multichain Technology that represents the actual interop infrastructure that supports "portals" with other networks such as Ethereum, BNB Chain, Bitcoin, etc.

Should we explain those concepts in more detail?

> In other words, they just started making shit up to be upset about to justify getting paid

I think this is too aggressive. They had gas optimizations that were valid, but pointless (like optimizing a tiny fraction of the gas cost). Regardless, we don't want to mock them. Just highlight that no issues were found, not even "minor".

> This fee supports an affiliate marketing system which is currently a WIP.

More context for this would help.

> The Orbital Liquidity Program was designed to mitigate risk and provide ample rewards for liquidity providers

Imo the key takeaway here is the Protocol Level Liquidity. I don't know any other blockchain that has a perpetual LP rewards flow directly piped to network emission. All other networks I know have ephemeral Liquidity Programs that eventually dry up, with no easy ways to replenish.

> Thanks to the taproot upgrade to Bitcoin, there are plans to use TSS technology to control native Bitcoin.

I think the last part is too vague/there is too little information. We can brainstorm something better here or defer this part for a separate Medium post.

[quote="zyler9985, post:1, topic:1435"]
but maybe better to wait
[/quote]

I'm finishing the WalletConnect integration right now. We can make a follow up with a tutorial on how to use the Bridge and provide liquidity via Orbital Program.

-------------------------

zyler9985 | 2023-05-14 12:04:48 UTC | #3

Thanks for the encouragement bro! You're doing a great job too. If just writing about all of this is kinda complicated, I can't imagine being among the builders actually building it!! I'll offer some changes here, I hope these improvements are good, otherwise let me know and we'll change it again:

1) So the intro of "audited bridge to ethereum" I think should be left as it is, because intro would quickly become bloated and difficult to grasp otherwise. But could change the first paragraph in body of article to this:

The decentralised bridge to Ethereum which has been released is actually a subset of the NoM Multichain Technology. The infrastructure facilitates interoperability with other networks such as Ethereum (already supported), BNB Chain and later Bitcoin. You can learn more about the plans for Bitcoin interoperability here (link to a separate article yet to be made). Because it involves innovative solutions such as the use of TSS technology, some of these future developments wouldn't strictly classify as a bridge which is why the nomenclature for 'Portals' to other networks has been adopted by the Zenon Community. 

^^ I'd need help with a BTC interoperability article. We could defer that brainstorming for a separate forum post.

2) The mocking line was just for the lols, next sentence I said I was testing if anyone was actually reading the draft. Thanks for passing the test!! Will remove the line.

3) So we can talk more about the affiliate marketing system for sure. I'll re-read the forum post and I will reply with some Questions I have, to clarify my understanding so I can make a concise paragraph or two about it. It is a really cool idea worth including, shows our sophistication with marketing and could even attract people to vie for those rewards.

4) I didn't understand how special it was to have protocol level liquidity. God, more I learn about Zenon the more it feels like a blessing to be here. How about I change the paragraph to this: 

The Orbital Liquidity Program was designed to mitigate risk and provide ample rewards for liquidity providers. It does that in a number of ways which are explained below, but one of the key takeaways is that this is Protocol Level Liquidity – so LP rewards come directly from network emissions. This means the Liquidity Program is governed by the DAO and has the capacity to be readily replenished if need be. Longterm sustainability is therefore a core feature of this Liquidity Program.
The rewards are in both ZNN and QSR, which come from protocol-level emissions at a baseline of 561.6 ZNN/day and 1250 QSR/day. On top of this, there are Bootstrap Rewards to incentivise early participants. Finally, there is also a liquidity multiplier to reward longterm commitment. This begins at 1 month (for a 1X multiplier) and increases in monthly increments up to a maximum of 12 months (for a 12X multiplier). 

5) Okay sir, so we wait for a bit? Need walletconnect integration to be complete and bridge to be live. Once we can actually do these things, we can link a companion article which is a tutorial for buying, providing liquidity and how to bridge it. Will enhance effectiveness if we spoonfeed humans this to turn them into aliens. I'll need help with getting screenshots for it, especially for LPing part. And I'll make it sound more formal than the fun pancakeswap one I did lol. Gotta sound authoritative.

-------------------------

zyler9985 | 2023-05-14 15:20:38 UTC | #4

3. Affiliate marketing fee more context:

So going from wZNN to ZNN, or from wQSR to QSR, is feeless. But going from ZNN to wZNN, or from QSR to wQSR, does incur an X% fee. The X% fee supports an affiliate marketing system. The current upper limit for this fee is 3%, but it is expected to decrease over time pending the DAO's decision which takes into account multiple factors. The benefit is that marketers can be given both an incentive to grow Zenon as well as the means to measure their performance in a way which directly relates to price, liquidity and volume – hard and sound metrics to make sure the value added can justify the spend. To give an example of how this works:

Each time a person leaves Zenon's ecosystem, the 3% fee becomes embedded into the bridge contract. When someone else enters Zenon's ecosystem via an affiliate link a marketer has generated, the buyer receives a 1% bonus and the marketer receives the other 2%. The 1% and 2% bonuses are supplied 1:1 by the 3% fee, making this a self-sustaining mechanism which also scales infinitely with price. Click here to learn more about the affiliate marketing system (link to an article yet to be created/ a page which explains how to make affiliate links).

-------------------------

mr.ztark | 2023-05-15 12:56:23 UTC | #5

Excellent! I like how your writing style is evolving and is less conversational, more concise, and cleeeaaannnn.

Beautiful.

-------------------------

zyler9985 | 2023-05-15 14:27:07 UTC | #6

If I'm doing a press release, it's gotta be concise, clean and so formal it will give even giga boomers a boner.

But a zyler article that's just from my medium will always sound like it was written by a madman I'm afraid.

-------------------------

0x3639 | 2023-05-15 14:31:43 UTC | #7

After you update the draft with feedback, I'm happy to put it into chatGPT 4.0 (I have a license) and can ask it:

Convert this article into a Press Release.  

A press release picked up by news agencies must follow a standard format.  @angelo_a_jr might have some examples he can share.  They use certain words, like For Immediate Release, and require a city/ state.  I think they also have word limits.  

Maybe we can release two versions of the post.  Maybe and article version and true "press release" version.

-------------------------

zyler9985 | 2023-05-15 14:50:12 UTC | #8

The feedback has now been incorporated into the draft.
I could redo it within a word limit if needed, and/or we could look at the chatGPT version if a presser so requires it. 2 versions sounds good, an article and a presser.

Only thing that's missing is a companion article that's a tutorial for buying/bridging/providing liquidity and an article discussing BTC interoperability (WIP)
^^ ideally both of those will be linked within the article.

-------------------------

mr.ztark | 2023-05-15 15:00:53 UTC | #9

Boomer boner: Confirmed.

-------------------------

