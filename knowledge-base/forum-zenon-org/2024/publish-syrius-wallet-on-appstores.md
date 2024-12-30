Thread: publish-syrius-wallet-on-appstores
aliencoder | 2023-06-20 19:52:37 UTC | #1

In order to increase the visibility of Zenon and the confidence in using Syrius wallet (especially on MacOS where you're prompted to move it to Trash), we need to list it on major AppStores:

- [Windows Store](https://learn.microsoft.com/en-us/windows/apps/publish/publish-your-app/overview?pivots=store-installer-msix)
- [Mac AppStore](https://developer.apple.com/macos/submit/)
- [Snapcraft](https://snapcraft.io/store) for Linux
- [Flathub](https://flathub.org/) for Linux

-------------------------

dat_she_pepe | 2023-06-15 13:30:38 UTC | #2

The mobile wallet and the extensions should be on stores as well.

-------------------------

aliencoder | 2023-06-15 13:31:10 UTC | #3

Can you help us with the listings?

-------------------------

angelo_a_jr | 2023-06-15 15:30:30 UTC | #4

What do you need specifically?  Just a willing entity with an App Store account?

-------------------------

aliencoder | 2023-06-15 16:27:08 UTC | #5

[quote="angelo_a_jr, post:4, topic:1481"]
What do you need specifically?
[/quote]

Let's see what are the requirements to list Syrius in the first place. I think it's a lot easier than the smart contract audit stuff.

-------------------------

aliencoder | 2023-06-18 11:00:28 UTC | #6

Where do you want to see Syrius published first?

[poll type=multiple results=always min=1 max=4 chartType=bar]
* Windows Store
* Mac AppStore
* Snapcraft (Linux)
* Flathub (Linux)
[/poll]

A good start is to create an Apple developer account and notarize Syrius. Without [Apple's notarization process](https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution), it just looks like a computer virus.

We can either use a [dedicated Flutter library](https://distributor.leanflutter.org/) or standalone packages (for Windows we can use [msix](https://github.com/YehudaKremer/msix/tree/main/example))

-------------------------

romeo | 2023-06-18 12:47:01 UTC | #7

Some info regarding Windows Store:

- Need an MS account (free)
- Need to register a developer account ($20 - requires some level of verification) https://developer.microsoft.com/en-gb/microsoft-store/register/
- some further reading https://learn.microsoft.com/en-gb/windows/apps/publish/publish-your-app/overview

-------------------------

sol | 2023-06-18 14:10:12 UTC | #8

Please inform the community of the costs before asking for a vote.

.msix certificates are a recurring, fluctuating cost in the low $100s/year.

-------------------------

angelo_a_jr | 2023-06-18 14:35:55 UTC | #9

How do we account for legal liability of the publishing account?  Can this be abstracted away somehow?  Certain jurisdiction of publishing entity perhaps?

-------------------------

aliencoder | 2023-06-18 19:57:11 UTC | #10

There are a ton of open source & non-custodial wallets published on various platforms. 

We need to find a solution asap because if we want adoption to happen, we need to act now. Users are always looking for the easiest way to install and run a wallet.

-------------------------

aliencoder | 2023-06-18 19:56:09 UTC | #11

[quote="sol, post:8, topic:1481"]
Please inform the community of the costs before asking for a vote.
[/quote]

For the moment, this thread is just informational. We need to discuss how to distribute Syrius wallet on major app stores for increased visibility & user confidence.

-------------------------

aliencoder | 2023-06-20 19:04:12 UTC | #12

I've done some research regarding Flutter app distribution and this is one of the best tools for the job:

https://distributor.leanflutter.org/

For Linux:

* [appimage](https://github.com/leanflutter/flutter_distributor/blob/main/packages/flutter_distributor/packages/flutter_app_packager/lib/src/makers/appimage) - Create a `AppImage` package for your app.
* [deb](https://github.com/leanflutter/flutter_distributor/blob/main/packages/flutter_distributor/packages/flutter_app_packager/lib/src/makers/deb) - Create a `deb` package for your app.
* [rpm](https://github.com/leanflutter/flutter_distributor/blob/main/packages/flutter_distributor/packages/flutter_app_packager/lib/src/makers/rpm) - Create a `rpm` package for your app.

For MacOS we already have `DMG`. We only need to notarize both the `.app` and the `.dmg`.

For Windows:
* [exe](https://github.com/leanflutter/flutter_distributor/blob/main/packages/flutter_distributor/packages/flutter_app_packager/lib/src/makers/exe) - Create a `exe` package for your app.
* [msix](https://github.com/leanflutter/flutter_distributor/blob/main/packages/flutter_app_packager/lib/src/makers/msix) - Create a `msix` package for your app.
* [zip](https://github.com/leanflutter/flutter_distributor/blob/main/packages/flutter_distributor/packages/flutter_app_packager/lib/src/makers/zip) - Create a `zip` package for your app.

Would you support an AZ project worth 5k ZNN/50k QSR to implement the `flutter_distributor`?

[poll type=multiple results=always min=1 max=1 chartType=bar]
* Yes
* No
[/poll]

After the implementation is complete, we can start publishing the resulting packages.

-------------------------

sol | 2023-06-20 19:35:19 UTC | #13

Why not [Snapcraft](https://docs.flutter.dev/deployment/linux) or brew for Linux?

Challenges/trade-offs with msix and exe should be understood by the community.

Logistically, doxing may be required for binary signing. Who will be responsible for that?

-------------------------

aliencoder | 2023-06-20 19:56:47 UTC | #14

[quote="sol, post:13, topic:1481"]
Why not [Snapcraft](https://docs.flutter.dev/deployment/linux) or brew for Linux?
[/quote]

brew is for Mac :slight_smile: [insert sarcasm]

[quote="sol, post:13, topic:1481"]
Challenges/trade-offs with msix and exe
[/quote]

`exe` with installer/uninstaller is very noob-friendly.

[quote="sol, post:13, topic:1481"]
Logistically, doxing may be required for binary signing. Who will be responsible for that?
[/quote]

Someone that will recognize the added value that publishing will bring for the project.

-------------------------

mehowbrainz | 2023-06-20 19:52:27 UTC | #15

Topic moved to #operations:funding-staging

-------------------------

sol | 2023-06-20 19:54:15 UTC | #16

[quote="aliencoder, post:14, topic:1481"]
brew is for Mac
[/quote]

[zir...](https://docs.brew.sh/Homebrew-on-Linux)

[quote="aliencoder, post:14, topic:1481"]
`exe` with installer/uninstaller is very noob-friendly.
[/quote]

This may be the most viable option on Windows until we decide how we want to sign binaries.

-------------------------

ZNNAYIID | 2023-06-20 20:00:34 UTC | #17

[quote="sol, post:13, topic:1481"]
Who will be responsible for that?
[/quote]

Would you support an AZ project worth 5k ZNN/50k QSR for me to doxx and submit these apps?
[poll type=regular results=always chartType=bar]
* YES
* FOR SURE
[/poll]

-------------------------

romeo | 2023-06-22 01:58:07 UTC | #18

Jokes aside, I would support AZ payment for someone willing to dox and manage the submission/certificate issuance and signing requirements for this use case as well as getting the Syrius exe signed/trusted by Microsoft for use in Windows

-------------------------

aliencoder | 2023-06-22 08:42:52 UTC | #19

If we really want adoption to happen, we **must** publish Syrius in AppStores.

Let's start with a simple task: [notarize](https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution/customizing_the_notarization_workflow) Syrius for MacOS. It requires only an Apple developer account to manage [certificates](https://help.apple.com/xcode/mac/current/#/dev154b28f09) and it's free.

-------------------------

0x3639 | 2023-06-22 08:57:02 UTC | #20

I can look into this.  What does "notarizing" Syrius do for us?  If I were to open a new Apple Developer account, can I generate certificates needed in the notarize process?

I want to make sure I don't violate the TOS.  I'm assuming this would need to be some sort of "team" account given that I'm not the one writing the code.

-------------------------

aliencoder | 2023-06-22 09:04:11 UTC | #21

[quote="0x3639, post:20, topic:1481"]
What does “notarizing” Syrius do for us?
[/quote]

When you first install Syrius on MacOS, you're prompted to move it to Recycle Bin. This happens because the binary is not signed by Apple aka notarized.

This **does not** mean that Syrius is published on the Mac AppStore.

[quote="0x3639, post:20, topic:1481"]
can I generate certificates needed in the notarize process
[/quote]

Yes. I can make a [Github Action](https://github.com/marketplace/actions/xcode-notarization-action) for the notarization process.

Required parameters:

```
apple-id: ${{ secrets.APPLE_ID }}
password: ${{ secrets.PASSWORD }}
team-id: ${{ secrets.TEAM_ID }}
```

-------------------------

0x3639 | 2023-06-22 09:04:32 UTC | #22

So what does the certificate certify?  I assume it notarizes the code with a certificate tied to an individual.  So if the code turns out to be a virus, they know who to go after?

-------------------------

aliencoder | 2023-06-22 09:10:33 UTC | #23

[quote="0x3639, post:22, topic:1481"]
So what does the certificate certify?
[/quote]

That the binary is checked by Apple.

[quote="0x3639, post:22, topic:1481"]
So if the code turns out to be a virus, they know who to go after?
[/quote]

If it has a virus, the binary won't pass the notarization process, so it won't be notarized.

You [cannot notarize](https://support.apple.com/guide/security/protecting-against-malware-sec469d47bd8/web) a malicious app:

"*Notarization* is a malware scanning service provided by Apple. Developers who want to distribute apps for macOS outside the App Store submit their apps for scanning as part of the distribution process. Apple scans this software for known malware and, if none is found, issues a Notarization ticket."

-------------------------

0x3639 | 2023-06-22 10:18:08 UTC | #24

This seems like something we should do for sure.  Does anyone disagree?

-------------------------

sol | 2023-06-22 17:44:02 UTC | #25

[quote="aliencoder, post:23, topic:1481"]
You [cannot notarize ](https://support.apple.com/guide/security/protecting-against-malware-sec469d47bd8/web) a malicious app:
[/quote]

Challenge accepted. /s
[1](https://objective-see.org/blog/blog_0x4E.html) and [2](https://lifehacker.com/great-now-the-apple-app-store-has-malware-too-1849386738)

Who will be allowed to notarize copies of Syrius?

I'm having trouble finding fee information for this process. Is it $100/year to notarize and list on the AppStore?

To avoid revocation of our signing accounts, we may want to implement an internal code review process.

-------------------------

aliencoder | 2023-06-22 14:56:59 UTC | #26

[quote="sol, post:25, topic:1481"]
Challenge accepted. /s
[1 ](https://objective-see.org/blog/blog_0x4E.html) and [2 ](https://lifehacker.com/great-now-the-apple-app-store-has-malware-too-1849386738)
[/quote]

These are exceptions.

-------------------------

sol | 2023-06-22 15:24:24 UTC | #27

Yeah, they are exceptions, but I think we shouldn't rely on the MacOS notary process for malware identification.

What about my other question? 
Will you be notarizing your dev builds?

How do you feel about code review?

-------------------------

aliencoder | 2023-06-22 20:43:47 UTC | #28

[quote="sol, post:25, topic:1481"]
Challenge accepted. /s
[/quote]

I'm here not to challenge you. I want to help you, if I can. Create value.

[quote="sol, post:27, topic:1481"]
we shouldn’t rely on the MacOS notary process for malware identification.
[/quote]

The purpose of notarization is to avoid the nasty popup dialog that prompts you to move Syrius to Trash.

[quote="sol, post:25, topic:1481"]
I’m having trouble finding fee information for this process. Is it $100/year to notarize and list on the AppStore?
[/quote]

The developer account is $100/year. I don't know yet if we need a dev account to notarize apps.

[quote="sol, post:27, topic:1481"]
Will you be notarizing your dev builds?
[/quote]

We only need to notarize releases. Only stable releases will be opened by regular users that don't know how to bypass the `Move to Trash` dialog (`System Preferences -> Security & Privacy -> General -> Open anyway`)

-------------------------

aliencoder | 2023-06-22 22:25:30 UTC | #29

[quote="aliencoder, post:28, topic:1481"]
I don’t know yet if we need a dev account to notarize apps.
[/quote]

We need a [paid developer account as per this blog post](https://scriptingosx.com/2021/07/notarize-a-command-line-tool-with-notarytool/):

"You need either the paid membership in the [Apple Developer Program](https://developer.apple.com/programs/) or be invited to an [Apple Developer Enterprise Program](https://developer.apple.com/programs/enterprise/) team with access to the proper certificates.

You cannot get the required certificates with a free Apple Developer account, unless you are member of a team that provides access."

We also need to adjust the building process by enabling *Hardened Runtime*.

-------------------------

0x3639 | 2023-06-22 23:15:20 UTC | #30

Need LLC and website associated w/ that LLC. 

https://developer.apple.com/programs/enroll/

-------------------------

0x3639 | 2023-06-22 23:24:47 UTC | #31

it costs $100 for an individual and $300 for an entity.  It requires a full doxing with drivers license, operating agreements, D&B registrations, proof of address.

https://developer.apple.com/support/app-account/

-------------------------

aliencoder | 2023-06-23 07:38:10 UTC | #33

I think for the moment an individual account is enough for the moment.

-------------------------

cryptocheshire | 2023-06-23 10:19:02 UTC | #37

It's easy if someone is willing to doxx. If not, different q.

-------------------------

0x3639 | 2023-06-23 12:03:42 UTC | #38

I will consider this but only as an LLC. I’ll investigate further.

-------------------------

angelo_a_jr | 2023-06-23 14:50:16 UTC | #39

I'd be open to forming a joint LLC (or other entity type) for this purpose if that is of interest for the sake of getting this published.  Perhaps also leveraging one of the more web3 friendly jurisdictions such as Catawba or Wyoming.

EDIT:  Tagging @mehowbrainz here as well who will also likely need an entity of sorts for some of the marketing efforts:  https://forum2.zenon.org/t/global-adoption-a-user-experience-and-regulatory-effort/1508?u=angelo_a_jr

CC: @LegalZNN what liability if any would the LLC have for the Syrius mobile wallet as just the publisher for the App Store?  Can we absolve liability of the LLC since the underlying infra behind the wallet UI is all open source?

It would benefit for more than just this publishing to have some joint entity (501c3, LLC, DAO LLC, etc.) for Zenon community that can start to act in the "real world" for Zenon community initiatives.

-------------------------

0x3639 | 2023-06-23 17:53:05 UTC | #40

I'm going to spend some time on this topic.  I wonder if the Pillars can form a DAO in WY so we can engage with firms like Apple and others.  I'm going to add this discussion over here too.

https://forum.hypercore.one/t/embedded-governance-design/129/42

The more advancements we make the more we will need some corporate entity to do "stuff".  In the case of Apple, i needs to be "legit" with a website and org docs, etc..

-------------------------

dat_she_pepe | 2023-06-23 18:27:27 UTC | #41

I won't be a part of any DAO or legal entity involving U.S.A. If Zenon succeed, they'll try to grab whatever they can have a hold on. Build in the Seychelles.

-------------------------

aliencoder | 2023-06-23 18:32:28 UTC | #42

[quote="dat_she_pepe, post:41, topic:1481"]
Build in the Seychelles
[/quote]

There are a dozen of other crypto-friendly jurisdictions around the world.

Can you start another thread on this issue?

-------------------------

romeo | 2023-06-24 23:48:18 UTC | #43

Good discussion on this issue here

https://news.ycombinator.com/item?id=31763451

-------------------------

romeo | 2023-06-24 23:50:41 UTC | #44

[quote="0x3639, post:40, topic:1481"]
I’m going to spend some time on this topic. I wonder if the Pillars can form a DAO in WY so we can engage with firms like Apple and others. I’m going to add this discussion over here too.
[/quote]

> "Assuming you are in the US, and depending on your state laws, you can go to your County Clerks office and file an Assumed Name for Unincorporated Business (DBA). That is enough to open a business bank account and use that name for the Apple Developer program. It also won't have all your information plastered all over the place like LLCs/Corps (from personal experience with both)"

Not sure how legitimate that statement is though

-------------------------

romeo | 2023-06-25 04:14:33 UTC | #45

I'm wondering if no one's wants to dox can we just hire a developer for the sole purpose to publish Syrius under their apple developer ID

-------------------------

aliencoder | 2023-06-25 09:07:43 UTC | #46

[quote="aliencoder, post:34, topic:1481, full:true"]
I don’t think this would be a good idea. What happens if the account gets suspended or invalidated? What happens if that user posts crap apps beside Syrius? What happens if he changes descriptions or other stuff?
[/quote]

We've already discussed this.

-------------------------

romeo | 2023-06-25 09:49:23 UTC | #47

We can take ownership of the account as part of the deal, essentially hiring someone's ID then they pass the creds over to us. No idea if anyone would go for it though

-------------------------

0x3639 | 2023-06-25 16:51:30 UTC | #50

No, If I do this I will do it the "right" way.  I think I have a path to provide the protection I'm looking for.  It's going to take some time to set this up, but I think I can do it.

-------------------------

romeo | 2023-06-25 22:08:04 UTC | #52

Breaking the Apple TOS isn't breaking the law

-------------------------

aliencoder | 2023-06-26 07:43:26 UTC | #53

I agree with @dat_she_pepe and avoid US incorporation. There are many crypto-friendly jurisdictions around the world.

-------------------------

cryptocheshire | 2023-06-26 11:49:51 UTC | #54

Couldn't agree more. We should stay away from US exposure by any means necessary

-------------------------

LegalZNN | 2023-06-29 21:45:30 UTC | #55

Hello, Angelo. Thanks for tagging me here.

The LLC would be assuming full legal and compliance responsibility. I recommend handling this with great care and evaluating each step carefully.

DAOs are not the holy grail many people think it is. Depending on the circumstances, they could actually be riskier than traditional entities such as an LLC or a Corporation. A recent case, for reference:

https://www.klgates.com/CFTC-Asserts-Jurisdiction-Over-DAOs-in-Groundbreaking-Enforcement-Action-9-29-2022
*The order also imposes personal liability on certain of the Ooki DAO’s tokenholders as active participants, an argument which the CFTC asserts is based on partnership law: “**Individual members of an unincorporated association organized for profit are personally liable for the debts of the association …**” (emphasis added). As noted above, the **CFTC considers a DAO to meet the federal definition of an “unincorporated association” because it is a “voluntary group of persons … without a charter … formed by mutual consent for the purpose of promoting a common objective.”***
*As defined by the CFTC, any tokenholder who voluntarily votes his or her tokens to affect the outcome of a DAO governance vote is considered to be a “member” of the DAO. This should be considered as a serious warning sign to DAO tokenholders who are active in voting on governance issues: beware the extra-legal activities of the DAO, as you may be left holding the bag. This does, however, exclude passive tokenholders, which is a meaningful distinction, given that governance participation is not mandatory and that governance tokens liquidly trade on decentralized exchanges.*

I could formulate a project to do detailed research on this, determining the ideal steps to follow that would minimize, to the minimum possible, the regulatory and legal risk of publishing mobile applications. Is this something the community would be interested in?

Looking forward to your comments,
Legal

-------------------------

cagri | 2023-12-21 17:54:45 UTC | #56

What is the last status of this topic?

-------------------------

TheDev1776 | 2024-04-02 15:50:03 UTC | #57

Perhaps we spin one of these up? 

https://a16zcrypto.com/posts/article/duna-for-daos/

-------------------------

