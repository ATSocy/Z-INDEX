Thread: crypto-ecosystems-taxonomy-update
coinselor | 2023-12-26 01:19:53 UTC | #1

As a token of appreciation for all contributors to NoM, I've taken the initiative to gather all (most?) github organizations or accounts that include any NoM related code.

We are a bunch of scattered aliens, it took me a little while and I'm sure I've missed a few. So, before I submit the PR from my forked repository to update it, can you come up with any repositories that I've missed?

Things to note:
- All repositories inside an organization (including subecosystem orgs) are indexed. That's why I didn't include the syrius repo, for example.
- I've included a few seemingly old repos like the Cano Wallet. The idea is to get as close to the real metrics for our developer activity.
- Tag naming suggestions are welcome.

https://github.com/electric-capital/crypto-ecosystems

https://www.developerreport.com/

```toml
# Ecosystem Level Information
title = "Zenon - Network of Momentum"

sub_ecosystems = [
    "Alien Valley",
    "HyperCore Team",
    "Ignition Pillar",
    "Zenon Hub",
    "Zenon Org",
    "Zenon Tools",
    "{H}yperCore One",
    ]

github_organizations = ["https://github.com/zenon-network"]

# Repositories
[[repo]]
url = "https://github.com/zenon-network/znn_sdk_dart"
tags = ["SDK"]

[[repo]]
url = "https://github.com/MoonBaZZe/znn-sdk-go"
tags = ["SDK"]

[[repo]]
url = "https://github.com/ignition-pillar/go-zdk"
tags = ["SDK"]

[[repo]]
url = "https://github.com/millerships/pyznn"
tags = ["SDK"]

[[repo]]
url = "https://github.com/2bonahill/znn_sdk_rust"
tags = ["SDK"]

[[repo]]
url = "https://github.com/digitalSloth/znn-php"
tags = ["SDK"]

[[repo]]
url = "https://github.com/hypercore-one/znn_sdk_csharp"
tags = ["SDK"]

[[repo]]
url = "https://github.com/DexterLabZ/znn.ts"
tags = ["SDK"]

[[repo]]
url = "https://github.com/alien-valley/znn.js"
tags = ["SDK"]

[[repo]]
url = "https://github.com/KingGorrin/znn_sdk_java"
tags =["SDK"]

[[repo]]
url = "https://github.com/ItsChaceD/zenon-android"
tags = ["SDK"]

[[repo]]
url = "https://github.com/DexterLabZ/syrius-extension"
tags = ["Wallet"]

[[repo]]
url = "https://github.com/Cano-Wallet/app"
tags = ["Wallet"]

[[repo]]
url = "https://github.com/znnpd/zenonbrowserwallet"
tags = ["Wallet"]

[[repo]]
url = "https://github.com/DexterLabZ/bridge-dapp"
tags = ["Bridge"]

[[repo]]
url = "https://github.com/MoonBaZZe/sentrify"
tags = ["Utilities"]

[[repo]]
url = "https://github.com/znnpd/znn-testnet-stresstest"
tags = ["Utilities"]

[[repo]]
url = "https://github.com/sol-znn/znn-node-parser"
tags = ["Utilities"]

[[repo]]
url = "https://github.com/sol-znn/Zenon-PoCs"
tags = ["Utilities"]

[[repo]]
url = "https://github.com/sol-znn/znn-address-generator"
tags = ["Utilities"]

[[repo]]
url = "https://github.com/dumeriz/zenon-repro"
tags = ["Utilities"]

[[repo]]
url = "https://github.com/0x3639/znndNode"
tags = ["Utilities"]

[[repo]]
url = "https://github.com/vilkris4/dynamic-plasma-ideas"
tags = ["R&D"]

[[repo]]
url = "https://github.com/uluCthulhu/wallet-connect-demo"
tags = ["R&D"]

[[repo]]
url = "https://github.com/Big-Inches-Club-House/htlc-demo"
tags = ["R&D"]

[[repo]]
url = "https://github.com/oxmah/awesomezenonnetwork"
tags = ["Resources"]

[[repo]]
url = "https://github.com/sultanofstaking/EXPERIMENTAL-Zenon-Pillar-Sentry-Architecture-For-Running-Pillars"
tags = ["Resources"]

[[repo]]
url = "https://github.com/Shazzamazzash/Zenon-Decks"
tags = ["Resources"]
```
Sub-ecosystems
Alien Valley: https://github.com/alien-valley
HyperCore Team: https://github.com/HyperCore-Team
Ignition Pillar: https://github.com/ignition-pillar
Zenon Hub: https://github.com/zenonhub-io
Zenon Org: https://github.com/zenonorg
Zenon Tools: https://github.com/zenon-tools
{H}yperCore One: https://github.com/hypercore-one





Merry Zmas DevZ :christmas_tree:

-------------------------

Shazz | 2023-12-25 05:55:53 UTC | #2

Ooh this is great @mehowz @0x3639 since so many investors in this space look at github activity as a proxy for project health

-------------------------

Chadass | 2023-12-25 15:39:57 UTC | #3

I will update this soon : https://github.com/oxmah/awesomezenonnetwork

-------------------------

Shazz | 2023-12-25 16:04:30 UTC | #4

This came just in time as new investors are asking why there"s "little" activity in the mainline. Is @sumamu's bridge and wbtc repo listed above @coinselor ?

-------------------------

coinselor | 2023-12-25 16:25:33 UTC | #5

Yes, It's under their parent HyperCore Team organization. Each subecosystem will be a separate .toml file in their repository, with their organization title and a url pointing to it. I don't think there's a WBTC repo... support for new tokens should just be passing some paramenters to the already deployed contracts, but I could be wrong. Last orchestator update was 2 weeks ago, and there was nothing WBTC related.

I've also included as an additional [[repo]] the bridge front-end since it seems to be living under dexter's github account.

The goal was to at least get a head count for the number of individual developers. I've omitted a few of the less relevant repos when I had already included that individual Github account. For example, Sultan has like one individual repo per tutorial, and has like 8 total, so I've just included one.

Interestingly, they consider a "full-time" dev anyone who has submitted code 10 days in a given month. For example, Immutable shows up as having 3 full time devs and 27 total developers.

-------------------------

coinselor | 2024-02-24 17:17:13 UTC | #6

This was merged 2 days ago :christmas_tree: 

https://github.com/electric-capital/crypto-ecosystems/pull/1074

-------------------------

coinselor | 2024-03-10 13:04:14 UTC | #7

Using thread as a Todo list:

[] Add [ZNNRigel](https://github.com/znnrigel?tab=repositories) repos to Taxonomy

-------------------------

