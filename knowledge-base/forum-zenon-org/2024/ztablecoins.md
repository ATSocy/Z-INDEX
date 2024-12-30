Thread: ztablecoins
angelo_a_jr | 2023-06-22 15:54:32 UTC | #1

Opening a thread here about what kind of stablecoin options we could put forth natively from NoM.

I know BTC is the backbone of NoM but a stablecoin gets into the capillaries of crypto ecosystems a lot better

Some early ideas:

USDZ (USD on NoM) - obviously not decentralized but high brand awareness

zDAI

Currency basket on NoM https://en.wikipedia.org/wiki/Currency_basket

Personally I'm bullish on the concept of a stablecoin based on the global competitive electricity price like Meter (https://docs.meter.io/overview-of-meter/mtr-the-metastable-coin)

@LegalZNN would love to get your thoughts here as well

-------------------------

dat_she_pepe | 2023-06-22 16:38:21 UTC | #2

There are a lot of ongoing research and experiment on stable coins so it could be interesting to allow the big ones to be swapped 1:1 

USDC
USDT
DAI
FRAX
LUSD
BUSD

I'm looking for more information related to the (non scam) algorithm based ones that could be forked for a native stable on NoM. This could be game changer. MTR is a good start. Allowing the old ones to be swapped 1:1 could attract liquidity at start though.

-------------------------

aliencoder | 2023-06-22 19:45:44 UTC | #3

I would go with `USDT`, `USDC` and `DAI` first.

-------------------------

aliencoder | 2023-06-22 21:21:29 UTC | #4

[quote="dat_she_pepe, post:2, topic:1516"]
This could be game changer.
[/quote]

If you find the game-changing algo, we can code it into an `embedded contract`. Protocol level stablecoins :face_with_hand_over_mouth: (or at least inside the extension-chain where we have more autonomy).

-------------------------

cryptocheshire | 2023-06-23 07:42:21 UTC | #5

We shouldn't epresent individual stables one by one on NoM. This unnecessarily fragments liquidity for trading pairs and forces users to diversify their stable exposure to minimize depeg risk.

Instead, we should create a basket of different reputable stablecoins and tokenize it with USDZ. USDZ can then be redeemed for the underlying stablecoins which can then be sent to issuers to burn and convert to FIAT. We could even go one step further and make the basket allocation dynamic based on the USDZ holders' redemption demand for the underlying stablecoins (usdt, usdc, frax etc).

This way USDZ becomes a synthetic stablecoin that just represents an IOU on an actual, likely regulated, underlying tokenized USD.

This model also allows to eventually move away from a single asset peg to a multi asset basket peg that can be structured to be inflation resistant by including tokenized assets other than just for USD.

-------------------------

dat_she_pepe | 2023-06-23 22:09:02 UTC | #6

I disagree with all your point. USDT and USDC (or even DAI) are a must on everychain because a lot of big player want to hold the ones they trust, not another random unknown basket and therefore this has to be seen as a liquidity bridge, not a danger of dilution. Do you think projects will swap their funds for a newly released basket of stables the day they fork on the NoM? No. Their pool will remain the same, their conservative habbits will remain the same.

-------------------------

cryptocheshire | 2023-06-23 21:18:03 UTC | #7

I disagree with your face

-------------------------

dat_she_pepe | 2023-06-23 22:09:47 UTC | #8

The idea of a basket based stable coin down the road is good though. Even, even, even if you're fat.

-------------------------

zyler9985 | 2023-06-24 07:09:43 UTC | #9

Don't try anything fancy guys. Algorithmic stablecoins caused a financial disaster last yr which disgraced many influencers/devs and exposed them as dangerous idiots. Just leaving this here to reinforce the principle of going for safety and simplicity
![Screen Shot 2023-06-24 at 3.04.23 pm|636x500](upload://8tTIrxbE5GYVRjbAtSXatohuxO6.png)

-------------------------

dat_she_pepe | 2023-06-27 14:35:12 UTC | #10

Copy pasting an interesting answer I got at Lobster here : 
![IMG_20230627_163357|335x500](upload://oVDz1tY6KyPG0awfnJarGOHyIHG.jpeg)

Edit: aliencoder doesn't sleep lol, reacted within seconds

-------------------------

aliencoder | 2023-06-27 15:21:30 UTC | #11

The single most important thing for stablecoins is to try maintaining the peg if they trade under the $1 value.

Collateral backed stablecoins will always have the problem of the underlying value of that collateral during uncertain market conditions: "the price of Malt will move from 1 dollar towards the intrinsic value of the collateral". They have 2 strategies:

- One of these strategies involves the Swing Trader using collateral to buy back Malt
- The other involves a public auction to raise funds for Malt repurchase, subsidized by liquidity extension

I don't understand the second strategy: why would I add more liquidity (collateral) during uncertain periods?

-------------------------

cryptocheshire | 2023-06-27 22:38:39 UTC | #12

The main challenge with usd stables are the fiat rails. USD rails are literally cut off from the rest of the world right now. USD correspondant banks will not transact for crypto businesses. Minting/Redeeming stables requires corporate relationships with Circle or Tether (USDC, USDT). There is literally no way for this community to have an anon rail to fiat pegged stables. There is a war happening between the SEC and CFTC because of FTX (SEC will win) and it's the reason why banks have stopped doing anything for crypto businesses.

Also dont forget that most stables are permissioned and can be frozen at will of the issuer.

Source: it's my job to know

-------------------------

cryptocheshire | 2023-06-27 22:40:02 UTC | #13

That said: Swiss Franc is a completely different story and what we should consider. If we focus on USD vased trading pairs we're gonna have a hard time.

-------------------------

dat_she_pepe | 2023-06-27 23:56:06 UTC | #14

This is all speculative. Beside, USDT and USDC or DAI would only require a contract on the NoM side and a way to bridge from ETH. 

Let's see what happen and follow the actual real useful liquidity rather than our wild imagination, the one that could be leading us to SWITZERLAND and very bad cheeses (and 0 liquidity).

-------------------------

cryptocheshire | 2023-06-28 05:28:22 UTC | #15

It may feel speculative if you don't know what's going on in the industry. I assure you the USD situation is very real.

-------------------------

dat_she_pepe | 2023-06-28 14:47:59 UTC | #16

I assure you the cheese situation is very real too. All I see is where the liquidity is and projects are built.

EDIT: offering 1:1 bridge to the biggest USD stables doesn't exclude having the cheese money in. We can do both.

EDIT2: you don't need to mint / redeem. You need to wrap. You don't need any corporate relationship for that.

-------------------------

LegalZNN | 2023-06-29 21:21:29 UTC | #17

Hello. Thanks for tagging me here.

I'm not an expert in stablecoins, so I can hardly make specific suggestions at this moment. However, I'll do my best to follow the developments of this discussion and give my opinion when possible.

At this stage, I can say that international organizations such as the FATF and the IMF have published papers related to Stablecoins. However, I'd say the best framework to follow would be the papers published by the [Global Blockchain Business Council](https://gbbcouncil.org/). They have published several papers on best practices, standards, and recommendations for improving trust in the blockchain world. They've published a paper called "[Principles of Stablecoin Issuers](https://www.gdf.io/wp-content/uploads/2020/12/Principles-for-Stablecoins-Refresh.docx.pdf)" as part of their suggested Cryptocurrency Code of Conduct. This paper covers many considerations from different perspectives, including the regulatory perspective.

I'll follow this discussion and research more to see how I can add my 2 cents.

Best,
Legal

-------------------------

dat_she_pepe | 2023-06-29 23:22:57 UTC | #18

I don't think anyone want to issue anything and, instinctively, the safest path would be wrapping.

Nobody tagged you though. Thank for the contribution nonetheless.

EDIT: the axioms of regulatory absolute compliance needs to be questioned.

-------------------------

