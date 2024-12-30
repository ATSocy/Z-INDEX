Title: Extension Chains: smart contracts for NoM

URL Source: https://forum.zenon.org/t/extension-chains-smart-contracts-for-nom/1512/print

Published Time: 2023-06-21T13:04:24+00:00

Markdown Content:
**WHAT ARE EXTENSION CHAINS?**

I see extension chains as sidechains (think of a layer-2 solution similar to [Liquid Network](https://docs.liquid.net/docs/technical-overview)) that complements and enhances NoM (with smart contracts) and has the following properties:

*   Allows users of the `ext-chain` to move `ZTS` tokens between the two networks with a `two-way peg`. `ZNN` used in the extension chain is referred to as `eZNN`/`xZNN`, and each `xZNN` has a verifiably equivalent amount of `ZNN` secured by the _Extension Consensus Group_: **ECG**.
    
*   The **ECG** is operated & governed by a (sub)set of `Pillars`. With no single entity in control and a geographically diverse membership, there is no single point of failure - similar to how `orchestrators` work. Also `Pillars` have strong incentives to grow the ecosystem and will be additionally rewarded in `xZNN` to run & manage the extension chain infrastructure (via a fee sharing mechanism). We can re-use some implementation details from [@sumamu](https://forum.zenon.org/u/sumamu)’s multi-chain technology.
    
*   We can adopt the [peg-in](https://docs.liquid.net/docs/technical-overview#peg-in-bitcoin-to-liquid) and [peg-out](https://docs.liquid.net/docs/technical-overview#peg-in-bitcoin-to-liquid) mechanisms from Liquid.
    

**WHY EXTENSION CHAINS?**

In my opinion this type of sidechain implementation that can bring `EVM`/`WASM` compatibility for NoM will greatly expand the ecosystem. As Mr Kaine already emphasized, extension chains are the fastest way to bring smart contracts to NoM. And we really need `EVM` compatible smart contracts to grow the ecosystem. Moreover, the base layer remains minimal & efficient as Mr Kaine strongly suggested and all the heavy work/bloat is kept in a separate execution domain.

**ARCHITECTURE DESIGN**

Pillars are the largest producer of `ZNN` inflation in the network. They also run `orchestrator` nodes for the bridge. It makes sense for them to also act as validators for the `ext-chain` where fees are paid in `xZNN`. It is important to note that the `ext-chain` cannot produce additional/separate inflation.

Users, Pillars and every other network participant can `peg-in` funds into the `ext-chain` to benefit from smart contracts for example. We can also incentivize/penalize `ext-chain` users via `peg-in`/`peg-out` fee similar to [@sumamu](https://forum.zenon.org/u/sumamu)’s affiliate fee. It is up to the `ext-chain` deployer make this decision.

`ZNN` is not a gas token because the `ext-chain` will use a wrapped representation of it. It can be called `eZNN` or `xZNN` (execution ZNN).

As I already mentioned earlier, we can re-use parts of [@sumamu](https://forum.zenon.org/u/sumamu)’s bridge and tweak them to support this type of wrapping. If we go with the burning fees, it would be a little bit different from wrapping `ZNN` to `wZNN` and unwrapping it later because `xZNN` will actually be consumed/burnt in the `ext-chain` (it won’t be a 1:1 backing).

`xZNN` can be associated with the gas concept for the `ext-chain`.

_BUILT-IN POSITIVE FEEDBACK LOOPS_

Since there won’t be any inflation within the `ext-chain`, we must rely on a fee distribution mechanism.

That’s why I propose the following fee distribution mechanism:

*   33% distributed to builders (contract deployers)
*   33% distributed to **ECG** (`ext-chain` validators)
*   34% burned (similar to ETH)

This single piece of ingenuity attracts builders which in turn attracts users.

I’ve already investigated [Canto](https://canto.io/) and why it mooned: they’ve implemented the “golden” fee mechanism (`contractDeploymentFee`).

Users will bridge/swap/convert `ZNN` for `xZNN` through an embedded contract (eg `ext-chain-embedded`) in order to be able to use their favorite dApps that will be run on the `ext-chain` (for example Unizwap, games, meme tokens, NFT collections, etc.).

Users will be required to pay gas fees to interact with the `EVM` smart contracts. Therefore, they will pay/consume `xZNN` and it will be redistributed according to the specified percentages directly by the system contract to the contract deployer, burn address and **ECG** (`ext-chain` validators).

_Positive feedback loop_:

```
More users => more activity => higher gas fees => more `xZNN` gets consumed => higher payouts for builders & validators => less ZNN in circulation
```

A win-win-win situation for the whole ecosystem.

The embedded that will convert `ZNN` to `xZNN` needs to be carefully designed, because there won’t be a 1:1 backing (we need to take into account `xZNN` burning).

**WEN EXTENSION CHAINS?**

I’m already working on a testnet that will go live during sometime during Q3 2023. I plan to release a fully functional mainnet release by the end of Q4 2023 or sooner.

Will extension chains be faster in term of confirmation time and throughput than the base layer? Also people talk a lot about L2 being less secure, can you elaborate about that when it comes to ext-chains and the NoM?

Great questions, zir!

So far I’ve achieved `>1000tps` with deterministic finality (1 confirmation required). I have other good news, but I want you to see it with your own eyes first.

We trade-off security and decentralization (of the base layer) for scalability & smart contracts (on L2).

What does the copying the burn accomplish on an L2?  
If there’s another extension chain that does 50% to contract, 50% to validators, all things being equal, why won’t people choose that chain instead?

Make `ZNN` more scarce.

This is up for debate.

I’m not questionning your design here but I’m really curious about how sidechains and L2 works in general. In this case, can you go deeper (if you have time) about how the tradeoff works? How the validation works etc.

Sidechains are a type of L2 (eg Liquid Network). Payment Channel Networks (PCNs) are another type of L2s (eg Lightning Network).

A sidechain is basically another chain that can have different consensus, validator set, etc. and interoperate with the L1 via different mechanisms (in this case the `peg-in`/`peg-out` mechanism).

Yes, I’ll compile a list with trade-offs and what design we should approach.

On a sidenote and for better UX I’d say that txs should be send seemlessly between L1 and sidechain. A different address structure would probably exists but I’d advocate for a transparent bridge interaction.

Definitely. `EVM` requires `secp256k1` so the addresses will be different for sure.

What do you have in mind? We can change the name `wrap` and `unwrap` to move across extension chains, but you’d still need to wait for confirmations to move funds between the L1 and the `ext-chain`.

What I meant is that from a user perspective it would be WAY more simple to copy paste the ext chain address and send over there without interacting with the bridge UI if they don’t want to. Less clicks. Better experience overall. Bring a popup about fee and confirmation to keep them informed but it’d be a better UX for those who seek for simplicity.

Can you check how [Avalanche is doing this](https://support.avax.network/en/articles/4058262-what-is-the-contract-chain-c-chain)? They have a similar [concept](https://support.avax.network/en/articles/6077308-what-are-the-differences-between-the-x-p-and-c-chains).

I think Harmony has this kind of trick too, with different kind of address but it’s transparent for the user.

Thinking from a positioning standpoint for the sake of marketing/comms, does this proposal essentially allow us to say you can “launch your own chain on NoM” in its final form?

This seems to be the way the market is headed:  
[https://twitter.com/yiryan/status/1671635818732040193?s=46&t=i2nSc9tNKGroSzBMw8\_UiQ](https://twitter.com/yiryan/status/1671635818732040193?s=46&t=i2nSc9tNKGroSzBMw8_UiQ)

Exactly. Extension chains will inherit some security properties from NoM, and in the future, from Bitcoin.

Amazing. This might be the perfect use-case for buildcities. Each city its own token, the entire ecosystem its own chain

Can’t wait for that last part

Super excited for this as well. Will the extension chain have its own name?

Alpha Centauri – it’s the closest star system to earth, and this Zenon sidechain is EVM compatible and therefore the closest alien ecosystem to crypto space/humans

No please don’t bring more cringe scifi thanks

[0x3639](https://forum.zenon.org/u/0x3639) June 23, 2023, 3:07pm  20

THORchain had all these crazy mythical names that were hard to say, remember, and type.

Look at the top 20 names. They are all easy to remember, say, spell, and type. Much better.

you’re an uncultured fatty  
let’s just name it “extension chain” to amplify the “if autism was a blockchain” theme we have going

I would like to discuss the extension chains fee structure further: why is it a bad choice to make it feeless and if there’s fee wouldn’t it be interesting to make dApps pay or decide of a custom fee structure? I came across an interesting article about how Chromia is doing it : [The Power of Customizable Fee Structures](https://blog.chromia.com/the-power-of-customizable-fee-structures/)

Where did you read this? The extension chain won’t be feeless.

How?

Customizable fees can be a future milestone.

Sorry, excuse my English. I meant why not making it feeless.

As for the fee structure I refered to dApps being able to control it but not only the distribution. Ad you can read on the Chromia article and docs a dApp can decide there to handle the fee aka buying upfront the necessary tokens to run the product and pay for users + can charge fee anywhere they want while letting certain kinds of tx free from fee if they wish to do so. I don’t know how the Chromia network allows this at a deeper level but it could be attracting for users depending on the product. They are focused on gaming for now with one good game already available on Steam (not the usual crypto crap).

I also think I missed the why an extension chain needs fee, hence my initial question followed by an exemple of a different way to handle the fee in allowing different business perspectives and models to unfold.

EDIT: with the structure suggested above we could for exemple imagine pillars or other entities sponsoring dApps with QSR, ZNN or plasma, opening a brand new market and models for business fully onchain.

Is it possible that it will just end up being the decision of the deployer how to incorporate fees into any future extension chain?

The bridge already appears to get a succesful effort from pillars to run the orchestrators so with the right dApps/business model any extension chain could be profitable enough, by means outside of tx fees, to the point of easily being able to incentivize pillars to participate as validators on the chain. In principle it does push things a little further away from decentralization and security of the L1, but the might be worth the tradeoff for the benefits of feeless txs.

Seems like it will depend on the application. Do these extension chain have this kind of flexibility?

Incentivize validators to spin up nodes, builders to develop smart contracts and passively every NoM user by burning `ZNN`.

They only need `xZNN` to run on the `ext-chain`.

Another interesting topic is revenue sharing: dApp contract deployers/businesses sharing fee revenue with their users.

Yes.

It is up to the `ext-chain` deployer to setup the fee structure.

Making good progress with the `ext-chain`.

Still need to test the `EVM` smart contracts, but we’re getting closer and closer to launching an initial `devnet`.

[0x3639](https://forum.zenon.org/u/0x3639) July 7, 2023, 9:54pm  29

#bullish

[![Image 91: 20230811_181032](https://forum.zenon.org/uploads/default/optimized/2X/4/4ac120f62023f942aee2d7d72f905959d43aee77_2_690x388.jpeg)](https://forum.zenon.org/uploads/default/original/2X/4/4ac120f62023f942aee2d7d72f905959d43aee77.jpeg "20230811_181032")

As you can see activity decreases with each L2.

How can our Extension chain stand out? We don’t even have a significant volume in our base chain and bridge.

We don’t want our extension chain to be just another one in the long list or DOA , do we?

Incrementally superior blockchains cannot compete with network effects of earlier, technically inferior ones.

To outpace it and break rheough competitor’s network effects, a new DLT must provide a revolutionary advantage.

See Google vs Bing vs GPT

All the other L2 are eth only related though. Plus, we’re in a giga bear market. What ultimately matters is the NoM. The L2 is a way to allow people to build easier and onboard faster. Not the core of Zenon.

[Stark](https://forum.zenon.org/u/Stark) August 14, 2023, 4:08pm  33

I just got off a call with someone who literally asked for this. They key is that the EVM is running on Zenon infrastructure and that it brings more awareness to the long term of the NoM. There are life forms out there who can appreciate what we’re building.

*   Since the NEAR-to-Ethereum Relayer only sends NEAR block headers to the Ethereum LiteNode every 16 hours, there’s a 16 hour delay between steps one and two when moving tokens in that direction. (Remember, this is because Ethereum gas fees make it prohibitively expensive for the Relayer to update the LiteNode on _every_ block.) There are a number of approaches that would allow us to reduce this delay, and the team is actively working on that.

We don’t have this issue on NoM. Transaction are feeless as long as there is enough PoW generated for the transaction containing the block headers.

**Frequency of NEAR Blocks Transfer:** NEAR blocks’ headers are sent to Ethereum only once every 4 hours due to the expensive gas fees on the Ethereum network. This can result in a total transfer time of up to 8 hours, including the block transfer and a challenge period.

PS: Aurora is Near’s EVM chain.

Added extension chains to the upcoming refactored release of [zenon.org](http://zenon.org/) ![Image 92: :slight_smile:](https://forum.zenon.org/images/emoji/twitter/slight_smile.png?v=12)

[![Image 93: Screen Shot 2023-08-22 at 6.15.33 PM](https://forum.zenon.org/uploads/default/optimized/2X/9/9241413019da6feebdf6407a811e40b0cf86c0fe_2_690x309.png)](https://forum.zenon.org/uploads/default/original/2X/9/9241413019da6feebdf6407a811e40b0cf86c0fe.png "Screen Shot 2023-08-22 at 6.15.33 PM")

The first EVM compatible extension chain is now live ![Image 94: :alien:](https://forum.zenon.org/images/emoji/twitter/alien.png?v=12) ![Image 95: :flying_saucer:](https://forum.zenon.org/images/emoji/twitter/flying_saucer.png?v=12)

How to connect an EVM compatible wallet to the `ext-chain`:

1.  Install [Metamask](https://metamask.io/)
2.  Create a new wallet
3.  Go to `Settings` → `Networks`

*   Network name: `XZNN`
*   New RPC URL: [https://ext-testnet.zenon.community](https://ext-testnet.zenon.community/)
*   ChainID: 73405
*   Symbol: `xZNN`

4.  Post your address below and request `xZNN` for testing. Maximum amount is `10000 xZNN` per user.

[nbd](https://forum.zenon.org/u/nbd) September 2, 2023, 9:08pm  37

0xa9720C65C9a5B441a9093115beBC6545cfd12723 will take one of these 10k xZNN plz ![Image 96: :slight_smile:](https://forum.zenon.org/images/emoji/twitter/slight_smile.png?v=12)

[nbd](https://forum.zenon.org/u/nbd) September 2, 2023, 9:10pm  39

Received. Thankz

[SugoiBTC](https://forum.zenon.org/u/SugoiBTC) September 2, 2023, 9:18pm  40

Woohoo!! Congratulations on the launch zir!

I would like to request 10k xZNN on this address: 0x3BB6aD1345f6996Fad3053691Da0Bd0f60D6150E

WAGMI ![Image 97: :sunglasses:](https://forum.zenon.org/images/emoji/twitter/sunglasses.png?v=12)

Can I have some to deploy stuff? 0xFbE94cDa4dA0Dc19905b9c266FD52d6Dcb9d41A8

[7nzalh](https://forum.zenon.org/u/7nzalh) September 2, 2023, 9:53pm  43

Counting on the needful, zer ![Image 98: :saluting_face:](https://forum.zenon.org/images/emoji/twitter/saluting_face.png?v=12)  
0x6449BBA6bAa8eb500f30CD177001D97605eF4a70  
thank you.

[DrD3](https://forum.zenon.org/u/DrD3) September 2, 2023, 11:30pm  44

Requesting 10000 xZNN cap’n- 0xFED6f3314AF4704839C42086C1af66006be48516

[sol](https://forum.zenon.org/u/sol) September 3, 2023, 12:57am  45

Congratulations! Excited to try it out! ![Image 99: :alien:](https://forum.zenon.org/images/emoji/twitter/alien.png?v=12)  
Will we be able to run testnet nodes/validators?

0x6354FE81d95aDb5d69Fd76608Ca562B2eDAee671

Looking forward to trying it out, thanks.

0xDb87DFe0bBD6bd5e8650d5c84c94E66C5CAB3FfE

[DCZenon](https://forum.zenon.org/u/DCZenon) September 3, 2023, 2:36am  47

Send it zir!

0x293961591c9Be20447CD10e50c4B8d98Ea755Cfa

mEGAbULLISH

Some xZNN plz My addy below  
0xbFe4891e8df6a676148eC550BE6d72c2950B655b

Is it a testnet? Validators are bridge orchestrators?

Happy building!

Same feeling!

At the moment this is an isolated testnet of the `ext-chain`. The EVM is completely separated from block production. The next phase is connecting the `ext-chain` to the NoM public testnet.

Everyone should have received `xZNN` by now.

It’s working  
![Image 100: image](https://forum.zenon.org/uploads/default/original/2X/d/d3acf659136da72a6eca2f4197a6c3de0ec0e995.png)

We should now discuss a way to incentive people to build on the ext chain.

New governance Token with airdrop probability to early adopters

[7nzalh](https://forum.zenon.org/u/7nzalh) September 3, 2023, 8:14pm  54

Ser wen allo? I’m yet to receive any xZNN ![Image 101: :broken_heart:](https://forum.zenon.org/images/emoji/twitter/broken_heart.png?v=12)  
I assure you they’ll serve great purposes ![Image 102: :alien:](https://forum.zenon.org/images/emoji/twitter/alien.png?v=12)

[0x3639](https://forum.zenon.org/u/0x3639) September 3, 2023, 9:45pm  55

hook me up with some token please.

0x6DF301ECe246B1eedBDB3db61B96be495db80e03

[0x3639](https://forum.zenon.org/u/0x3639) September 3, 2023, 9:50pm  56

[0x3639](https://forum.zenon.org/u/0x3639)

September 3, 2023, 9:50pm  57

This sounds dumb at first glance. Or let me rephrase, some will find it too degen. But hear me out: it’s a good idea. You want to attract degens first because they will give you a visibility boost so the builders and others come. Degens might even stay longer than expected. Some of them, at least. Nobody come in crypto for the tech: we come for money - most of us - then we stick around because it’s interesting. In that order. Don’t neglect degenerates. Curious to hear Aliencoder about that.

I’ll better fork UniswapV2

Excited to test it out, thanks for sending some xZNN.

0x2EcE9B490A2C105aB7Aca9A1C2411E83c0Dfc690

Hi [@aliencoder](https://forum.zenon.org/u/aliencoder), I would like to receive some xZNN please.

0x429dA04833BeB270d209c45E0AFEAae7bbbC8Aa5

Open-source explorer for the `XZNN EVM`:

Who wants to do this deployment?

[7nzalh](https://forum.zenon.org/u/7nzalh) September 4, 2023, 6:51pm  64

Legend. Thank you ![Image 103: :pray:](https://forum.zenon.org/images/emoji/twitter/pray.png?v=12)

[sol](https://forum.zenon.org/u/sol) September 4, 2023, 10:34pm  65

I attempted to deploy a similar explorer but it wasn’t able to access the entire chain state via the RPC url you provided. Maybe I was doing something wrong.

That’s why I asked if we could run nodes on the testnet.  
Blockscout documentation states that we require a [full archival node](https://docs.blockscout.com/for-developers/information-and-settings/client-settings).

The RPC is from a full archival node.

At the moment this is just a devnet with a limited number of validator nodes. A public testnet will follow.

What error did you get?

[0x3639](https://forum.zenon.org/u/0x3639) September 5, 2023, 2:37pm  67

I can try to spin one up today

[sol](https://forum.zenon.org/u/sol) September 5, 2023, 3:26pm  68

Which node variant are you using and which ports have you exposed?

The node variant is a fork based on [exchain](https://github.com/okx/exchain) codebase.

I’ve exposed only the `EVM` port. You’ll be able to participate when I’ll announce the public testnet.

[0x3639](https://forum.zenon.org/u/0x3639) September 6, 2023, 1:35am  70

For the explorer frontend `.env` settings…

```
ETHEREUM_JSONRPC_VARIANT: 'ganache' # << What should this be??
ETHEREUM_JSONRPC_HTTP_URL:  https://ext-testnet.zenon.community:8545/ # CORRECT?
ETHEREUM_JSONRPC_WS_URL:  wss://ext-testnet.zenon.community8545/ # CORRECT?
INDEXER_DISABLE_INTERNAL_TRANSACTIONS_FETCHER: 'true'
INDEXER_DISABLE_PENDING_TRANSACTIONS_FETCHER: 'true'
DATABASE_URL: postgresql://postgres:@host.docker.internal:7432/blockscout?ssl=false
ECTO_USE_SSL: 'false'
SECRET_KEY_BASE: '56NtB48ear7+wMSf0IQuWDAAazhpb31qyc7GiyspBP2vh7t5zlCsF5QDv76chXeN'
CHAIN_ID: '1337'
API_V2_ENABLED: 'true' # NOTE SURE WHAT THIS IS WILL TEST
MIX_ENV: 'prod' # I ASSUME THIS IS CORRECT
```

[0x3639](https://forum.zenon.org/u/0x3639)

September 6, 2023, 1:37am  71

[@sol](https://forum.zenon.org/u/sol) did you just setup the frontend only?

`ETHEREUM_JSONRPC_VARIANT: 'ganache' # << What should this be??`

*   I don’t know.

`ETHEREUM_JSONRPC_HTTP_URL:  https://ext-testnet.zenon.community:8545/ # CORRECT?`

*   Remove the port

`ETHEREUM_JSONRPC_WS_URL:  wss://ext-testnet.zenon.community8545/ # CORRECT?`

*   Remove this line entirely

`CHAIN_ID: '73405'`

*   Use `73405` as `chainId`

[0x3639](https://forum.zenon.org/u/0x3639) September 6, 2023, 12:53pm  73

cool - I’ll mess with it today.

[vilkris](https://forum.zenon.org/u/vilkris) September 8, 2023, 1:51pm  74

Requesting 10k xZNN: 0xD63Aa61977493de5235Dc0Ecc6994035D9f16e7B

Thank you.

I’m finishing the dynamic Plasma proposal right now and after that I’ll be back working on extension chains.

The devnet for the extension chain is up and running again.

All previous balances were preserved.

Extension chain RPC details:

Network name: **XZNN**  
New RPC URL: **[https://ext-testnet.zenon.community](https://ext-testnet.zenon.community/)**  
Chain ID: 73405  
Currency symbol: **xZNN**  
Block explorer URL: **TBA**

Requesting 5K xZNN

0x89A2279C8Fb664b97a1b71eFb3Fa169AFd75f6c4

The idea is to deploy a [Tendermint light client](https://pkg.go.dev/github.com/tendermint/tendermint/light) as an embedded contract on NoM to provide a bridge between NoM and Cosmos based chains (the extension-chain is a Cosmos chain fork).

“Light clients (and full nodes) operating in the Proof Of Stake context need a trusted block height from a trusted source that is no older than 1 unbonding window plus a configurable evidence submission synchrony bound. This is called weak subjectivity.”

“IBC uses light clients in order to provide trust-minimized interoperability between sovereign blockchains. Light clients operate under a strict set of rules which provide security guarantees for state updates and facilitate the ability to verify the state of a remote blockchain using merkle proofs.”

[0x3639](https://forum.zenon.org/u/0x3639) December 10, 2023, 12:13am  82

Are you thinking we do NOT use the bridge for connection between the L1 and Extension Chain?

For v1 we should use the bridge. Fastest go-to-market strategy.

I think we’ll go with a simpler 50% - 50% fee distribution model where the fees are split evenly between `extension-chain` validators (Pillars) and contract deployers.

Pillars will be able to run nodes and they should be properly incentivized to sustain the `extension-chain`.

**Supernova** extension-chain with dual-VM support `EVM` and `WASM`

*   Pillars will be able to register as `extension-chain` validators with their producer keystore
*   Orchestrator support for `ext-chain` (with configurable parameters)
*   Built-in support for swapping `ZNN` ↔ `xZNN`
*   Deploy `EVM` contracts
*   Deploy `WASM` contracts

I’m searching for a name for the first NoM `extension-chain`, if you have ideas please share them over here.

*   Supernova
*   Neutronum
*   Starfield
*   Other

[0x3639](https://forum.zenon.org/u/0x3639) February 3, 2024, 11:16am  85

Starfield sound pretty cool!!

[Manu](https://forum.zenon.org/u/Manu) February 3, 2024, 11:47am  87

I suggest **CYGNUS**

Cygnus is a binary star. It is the optical counterpart of Sirius.

[0x3639](https://forum.zenon.org/u/0x3639)

February 3, 2024, 11:54am  89

[![Image 104](https://forum.zenon.org/uploads/default/original/2X/e/e41241c9f4a9508b22e4b84c4fc70111131f22ed.jpeg)](https://www.youtube.com/watch?v=cNYO349i1-Q&t=20)

[coinselor](https://forum.zenon.org/u/coinselor) February 3, 2024, 2:32pm  90

Zenon XT

It would make much more sense ticker wise if we are set on xZNN or something similar. If we really want to maintain ZNN as part of the ticker, I think maintaining Zenon in the name makes sense.

Zenon Plus  
Zenon Infinity  
etc

Alternatively, we can just use ZNN as the native ticker, without any distinctions, akin to how Arbitrum/Optimism/etc name ETH just ETH. In that case, we could use any name. Here’s a list of random stars:

1.  Sirius
2.  Canopus
3.  Arcturus
4.  Vega
5.  Capella
6.  Rigel
7.  Procyon
8.  Betelgeuse
9.  Altair
10.  Aldebaran
11.  Antares
12.  Spica
13.  Pollux
14.  Fomalhaut
15.  Deneb
16.  Regulus
17.  Castor
18.  Gacrux
19.  Bellatrix
20.  Algol
21.  Alphard
22.  Mizar
23.  Dubhe
24.  Algenib
25.  Mirfak
26.  Alnair
27.  Alnilam
28.  Alnitak
29.  Diphda
30.  Mimosa
31.  Regor
32.  Wezen
33.  Suhail
34.  Kaus Australis
35.  Avior
36.  Alkaid
37.  Menkent
38.  Acrux
39.  Almach
40.  Eltanin
41.  Scheat
42.  Markab
43.  Alpheratz
44.  Hadar
45.  Denebola
46.  Gienah
47.  Muhlifain
48.  Naos
49.  Schedar
50.  Shaula
51.  Nunki
52.  Zubenelgenubi
53.  Zubeneschamali
54.  Sargas
55.  Kaus Media
56.  Kaus Borealis
57.  Thuban
58.  Rastaban
59.  Alderamin
60.  Altarf
61.  Ankaa
62.  Azha
63.  Caph
64.  Deneb Algedi
65.  Enif
66.  Fafnir
67.  Girtab
68.  Hamal
69.  Izar
70.  Kraz
71.  Lesath
72.  Markeb
73.  Nihal
74.  Phact
75.  Ruchbah
76.  Sadr
77.  Skat
78.  Tureis
79.  Unukalhai
80.  Vindemiatrix
81.  Zaurak
82.  Zosma
83.  Acamar
84.  Achernar
85.  Agena
86.  Alcor
87.  Alioth
88.  Alphecca
89.  Alshain
90.  Altair
91.  Alya
92.  Anser
93.  Arneb
94.  Ascella
95.  Asterope
96.  Atik
97.  Atlas
98.  Atria
99.  Auva
100.  Azmidiske

Any particular reason for the separate name?

[Stark](https://forum.zenon.org/u/Stark) February 3, 2024, 6:43pm  93

I like Supernova ZVM. It feels like lotion on my brain.

[baggot](https://forum.zenon.org/u/baggot) February 4, 2024, 7:15am  95

The roadmaps now mapped in the starfield.

[dot](https://forum.zenon.org/u/dot) February 4, 2024, 9:03am  96

[@aliencoder](https://forum.zenon.org/u/aliencoder) please can you reconsider this fees topic.  
give the people what they want  
feeless ETH - like ETH but feeless  
the degens can then copy pasta fork eth contracts on the extension chains  
we can have fun punting shitcoins without fees  
also we can explore new stupid and pointless business models that weren’t possible without fees before

[dot](https://forum.zenon.org/u/dot) February 4, 2024, 9:27am  97

[@aliencoder](https://forum.zenon.org/u/aliencoder) I am too regarded to form concise points so chatgpt delivered my telegram chitchat to explain what i’m saying in the third person. hope it makes sense:

The conversation revolves around advocating for a feeless architecture for Zenon, drawing on various points to bolster this argument. It starts with the assertion that feeless alternatives to Ethereum would be highly attractive, especially for those looking to maximize their investments without incurring transaction fees. The idea is that by replicating Ethereum’s success in a feeless environment, Zenon could significantly attract both developers and users, particularly those disenchanted by the fees on other platforms.

The speaker underscores the importance of tapping into the enthusiasm of the cryptocurrency community, particularly those who are heavily invested in Zenon and are motivated by the prospect of feeless transactions. This community is described as vibrant, engaged, and crucial in driving the hype cycles that could propel Zenon’s value and adoption.

Moreover, the conversation touches on the strategic advantage of leveraging Ethereum’s existing contract ecosystem, suggesting that Zenon could benefit from adopting successful Ethereum contracts directly onto its platform. This approach is seen as a way to rapidly populate Zenon with a rich tapestry of applications, attracting a user base looking for Ethereum-like experiences without the fees.

The discussion also acknowledges the need for Zenon to create trends and establish itself as a leader in the feeless blockchain space. The speaker suggests that Zenon’s growth depends on its ability to differentiate itself and capture the imagination of the cryptocurrency community with its feeless proposition.

There’s an acknowledgment of the practicalities and challenges involved in maintaining a feeless architecture, including the reliance on the goodwill of node operators and the necessity of fostering a supportive ecosystem. Despite these challenges, the speaker remains optimistic about the potential for Zenon to innovate and lead with a feeless model, drawing on the community’s enthusiasm and the foundational principles of the platform.

In summary, the argument is for Zenon to pursue a feeless architecture as a means to differentiate itself, attract a dedicated user base, and capitalize on the growing demand for cost-effective blockchain solutions. This strategy is seen as aligning with Zenon’s foundational values and as a critical step in securing its place in the competitive blockchain ecosystem.

[tapwoot](https://forum.zenon.org/u/tapwoot) February 4, 2024, 9:36am  98

Feeless pls, dot guy has a point

It really doesn’t make any sense to be another smart contract shitcoin with fees… all this effort just to launch something mediocre will get drowned amongst the noisy influencers

Validators are already incentivised indirectly from pillar rewards and we should vote to replenish AZ funds from a different source

[dot](https://forum.zenon.org/u/dot)

February 4, 2024, 9:51am  99

![Image 105: image](https://forum.zenon.org/uploads/default/original/2X/1/11005e1be0894f3545f385e1565da72d04e0b037.png)

[0x3639](https://forum.zenon.org/u/0x3639)

February 4, 2024, 11:33am  100

[![Image 106: Screenshot 2024-02-04 at 5.32.54 AM](https://forum.zenon.org/uploads/default/original/2X/a/ad639914f3aa972eb18d8b52ff2fe39b9a15d4eb.png)](https://t.me/zenonnetwork/347736)

[coinselor](https://forum.zenon.org/u/coinselor) February 4, 2024, 11:54am  102

Doesn’t it take the same amount of time to share a screenshot than to copy/paste? We want the content to be indexed by search engines ![Image 107: :sweat_smile:](https://forum.zenon.org/images/emoji/twitter/sweat_smile.png?v=12)

[0x3639](https://forum.zenon.org/u/0x3639) February 4, 2024, 11:57am  103

true. Im trying to break the matrix.

[dot](https://forum.zenon.org/u/dot) February 4, 2024, 1:05pm  104

i’m horny for zenon

[tapwoot](https://forum.zenon.org/u/tapwoot) February 4, 2024, 6:11pm  105

so what do you propose as the solution for spam protection on the ext chain if its feeless without plasma?

[MeMeMeMe](https://forum.zenon.org/u/MeMeMeMe) February 4, 2024, 6:44pm  106

Nice names and suggestions.

I think an extension chain can be thought of as a planet’s moon, an orbiting object, or a sister to balance out masculine nomenclature.

These concepts are parallel worlds or clear familial ties with a feminine nod; Zenon’s ’sister chain’ insert name.

Lunar / Lunaris would have been nice but associated with Terra.

The Ancient Greek name for moon; Selene.

Latin for sister: Soror.

Twin: Gemella

[MeMeMeMe](https://forum.zenon.org/u/MeMeMeMe) February 4, 2024, 6:51pm  107

I’m told that the ancient Chinese word for sister is zizi, pronounced something like zee-zee.

Zizi would be feminine, imply relatedness to the main chain, be easy to say, appeal to the East Asian market whilst having an ancient root, and have a very Zenon ‘lite’ feel with the zeds or zee’s.

[dot](https://forum.zenon.org/u/dot) February 4, 2024, 7:36pm  109

what a lovely passage

zizi

[Sir\_D](https://forum.zenon.org/u/Sir_D) February 5, 2024, 3:33am  110

0xCb4f86aeE2251570C9885F034a4734B376076519

10k please thanks

Zizi is a cute form of saying dick in French

Shazz doxxed himself. Lol

[coinselor](https://forum.zenon.org/u/coinselor) February 5, 2024, 2:54pm  113

That would still be feminine, then.

Zizi +1

Done.

The base layer is feeless. This particular `extension-chain` needs fees to support both validators and developers.

How? Who pays them to run a validator node on the `ext-chain`?

I’ve proposed several ways [over here](https://forum.hypercore.one/t/network-of-momentum-phase-1/253/75).

[coinselor](https://forum.zenon.org/u/coinselor) February 6, 2024, 10:30am  115

I think he meant pillars are indirectly incentivized to support everything that brings utility to ZNN, i.e orchestrators. Although theory is not working as well as it should… I blame our pillar set, sample size not big enough for conclusions. Historically, we’ve had some pillars with terrible engagement metrics.

[dot](https://forum.zenon.org/u/dot) February 10, 2024, 4:02pm  116

quasar  
onchain dynamic plasma calcs  
time lags between tx  
providing proof of work
