Thread: crypto-friendly-jurisdiction-for-apple-developer-account-registration
0x3639 | 2023-06-23 19:30:09 UTC | #1

Start the discussion of crypto friendly jurisdictions to form an entity to create an Apple Developer Account to follow up from the post started here:

> Let’s start with a simple task: [notarize ](https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution/customizing_the_notarization_workflow) Syrius for MacOS. It requires only an Apple developer account to manage [certificates ](https://help.apple.com/xcode/mac/current/#/dev154b28f09) and it’s free.

https://forum.zenon.org/t/publish-syrius-wallet-on-appstores/1481/42?u=0x3639

I'll research and post updates here.

-------------------------

Shazz | 2023-06-24 06:43:34 UTC | #2

Switzerland
Seychelles
Vanuatu
Caymans
Bahamas
Bermuda
Costa Rica
Dubai
British Virgin Islands

-------------------------

aliencoder | 2023-06-24 07:34:41 UTC | #3

I would add the following:

Europe:

- Estonia
- Lithuania
- Malta
- Luxembourg
- Liechtenstein
- Gibraltar

Asia:

- Japan
- Hong Kong
- Singapore

-------------------------

0x3639 | 2023-06-24 11:36:03 UTC | #4

Adding this image here too

https://s3i2u4s3.stackpathcdn.com/original/1X/80b73d688009134c9d96e18628e3567c7e79e245.png

-------------------------

coinselor | 2023-06-26 15:43:04 UTC | #5

These articles might be worth a read for context:

https://a16z.com/tag/legal-frameworks-for-daos-series/

https://daos.paradigm.xyz

I understand the immediate need is just to notarize some code in the AppStore, but I think it will be worth it to consider the entity thinking about future needs that might arise later on for our Network.

-------------------------

angelo_a_jr | 2023-06-28 16:36:59 UTC | #6

Any updates here?  One of the other important items needed for registration will be a ToS + Privacy Policy.

Dug up a few that are hosting similar apps:

Consensys (Metamask) ToS:  https://consensys.net/terms-of-use/
Consensys (Metamask) Privacy Policy:  https://consensys.net/privacy-policy/

Phantom (Solana Wallet) ToS:  https://phantom.app/terms
Phantom Privacy Policy:  https://phantom.app/privacy

Trust Wallet ToS:  https://trustwallet.com/terms-of-services
Trust Wallet Privacy Policy:  https://trustwallet.com/privacy-policy

Strike (BTC payments) ToS:  https://strike.me/legal/tos/
Strike Privacy Policy:  https://strike.me/legal/privacy/

Casa (BTC storage) ToS:  https://keys.casa/terms-of-service/
Casa Privacy Policy:  https://keys.casa/privacy/

-------------------------

0x3639 | 2023-06-28 17:16:35 UTC | #7

Ya, I've been digging through stuff.  Here is my general conclusion.

1) Setting up a DAO for pillars is a nonstarter.  Few if any will participate
2) For me, setting up an entity in a foreign land will be a mistake.  I don't do any international business and have no idea how to setup the entities, how to tax and report them.  I would need to hire an atty to advise me and that is a waste of money.  Then I need to hire a tax professional who does international returns.  More wasted time and money.
3) It's possible I setup a foreign entity and lose protection b/ I'm operating out of the US.  
4) The only option for me is to setup a WY LLC.  I would prefer to do it solo so it's a disregarded entity that does not file a tax return.

I'm going to setup this entity regardless of what others do.  I would encourage other US citizens to setup a WY entity so they can also participate. It costs $150/y and you can keep your identity private but known to a registered agent.  

The setup can be complete in a few days.  That's where I'm at.

I think other international community members in crypto friendly jurisdictions should also create LLCs.

-------------------------

georgezgeorgez | 2023-06-28 19:10:13 UTC | #8

[quote="0x3639, post:7, topic:135"]
* For me, setting up an entity in a foreign land will be a mistake. I don’t do any international business and have no idea how to setup the entities, how to tax and report them. I would need to hire an atty to advise me and that is a waste of money. Then I need to hire a tax professional who does international returns. More wasted time and money.
[/quote]

I haven't done it but from what I've read setting up international for US citizens is very strict. You forget to file a form and consequences are pretty harsh.

-------------------------

angelo_a_jr | 2023-06-28 19:34:03 UTC | #9

If it's all the same to you, just registered a Catawba DAO LLC entity a few days ago and have a pending DUNS number needed for App Store submission.  It is a Zone I plan to work closer with anyways so can proceed accordingly to get this across the line with @aliencoder if that works.

Apps can also be transferred between entities so in the long-run I do think an ideal scenario is a Pillar-operated DAO LLC (whether it is Wyoming, Catawba, or elsewhere).

-------------------------

aliencoder | 2023-06-28 20:54:18 UTC | #10

[quote="angelo_a_jr, post:9, topic:135"]
DUNS number needed for App Store submission
[/quote]

Notarization is not the same as AppStore submission. For notarization, only an active Apple developer account is needed.

AppStore submission can be done later, for example when we have `v0.1.0` ready.

-------------------------

0x3639 | 2023-06-28 22:10:17 UTC | #11

awesome.  you need a DUNS and a website for that entity in order to get a corporate Apple Developer Account.  LMK if you need any help.

-------------------------

0x3639 | 2023-07-04 16:08:26 UTC | #12

Just wanted to double check that you are working on the Corporate Dev Account for Apple.  I'm working on the same so we have two options.  

@angelo_a_jr do you need help with the website?

-------------------------

angelo_a_jr | 2023-07-04 16:53:04 UTC | #13

Just waiting on DUNS number, had to work with Catawba to make sure they were recognized but they were quick to respond.  In correspondence with DUNS now to get it registered.

On a side note, how is the publishing entity going to be able to protect and absolve itself in the event of faulty or [even malicious code](https://thenextweb.com/news/hackers-inject-coin-stealing-malware-into-official-monero-cryptocurrency-wallet).

Ideally this would be a distributed responsibility in the long-term not only to distribute risk for the entity but also adds more leverage to the network.  Pillars as a DAO entity I do think is at least logically the best structure.  Can abstract identities behind an LLC for each Pillar and each Pillar as a DAO actor.

-------------------------

aliencoder | 2023-07-04 17:01:34 UTC | #14

[quote="angelo_a_jr, post:13, topic:135"]
how is the publishing entity going to be able to protect and absolve itself in the event of faulty
[/quote]

Disclaimers.

[quote="angelo_a_jr, post:13, topic:135"]
[even malicious code](https://thenextweb.com/news/hackers-inject-coin-stealing-malware-into-official-monero-cryptocurrency-wallet)
[/quote]

This won't happen for Apple software. They check your code (sometimes even manually) and if it's susceptible to intrusions, they will reject the app. It will also get rejected if it doesn't meet certain security standards.

-------------------------

sol | 2023-07-04 20:26:02 UTC | #15

[quote="aliencoder, post:14, topic:135"]
This won’t happen for Apple software.
[/quote]

Respectfully, this is false. I can develop custom malware for NoM that will bypass their screening process.

-------------------------

aliencoder | 2023-07-04 21:32:06 UTC | #16

[quote="sol, post:15, topic:135"]
I can develop custom malware for NoM that will bypass their screening process
[/quote]

I was referring to the example given in the link.

-------------------------

sol | 2023-07-04 21:40:35 UTC | #17

[quote="aliencoder, post:14, topic:135"]
[quote="angelo_a_jr, post:13, topic:135"]
how is the publishing entity going to be able to protect and absolve itself in the event of faulty
[/quote]

Disclaimers.
[/quote]

[What are your thoughts on code review?](https://forum.zenon.org/t/publish-syrius-wallet-on-appstores/1481/27)

We say "Don't trust. Verify." but who's actually doing this?

-------------------------

aliencoder | 2023-07-04 21:48:12 UTC | #18

[quote="sol, post:17, topic:135"]
We say “Don’t trust. Verify.” but who’s actually doing this?
[/quote]

I didn't exclude code audits for any piece of software, especially for software that will hold user funds (we don't want to be the next AtomicWallet).

-------------------------

sol | 2023-07-04 21:53:43 UTC | #19

Okay, I'm glad you think it's important, but I haven't seen you answer the question with a solution.

We cannot and should not solely rely on Mr Kaine to protect the community.

-------------------------

aliencoder | 2023-07-05 07:06:17 UTC | #20

[quote="sol, post:19, topic:135"]
We cannot and should not solely rely on Mr Kaine to protect the community.
[/quote]

That's why having independent audits is a must.

What should be audited for a mobile app:

- Seed generation (`secure random`) and import
- Wallet derivation (`derivation path`)
- Wallet encryption/decryption (`keyStore`)
- Input sanitization for transaction signing
- Seed screen screenshot/copy protection
- Apps distribution

I found the audit of [Zcash mobile apps](https://electriccoin.co/wp-content/uploads/2020/06/audit-report-v1.3.pdf).

Issues (high and medium severity) found that we should also look after:

- *Severity: High*
  - (Exploitability: N/A) Seed phrase checksum is not validated in the Android app
  - (Exploitability: Likely Impossible) Seed generation timing may leak information about the seed
- *Severity: Medium*
  - (Exploitability: Easy) Official looking text can be controlled through the memo field
  - (Exploitability: N/A) Seed phrase verification is not implemented or enforced
  - (Exploitability: Hard) Users are not informed that Crashlytics collects information
  - (Exploitability: Hard) Unspendable balance from extreme amounts of dust

Here is the [IOTA wallet security audit](https://files.iota.org/papers/Trinity-Sixgen-Assessment.pdf).

-------------------------

sol | 2023-07-05 12:28:09 UTC | #21

[quote="aliencoder, post:20, topic:135"]
That’s why having independent audits is a must.
[/quote]

I'm not certain about this, though I'm not against it.
I think we have enough experience in the community to verify most of our code, but we need to be more methodical and organized.

I'm worried about build-over-build code review.
Updates for Syrius, Dart SDK, Syrius libraries.
Same situation for any "official" app that is published by a doxed individual/entity.

Who will review those?

-------------------------

aliencoder | 2023-07-05 15:07:28 UTC | #22

[quote="sol, post:21, topic:135"]
Who will review those?
[/quote]

We can setup a methodology for independent community review. You, me, @CryptoFish @georgezgeorgez and @sumamu can be part of the audit/review committee.

-------------------------

0x3639 | 2023-07-05 15:36:25 UTC | #23

I've started to setup my structure to open an apple developer account.  This will be a US entity.  I need to get the D&B number and create a website.    Will keep you posted.

-------------------------

0x3639 | 2023-07-13 13:49:20 UTC | #24

@angelo_a_jr did you get your D&B number?  Looks like you need to provide your office address and that then gets published.  Were you aware of that?  How are you addressing that?

-------------------------

angelo_a_jr | 2023-07-13 18:09:01 UTC | #25

Still waiting for response, they unfortunately said up to 30 days, I imagine the Sovereign Nation doesn't make it easier.

As for office address though we are using the Zone as our registered address.  I imagine you could do the same with any entity and a registered agent address service.

-------------------------

0x3639 | 2023-07-13 19:18:52 UTC | #26

OK - that's what I will try too.  thx

-------------------------

0x3639 | 2023-07-21 13:39:55 UTC | #27

I'm still working on this.  I'm trying to get my entity insured.

-------------------------

0x3639 | 2023-07-26 19:13:01 UTC | #28

Still working on insurance.  We are into the market to price it now.

-------------------------

0x3639 | 2023-08-07 21:05:47 UTC | #29

I found someone who will write the insurance.  I just got the application.  Let's see how much it will cost.

-------------------------

angelo_a_jr | 2023-08-12 13:16:46 UTC | #30

You're much further ahead than ours and an insured entity will be much stronger protection.  I don't know if the Catawba entity would be the best after all.

-------------------------

