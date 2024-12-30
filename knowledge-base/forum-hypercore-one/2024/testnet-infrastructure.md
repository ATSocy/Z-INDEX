Thread: testnet-infrastructure
sol | 2023-05-30 15:01:10 UTC | #1

This thread will be used to document Testnet infra that is publicly available.

- **Chain ID**: 321
- **Explorers**: 
  - https://explorer.zenon.network/ (Node = https://node.zenon.fun:35997)
  - https://testnet.zenon.info (Node = https://testnet.deeznnutz.com:3597)
- **RPCs**: 
  - wss://node.zenon.fun:35998 
  - wss://testnet.deeznnutz.com:3598
- **Faucet**
  - https://faucet.hypercore.one
  - Dispenses 15 tZNN and 150 tQSR
  - Based on [Pylon](https://github.com/ignition-pillar/pylon)
  - Linux Example: ```curl -X POST https://node.zenon.fun:35999/faucet -H 'Content-Type: application/json' -d '{"address":"z1qr3uww8uqh75qnsuxqajegvwaesqynfglrare2"}' ```
  - Windows Example: `curl -X POST "https://node.zenon.fun:35999/faucet" -H "Content-Type: application/json" -d "{\"address\":\"z1qqtuepp88cwzjrteaa657hxgmgadycwjs7mgg8\"}"`

-------------------------

Chadass | 2023-05-30 14:10:16 UTC | #2

Installing in a VM

-------------------------

CryptoFish | 2023-07-19 10:11:56 UTC | #3

Do we have a testnet supporting bigint?

I'm currently only aware of wss://my.hc1node.com:35998 both which bridge mainnet and bridge testnet are using. I believe chain id 1 for mainnet and 3 for testnet?

I tried to use the Zenon Public Testnet Faucet bot to send some funds, but that doesn't work.

-------------------------

sumamu | 2023-07-19 12:56:00 UTC | #4

[quote="CryptoFish, post:3, topic:37"]
Do we have a testnet supporting bigint?
[/quote]

Sure. Check this out:
https://github.com/oxmah/awesomezenonnetwork

[quote="CryptoFish, post:3, topic:37"]
I tried to use the Zenon Public Testnet Faucet bot to send some funds, but that doesn’t work.
[/quote]

The one found in the awesomezenon repo?

-------------------------

CryptoFish | 2023-07-19 16:22:00 UTC | #5

[quote="sumamu, post:4, topic:37"]
The one found in the awesomezenon repo?
[/quote]

Yes, I've used that one. It doesn't seem to work.

-------------------------

sumamu | 2023-07-20 14:28:04 UTC | #6

[quote="CryptoFish, post:5, topic:37"]
Yes, I’ve used that one. It doesn’t seem to work.
[/quote]

Fixed it, sorry.

-------------------------

