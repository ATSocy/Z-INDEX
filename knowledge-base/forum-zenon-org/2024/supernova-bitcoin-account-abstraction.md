Thread: supernova-bitcoin-account-abstraction
aliencoder | 2024-11-20 15:27:33 UTC | #1

# Supernova Bitcoin Account Abstraction (AA)

Supernova is the first EVM extension-chain of Zenon and a hub for upcoming DeFi innovation where Solidity developers can directly participate in the Network of Momentum's ecosystem using familiar tools and resources. Supernova is run by a subset of Pillars and is closely aligned with all the principles of the Network of Momentum, including Bitcoin support and use-cases.

The Bitcoin Account Abstraction (AA) layer of the Supernova extension-chain allows users to leverage their existing Bitcoin keys to sign transactions via smart wallets deployed as Solidity smart contracts. 

It is designed to provide full compatibility with popular Bitcoin wallets like [Xverse](https://www.xverse.app/), which allows users to hold, swap and send [Ordinals](https://decrypt.co/resources/what-are-ordinals-a-beginners-guide-to-bitcoin-nfts) and [Runes](https://decrypt.co/221962/bitcoin-runes-launch-at-the-halving-heres-everything-you-need-to-know). This enables new DeFi use-cases on Supernova by tapping into well-established Bitcoin communities.

For developers, this solution opens up new opportunities to create innovative applications that leverage the strengths of Bitcoin and the use-cases provided by the EVM. It also helps attract a larger user base to Supernova by offering a familiar and convenient way to interact with it.

The implementation adheres to [EIP-4337](https://eips.ethereum.org/EIPS/eip-4337) specification.

Bitcoin support for both `ECDSA` and `Schnorr`. More info about popular Bitcoin addresses types [here](https://unchained.com/blog/bitcoin-address-types-compared/).

- Support for `P2SH`: send and receive `BTC`
- Support for `P2TR`: send and receive `BTC`, `Ordinals`, and `Runes`
- `ECDSA` support
- `Schnorr` support
- `Paymaster` support for handling gas fees

-------------------------

aliencoder | 2024-11-14 09:04:43 UTC | #2

The team working on Bitcoin Account Abstraction is almost ready.

Current status:

* Support for `P2SH`: :white_check_mark:
* Support for `P2TR`: :white_check_mark:
* `ECDSA` support :white_check_mark:
* `Schnorr` support :white_check_mark:
* `Paymaster` support for handling gas fees: pre-funded account :white_check_mark:
* Testing: in progress

I'll post here the AZ project. They are interested in continuing developing on NoM, so it's important to show support for their work and pass the AZ project faster.

-------------------------

aliencoder | 2024-11-23 15:09:41 UTC | #3

Current status:

* Support for `P2SH`: :white_check_mark:
* Support for `P2TR`: :white_check_mark:
* `ECDSA` support :white_check_mark:
* `Schnorr` support :white_check_mark:
* `Paymaster` support for handling gas fees: pre-funded account :white_check_mark:
* Added `go-ethereum` precompiles to speedup signature verification :white_check_mark:
* AZ project: voted :white_check_mark:
* Web app demo: in progress
* Testing: in progress

:grey_exclamation: Attention all Supernova extension-chain participants :grey_exclamation: 

Please update your nodes to [Supernova v0.0.8](https://github.com/AliensZone/supernova/releases/tag/v0.0.8). This update doesn't require a re-sync. Just stop the node (or service), replace it with the new version and start the node (or service) again.

```
systemctl stop supernova
*replace /usr/local/bin/supernovad*
systemctl start supernova
systemctl status supernova
```

-------------------------

aliencoder | 2024-11-27 16:01:12 UTC | #4

Current status:

* Support for `P2SH`: :white_check_mark:
* Support for `P2TR`: :white_check_mark:
* `ECDSA` support :white_check_mark:
* `Schnorr` support :white_check_mark:
* `Paymaster` support for handling gas fees: pre-funded account :white_check_mark:
* Added `go-ethereum` precompiles to speedup signature verification :white_check_mark:
* Web app demo: :white_check_mark:
* Testing: :white_check_mark:
* AZ project: voted :white_check_mark:
* AZ phase: in progress

BTC account-abstraction [smart contracts repository](https://github.com/AliensZone/supernova_account_abstraction)

BTC account-abstraction [demo web app repository](https://github.com/AliensZone/supernova_account_abstraction_demo)

-------------------------

aliencoder | 2024-12-04 13:53:40 UTC | #5

The [AZ phase](https://zenonhub.io/accelerator-z/phase/5304b4768bc96596029f71e3647bb5ab8d46551c95b70bf0bf340d7e7d24b9ca) was successfully paid out! Thank you for your support!

Next project will be outlined zoon.

-------------------------

