Thread: s-y-r-i-u-s-chrome-extension-improvements
coinselor | 2023-04-30 16:28:29 UTC | #1

I've been using Dexter's chrome extension to test NoM multichain. I'd like to compile a list of improvements in this thread for easier access, eventually moving them to the Mattermost board.

Improvements:

 - QoL: See if we can increase the speed of animations to make it feel more snappy.
- Bug: unlock screen flashing unnecessarily when wallet is already unlocked.


After wallet is unlocked and the popup for transaction approval appears:

- QoL: Disable intro animation
- Bug: unlock screen flashes for a second before the approval screen shows up
- QoL: if possible, consolidate both the 'approval' and 'granted access' screens under a single window, to avoid the unnecessary 'Done' after approving the tx.

-------------------------

sol | 2023-03-31 18:54:57 UTC | #2

A couple improvements:
- Chrome: Manifest v3 support
  >Manifest version 2 is deprecated, and support will be removed in 2023. See https://developer.chrome.com/blog/mv2-transition/ for more details.
- Firefox support
   - The extension actually loads in FF but the animations are choppy and some testnet data won't load

-------------------------

ZNNAYIID | 2023-04-01 01:06:02 UTC | #3

I’ve already sent my feedback to dexznnter back when he first released the extension, but still has the same issues.. don’t forget that people will use this extension to interact with the new trustless bridge.
I also have a prototype for a redesigned extension, we just need someone to implement it.

-------------------------

coinselor | 2023-04-01 14:28:21 UTC | #4

Feel free also to add the feedback here. The idea is to consolidate all the feedback in a single place. Anyone willing and capable to help fix some of these issues would have an easier time doing so.

-------------------------

aliencoder | 2023-04-01 20:16:00 UTC | #5

[quote="sol, post:2, topic:1342"]
* > Manifest version 2 is deprecated, and support will be removed in 2023. See [The transition of Chrome extensions to Manifest V3 - Chrome Developers](https://developer.chrome.com/blog/mv2-transition/) for more details.
[/quote]

Harder than you think. Tried to get it working with Manifest V3 without success.

[quote="ZNNAYIID, post:3, topic:1342"]
I also have a prototype for a redesigned extension
[/quote]

Can you post the link over here?

-------------------------

ZNNAYIID | 2023-04-02 02:02:01 UTC | #6

https://www.figma.com/file/UvTkW8Gb1wxra4ZdMMvYUk/S-Y-R-I-U-S--Extension-Wallet

It still needs some polishing, but I stopped working on it since the dev didn’t show any interests in updating the extension.

-------------------------

aliencoder | 2023-04-02 09:01:24 UTC | #7

Looks very similar to the Mobile App design. And that's just awesome. Amazing work! 

Do you have a Github account? I'll reach out @dexter703 , but if you have an account, please ping him over there. I'll keep you updated.

-------------------------

ZNNAYIID | 2023-04-02 12:20:51 UTC | #8

Yes, I tried to have a similar ui to the mobile app with a similar ux to the other known wallet extensions, so anyone can use it flawlessly and without getting confused. 
Just reach out to him, I’m personally done with asking him every time lol

-------------------------

coinselor | 2023-04-03 22:20:22 UTC | #9

Amazing, I remember looking at it but I think you added a lot more since the last time I checked. I assume there are a lot more screens/flows that are not even implemented in the current version of the chrome extension. We should look to update the look and feel of what's there, to gradually implement the other screens to rich parity with syrius mobile/desktop.

I'll be curious to know what's metamask/chrome extension wallets market share and how it's trending. There seems to be a growing trend towards mobile wallets (trust wallet, the upcoming uniswap wallet, etc...). We'll need to have a capable chrome extension anyway, but with syrius desktop/mobile + wallet connect, it might be smart to look at the data. We should prioritize support/fixing bugs of whatever has more marketshare/growing potential.

-------------------------

0x3639 | 2023-04-04 18:56:26 UTC | #10

wow I did not realize you provided a complete design.  this looks awesome!

-------------------------

romeo | 2023-04-04 21:27:56 UTC | #11

Looks awesome, great consistency across efforts

-------------------------

mehowbrainz | 2023-04-30 16:28:18 UTC | #12

Congrats on the project. I will temporarily move it to #development:funding-staging and once you submit it on-chain we will move it back to #development:funding-submissions.

-------------------------

