Thread: az-cex-integration-xeggex-and-mercatox
0x3639 | 2024-03-08 13:45:58 UTC | #1

We are currently working on two CEX integrations:

1) Xeggex
2) Mercatox

I've paid the $2500 USDT listing fee for Xeggex.  I'm working with them now to facilitate the integration and setup. 

![telegram-cloud-photo-size-4-6001370967231807056-x|486x331](upload://6OqluNPJr2rtkIqSEQuMvEVAgxf.jpeg)

Mercatox has agreed to list wZNN and trade it on their platform.  They hold 20600 native ZNN today (it was swapped from Alpha Net) and it is owned by the community.  In order to activate trading they need to move this to wZNN and incur the 3% bridge tax.  [The community voted](https://forum.zenon.org/t/open-letter-to-mercatox/1332/18?u=0x3639) and agreed to pay this fee 618 wZNN.  To get 618 wZNN we need (637 ZNN x .97) = 618 wZNN.

@sugoibtc asked if Mercatox would list native ZNN and they said they would consider it if we could provide an integration guide.  

![Screenshot 2024-03-06 at 11.36.06 AM|690x446](upload://yXaW8X0tyYDPdfvbCmCnEwBCj50.jpeg)

I will prepare a [CEX Integration Guide](https://forum.hypercore.one/t/cex-integration-guide/380) and it will look something like [this]( https://docs.optimism.io/builders/cex-wallet-developers/cex-support) but more elaborate.  It will include a node setup guild, CLI instructions and answers to questions all CEXs will have. We can strive to improve over time like the [Sol guide](https://solana.com/docs/more/exchange), but I don't think this level is necessary right now. I will post the guide to the HC1 forum and anyone can repurpose it and/or repost it in any form.  

I'm adding another example CEX listing guide example:
- https://wiki.alephium.org/integration/exchange/
- https://docs.ergoplatform.com/node/swagger/
- https://docs.dero.io/Developers/rpcapi
- https://dynexcoin.org/learn/guide-dynex-walletd-rpc

**Total Cost of Integration**
Xeggex Listing fee = 1,786 ZNN ($2,500 / 1.4)
Mercatox Reimbursement = 637 ZNN (converts to 618 wZNN)
ETH Fees = 14 ZNN ($20 / 1.4)
Integration Guide and Coordination for 2 CEXs = 750 ZNN
QSR AZ Minimum = 100 QSR

Total Cost = 3,187 ZNN + 100 QSR

## Update

We might need to create an API wrapper for the DART / C Sharp SDK that performs these functions, at a minimum.  We might also need to create the ability to manage plasma or PoW.  I'm discussing this with @CryptoFish and XeggeX and this AZ does NOT include this work.  
```
getNewAddress: 
validateAddress: 
getFeeEstimate:
sendTransaction:
receiveTransaction:
```

---
[poll type=regular results=always public=true chartType=bar]
* Yes I support this AZ
* No I do NOT support this AZ
[/poll]

-------------------------

VTO | 2024-03-06 21:44:07 UTC | #2

Listing on Xeggex is perfect !! but what is the benefit of listing wZNN on Mercatox if we have a bridge for it? they're only offering it to us for the fee? We need to reach the mass of ordinary users, not another several  "geeks" who likes to make xy steps to get native ZNN to their wallet..

Sugoi, romeo, coinsellor and others also asked this question on zenon.org forum, but without any answer..

-------------------------

0x3639 | 2024-03-06 22:29:00 UTC | #3

Good question.  @sugoibtc reminded me they will consider a native integration but want to see our Integration Guide.  Based on the feedback above I will submit an AZ and hopefully start working on it.

-------------------------

0x3639 | 2024-03-06 22:32:15 UTC | #4

Please note this update to the post above

![image|690x246](upload://eMh3X4Exc8wST3CfGqtYx4IsE1d.png)

-------------------------

Blueginger | 2024-03-07 06:02:08 UTC | #6

I support this. 
This requirement could be easily met with donations.

-------------------------

coinselor | 2024-03-07 11:11:20 UTC | #7

We are in the process of setting up a community multisig for the CEX fundraiser. If we are able to raise funds before the AZ phase payout, we can send the equivalent to the CEX listing fees to @0x3639. If we do not beat AZ to it, we can donate the same amount back to the AZ fund.

-------------------------

