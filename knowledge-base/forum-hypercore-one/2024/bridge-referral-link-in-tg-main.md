Thread: bridge-referral-link-in-tg-main
0x3639 | 2024-02-28 02:50:04 UTC | #1

## Background
Some time ago I tried to have a discussion with the community about a bridge referral link in the `/bridge` command in the Main Telegram Channel.  During this time we were discussing ways to increase funding to AZ.  One of those ideas was to reduce pillar rewards and divert them directly to AZ.  Another idea was to generate bridge affiliate fees from Telegram Main and redirect them to AZ.  I proposed that idea [here](https://forum.zenon.org/t/bridge-referral-link-from-tg-main/1701) and linked to it in TG [here](https://t.me/zenonnetwork/332420). 

I explored ways to deposit the bridge affiliate fees directly into AZ, but after discussions with @sol we determined that was not possible. So my proposal was to receive the fees into the address `z1qz78vztx78hzpyzhfe0hk0mndszrf344na3zlr` and then manually deposit them into AZ.  To date, that address has received ZERO $znn.  It's possible there are some unreceived fees.  To be honest, I have never checked.  But no matter what, they are due to the community as discussed in that post.     

I never got any feedback (for or against) so I implemented the bridge affiliate link as proposed.  

When you type `/bridge` in TG you see this Website for the bridge.  

![Screenshot 2024-02-27 at 8.31.11 PM|690x280](upload://gTCiLEWz6fduX8GZDAYekW825MF.png)

That URL points to this short link `https://znn.link/bridgezts` so we can track the number of clicks.  It has been clicked 39 times.  

![Screenshot 2024-02-27 at 8.34.46 PM|690x72](upload://mNHYNW5ZBAefGj4y39pJRB0T4TK.png)

That link redirects to `https://bridge.mainnet.zenon.community/?referral=2f5b370a4e6e3a382130746d023c00002c242430782b3e5a2b1e1d253630337b7761042743033a3e`

## Feedback

I would like to know if we should continue this program to attempt to farm bridge affiliate fees from the Main Telegram channel and manually deposit them to AZ.

And, if we continue this program should we change the links or how we do it?

If we decide to remove the bridge affiliate link from the TG channel it's likely someone else will collect the fees: Funnelz, Nodez, Front end affiliate logic as disclosed by @sumamu, other affiliates, etc.

I hope we can get some feedback so everyone in the community is comfortable with this link.

-------------------------

mehowz | 2024-02-28 06:49:36 UTC | #2

Both the zenon.network and Zenon_Network handle don't have default referral links. The reward system was designed to reward community for creating content, referring users to the bridge in hopes to earn some rewards. What's the point to give such tools to the community if core routes like TG main have a default referral built-in? Might as well put the default on zenon.network and Zenon_Network twitter handle and give all the future rewards to AZ. Even the bridge itself asks for users to find their own referral links, passing the opportunity onto the community to earn some rewards. 

Let's leave core routes alone from rewards which could undercut efforts of community to earn. And especially if it has to be deposited to a community member's address first.

[quote="0x3639, post:1, topic:383"]
If we decide to remove the bridge affiliate link from the TG channel it’s likely someone else will collect the fees: Funnelz, Nodez, Front end affiliate logic as disclosed by @sumamu, other affiliates, etc.
[/quote]

As intended by design, why block organic efforts? Anyone sharing an Attribute link / referral link should be granted that reward if he's first to help someone, effort well deserved no?

My bigger question is: why was this opportunity diverted from community earning rewards, to AZ? And why are network-owned channels like TG main not governed by Pillars via on-chain voting?

-------------------------

coinselor | 2024-02-28 11:43:37 UTC | #3

From memory, the sequence of events unfolded as follows:

1. A complaint was raised about the difficulty of noticing the absence of an affiliate link (the user had already swapped and missed the rewards). As evidenced by Dexterz's latest bridge version, improvements have been made in this area by moving the notification to a more prominent position.

2. It was highlighted that there was a need to find a referral link, and a debate ensued regarding this being a poor user experience due to users missing out on rewards.

3. As a "TEMPORARY" solution, we agreed to add a referral link to the TG notification to mitigate the issue in the meantime. As more people create content and the issue becomes less significant, this referral link will become unnecessary for the reasons you've mentioned: by design, referral rewards should reward organic efforts.

If we believe the community has already made significant improvements, and we anticipate a decrease in the percentage of users bridging without a referral code, we should consider removing the affiliate link from TG.

**Personally, I would prefer to wait until the new bridge front-end, currently in the staging phase, is live.**

-------------------------

mehowz | 2024-02-28 13:38:40 UTC | #4

I disagree, core channels should not have any default links. The intended design of the bridge was for users to find their own links, otherwise they would've just placed a default link on their bridge page. It's a few in the community who decided that a default link should be assigned from a network-owned channel, and I believe such decisions should be pushed into a consensus mechanism, like AZ for votes by Pillars. Mods of these channels act only as enforcers of what's voted-by Pillars.

-------------------------

sugoibtc | 2024-02-28 16:25:13 UTC | #5

While I agree that the core channels should not have any affiliate links attached to them, we're currently still in the staging phase of the new bridge front-end as commented above.

For that reason, I think that keeping the A-Z affiliate link as a temporary placeholder is okay. We were looking for ways to increase the A-Z fund, and this way the whole network could benefit from it.

Once the new front-end has been deployed, we can turn the A-Z affiliate link off and all creators would be able to earn rewards through their own services/tools the moment they leave the neutral channels.

I also trust @0x3639 in that he would've donated any affiliate rewards gained through that link to A-Z. He has done a lot for the community already and I don't believe that he would act in bad faith.

-------------------------

0x3639 | 2024-02-29 22:53:04 UTC | #6

I just checked the affiliate link associated with the Main TG Account.  Here is the total.  This is owned by the community.  In my original post I proposed these either go to AZ or the community comes to some consensus on what to do with them.  I will receive and deposit these into AZ if the community does not propose and approve an alternate within 7 days.


![image|491x500](upload://ldinSs1gMiYHfLC39LVvTDHBR0C.jpeg)

-------------------------

0x3639 | 2024-03-08 13:28:37 UTC | #7

According to the [original post](https://forum.zenon.org/t/bridge-referral-link-from-tg-main/1701), I will be farming these rewards and depositing into the AZ contract.  If anyone objects, please let me know and propose a new community initiative for a vote.

Looks like the 7 days has expired so I would like to do this soon if there is no objection.

-------------------------

0x3639 | 2024-06-17 23:24:09 UTC | #8

This was completed.  The tg bridge affiliate link on telegram (legacy account) received 187.78263276 ZNN.  That was farmed and sent to the AZ contract.  

https://zenonhub.io/explorer/transaction/fc1c8816a9eac39cf1bc5bb9ec1c17d770acedda4d5b4779b70e1e697d3ff599

-------------------------

