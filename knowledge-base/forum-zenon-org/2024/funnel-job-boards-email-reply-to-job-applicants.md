Thread: funnel-job-boards-email-reply-to-job-applicants
mehowbrainz | 2023-02-08 22:33:43 UTC | #1

Hey,

Here is how I reply to job applicants that come in via email thanks to the job board listings. I’ve noticed some devs join various telegram channels, asking to hire them. Ideally this copy will get translated to a landing page on zenon.org that’ll guide all.

In my emails, the links are all tracked using click.zenon.link short links:

https://twitter.com/zenonorg/status/1544508498565808128

How does the funnel look like?

1) Someone in the world needs work, he visits cryptojoblist.com or webassemblyjobs.com

2) He stumbles on the job posts.

3) He doesn’t know yet that Zenon funding is governed by pillars on-chain, so he applies and says something in the lines of “I’m ready to work asap!” — we get the application via email.

4) We reply with the email below.

This is called inbound marketing as we’re positioning opportunities in traffic sources where people are closest to converting. In this case they’re looking for jobs, and hence visit job boards. 

Always reach for low hanging fruits first.

The whole will eventually be streamlined with landing pages on the zenon.org. The more organized we are with docs and resources for newcomers, the easier this’ll all become. Zenon.org will make sure to architect the best highways for inbound traffic :)

The next level would be retargeting and re-engaging with candidates to convert them into contributors.

————

Hey,

Thanks for your interest in contributing to [Zenon Network](https://twitter.com/Zenon_Network)’s development.

My name is [mehowz](https://twitter.com/mehowbrainz), I was previously contributing to THORChain and [helped that community grow from a $15M market cap to many billion](https://twitter.com/THORChain/status/1506810398552444930?s=20) between 2019-2021 thanks to various successful campaigns and the development of the THORChain.org website. My expertise is growth hacking.

In 2022 I moved on from THORChain and joined the [ZenonOrg](https://twitter.com/ZenonOrg) team. We’re a pillar-operating organization, meaning that we run validator pillars (nodes essentially) in the Zenon Network. ZenonOrg’s mission is to develop distribution networks and marketing systems for the Zenon ecosystem. You’ll see us roll out a new [zenon.org](http://zenon.org/) website soon, which’ll tie itself with a variety of marketing funnels to onboard new participants into the Zenon Network.

As a first priority, we’re looking to onboard:

- Developers (I’ll get to dev needs later in this email).

- Delegators , they’re essentially ZNN token hodlers which delegate their ZNN to pillars via the Zenon [syrius desktop wallet](https://zenon.network/#downloads) in exchange for protocol-emitted [reward splits](https://zenon.tools/pillars), shared between the pillar and delegator (the pillar decides the % split). The more delegation weight a pillar has, the more the pillar [increases in rank](https://zenon.tools/pillars) which further increases his chance of producing momentum heights and earning more, (top 30 weighted pillars earn more than others). This network design invites pillars (like ZenonOrg) to [create new value](https://twitter.com/ZenonOrg/status/1543642431870173186) for the ecosystem in order to [gain support from delegators](https://twitter.com/ZenonOrg/status/1543941085373906944).

As a second priority, we’ll be looking to onboard more:

- Pillars and Sentinels. They help secure the network. As of today there’s about 82 pillars and 153 sentinel nodes in the network. There’s a cost to deploy these, details are [highlighted here](https://medium.com/@zenon.network/znn-x-qsr-alphanet-specifications-83d27c005c09).

- Liquidity Providers to the [wZNN/BNB pool on PancakeSwap](https://pancakeswap.finance/swap?inputCurrency=0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c&outputCurrency=0x84b174628911896a3b87fa6980d05dbc2ee74836). wZNN can later be [converted to ZNN](https://twitter.com/zyler9985/status/1510619413506326530) via the bridge (the bridge [code is linked here](https://github.com/zenon-network/wznn-bsc), useful for any dev who wants to develop the wQSR bridge which we explain later in this email).

- Stakers, they earn QSR tokens for time-locking their ZNN to staking.

- Marketers, we’re working on distribution architecture and systems to unify a performance-focused marketing community. The idea is to guide the marketing community towards a proof-of-performance ethos.

Going back to the developer needs. The anonymous core developers of the Zenon protocol have been working for over 3 years, and written over 1.3M lines of code. They [open-sourced quite a bit of the code](https://github.com/zenon-network/go-zenon) on Github due to their progressive objectives to decentralize the network (modelled around the values of and ethos of Bitcoin). They’re expecting the community to take lead on many of the much needed core developments.

They launched a program called [Accelerator-Z](https://zenon.network/accelerator.html) (aka A-Z), which allows anyone to write a proposal and request funds to carry out the work, whether it be development, marketing etc. Proposals are submitted in the [syrius desktop wallet](https://zenon.network/#downloads), while pillars use the wallet to vote (on-chain) in-favour or against. Once a quorum is reached, the proposal either passes or gets rejected, and then the proposal leader is asked to submit a 2nd proposal for his work phase (which goes through the same round of on-chain voting). [Most A-Z submissions](https://zenon.tools/accelerator) have been dev-oriented due to the pressing development needs initiated by the [Hyperspace program](https://medium.com/@zenon.network/hyperspace-x-accelerator-z-towards-a-dao-of-daos-38dfad496365).

As a first priority, the Zenon network needs:

- SDK’s for the following languages:
— Python
— Swift
— Java/Kotlin
— Javascript/Typescript (in-progress)
— Rust (in-progress)
— Go (in-progress)
— C/C++ (in-progress)
— C# (in-progress)
— Common Lisp (in-progress)

As a 2nd priority:

Interoperability solutions so that there’s more liquidity that can enter and exit. For that we need:

- A wQSR BSC bridge (analog to the [wZNN bridge](https://github.com/zenon-network/wznn-bsc)) and an ETH bridge for ZNN and QSR. Bridges should be as trustless as possible hence we'd need someone with cryptographic know-how on multi-party-computation to design a solution how pillars can effectively manage and maintain bridge liquidity in a secure way. QSR (known as Quasar) is an asset that’s fused to z-addresses to generate Plasma. This locks the QSR to the address and forms a Proof of Stake, at the same time creating the energy to fuel transactions. So in a way you do have to pay for transactions by buying and fusing Quasar, but that Quasar can be unfused at any time after an initial short lock time and is not depleted through the action of creating Plasma. The Quasar/QSR you put in to fuse is what you get back when you un-fuse. The Plasma generated through fusing is algorithmically determined to ensure the network stays stable and cannot be spammed - there will never be enough plasma in the network to congest it. Everyone only gets a portion of the throughput depending on how much QSR is staked. The PoW is apparently very difficult so its effects are negligible.

- Atomic swaps and related technologies (HTLCs). It’s an alternative which [George is already working on](https://forum2.zenon.org/t/btc-atomic-swaps-via-htlc-cope-edition/584) but afaik it would also require pillars to hold custody of BTC.

- Wrapped assets like zBTC to transact them feelessly via the Zenon Network of Momentum (NoM). This also requires asset pooling by pillars and secure transaction signing. I don't know how this would be implemented but MPC might play a role here too to improve tx authorization security. On a side note, the [syrius desktop wallet](https://zenon.network/#downloads) allows the easy minting of ZTS (Zenon Token Standard) tokens.

- Cross-chain bridges (with other L1/L2 networks)

- Merge mining so that BTC miners can also earn ZNN with the same mining algo.

This is basically the foundation - liquidity can flow in and out in a secure and efficient way and devs can use different programming languages to interact with Zenon NoM.

As a 3rd priority:

Now that that's covered, we need to look at what is needed from a product / zApp perspective that allows product devs to build meaningful applications on top of Zenon NoM.

- Smart Contract Runtime - Absolutely critical for any zApp. The core team developers suggested WASM. We don't have anyone yet with the capability to implement WASM (Web Assembly). Based on this devs can now build end-user applications (like swapping services, NFT projects or whatever). Discussions regarding the topic can be found in [these forum topics](https://twitter.com/mehowbrainz/status/1543340726834106368).

As a 4th priority:

In order for these zApps to support potentially millions of users, the Zenon NoM protocol has to advance from Alphanet to Betanet and implement sentinels so that higher scalability and transactions per second is achieved.

Note that not all interoperability solutions need to be realized in order for the network to move ahead to other priorities. It just facilitates the flow of capital and reduces entry barriers. A few trustless bridges + atomic swaps or wrapped assets are already more than enough.

Priority 4 will likely happen before priority 3 (as it's theoretically scheduled for end of year), and a gant-style Phase 2 can be a very long phase that overlaps 3 and 4.

———

You applied to the [WebAssembly / Smart Contract Runtime job post](https://twitter.com/mehowbrainz/status/1543340725361942528), which is listed in the 3rd priority. Any advancement in the priorities listed are welcomed.

You can read more about Hyperspace x Accelerator-Z in the [forum topic](https://forum2.zenon.org/t/zenon-network-grants-hyperspace-x-accelerator-z/439), it includes a link to the [template](https://forum2.zenon.org/t/zenon-network-accelerator-z-proposal-template/228/6) most applicants use to develop an A-Z proposal in the Accelerator-Z category. We welcome you to browse through previous [submissions using Zenon.tools](https://zenon.tools/accelerator) to see which were approved and funded.

Zenon is a network-governed decentralized entity. No single entity or brand can decide whether one will get funded (as a network of pillar validators vote on proposals on-chain), but looking at historical submissions and on-chain approvals, developers are highly prioritized and more-often-than-less funded for work. Developers just need to write good proposals and show commitment. Given the [low market cap of the $ZNN token](https://coinmarketcap.com/currencies/zenon/) this is the time to earn some ZNN via the A-Z program. The $QSR token doesn’t have any markets yet other than an [OTC channel](https://t.me/znnotc) due to the lack of a wQSR bridge as highlighted above.

Here are some important Telegram channels to join:

- [Official Zenon](https://t.me/zenonnetwork)
- [Community Zenon](https://t.me/Zenon_Community)
- [Zenon Builders](https://t.me/zenon_builders) (devs)
- [Z-Hub Updates](https://t.me/znnhub)
- [Accelerator-Z Updates](https://t.me/acceleratorz_updates)

Ideally we believe the best space is on the ZenonOrg [forums](https://forum2.zenon.org/) as it’s easier to track the progressions of conversations. We welcome you to join them and browse the [Developers](https://forum2.zenon.org/c/developers/5) category.

If you have any questions, feel free to email us back at [contact@zenon.org](mailto:contact@zenon.org) or DM us via our [ZenonOrg](https://twitter.com/ZenonOrg) handle. You can find me personally on [Twitter](https://twitter.com/mehowbrainz) and [Telegram](http://t.me/mehowbrains).

-------------------------

mehowbrainz | 2022-07-06 04:48:02 UTC | #2

Special thanks to @cryptocheshire who got me up to speed on network priorities after I recovered from my hospitalization, and great job @vilkris for zenon.tools and @0x3639 with the resources you’re pinning in the forums!

-------------------------

cryptocheshire | 2022-07-06 06:01:08 UTC | #3

Thank you for your drive and initiative man, it's an absolute pleasure watching you work!

-------------------------

Zashounet | 2022-07-06 09:04:36 UTC | #4

This is awesome, thank you for your dedication!

-------------------------

