Thread: ledger-hardware-wallet-for-s-y-r-i-u-s
CryptoFish | 2023-05-24 07:12:25 UTC | #1

The full Accelerator-Z proposal can be found here at https://github.com/hypercore-one/ledger-app-zenon/blob/main/az.md

-------------------------

0x3639 | 2023-04-30 16:22:43 UTC | #2

Wow.  This is a super exciting and needed project.  I'm happy to help in any way possible.  I suspect an audit would cost more (a lot more) than the bridge.  Maybe I can work with some other pillars to get together the funds to pay for an audit in the future.  So maybe that can be our contribution when the time comes.  

Also happy to help with any project management / coordination type activities.

-------------------------

mehowbrainz | 2023-04-30 16:26:53 UTC | #3

Congrats on the project. I will temporarily move it to #development:funding-staging and once you submit it on-chain we will move it back to #development:funding-submissions.

-------------------------

CryptoFish | 2023-04-30 18:26:06 UTC | #4

[quote="mehowbrainz, post:3, topic:1405, full:true"]
Congrats on the project. I will temporarily move it to #development:funding-staging and once you submit it on-chain we will move it back to #development:funding-submissions.
[/quote]

Thanks.

[quote="0x3639, post:2, topic:1405"]
Wow. This is a super exciting and needed project. I’m happy to help in any way possible. I suspect an audit would cost more (a lot more) than the bridge. Maybe I can work with some other pillars to get together the funds to pay for an audit in the future. So maybe that can be our contribution when the time comes.
[/quote]

@0x3639 Not sure what pricing we're talking about yet, will try to find out some estimates and include it in the final proposal. One of the requirements for auditing a developer release is that the coin needs to be in the top 600 on CMC. Not that much of an issue the way we're currently going (rank #692). More on the conditions can be found [here](https://developers.ledger.com/docs/embedded-app/security-audit/#conditions).

-------------------------

aliencoder | 2023-04-30 19:09:31 UTC | #5

Hardware wallet support is important for the masses.

I've already started working on an implementation for the Syrius <-> Ledger connection.

The Ledger device should only sign the final `accountBlock` and Syrius will populate all required fields including generating Plasma via PoW, if necessary.

We need someone that has in-depth `Rust` knowledge to code the embedded app. I think it's both easier and *safer* than using plain old `C`.

Examples of Ledger apps in Rust:

https://github.com/LedgerHQ/app-avalanche
https://github.com/LedgerHQ/app-blockstack
https://github.com/LedgerHQ/app-sui
https://github.com/LedgerHQ/app-pocket

Other resources:
https://github.com/alamgu/alamgu-example

But first I need to finish all other projects :slight_smile:

-------------------------

shaimo | 2023-04-30 20:14:20 UTC | #6

Ledger support would be incredible, especially for all of us long term holders.
Do keep in mind that full support will likely require some changes not only to Syrius itself, but probably also to the APIs, and possibly also to some of the internal contracts. A couple of examples:
- For complete support we will need a way to move pillars/sentinels from one address to another without dismantling them (and re-burning QSR, etc). Without this all existing pillars/sentinels will forever stay in “hot” wallets. 
- To receive “unreceived” transfers, does Syrius need to implicitly sign something? If so, then likely a UI change will be needed to show unreceived transactions and ask the user to sign them on the ledger. It’s a bit less convenient, but at least it gives more control and I’m not sure there is any way around it anyway.

-------------------------

CryptoFish | 2023-05-01 08:05:02 UTC | #7

Thanks for the resources @aliencoder

`Rust` is indeed an easier and safer option. The [sdk for rust](https://github.com/LedgerHQ/ledger-nanos-sdk) seems to lack behind the [official sdk](https://github.com/LedgerHQ/ledger-secure-sdk) a bit, but it will probably be enough for our requirements. I'll make sure to include it in the proposal.

[quote="shaimo, post:6, topic:1405"]
For complete support we will need a way to move pillars/sentinels from one address to another without dismantling them (and re-burning QSR, etc). Without this all existing pillars/sentinels will forever stay in “hot” wallets.
[/quote]
Exactly, although creating another address would be the least desired option. Wouldn't it be possible to use the same BIP-39 24-word mnemonic to create the [master seed](https://developers.ledger.com/docs/embedded-app/psd-masterseed/) for the Ledger device.

[quote="shaimo, post:6, topic:1405"]
To receive “unreceived” transfers, does Syrius need to implicitly sign something? If so, then likely a UI change will be needed to show unreceived transactions and ask the user to sign them on the ledger. It’s a bit less convenient, but at least it gives more control and I’m not sure there is any way around it anyway.
[/quote]
You need to sign to receive unreceived transactions. I believe this was already on the list of s y r i u s improvements. The ability to automatic/manual receive transactions. Whatever the case, the UI will need to able to handle both cases. The file based wallet implementation of the SDK's will need a layer of abstraction. This way s y r i u s can just use the abstract interface for interacting with the wallet.

-------------------------

shaimo | 2023-05-01 08:28:03 UTC | #8

[quote="CryptoFish, post:7, topic:1405"]
Exactly, although creating another address would be the least desired option. Wouldn’t it be possible to use the same BIP-39 24-word mnemonic to create the [master seed](https://developers.ledger.com/docs/embedded-app/psd-masterseed/) for the Ledger device.
[/quote]

This is likely possible, but imo it's not an acceptable solution. The whole point of using a ledger is that your private key (and seed) were never shared in a digital form. When you created the syrius wallet and got the seed it was already on your PC (or wherever you created it). Moving it to a ledger is pointless even if you delete it from your PC. Once it was there this could no longer be considered a cold wallet and will never be as secure as such...
So to do it right I see no way around it other than allowing migration of pillars/sentinels to new addresses.

-------------------------

CryptoFish | 2023-05-01 09:08:09 UTC | #9

[quote="shaimo, post:8, topic:1405"]
This is likely possible, but imo it’s not an acceptable solution. The whole point of using a ledger is that your private key (and seed) were never shared in a digital form. When you created the syrius wallet and got the seed it was already on your PC (or wherever you created it). Moving it to a ledger is pointless even if you delete it from your PC. Once it was there this could no longer be considered a cold wallet and will never be as secure as such…
So to do it right I see no way around it other than allowing migration of pillars/sentinels to new addresses.
[/quote]
You're right, valid points and having the ability to migrate pillars/sentinels is a useful feature no matter the application. The consequences of a change of address will have to be thoroughly investigated. Although it is certainly useful to have this functionality, I don't consider it a requirement for the Hardware wallet. Maybe this is something for the go-zenon devs to pick up on?

-------------------------

shaimo | 2023-05-01 09:29:00 UTC | #10

Agreed - would consider it an independent feature (that would be very valuable once we have ledger support).

-------------------------

CryptoFish | 2023-05-24 07:13:13 UTC | #11

I've worked out the proposal and would like to ask the community for a final round of feedback before submitting the proposal.

The full Accelerator-Z proposal can be found here at https://github.com/hypercore-one/ledger-app-zenon/blob/main/az.md

@aliencoder you have indicated that you are working on the implementation of the Syirus <-> Ledger link. Can you give more details about what exactly you are working on, how you plan to make it and why you started with the implementation of the connection?

-------------------------

aliencoder | 2023-05-15 15:09:31 UTC | #12

[quote="CryptoFish, post:11, topic:1405"]
Can you give more details about what exactly you are working on, how you plan to make it and why you started with the implementation of the connection?
[/quote]


Basically the communication between Syrius (Dart code) and the Ledger device. I plan to use existing libraries and open source code. I've started with the implementation of the connection because it's the most basic thing that we can start with:
- Detect the Ledger device in Syrius
- Open a port (via USB) on the Ledger device (Nano Ledger S and X)
- Send raw bytes to the Ledger device (account block with Plasma computed by Syrius)
- Listen to the raw bytes (account block signed)
- Publish the account block and propagate it into the network

I want to mention that the connection to the Syrius desktop wallet will be available over an USB port.

Only Nano Ledger X supports Bluetooth. It's suitable for the mobile apps integration.

-------------------------

mr.ztark | 2023-05-16 12:57:42 UTC | #13

![image|330x500](upload://umIbIs6zKIOEcOuKzWhFObWBjY9.jpeg)
![image|230x500](upload://wgtAn2bxq45ldpv7BhBtH4R3MnZ.jpeg)

-------------------------

NeoShredder | 2023-05-16 16:41:43 UTC | #14

Not owning your own keys anymore huh!

-------------------------

CryptoFish | 2023-05-16 21:05:57 UTC | #15

Thanks for the update @mr.ztark 

The feature seems to be optional and only for Ledger Nano X devices, but still definitely a step in the wrong direction if you ask me.

-------------------------

romeo | 2023-05-17 03:08:45 UTC | #16

They'll have to revert I imagine, the added revenue from the recovery subscription likely won't offset lost sales/customers who are impacted by this change

-------------------------

aliencoder | 2023-05-17 07:11:26 UTC | #17

The worst part is that they set a precedent. Basically they publicly admitted that they can "manage" your private keys OTA. They literally shitted on their security model (private keys don't leave the device). I won't trust them from now on with any of their products.

-------------------------

sumamu | 2023-05-17 11:21:35 UTC | #18

[quote="romeo, post:16, topic:1405, full:true"]
They’ll have to revert I imagine, the added revenue from the recovery subscription likely won’t offset lost sales/customers who are impacted by this change
[/quote]

They might not have that option. If the only 2 options were `leak private keys` OR `shut down the service`, they probably chose the 2nd one so they can continue to "milk" the business.

Otherwise I don't see how a business could misunderstand its own product at such a level.

-------------------------

aliencoder | 2023-05-17 20:31:05 UTC | #19

I'll do a poll to gauge the community interest in developing a Ledger implementation given the (bad) news.

[poll type=multiple results=always min=1 max=2 chartType=bar]
* Go ahead with Ledger
* Ledger can be considered compromised
* Other hardware wallet implementation
[/poll]

-------------------------

cryptocheshire | 2023-05-17 21:14:38 UTC | #20

Pretty sure that the majority of users won't care or are even glad to have a backup option. Dont forget why so many people would pay to hold crypto at a bank. Only few are so dogmatic about self custody. We need multi hw and sw wallet support anyway.

-------------------------

sumamu | 2023-05-18 07:22:03 UTC | #21

[quote="aliencoder, post:19, topic:1405"]
I’ll do a poll to gauge the community interest in developing a Ledger implementation given the (bad) news.
[/quote]

If progress has already been done on the subject, why not finish it? 

Maybe people will continue to use Ledger HW or maybe they won't, but either way, it's a good exercise and it will make implementing other HW easier.

-------------------------

0x3639 | 2023-05-18 08:57:17 UTC | #22

I personally think this is a flash in the pan issue. I believe they will with "fix" the public relations issue or technical issue.  Or both.  Ledger seems to have wide adoption and with their new model coming out soon I don't think they are going away.  

These devices need social recovery for people who cannot manage their own keys.  That solution will iterate and change over time.  They will solve that issue, because social recovery is necessary for wide crypto adoption.  

So who is going to solve social recovery "well"?  Who has wide customer adoption? Who is likely to be around in 5 to 10 years?  

Probably Ledger.

-------------------------

cryptocheshire | 2023-05-18 09:32:41 UTC | #23

Yup!

-------------------------

coinselor | 2023-05-20 00:34:31 UTC | #24

Probably a player not (fully) in crypto yet, but with the user base.

-------------------------

CryptoFish | 2023-05-23 19:27:05 UTC | #25

After the community feedback I think it is safe to proceed with the az proposal. I propose to close this thread and give the last word to the pillars by submitting the proposal.

-------------------------

cryptocheshire | 2023-05-23 20:17:22 UTC | #26

https://twitter.com/NFTherder/status/1661026174779420672?t=VAs6DG71V_m2rpUBTCTvOg&s=19

-------------------------

CryptoFish | 2023-06-09 07:48:47 UTC | #27

The proposal was recently accepted. Thanks for your confidence. We will do our best to deliver the best possible product. Further updates on the project will be posted on the [HyperCore-One](https://forum.hypercore.one/) forum.

See the link below.

https://forum.hypercore.one/t/project-ledger-zenon-app/112

-------------------------

aliencoder | 2023-06-15 09:07:44 UTC | #28

[quote="sumamu, post:18, topic:1405"]
Otherwise I don’t see how a business could misunderstand its own product at such a level.
[/quote]

I want to highlight a very important paragraph from [Apple's secure enclave documentation](https://developer.apple.com/documentation/security/certificate_key_and_trust_services/keys/protecting_keys_with_the_secure_enclave):

**Can’t encode preexisting keys. You must use the Secure Enclave to create the keys. Not having a mechanism to transfer plain-text key data into or out of the Secure Enclave is fundamental to its security.**

Ledger is playing us.. don't trust them. (to be clear, I'm not saying anything against the proposal/project, just general info for everyone)

-------------------------

