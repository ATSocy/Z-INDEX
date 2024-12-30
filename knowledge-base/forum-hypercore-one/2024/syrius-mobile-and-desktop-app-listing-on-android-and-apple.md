Thread: syrius-mobile-and-desktop-app-listing-on-android-and-apple
0x3639 | 2024-06-02 19:49:33 UTC | #1

I've completed the process to register an apple developer account and google play developer account.  We are going to start the process to [notarize](https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution) the syrius desktop code to prevent the security warnings that require manual override.  

In addition we are going to work towards listing the Syrius Mobile App:
* [Google AppStore](https://play.google.com/console/about/storelistings/)
* [Mac AppStore ](https://developer.apple.com/macos/submit/)

I will use this post to coordinate that effort.  It will require participation from the community.  We need to develop a website and offer support for the wallet.  I'm not sure sure yet which website can be associated with the wallet.  I acquired syriuswallet.com and hope we can use that.  I've disclosed to Apple and Google this is a non-commercial app with no intent to market, sell or generate fees from its use.  

If you have any questions or comments please do so below.  I'll update the post as I start the process to list the mobile wallet.

Check out the [Trust Wallet Apple Store](https://apps.apple.com/us/app/trust-crypto-bitcoin-wallet/id1288339409) presence.

## Useful Links for Reference
- Trust Wallet [Support Link](https://community.trustwallet.com/c/helpcenter/8)
- Trust Wallet [Website Link](https://trustwallet.com/)
![Screenshot 2024-06-02 at 2.48.29 PM|690x84](upload://ybxyTKNT7J8ih9jsbNsPl0kIHsF.png)

-------------------------

Stark | 2024-06-03 02:31:12 UTC | #2

This very exciting and a HUGE leap leap forward for onboard new network participants. Thank you for taking this on and please let me know if there is anything I can do to help out.

-------------------------

aliencoder | 2024-06-03 17:08:54 UTC | #3

We need to prepare the following:

- Website for the mobile app
- Support page (TrustWallet has a dedicated [forum](https://community.trustwallet.com/c/helpcenter/8))
- Localizations and graphic assets

-------------------------

0x3639 | 2024-06-03 19:23:27 UTC | #4

I have syriuswallet.com  

Was thinking about a next.js website - something like this https://vercel.com/templates/next.js/nextjs-enterprise-boilerplate  We will need a website dev and graphic designer to help out.  

We can setup a forum or helpdesk on zendesk or zoho.  I have experience with all of them.  A dedicated forum could be easiest for multiple community members to help out with.  Zendesk is expensive per user.  Zoho is cheaper.

-------------------------

0x3639 | 2024-06-03 19:27:30 UTC | #5

![image|663x500](upload://4b1vysoegkfU07SPasQPOArWjq6.png)

Example discourse support forum.  https://discourse.stonehearth.net/

Might be easier and cheaper to start with an open forum where multiple people could pitch in and make it 100% focused on syrius wallet support.

-------------------------

0x3639 | 2024-06-03 19:41:33 UTC | #6

We are going to start researching mobile wallet websites we like.  If anyone finds one they like please share it below.  Also, here are some next.js templates we can start from.  Enterprise Boilerplate looks like an OK start but feel free to propose something else.  

https://vercel.com/templates/next.js

-------------------------

Stark | 2024-06-04 02:58:43 UTC | #7

I like that Kaspium has a very simple appearance and uses a dark theme. I think that it would be good to include 3-4 sections on the front page to inspire confidence and a professional impression.

Here's some copy to work with.
<h1>1. Secure Your Digital Life.</h1>

* **Headline:** Your Gateway to Web3
* **Body Text:** 
Syrius Wallet offers industry-leading security features, including private key control and biometric authentication, to keep your holdings safe. 

<h1>2. Designed for Everyone.</h1>

* **Headline:** Intuitive and Secure. 
* **Body Text:** 
Whether you're a seasoned crypto enthusiast or just starting your Web3 journey, Syrius Wallet is designed for you. The intuitive interface makes it easy to navigate, while robust features empower you to take control of your digital assets.

<h1>3. Built for the Zenon Network.</h1>

* **Headline:** Optimized for Convenience and Speed.
* **Body Text:** 
Experience the full potential of the Zenon Network with the Syrius Wallet. The app is specifically designed to leverage Zenon's fast transaction processing and advanced security features, providing a seamless and optimized user experience.

<h1>4. New Features on the Horizon.</h1>

* **Headline:** Constantly Improving to Meet Your Needs.
* **Body Text:** 
The Syrius team is dedicated to continuous development. Stay tuned for exciting new features and integrations that will further expand the capabilities of your Syrius Wallet and empower you to explore the ever-evolving Web3 landscape.

<h2>4.1. Manage Your NFTs with Ease.</h2>

* **Headline:** Showcase and Manage Your NFT Collection with Syrius Wallet.
* **Body Text:** 
Securely store, view, and transfer your NFTs with a user-friendly interface. Keep track of your growing collection and interact with NFT marketplaces directly from the app.

<h2>4.2. Unlocking the Power of DeFi.</h2>

* **Headline:** Invest, Earn, and Trade.
* **Body Text:** 
Syrius Wallet is built to seamlessly integrates with Decentralized Finance (DeFi) protocols. Effortlessly access DeFi applications to earn interest on your crypto, swap tokens, and participate in innovative financial services directly from your mobile app.

<h1>5. Download Now.</h2>

* **Headline:** Unlock a Realm of Infinite Possibilities. 
* **Body Text:** 
Start your journey into Web3 with Syrius Wallet. Download the app now and experience a secure, user-friendly platform to manage your digital assets and explore your potential in the Zenon Network.

-------------------------

Stark | 2024-06-04 03:05:57 UTC | #8

![home|266x499](upload://cA1wgFkLFG3vxkVImceuzDdCxe3.png)

-------------------------

0x3639 | 2024-06-05 09:35:09 UTC | #9

Latest thinking on the website (syriuswallet.com) and support forum based on discussions with @digitalSloth.  

UI Kit
[https://preline.co](https://preline.co/)

Template
https://vercel.com/templates/next.js/nextjs-boilerplate

Support Forum Example
https://community.trustwallet.com/

We can incorporate an AI Bot also
https://meta.discourse.org/t/discourse-chatbot-now-smarter-than-chatgpt/256652

Hosting Framework
https://coolify.io/

[Coolify 101](https://www.youtube.com/watch?v=taJlPG82Ucw) How to Video

Example Wallet Sites:
https://trustwallet.com/
https://phantom.app/

Just want to make sure everyone knows this will turn into an AZ and I hope we can engage as much of the community as possible.  The community can help with support articles: FAQs, How to, and Troubleshooting.  And anyone who engages in design, development, testing, content, graphics, etc.. can expect to be included in the AZ.  I hope we can get a lot of people involved in this.  

If you want to engage start thinking about FAQs and How To articles we can write.

-------------------------

jovi | 2024-06-04 15:27:36 UTC | #10

@0x3639 thank you for the invitation. I have a problem uploading the video: Sorry, new users can not upload attachments.

-------------------------

0x3639 | 2024-06-04 15:54:42 UTC | #11

[quote="jovi, post:10, topic:468"]
new users
[/quote]

I just updated your status.  Can you please try again?

-------------------------

0x3639 | 2024-06-04 16:11:03 UTC | #12

I just increased the size.  If that does not work maybe share via DM with a link from a free hosting service and I can upload to DO spaces and share the link here.  That is how we shared the Mobile Wallet in the past.  

![Screenshot 2024-06-04 at 11.09.22 AM|690x233](upload://tDqW2AiS2SyC8Bl9q6q4ZqQzSU8.png)

-------------------------

jovi | 2024-06-04 21:45:44 UTC | #13

Thank you @0x3639!

A sneek peek of the presentation video:

![star_s|video](upload://xsMIzzswLvk8QCLnfjzGv6VLQDx.mp4)

If you like my work, I will apply for AZ grant. First phase can include the logo and mobile app showcase graphics. Next phase can include the presentation video for the mobile wallet. And I can continue delivering custom graphics and other materials in the future.

-------------------------

0x3639 | 2024-06-04 23:08:18 UTC | #14

I think your work is great.  It would be nice to get @Dr.GreenThumb involved too.  His video animations are awesome!!  Check out a sample here: https://hypercore.nyc3.digitaloceanspaces.com/video/YouCut_20230321_101505605.mp4

We can either include your work in the syriuswallet.com AZ or you can apply separately.  It's up to you.

-------------------------

Stark | 2024-06-05 15:04:57 UTC | #15

This an awesome design concept. Can you create the text as "s y r i u s" ?

Do you think you could use this to develop an animated variation of the logo?

Love your work.

-------------------------

coinselor | 2024-06-06 19:22:54 UTC | #16

That's a lovely reveal for the icon. Good job!

-------------------------

