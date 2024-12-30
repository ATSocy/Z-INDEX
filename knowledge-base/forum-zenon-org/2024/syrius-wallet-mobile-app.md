Thread: syrius-wallet-mobile-app
DrBlaze_21 | 2023-02-11 22:49:02 UTC | #1

Hello, Zenon community,

Here's Blaze, I am a tech-savvy entrepreneur developing mobile applications on both Android & iOS using Flutter technology.

I've been reached by my buddy who's part of your community and has introduced Zenon to me & proposed to start building new products under the Accelerator-Z umbrella.

I've taken a look at the whitepaper, current tech & projects within the ecosystem and realized there's no functional mobile app for Syrius which I can help you with by building an end-to-end Syrius mobile wallet.

We've already spent some time working on the app's design & some future screens, but unfortunately I could not attach all files. However, here are the main features I want to start developing: 

* create & import wallet
* send & receive transactions
* generate plasma using pow and by fusing QSR
* settings: manage wallet, backup seed, backup mnemonic, manage nodes, OS-specific biometrics for unlocking wallet, auto-lock interval, change the passcode, change password, auto-erase interval
* staking
* delegation

Please share your initial feedback!
I am looking forward to applying to Accelerator-Z and starting to work among you :)

![X - 13|225x500](upload://qkndKkplPx9zS2xEZXQXvcYVVl7.png)

-------------------------

ImperiumBNC | 2022-06-06 20:10:48 UTC | #2

This is really a great news, the first look is amazing ! Can’t wait

-------------------------

dat_she_pepe | 2022-06-06 20:15:56 UTC | #3

As much as I hate the idea of people having their cryptos on a phone I understand the regular Joe wants this kind of app. The screen looks clean and it would definitely help. I'd support this.

-------------------------

DrD3 | 2022-06-06 20:24:08 UTC | #4

+1 the very notion of having my zennies or any crypto on my smartphone makes me really queasy. We do need a mobile wallet for mass adoption tho so you have my support.  But also daaayum those colors and dat template look zexy as fuck!

-------------------------

mr.ztark | 2022-06-06 20:31:02 UTC | #5

Welcome! Looks awesome. 

Fyi, there is another mobile wallet project called Cano. tg user: Oliver Martinez

No harm in having two projects / mobile wallets. Maybe they will have important differentiations.

Another idea might be that you could each gain a-z grants and work together.

Probably not what you’re looking for as feedback but just suggesting collaboration as a potential option.

Thank you for sharing your progress. Exciting times.

-------------------------

cryptocheshire | 2022-06-06 20:40:58 UTC | #6

Will the wallet be shipped with embedded nodes or will users rely on connecting to public nodes?

-------------------------

0x3639 | 2022-06-06 23:29:27 UTC | #7

Excited to see this development.  I would support this A Z project for sure.

-------------------------

romeo | 2022-06-06 23:34:23 UTC | #8

This is a really interesting point, you would imagine public nodes for the mobile wallet would be the default but it would be really cool to have a full Embedded node on a mobile device.

When would it sync? Periodically or just when launched? How much battery would it use? What about it you don't have plasma and need to do POW?

-------------------------

coinselor | 2022-06-07 00:46:08 UTC | #9

Welcome to our community. I'll make sure to buy a space drink to the alien who referred you to our cause. 

The initial ui looks clean. The plasma meter is a nice touch. Maybe black might be better contrast instead of white on top of the green bg - or flip horizontal the darker green side.

I am also interested on the possibility of running an embedded node on mobile devices. Share your findings when possible.

-------------------------

vilkris | 2022-06-07 05:42:57 UTC | #10

Welcome! Glad to have new devs/entrepreneurs joining.

Like already mentioned there's been an effort to develop a mobile wallet. I'm not sure if the developer has recently had time to continue development but it has a website and the source code is available on GitHub: https://canowallet.app/#/

As for the embedded node on mobile, I ran the node on a three year old flagship Android but the syncing was extremely slow, the phone was burning hot and it would have taken like two weeks to sync so I gave up. I recall Mr Kaine saying he was running a node without issue on a newer flagship Android. In any case I think the embedded node functionality on mobile is a somewhat complex topic in terms of how to make it user friendly, not drain the battery completely or hog all the resources and how to keep the node synced when the wallet is not open.

-------------------------

DrBlaze_21 | 2022-06-10 11:40:16 UTC | #11

I have collected all the questions and made a Q&A: 

Q:
Will the wallet be shipped with embedded nodes or will users rely on connecting to public nodes?

A: 
It’s should be possible to include a go mobile binary on Android, but it unlikely that will be accepted on AppStore. 

Q:
This is a really interesting point, you would imagine public nodes for the mobile wallet
would be the default but it would be really cool to have a full Embedded node on a mobile
device
When would it sync? Periodically or just when launched? How much battery would it use?
What about it you don't have plasma and need to do POW?

A:
Yes, there a lots of cases that need to be taken in consideration, that why the mobile syrius will likely need to connect to a remote node. 

PoW will be computed on the user’s terminal. There are 2 options we can use:
A. Native implementation called from a library through ffi (faster, but might not be accepted by playstore/appstore)
B. Dart implementation (slower, but more likely to be accepted)

Of course, it’s recommended that users fuse qsr for plasma, so they can experience instant transactions.

-------------------------

DrBlaze_21 | 2022-06-12 12:15:00 UTC | #12

Further research & development is needed to entirely comprehend how Syrius works.
We’ll create a project to fund the research and the design.

-------------------------

mehowbrainz | 2022-06-25 12:27:36 UTC | #13

Would it be possible to add a web connect feature where one can use the mobile wallet to connect their wallet to a supported website ie a DEX? Just like how you can use the WalletConnect/TrustWallet app to connect to THORSwap. 

Would be an awesome feature to port to the desktop app too ie how the desktop Ledger Live app is used to connect with MetaMask.

-------------------------

DrBlaze_21 | 2022-08-05 12:08:43 UTC | #14

Hello Zenon community,

I have successfully completed the first milestone for the mobile apps project to bring Syrius wallet on iOS and Android.

Milestone details:
	- UX/UI for the app
	- user flows for wallet related functionalities
	- interactive prototype
	- research for Syrius features (create/import wallet, Plasma PoW, fuse Plasma, staking, Sentinel, A-Z)
	- compilation of Syrius desktop in order to understand how it uses the shared libraries

Requested funds: 5000 ZNN and 50000 QSR

Design link: https://www.figma.com/file/BmmfUT2DOiLzweeMfcLCse/App?node-id=0%3A1

-------------------------

Zashounet | 2022-08-05 13:09:21 UTC | #16

Beautiful work. Congratz

-------------------------

coinselor | 2022-08-05 14:03:23 UTC | #17

Amazing work, now that's a mobile UI/UX that makes s y r i u s proud. 

Be right back, I'm gonna go draft a ZIP to increase the cap of Accelerator-Z rewards, or to add a bonus to the hyperspace rewards winner :joy:

-------------------------

cryptocheshire | 2022-08-05 14:25:43 UTC | #18

This looks very well designed. The mobile wallet looks like it has extensive functionalities, even more than the current desktop wallet. Obviously, that can be great but functional complexity comes at an increased risk of UX tradeoffs.

Are you planning to iteratively test and improve the wallet with community members to mitigate that risk?

Will this also be available for tablets?

Thanks a lot for this work!

-------------------------

mehowbrainz | 2022-08-05 21:43:22 UTC | #19

Great UX, you carried the styling from the desktop app.. well done!

How will cross-chain swaps work?

-------------------------

DrBlaze_21 | 2022-08-10 11:55:53 UTC | #20

Yes, the app will be released to the community in it’s early stages so we can work together to achieve the best results.

-------------------------

DrBlaze_21 | 2022-08-10 11:57:26 UTC | #21

The swapping features will take advantage of Web3 solutions to allow users to swap between native assets + most ERC20/BEP20 and wZNN/wQSR (assuming wQSR will be an option). It does that by leveraging well known AMM platforms such as Uniswap/Pancakeswap either directly or though routing solutions (eg. 1inch). 

For cross-chain swaps, the solution available at the moment of the integration will be integrated.

The purpose is to allow users to get ZNN/QSR in the quickest & easiest way.

-------------------------

ToKR | 2022-08-12 03:24:31 UTC | #22

Great work!   Looks amazing!  Already voted to fund but am wondering how many phases to completed project and will future updates require further future funding?

-------------------------

Dumeril | 2022-08-12 10:38:24 UTC | #23

I just now have looked at this and it seems that all we get for 5k/50k would be some nice looking mocks. Is that so? No coded prototype, no reusable research results?

-------------------------

ZNNAYIID | 2022-08-12 11:53:55 UTC | #24

Also it would be nice to know the total amount you gonna request to get to the final product.

-------------------------

0x3639 | 2022-09-12 21:54:02 UTC | #27

@DrBlaze_21 I am encouraging @thoglund to pick up your framework and complete the wallet.  If we don't hear back from you soon I do think someone will forward to complete your work.  If you have other plans, please let us know this week.

-------------------------

Zashounet | 2022-09-13 14:27:07 UTC | #28

I think we should have some patience and let Dr.Blaze finish what he started.
He said everything’s going to be ready for the end of the year.

-------------------------

DrBlaze_21 | 2022-09-15 09:50:41 UTC | #29

Sorry for the late reply, there's been a lot of stuff to learn and get done. Of course the wallet is still under heavy development. 

The project was never just about the design. The mocks and wireframes are just a starting point and were released in order to support the further development of the mobile wallet and gather valuable feedback from the community. 

I am guessing there probably aren't many technical people in here, since there was an expectation that an entire mobile app (actually both iOS and Android versions) can be developed for 5000 znn + 50000 qsr. This kind of apps cost companies millions, Accelerator-Z alone wouldn't be able to cover it. First look at this: https://www.glassdoor.com/Salaries/junior-mobile-developer-salary-SRCH_KO0,23.htm

And also check out Solana's Phantom App that recently got some investments in the tens of millions to support its operations: https://www.fintechfutures.com/2022/02/crypto-wallet-phantom-launches-app-following-109m-series-b-raise

An exact cost hasn't been calculated for this project, but it will probably be over 250k excluding maintenance. Anyhow, a release should be possible in late October/early November.

-------------------------

0x3639 | 2022-09-15 12:37:11 UTC | #30

Thank you for that update.  Some community members were interested in the helping.  If you are looking for more team members please contact @thoglund

-------------------------

ToKR | 2022-09-15 19:25:19 UTC | #31

I don't think there's a lack of understanding regarding the scope of your project here.  As you know I personally was proposing a similar project which I tabled in favor of yours.  The questions relate to your expectations of reimbursement through AZ for your work in its completion and maintenance.  

The project you are doing is massive and I believe will prove to be extremely beneficial to the overall project in the future but surely you're not expecting to apply for a dozen or more phases at 5k/50k?

I think it's reasonable to reach a mutual  understanding of what the future and ongoing AZ rewards might look like for any given project.  One might envision a situation where the community and any project could reach a stalemate where a project isn't realized due to a difference in expectations.  

None of us want someone putting in valuable time and resources only to be disappointed when the expected and realized rewards don't reconcile.

-------------------------

0x3639 | 2023-01-15 13:21:09 UTC | #32

@DrBlaze_21 We have some new community developers interesting in getting involved w/ the Mobile Wallet development.  Are you still working on the project?  Would you be willing let other community members join in the effort?

-------------------------

mehowbrainz | 2023-02-10 23:03:56 UTC | #33

[quote="DrBlaze_21, post:14, topic:659"]
- interactive prototype
[/quote]

I began to work on the interactive prototype: https://www.figma.com/proto/oUykfWEFY0TIL8PApSiuXm/SYRIUS-Mobile-App?page-id=0%3A1&node-id=2%3A1339&viewport=6865%2C11090%2C1&scaling=min-zoom&starting-point-node-id=2%3A1339

There are some design alignment inconsistencies between some views, but overall the design framework has been well thought out. Will notify you all when the prototype is fully completed. You can begin to click through it to experience the design.

[quote="DrBlaze_21, post:29, topic:659"]
An exact cost hasn’t been calculated for this project, but it will probably be over 250k excluding maintenance. Anyhow, a release should be possible in late October/early November.
[/quote]

I understand that the intention was to of course provide design files + prototype for the 5K ZNN / 50K QSR, which was approved on-chain.

I recently hired a developer knowledgeable in Flutter, I think he will be a good fit to evaluate SYRIUS desktop and his ability to develop this mobile app at a much lower cost than $250K. He's currently doing some work on the zenon.org framework, hopefully he can be done next week or the following. I will be introducing him to this project. So far from what I see that he's doing for us, he's capable, organized and works at a relatively fast and focused pace. Impressive young developer. I'm asking him to speed through our work so he can be proposed this mobile app project as an A-Z submission.

-------------------------

0x3639 | 2023-02-11 13:04:23 UTC | #34

[quote="DrBlaze_21, post:29, topic:659"]
The project was never just about the design. The mocks and wireframes are just a starting point and were released in order to support the further development of the mobile wallet and gather valuable feedback from the community.
[/quote]

@DrBlaze_21 it would be very helpful if you could explain your roadmap to the community.  We noticed you recently made some very nice design improvements to the Figma files.  They look great.  Last time we got an update you stated the project is more than just design and we could expect an update by year end.  

Moving forward we are trying to do a better job of communicating with each other through [monthly updates](https://www.zenon.info/zenon-network-january-2023-update/). 

Can you please give us an update on your work?  Do you need any resources from the Community?

-------------------------

mehowbrainz | 2023-02-11 18:02:48 UTC | #35

I also think the design is missing considerations for diff resolutions/devices. From a height perspective many of the views will not fit on my iPhone XR (I know old). Unless you expect that the design requires a scroll (and of course some pages require that), but others where there's a button at the bottom: it's unclear what the design/experience expectation was. A few success messages are missing in the workflow/design file, but those can be assumed based on other styles.

I don't expect him to reply, but if he does then I hope he answers questions about dev, though I'll be assuming that the development is not included in his fees or future milestones. This could've had been started months ago if the milestone was ever planned.

-------------------------

mehowbrainz | 2023-02-11 23:27:28 UTC | #36

I dug deeper, he played us.

If we actually look at the on-chain description submitted: https://zenonhub.io/accelerator-z/project/9edc26f719405e6b28e76f01ae3349df068d747fb8bbb0027db1f2ad7b344e65

It says:

> Development of mobile applications for both Android & iOS using Flutter technology.

But then he requested the full funds for the "Research, Design, Prototyping" Phase. 

The way I see it: we were led on to believe that the original entire proposal was for 5K ZNN + 50K QSR for "Development of mobile applications for both Android & iOS using Flutter technology." ... but then that was changed when he submitted the first phase and only delivered the drawings for the full submission.

In August he created the submission and it was voted yes. In September he then [changes his POV](https://forum2.zenon.org/t/syrius-wallet-mobile-app/659/29?u=mehowbrainz) and says it'll cost $250K.

At no point in his early first proposal did he mention that he would need more than 5K ZNN + 50K QSR to complete everything. His submission on-chain says iOS and Android.

He got paid August 17, 2022 when wZNN was $2.10-2.20. Estimated value of the design: ~$21,500. What a waste. I could draw that same interface in 1 month's time or less for free if I wanted.

Who's fault is this? The Pillars and community not paying close attention to deliverables and the change in the project's scope. No one noticed what was going on.

But hey don't dare asking AZ to..

![7au416|500x500](upload://AaSiQGezrURJHqSdgNmBojW8FIW.jpeg)

-------------------------

sol | 2023-02-11 23:40:57 UTC | #37

Massive L. We need better oversight on deliverables before pillars vote Yes on phase payouts.

-------------------------

mehowbrainz | 2023-02-12 00:29:58 UTC | #38

I have an idea that'll pivot the way we think about AZ, engage pillars and re-imagine what we were initially led to believe for Zenon. Will be posting a new topic, starting to type the vision.

-------------------------

0x3639 | 2023-02-12 03:44:24 UTC | #39

@vilkris did point out that his last design revision was in January 2023, so less than 2 weeks ago.  He was paid in full but continues to improve the design.  If he was not acting in good faith I find it hard to believe he would continue to update the design after submitting it and getting paid in full.  

He also stated in his last post this project was always about more than the design.   So, putting it all together:

1) Paid in full months ago and continues to work on the design
2) Previously said his project is about more then just the design and said it could cost a lot to complete
3) Has not coordinated with the broader community 

My guess is he is still working on the project and I hope he can coordinate with the community so we don't waste time building a back end that he is working on.

-------------------------

sol | 2023-02-12 04:55:42 UTC | #40

[quote="0x3639, post:39, topic:659"]
My guess is he is still working on the project and I hope he can coordinate with the community so we don’t waste time building a back end that he is working on.
[/quote]

I'm tired of guessing this, hoping that.

For primary network objectives (such as the main mobile wallet), contributors should have enough respect for the community to announce their intentions* in a timely manner instead of working in isolation and throwing their work over the fence when they think they're done. 

When they do announce their intentions, we should consider these to be best effort -- unforeseen circumstances happen. 
But at least keep the community informed so we can make other arrangements.

For DrBlaze -- if you have an employer, is this how you communicate with them? Why should your relationship with AcceleratorZ be any different?

I posted a note on the figma page 10 days ago. If we don't hear a response in the next three weeks, we really should consider moving on.

\* This applies to sentinels, smart contracts, NFT Standard, etc, as well.

-------------------------

mehowbrainz | 2023-02-12 13:55:21 UTC | #41

The point isn't if he's still continuing to improve his design, it's:

1) The fact that his initial on-chain submission sub-title promised an iOS/Android app in Flutter. Many pillars must've from that point on thought that they were getting a full app for the cost.
2) He then says it'll cost $250K to build the app, but it can be done for October/November.

If he does deliver the app, are we really gonna pay him $250K worth of ZNN and QSR? ZenonOrg from now on is done with these big bang expensive proposals which promise one thing, and end up being something completely different. Project-based submissions in my opinion don't work, the network is getting milked for those who understand: must accumulate as much ZNN as possible to get some bag. Imagine we instead just hired a network UI designer to work full-time, at $21,500 and an hourly rate of let's say $20 per hour (depending which country we source the talent from), we could've had bought 1,075 hours of work. Do you really think this mobile app design cost 1,075 hours of work? That's 26 weeks of drawing 40 hours a week. Insane. This design at most took him 1-2-3 months part time, and no where near 1,075 hours. At first when you see 5K ZNN you're like "that's worth like $5k okay fine" (you don't really do any proper math and assume 1 ZNN = $1 for some stupid reason), but when you add it all up and it ends up being $21K, it's a wake up call that we're not paying close attention.

We'll be proposing an alternative method shortly which'll include the network acting like a regular company which hires and manages key professionals that produces work on a full-time basis.

-------------------------

0x3639 | 2023-02-12 15:28:19 UTC | #42

I can definitely understand everyones frustration.  And if this was a corporate setting these circumstances would not be tolerated.

In the future I think we should set the expectations for communication before approving an AZ.  We don't need a weekly update, but there should be some level of coordination with all the other developers here.  People are busting there ass and we should be able to coordinate our efforts at a high level.  

I'm going to continue to reach out to @DrBlaze_21 in hopes that he gives us an update.

-------------------------

coinselor | 2023-02-14 00:51:03 UTC | #43

From my vague understanding of @DrBlaze_21 reply


- He acknowledges the scope of his work should not/can't be covered by AZ funds alone.

[quote="DrBlaze_21, post:29, topic:659"]
Accelerator-Z alone wouldn’t be able to cover it
[/quote]

- He didn't even calculate an exact cost for the project. Signals intention to "overdeliver" at current market prices. Too vague for us, we need the terms to be more clear.

[quote="DrBlaze_21, post:29, topic:659"]
An exact cost hasn’t been calculated for this project
[/quote]

- Misses release date, which is not a big deal given the scope of the project. But communication with other community devs (especially given we had more than a couple interested in helping in this endeavor) must have a periodical and consistent cadence. Pillars should start to enforce this for future AZ projects.

-------------------------

mehowbrainz | 2023-02-14 01:06:46 UTC | #44

He submitted the proposal on-chain with a subtitle for 5K ZNN + 50K QSR.

> Development of mobile applications for both Android & iOS using Flutter technology.

And then later changed his mind on the price. Maybe we would've thought twice on the original proposal approval and its price if we would've had known it was only going to be for UI design, and that the eventual estimated development price would be at least $250K as he states. Things were convoluted. I don't see how we could defend him given his total lack of communication and clarity.

-------------------------

mehowbrainz | 2023-02-14 15:01:45 UTC | #45

Another possibility: perhaps there was speculation that the treasury would be worth more by a certain point, and the $250K+ would've been minimal as an expense?

I propose that we put an expiration date. If @DrBlaze_21 doesn't reply/clarify by a certain point, we can assume he has no interest to communicate further and the community can move with its own plans.

[poll type=multiple results=always min=1 max=1 chartType=bar]
* Let's put an expiration date
* Let's not
[/poll]

-------------------------

cryptocheshire | 2023-02-14 16:54:54 UTC | #46

imo there's no need to wait for anyone who doesn't bother communicating after leaving the community in ambiguity for so long. Best to just rip off the bandaid, accept that we've paid >20k in znn & qsr for mockups, learn from it, and move on.

-------------------------

coinselor | 2023-02-14 22:12:04 UTC | #47

At current market prices, we are paying him like 7k. I'm not sure whose band-aid needs to be ripped off. But given the amount and quality of the work, I think we are getting a good deal. If not, ask an actual designer how much that's worth.

We should definitely learn from every single AZ project submission, this one is no different.

-------------------------

0x3639 | 2023-02-14 22:34:31 UTC | #48

In the list of priorities, I believe the delivery of the mobile wallet is less important than:

- dynamic plasma
- sentinels
- wasm
- unikernels

Once we have these critical components of the network functioning I believe the price of ZNN will be higher and it will be "easier" and less costly to complete the mobile wallet.  

My recommendation is we discuss a community roadmap and establish priorities before taking any action.

-------------------------

DrBlaze_21 | 2023-02-15 09:21:30 UTC | #49

[quote="0x3639, post:34, topic:659"]
Can you please give us an update on your work?
[/quote]

I finished the Dart SDK porting to Android and iOS and I've started implementing the Figma screens.

[quote="mehowbrainz, post:36, topic:659"]
I dug deeper, he played us.
[/quote]

I won't engage in a polemic with you, sorry.

[quote="0x3639, post:39, topic:659"]
My guess is he is still working on the project
[/quote]

Yes, I'm working and preparing an APK release for the community to play with.

[quote="0x3639, post:34, topic:659"]
explain your roadmap to the community.
[/quote]

1. I've redesigned the UI/UX of the mobile app after I've completed an in-depth UX research.
2. Modify the Dart SDK for mobile app compatibility (Android and iOS): currently the Dart SDK only supports Windows, Linux and macOS.
3. Creating the screens according to Figma user flows.
4. Implement basic functionality: Send, Receive and Plasma.
5. Implement extended functionality: Rewards, Sentinel.
6. Implement security features: biometric unlock, root detection, etc.
7. Polishing the app, bug fixing, testing and preparing it for release.

-------------------------

cryptocheshire | 2023-02-15 11:15:15 UTC | #50

I stand corrected

-------------------------

ZNNAYIID | 2023-02-15 11:16:49 UTC | #51

any ETA for beta release?

-------------------------

mehowbrainz | 2023-02-15 13:05:13 UTC | #52

[quote="DrBlaze_21, post:49, topic:659"]
I won’t engage in a polemic with you, sorry.
[/quote]

See, all it took it some noise for you to come around and clarify things. It ain't heroic the way you've gone missing for 5 months so feel free to engage if you have anything to say.

-------------------------

mehowbrainz | 2023-02-15 13:03:36 UTC | #53

Now the question is: at what price @DrBlaze_21. $250K? Less? More?

-------------------------

mr.ztark | 2023-02-15 13:13:21 UTC | #54

I stand erected.

-------------------------

sol | 2023-02-15 14:31:28 UTC | #55

Welcome back and thanks for the update.
I'm impressed that you have the skills to create a beautiful mobile UI and to update the Dart SDK.

What is your expectation of payment for your work?

Please keep us informed about your plans.

-------------------------

Sir_D | 2023-04-07 09:21:33 UTC | #56

the syrius wallet mobile will be ready when you know approximately?

-------------------------

0x3639 | 2023-04-07 09:23:14 UTC | #57

We are not sure.  Maybe this quarter we will be able to test it?  But that is a guess with NO feedback from the developer.  We have been tracking the UI development which will get shared in the March dev update.  Make sure to follow @learn_zenon on twitter.

-------------------------

DrBlaze_21 | 2023-04-16 09:09:07 UTC | #58

Making good progress: public beta testing will start this month.

-------------------------

0x3639 | 2023-04-16 13:36:20 UTC | #59

great news.  thanks for the update.

-------------------------

0x3639 | 2023-04-16 22:09:41 UTC | #60

@DrBlaze_21 Will the wallet have an embedded node?  Have you addressed the IBD (Initial Block Download) issue?  

![node|416x499](upload://mo3fQl724vXkpBZlKlPAqNus7nq.jpeg)

-------------------------

ZNNAYIID | 2023-04-30 18:43:16 UTC | #61

And…

-------------------------

0x3639 | 2023-06-15 20:03:51 UTC | #62

a16z developed this light node that can do an IBD in 2 seconds.  Maybe something interesting here.  

https://github.com/a16z/helios

-------------------------

DrBlaze_21 | 2023-06-30 18:58:40 UTC | #63

Hello,

I'm pleased to announce the first alpha release of the mobile app. For the moment only the Android version is available for testing.

I need permissions to upload the `APK` file.

*Do not* use it on `mainnet` or store any real funds until a stable release is ready.

Please use the `testnet` instead.

[quote="ZNNAYIID, post:61, topic:659, full:true"]
And…
[/quote]

No more "deadlines" from now on.

[quote="0x3639, post:62, topic:659"]
a16z developed this light node that can do an IBD in 2 seconds. Maybe something interesting here.

https://github.com/a16z/helios
[/quote]

Do we have a light node for NoM?

-------------------------

mehowbrainz | 2023-06-30 19:02:20 UTC | #64

[quote="DrBlaze_21, post:63, topic:659"]
I need permissions to upload the `APK` file.
[/quote]

Added apk to the permitted extensions, try now please.

-------------------------

sol | 2023-06-30 20:34:13 UTC | #65

Welcome back

[quote="DrBlaze_21, post:63, topic:659"]
I need permissions to upload the `APK` file.
[/quote]

Can you please upload it to Github, as well?
We can potentially build it with Github Actions.

[quote="DrBlaze_21, post:63, topic:659"]
Do we have a light node for NoM?
[/quote]

Not yet.

-------------------------

DrBlaze_21 | 2023-06-30 19:09:26 UTC | #66

"Sorry, that file is too big (maximum size is 4 MB)."

I need ~100Mb. 

It contains the [TrustWallet Core](https://github.com/trustwallet/wallet-core) library that has over 80Mb.

-------------------------

sol | 2023-06-30 19:11:21 UTC | #67

Will you be sharing any source code at this time?

-------------------------

mehowbrainz | 2023-06-30 19:22:24 UTC | #68

[quote="DrBlaze_21, post:66, topic:659"]
I need ~100Mb.
[/quote]

Updated temporarily to 125mb, but there's potentially other settings required in the infra side to support this as he wasn't able to upload the file, I quote:

> The maximum attachment files upload size in kB. This must be configured in nginx (client_max_body_size) / apache or proxy as well.

I reverted the changes. @DrBlaze_21 agreed to upload the file in some file sharing service.

-------------------------

DrBlaze_21 | 2023-06-30 19:23:06 UTC | #69

[quote="sol, post:67, topic:659, full:true"]
Will you be sharing any source code at this time?
[/quote]

Not at this time. The apps are still in heavy development.

Download [Syrius Mobile alpha version APK](https://t.ly/XmQc)

- *Do not* use it on `mainnet` or store any real funds until a stable release is ready
- Please use the `testnet` instead

-------------------------

DrBlaze_21 | 2023-06-30 19:36:29 UTC | #70

[quote="0x3639, post:60, topic:659"]
@DrBlaze_21 Will the wallet have an embedded node?
[/quote]

I can integrate the embedded node, but it needs to be compiled for `Android` and `iOS`. I saw that `libznn` is built only for desktops.

[quote="0x3639, post:60, topic:659"]
Have you addressed the IBD (Initial Block Download) issue?
[/quote]

This is something `go-zenon` developers should address.

I've suggested @mehowbrainz to setup a dedicated chat for mobile apps feedback.

-------------------------

mehowbrainz | 2023-06-30 19:40:15 UTC | #71

[quote="DrBlaze_21, post:70, topic:659"]
I’ve suggested @mehowbrainz to setup a dedicated chat for mobile apps feedback.
[/quote]

Here is the chat: https://forum2.zenon.org/chat/c/-/46/2084

-------------------------

aliencoder | 2023-06-30 21:24:25 UTC | #72

[quote="DrBlaze_21, post:70, topic:659"]
but it needs to be compiled for `Android` and `iOS`
[/quote]

At the moment the `go-zenon` depends on `C` code:

```
Building znnd requires both a Go (version 1.16 or later) and a C compiler.
```

That means that we need to cross-compile it for every CPU architecture. I used `xgo` to do that and [unfortunately](https://github.com/crazy-max/ghaction-xgo/issues/77) it [doesn't support](https://github.com/crazy-max/xgo/issues/19) mobile targets.

If we can get rid of the `C` code dependencies and have a clean `Go` only codebase, we can easily target `Android` and `iOS`.

-------------------------

0x3639 | 2023-07-03 09:14:06 UTC | #73

Looks like the wallet link expired.  I uploaded it here.

https://hypercore.nyc3.digitaloceanspaces.com/mobile-wallet/syrius-debug-alpha.apk

@DrBlaze_21 can you please share the checksum of the original file so others can verify the authenticity of this file?  Maybe others community members can do it too who downloaded the file.  

Windows
`certutil -hashfile syrius-debug-alpha.apk MD5`

Mac
`md5 syrius-debug-alpha.apk`

-------------------------

Asgardians-Pillar | 2023-07-03 16:13:27 UTC | #74

![Screenshot_20230703_175806|225x500](upload://ohDy77AFbs7VBlNnwVMjYAgWXOB.jpeg)

Send 200znn and 500 qsr but the 500 qsr balance displays wrongly.

Also can't change the name of adress 1.


And yeah I accidentally did it on main net, saw your post @DrBlaze_21 about asking not to after 😂

-------------------------

Zashounet | 2023-07-03 17:17:29 UTC | #75

Beautiful wallet and thank you for the work. 

There’s a bug when you have the same word twice in your seed. 
The word is "movie" in this case. 
Once I select it, both turn grey and I’m left with 11 words and can’t confirm my seed backup. 


![image|264x500](upload://d4VJPHZLQxqFEHtjrPokW33KzxQ.jpeg)
![image|271x500](upload://e9nHGEJSXmJXgjQHGaeN9j6x5HQ.jpeg)

-------------------------

DrBlaze_21 | 2023-07-03 20:45:16 UTC | #76

[quote="aliencoder, post:72, topic:659"]
If we can get rid of the `C` code dependencies and have a clean `Go` only codebase, we can easily target `Android` and `iOS`.
[/quote]

It would be great.

[quote="0x3639, post:73, topic:659"]
@DrBlaze_21 can you please share the checksum of the original file so others can verify the authenticity of this file? Maybe others community members can do it too who downloaded the file.
[/quote]

The app is signed with a [debug keystore](https://developer.android.com/studio/publish/app-signing#debug-mode). `SHA-256` checksum: 

```
1c646b209cf913ee992edd71218408007843d827765bafdd818a5ecf62724264
```

[quote="Asgardians-Pillar, post:74, topic:659"]
Send 200znn and 500 qsr but the 500 qsr balance displays wrongly.
[/quote]

What node do you use?

[quote="Asgardians-Pillar, post:74, topic:659"]
Also can’t change the name of adress 1.
[/quote]

WIP.

[quote="Zashounet, post:75, topic:659"]
There’s a bug when you have the same word twice in your seed.
[/quote]

Hmm.

-------------------------

DrBlaze_21 | 2023-07-03 21:14:02 UTC | #77

I'm interested in UX feedback. How can we improve the UX of the mobile apps?

-------------------------

Asgardians-Pillar | 2023-07-04 05:50:29 UTC | #78

[quote="DrBlaze_21, post:76, topic:659"]
?
[/quote]

Used my own pillar adres as a node.

-------------------------

0x3639 | 2023-07-06 23:10:07 UTC | #79

@DrBlaze_21 does this require a go-zenon v0.0.6 node that supports big int?  I'm trying to get some testnet ZNN from https://faucet.hypercore.one/ but I cannot seem to get any.  

using my testnet node on the hypercore testnet - wss://testnet.deeznnutz.com:3598

sending to this address: z1qzu0c96cdq5q5z7amrlha64vea3j4funkfjf45
https://testnet.zenon.info/address/z1qzu0c96cdq5q5z7amrlha64vea3j4funkfjf45

I can see lots of unreceived TXs.  this is the wallet address for the mobile wallet I'm testing.  I have the chain ID set to 321.

I see lots of spinning circle here

![image|633x363](upload://d7KdwyDjpZZngieunzhSZMRdIk3.png)

-------------------------

DrBlaze_21 | 2023-07-09 19:50:20 UTC | #80

[quote="0x3639, post:79, topic:659"]
@DrBlaze_21 does this require a go-zenon v0.0.6 node that supports big int? I’m trying to get some testnet ZNN from https://faucet.hypercore.one/ but I cannot seem to get any.
[/quote]

Yes, the mobile wallet only supports `big-int` nodes.

-------------------------

DrBlaze_21 | 2023-07-09 20:09:37 UTC | #81

Syrius Mobile Wallet `v0.0.2` is now live

1. If you have a previous version of the Syrius wallet installed on your mobile device, please uninstall it (the versioning changed).
2. Install [Syrius v0.0.2](https://tinyurl.com/vppawyjv)

**CHANGELOG**:

- :alien: Added Staking feature
- :alien: Added Delegation feature
- :cockroach: Fixed mnemonic bug
- :cockroach: Fixed `QSR` display bug

-------------------------

romeo | 2023-07-10 00:30:25 UTC | #83

Can someone send me some test funds?
z1qp5ksd8jgjjt99zqn7vx7lg2daygn2avdmm98d

Notes:
connected to wss://syrius-testnet.zenon.community:443
Chain ID 3

- no need to set mnemonic off the bat, prompts you to backup

- assets tab just shows the green loading circle thing endlessly. History tab successfully shows "nothing to show"

- was able to create new addresses
- was not able to rename wallet addresses

- love the AZ tab, none of the buttons are live yet it seems



UX wise - no major complaints, the logic behind actions and clicks seems very sound. Couple of small things though:

- Font size of warnings such as the text when setting a PIN, seems a bit small "The PIN will be used to encrypt your seed"
- I haven't been able to find a direct way to bring up the token list
- The 'long-click' on fields, is that meant to trigger a Copy action? Or it the animation just for visual effect?

Awesome work - many thanks for your efforts

-------------------------

0x3639 | 2023-07-10 02:05:27 UTC | #84

I've reposted v0.0.2 on DigitalOcean in case we run out of downloads

https://hypercore.nyc3.digitaloceanspaces.com/mobile-wallet/syrius-debug-alpha-v0.0.2.apk

-------------------------

coinselor | 2023-07-10 16:27:11 UTC | #85

Suggestions:
- Increase contrast of the "..." button with the background. At least to the lighter shade of the Fuse,Send, Receive buttons.
![image|487x234](upload://w1B2JrwaMXvyxoEPDSLRaNMqY7G.png)

- After copying the wallet address to the clipboard, I think the initial bottom modal popup notification is enough. The top right Bell indicator should not light up with the same (1) notification. I think showing the notification is fine when you open the bell, but should be shown as already greyed out given the user has already seen it at the bottom once.

Possible bugs:
- Endless loading indicator in the assets tab on the main screen (I think I'm correctly connected to the testnet node, no reason for it to permanently load). Could use some QSR to test fusing and other functionality, please send testnet funds to:

z1qruuq0aafta69sc5fwdq5zdcnu249n3tg90tkj

-------------------------

TrevorLeahy3 | 2023-07-11 12:31:37 UTC | #86

I did have v0.0.1 running without problems but after uninstalling and trying v0.0.2 it will not get past the logo loading screen. Any ideas?

Thank you for your time.

-------------------------

Dr.GreenThumb | 2023-07-11 13:18:38 UTC | #87

I've fused 1000 QSR and I'm getting this prompt when I'm trying to send some founds to another address. The tx goes through. 
![Screenshot_2023-07-11-15-52-45-43_b8f5adacd1a9a55e43f3920841f86346|225x500](upload://hHkXm8llUD29dVtnk22XVdhqZfU.jpeg)

In the wallet section I'm getting the endless spinning circle for the assets tab
![Screenshot_2023-07-11-15-52-57-02_b8f5adacd1a9a55e43f3920841f86346|225x500](upload://lqNGJfRGAqW25wWYBbvU0wZlz06.jpeg)

The button for editing the address name doesn't seem to work, also I can't switch between addresses
![Screenshot_2023-07-11-16-15-10-82_b8f5adacd1a9a55e43f3920841f86346|246x500](upload://nsX6r5dH25BG1zgTi9xtl0PeSCN.jpeg)

-------------------------

DrBlaze_21 | 2023-07-11 18:46:02 UTC | #88

[quote="romeo, post:83, topic:659"]
* was able to create new addresses
[/quote]

This should work. Try clicking again on the `+ Create new address`

[quote="romeo, post:83, topic:659"]
* was not able to rename wallet addresses
[/quote]

Not implemented yet.

[quote="0x3639, post:84, topic:659"]
I’ve reposted v0.0.2 on DigitalOcean in case we run out of downloads
[/quote]

Check new download link below.

[quote="TrevorLeahy3, post:86, topic:659"]
I did have v0.0.1 running without problems but after uninstalling and trying v0.0.2 it will not get past the logo loading screen. Any ideas?
[/quote]

Did you try to create a new wallet?

[quote="Dr.GreenThumb, post:87, topic:659"]
I’ve fused 1000 QSR and I’m getting this prompt when I’m trying to send some founds to another address. The tx goes through.
[/quote]

This should be considered as a "recommendation" rather than a "prompt".

[quote="Dr.GreenThumb, post:87, topic:659"]
In the wallet section I’m getting the endless spinning circle for the assets tab
[/quote]

Coingecko API is broken.

[quote="Dr.GreenThumb, post:87, topic:659"]
The button for editing the address name doesn’t seem to work, also I can’t switch between addresses
[/quote]

You need to click in the top right corner.

New v0.0.2 version. I forgot to add a `SHA-256` checksum. Here's the hash for the latest version:

```
b5841f7bef7602fe5d64e9edeb0ccf094d7a7bd75606efac21f5d6f645a3da34
```

Download [latest version here](https://t.ly/6DCEI). It is still `v0.0.2` and you should first uninstall it.

- Please don't use mainnet funds
- Check `SHA-256` hash before installing

**CHANGELOG**:

* :cockroach: Fixed delegation amount
* :cockroach: Fixed owner address display

-------------------------

crack | 2023-07-12 00:00:41 UTC | #89

Since enter the last pin, it take about 2-3 seconds being on this display.
And the last pin "dot" doesnt filled.
Hope for better ux at this stage
![Screenshot_2023-07-11-11-25-14-05_b8f5adacd1a9a55e43f3920841f86346|234x500](upload://3ZnH7PCxzWhCfBFXKGDOfFDLudg.jpeg)

-------------------------

romeo | 2023-07-12 04:18:12 UTC | #90

[quote="DrBlaze_21, post:88, topic:659"]
This should work. Try clicking again on the `+ Create new address`
[/quote]

I was reporting it does work 👍 sorry for the confusion

Tested the newest version too, experienced the same lag on entering the last pin digit as @crack above

Also still have the spinning wheel under Assets tab always

Another UX suggestion: add a plasma indicator on the Wallet page for the selected address. Like a bar or something that is filled a percentage based on how much plasma you have fused?

-------------------------

coinselor | 2023-07-12 17:34:54 UTC | #91

[quote="romeo, post:90, topic:659"]
add a plasma indicator on the Wallet page for the selected address
[/quote]

I second this request, I think in an earlier iteration of the wallet ui you already had the feature.

-------------------------

mehowbrainz | 2023-07-17 16:54:43 UTC | #92

[quote="DrBlaze_21, post:88, topic:659"]
Download [latest version here ](https://t.ly/6DCEI). It is still `v0.0.2` and you should first uninstall it.
[/quote]

The link expired btw.

-------------------------

sumamu | 2023-07-17 16:58:02 UTC | #93

[quote="mehowbrainz, post:92, topic:659"]
The link expired btw.
[/quote]

It's not possible to upload the APK directly to the forum?

-------------------------

mehowbrainz | 2023-07-17 16:58:56 UTC | #94

See this @sumamu

-------------------------

sumamu | 2023-07-17 17:00:24 UTC | #95

I understand.
@DrBlaze_21 you can create an empty github repo and upload the APK to the Releases section.

-------------------------

0x3639 | 2023-07-17 19:37:20 UTC | #96

[quote="mehowbrainz, post:92, topic:659"]
The link expired btw.
[/quote]

This should work

https://hypercore.nyc3.digitaloceanspaces.com/mobile-wallet/syrius-debug-alpha-v0.0.2.apk

Check the checksum.

-------------------------

nbd | 2023-08-20 20:54:53 UTC | #97

Got this error message when I tried to create a new wallet. 
![image|239x500](upload://8he6bFYK2zePPiPTH0AQS37PEI3.jpeg)

-------------------------

nbd | 2023-08-23 00:45:20 UTC | #98

@DrBlaze_21 Some assistance or at least an answer would be appreciated. Thank you.

-------------------------

nbd | 2023-08-24 23:41:31 UTC | #99

bump

-------------------------

NeoShredder | 2023-08-25 02:21:46 UTC | #100

@DrBlaze_21

-------------------------

nbd | 2023-08-30 23:53:59 UTC | #101

bump

-------------------------

nbd | 2023-09-05 14:21:16 UTC | #102

bump

-------------------------

angelo_a_jr | 2023-11-18 22:01:29 UTC | #103

Could be an epic time to finally get this into production.  Are there major changes needed to keep up with latest Syrius versions?  @DrBlaze_21 @aliencoder

-------------------------

aliencoder | 2023-11-19 17:42:55 UTC | #104

In my opinion I want to wait for the final conclusions regarding dynamic Plasma. AppStores usually are against proof-of-work in mobile devices and it would be harder to list an app that uses CPU/GPU to compute PoW.

Moreover, people with lower end devices would need to wait more time to send/receive transactions, making the UX progressively worse.

That's why I'm advocating for a [hybrid approach](https://forum.hypercore.one/t/dynamic-plasma-discussions/62/208) where we have a tri-lane system for creating Plasma:
- PoW with multiple algos (RandomX, SHA-3 and Equix)
- Fuse (lock) QSR with dynamic thresholds
- Burn ZNN

I'm trying my best to find ways to complement the feeless narrative with a more robust system, while promoting game-theoretic compatible models that will ensure the long term sustainability of the network. 

Burning ZNN/fusing QSR would be the preferred way to go for mobile users that are constrained by low computing resources.

Alternatively, PoW can be an option for APKs or IPAs distributed outside official AppStores if they reject the apps containing the libpow binaries.

-------------------------

