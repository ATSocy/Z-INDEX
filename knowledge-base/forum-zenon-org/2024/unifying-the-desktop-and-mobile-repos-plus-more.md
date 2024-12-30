Thread: unifying-the-desktop-and-mobile-repos-plus-more
john.maxwell | 2024-09-18 15:22:50 UTC | #1

Hello!

I'm an experienced Flutter developer, having built apps for desktop, mobile and web, with a newly discovered passion for cryptocurrencies and with the help of @DrBlaze_21 I found out about the Zenon project.

Until now, for Zenon, I've already delivered some work for the Syrius mobile app and I also looked through the Syrius desktop app repository.

All this being said, I would like to propose the following to the community:

1. Unify the desktop and mobile repos

* This will involve making the desktop code base modular and integrating BTC and EVM support in the desktop app
* Uplift the security of the desktop wallet (starting with secure storage and local authentication)
* Use clean Material UI elements (like the ones used in the mobile app)
* Make the code more maintainable (the design will, largely, be unmodified)
* Bug fixing and unit testing
* Improved documentation

Budget asked: 3-4 AZ projects

Time: 10 - 12 weeks

2. Feature mirroring and multi-wallet support

* Porting features from the desktop app to the mobile app and the other way around (integrate the P2P swaps in the mobile app, desktop WebView). Those tasks will depend largely on what Flutter packages are available for both desktop and mobile.
* Add multi-wallet support

Budget asked: 2-3 AZ projects

Time: 6-8 weeks

3. Feedback integration and further improvements

* Here you can propose changes and features, and depending on their complexity, they might or not be included in the already specified budget.

I am now available to work full time and I already have another friend that can help me with the testing part (both manual and unit testing).

After I finish the work, it will be much easier for new devs to develop and integrate new features for both the desktop and mobile apps (including adding support for more blockchain networks).  I will also be available for new projects and open to collaborate with other community members. This includes providing guidance and onboarding of new Flutter developers that want to learn and create new features for the Syrius wallet.

For any questions, please leave a comment.

-------------------------

0x3639 | 2024-09-18 19:02:47 UTC | #2

Are you aware that other devs are currently scoping improvements to the SYRIUS desktop app.  They have established a SYRIUS Special Interest Group and are looking for additional contributors.  

https://zenon.wiki/index.php/Syrius_SIG

We also have a matrix chat where we are discussing the scope of improvements.  If you can DM me your matrix username I'm happy to add you there also.

I also wanted to point out that the devs in the group have been involved with several improvements to syrius, including the p2p HTLCs,  PTLCs, ledger integration, and countless other improvements.  I hope we can work together in the open with support and collaboration with the community.  An AZ this large really needs transparency.

-------------------------

DrBlaze_21 | 2024-09-18 20:03:14 UTC | #3

I fully endorse @john.maxwell. I'll explain why:

He's a senior developer that can handle all the complexities required by the unification of the Syrius Desktop and Mobile repositories. He has extensive cryptography knowledge and he masters the best practices in developing cross-platform Flutter apps.

I can give you 2 concrete examples:

- Bitcoin Taproot integration (including custom `UTXO` management, `RBF` support, etc)
- Migrated [hive](https://pub.dev/packages/hive) package (unmaintained) to [drift](https://pub.dev/packages/drift) (this will also benefit Syrius desktop)

@0x3639 the fact that he's able to do it full time is one of the most important things in this proposal (and the proposed timeline). We want to be prepared for the upcoming bullrun with an up to date, native cross-platform Syrius with a modular codebase that's both easy to maintain and upgrade.

-------------------------

0x3639 | 2024-09-18 20:34:42 UTC | #4

Thank you for that vote of confidence.  And thank you for introducing him to the project!!  I hope you and John can join the SYRIUS SIG so all the devs can coordinate the scope and hopefully work together.  

@DrBlaze_21 it would be helpful if you joined that group too.  The devs in the group are very skilled and have a proven track record of working collaboratively.  You can join by creating a matrix account and DM me your username.  I will invite you to that group.  

Here is an example of how we've been running a different group:
https://zenon.wiki/index.php/HC1:_Operations_SIG

-------------------------

coinselor | 2024-09-18 21:28:17 UTC | #5

Thanks for your interest and for helping Blaze integrate BTC into the mobile app.

For completeness, [here's the recent initiative](https://forum.hypercore.one/t/syrius-sig-collaboration/488) that @0x3639 mentioned. It seems to require a major refactor of the syrius desktop UI. I believe it's a great time to coordinate efforts and structure moving forward. If we want to set the foundation for onboarding more developers into Syrius in the future, this would be a great approach.

-------------------------

Stark | 2024-09-19 01:03:54 UTC | #6

Welcome to Zenon. Thank you for this proposal.

Do you have a sense of whether you are most interested in:

1. Earning ZNN and QSR to hodl / stake / delegate.
2. Accumulating ZNN and QSR for infrastructure (a pillar?)
3. Earning $$$ for short to medium term income.

The community has a strong culture and it might be helpful to know: 

What is your impression of Zenon?
Why you have chosen to offer to work on Syrius?

-------------------------

0x3639 | 2024-09-19 14:58:27 UTC | #7

[quote="john.maxwell, post:1, topic:1940"]
Add multi-wallet support
[/quote]

Can you please elaborate on what this means exactly?

-------------------------

john.maxwell | 2024-09-19 18:15:29 UTC | #8

Right now, with the mobile and desktop app, you can only import or create one wallet, that can hold cryptocurrencies for you. If you want to create another wallet and manage your assets, you will need to delete the current wallet and create a new one.

With the multi-wallet support you will be able to manage more easily your assets from different wallets. In one app session, you could create a wallet for holding ZNN, one for ETH and one for BTC, for example.

-------------------------

0x3639 | 2024-09-19 19:03:42 UTC | #9

Great feature!  That would be super helpful.

-------------------------

john.maxwell | 2024-09-19 19:39:36 UTC | #10

I'm more interested in holding the assets, but I don't have a clear strategy for generating rewards long term. I haven't thought that long in advance

What I like most about the Zenon project is the decentralized philosophy: behind the project there is not one, or a few people, but a community. The dual coin system, the fee-less transfers and the reward distribution are other things that I found appealing.

The main reason that I offered to work on Syrius is that I have the right skills to help the project grow, and the things that I proposed for implementation will benefit the community and the ends users. I'm passionate about Flutter, and I enjoy working on a diverse set of Flutter projects.

-------------------------

aliencoder | 2024-09-20 06:12:21 UTC | #11

Yes, especially for Pillar owners that will be able to import the `producer` keystore and vote AZ projects while holding funds and transacting on a separate keystore. 

Multi-wallet is also helpful for privacy oriented individuals that want to keep separate wallets for EVM chains (not sharing the same address for Supernova and Ethereum for example).

-------------------------

CryptoFish | 2024-09-20 11:13:35 UTC | #12





[quote="john.maxwell, post:1, topic:1940"]
1. Unify the desktop and mobile repos

* This will involve making the desktop code base modular and integrating BTC and EVM support in the desktop app
* Uplift the security of the desktop wallet (starting with secure storage and local authentication)
* Use clean Material UI elements (like the ones used in the mobile app)
* Make the code more maintainable (the design will, largely, be unmodified)
* Bug fixing and unit testing
* Improved documentation
[/quote]

What's the reasoning for wanting to unify the Desktop and Mobile repos? What benefit will it bring to the users?

As pointed out by others, the current UI uses a [deprecated widget](https://github.com/zenon-network/syrius/issues/127) which needs to be replaced in order to use the latest Flutter version. This replacement could impact the way the current layout functions. It also offers a good oppertunity to rethink the current design.

While I agree mostly with your suggested points from a developer perspective. Adding unit testing, documentation, more maintabable code and clean material UI elements. From an user perspective the community is paying 3-4 AZ projects for BTC and EVM support. I don't think users care much about whether the code base is modular or not.

I would rather see a collaboration take place on redesigning the layout and make parts of the code more manageable in the proces rather treating the above mentioned improvements as a primary goal.

Otherwise this proposal is just you saying I'm going to solve all your technical debt for a shitload of Zenon. Trust me it's going to be geat.

Don't get me wrong, I think it's great that you want to work fulltime on this project. I just don't think it will help the community get involved and be part of the development proces.

How will your proposed improvements help us improve collaboration and involve more developers in the development process? It's only a matter of time before technical debt piles up again, because there's no one involved or incentivized for helping out.

[quote="john.maxwell, post:1, topic:1940"]
2. Feature mirroring and multi-wallet support

* Porting features from the desktop app to the mobile app and the other way around (integrate the P2P swaps in the mobile app, desktop WebView). Those tasks will depend largely on what Flutter packages are available for both desktop and mobile.
* Add multi-wallet support

Budget asked: 2-3 AZ projects
[/quote]

I think you're asking quite a lot here without further defining the details. 

Adding support for multiple wallets shouldn't be too difficult. It mainly requires an addition to the UI to select between the different wallets and to be able to unload/reload the hive state.

I would like to see a high level overview of the features you think might be ported between both Desktop and Mobile version.

[quote="john.maxwell, post:1, topic:1940"]
After I finish the work, it will be much easier for new devs to develop and integrate new features for both the desktop and mobile apps (including adding support for more blockchain networks). I will also be available for new projects and open to collaborate with other community members. This includes providing guidance and onboarding of new Flutter developers that want to learn and create new features for the Syrius wallet.
[/quote]

Will you be available and open to collaborate before the work?

-------------------------

TheDev1776 | 2024-09-20 15:20:23 UTC | #13

@CryptoFish brings up a lot of great points.

@john.maxwell maybe a compromise between your preferred work style and the community's preference for collaboration you could break up the proposal into more segments?

So instead of two large initiatives, it's more like 4-5 with a corresponding AZ ask for each initiative sequenced by which ones you would tackle first.

-------------------------

sultanofstaking | 2024-09-21 02:04:02 UTC | #14

This proposal got me thinking about the vested pillar discussions. To date we have mostly been discussing vested pillars with regards to KOLs. I would agree this is a great initiative and working on it full time is a massive benefit. I also agree with others that you are asking for a shit ton of ZNN (my words). If we had vested pillar + redirected some of pillar rewards to AZ to perpetually fund it I think larger ask for larger pieces of work like this would be easier to digest... just a thought. At a minimum would be interested in hearing your response to fish + hoping you continue the convo here

-------------------------

0x3639 | 2024-09-21 16:38:10 UTC | #15

Just want to give everyone a heads up that in order to get my support on this AZ we need to collaborate with the other the developers in the community. @CryptoFish and others have been trying to scope syrius improvements and get other developers involved. He has an active SIG to do this.  CF has been here for years busting his ass consistently delivering high quality work. He has earned our trust.  

I strongly encourage @john.maxwell to join the SIG and start working on the scope with other developers and with support from the community.  Please!

-------------------------

john.maxwell | 2024-09-21 21:46:22 UTC | #16

Unifying the two repos will mean that we will have less code to maintain and it will be easier to develop features for desktop and mobile. Giving the fact that now we have two repositories, EVM and BTC support is only available for mobile. Further more, if I want to create multi-wallet support, without a common repo, then I will have to develop for mobile, and then for desktop.

The end users will profit by having a wider selection of features available and block chains. I do understand that end users don't care about code bases, and maybe I have put to much focus on the code aspects, and didn't quite explain what the users gain.

In just a few works: the desktop users will have EVM, BTC, local authentication, secure storage, WebView and much more smaller features. For example, I want to use Dart isolates so that the UI won't freeze anymore when you enter your password to access the application. I also want to fix the problem with preserving state across tabs: now you enter an amount in the Transfer Tab, navigate quickly to the Settings Tab to copy an address, and the amount in the Transfer tab is gone.

Here is in more details what I want to do on the development side: 

* refactor the code according to the bloc architecture - https://bloclibrary.dev/architecture/ - and essential step in creating a modular code base with business logic components that can also be consumed by the mobile app
* replace Hive library with drift, as Hive was replaced by Isar, but Isar itself had it's last update 17 months ago
* audit the current packages that we use: those that are not constantly updated should be replaced by other ones, or check if they can be replaced by features from the Flutter SDK; if not, build the functionality that the library offers myself, if it makes sense in terms of time and effort; this is an important task because, as other developers have noticed, an outdated library can block you from upgrading the Flutter version that the project uses
* create flavors for apps (prod, test, dev) so that when testing the app, you can skip, for example, the unlocking of your wallet
* use the new Dart language features created in the last 3 years
* establish Dart analyzer rules that developers should follow
* use isolates for the UI blocking operations
* write unit tests and documentation

So I don't think that I am just solving technical debt. I bring a change and with it improvements. 

You say that there are no developers to continue working on the project. In the mean time, I offer to work full time on bringing features for the desktop app and make the entry of new developers easier, and somehow, my ideas won't help the community. Although I have done some work for the benefit of it already.

I think a developer chooses his projects largely on the present quality of the  repo. Why would a developer get involved into projects with technical debt? And will a new developer get involved without a proper documentation? Without unit tests to sustain his development?

I dare ask you myself: how is redesigning the layout help bring more developers to the project? What actual value does it brings to the present users? Or how will it bring more users? 

You have to understand that I also need to be incentivized to work on this project. Development cost money, you can't only pay for the part of development that the users sees and interacts with. That's not how it works. Developers don't spent all of their time coding features for users. They write documentation, tests, fix technical debt because one outdated library can block you from upgrading to a new Flutter version: and that version might bring new UI render engine, for a smoother experience, or new widgets, or a faster Dart compiler.

Regarding the asked budged: if I am not mistaken, the EVM support plus other features for the mobile app got 2 AZ projects. I propose EVM and BTC support, local authentication, secure storage, WebView , at least, for the desktop app, plus code base improvements, and 3-4 AZ projects is a lot.

You have to understand that if I deliver a product that you are satisfied with, then I should also be satisfied with what I get back. Ultimately I am willing to deliver the product, the community can analyze it and be paid what you think it's worth it.

Regarding the second project, I will bring further details in another post. But as a developer, you should know that very often something that seems easy, takes a lot of time and effort. We don't have the 90/90 rule for nothing in programming (https://en.wikipedia.org/wiki/Ninety%E2%80%93ninety_rule).  That's the exact reason why I asked for 3 or 4 AZ projects: some things might take more time and effort than anticipated.

I am open for collaborations, but ask yourself this: if you have a modular code base, like in the bloc library fashion, don't you think it would be easier for some developers to work on the UI and others on the business logic? 

I hope that, at least, for the first project, it's more clear for everybody the scope of the work that I want to do.

-------------------------

john.maxwell | 2024-09-21 22:06:51 UTC | #17

I can split the proposal in other smaller projects, as I already has a technical sketch that I want to follow. I will discuss more on the SIG chat with the others developers.

@0x3639 I will send you my ID for SIG shortly

-------------------------

CryptoFish | 2024-09-22 10:43:28 UTC | #18

Thank you for your detailed explanation. You seem to have a lot of knowledge about Flutter/Dart and how to bring this project to the latest standards. In that respect I am actually very enthusiastic about your proposal. I also think that your proposed improvements will improve the conditions for new developers, but I think more is needed to get new developers to actually working on the project and reward them. The AZ mechanism is not ideal for paying small tasks that are taken up by several developers. Especially testing and writing documentation are often difficult to measure. The SIG groups are an attempt to improve the conditions for collaboration. Not all developers know what is needed to bring the project to a new level and/or do not have the time available to work on it. You seem to have the time and knowledge to take on the role of chair for the Syrius SIG group.

More explanation about the concept of the SIG groups can be found here, https://zenon.wiki/index.php/HC1:_SDLC_SIG.

Whether the mechanism of the SIG groups is something you only want to work with after you have laid a foundation or whether it can be applied immediately is up to you to decide. We can best discuss that within the group. At the very least, you take us along on your journey and the process is recorded for future reference.

-------------------------

cryptocheshire | 2024-09-23 03:31:49 UTC | #19

I support this initiative

-------------------------

0x3639 | 2024-09-23 12:23:08 UTC | #20

For anyone looking to track the progress of the syrius improvements please follow this matrix room: https://matrix.to/#/#sig-syrius:hc1.chat

Sounds like John is going to get going today or tomorrow on the upgrading Flutter and rearchitecting the app.  That will be a solitary task but he has agree to collaborate with other developers where it make sense.

-------------------------

coinselor | 2024-09-24 00:24:42 UTC | #21

John's explanation makes a lot of sense to me. Unifying the two Flutter codebases is almost mandatory to properly leverage the cross platform benefits of the framework. 

It's a lot of code. I know because I learned how to properly touch type using the syrius codebase :joy:. There's definitely some Bloc used already, but I'm guessing it can be expanded to cover more parts of the syrius logic.

I look forward to the SIG discussions, and being able to contribute, even if it's just a locale translation early on!

-------------------------

TrevorLeahy3 | 2024-09-25 18:06:26 UTC | #22

It would be very helpful to have things seperated into smaller projects where it makes sense to do that. 

Thank you for the contributions

-------------------------

john.maxwell | 2024-10-09 13:34:19 UTC | #23

Hello! 

Here is a technical sheet with what I want to do for the repo unification part:

* refactor the code according to the bloc architecture - https://bloclibrary.dev/architecture/ 
* use cleaner Material UI elements, like in the mobile app, to make the code more maintainable - the design will, largely, be unmodified
* integrate the mobile codebase with the desktop codebase
* enable EVM and BTC support for desktop app
* bring more safety features into the desktop app (secure storage and local authentication, for a start)
* replace Hive library with drift, as Hive was replaced by Isar, but Isar itself had it's last update 17 months ago
* replace walletconnect_flutter_v2 with reown_walletkit, because the former has been discontinued
* audit the current packages that we use: those that are not constantly updated should be replaced by other ones, or check if they can be replaced by features from the Flutter SDK
* create flavors for apps (prod, test, dev) so that when testing the app, you can skip, for example, the unlocking of your wallet
* use the new Dart language features created in the last 3 years
* establish Dart analyzer rules that the code pushed into the repo should follow
* use isolates for the UI blocking operations
* write unit tests 
* write comments for the code that will be a part of the documentation
* bug fixing

If somebody wants to help with any of the tasks, let's discuss on the SIG matrix chat. Please specify how many hours per week you can dedicate for your desired task.

From what I understood chatting with the others developers on the matrix chat, they are okay with me doing the whole project. Please correct me if I'm wrong. I am also okay with integrating others in my effort. I can provide documentation and guidance for the mentioned tasks.

I haven't posted here as often as I hoped, but I want to inform the community that work on the refactoring has already started. After this step is done, I will be able to work also on proper end user features, like EVM and BTC support. In the meantime, I was able to make some changes to the current codebase in order to support the latest Flutter version. Details here:  https://github.com/zenon-network/syrius/pull/128

-------------------------

0x3639 | 2024-10-09 22:26:42 UTC | #24

Thank you for this update.  My hope for this upgrade was for it to be open, transparent and in collaboration with other devs.  I hope others have time to help out, but if not, I don’t see any reason for you to slow down.  

Thanks for  joining matrix and keeping us up to date!!  Excited to see this come together.

-------------------------

CryptoFish | 2024-10-13 14:43:38 UTC | #25

[quote="john.maxwell, post:23, topic:1940"]
In the meantime, I was able to make some changes to the current codebase in order to support the latest Flutter version. Details here: [Upgrade dependencies by maznnwell · Pull Request #128 · zenon-network/syrius · GitHub ](https://github.com/zenon-network/syrius/pull/128)
[/quote]

Please request for review if you want these changes to be reviewed and merged.

-------------------------

john.maxwell | 2024-10-15 07:45:01 UTC | #26

OK. I will.

-------------------------

john.maxwell | 2024-12-22 19:48:43 UTC | #27

Hello! A small update: things are progressing with the refactor. Not as fast as I wanted, though. For a lot of reasons, but mainly because I don't want to cut corners and I will only submitted some work when I'm fully satisfied with it. 

I'm not only refactoring code, I'm also improving on the UI/UX aspect. The transfer tab took a while, and I consider that it was worth the whole back-and-forth that I went through to get this end result: 
![Screenshot 2024-12-22 203024|690x356](upload://rmpIQ1JKfzOcgZUy688bI4H4csQ.png)

You will be able to search through your addresses and tokens. The transactions list table is more colorful, you can easily copy the content that you want.  I fixed the QR reading issues that I personally had on my iPhone.

As a deadline, I would say the end of Q1 2025 is a more reasonable date to be able to deliver everything that I proposed. Plus all the other smaller features and fixes that I will do along the way.

-------------------------

0x3639 | 2024-12-24 02:20:37 UTC | #28

Thank you for that update and for all your work.  We appreciate the coordination in Matrix also!

-------------------------

