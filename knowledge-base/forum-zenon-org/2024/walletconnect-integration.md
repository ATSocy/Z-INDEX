Title: WalletConnect integration

URL Source: https://forum.zenon.org/t/walletconnect-integration/1178/print

Published Time: 2023-01-12T19:35:17+00:00

Markdown Content:
January 12, 2023, 7:35pm  1

Bring Web3 connectivity to the Zenon ecosystem.

Integrate the [WalletConnect protocol](https://walletconnect.com/) into Syrius:

*   [Web3Wallet SDK for Dart/Flutter](https://pub.dev/packages/wallet_connect)
*   [Web3Modal SDK for Dart/Flutter](https://pub.dev/packages/walletconnect_qrcode_modal_dart)
*   Integrate ZNN cryptography
*   Syrius deep link support
*   Syrius scan QR code support
*   Testing

I am supportive of your suggestion for utilising WalletConnect.

I’ve read through the reasoning presented by both sides and I think this is the way to go. I don’t mind if this means more time to implement it; if it needs to be done it needs to be done.

Thank you for your support, I’ll start with an in-depth research of the WalletConnect protocol and after that see what dependencies are required for the integration.

Its workflow hasn’t been validated for marketing/analytics needs sought, so I wouldn’t say it’s the way to go just yet. There may be simpler paths available, though I’m sure such integration may be useful nonetheless for other reasons than marketing.

Regarding the WalletConnect integration:

*   [Web3Modal demo for Web](https://web3modal.com/try-it-out)
*   Updating the znn.ts SDK
*   Updating the ZNN Dart SDK to work on Web (harder to do given the `ffi` dependency)
*   Syrius desktop deep linking / copy-paste WC link / upload QR with detection / scan QR using screen recorder ([check out this wallet](https://infinitywallet.io/) to see how WC should work - it only lacks basic copy-paste support)

I have some questions:

*   Would deeplinks work if the wallet is closed/unauthenticated?
*   Is the connection made with the entire wallet (meaning all of its addresses?), or is it on an address basis?
*   If by address, can multiple connections be made from the web for each address?
*   I assume a new view will be added in syrius desktop to confirm/reject the transaction. Upon confirmation.
*   Can the web button deeplink into the syrius wallet to enable the connection in the first place, bypassing the need for a WalletConnect modal? Otherwise I guess users need to go in the “Desktop” section of the modal and find syrius? If yes, how do we get listed here:

[![Image 107: Screenshot 2023-01-15 at 2.59.58 PM](https://forum.zenon.org/uploads/default/optimized/2X/5/524c2aa41716fdf5c90a5eb4020b0bcbe4febe3c_2_690x253.png)](https://forum.zenon.org/uploads/default/original/2X/5/524c2aa41716fdf5c90a5eb4020b0bcbe4febe3c.png "Screenshot 2023-01-15 at 2.59.58 PM")

Yes, it will literally open the wallet (if it’s unauthenticated, you’ll need to unlock it first). Even better, it will also work if Syrius is not installed yet: check how Infinity wallet works (clicking on `Go to wallet` will open [https://infinitywallet.io/wc/?uri](https://infinitywallet.io/wc/?uri) where you can hook your tracking analytics).

Just one address per connection (Syrius works this way).

Yes

Yes and I also see that `v2` has the `auto-signing` feature.

We can get listed [here](https://explorer.walletconnect.com/) → Submit project

How does the connection know which address to connect-to? Will it ask in syrius, or it assume that the currently selected address is the one to connect? If it can ask which address to connect, or even give options to connect to multiple (or all), would be great but I understand it may not be possible due to the way syrius is built.

Could be great to develop a web-based syrius, though even though it can auto-sign, it would still open syrius to trigger the tx signing automatically after the user authenticated into his wallet right?

It will assume the currently selected address. It cannot connect to multiple addresses (and it shouldn’t).

Flutter for Web is in beta, but I saw that the [Syrius browser extension](https://github.com/DexterLabZ/syrius-extension) is already in development. I don’t know how the auto-signing works, but I saw that Infinity wallet has this feature implemented and it works in production.

We’ll add the ability to connect-to multiple addresses (one by one) from the web. If someone attempts to transact from an unselected address within syrius, can there be a method via deeplink to change the address profile for syrius, and then trigger the transaction? (note: which would be required regardless)

[sol](https://forum.zenon.org/u/sol) January 16, 2023, 2:39pm  11

Address profile switching in Syrius is not required to sign transactions for alternate addresses that are part of the same keystore.

Thanks [@sol](https://forum.zenon.org/u/sol), that simplifies the UX

Also in that case, I wonder if a web-based dApp can serialize reward claiming for all connected addresses… something missing in syrius atm as you have to switch between profiles to claim for each address.

[sol](https://forum.zenon.org/u/sol) January 16, 2023, 3:36pm  14

That may or may not have been intentional.

I think it’s intentional. I think mixing addresses together can hurt on-chain privacy. I personally wouldn’t use this feature.

I see, so the idea of intentional delays between transactions of different addresses (part of a keystore), invites more privacy as one can assume less potential links between addresses?

[sol](https://forum.zenon.org/u/sol) January 16, 2023, 10:54pm  18

Currently, there aren’t any explicit delays in the wallet. The process of requiring users to manually switch to a different address introduces a delay.

Mehowz might be inquiring about his service inserting an artificial delay between transactions that originate from the same keystore.

Yes this is what I meant.

If something like that was built, and if we can manage to serialize transactions one after another to claim all connected wallet rewards.

Started working on `WalletConnect v2` integration.

`WebApp` ← → `WalletConnect SDK` ← → `Syrius`

How does it work?

*   Step 1: The user opens the `WebApp` and clicks [“Connect Wallet”](https://web3modal.com/)
*   Step 2: The user has 3 options:  
    Option A: He `scans` the `QR code` (containing the WC link encoded as a QR)  
    Option B: He `copies` the `WC link`  
    Option C: He `clicks` on Desktop → `Syrius` (`deep linking`)
*   Step 3: `Session approval`: he confirms the connection from the `Syrius` wallet
*   Step 4: `Sign message`: When a transaction is initiated by the `WebApp`, the user signs it in `Syrius`
*   Step 4: `Session disconnect`: The user can manage his active connections and terminate the connection with a particular `WebApp`

There are 2 requirements to finish this project:

1.  Syrius WalletConnect support

*   WalletConnect Tab
*   Deep linking support
*   WalletConnect link support
*   QR code scanning

2.  WalletConnect SDK

*   `Dart` language support
*   `Zenon` cryptography integration

[vilkris](https://forum.zenon.org/u/vilkris) January 31, 2023, 8:48pm  21

Before taking on this work, don’t you think the previous features you’ve been working on should be finalized first and made into PRs in the main Syrius repo? There’s a lot of stuff pending that we should focus on getting reviewed and merged first in my opinion.

One question about WalletConnect:

If I understand correctly it requires you to register a WalletConnect account so you get the “project id”. How will this account be controlled?

I agree that the wallet requires in-depth testing, but most of the tasks are done and working fine.

I’ll setup the account and create a `projectId`. But in the future the relay server can be [self-hosted](https://github.com/WalletConnect/walletconnect-monorepo/discussions/1575).

[vilkris](https://forum.zenon.org/u/vilkris) February 1, 2023, 9:09pm  23

So in the future would it be possible to have multiple community members running the WC relay server and a user could select their server in Syrius? Or would it have to be just be one server?

Still, I’m not too enthusiastic about only one community member being in control of the project ID and having the power to shut it down.

Unfortunately today the solution is limited in this regard. I dislike this solution too, but we’ll have to wait until they open source the server part.

Yes. We can implement it in an invisible manner for the end user, in a round-robin fashion and if a server fails, we’ll have a fallback option.

[0x3639](https://forum.zenon.org/u/0x3639)

February 1, 2023, 9:57pm  25

looks like the open source server is in their roadmap.

I know, I’ve already pointed this out.

Check [this out](https://web3modal-dev.pages.dev/v2Customised) (replace OREID with Syrius):

[![Image 108: wc](https://forum.zenon.org/uploads/default/optimized/2X/a/a3e24ae8ed3e210a73cbcd8f5fe132cf378f0148_2_211x375.png)](https://forum.zenon.org/uploads/default/original/2X/a/a3e24ae8ed3e210a73cbcd8f5fe132cf378f0148.png "wc")

WalletConnect integration status update:

WalletConnect Tab ![Image 109: :white_check_mark:](https://forum.zenon.org/images/emoji/twitter/white_check_mark.png?v=12)  
Deep linking support ![Image 110: :white_check_mark:](https://forum.zenon.org/images/emoji/twitter/white_check_mark.png?v=12)  
WalletConnect link support ![Image 111: :white_check_mark:](https://forum.zenon.org/images/emoji/twitter/white_check_mark.png?v=12)  
QR code scanning ![Image 112: :white_check_mark:](https://forum.zenon.org/images/emoji/twitter/white_check_mark.png?v=12)

WalletConnect integration is almost ready for testing:

Syrius 0.0.7 is going to be epic!

Syrius **WalletConnect** version is [ready for download](https://github.com/alienc0der/syrius/releases/tag/v0.0.6-alphanet).

[0x3639](https://forum.zenon.org/u/0x3639) April 24, 2023, 9:37pm  34

Guys we should discuss who is going to test on what machine type.

I will test on a Mac with M1 processor. I will sync with a local node and try a remote node. We should discuss a testing protocol. Maybe [@sol](https://forum.zenon.org/u/sol) could recommend a testing protocol? Or if anyone else wants to, let’s all use the same procedure so we get consistent testing.

We’ll also need an online minimal web app to test it on?

[romeo](https://forum.zenon.org/u/romeo) April 25, 2023, 3:26am  36

Agreed if someone can write up a test case I’ll gladly run through it on multiple desktops

Also awesome work [@aliencoder](https://forum.zenon.org/u/aliencoder) ![Image 113: :pray:](https://forum.zenon.org/images/emoji/twitter/pray.png?v=12)

Yes. The web app can be written in any language that is supported by the [Web3Modal SDK](https://docs.walletconnect.com/2.0/web3modal/about).

Clipboard watcher support ![Image 114: :white_check_mark:](https://forum.zenon.org/images/emoji/twitter/white_check_mark.png?v=12)

Syrius desktop can automatically detect a WalletConnect URI directly from your clipboard. You need to explicitly enable this feature by navigating to Settings → Wallet Options → Enable clipboard watcher

Anyone that wants to develop dApp clients to interact with Syrius can integrate the following:

[WAGMI Connect Wallet](https://wagmi.sh/examples/connect-wallet)

[Web3Modal](https://web3modal.com/)

[ConnectKit](https://docs.family.co/connectkit/try-it-out)

[ZNNAYIID](https://forum.zenon.org/u/ZNNAYIID) April 27, 2023, 8:04pm  39

feedback, it gives me unlock failed, I tried the common fix where you disable the internet and login but it didn’t work, then I switched to my embedded node through 0.05 since I was using a public node in order to use syrius 0.0.6, but while syncing it force closed and now none of the versions is working and all of them are force closing few seconds after the splash screen (0.0.3-0.0.6)… only 0.0.2 is working but I guess because it didn’t have the embedded node option… so this issue is 100% related to the embedded node and now after trying this version of syrius all the other versions are affected now.

I guess I’ll stop using syrius for quite sometime until it’s stable again.

It’s working perfectly on Windows 11 and MacOS latest version.

I sent you a DM to identify your issue.

I’ve thoroughly investigate the issue and found the problem:

The `libznn`, `argon2` and `libpow` dynamic libraries are missing from the builds. This is due to merging code that was modifying the build scripts.

I will fix the issue and release a new version shortly.

[ZNNAYIID](https://forum.zenon.org/u/ZNNAYIID) April 28, 2023, 12:08pm  42

0.0.6 on the official repo has all the files, but still crashes after splash screen when using embedded node.

The WalletConnect integration is ready for testing:

[https://github.com/alienc0der/syrius/releases/tag/v0.0.6-alphanet](https://github.com/alienc0der/syrius/releases/tag/v0.0.6-alphanet)

Navigate to WalletConnect tab and paste a `WalletConnect v2` link. There are 2 tables, one for pairings and another one for sessions.

I’ve tested it with a `WalletConnect` client written in `Dart`:

The implementation consists of:

1.  The following methods (can be called by the `dApp`):

*   `znn_sign`: signs a message
*   `znn_info`: retrieve current `address`, `node URL` and `chainId`
*   `znn_send`: sends an `accountBlock`

2.  The following events (are pushed to the `dApp` in real time):

*   `chainIdChange`: notifies the `dApp` when the `chainId` is changed
*   `addressChange`: notifies the `dApp` when the `address` is changed

At the moment the you can pair Syrius with any dApp using the following methods:

*   Desktop QR scan (on-screen scanner)
*   WalletConnect v2 URI (you can enable clipboard watcher from `Settings` → `Wallet Options` and it will automatically detect valid WalletConnect URIs)
*   Deep linking via `syrius://`

[sol](https://forum.zenon.org/u/sol) May 28, 2023, 5:52pm  44

Are any of these features dependent on host OS?  
If so, which ones?

Glad you’ve asked.

Supported on Windows, Linux, MacOS.

Supported on Windows, Linux, MacOS.

Supported on Windows, MacOS. No Linux support at the moment.

Upcoming implementation:

*   Desktop Camera scan (using the camera of the device)

Windows package was published [4 days ago](https://pub.dev/packages/camera_windows)  
MacOS package was published [34 days ago](https://pub.dev/packages/camera_macos)

The implementation is now complete. Next week I’m planning to apply for AZ funding.

I’ve asked [@0x3639](https://forum.zenon.org/u/0x3639) to create a new WalletConnect project (create an account on [https://cloud.walletconnect.com/](https://cloud.walletconnect.com/)) and I’ll integrate the corresponding `projectId` into the build system.

We’ll need the following resources:

*   Name\* The name to display in the explorer
*   Description\* A short description explaining your dapp/wallet
*   Homepage\* The website URL for your project
*   Logo\* Square format is a requirement for our Explorer API. At least 500x500px PNG. Max 2MB.
*   Testing Instructions\* Instructions on how to test your WalletConnect integration.
*   Short name\* Displayed in the QRCode Modal → should be “syrius” or “Syrius”
*   Primary color Set button and UI colors
*   Secondary color Set button and UI colors

[@ZNNAYIID](https://forum.zenon.org/u/znnayiid) can help us with the logo I guess

[sol](https://forum.zenon.org/u/sol) May 28, 2023, 6:53pm  46

It would be nice to support URIs on all three OS.  
Any plans to support Linux in the future?

I know, but the [package](https://pub.dev/packages/app_links) I use [doesn’t support Linux](https://github.com/llfbandit/app_links/issues/20) yet.

It is well maintained, so we can assume that they will add Linux support in the future.

Fortunately, most users are on Windows and MacOS. Linux users can use the on-screen scanner or the copy-paste URI method.

The camera method is also an “overkill” (I assume most users will use either the copy-paste or the on-screen QR scanner), but I’ll gladly add it to cover all possible scenarios.

Go ahead and try the WalletConnect integration now by connecting your Syrius desktop wallet to the demo dApp (you have to thank [@dexter703](https://forum.zenon.org/u/dexter703)):

Download [Syrius v0.0.7](https://github.com/alienc0der/syrius/releases/tag/v0.0.7-alphanet)  
Check [Demo dApp](https://demo.zenon.community/demo)

Feel free and DM me any bugs related to the WalletConnect implementation. I will prepare the AZ application in the meantime.

A few questions/comments:

*   Why is the pairing added to the list before I’ve accepted it?
*   I tried to connect with the WalletConnect Link and with the QR Scanner but nothing happens in the webapp when I approve the session.
*   Should the yes no button colors be reversed?

[![Image 115: image](https://forum.zenon.org/uploads/default/optimized/2X/7/75168b99c403e1eda77f09d644b1ad54695066dc_2_690x345.png)](https://forum.zenon.org/uploads/default/original/2X/7/75168b99c403e1eda77f09d644b1ad54695066dc.png "image")

Also, I’m getting this error on all the cards:

[![Image 116: image](https://forum.zenon.org/uploads/default/optimized/2X/e/ea56b86d5319ff3395556418e12c9c36713e25c6_2_690x350.png)](https://forum.zenon.org/uploads/default/original/2X/e/ea56b86d5319ff3395556418e12c9c36713e25c6.png "image")

You don’t accept pairings, you accept session requests. This is how it works:

Step 1: Pairing  
Step 2: Session request

You need to do the pairing first. You can see that the title of the dialog is “Approve session”. Also look at the Pairing List table from your screenshot and you’ll see that “Active” is still “No” until you accept the session request.

First, you’ll need to disconnect from the current session/pairing before reconnecting. What OS do you use?

I’ve used the standard dialog colors.

You’re probably connected to mainnet `znnd`. You’ll need [@MoonBaZe](https://forum.zenon.org/u/moonbaze)’s `znnd` that has `BigInt` support. This Syrius version is shipped with `BigInt` support.

[vilkris](https://forum.zenon.org/u/vilkris) June 7, 2023, 9:53am  51

I’m on Win10. Tried it with Brave and Firefox.

There is an edge case for the on-screen QR scanner when the QR code is white on black (dark mode) - it won’t work (only black on white QR codes can be processed). I’m already looking into it.

Please check the [latest release](https://github.com/alienc0der/syrius/releases/tag/v0.0.7-alphanet).

Update 1: The namespace was changed to `mainnet`: `zenon:1`. This is different from the `chainId`. You’ll be able to test the wallet on `mainnet`, `testnet` or `devnet`.

Update 2: The [demo web app](https://demo.zenon.community/demo) is now live with the `mainnet` namespace.

Tested on latest Safari release. Everything works flawlessly. Well done and thank you, this is a great tool for creating awesome UX’s

I just tested with chrome + firefox concurrently. Everything works like a charm, wasn’t able to find any edge cases. Was testing with and without a ZNN balance.

Any dev know if this is possible?

1.  An event is triggered in syrius app using WC (from let’s say a Safari/Chrome/Firefox session).
2.  The user approves the prompt for the event i.e. sending a transaction.
3.  Since the event trigger came from a Safari/Chrome/Firefox session, the syrius dapp puts into focus that last application which triggered the event? This way the user doesn’t have to switch between apps himself? (only an inconvenience really for users with 1 monitor who have to switch between apps, users with multiple monitors may not see this as a requirement since they’ll see their Safari/Chrome/Firefox session update on its own).

The same question for the reverse case, where if an event is triggered from a Safari/Chrome/Firefox session using some dapp, the syrius app is put into focus so the user automatically sees the prompt to approve/reject the tx.

In the approval prompt windows, a ZN logo is loaded. Where is that ZN logo sourced from? And can any dapp make their own image appear in the prompt?

[0x3639](https://forum.zenon.org/u/0x3639) June 9, 2023, 1:29am  58

[@aliencoder](https://forum.zenon.org/u/aliencoder) [@sumamu](https://forum.zenon.org/u/sumamu) looks like when you use my upgraded node: wss://my.hc1node.com:35998 that is running go-zenon 0.0.6 with the latest RC of syrius you cannot see all the pillars and sentinels.

I think it’s possible, but I need to implement it first.

[romeo](https://forum.zenon.org/u/romeo) June 11, 2023, 1:03pm  62

all Yes and No prompts in Syrius are Red for Yes and Green for No - I always assumed it was to make you think twice before pressing

[romeo](https://forum.zenon.org/u/romeo)

June 11, 2023, 1:05pm  63

works seamlessly with the demo dApp and was really responsive.

A couple of things I noticed:

*   When cancelling an action, I get two of the error prompt  
    ![Image 117: image](https://forum.zenon.org/uploads/default/original/2X/1/1e636f3206afeda50eb216529c014cda4d246f91.png)
*   After disconnecting from the Syrius end, you get no prompt on the dApp (browser) side, not sure if it’s possible to provide a disconnected prompt on the web side?

thanks!

This is a web app bug. I’ll ping [@dexter703](https://forum.zenon.org/u/dexter703) to fix it.

In Syrius I have an `onDisconnect` callback. I’ll check and inform [@dexter703](https://forum.zenon.org/u/dexter703) if it’s possible.

I’ve submitted 2 projects for WalletConnect:

*   [WalletConnect integration (1/2)](https://zenon.tools/accelerator/58e711ca182e2a440f3a2645a4f314d2b6d4f69deb46ade32dc6f44cbaf9a1ec)
*   [WalletConnect integration (2/2)](https://zenon.tools/accelerator/cd0398ffec479c7e704ac58545b1859f93188dff8fc8a9da6e9d2992f96942c1)

I will request funding (submit phase) only for 1.5 projects. I will proceed requesting the remaining funds after I finish implementing the feedback.

A fraction of the funds are reserved to [@dexter703](https://forum.zenon.org/u/dexter703) for this awesome demo web app.

Thank you for the feedback!

[ZNNAYIID](https://forum.zenon.org/u/ZNNAYIID) June 11, 2023, 8:29pm  66

Since we are paying also for the web app demo, can you tell us how much did it cost?

The cost is between 1/4 and 1/5 of one project.

[ZNNAYIID](https://forum.zenon.org/u/ZNNAYIID) June 11, 2023, 9:57pm  68

so we gonna pay around 1100 ZNN and 11K QSR for a web app DEMO which was supposed to be used to test the web connect integration, and now it’s basically useless and it won’t be used anymore?

You’re either naive or ignorant. The demo web app is definitely not useless: it can be used as a skeleton for future WalletConnect web projects. In fact this was its purpose from the very beginning.

It also includes a dev [documentation](https://demo.zenon.community/).

[ZNNAYIID](https://forum.zenon.org/u/ZNNAYIID) June 12, 2023, 10:35am  70

Instead of calling me naive or ignorant, maybe you should’ve pointed out to all of these points when you submitted your proposal instead.  
Not just “ A fraction of the funds are reserved to [@dexter703](https://forum.zenon.org/u/dexter703)” without further explaining it. You are asking for 2 sentinels so you better explain in details what this community is paying for.

Here you go with a proper and well explained proposal submission :

Maybe you’ll do better next time.

[0x3639](https://forum.zenon.org/u/0x3639) June 12, 2023, 12:04pm  72

[@aliencoder](https://forum.zenon.org/u/aliencoder) can you estimate the rough number of hours you have spent? Looks like at least 2 months of work or more. Clearly you and MIke have spent a ton of time.

[@mehowbrainz](https://forum.zenon.org/u/mehowbrainz) I’ve implemented the feedback.

**Bonus**

_Custom_ deep links:

Staking: `syrius://stake`  
Delegating: `syrius://delegate`  
Fusing: `syrius://fuse`  
Sentinels: `syrius://sentinel`  
Pillars: `syrius://pillar`

Next step: _custom_ deep links with actions =\> by showing a dialog to the user

PS: I’ve also fixed a bug that was causing “freezing” on the splash screen due to WalletConnect websocket timeouts.

Download & test the [latest version](https://github.com/alienc0der/syrius/releases/tag/v0.0.7-alphanet).

I started doing research on WalletConnect the next day after I’ve published this thread.

I hope this tool will be used by skilled web developers like [@dexter703](https://forum.zenon.org/u/dexter703) [@vilkris](https://forum.zenon.org/u/vilkris) and others to enhance the overall user experience. [@dexter703](https://forum.zenon.org/u/dexter703) has done a very good job integrating it into the Bridge UI.

We should list NoM [here](https://docs.walletconnect.com/2.0/advanced/multichain/chain-list).

Another interesting feature of WalletConnect is the [Chat API](https://docs.walletconnect.com/2.0/api/chat). I think it is an important piece of puzzle for the off-chain coordination of P2P swaps.

[0x3639](https://forum.zenon.org/u/0x3639) June 13, 2023, 10:18pm  76

I can work on that tomorrow.

The custom deep links + actions = awesome. Also implemented [this feedback](https://forum2.zenon.org/t/walletconnect-integration/1178/56?u=mehowbrainz)?

If changeAddress is triggered, can we notify the user in the web app? i.e. “Would you like to maintain the connection to this new address? Yes/No” If no, it closes the session.

You can notify the user, but you can’t force him to stay on a particular address (it can be possible if you add a code into Syrius that does this). He can do whatever he wants in Syrius. WalletConnet is a protocol, you can’t control user actions with it.

I cant seem to change the node used for the bridge, not sure if its a WalletConnect thing though. Initially used WC while connected to the HC1 public node but now trying to use the embedded in Syrius but HC1 seems to be the only one available to the bridge.

I noticed whichever address is selected in Syrius is reflected at the bridge app but should the bridge node update in the same way?

The bridge can’t use the embedded node because it can’t connect to it. The embedded node is running on your computer (localhost) and the bridge cannot connect to it for obvious security reasons (nobody should be able to access your internal network or connect to your computer from the Internet).

Since you’re not connected to a public node, the bridge uses a default public node to connect to.

[sol](https://forum.zenon.org/u/sol) June 18, 2023, 2:15pm  83

I’m not sure if this is correct.

explorer.zenon.network can connect to locahost nodes.

Only if you load it via `http` otherwise it throws the following error:

`Mixed Content: The page at 'https://explorer.zenon.network/' was loaded over HTTPS, but requested an insecure XMLHttpRequest endpoint`

I started getting this error when opening the Syrius that has WalletConnect. Can’t do anything after this, it’s just a blank screen showing the error after the start up animation.

Syrius with no WalletConnect works fine.

[![Image 118: image](https://forum.zenon.org/uploads/default/optimized/2X/1/17812df1928ae40bb44301ba445acba6e6870932_2_625x500.png)](https://forum.zenon.org/uploads/default/original/2X/1/17812df1928ae40bb44301ba445acba6e6870932.png "image")

I’ll check.

[@vilkris](https://forum.zenon.org/u/vilkris) I’ve added [persistent logging](https://forum2.zenon.org/t/syrius-improvements/578/132?u=aliencoder) to pinpoint the error. Please download the latest build.

[0x3639](https://forum.zenon.org/u/0x3639)

June 21, 2023, 9:53am  87

Trying to connect the latest syrius build from yesterday to walletconnect and get the following (see video). I cannot connect the two. Does not seem to produce an error. I’m running this on windows 10.

[![Image 119](https://forum.zenon.org/uploads/default/original/2X/5/56e92d8bee252b76be927e2c2f68c85133850920.jpeg)](https://www.youtube.com/watch?v=WByINhGIn70)

This is the release I’m testing

[![Image 120: image](https://forum.zenon.org/uploads/default/optimized/2X/d/d81c3114512c700a9db5dd362fe0af99bfecc1ec_2_689x370.png)](https://forum.zenon.org/uploads/default/original/2X/d/d81c3114512c700a9db5dd362fe0af99bfecc1ec.png "image")

I’m on it.

[@0x3639](https://forum.zenon.org/u/0x3639) can you check now please? [Here](https://github.com/alienc0der/syrius/releases/tag/v0.0.7-alphanet) is the latest release.

Thank you for voting me!

I’ve created two payout phases ([Phase 1/1](https://zenon.tools/accelerator/58e711ca182e2a440f3a2645a4f314d2b6d4f69deb46ade32dc6f44cbaf9a1ec#phases) for the first project and [Phase 1/2](https://zenon.tools/accelerator/cd0398ffec479c7e704ac58545b1859f93188dff8fc8a9da6e9d2992f96942c1#phases) for the second one). I’ll apply with Phase 2/2 for the second project after all bugs are fixed & feedback is properly implemented.

[0x3639](https://forum.zenon.org/u/0x3639) June 21, 2023, 5:49pm  90

I can report this upgrade fixed the issue I was experiencing.

[0x3639](https://forum.zenon.org/u/0x3639) June 21, 2023, 5:50pm  91

I think you applied for phase 1 & 2. I just approved Phase 1

[vilkris](https://forum.zenon.org/u/vilkris) June 21, 2023, 7:35pm  92

After debugging this issue it turned out to be an obscure bug in the Shared Preferences library that the WallectConnect library is dependent on.

My shared preferences json file was corrupted and the shared prefs library could not read it.

My computer crashed unexpectedly yesterday while I had syrius running which likely caused the file to get corrupted.

The problem was resolved by removing the shared prefs json file.

[New improvement](https://github.com/alienc0der/syrius/commit/a40427c007e4c90812e3eee003478e793993d90e): programmatically display the WalletConnect tab based on the availability of the `projectId`

Update:

I just came across [this](https://github.com/orgs/WalletConnect/discussions/2100): “think of a projectId as a public identifier”.

I think we can safely assign the `WcProjectId` with the actual `String` provided by [@0x3639](https://forum.zenon.org/u/0x3639)

I’ll make the necessary changes.

Is there a way for the WalletConnect integration to seamlessly sign messages without any copy/pasting? I understand that a signature has to be sent back to the dapp.

You don’t want this feature: a malicious dApp can trick you signing transactions and broadcast them on its own. The user must approve every action, including `znn_info`.

What do you want the user to sign?

If you want to sign account-blocks and broadcast them, use `znn_send`.

The dApp can only request certain actions that _must_ be approved by the user inside Syrius.

[sol](https://forum.zenon.org/u/sol) June 27, 2023, 3:30pm  97

What’s the UX for znn\_sign?

1.  App requests message to be signed, calls znn\_sign
2.  Syrius is notified, displays signing prompt to user (Accept/Deny)
3.  User accepts, WC submits signed data back to the app

Is this right?

Yes. This is how it works. Test it by [yourself](https://demo.zenon.community/).

I’m going to integrate `WalletConnect` into the Syrius Mobile Wallet.

[@aliencoder](https://forum.zenon.org/u/aliencoder) any special requirements for mobile? I see that the desktop implementation works flawlessly.

So key. Will enable us to market to mobile audiences.

Awesome!

Only for the initial pairing between Syrius mobile and the `dApp`:

*   Syrius mobile deep link support: fortunately we use the [app\_links](https://pub.dev/packages/app_links) package that supports Android and iOS out of the box
*   Mobile camera support: for the desktop implementation we use an on-screen QR scanner, but for mobile you can use [ai\_barcode\_scanner](https://pub.dev/packages/ai_barcode_scanner)
*   Copy to clipboard: already implemented

If you have any questions or need any help, please dm me!

[@aliencoder](https://forum.zenon.org/u/aliencoder) not sure if this is already mentioned somewhere else, but I used s y r i u s v0.0.7 to create a pair using the WalletConnect button on the [mainnet bridge](https://bridge.mainnet.zenon.community/) website. I cannot connect after removing the pair from s y r i u s.

When trying to connect using the WalletConnect button it just waits for approval from the wallet. The wallet does not have a pair and does nothing.

How can I create a new pair?

Basically you disconnect and you try to reconnect again? Did you refresh the browser window? Feel free to dm me so we can fix this bug. We have persistent logs now (in the `syrius` folder), we should check them.

I’ve updated the `walletconnect_flutter_v2` to latest version `v2.0.12` and now I’m handling the `onSessionProposalError` callback by refreshing the `WalletConnectSessionsBloc`.

I was unable to reproduce the bug.

You mentioned that “typing in `localStorage.clear()` in the console solved the issue”.

Please find the [latest build here](https://github.com/alienc0der/syrius/releases/tag/v0.0.7-alphanet).

If the Syrius wallet freezes unexpectedly, [please update to the latest version](https://github.com/alienc0der/syrius/releases/tag/v0.0.7-alphanet).

It is caused by the `onRelayClientDisconnect` callback that gets called every millisecond. The wallet tries to establish a connection, but without success.

It also triggers the logger, which involves writing on disk (keeping the disk busy and freezing the wallet).

[@mehowbrainz](https://forum.zenon.org/u/mehowbrainz) experienced this earlier. He couldn’t add a node, an action that requires writing on disk.

[romeo](https://forum.zenon.org/u/romeo) July 12, 2023, 11:21pm  106

When do we think the release will be finalized?

Are you planning to submit 0.0.7 to the official Zenon repo (if not already)?

99% final I guess.

[Here](https://github.com/zenon-network/syrius/pull/19) is the pull request.

[0x3639](https://forum.zenon.org/u/0x3639) July 13, 2023, 1:51pm  108

Maybe they are waiting for all bugs to be squashed. Seems like we are very close to that.

I’ve added support for QR scanning using the MacOS built-in camera (it works with Android and iOS out-of-the-box, [@DrBlaze\_21](https://forum.zenon.org/u/drblaze_21) please look at the source code). For Windows I’ll [wait](https://pub.dev/packages/camera_windows#missing-features-on-the-windows-platform) for the official camera implementation.

Download the [latest build here](https://github.com/alienc0der/syrius/releases/tag/v0.0.7-alphanet).

If no bugs are present, I’ll create a new phase to unlock the remaining funds from AZ.

[nbd](https://forum.zenon.org/u/nbd) July 16, 2023, 2:52pm  110

Latest release works perfectly here on MacOS M1. No bugs ![Image 121: :clap:](https://forum.zenon.org/images/emoji/twitter/clap.png?v=12)

*   Fixed the session refresh bug
*   Updated WalletConnect library to [v2.0.14](https://github.com/WalletConnect/WalletConnectFlutterV2/releases/tag/v2.0.14)

Download the [latest build](https://github.com/alienc0der/syrius/releases/tag/v0.0.7-alphanet).

Anyone running this latest build? I can’t pair to the NoM Bridge website.

I’m successfully connected to both the [bridge](https://bridge.zenon.network/) and the [demo dApp](https://demo.zenon.community/demo).

When you see `relay: Instance of 'Relay', active: false` in the logs, it means that Syrius cannot establish a connection to the relay server operated by the WalletConnect team.

Can someone help us debug the issue? I think the [relay server](https://github.com/WalletConnect/WalletConnectFlutterV2/issues/148) is causing this issue.

Other [relevant issue](https://github.com/WalletConnect/WalletConnectFlutterV2/issues/94).

[0x3639](https://forum.zenon.org/u/0x3639) July 21, 2023, 1:30pm  114

I’ll try later today.

I have [massively](https://github.com/alienc0der/syrius/commit/11728cedce1f5609da61c750c3e0807ce8cd56d0) refactored the WalletConnect integration.

[@mehowbrainz](https://forum.zenon.org/u/mehowbrainz) please try the [latest version](https://github.com/alienc0der/syrius/releases/latest).

Hope it solves all the remaining issues.

[romeo](https://forum.zenon.org/u/romeo)

August 6, 2023, 5:02am  118

hey aliencoder

testing now

have lots of notifications on open:

![Image 122: image](https://forum.zenon.org/uploads/default/original/2X/a/a78da3ba80d1a635436ea495b48ba4d3ddc2a807.png)

(looks like the entire history of the wallet). Also can’t mass clear, have to press ‘x’ on each one individually?

Also took a while (30-40 seconds) to initialize the embedded node and continue synching on first launch (overwriting previous version of 0.0.7). Subsequent launches were normal and quick.

Will test Wallet Connect shortly

I guess we’ll need to add this feature as well.

What OS?

Hope everything is fine now.

[romeo](https://forum.zenon.org/u/romeo) August 6, 2023, 8:13am  120

Win11 x64, had spinning wheels for a while and grey synching circle but then came good when it turned orange

Will report back re Wallet Connect in a couple hours when I get home

[romeo](https://forum.zenon.org/u/romeo)

August 6, 2023, 11:15am  121

Ok so when on the bridge website, attempting to trigger WalletConnect from the browser didn’t seem to work

Selecting Syrius here:

![Image 123: image](https://forum.zenon.org/uploads/default/original/2X/2/2793d50f06b32363e88270d81b74d22ce0d9821b.png)

Then get this:

[![Image 124: image](https://forum.zenon.org/uploads/default/optimized/2X/8/8a66025660301389470f6004afb60daa52ac8795_2_377x500.png)](https://forum.zenon.org/uploads/default/original/2X/8/8a66025660301389470f6004afb60daa52ac8795.png "image")

I had Syrius open already, going to the WalletConnect tab doesn’t show any prompts.

Scanning with the QR code works though.

Need to transfer some Eth first to finish off the testing

Did you try with the `mainnet` or `testnet` bridge? Please try with the [testnet](https://bridge.testnet.zenon.community/) version.

[romeo](https://forum.zenon.org/u/romeo) August 6, 2023, 12:32pm  123

Only main net

Will try with testnet shortly ![Image 125: :+1:](https://forum.zenon.org/images/emoji/twitter/+1.png?v=12)

[0x3639](https://forum.zenon.org/u/0x3639)

August 6, 2023, 1:01pm  124

I’ve been having this issue too on mainnet. The way around it for me is to click the copy button here:

![Image 126: image](https://forum.zenon.org/uploads/default/original/2X/7/7f183e347e5ae77da8704a621a821a77bbc3a591.png)

Then paste here

[![Image 127: image](https://forum.zenon.org/uploads/default/optimized/2X/1/1d096cb85792e2152f48fb21c287ec81d61228e2_2_690x417.png)](https://forum.zenon.org/uploads/default/original/2X/1/1d096cb85792e2152f48fb21c287ec81d61228e2.png "image")

[romeo](https://forum.zenon.org/u/romeo) August 7, 2023, 12:56pm  125

Tried on testnet and had the same issue attempting the native connection, QR code worked again though

Can also confirm I utilized the main net bridge with the newest Syrius release and was successful all the way through

I’ve migrated alienc0der’s code with the recent v0.1.0 changes and created a [PR](https://github.com/zenon-network/syrius/pull/45) to get it merged in develop.

A release candidate will be made once all changes are approved and merged.
