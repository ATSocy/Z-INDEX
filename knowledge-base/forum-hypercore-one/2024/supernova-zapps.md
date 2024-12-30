Thread: supernova-zapps
build_republic | 2024-04-03 03:12:57 UTC | #1

Now that the [Supernova extension chain](https://forum.hypercore.one/t/extension-chains/52/42?u=build_republic) is about to go live, it's time to start getting the party started on the zApp side.  

Opening this thread to get ideas going (and ideally execution plans + zApp owners)

What's on aliens' minds?

![loop compositing GIF by Doze Studio|500x500](upload://npRIUghwIHrgPCxpCIAmwm4qTuI.webp)

-------------------------

sugoibtc | 2024-04-04 19:28:17 UTC | #2

I would really like to see these two:

- DEX/AMM
- NFT marketplace

-------------------------

build_republic | 2024-04-04 20:08:15 UTC | #3

Second that on NFT capabilities which also begs the question, would NoM/Supernova NFTs follow the [Zenon Standard](https://medium.com/@zenon.network/the-new-nft-standard-when-cryptography-meets-steganography-9e356007dcaa) that was alluded to or a standard that is built from [Cosmos Libraries](https://cosmos.network/interoperable-nfts/)?

-------------------------

aliencoder | 2024-04-04 21:08:57 UTC | #4

[quote="build_republic, post:3, topic:437"]
Supernova NFTs
[/quote]

Supernova has EVM support, so everything built on top must be EVM compatible. We can support ZTS <-> ERC-20 conversions with some modifications to the bridge/orchestrator layer. @sumamu is the expert in this field.

-------------------------

sugoibtc | 2024-04-07 13:27:29 UTC | #5

Does this also mean that if NFTs were to be launched on the xchain, that there could be an IFPS link within Syirus, so people can see their NFTs within the wallet? (If the NFT would be linked to a ZTS)

-------------------------

aliencoder | 2024-04-07 15:36:54 UTC | #6

We can make a fungible standard out of ZTS and support cross-chain transactions.

-------------------------

_Warrior | 2024-04-10 09:13:26 UTC | #7

Hello, @aliencoder 
I'd like to my FE skills to your project.
Could you give me chance to work with you?
Thanks.

-------------------------

aliencoder | 2024-04-10 09:15:18 UTC | #8

[quote="_Warrior, post:7, topic:437"]
Could you give me chance to work with you?
[/quote]

Feel free to DM me.

-------------------------

_Warrior | 2024-04-10 09:20:12 UTC | #9

I sent you.
Pls confirm it.

-------------------------

aliencoder | 2024-04-10 09:22:19 UTC | #10

[quote="_Warrior, post:9, topic:437"]
I sent you.
[/quote]

I didn't receive any DMs over here.

-------------------------

_Warrior | 2024-04-10 09:22:42 UTC | #11

I mean, on Discord.

-------------------------

_Warrior | 2024-04-10 09:28:25 UTC | #12

My Discord name is @shimamuratakehiko.
![image|118x92](upload://jgdPMhmjl8EKELW4nSmtVtWivLP.png)

-------------------------

sugoibtc | 2024-04-10 09:46:03 UTC | #13

I elevated your member status, you should be able to DM now.

-------------------------

_Warrior | 2024-04-10 09:58:31 UTC | #14

Thank you very much.

-------------------------

Bagwing | 2024-05-14 15:55:30 UTC | #15

~Apsis Online

~Permissionaless Poker Table dashboard extentsion in syrius

-------------------------

Bagwing | 2024-05-14 15:58:22 UTC | #16

A user friendly way  to launch and disitrubute tokens  maybe with some sort of white listing contract and an automatic dstirbution.

-------------------------

Stark | 2024-05-17 14:28:43 UTC | #18

Would Supernova be a good environment for BTC ordinals?

-------------------------

aliencoder | 2024-05-17 17:08:25 UTC | #19

Supernova  extension-chain can be the de-facto EVM layer for Zenon. 

I think we need to implement the interoperability at the base-layer (NoM) and let users decide what they want to do with their BTC assets (for example participating in DeFi enabled by the EVM extension-chain).

-------------------------

