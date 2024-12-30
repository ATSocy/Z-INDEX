Thread: global-adoption-a-user-experience-and-regulatory-effort
mehowbrainz | 2023-06-22 17:08:46 UTC | #1

As I'm building towards a [funnel framework](https://forum2.zenon.org/t/landing-page-funnel-framework/1494/3) designed to onboard participants into NoM, I keep reminding myself that the user experience is what'll enable that Global Adoption.

Let's imagine a funnel experience where the user is offered to swap from DOGE to ZNN with a single click. No need to go to THORSwap, then bridge the wZNN.ETH to ZNN as a separate process. Everything done as one function, without KYC.

Assuming it can be done using [THORSwap's SwapKit API](https://docs.thorswap.net/aggregation-api/swapkit-api) and the [Multi-chain bridge](https://bridge.mainnet.zenon.community) code, what stops us from designing the easiest onboarding experience into ZNN/QSR? Web3 sanctions regulations.

The design would have to take into account a semi-regulated route, using Special Economic Zones (SEZ) for the party designing, implementing and hosting such experience. Examples of such SEZ's: [Próspera](https://www.rfsa.hn/ptc), [CDEZ](https://catawbadigital.zone) (USA-based). In the case of Próspera you can negotiate the terms directly with the regulator i.e. KYC-less swaps in-and-out of ZNN. They likely would require some transaction screening system to be implemented (screening wallet addresses against sanctions list) using tools like Merkle Science or Chainalysis. If something hits a blacklist, it would need to be banned/reported. There's likely a best-practice framework out there.

I'd like to introduce everyone to @LegalZNN:

Lawyer and expert in AML/CFT & Sanctions Compliance and Regulations for the crypto space.
He holds several international certifications, publications and participations as speaker in the matter. He's advised international companies and crypto projects ensure they're not engaging in operations outside their risk appetite.

While I was contributing to THORChain, I had done an extensive amount of sanctions compliance research alongside @LegalZNN for a THORChain interface project we wanted to launch (but eventually let go).

Anyone in the community is welcome to collaborate with him for their projects.

The opportunity for such project may exists today thanks to the various tools available (WalletConnect integration, THORSwap SwapKit, Multi-Chain Bridge). Once we get some metrics from funnels, we'll be able to evaluate whether a simplified workflow could improve conversions. Building the Killer Funnel is very important to onboard many segments of the market.

-------------------------

angelo_a_jr | 2023-06-20 20:33:10 UTC | #2

On a regular cadence working with the CDEZ founder here, happy to deliver the plan when ready.

-------------------------

dat_she_pepe | 2023-06-20 20:59:20 UTC | #3

I don't see the point. But I'm smol brain.

-------------------------

mehowbrainz | 2023-06-20 21:11:03 UTC | #4

Landing page user experience one:

1. "Want native ZNN? You need to go to THORSwap to buy wZNN.ETH with your BTC, please come back when you're done, I'll tell you what to do next.".
2. "Okay you came back, thanks so much. Okay now you need to go to the multi-chain bridge to swap that wZNN.ETH into native ZNN. Let me know if you figure it out.".
3. "Did you do it? Yes, okay now connect your syrius desktop via WalletConnect so we can propose you Pillars to delegate-to".

Landing page user experience two:

1. "Want native ZNN? No problem, let's connect you to syrius desktop with WalletConnect"
2. "Enter how much native ZNN you want to buy with your native assets".
3. "Done, your native ZNN has been purchased and bridged, see your balance here. Would you like to delegate?"

-------------------------

angelo_a_jr | 2023-06-20 21:21:19 UTC | #5

In both scenarios, how would the Syrius installation onboarding take place as a prerequisite?

-------------------------

mehowbrainz | 2023-06-20 21:24:20 UTC | #6

The user is asked to install syrius desktop as one of the starting steps of the funnel. The idea is to minimize the amount of steps, and I think that given we have the tools we should be looking ahead to streamline experiences as much as possible.

-------------------------

angelo_a_jr | 2023-06-20 21:34:04 UTC | #7

Makes sense.   Wdyt it would add to the build-out time to do both and A/B test them via Optimizely, Google Optimize, or something similar?  

Or a way to create the page such that it is lightweight enough to test a bunch of combos through A/B tests.

-------------------------

mehowbrainz | 2023-06-20 21:47:41 UTC | #8

Yeah the variation testing is typically used to test in-page element changes. In this case it's a totally different experience, so we'd probably be looking at drop off / abandonment rates. We can assume that an embedded all-in-one experience would probably perform much better.

-------------------------

vilkris | 2023-06-21 19:58:14 UTC | #9

Could you elaborate on what the regulatory issue is with implementing a frontend that utilizes the SwapKit API for example?

Are you primarily referring to issues with US regulators?

-------------------------

mehowbrainz | 2023-06-21 20:07:39 UTC | #10

Interfaces (when it comes to DEXes) have responsibility to abide to AML/KYC regulations of their jurisdiction. The regulators say: well we want to make sure that no sanctioned country individual uses your swap interface for illicit activities. You need to screen the users and block any coming from XYZ country, and for other countries you should be monitoring the addresses transacting through your interface.

Every jurisdiction is different, there is no rule of thumb. Crypto-friendly SEZ are starting to appear.

@LegalZNN feel free to chime in.

-------------------------

sumamu | 2023-06-22 05:10:36 UTC | #11

[quote="mehowbrainz, post:10, topic:1508"]
@LegalZNN feel free to chime in.
[/quote]

Bullish

-------------------------

vilkris | 2023-06-22 06:08:54 UTC | #12

@LegalZNN Do you have any insight on using third party swap widgets on a website to allow users to swap tokens?

I've previously used this swap widget by Rubic on my website: https://docs.rubic.finance/integrate-widget/rubic-relay-widget

Uniswap also has a swap widget that you can embedded into your website: https://docs.uniswap.org/sdk/swap-widget/guides/getting-started

Anyone can easily embed such a widget into their website with a few lines of code and allow users to do swaps.

Some time ago I made an inquiry to the regulator about using third party swap widgets like this and they basically said that I'm not under any legal obligations since I'm not the one forming a customer relationship with the user, the widget provider is.

But what is the difference between a third party widget and a third party SDK in this context?

-------------------------

angelo_a_jr | 2023-06-22 20:50:00 UTC | #13

Latest PR on CDEZ; good to see coming from Bitcoin Magazine:

https://bitcoinmagazine.com/legal/catawba-nation-is-seeking-seasoned-banking-regulators-for-bitcoin-friendly-jurisdiction

-------------------------

LegalZNN | 2023-06-29 21:02:55 UTC | #14

Hello, **vilkris**. Thank you very much for your question.

It depends on the regulator. Most regulators are taking a conservative approach to this, to the point that VASPs will eventually have to comply with tighter restrictions than Traditional Finance institutions. Due to this, VASPs are no longer in a "regulatory grey area" or an "unregulated space" as we were a couple of years ago. The exception would be the Special Economic Zones (SEZ) regulators, who are open to discussing regulations directly with the projects.

There are still places with little regulation, and that is true. However, as we aim for a global audience, we must either: comply with the highest standard so we don't get in trouble or get used to banning and restricting access to an evergrowing amount of jurisdictions to the point that the projects stop being global. I prefer the first scenario.

Jurisdictions aim to implement [FATF's Guidance on VASP](https://www.fatf-gafi.org/en/publications/Fatfrecommendations/Guidance-rba-virtual-assets-2021.html), which is the most important document for forecasting what will be regulatory landscape look like. Points 67 to 70 of the guidance would be key here.

As a rule of thumb, all customer-facing businesses must, eventually, comply with KYC/KYB and Transaction Monitoring, and this requirement extends to traditional technology providers that influence customers' funds and their safety, such as Wallet Custody Service Providers. But going back to your specific question, when you embed a widget, you're controlling the range of options the customer has for their swaps/operations, so it could fall within the case of Point 67:

> 67. A DeFi application (i.e. the software program) is not a VASP under the FATF
> standards, as the Standards do not apply to underlying software or technology (see
> paragraph 82 below). However, creators, owners and operators or some other
> persons who maintain control or sufficient influence in the DeFi arrangements, even
> if those arrangements seem decentralized, may fall under the FATF definition of a
> VASP where they are providing or actively facilitating VASP services. This is the
> case, even if other parties play a role in the service or portions of the process are
> automated. Owners/operators can often be distinguished by their relationship to
> the activities being undertaken. For example, there may be control or sufficient
> influence over assets or service'scts of the service’s protocol, and the existence of
> an ongoing business relationship between themselves and users, even if this is
> exercised through a smart contract or in some cases voting protocols.

For code/API/SDK, the customer-facing person or entity would be responsible for the functioning and operation of the actual application. A rule of thumb would be that there's always somebody who has to comply with regulatory requirements.

Let me know if this was helpful or if there's any other point you'd like me to go more in-depth.

Best,
**Legal**

-------------------------

mehowbrainz | 2023-06-29 23:28:30 UTC | #15

Welcome @LegalZNN and thank you for joining the conversations. Feel free to check out some of the other mentions of your handle in the forums, I think I've seen one or two others!

-------------------------

mehowbrainz | 2023-06-29 23:38:51 UTC | #16

I have a question for you @LegalZNN: Off the top of your head without going too deep into research, how do these guidelines apply for applications like [peer-to-peer (p2p) swaps](https://forum.hypercore.one/t/the-p2p-revolution-p2p-swaps-in-syrius/108)? It's an initiative one of the HyperCore teams is working on.

-------------------------

vilkris | 2023-06-30 09:16:17 UTC | #17

Thank you for the detailed response. Very insightful.

[quote="LegalZNN, post:14, topic:1508"]
For code/API/SDK, the customer-facing person or entity would be responsible for the functioning and operation of the actual application. A rule of thumb would be that there’s always somebody who has to comply with regulatory requirements.
[/quote]
Does this mean that websites such as Etherscan.io would have to comply with these regulatory requirements, since you can use their website to interact with smart contracts to trade assets?

[quote="LegalZNN, post:14, topic:1508"]
However, creators, owners and operators or some other
persons who maintain control or sufficient influence in the DeFi arrangements, even
if those arrangements seem decentralized, may fall under the FATF definition of a
VASP where they are providing or actively facilitating VASP services. This is the
case, even if other parties play a role in the service or portions of the process are
automated. Owners/operators can often be distinguished by their relationship to
the activities being undertaken. For example, there may be control or sufficient
influence over assets or service’scts of the service’s protocol, and the existence of
an ongoing business relationship between themselves and users, even if this is
exercised through a smart contract or in some cases voting protocols.
[/quote]
Isn't this a very ambiguous statement? How is an "ongoing business relationship" defined for example?

If jurisdictions aim to implement these FATF guidelines, aren't SEZs in risk of being determined to have "weak AML/CFT frameworks", as stated in paragraph 107, and thus run the risk of being cut off from VASPs in countries with strong regulations?
> In addition to P2P transactions, the FATF has identified other potential risks which
> may require further action, including; VASPs located in jurisdictions with weak or
> non-existent AML/CFT frameworks (which have not properly implemented
> AML/CFT preventive measures) and VAs with decentralised governance structures
> (which may not include an intermediary that could apply AML/CFT measures).
> These risks may require countries or VASPs to identify VASP- or country-specific
> risks and implement specific safeguards for transactions that have a nexus to VASPs
> and countries lacking in regulation, supervision, or appropriate controls based on
> these risks. These risks are particularly heightened if there is mass-adoption.

-------------------------

dat_she_pepe | 2023-06-30 15:04:36 UTC | #18

It would be great not to rely on one single self proclaimed legal expert. Also, again, if you want to follow the Bitcoin ethos, are you really willing to follow Gensler's guidelines? Find loopholes.

-------------------------

angelo_a_jr | 2023-06-30 16:42:39 UTC | #19

Vilkris is simply asking follow-up questions to another respondent who is being generous with their time and prior experience so we can learn more about how they view the situation.  There's nothing implied about reliance on new insights surfaced here in a civil manner.


Fortunately NoM seems to already account for your weight in some of these topics.
![Screenshot 2023-06-30 at 12.35.51 PM|689x131](upload://igdFKxdJOQVDZcWsQk8x7dwDFeH.png)

-------------------------

dat_she_pepe | 2023-06-30 17:10:38 UTC | #20

I'm being very civil. I don't care if people spend time giving what could be misleading advices: we cannot seek more views at the moment and Zenon is well known for the cultish behaviors of its community. Distribution of trust is better than what you and mehow desperately try to enforce. As for my pillars, they don't share rewards with people like you and will never do. I however feel like this is off topic and you're just lost here, seeking for advices you'll end up following without being able to put them in perspective. Fortunately you don't have any voting rights at all on the NoM: no matter of the weight, I do have a voice, remember that.

Zenon has wrongly branded itself as a Bitcoin ethos driven project. Let's see how it plays in regard to regulators following Gensler guidelines.

-------------------------

mehowbrainz | 2023-06-30 17:14:39 UTC | #21

[quote="dat_she_pepe, post:20, topic:1508"]
Distribution of trust is better than what you and mehow desperately try to enforce.
[/quote]

May you elaborate.

-------------------------

dat_she_pepe | 2023-06-30 17:22:19 UTC | #22

I'm scared of this community reaction when a single person pops in with the aura of an expert. Aside of that the regulators and the whole crypto world have very different roots and political views. I'm worried about the whole scene following every guidelines without even putting on a (legal) fight.

I'm not questioning LegalZNN skills or knowledge here, but if crypto wants to carry more of what it was, there's a need for more thinking about what we want and what we do.

-------------------------

mehowbrainz | 2023-06-30 17:40:21 UTC | #23

[quote="dat_she_pepe, post:22, topic:1508"]
I’m worried about the whole send following every guidelines without even putting on a (legal) fight.
[/quote]

This is a great comment, I'd love @LegalZNN to shine some of his opinion on why this could work, or backfire on a project. And does he have an example of success and failure stories.

[quote="dat_she_pepe, post:22, topic:1508"]
if crypto wants to carry more of what it was, there’s a need for more thinking about what we want and what we do.
[/quote]

@LegalZNN how do you see the long term sustainability of the loophole paths? What's your outlook on this fight for the industry?

-------------------------

aliencoder | 2023-06-30 17:53:43 UTC | #24

[quote="dat_she_pepe, post:22, topic:1508"]
when a single person pops in with the aura of an expert
[/quote]

I have to agree with @dat_she_pepe here, regardless of the domain (dev/marketing/etc).

[quote="dat_she_pepe, post:22, topic:1508"]
the whole crypto world have very different roots and political views
[/quote]

Like every other (big) industry.

[quote="dat_she_pepe, post:22, topic:1508"]
I’m worried about the whole scene following every guidelines without even putting on a (legal) fight
[/quote]

Exactly: look at Coinbase now.

[quote="dat_she_pepe, post:22, topic:1508"]
there’s a need for more thinking about what we want and what we do
[/quote]

Well said, again.

-------------------------

cryptocheshire | 2023-07-01 00:17:22 UTC | #25

Coinbase has irreparably damaged itself by going against regulators. The only thing we can and should do is to become as ungovernable as possible through decentralization.

-------------------------

angelo_a_jr | 2023-07-01 02:47:07 UTC | #26

In the purely digital sense I agree with this sentiment and Bitcoin fulfilling its fate as the global reserve currency.

But the world is more than just currency and requires interfacing with TradAPIs.  Take the notion of "Bitcoin-Powered Network States" from the Zenon Org pages which I'm basically trying to create a version of at build_republic.  This requires real estate.  Unless we want to live in the metaverse it requires a lot of traditional interfacing.

Zooming out on the Coinbase situation they may have done damage in US but now they are playing jurisdictional arbitrage with other countries like UAE rolling out red carpets for them.  It's the same tactic a BTC miner would move their equipment around for cheaper electricity, Coinbase is instead just shuffling legal teams and jurisdictions for ease of business.  CZ/Binance has been playing this game for ages and we all benefit from the service for liquidity.

This could, should, and will likely turn into a long-running debate and challenge but the way forward is going to be in the weeds.  As long as we're matching philosophical alignment with a pragmatic strategy, we'll get there.

-------------------------

cryptocheshire | 2023-07-01 06:40:44 UTC | #27

The real estate is still  managed and owned by legal or natural persons/entities/DAOs that are subject to laws. But the consensus layer these assets are being transferred by (or where the ownership provenance of assets is being authenicated & recorded) is   as trustless as bitcoin and should remain so.

-------------------------

cryptocheshire | 2023-07-01 06:42:22 UTC | #28

CZ is a persona non grata in UAE and Coinbase has to be careful too because UAE doesn't want to sour relationships with US over some crypto punks :)

-------------------------

dat_she_pepe | 2023-07-02 00:56:04 UTC | #29

[quote="cryptocheshire, post:28, topic:1508"]
a in UAE and Coinbase has to be careful to
[/quote]

CZ was in Dubai not so long ago.

-------------------------

cryptocheshire | 2023-07-02 06:22:16 UTC | #30

So was my bald neighbour. You can take my word for it, it's my job to know. Or don't, idc

-------------------------

dat_she_pepe | 2023-07-02 13:05:50 UTC | #31

Why would he be banned from Dubai like hewwo from all alt rights TGs?

-------------------------

cryptocheshire | 2023-07-02 15:03:45 UTC | #32

Same reason. He didn't know his place lol

-------------------------

dat_she_pepe | 2023-07-02 16:32:39 UTC | #33

Do you have a source for this? Because really, a few weeks ago he was there.

Even if you're trustable, you have your own biases.

-------------------------

coinselor | 2023-07-02 16:33:53 UTC | #34

I think there is room for both point of views, they seem very valid to me. I'm almost never in agreement with Chadasss, but he sounds particularly convincing in his arguments on this topic.

If we follow the bitcoin ethos, we truly care about the principles underpinning the base layer, but the products built on top can (and should) do whatever is necessary to bring them to market in a compliant fashion. 

I encourage builders like vilkris to dig deeper and figure out their legal responsibilities. And I equally encourage the chadass type alien who does not want to package our base layer with said legislation and prefer finding the loopholes and workarounds that better fit their believe system.

Zenon should (like BTC) remain agnostic to any specific country legislation.

-------------------------

