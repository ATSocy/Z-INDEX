Thread: wallet-connect-1-0-customer-notification
0x3639 | 2023-10-03 18:07:50 UTC | #1

I received the following email from Wallet Connect.  Wanted to share with the devs here.

Hello,

In June, we shut down WalletConnect v1.0, the culmination of a months-long migration to WalletConnect v2.0. This was an enormous moment for not just WalletConnect but the web3 ecosystem, because WalletConnect v2.0 enables a more reliable and faster end-user experience — and also brought an end to chain switching.

To achieve this, WalletConnect v2.0 exposes a developer-friendly abstraction called “[namespaces](https://lqblze.clicks.mlsend.com/te/cl/eyJ2Ijoie1wiYVwiOjE2NDQ4NyxcImxcIjoxMDEwMzY3ODMxMDMzNzk0MDIsXCJyXCI6MTAxMDM2ODEzNjU5OTMyNDU0fSIsInMiOiI5MTdhODBkYmVjMTc5YTI4In0)”, designed in accordance with [CAIP-25](https://lqblze.clicks.mlsend.com/te/cl/eyJ2Ijoie1wiYVwiOjE2NDQ4NyxcImxcIjoxMDEwMzY3ODMxMDg2MjIyODMsXCJyXCI6MTAxMDM2ODEzNjU5OTMyNDU0fSIsInMiOiIxYTNhOTNiNDdlMTc3NDc4In0). During the migration, many apps opted to *require* all of the most critical chains, methods, and events **at first connection** (i.e. required namespaces), leaving others as optional for end user flexibility (i.e. optional namespaces).

While this implementation works well for many wallets, it creates challenges for others. This includes smart contract wallets like Safe as well as non-smart contract wallets that also run on only one chain at a time as a matter of design.

To resolve this issue, we are asking all wallets, both smart contract wallets and others, to test your wallet and upgrade, if need be, so that your wallet can handle all possible namespace scenarios that apps may support.

Given the urgency of the matter, we are asking that you test your ability to support namespaces **by October 18, 2023** so that we can commence our app outreach and ensure that seamless connection can be enjoyed by all. The test itself takes no longer than a few minutes (if that) and there are details below; if subsequent action is required, you will only need to perform a simple update to your Web3Wallet SDK. Should you have any questions or concerns, reach out to us at [devrel@walletconnect.com](mailto:devrel@walletconnect.com).

We recognize the ask involved and take full ownership of the impact caused by the original implementation of namespaces, which overlooked the lift required by certain wallets, in particular smart contract-based ones. We thank WalletConnect users for bringing it to our attention, and we appreciate your patience as we’ve worked to resolve this.

While the above deadline is **not** a hard deadline, we hope you can complete the steps below as soon as possible. It’s a quick and easy test that goes a long way in ensuring a reliable and first-class connection experience for your wallet’s users.

How to ensure your wallet supports namespaces

To see if your wallet can connect to apps that have empty or undefined required namespaces, simply connect your wallet to our example app here: [https://se-sdk-dapp.vercel.app/](https://lqblze.clicks.mlsend.com/te/cl/eyJ2Ijoie1wiYVwiOjE2NDQ4NyxcImxcIjoxMDEwMzY3ODMxMTQ5MTM3NDAsXCJyXCI6MTAxMDM2ODEzNjU5OTMyNDU0fSIsInMiOiI3YWNlMDBjZTdlZTkzY2Q2In0).

**If you can connect**, it is a good indicator that your wallet correctly supports namespaces. Hooray - there’s nothing for you to do!

**If you can’t connect**, we recommend updating your wallet as soon as possible by doing the following.

* Ensure you are leveraging our[ namespace builder util tool](https://lqblze.clicks.mlsend.com/te/cl/eyJ2Ijoie1wiYVwiOjE2NDQ4NyxcImxcIjoxMDEwMzY3ODMxMTgwNTk0NjksXCJyXCI6MTAxMDM2ODEzNjU5OTMyNDU0fSIsInMiOiIwZjhhYTkwZTk2ZDJjNjY4In0) (and the latest Web3Wallet SDK version) which does namespace parsing for you, allowing your wallet to handle all possible namespace scenarios that apps may have as supported by [CAIP-25](https://lqblze.clicks.mlsend.com/te/cl/eyJ2Ijoie1wiYVwiOjE2NDQ4NyxcImxcIjoxMDEwMzY3ODMxMjMzMDIzNTAsXCJyXCI6MTAxMDM2ODEzNjU5OTMyNDU0fSIsInMiOiJiMDIwNmFjNDhiYTkyNWY2In0).

Web3Wallet SDK latest versions

Swift: 1.8.6

Kotlin: BOM-1.17.0

JavaScript: ^1.9.1

If you choose not to leverage our namespace builder (not recommended) or if it is not available on your platform of choice, ensure at a minimum that your wallet can handle the following common usage patterns:

Case #1 - **Recommended default for all apps**

* requiredNamespace is empty / undefined
* optionalNamespace is defined

Case #2

* requiredNamespace is defined
* optionalNamespace is defined

Case #3

* requiredNamespace is defined
* optionalNamespace is empty / undefined

Case #4

* requiredNamespace is empty / undefined
* optionalNamespace is empty / undefined

And that's it!

If you require technical support along the way, please drop a message on the [WalletConnect GitHub](https://lqblze.clicks.mlsend.com/te/cl/eyJ2Ijoie1wiYVwiOjE2NDQ4NyxcImxcIjoxMDEwMzY3ODMxMjk1OTM4MDcsXCJyXCI6MTAxMDM2ODEzNjU5OTMyNDU0fSIsInMiOiJlZmY5ZTQzYzBkMzVhYjlhIn0) and our team will get back to you as soon as possible.

We want to thank you once again for your patience and support throughout these past few months. Thanks to your cooperation, we can improve web3 experiences for users everywhere.

-------------------------

sol | 2023-10-03 20:38:04 UTC | #2

I believe Syrius supports WC v2 and [namespaces](https://github.com/zenon-network/syrius/blob/master/lib/services/wallet_connect_service.dart#L400).

I've also been testing Syrius WC with WalletConnect v2 reference material, no issues so far.

-------------------------

aliencoder | 2023-10-19 20:42:36 UTC | #3

[quote="sol, post:2, topic:219"]
no issues so far.
[/quote]

Music to my ears.

-------------------------

