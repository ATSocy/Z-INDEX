Thread: frosted-the-first-step-towards-a-seedless-future
aliencoder | 2024-01-26 20:26:59 UTC | #1

# FROSTED seedless wallet

[FROSTED](https://github.com/alienc0der/frosted) is a Flutter demo application that integrates a Rust-based implementation of the [FROST](https://github.com/ZcashFoundation/frost) (Flexible Round-Optimized Schnorr Threshold) by the Zcash Foundation. 

It showcases an interactive demo, primarily focused on building cryptocurrency seedless wallets using threshold signatures, enhancing security and flexibility for blockchain users.

## Why?

Most of you are familiar with [BIP39 cryptocurrency wallets](https://www.blockplate.com/blogs/blockplate/one-seed-phrase-bip39-wallet). The problem with such a wallet is obvious: if your seed is compromised, your funds are gone.

## Can we do better?

* **Distributed Trust**: In seed-based wallets, the entire security hinges on the seed phrase. If this seed is compromised, all associated assets are at risk. In contrast, seedless wallets distribute trust across multiple key shards. An attacker would need to compromise multiple shards to gain control, significantly raising the security bar.
* **Reduced Single Points of Failure**: By avoiding a single seed phrase, seedless wallets eliminate a critical single point of failure. This distributed approach to key management reduces the risk of total asset loss due to single key compromise.

## Key shard security

This is the most important aspect: the key shards must be encrypted and stored separately such that an attacker is unable to perform the `keysign` operation.

Example for 2 out of 3 threshold setup:
- One key shard protected by the secure enclave of the processor
- One key shard backed up on a cloud provider
- One key encrypted using a `PIN` or `passphrase`

In the future, it can be integrated in both Syrius desktop and Syrius mobile wallets.

PS: I'm planning to apply for an AZ grant for this project.

-------------------------

aliencoder | 2024-01-27 09:20:53 UTC | #2

A demo is worth a thousand words:

I invite you to test the [latest release](https://github.com/alienc0der/frosted/releases/tag/master).

-------------------------

0x3639 | 2024-01-27 11:32:06 UTC | #3

Very cool.  Maybe @Nostromo can use this with the Gravity Wallet?

@aliencoder if you have 2 of 5 required, would you sign a TX in syrius AND would you need to use another device to sign also?

Or, do you map the location of the other seed shards in Syrius and sign all shards right from syrius?  If a second device is not needed to sign, can an attacker compromise syrius and download the mapped shards and still sign messages?

![Screenshot 2024-01-27 at 5.18.40 AM|630x500](upload://rIWm4alT3GGTIkJoEhjx9MDWYKp.jpeg)
![Screenshot 2024-01-27 at 5.18.30 AM|633x500](upload://hvrGsZGtaT7zs4l1qiKHPO4ZYHT.png)
![Screenshot 2024-01-27 at 5.18.17 AM|631x500](upload://cXAVzM6hOFnyaOLZ0ICGNrAidG0.png)

-------------------------

aliencoder | 2024-01-27 21:10:31 UTC | #4

[quote="0x3639, post:3, topic:326"]
@Nostromo can use this with the Gravity Wallet?
[/quote]

Yes. And Dr. Blaze with the Syrius Mobile Wallet.

[quote="0x3639, post:3, topic:326"]
@aliencoder if you have 2 of 5 required, would you sign a TX in syrius AND would you need to use another device to sign also?
[/quote]

All the operations are performed locally. It is implemented using the `Trusted Dealer` setup that assumes a trusted entity (eg. the non-tampered app on your certified device) to run the `keygen` ceremony.

The security of the `FROSTED` implementation comes from the idea that every key shard should be decrypted only by an authorized party.

[quote="0x3639, post:3, topic:326"]
If a second device is not needed to sign, can an attacker compromise syrius and download the mapped shards and still sign messages?
[/quote]

Think it this way: you can have 2 shards on your mobile device, one encrypted by your `secure enclave processor` and another one by a `passphrase`. The attacker needs *both* your `FaceID`/`TouchID` *and* your passphrase in order to be able to perform a successful `keysign` ceremony. The 3rd shard (backup shard) can be safely stored on your `Google Drive` or `iCloud` account. 

So the attacker must spoof your passphrase *and* compromise your `Google Drive` or `iCloud` account (assuming that he is not a nation-state that can break into the `secure enclave`), which is significantly harder than social engineering a user into giving up his `mnemonic`.

-------------------------

coinselor | 2024-01-28 15:16:49 UTC | #5

Seedless under the right setup seems to be a lot less stressful than managing the security of a 24 word seedphrase. Backups, social recovery, etc all becomes much more manageable.

I recently came across the concept of ICP's [Oisy wallet](https://github.com/dfinity/oisy-wallet). I didn't fully grasp the technical implementation; it appears to involve an embedded contract and some form of ID layer, which already raises some privacy concerns. Nevertheless, it seems to effectively implement a similar seedless multi-party threshold signature.

What I found particularly impressive was the user experience of the wallet, which requires no app or extension installation. If we can replicate this while simultaneously including PoW providers for a truly feeless onboarding experience, that could be something truly amazing.

-------------------------

aliencoder | 2024-01-28 22:02:54 UTC | #6

[quote="coinselor, post:5, topic:326"]
I didn’t fully grasp the technical implementation
[/quote]

`FROST` is far superior than ICP's [ECDSA TSS](https://internetcomputer.org/docs/current/developer-docs/integrations/t-ecdsa/).

-------------------------

coinselor | 2024-01-29 06:32:04 UTC | #7

:cold_face: :cold_face:

-------------------------

