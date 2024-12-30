Thread: develop-syrius-wallet-mobile-app
mehowbrainz | 2023-02-11 02:31:08 UTC | #1

Following my [reply on the Syrius Wallet Mobile App design/prototype topic](https://forum2.zenon.org/t/syrius-wallet-mobile-app/659/33?u=mehowbrainz), I believe there are a few points to address and discuss with the community before anyone takes-on the development of this mobile app:

- To publish to the iOS Apple / Google Play store you need a developer account which requires company name, address, contract information. 
- Swaps within a wallet app invites regulatory scrutiny. I have experience when I was in a DEX team and it's a pretty complicated subject.
- @sol mentioned that some libraries that the embedded node uses may not be accepted by Google/Apple.

Some of these topics come with immense responsibilities. Let's discuss.

-------------------------

sol | 2023-02-11 02:50:45 UTC | #2

1. Is anyone here willing to dox to publish the app in either app store? 
Otherwise, we might have to host on 3rd-party app repositories and/or funnel users to our website(s) for a direct download + .ipa/.apk sideload.
Note: non-technical users may think these alternatives are sketchy, despite open-sourcing the code.
2. By "regulatory scrutiny", do you mean users will be subject to KYC or just the publishing party?
3. I was mistaken, DrBlaze mentioned the [PoW library might not be accepted](https://forum2.zenon.org/t/syrius-wallet-mobile-app/659/11?u=sol_sanctum) by Google/Apple.
Some experimentation may be required here.

There are a few decisions we should agree on before we begin software development.
Vilkris brought up some good points about the embedded node in [this post](https://forum2.zenon.org/t/syrius-wallet-mobile-app/659/10?u=sol_sanctum).

DrBlaze has provided us with a beautiful UI. 
Let's discuss technical/operational logistics and build this app. :)

-------------------------

mehowbrainz | 2023-02-11 03:03:02 UTC | #3

[quote="sol, post:2, topic:1288"]
By “regulatory scrutiny”, do you mean users will be subject to KYC or just the publishing party?
[/quote]

From my experiences with the AML specialist I spent many months working-with: likely either or, or even both.

As for the publishing if you blindly trust GPT like I do:

![Screen Shot 2023-02-10 at 10.02.40 PM|676x500](upload://7BYM2xuvPtVCW5qDlL2av8OP9Pg.png)

-------------------------

mehowbrainz | 2023-02-11 03:06:49 UTC | #4

>  you can distribute progress builds to a limited set of users on known devices, without having to go through beta app review

Apple doesn't specify the number of devices: https://developer.apple.com/documentation/xcode/distributing-your-app-to-registered-devices

-------------------------

vk_stex | 2023-02-13 15:24:25 UTC | #5

there are no KYC requirements in stores for wallet apps
they could be if you positioning your app as exchange/trading platform, but stores not a government they do basic compliance only 
about accounts in stores, google 25$ once, apple 99$ annually
from my experience iOS brings way better users, it's definitely worth to focus there 
any out of stores ways like sideload, f-droid/apk could work for very enthusiastic users, this way has no mass adoption or even harm trust by "oi, their app unsafe because it doesn't exist in stores"
What you see in "about" is not always the same person or business boarded to store, this data could be edited for any purpose. So if you not hiding from authorities but wanna protect you personality there are no any visible problem based on my experience.

-------------------------

mehowbrainz | 2023-02-13 15:28:46 UTC | #6

Would having a swap feature within the wallet automatically position it as an "exchange/trading" platform?

-------------------------

vk_stex | 2023-02-13 15:42:15 UTC | #7

If it dex - no. There are chance that you would prove that’s decentralized. But trust wallet or tronlink has no kyc for example.

-------------------------

romeo | 2023-02-13 22:28:08 UTC | #8

A few points to add:

* I think connecting to a public node should be the default behavior of a mobile syrius, an embedded node would require heaps of testing and also likely have baseline hardware requirements. Perhaps it could randomly select from a defined list of public nodes on launch? The list could get updated daily when the wallet is open.

* re IOS vs Android - trust wallet is a good example of the intricacies of the Apple ecosystem. The Android version of Trust wallet has embedded dApps that you can run from within the wallet, including a browser. Apple doesn't allow this, so the feature is completely absent on IOS. Something to consider if you think we may end up with zApps running natively out of Syrius in the future.

* On the publishing front, I feel it's critical to have it in the relevant app stores as opposed to a side load/apk install. As @vk_stex said, there are ways to obfuscate your identity to the broader public, just need an individual who's willing to do the paperwork.

-------------------------

