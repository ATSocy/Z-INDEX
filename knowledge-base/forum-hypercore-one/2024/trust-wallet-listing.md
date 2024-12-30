Thread: trust-wallet-listing
aliencoder | 2024-06-05 06:48:35 UTC | #1

In order to increase the visibility of Zenon Network, we need to start making it accessible for regular crypto users.

That's why I'm proposing to integrate support for Zenon in third party multi-chain wallets.

One of the biggest 3rd party multi-chain wallets is Trust Wallet with over [100 million users](https://finance.yahoo.com/news/trust-wallet-reaches-122-million-152800389.html).

I think this move will massively benefit Zenon's adoption during this bull run. We need to start the implementation as soon as possible.

The listing process is no easy task:

https://developer.trustwallet.com/developer/wallet-core/newblockchain

But we have 2 options:

1. List native `ZNN` (NoM support)

This is more complicated because we need the `C++` and `Rust` SDKs that are currently not available. Also in order to list a new blockchain it must be approved by their governance system:

- The native coin is listed in the top 100 coins on CoinMarketCap and proposal gets approved on [https://governance.trustwallet.com].

I don't think we currently have any chance to get native `ZNN` listed, but we can give it a shot.

2. List `xZNN` (Supernova support)

This is easier to accomplish because we don't need to reinvent the wheel (Supernova is an EVM chain):

https://developer.trustwallet.com/developer/wallet-core/newblockchain/newevmchain

We also need to cover some listing [fees](https://developer.trustwallet.com/developer/listing-new-assets/new-asset#fee) and [meet some requirements](https://developer.trustwallet.com/developer/listing-new-assets/requirements#listing-acceptance-guidelines) for example: "minimum 10,000 token holders and 15,000 transactions".

-------------------------

aliencoder | 2024-06-05 07:56:26 UTC | #2

[quote="aliencoder, post:1, topic:470"]
2. List `xZNN` (Supernova support)
[/quote]

We might have a good chance to list Supernova. For example they've listed [Horizen EON](https://eon.horizen.io/), a [Horizen EVM sidechain](https://github.com/HorizenOfficial/eon).

```
  {
    "id": "zeneon",
    "name": "Zen EON",
    "coinId": 7332,
    "symbol": "ZEN",
    "decimals": 18,
    "blockchain": "Ethereum",
    "derivation": [
      {
        "path": "m/44'/60'/0'/0/0"
      }
    ],
    "curve": "secp256k1",
    "publicKeyType": "secp256k1Extended",
    "chainId": "7332",
    "addressHasher": "keccak256",
    "explorer": {
      "url": "https://eon-explorer.horizenlabs.io",
      "txPath": "/tx/",
      "accountPath": "/address/",
      "sampleTx": "0xb462e3dac8eef21957d3b6cff3c184d083434367a726dd871e98a774f4d037a5",
      "sampleAccount": "0x09bCfC348101B1179BCF3837aC996cF09357215f"
    },
    "info": {
      "url": "https://eon.horizen.io",
      "source": "https://github.com/HorizenOfficial/eon",
      "rpc": "https://eon-rpc.horizenlabs.io/ethv1",
      "documentation": "https://eon.horizen.io/docs"
    }
  }
```

We need to prepare the `documentation`, `rpc` endpoint(s) and have the explorer up and running.

-------------------------

Bzed | 2024-06-05 09:37:21 UTC | #3

Hard to say if Supernova will be the right choice right now with the reliability of the bridge. The swap ux is quite smooth overall but still seems like it would be a hurdle for a lot of users as it is now if that is a required step in using the extension chain.

-------------------------

aliencoder | 2024-06-05 10:54:05 UTC | #4

[quote="Bzed, post:3, topic:470"]
as it is now if that is a required step in using the extension chain
[/quote]

It won't be a required step. Users will be able to join Supernova without going into native ZNN first. Integrations with Supernova will be easier given it's an EVM based chain.

-------------------------

Bzed | 2024-06-06 12:20:33 UTC | #5

Ok thanks for the clarification.

-------------------------

