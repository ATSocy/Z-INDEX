Title: Perpetual ecosystem growth

URL Source: https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print

Published Time: 2023-05-04T09:34:28+00:00

Markdown Content:
Before getting into details, I would like to know how everyone feels about the following.

Would it bother you if sellers would be paying a fee and that fee would then be used to incentivize affiliate marketers who bring in buyers?

*   YES
*   NO
*   Show results

[https://twitter.com/su\_mamu\_/status/1650954683224059919](https://twitter.com/su_mamu_/status/1650954683224059919)

[0x3639](https://forum.zenon.org/u/0x3639) May 4, 2023, 9:45am  2

Just wanted to clarify the question and answer a little.

You need to vote NO if you are in support of incentivizing affiliate marketers to attract buyers by charging sellers a small TX fee. I assume that fee would go into some marketing pool to be used by marketers to attract buyers.

This seems like a great program that will be self sustaining (i.e. perpetual motion machine) and will benefit the entire network.

[sumamu](https://forum.zenon.org/u/sumamu) May 4, 2023, 9:54am  3

Yes, that’s accurate.

Another take here : a different marketing strategy is deep liquidity : the seller / buyer could may a fee which could be redirected into a liquidity pair (znn-eth?). We can have the best marketing in the world, at the end of the day attracting capital come from liquidity + apr. Zenon has been suffering from low liq since years and this could help quite a lot to get the interest of those looking to enter the ecosystem easily. What do you think?

[sumamu](https://forum.zenon.org/u/sumamu) May 4, 2023, 10:42am  6

Yes, I agree that liquidity is very important. Uniswap pools already redistribute trading fees to liquidity providers. And we already have Orbital program that incentivizes liquidity providers.

Please correct me if I’m wrong, you’re proposing that there should be a trading fee that gets locked in the pool as liquidity that wouldn’t be owned by anyone. That is a great idea, indeed and I will think about its impact.

We still need a mechanism that will inject new value into the ecosystem, which is why I’m looking to incentivize affiliate marketers to go out and bring that value here.

I don’t know what would be the best model but I’m afraid that APR alone - as incentives for LP - would’t be competitive on a low mcap and without a big push from a MM. Usually when a project launch such program there are VC’s pumping to make the whole thing attractive hence why I thought about some fee going to the pool and being owned by nobody. I see several pros to this proposal:

*   we don’t solely rely on big players to push liquidity up as they usually pull away within a week anyway.
*   the liquidity will keep increasing no matter what.

It makes me think about the protocol owned liquidity I saw in defi but I don’t recall how it used to work.

By selling you mean ZNN to wZNN bridging?

Same question. Are we talking about wZNN trading on ETH?

[sumamu](https://forum.zenon.org/u/sumamu) May 4, 2023, 2:59pm  10

Very bold affirmation. Can you explain the inner workings of this mechanism?

Orbital Program is basically protocol owned liquidity, we just choose to pay it out as extra APR instead. Locked-in liquidity have indeed helped other projects, as it acts as a guaranteed that there would be some exit liquidity.

I don’t think it should be “owned” by anyone, but owned by the network participants. I think having the same guarantees as what it takes to halt the bridge, to be able to move the liquidity say from ETH to Avalanache, if the community desires to, would work well in terms of both capital efficiency and as a liquidity guarantee, as it would negatively impact the reputation of the network if the liquidity is not thoughfully moved around from chain to chain.

I would also like to point out, that if we can show what percentage of the LPs are locked in for a full year (to take advantage of the APR multiplier) then this might be enough of a guarantee for most people. It would just be a game of increasing the depth of the liquidity, which the marketing fee can be of great help.

It’s not the same thing as a small fee per tx would increase the liquidity over time.

If you use a % of the outstanding Orbital funds to create a LP position, that position will also acrue fees from the Uniswap LP as well as Rewards from orbital, therefore compounding and increasing overtime.

A direct fee will definetely increase the liquidity much faster, especially in times of extreme volume peaks.

How would that work and how do you get ETH from those immense funds without destroying the price ? The interesting pairs are the in / out for ZNN not the QSR/ZNN one

[sumamu](https://forum.zenon.org/u/sumamu) May 9, 2023, 11:32am  17

So we have the results of the poll and 76% of the respondents would be willing to pay some kind of selling fee in order to incentivize marketers to bring value.

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#whats-the-objective-1)**What’s the objective?**
------------------------------------------------------------------------------------------------------------------

It is linked to the bridge and it goes like this (values and assets are just for sake of simplicity):

*   ideally we’d want to reward marketers for bringing value to the ecosystem, which would mean a new user that buys ZNN
*   we can’t do that easily, but we have some control over the bridge and the next best thing we can do it consider users swapping ZNN \> wZNN potential sellers and users swapping wZNN \> ZNN potential buyers

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#where-do-the-funds-come-from-2)**Where do the funds come from?**
-----------------------------------------------------------------------------------------------------------------------------------

*   every time a potential seller swaps from ZNN to wZNN, a fee of 3% remains in the bridge embedded
*   every time a potential buyer swaps wZNN to ZNN, they can use a referral link, which will give the potential buyer a 1% bonus and the referral another 2%
*   this mechanism is 100% sustainable, infinitely scalable and unlimited since there can only be as many wZNN bought as there were sold

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#what-does-the-marketer-need-to-do-3)**What does the marketer need to do?**
---------------------------------------------------------------------------------------------------------------------------------------------

*   marketers can generate affiliate links and send leads to them or they can fork the bridge web app and hardcode their referral address

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#why-would-buyers-use-the-referral-link-4)**Why would buyers use the referral link?**
-------------------------------------------------------------------------------------------------------------------------------------------------------

*   most buyers won’t even be aware of this program, since the marketers will reach out to them with a landing page that already contains the referral link.
*   but even the ones that are aware will likely use a referral link because they are incentivized to do so (1% bonus)

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#how-does-it-work-technically-5)**How does it work technically?**
-----------------------------------------------------------------------------------------------------------------------------------

It’s going to be much easier than setting up any tracking service:

*   the affiliate will provide a link to the bridge web app that contains a referral.
*   that’ll be saved in the user’s session and when a swap from wZNN to ZNN happens, the referral will be included onchain.
*   once it’s onchain, the orchestrator will see it, validate the affiliate’s referral address and distribute the affiliate’s share as ZNN.

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#so-all-users-must-be-sent-to-the-bridge-web-app-by-the-marketers-6)**So all users must be sent to the bridge web app by the marketers?**
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

If the affiliate wants to use a different landing page and not the bridge web app directly, which will likely be the case, then they just need to include a tiny code (probably an iframe or an image) in that landing page that will set the referral as a cookie for the visitor.

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#why-wouldnt-the-buyers-just-use-their-own-addresses-as-referrals-and-get-the-whole-3-7)**Why wouldn’t the buyers just use their own addresses as referrals and get the whole 3%?**
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

*   buyers who are not aware of the program, won’t even think about this possibility
*   buyers who become aware of the program won’t be able to easily get a referral address
*   if things get out of hand, there are technical solutions to prevent it and we’ll cross that bridge when we get to it

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#whats-next-8)**What’s next?**
------------------------------------------------------------------------------------------------

I’ll make a poll so we can decide on the fee.

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#will-it-launch-with-the-bridge-9)**Will it launch with the bridge?**
---------------------------------------------------------------------------------------------------------------------------------------

No, because it’s still WIP. But we need to set the fees right from the start.

[sumamu](https://forum.zenon.org/u/sumamu) May 9, 2023, 11:37am  18

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#read-the-discussions-before-voting-1)! Read the discussions before voting
--------------------------------------------------------------------------------------------------------------------------------------------

Fee percentage for swapping ZNN \> wZNN. The bigger the fees the more incentivize for marketers.

*   2%
*   3%
*   5%
*   8%
*   10%

Thanks for the clarification! I’m amazed how wonderful this mechanism can generate perpetual growth (marketing) for the ecosystem!

Imagine some twitter airdrop influencers take up this !

What is the typical fee in the industry [@vk\_stex](https://forum.zenon.org/u/vk_stex)?

THORSwap charges 0.30%. I think 2% is waaaay too high, people will complain.

![Image 113: Screenshot 2023-05-09 at 8.23.02 AM](https://forum.zenon.org/uploads/default/original/2X/e/ea83c0155f0b1893f076c76a62db1f514c9973c1.png)

[bayrum](https://forum.zenon.org/u/bayrum) May 9, 2023, 1:54pm  23

Let’s add “1%” option and maybe 0.5%

Spot taker fees are usually around .2 - .3%

In this case, however, fees feed a positive feedback loop to attract more buyers. Which is not the case when you pay an exchange for matchmaking.

You can’t compare the two.

[0x3639](https://forum.zenon.org/u/0x3639) May 9, 2023, 3:19pm  25

I voted 2%, but wish I could vote 1%. [@sumamu](https://forum.zenon.org/u/sumamu) do we have any examples of this in the wild where we can compare fees? Something more akin to a marketing fly wheel rather than fees paid in a CEX.

Overall I think this strategy is excellent. All these discussions about submitting AZs for posting on Twitter will go away. People who generate good contact will attract buyers and get rewarded.

Great initiative IMO.

Should [Zenon.Org](http://zenon.org/) fork it, integrate Attribute event into it (so the referrer can be tracked throughout his entire journey on any [zenon.org](http://zenon.org/) page), and parse the marketer’s built Attribute link zenon address so it can inject it as the referrer address dynamically? This way Attribute links also support paying marketers for referrals. The Attribute dashboard will also be able to show you how much your referred buyer swapped to ZNN so you can publicly show off the value you generated. We’d also create custom funnels for the entire flow to improve on the UX. The forked bridge would remain open sourced.

*   Yes, I would use the forked version + Attribute
*   Yes, but I wouldn’t use the forked version + Attribute
*   No

If one of our selling points is being a feeless network, I think this fee should be small, similiar to thorchain’s 0.3%  
Not sure though. If ppl could explain the pros and cons of 0.3, 0.5, 1? We do have AZ to pay marketers, so 2 seems excessive. I’m not an expert at this though.

[sol](https://forum.zenon.org/u/sol) May 9, 2023, 4:26pm  28

Interesting idea. I’ve got a couple questions/comments:

1.  How do marketers register their referral address?
    *   Will the referral code → zenon address lookup be performed on-chain or in an orchestrator-specific database?
    *   How does that information propagate to others running orchestrator code?
2.  I would be more comfortable with a 1% sell tax, split 67/33 or 50/50.
3.  Can the web app provide a referral form/field as well?
    *   In case users don’t access the page with a specific link
    *   Some people may want to manually enter the code when they swap
4.  Do you think this solution will be compatible with other wallets, like Syrius Desktop?

[sumamu](https://forum.zenon.org/u/sumamu) May 9, 2023, 4:55pm  29

A better question to ask [@vk\_stex](https://forum.zenon.org/u/vk_stex) is how much does it cost to aquire a new user and what is the average purchase of a user.

I understand that, but ever since I joined the community, most people complained about a lot of things, so that’s pretty much the norm. At least this time they can complain while the community is grown by this program and the WZNN price goes up.

Think of it this way, if the fee is too small for marketers to even consider it, the program will fail from the start, so it might as well be zero.

On point [@cryptocheshire](https://forum.zenon.org/u/cryptocheshire).

Exactly, everyone will be welcome and all results are verified automatically and rewarded.

The network will still be feeless, the swaps from WZNN to ZNN will also be feeless. The only fee is paid by sellers. Once a user sells, the incentives for that user to continue to bring value to the ecosystem drops, but at least with this fee someone else will be incentivized to bring value.

At first, they’ll just have to generate a short link with their address embedded. If things get messy and referrals find way to use that to cheat the system, then we’ll start adding conditions such as: holding at least X ZNN, having been a holder for at least X days, eventually having to submit an AZ proposal to get approved as a referral.

Everything will be onchain, verifiable and trackable.

The economical problem is that whichever fee is set initially will be the maximum fee that’ll ever be able to set. So it’s better to start with a higher fee and lower it as the price/WZNN increases than have the program fail from the start if the incentives are too low.

The fee remains in the bridge contract and the user doesn’t get the bonus for using the referral link. A banner can be displayed to the user to look for a referral link in order to receive the bonus.

It won’t be possible, they’ll have to use a referral link.

Sure, it’s onchain and everything should work on any wallet/platform if implemented correctly.

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#bonus-1)BONUS:
---------------------------------------------------------------------------------

Users in the community are rather experience and could register themselves as referrals, so that when they swap ZNN to WZNN to sell, they’ll still pay the fee, but if they don’t sell or buy back, they can use their own referral link when swapping the WZNN back to ZNN and have the entire fee refunded, as long as they return to the ecosystem.

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#reality-check-2)Reality check:
-------------------------------------------------------------------------------------------------

Let’s face it, even a 10% fee after a 5X is cheaper than a 0% fee after a -90%. ![Image 114: :wink:](https://forum.zenon.org/images/emoji/twitter/wink.png?v=12)

I voted 3%.

Keep in mind this only applies to using the multichain NoM bridge going from wZNN to ZNN. You could still find a buyer doing a P2P trade using an atomic swap directly within syrius in a trustless fashion.

Liquidity should concentrate around Orbital and the NoM bridge initially. But long-term, other liquidity-building solutions might ask for Orbital funds and become the main hub for ZNN trading.

[sumamu](https://forum.zenon.org/u/sumamu) May 9, 2023, 5:17pm  31

Even at this point Orbital can be extended to other liquidity solutions. As long as the user has a ZTS or another LP token that can be wrapped to ZTS, Orbital can allow them to stake it.

CAC per new retail trader for a big CEX ranges around $35 -$65

[sumamu](https://forum.zenon.org/u/sumamu) May 9, 2023, 5:25pm  33

Thank you, very good info! Now all we need is the average purchase value of a user and we could calculate a minimum fee at the current price of ZNN.

Is there a possibility for a dynamic fee which adjusts based on the size swapped?

[sumamu](https://forum.zenon.org/u/sumamu) May 9, 2023, 5:31pm  35

Unfortunately no. This whole idea came after the bridge PR was created so nothing was specifically implemented for it, but luckily somehow it fit perfectly.

How will we be able to detect cheating?

[sumamu](https://forum.zenon.org/u/sumamu) May 9, 2023, 5:41pm  37

At worst cheaters would get their own fee back, so there’s no incentive to cheat. It’s a zero-sum game.

Thanks for this benchmark. I can’t wait to see if I can beat that with clever inbound campaigns/channels.

Right thought the marketer spending budget on the acquisition could be losing. I will try to think of a way to see if Attribute can help here with some monitoring stats which can clue in on hijacking…

[sumamu](https://forum.zenon.org/u/sumamu) May 9, 2023, 6:01pm  40

Check this out:

If cheating becomes an issue, we’ll find ways to overcome it.

That’s hard to estimate. But if we assume retail crypto portfolios to be somewhere between 5k-50k and a per asset allocation of 5-15% of the entire pf, we’re at range of $250-$7500. This is how much on a rough average a retail trader would allocate to znn.

Sounds like for the average retail portfolio the acquisition buffer isn’t too high. A $7500 swap is only $15 commission. We have to also remember that even though we have to be inviting to newcomer marketers into the ecosystem, someone inexperienced and unwilling to experiment with his own cash / data tools upfront, may have a hard time to justify his budget to AZ. It’ll always be in the proof for me, and hence the need for pre-built conversion rate proven funnels aka what [zenon.org](http://zenon.org/) is attempting to build i.e. eliminating the complex architectural requirements to prove performance. Then marketers become awareness / remarketing drivers. Hopefully other performance marketers come around and build their own systems / funnels too.

[sumamu](https://forum.zenon.org/u/sumamu) May 9, 2023, 6:45pm  43

Traders can just hold WZNN during the trade. The fees only apply when swapping between ZNN/WZNN.

The fee only applied when swapping ZNN to wZNN.

Yes, but to get volume we need to reach out to new users. And marketing does that. As you can see we’re not getting any volume now and I haven’t seen much volume in the past 10 months since I’ve joined the community, so we need to start somewhere.

What’s the alternative?  
We keep chasing our own tail:  
we don’t grow \> we need marketing \> new marketer comes \> can’t prove results before getting funds \> can’t get funding to prove results \> marketer leaves \> we don’t grow

Oh right my bad, in that case 1 or 2% should be fine. I’ll edit my statement above

Yes, fully supporting this.

Right on the spot! We really need these types of mechanisms to ensure sustainable marketing for this project.

Well said ![Image 115: :clap:](https://forum.zenon.org/images/emoji/twitter/clap.png?v=12)

[0x3639](https://forum.zenon.org/u/0x3639) May 9, 2023, 7:06pm  47

Funny.

True

Good point. Increasing it will / could cause us to run out of ZNN. Maybe 1% is too low as I suggested.

Amazing. So LPs will not be punished. This entire proposal is very bullish IMO.

[0x3639](https://forum.zenon.org/u/0x3639) May 9, 2023, 7:16pm  49

I like 3% now. We can always go down from there and it costs LPs nothing. This will be a real incentive to market this project.

I think 3% is the sweet spot: not too low to dismiss the referral program, not too high to cause disruption.

For example, for a common $200 ZNN → wZNN swap the fee paid will be $6, enough to bring back 2 users into the ecosystem (and hopefully twice the value in $ terms that will flow back into the ecosystem).

[sol](https://forum.zenon.org/u/sol) May 9, 2023, 8:38pm  51

If you’re planning to be able to adjust this in the future, why not set the maximum fee to 10% and initialize a `currentFee` variable with the result of the poll?  
This way we can adjust based on the whole spectrum of the poll, not just the winning the result.

I don’t understand this limitation. Won’t the API only require the referral code anyways?  
What’s the difference between a referral code and a referral link?  
Syrius Desktop doesn’t support URIs yet.

[sumamu](https://forum.zenon.org/u/sumamu) May 10, 2023, 8:49am  52

Theoretically you’re right, but there’s a minimum delay between these changes, so it’s better to be set to a percentage that’s been agreed on.

The web app will only support referral links. If you are planning to implement the bridge interface in syrius you can allow users to just paste the referral link or a referral code.

[mr.ztark](https://forum.zenon.org/u/mr.ztark) May 11, 2023, 10:30pm  53

Not sure if I understand…

1.  What if the ZNN to wZNN lane has lower volume than the wZNN to ZNN lane on the bridge?
    
2.  If I want to bridge 1000 ZNN to wZNN when ZNN is $20, I’ll be looking at a $600 fee at 3%.
    

If I understand correctly, that’s offensive. I think the fee would have to be less than 1%.

How about a sliding scale?

Or…

How about something that utilizes protocol emissions to reward affiliates?

Lazy idea: Stake a bunch of ZNN from AZ for perpetuity and pay monthly $QSR to affiliates according to performance.

It doesn’t have any impact. The idea is to penalize exiting the ecosystem.

If you want to dump such a large amount, $600 is peanuts for you. Initially, I voted for `5%`. You’re penalized because you want exit the ecosystem. This means you have no interest left in this project. You will not contribute to this project anymore. Your sole purpose is to profit. Therefore, your `30 ZNN` fee (notice I didn’t use the $ value) will be on good hands: marketers, believers, ZNN maxies or even fellow aliens (with the help of the referral program) will make use of the funds to engage, attract and convert new participants.

Even businesses can charge 2-3% and no one is complaining about fees. And they’re charging you for every credit card purchase.

This can be implemented only into a sidechain. Another take: would you change protocol emissions for Bitcoin?

Here is my proposal for the `xZNN` fee mechanism:

I think this is a valid idea that should be taken into consideration. The only problem is that the `ZNN` `QSR` are locked into the A-Z embedded.

[0x3639](https://forum.zenon.org/u/0x3639) May 12, 2023, 10:51am  55

Alien is right. Look at sales tax. We pay 10% in certain markets in and around Chicago.

[mr.ztark](https://forum.zenon.org/u/mr.ztark) May 12, 2023, 12:02pm  56

I live in a tax free state and I don’t accept credit cards for this very reason. And ‘everyone’ complains about taxes. ![Image 116: :stuck_out_tongue:](https://forum.zenon.org/images/emoji/twitter/stuck_out_tongue.png?v=12)

[sumamu](https://forum.zenon.org/u/sumamu) May 12, 2023, 2:29pm  57

It’s not possible, because there can only be as much wZNN as was swapped from ZNN.

I’m not saying $600 out of $20000 is cheap, but…if this mechanism gets us there I don’t think many will complain. And imagine how incentivized marketers will be to attract even more users.

The fee can be lowered in the future if the community decides so, but it’s important to know that once the fee is lowered to a level, it can never be raised above that level ever again.

Any external incentives source will be make it profitable to abuse the mechanism.

Awesome!

The main objective of this mechanism is to provide a sustainable source for rewarding marketing efforts so the community can grow over time. Accelerator-Z does something similar for the builders of the ecosystem and it’s working.

How to shoot yourself in the foot. Setup a ridiculously high fee for crosschain txs. You guys are obsessed by marketing and forget that liquidity + volume is what gets you traction. I can’t wait to see influencers fighting for their shares of a ref links over a 100k liquidity market which will turn into a p&d fest.

[@sumamu](https://forum.zenon.org/u/sumamu) one issue I see is that if thevpenalty is too high it will disincentivize people from using wznn in the first place, especially if you add eth gas fees on top.

This could very well impact liquidity growth as [@dat\_she\_pepe](https://forum.zenon.org/u/dat_she_pepe) pointed out.

I know I also voted 3% but a smaller fee probably makes most sence. There is no shortage of funds to pay marketers. The shortage are marketers who actually know what they’re doing (or people who understand what effective marketing means)

Our focus should be on building liquidity and volume first and foremost.

There is a shortage of _liquid_ funds to pay marketers. AZ _cannot_ sustain everything because (unfortunately) is not replenishable. Luckily, this mechanism is _both auto-replenishable and scalable_.

The shortage are _marketers_. There is literally _no active marketing_ right now.

You forget that people that join the community and _buy_ gets you liquidity + volume. What **do you do** to attract and convert people?

It’s in the title: “_perpetual ecosystem growth_” ![Image 117: :man_facepalming:](https://forum.zenon.org/images/emoji/twitter/man_facepalming.png?v=12)

Like the team wisely said, _Acta non verba_

[sumamu](https://forum.zenon.org/u/sumamu) May 13, 2023, 9:49am  61

I’m all for getting liquidity + volume, I want this to be very clear. My experience simply happens to be that traction comes from marketing, retention from utility, volume from buyers and sellers and liquidity from incentivizing liquidity providers.

If what you’re saying were to be true, then we should already have liquidity + volume on STEX and it should’ve been there on Pancake Swap too.

That’s not the case, so what you’re saying must be incomplete.

Orbital is about to start, which will attract liquidity. Also, during the campaign, the rewards will be higher than ever, so it will likely attract even more liquidity.

For current ZNN holders there are 2 reasons to use wZNN:

1.  providing liquidity - and this case is even incentivized
2.  selling wZNN - which will happen if the price and/or liquidity are better than STEX

Now for the 2nd case, which is valid if the price and/or liquidity are better than STEX. That is likely to happen for the following reasons:

*   buying from Uniswap, 1inch or other DEXs doesn’t require the user to trust and deposit the funds on a CEX
*   the referral program will incentivize affiliate marketers to promote wZNN
*   Orbital program incentivizes liquidity providers if they lock their liquidity over a period of time, which means that wZNN will likely have a deep liquidity pool

The problem is not the shortage of funds, but the lack of a mechanism that accurately rewards marketers who actually bring added value to the ecosystem.

Sure we can go ahead and reward social interactions, onchain activity, wallet downloads and whatnot, but in the end, if we were to try and measure the success of these, we’d still look at how well we’re doing in terms of: price, liquidity and volume.

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#why-1)Why?
-----------------------------------------------------------------------------

*   Success in terms of price means the **price** is getting higher, which happens when someone buys.
*   Success in terms of **liquidity** means we have as much ETH in the AMM pool as possible, which again happens when liquidity is added (already taken care by Orbital) or someone buys.
*   **Volume** is the only metric that benefits from both buyers and sellers.

So the one common factor that measures the success of these 3 metrics is how much “buy” a marketer brings.

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#well-then-why-dont-we-use-the-same-mechanism-but-a-different-funding-source-2)Well then why don’t we use the same mechanism but a different funding source?
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

*   We could, but they wouldn’t be as sustainable as this one.
*   We could, but if we used another funding source, it would incentivize current holders to cheat the mechanism.
*   We could, but any other available funding source would penalize the holders and/or buyers instead of the sellers.

Orbital already does that and it’s not clear to me how a 3% fee would harm liquidity and volume.

*   A seller won’t sell anymore because of the 3% fee? I’d say that’s a win.
*   A liquidity provider won’t provide liquidity because of the 3% fee? But it gets refunded when the LP returns to the ecosystem.
*   A buyer won’t buy anymore because of the 3% fee? Buyers actually receive a 1% bonus to swap from wZNN to ZNN, that’s pretty much all they’ll know at that point.

[](https://forum.zenon.org/t/perpetual-ecosystem-growth/1417/print#conclusion-3)Conclusion
------------------------------------------------------------------------------------------

We could continue to argue or we could give it a try and see how it goes for a few months. If later we decide to lower the fee, we can do that, but if we lowered it from the start, we actually shoot ourselves in the foot because we won’t ever be able to increase the fee beyond that amount for the referral program.

[0x3639](https://forum.zenon.org/u/0x3639) May 13, 2023, 10:10am  62

This fee proposal is very different than a standard swap fee. I think we all have experience with those fees, and paying 3% to swap ERCs would be a nonstarter. I can tell you first hand the swap fees on THORchain are a big obstacle to adoption.

If you buy wZNN and then trade it on uniswap, you only pay swap fees on the CEX. This 3% fee will not impact trading in any way on Ethereum. The fee only impacts people who are exiting.

This is a novel approach to marketing that we have not seen before. Setting the fee too low will not give us the opportunity to test any price levels. And initially it will only impact LPs who will get it back upon repatriation.

Why run an experiment with no room to experiment? I voted for 3% but think it could be even higher - maybe 5%. Also, think about the incentives for the people responding here. If someone wants out, they want the fee as low as possible. And for those who want to experiment with the novel approach, setting a higher number likely makes sense so we can test.

Also wanted to point out that if you buy 100 wZNN and move it to ZNN you now have 101 ZNN. When you move it back to Ethereum you have about 98 wZNN (assuming no natural price movement). The net fee is 2% doing a round trip from ETH \> ZNN \> ETH.

Thanks for the explanations. I’m not dismissing anything. Just challenging some thoughts. A critical discourse should be acceptable either case. I am still supporting this, it doesnt mean I can’t question design decisions.

[sumamu](https://forum.zenon.org/u/sumamu) May 13, 2023, 10:15am  64

That was a general mention, it was not directed at you. Sorry if it seemed so.

Indeed, this is NOT a trading fee, nor a transfer fee. It only applies to swaps from ZNN to wZNN.

That’s right.

Wrong assumption at the begining. You get liquidity with PA and good incentives. AKA you market a clear and competitive APR. Stex is unknown and there’s 0 real trader going there. You only took what suit your views from what I said. Here’s the complete ELI5:

*   Outrageous fee will get you rekt

Why ?

*   Deep liquidity allows OI which allows a good PA people can actually trade and that’s your best marketing because THEY TALK. Some might even MM your asset.

Guess what ?

*   Zenon has non of those because it NEVER found a good way to incentive liquidity. No vampire campaign, no APR marketed on except on a bridge people that broke ridiculously on a chain which is perceived as the fruit farm one.
    
*   Here you have a way to do real marketing and not Twitter campaigns funded by the community money, campaigns that resulted so far with 0 effects. I guess being in a bear market should be an important information in decision making here.
    

[0x3639](https://forum.zenon.org/u/0x3639)

May 13, 2023, 4:31pm  66

If you don’t fuck around, you will never find out.

[![Image 118](https://forum.zenon.org/uploads/default/original/2X/f/f013145df7971aa2419f5a43a768f93067475536.jpeg)](https://www.youtube.com/watch?v=WntjAM2wqF8)

I am excited. Can wait for bridge to go live.

Interesting idea to use the fee only as incentive to attract potential zAliens. Personally I would be willing to pay 3% to convert ZNN to wZNN as it would be logical to enlarge the ZNN network. Although one could say being feeless is one of the pillars of ZNN. And it still is, just the bridge has a incentive fee. Good job guys ^^

The feeless property applies only when you’re within the ecosystem. The interaction with the embedded contract is indeed feeless: you can do `PoW` to send your `ZNN` to the `embedded bridge`. The actual conversion of `ZNN` to `wZNN` is an action that signals the intention of exiting the ecosystem, so the feeless property doesn’t apply anymore.

You are absolutely right, and I think that’s fair to ask for a fee to help the ecosystem. Thanks for the clarification!

Agree, worst thing that happens is people complain about the fee, this doesnt work, and we scrap it. Best thing is it gains traction and attracts people to ZNN. So seems like v little potential downside for v much potential upside. Dont see why we wouldnt try it.

[sumamu](https://forum.zenon.org/u/sumamu) May 19, 2023, 2:49pm  73

Thanks for taking the time to visit the forum and reply!  
It does seem great at least on paper and we’re very curious how things will turn out once it’s live.

[0x3639](https://forum.zenon.org/u/0x3639) May 19, 2023, 7:19pm  74

We could write a “liquidity black hole” article.

[https://twitter.com/Rewkang/status/1272631205263900672?s=20](https://twitter.com/Rewkang/status/1272631205263900672?s=20)

We should coin our own term.

Perpetual Marketing Machine  
Perpetual Community Engagement  
Perpetual Marketing Theory

Ideas / Suggestions?

[crack](https://forum.zenon.org/u/crack) May 19, 2023, 10:33pm  76

So what your idea?

[sumamu](https://forum.zenon.org/u/sumamu) May 20, 2023, 9:03am  77

Positive feedback loops are powerful, they can create exponential results.  
Luckily this concept is integrated in our mindset so it becomes part of what we build.

Perpetual Network Marketing Theory?  
Perpetual Multi Level Marketing Theory?

[0x3639](https://forum.zenon.org/u/0x3639) May 22, 2023, 2:44pm  79

[@mehowbrainz](https://forum.zenon.org/u/mehowbrainz) remember when that post came out for THORchain…

[sumamu](https://forum.zenon.org/u/sumamu) May 22, 2023, 2:47pm  80

How did it go?

Worked wonders, but Kang had an audience as well…

[0x3639](https://forum.zenon.org/u/0x3639) May 22, 2023, 3:12pm  82

ya he had a very large following.

We can buy a big shitfluencer

He need to be the right one. Not Gmak and others larps

Has to be a well-known Bitcoiner. But not a retard maxi. Udi or Erik Vorhees for example. Or Balaji. He’s tweeting 24/7 and angelo from our community knows him

You can’t buy Balaji, you can only make a strong case for Zenon’s value proposition and how that helps Bitcoin.

Thing is those dudes don’t need the money.

True, but find me one crypto shitfluencer with a bitcoiner audience who does

wb @aantonop

[![Image 119: image](https://forum.zenon.org/uploads/default/original/2X/a/a7c1be884030e7720f79a99b1ffece5e23598cc4.jpeg)](https://forum.zenon.org/uploads/default/original/2X/a/a7c1be884030e7720f79a99b1ffece5e23598cc4.jpeg "image")

He’s more than a maxxie though. Noway this dude is going to shill anything out of BTC when he’s been shilling it for free since ages

He was difficult on THORChain back in the day as well. I recall he blocked me. I don’t see him shilling anything but BTC.

I’m we need a usecase strong enough to be turned into a story telling for BTC but it’ll have to be 1) not just technical shenanigans and speculative assertions and 3) not just marketing buzzwords. It needs to be a simple clear usecase for BTC that make absolute sense. Then shilling will be much much easier

While you’re 100% right I think there’s a 1% chance this community can pull that off.

[tapwoot](https://forum.zenon.org/u/tapwoot) May 26, 2023, 12:36am  94

weak prediction

Historical data begs to differ. How’s the guy you funded doing?

Not going to apply for AZ, but I’m not going anywhere. Anticipating the launch of the bridge, and we’ll start to share some memes.

Suppose we have the intention to establish a business development and sales team to enhance our liquidity pools. Currently, we lack a system to financially reward or motivate these business development and sales professionals to successfully recruit new Liquidity Providers (LPs). Enhancing the depth of these pools is a crucial factor for attracting new participants into our network, which also influences the capacity of affiliates to facilitate large-scale wZNN purchases.

Napkin draft on enhancing ZNN’s value through the NoM Bridge / Affiliate Program:

Step 1) Campaign to Augment Liquidity Pools:

1.  A dedicated marketing team would be tasked with generating, qualifying, and warming up leads through the use of lead magnets. The effectiveness of these lead magnets can be assessed by tracking conversion rates using an [Zenon.Org](http://zenon.org/) funnels + Attribute.
    
2.  These prepped leads would then be channelled to sales teams for converting them into Liquidity Provider (LP) positions. Attribute can also be incorporated into the NoM Bridge’s “Add Liquidity” interface to monitor these conversions. As of now, the Affiliate program doesn’t offer rewards for referrals that result in new LP positions. Is it possible to change this? If not, should AZ consider providing the incentives? If so, how can AZ compensate these referrals without self-sabotaging (for example, to avoid an endless cycle of LP withdrawals and additions)?
    

Step 2) Campaign to Promote wZNN to ZNN Swaps:

1.  A marketing team would be tasked with generating, qualifying, and warming up potential leads through the use of lead magnets. The effectiveness of these lead magnets can be assessed by tracking conversion rates using an [Zenon.Org](http://zenon.org/) funnels + Attribute.
    
2.  These nurtured leads would then be directed to sales teams, with the aim of converting them into wZNN to ZNN swaps. Attribute can be integrated into the NoM Bridge’s “Bridge Tokens” section to monitor these conversions. While the Affiliate program does provide a reward for facilitating this swap, it remains uncertain whether the incentive is sufficient for sales professionals who deal with high-ticket sales. This is something we need to explore further.
    

IMO the art of growth here is a mix between clever calculators to display opportunities, education/demos, lead generation, automations / warming up / qualifying leads, spectacular sales/support and simplicity/beauty to make the whole look effortless. Scaling the whole will require an array of talent specializing in a variety of marketing, sales, biz dev and support. Crafting this will become my next obsession now that the Nuxt3 [Zenon.Org](http://zenon.org/) upgrade is completed (pending release shortly).

Critique please.

[@sumamu](https://forum.zenon.org/u/sumamu) what do you think of displaying the following information for the Liquidity Staking variant of the NoM Bridge?

*   Starting LP position weights + values in fiat
*   Current LP position weights + values in fiat
*   Impermanent loss value in fiat
*   Rewards earned + values in fiat
*   Total value compared to starting value in fiat

[sumamu](https://forum.zenon.org/u/sumamu) July 20, 2023, 2:18pm  99

For a napkin draft, it’s pretty well laid out.

That’s correct. It doesn’t offer rewards, but if a user swaps LP tokens and uses an affiliate link, this is still recorded onchain and the conversion can bet attributed to the affiliate.

Swapping LP tokens is feeless, so the affiliate program can’t distribute any rewards for that. However, since the conversions can be attributed to an affiliate, a separate program can use that info to reward affiliates who bring in liquidity.

If this separate program existed, it could use any source of funding as long as the rewards are distributed based on the amount and staking period of the LP tokens.

The affiliate program is currently distributing 1% to the user and 2% to the affiliate. This can be adjusted to 0% for the user and 3% to the affiliate without having to readjust the fees.

If the affiliates were to HODL the rewards, they might benefit from the snowball effect generated by their own efforts.

Down the road, if the community decides to increase the fees and the rewards for the affiliate program, the resulting discrepancies MUST be filled by an external source of funds, such as, but not limited to, AZ.

However, higher fees might discourage new users from joining the ecosystem given the fees they would face when exiting.

I do believe such information should be available since it could be an important factor for users deciding where to put their ZNNs.

I’ve seen the Zenon.tools calculator and it’s awesome. If [@vilkris](https://forum.zenon.org/u/vilkris) would be willing to integrate Orbital Staking and maybe even the affiliate program into Zenon.tools calculator and dashboard, I’d be willing to assist with the implementation and publicly support this as an AZ project.

Dumb question but why not creating a ZTS (with its equivalent bridgeable from ETH) meant to incentive a LP farm which would have boosted rewards on ZNN / ETH? Make it leveraged farming so maybe it can sustain a bit.

[0x3639](https://forum.zenon.org/u/0x3639) July 21, 2023, 1:35pm  101

I think the most important thing here right now is calculators and demos. Thinking back to the THORchain days, someone made an easy calculator that allowed people to post the LP yields on BSC. That started to fuel itself and then people started making tutorials and videos to support the effort.

[0x3639](https://forum.zenon.org/u/0x3639) July 21, 2023, 1:37pm  102

I was going to try and make something manually so I can automate posts like this. But anything I make will be totally goatastic and not usable by the “public”

[https://twitter.com/Learn\_Zenon/status/1682110801774092292](https://twitter.com/Learn_Zenon/status/1682110801774092292)

[vilkris](https://forum.zenon.org/u/vilkris) July 21, 2023, 6:18pm  103

I’ve started to look into what would be needed for the LP reward calculator.

[0x3639](https://forum.zenon.org/u/0x3639) July 21, 2023, 7:23pm  104

[@vilkris](https://forum.zenon.org/u/vilkris) this would be a very valuable to stimulate interest. Being able to generate a screen shot with “returns” or earnings to post to twitter could be great.

[0x3639](https://forum.zenon.org/u/0x3639) July 21, 2023, 7:25pm  105

check out this site: [THORYield](https://app.thoryield.com/dashboard)

The most important, basic function is being able to input a ZTS address and generate returns for that address and be able to share that with twitter. That is how THORyield started out.

I really like the `share to` idea.

[@vilkris](https://forum.zenon.org/u/vilkris) can you implement it for the calculator as well?

wen **ZNNyield**

[vilkris](https://forum.zenon.org/u/vilkris) July 22, 2023, 6:54am  107

I’ll look into that as well.

[bayrum](https://forum.zenon.org/u/bayrum) July 22, 2023, 12:28pm  108

Sooner or later liqudity providers will get crushed by low ROI and impermanent loss. In one week ROI went from 150% to 75%. I don’t see anypoint to get a deep pool with low ROI which can turn easily in -ROI and people posting high rewards picture without explaining that this can become a failed investment. Is our main goal attracting more liqudity providers?

I think the main goal is to attract more people in general. The community is still very small and any new people that come and stay should be welcomed. I also think we need to bring in a “critical” mass of new users in order to create a sustainable price increase in the short and medium term.

A simple casino game would do imo: A coin is flipped. Players get 50/50 odds to lose all their ZNN, and 50/50 odds to 5x their stack. That’s catchy. Could work with ETH and BTC too when the time comes. Need to be degen, high risk high rewards. Coin flip online. Simple casino for simpletons like me. ZNN holders could even get some fees. As well as the A.Z funds.

I agree gambling is highly addictive, but casinos require licenses and all sorts of legal stuff… I have some ideas for games of skill (as opposed to games of luck they are free from legal burden) that are addictive and can easily bring users, but I’ll focus at the moment on delivering the `ext-chain`.

Make it fully onchain so no legal involved. I’m a licenced degen so I can degen your idea, whatever it is.

Majority of tokens on eth are pure scams or gambling. As long as their L1 market cap is in the billions it will be called “adoption”

[0x3639](https://forum.zenon.org/u/0x3639) July 22, 2023, 8:50pm  115

can you please post the math to support this statement?

Yes. But again, unless you’re a boomer, you gonna love hamster gambling.

Dude hamster gambling sounds freakin lit

[0x3639](https://forum.zenon.org/u/0x3639) July 23, 2023, 1:56am  118

agree. sounds retarded and fun

[bayrum](https://forum.zenon.org/u/bayrum)

July 23, 2023, 1:45pm  119

[![Image 120: image](https://forum.zenon.org/uploads/default/optimized/2X/4/4c9f633e304157b887a08ca607bfce9b48401a78_2_690x352.jpeg)](https://forum.zenon.org/uploads/default/original/2X/4/4c9f633e304157b887a08ca607bfce9b48401a78.jpeg "image")

  

[![Image 121: image](https://forum.zenon.org/uploads/default/optimized/2X/f/fb22ea972c74ef311d280d35e6a53befc9c06b2d_2_690x393.jpeg)](https://forum.zenon.org/uploads/default/original/2X/f/fb22ea972c74ef311d280d35e6a53befc9c06b2d.jpeg "image")

One week ago 0.019 ethlp.  
Staking 1000znn + eth= 3200 znn anual return = 160% ROI

Today 0.030 ethlp.  
Staking 1000znn+ eth = around 1850 znn anually = 92.5% ROI. I miscalculated with 7.5%.

[DrD3](https://forum.zenon.org/u/DrD3)

July 23, 2023, 3:41pm  120

[![Image 122: Screenshot 2023-07-23 at 5.38.22 PM](https://forum.zenon.org/uploads/default/optimized/2X/8/8d147ee1d74a56ab8f75d429f3ab8306633e29b0_2_690x187.png)](https://forum.zenon.org/uploads/default/original/2X/8/8d147ee1d74a56ab8f75d429f3ab8306633e29b0.png "Screenshot 2023-07-23 at 5.38.22 PM")

I meannn someone did go and add nearly a fourth of the total liquidity we have on Uniswap ![Image 123: :man_shrugging:](https://forum.zenon.org/images/emoji/twitter/man_shrugging.png?v=12)

What I’m curious to know is how quickly we’re going to drain 10% of Orbital’s reserves as a consequence of this.

It’s ZenonORG’s position.

[DrD3](https://forum.zenon.org/u/DrD3) July 23, 2023, 5:39pm  122

Thought so ![Image 124: :wink:](https://forum.zenon.org/images/emoji/twitter/wink.png?v=12)

[0x3639](https://forum.zenon.org/u/0x3639) July 24, 2023, 3:00pm  123

I think the hope is to get more LPs who stake for 12x so we can deepen the liquidity pool. [@sumamu](https://forum.zenon.org/u/sumamu) did a calculation estimating the duration. Let me look for that.

[crack](https://forum.zenon.org/u/crack) July 24, 2023, 10:55pm  124

Sumamu said about 58 days if 2x multiplier applied (constant), currently about 1,7 x

Prototyping a calculator for LPs.

[vilkris](https://forum.zenon.org/u/vilkris) July 29, 2023, 7:18pm  126

An initial version of the calculator is now live: [Zenon Tools](https://zenon.tools/calculator/liquidity)

[sumamu](https://forum.zenon.org/u/sumamu) July 30, 2023, 10:02am  127

Amazing work as always, [@vilkris](https://forum.zenon.org/u/vilkris)! The quality of your work speaks for itself.

First preview of my LP Simulator… I lost some brain cells building this one ![Image 125: :alien:](https://forum.zenon.org/images/emoji/twitter/alien.png?v=12) ![Image 126: :gun:](https://forum.zenon.org/images/emoji/twitter/gun.png?v=12)

Written thanks to a mix of GPT 3.5 + GPT 4 + maths + [ZenonHub.io](http://zenonhub.io/) APIs + Uniswap GraphQL requests.

Goals of the tool:

1.  Allow upcoming LP’s to calculate their rewards.
2.  Allow upcoming LP’s simulate what their rewards will be with pool growth, wZNN, ETH price changes.
3.  Allow current LP’s to calculate their rewards after a new LP enters, and values are simulated in 2).
4.  Allow for anyone to play with their imagination and see potential in Zenon.
5.  Act as an inbound lead generation tool. I will likely use a sign up form to capture basic info for anyone interested in playing around with it.

Confidence of the tool:

1.  95% confident. Will be testing quite extensively. Won’t release it until I validate it further.
2.  I’m aware that the current reward formula is not spot on. I’ve been chatting with [@sumamu](https://forum.zenon.org/u/sumamu) and messaged [@vilkris](https://forum.zenon.org/u/vilkris) to discuss. I’ve implemented [@sumamu](https://forum.zenon.org/u/sumamu)’s formula, but I get a different result than when using zenon.tools’ calculator, will get to the bottom of the issue. It’s not a major problem. The hard part was to calculate the `ZNNETHLP Share Percentages`.

May create a new tab with a simplified view where the user just enters 3-4 values and will see the results in big numbers. This view could be the “detailed” calculations view.

[![Image 127: Screen Shot 2023-08-01 at 10.43.51 PM](https://forum.zenon.org/uploads/default/optimized/2X/e/edc629eb7bd9676687fda32a11cae176cb733d34_2_617x500.png)](https://forum.zenon.org/uploads/default/original/2X/e/edc629eb7bd9676687fda32a11cae176cb733d34.png "Screen Shot 2023-08-01 at 10.43.51 PM")

It’s slightly improved / simplified here. Will add another toggle to hide/show existing LP rewards.

[https://twitter.com/mehowbrainz/status/1687247043863937024?s=20](https://twitter.com/mehowbrainz/status/1687247043863937024?s=20)

What’s the plan with the LP rewards after the first 12 months are finished?

[DrD3](https://forum.zenon.org/u/DrD3) April 17, 2024, 9:40pm  132

Fair point- when does the first year lapse again?

Theres about a month and a half until 1 year lock ups start to open.

The rewards are coming from emissions dedicated to LP so they shouldnt change unless we decide to, like add more lp pools or vote to stop. [@sumamu](https://forum.zenon.org/u/sumamu) could confirm here though.

ZenonOrg may be removing its LP position at the end of its 1 year lockup period.

Chadass Capital will remove its LPs at the end of the one year lockup period.

Yield go up ![Image 128: :slight_smile:](https://forum.zenon.org/images/emoji/twitter/slight_smile.png?v=12)

[0x3639](https://forum.zenon.org/u/0x3639) May 14, 2024, 6:06pm  138

DeeZ will not be removing liquidity.
