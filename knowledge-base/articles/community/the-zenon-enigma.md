Title: The Zenon Enigma - Shai Mohaban - Medium

URL Source: https://medium.com/@shaimo/the-zenon-enigma-782f8b293bd6

Published Time: 2019-12-07T16:49:48.122Z

Markdown Content:
[![Image 9: Shai Mohaban](https://miro.medium.com/v2/resize:fill:44:44/0*TE97EaXAvm1_1MnM.jpg)](https://medium.com/@shaimo?source=post_page---byline--782f8b293bd6--------------------------------)

\[Disclaimer: This is not an investment advice. The below is my own personal experience and opinions. I don’t personally know anyone from the Zenon team, nor their identities, and am not affiliated with the project in any way\]

![Image 10](https://miro.medium.com/v2/resize:fit:700/1*TPMwpu73B5aFISsx7eOliQ.png)

The Bitcoin whitepaper was published by “Satoshi Nakamoto” in 2008 and started the blockchain revolution. Over the last decade the new emerging crypto space have experienced a dazzling growth with thousands of “projects” popping up, peaking with the ICO craze of 2017–2018. Most projects tend to follow the same pattern — a team comes together, publishes a whitepaper detailing the technology, token metrics/economics, team’s experience, etc, and tries to raise funds to get the project rolling. I think it’s fair to say that almost all the projects in the crypto landscape are mediocre useless me-too’s at best and pure money grab scams at worst.

But here and there a gem is spotted. Enter Zenon…

Zenon is a project which was first exposed publicly in March 25th 2019 with a [Bitcointalk article](https://bitcointalk.org/index.php?topic=4281633.msg38564494). A few days later I was lucky to learn about it through some random tweet by someone I follow on Twitter. I joined the Zenon community that first week and did a deep research on the existing materials. Since then it has been the project I’m most intrigued with. In this article I will outline why I think Zenon is unique and different.

**_“Product” maturity at launch_**

Most projects start with a whitepaper and some vaporware and often take months or even years before delivering anything (if at all).

Zenon launched with a working blockchain. There was a wallet ready for all the common platforms (Mac, PC, Linux), an explorer, a nice looking website, and everything one needs in order to get started. And the only way to describe the onboarding experience was… SLICK. The website was beautifully designed. The colors of the logo, the explorer, the wallet UI, the BTT article, all perfectly matched. Somebody put a lot of thought into this before it was made public…

The one caveat about this “product” (and why I put it in apostrophes) is that the first phase of Zenon, as outlined in the BTT article, is really just a fork of PIVX, used as a placeholder to bootstrap the community, initialize the decentralization of the network building blocks, and attract the first set of loyal “pillar” holders, while the next and important phase, the Network Of Momentum (NoM), is being developed. And yet, it’s non trivial and not something that you see often.

**_Fund “raising” mechanism — the xStakes_**

Most projects raise funds by having “investors” send them cryptocurrency, usually ETH, and sometimes also fiat money, and receiving in return tokens/coins either on the spot or later when the tokens are generated or when the network is launched. In the last couple of years the fund raising scene has been evolving with projects raising funds in multiple tranches with different conditions and terms, lockup periods, vesting mechanisms, different token prices, etc. This often ends with a complicated ugly unfair process resulting with many unhappy investors.

Zenon did none of that. They came up with an innovative unique mechanism called xStakes. A new comparable mechanism is now known as “Lockdrop”, and was recently also used by e.g. [Edgeware](https://edgewa.re/lockdrop/). Another similar approach is the “[WorkLock](https://blog.nucypher.com/the-worklock/)” by [NuCypher](https://www.nucypher.com/). The basic idea is that the participants send their funds to some sort of a smartcontract, and in return get their tokens. The participants are then expected to adhere to some predefined conditions in order to qualify to receive their funds back from the smartcontract over a period of time.

In the case of Zenon, one is required to run a network node (on the temporary Zenon network) where the collateral is ZNN coins that were received as a result of sending the funds. xStakes are paid monthly over a period of 2 years (or until the NoM is ready, whichever comes first). In essence this creates an active community of loyal supporters that have the incentive to run their nodes and be part of the network in its first phase.

**_Bitcoin Smartcontracts?_**

The plot is thickening. Zenon only allowed participants to send BTC. Using the wallet (a separate “ZX” tab), a participant had to generate a fresh BTC address and then send the BTC to it. It also asked the participant to provide a return BTC address to which the monthly xStakes will be sent (or a refund in case the cap was reached). As a result of sending the BTC, ZNN coins were sent to the wallet address (5000 ZNN for every 1 BTC), and the participant was then expected to lock them up as collateral for running a Zenon node.

The process of sending the funds, receiving the coins, creating the collateral for running the node, and earning node and staking rewards were all seamlessly integrated into the wallet from day 1 and worked very smoothly. Zenon called the algorithm behind the entire process including the xStakes distribution the “ZX Algorithm” (ZX for Zenon xStakes).

Although there is no proof, and the team would not confirm anything, I would dare to bet that some sort of smartcontract mechanism involving Bitcoin and crosschained to Zenon was used here. First, the entire loop here of generating a fresh BTC address, sending the BTC to it and receiving the ZNN coins was almost certainly automatic without any manual intervention. Adding to that, the conditions required to qualify for the xStakes distribution are also with a very high probability checked automatically and are cross chained between Zenon and Bitcoin — one has to look at the UTXO outputs used as collaterals for nodes, making sure they weren’t spent, that they originated from BTC that was sent, and that a correct Zenon block height was reached. And maybe the most intriguing part — in the coming months after the network launch there were a couple of cases of people accidentally spending their collateral and thus losing their xStakes. The team which is generally very helpful and supportive could not help. I suspect that if this was some simple software running off some database or spreadsheet, then the team would go ahead and fix the individual issue, e.g. by re-locking new collateral instead of the spent one, but it really appeared like they have no way of fixing it, hence my guess that some sort of smartcontracts are involved…

**_Limited time and cap for fundraising_**

The initial ZNN coins were generated over 14 cycles of 24 hours each, up until block 20160 (blocks in Zenon are every minute). There was a hard cap of 4.5M ZNN which was not reached (around 2.5M were generated). At block 20160 the ZX tab forever vanished from the wallet and you could no longer send BTC to generate new ZNN.

The team could have easily extended the distribution phase in order to raise more funds but they didn’t.

**_Zero marketing efforts_**

During the initial distribution phase there was absolutely no effort made by the team to attract new contributors. The small community (around 30 when I first joined) was built 100% by word of mouth. Even up till this day even the little outbound activity that does take place is community driven. Even the recent [Awareness Campaign](https://zenon.network/awareness) was a result of community members asking the team to try and attract more people before the Pillar lockup phase (more about that below).

The team could have easily used the slick website and product and spend more time bringing more contributors into the initial fund raising phase, but they didn’t.

**_Riddle_**

During the initial distribution phase the website presented a cryptic riddle in the form of 5 wallets named after 5 byzantine generals (BFT anyone?), each leading to a stash of ZNN to be won. Solving the riddle required reading very deeply, sometimes up to the letter, all the provided materials (BitcoinTalk article, lightpaper, website, tweets) and also doing lots of guessing plus cryptic puzzle work. It was very challenging and very intriguing (and I personally solved 4 of the 5, with the last one tricking me for 3–4 sleepless nights). This was a unique experience with, again, a lot of thought behind it.

**_Whitepaper Academic review_**

Most crypto whitepapers are nothing more than a flashy PDF with lots of graphics and illustrations to make a project look attractive in the eye of a naive investor. Very few whitepapers contain any novel technological info. Zenon is planning an academic level whitepaper that will also be peer reviewed by the research community. While this is still just a promise, the team has delivered on all of their other promises to date…

**_Professional handling of network issues_**

During the 6 months of the network existence multiple exploits were discovered in the general pivx codebase allowing hackers to affect how network rewards (nodes and staking) were distributed. This affected most if not all existing PIVX forks including Zenon. It took a bit of time to mitigate each of the issues but the team did it in a very professional way and restored the network to a healthy fair state.

**_Pillars phase_**

While the initial network was focused on PoS nodes, Zenon from the start targeted the 2nd phase which is the distribution of Pillars. This is detailed upfront in the [Bitcointalk article](https://bitcointalk.org/index.php?topic=4281633.msg38564494) and is creating the foundation for the NoM. That phase [started](https://medium.com/@zenon.network/pillar-lock-in-phase-de5b7d89b130) (with a slight delay due to the network issues mentioned above) at block 365670 and is currently ongoing until block 385920 (a period of about 2 weeks).

When first reading about it in the early days, this also seemed like a mysterious phase. Why even bother with another phase after nodes? How would xStakes carry into pillars? How would pillars be used in NoM? How many pillars will there be? Why limit the number of pillars and not allow additional ones to be locked later? How can a pillar be transferred to a new owner?

Some of these questions are being unraveled now as the community is growing and more and more members are setting up pillars (there are over 120 at the time of writing). Yet new questions emerge — what are those “development voting rights” that pillars will have? How would pillars participate in the upcoming NoM testnet?

**_Anonymous team_**

The Zenon team remains anonymous. That fact alone must have deterred many individuals from ever getting involved in the project. Many if not all crypto investors were affected by costly scams at some point, and most have become very suspicious of every new project, and rightfully so.

Still the fact is the team chose to remain anonymous, and most likely that will never change. There could be many reasons for that choice. One is to avoid personal liability. Another is to avoid regulatory issues (governments can try and stop Facebook’s Libra, but they have no way to stop Satoshi Nakamoto if they don’t know who he is). And yes, this can also be to scam people. Though one have to wonder how bad you have to be at scamming if you went through all these developments and efforts as outlined in this article, just for a small amount of funds, that you didn’t even bother to try and maximize and that you are giving back via xStakes. Just too funny…

**_Network Stability Fund (NSF)_**

As detailed in the BTT article, during the initial distribution phase, the team set aside 1.5% of the coins to build nodes to initiate the network and keep it stable. Once enough nodes were setup by the community these initial nodes were no longer required and the team tore them down so all node rewards will go to the community members. Moreover, the NSF is being distributed back to the community. The team has been sending periodic amounts of ZNN to all running nodes every month or so. They have also used small part of the NSF for the pillar awareness campaign.

**_Funding_**

As mentioned above, the initial funding was really just a lockdrop mechanism and the funds have been flowing back to the initial contributors (8 xStakes out of 24, or about 1/3 of the initial funds raised, have been sent to date). To be eligible to receive xStakes one had to send a whole BTC (or multiple BTC). Any smaller amounts are thus supposedly held by the team, which is likely not very much, given the small raise to start with (around 2.5M ZNN were distributed so around 500 BTC were contributed).

So here is a mystery — how is the project funded?

It is even more of a mystery if you recall that a lot of effort and development took place prior to the fund raising. When Zenon was first published in March 2019 it already had everything ready, including the wallet and network running, the website, all brand identity materials, a lightpaper, detailed plan outlined in a bitcointalk article, etc.

My guess — some commercial company is behind the project.

**_Brand and identity_**

As already described above, from day 1 the project’s look & feel was absolutely slick. If you take another look at the logo you will notice the ZN letters in any direction and any orientation. The logo looks like a pillar. It looks like it’s built on 3 columns (the 3 nodes it’s composed of). The animations on the website are beautiful. The wallet is very smooth. The explorer looks good and uses the same colors. A lot of thought went into the branding and early outbound materials. This is very rarely the case with crypto projects.

**_Team interaction_**

If you ever joined a crypto project Telegram group you surely experienced poor English, spam, clueless admins who are just there to control the community and relay messages to the team, etc. Zenon is different.

Every single Zenon team member I have interacted with (and I had long discussions with many of them, especially during the riddle days) are clearly native English speakers. I would dare to guess North Americans (US/Canada). They are all also very nice and polite. And they are very knowledgeable and apparently tech savvy. Setting up a node is no rocket science, but many crypto folks have no previous experience in creating a VPS, installing software from the cloud on Linux, etc. The team has been very patient and helpful throughout the different phases, and “customer support” so to speak is simply astounding. Did we say corporate America?

An interesting anecdote is that the team will often point you to the BTT article or lightpaper instead of directly chewing the info for you. They really want you to do your own research and almost all info is indeed included if you just care to read more carefully.

**_Bitcoin focus_**

Zenon has that rare smell of Bitcoin OG material:

-   The project was announced through a single simple post on [Bitcointalk](https://bitcointalk.org/index.php?topic=4281633.msg38564494)
-   Fund raising was with BTC only
-   xStakes used to send back BTC to contributors
-   Bitcoin smartcontracts?
-   Academic level peer reviewed whitepaper
-   A set of short educational [articles](https://medium.com/@zenon.network) about Blockchain building blocks
-   The team said they will introduce a new type of DLT which is not Blockchain nor DAG

**_Corporate America smell_**

A number of factors lead me to believe that some (potentially large) corporate is behind Zenon:

-   Focus on branding, look & feel and UI from the outset. Anyone who have ever worked for a US company knows these are considered extremely important when building or launching a company or a product, pretty much from day one.
-   Highly trained and communicative team
-   Outstanding customer support
-   Virtually no funding

**_Community_**

Given the mystery and uniqueness of Zenon as outlined in this article, along with some persistent [rumors](https://cdn.discordapp.com/attachments/597130295547920385/624219224881102869/moonpaper_1_final_extended_2.pdf) (that I will not address here), the project gradually attracted a very unique community. There is an official [Telegram channel](https://t.me/zenonnetwork) and a [Discord server](https://discord.gg/cygwWT3). There is a Telegram [OTC group](https://t.me/znnotc) (not very active as nobody seems to be selling at current levels). And there is a community driven Discord server, called the [Zenon Cult](https://discord.gg/bRQJNA) (and for a good reason…)

The day-to-day admins are community members, while the team members popping up when needed (e.g. when there is a network upgrade or other changes that require their support such as before the pillar lockup phase). There are no bots and no spam and most of the discussion is civilized and to the point. I’m a member of dozens of Telegram channels and I think Zenon is the only one which I did not permanently mute.

**_Conclusion_**

If you read this far it should be very clear to you that Zenon is not your typical crypto project. Sure, the team still needs to deliver even just the whitepaper, not to mention the actual NoM. And we know next to nothing about the actual technology and future network.

But all the above clearly proves the following:

-   The team didn’t do this for the money (they got almost nothing and did no effort to get more, while distributing back the little that they did get)
-   The project is backed by some other resources, most likely some corporate
-   The team is very knowledgeable and professional
-   There is innovation coming (Bitcoin smartcontracts, pillars, new type of DLT, academic backed technology)
-   The team is delivering on all their promises until now (8 xStakes delivered like clockworks, move to pillar is happening as we speak, whitepaper and testnet on track).

With this it only remains to imagine where we can go if the team indeed continues to deliver. I don’t know about you, but I can’t wait for next year!

@shaimo1000
