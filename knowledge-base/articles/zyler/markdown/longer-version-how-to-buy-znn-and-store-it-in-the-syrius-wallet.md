Title: Longer Version: How to buy $ZNN and store it in the SYRIUS Wallet

URL Source: https://medium.com/@Zyler9985/longer-version-how-to-buy-znn-and-store-it-in-the-syrius-wallet-e197233ccb24

Published Time: 2023-06-20T09:50:50.794Z

Markdown Content:
[![Image 27: Zyler9985](https://miro.medium.com/v2/resize:fill:44:44/1*KaL4NYzSxXL6fDt1krksEA.png)](https://medium.com/@Zyler9985?source=post_page---byline--e197233ccb24--------------------------------)

This article is a step-by-step guide for how to buy $ZNN and store it in the SYRIUS wallet. It also contains tricks to get a better price (by avoiding front-running bots) as well as troubleshooting for initially setting up the SYRIUS wallet.

This guide is designed to be beginner-friendly with lots of pictures & screenshots as complicated language/assumptions of knowledge is a needless barrier to community growth. Let’s get started!

Disclaimer: This article is not financial advice and may contain speculation

![Image 28](https://miro.medium.com/v2/1*GaBJkhEmvr8cJiI4ZXI-Wg.jpeg)

Infrastructure peripheral to the Zenon Citadel.

## 1\. Install MetaMask

Metamask is a crypto wallet that lives in your browser. This step can actually be done with any web browser extension wallet that is compatible with Ethereum, but at time of writing Metamask is the most popular one. See the link below for their tutorial in setting it up:

## 2\. Send ETH to your MetaMask

Now send $ETH (Ethereum) to your MetaMask wallet address. **IMPORTANT**: Only send a **SMALL** amount to **TEST** the process. First you need to practice buying wZNN and getting it inside of SYRIUS. Only once you are confident with the whole process, then it is more appropriate to play around with larger amounts. That way if any mistakes are made, you only lose $10 and you can learn from it.

Your metamask should look like the screenshot below:

![Image 29](https://miro.medium.com/v2/resize:fit:700/1*dPP-wdP0g1LU_Q7UYQjy1g.png)

## 3\. Connect your MetaMask wallet to Uniswap

Uniswap is a DEX you can interact with using your metamask wallet. Beware of fake links/scammers. I like to just google it, click the first link which is [http://uniswap.org,](http://uniswap.org,/) click launch app, click get started and get to the swap screen. Click the top right button ‘connect’ and choose your metamask wallet from the list of options. If all goes well, you should see your ETH balance appear as a preview in the swap interface.

![Image 30](https://miro.medium.com/v2/resize:fit:700/1*d2jx3bmtiIsxgyhPNdtyvw.png)

## 4\. Find the “contract address” for wZNN

**NOTE**: You can actually **SKIP** this step by visiting the main site for Zenon. Visit “zenon.network” which you can find [here](https://zenon.network/). Scroll down to the part listing DEXs. Look for the uniswap icon and click “wZNN” and it should take you to the uniswap interface with the correct wZNN already loaded.

![Image 31](https://miro.medium.com/v2/resize:fit:700/1*XyQcJa1IdgHyxcFwhDhClg.png)

![Image 32](https://miro.medium.com/v2/resize:fit:700/1*Cwf1EABnVbsl6O6chrdraA.png)

Alternatively, you can find the ETH contract from coingecko or from etherscan or from this tweet from the official twitter. Make sure they are all consistent with one another. This contract is correct at the time of writing (June 2023). And don’t confuse it with a contract for a different chain such as the BNB Chain; so far we only have an Ethereum contract for wZNN.

![Image 33](https://miro.medium.com/v2/resize:fit:700/1*zL4SQknBApIyEwBX40EvMg.png)

![Image 34](https://miro.medium.com/v2/resize:fit:700/1*uZ3NMvjJ5rb2GfuVrklz2w.png)

![Image 35](https://miro.medium.com/v2/resize:fit:646/1*_rpVP9Mm6CBGU6P-xhgx7A.png)

## 5\. Optimise your settings and beat the bots

Before you buy, try to optimise your settings. Sometimes there are front-running bots. These bots will see you have placed a buy order, they will quickly buy before you can (increasing the price) forcing you to buy at a slightly higher price. The bots will then instantly sell, making a slight profit at the expense of you who has to buy at a higher price.

To defeat the bots, try a few things. Avoid Low liquidity pools, look for depth so it’s harder to move the price. Having your maximum slippage as low, which means you will only tolerate a small X% variation in expected return. 0.1% is quite low which is good, and 1% is perhaps the most you should do; but no hard rules for this. Also, try trading in smaller amounts throughout the day rather than one big buy. Perhaps just trade 0.1–0.5 ETH at a time. You can also pay a higher gas price for a faster transaction to decrease the chances of a bot beating you, so set a shorter transaction deadline. My go-to: 0.2 ETH at a time, 0.1% slippage, 30min Tx deadline.

More advanced things you can try is to use the Flashbots Protect RPC; instead of Ethereum mainnet use “Custom RPC” and use their design. Hides your Tx from mempool so bots can’t snipe it. Or you can use the MEV blocker as your Custom RPC.

![Image 36](https://miro.medium.com/v2/resize:fit:537/1*b9NbAtJCk-Jx3A8bBPiB9g.png)

## 6\. Swap your ETH into wZNN

Input the amount of ETH you wish to swap into wZNN. Click swap. Click confirm swap. Your metamask will have a popup in the top right of the screen; click confirm in this popup. It will then say transaction submitted. Once it’s done, a “swapped” message should popup.

Go back to the tab where you have your fullscreen metamask. At the bottom, click “import tokens”. Then instead of search, click “custom tokens” and paste the “contract address” and wZNN should come up. When we are bigger, you will be able to find wZNN by searching, but for now in early stages you need to do it this way. Go back to step 4 of this article if you forget how to get the “contract address”. And no, I will never stop quoting the “contract address”.

The balances of both ETH and wZNN should be there now in your metamask. Now we need to setup the SYRIUS wallet.

## 7\. Download the SYRIUS wallet and sync the node

Visit the main site ‘zenon.network’ and scroll to the bottom. Choose a desktop wallet. This tutorial is for Mac users. Download the SYRIUS desktop wallet app and move it to the applications folder. We are in the process of getting it listed on the App store; but for now you may have issues with opening it. You need to go to your settings app for your laptop, into security and privacy, and use your admin password to make an exception for SYRIUS and allow it to open/launch even though it is from “unknown developers”.

On launching it you will be prompted to create and store your seedphrase, create a password and so on. Very important is that you sync your node to be updated. You have two options: use your embedded node or use a public node. The public node will sync it very quickly/instantly. But the recommended option is to sync the embedded node; this means your computer will verify every transaction and will give you maximum privacy, control (your node your rules), and decentralisation. Only con is you will need to kill other applications and run it overnight, possibly for 24–48 hours. The IBD (initial block download) time may be reduced in the future via zerosync technology, but that is still a WIP.

Go to the settings icon, scroll down, choose embedded node and click confirm node. Leave the program running. Even if it times out and locks you out, it should still sync. You can leave it on overnight for example for 1–3 nights to get it synced and the circle will turn orange.

![Image 37](https://miro.medium.com/v2/resize:fit:700/1*VdTaWSQ2JwekoOTGVe1cYw.png)

## 8\. Visit the NoM Multichain Portal (it’s a bridge)

You need to get your wZNN into the SYRIUS wallet where it will become ZNN; it will be safer there and you can also start participating in the network and earning rewards once inside SYRIUS.

Keep your SYRIUS desktop wallet open and running. Also keep your MetaMask web browser extension wallet open and running.

Go to the “NoM Multichain” website. This is linked on the mainsite, but you can also use the link below:

Now follow the steps; the website will guide you through it. When it comes to “Web3 Wallet” or “WalletConnect” it is easier for beginners to go “WalletConnect” to gain permission from your desktop SYRIUS wallet.

Send your wZNN through the portal to become ZNN inside SYRIUS. This whole process works the same for wQSR to become QSR inside SYRIUS, but it will obviously need to use QSR’s ETH contract address.

## 9\. Consider using the affiliate marketing links

Fun fact! Once you are at this point, bridging wZNN from MetaMask into ZNN in SYRIUS is feeless. It is only bridging from native ZNN inside SYRIUS back to wZNN inside MetaMask which does require a small fee to be paid.

This fee is used for an affiliate marketing system, which supports ecosystem growth. To give an example of how this works: Each time a person leaves Zenon’s ecosystem, the 3% fee becomes embedded into the bridge contract. When someone else enters Zenon’s ecosystem via an affiliate link a marketer has generated, the buyer receives a 1% bonus and the marketer receives the other 2%. The 1% and 2% bonuses are supplied 1:1 by the 3% fee, making this a self-sustaining mechanism which also scales infinitely with price.

**TLDR**: Use the affiliate marketing links, you will be given **bonus ZNN** every time you buy. This is supplied by people being charged a small fee every time they leave the ecosystem (bridge from ZNN to wZNN).

**Thanks for reading. Get Zenonized and WAGMI!**

## Useful Links

See the [first article](https://medium.com/@Zyler9985/zenon-network-i-the-green-pill-883e608727a) in the series
[The Main Site](https://zenon.network/) as well as a [Buying/SYRIUS Wallet Tutorial](https://medium.com/@Zyler9985/zenon-network-how-to-buy-znn-and-store-it-in-the-syrius-wallet-65a8f3ced4db)
[The Official Twitter](https://twitter.com/Zenon_Network) and a [Community Twitter](https://twitter.com/Learn_Zenon)
[Discord](https://discord.com/invite/zenonnetwork) and [Telegram](https://t.me/zenonnetwork)
The Dev Forums [here](https://forum.zenon.org/) and [here](https://forum.hypercore.one/)
To find work in the ecosystem and get paid by the on-chain funding mechanism see [here](https://www.zenon.org/funding/programs/accelerator-z?_gl=1*u6tjom*_ga*MzQ0OTU3Njk3LjE2NTA3MDcyMzk.*_ga_M2F8KJ59YQ*MTY4NzAwNDg3OC4xNDM5LjEuMTY4NzAwNTI1OS4wLjAuMA..#purpose) and to see what’s already been funded see [here](https://zenon.tools/accelerator)
