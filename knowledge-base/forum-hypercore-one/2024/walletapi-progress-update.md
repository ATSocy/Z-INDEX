Thread: walletapi-progress-update
0x3639 | 2024-04-03 00:30:55 UTC | #1

A few people have asked about the walletAPI.  This post will share a quick update.
@CryptoFish and I have been working with [XeggeX](https://xeggex.com/) to develop a wallet API app that CEXs can use to help them manage ZTS assets on their exchange.  We currently have the following endpoints (images).  These include everything that XeggeX has asked for.  

This walletAPI is designed to be run within the CEX's private infrastructure.  It should never be exposed to the public.  There is one wallet and each user will have their own accountIndex.  The CEX can use local QSR to fuse to each address OR use the Plasma Bot at ZenonHub.io.  There are basic send and receive functions, fuse / unfuse plasma, and various ledger options.  In addition, the CEX has the ability to add and remove addresses to an auto receive function so the wallet receives TXs automatically.  Finally, there is DOS protection if someone sends many small TXs to a wallet address.   

The wallet will have a simple User ID and Password to establish a secure connection to the wallet.  This UI could be expanded in the future to setup multiple users with privileges. 

The goal is to have this wallet ready for production in April.  

![Screenshot 2024-04-02 at 7.05.24 PM|690x236](upload://8P2sW3bSzCd11q2GppH2eogO7Nc.png)
![Screenshot 2024-04-02 at 7.05.37 PM|690x209](upload://1GqUQQjsuW5Qox8Sx19OxwYz3i0.png)
![Screenshot 2024-04-02 at 7.05.45 PM|690x179](upload://pGEEUbzTcxWW5p1IThfc2Czu8ha.png)

-------------------------

