Thread: steps-to-troubleshoot-the-wznn-znn-bridge
0x3639 | 2023-12-02 00:33:35 UTC | #1

The process to bridge assets from $ZNN => $wZNN or $wZNN => $ZNN should take about one hour with all the security measures in place.  If you are "stuck" on "1/2" or "estimating" here are the steps you should take.  These messages should appear for up to 20 minutes each.  

1) Make sure Metamask is updated. Metamask had a bug they fixed here: https://github.com/MetaMask/metamask-extension/issues/20847

How to update metamask extension here: https://community.brave.com/t/how-to-get-chrome-extension-up-to-date/43177/2

2) Make sure to only interact with the bridge on Google Chrome. After updating Metamask close Chrome. 

Brave has a function called "Shields are UP".  This will prevent the Bridge from working correctly.  

![Screenshot 2023-11-18 at 4.33.52 PM|690x250](upload://d0nQbjE1INWdTBoEqaBZdNVjEzQ.png)

3) We are finding that several extension can block access to the bridge.  If you cannot trouble shoot that yourself, put Google Chrome into 'incognito" to interact with the bridge site.  That will clear your cache and disable plugins that might prevent access to the bridge.

4) Make sure extensions are enabled in Google Chrome incognito.  Only enable Metamask. 

5) In Chrome: Right click > Inspect Element > Application tab > Storage > Clear site data

6) Go into SYRIUS and remove any existing connection under Wallet Connect.

7) Navigate to the bridge https://bridge.mainnet.zenon.community/ and connect both wallets (SYRIUS and Metamask).  Make sure you are incognito.

---

If you want to see your actual TX status in the bridge follow these steps.

- Wrap Requests (znn > wznn) Go to Zenon Hub and check your [Wrap Request](https://zenonhub.io/tools/api-playground?address__request=Bridge.getAllWrapTokenRequestsByToAddress&request=Bridge.getAllWrapTokenRequestsByToAddress).  Provide your 0x Ethereum address and submit.
- Unwrap Requests (wznn > znn) Go to Zenon Hub and check your [Unwrap Request](https://zenonhub.io/tools/api-playground?address__request=Bridge.getAllWrapTokenRequestsByToAddress&request=Bridge.getAllUnwrapTokenRequestsByToAddress).  Provide your ZTS address (Zenon Address) and submit.

-------------------------

0x3639 | 2024-12-25 18:16:52 UTC | #2

## [Issue](https://github.com/DexterLabZ/bridge.mainnet.zenon.community/issues/17): Wallet Connection between syrius and bridge GUI fails if you change wallet address after making a WC connection.

## Resolution

* Cancel existing WalletConnection in syrius.  (If you skip this this step the instructions will NOT work)

You will see it in the WalletConnection paring list.  There will be a red "X" on the right side to terminate the connection.  Terminate all connections.  If there are no connections, that is OK.  Proceed to the next step.  

![Screenshot 2024-12-25 at 7.22.13 AM|690x423](upload://bXugT6Fue7GQlScuKiQh5vbYuuL.jpeg)

* Close the syrius wallet software
* Cancel any existing connections to WalletConnect on the Bridge website.  Click the red X below.  

![Screenshot 2024-12-25 at 7.31.50 AM|587x500](upload://pqMNGarZGyNQFiwj7b0sqkqaVnO.jpeg)

* While on the [bridge website](https://bridge.mainnet.zenon.community/) > clear cache in browser > Right click on the page > Inspect Element > Application tab > Storage > Clear site data

![Screenshot 2024-12-25 at 7.24.40 AM|645x500](upload://1Tvh0wWssz626P8pbJUKODqbIa9.jpeg)

![Screenshot 2024-12-25 at 7.25.46 AM|690x275](upload://8h8OE5FoKqEJq4rKVz0bCJX382F.png)

* Close (quit in mac) the browser
* Open the syrius desktop software and login
* Open the browser (Google Chrome) and navigate to the [bridge](https://bridge.mainnet.zenon.community/) website
* Connect syrius to bridge website per the How to Video below.  The video starts 46 seconds into the instructions.  

https://youtu.be/Ui2x1IECwys?si=wE2WYFoFzoFM073o&t=46

-------------------------

