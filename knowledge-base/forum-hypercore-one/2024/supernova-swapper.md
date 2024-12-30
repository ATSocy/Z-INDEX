Thread: supernova-swapper
aliencoder | 2024-06-13 17:08:39 UTC | #1

Ideally we need a way for users to swap between `wZNN` and `xZNN` from their Web3 wallets directly, without having to go through a lengthy process involving the Syrius wallet and without having to connect to any bridges.

Since the addresses are the same for both `wZNN` and `xZNN` (same private key), the user could just send for example the `wZNN` using only Metamask to the bridge address and have them magically appear as `xZNN` on Supernova.

This frictionless swap process will boost adoption for the Supernova EVM extension-chain and at the same time will unlock a lot of interesting use-cases for `wZNN` holders.

-------------------------

Bzed | 2024-06-17 16:22:51 UTC | #2

Very nice, simpler the better. Thank you.

-------------------------

Stark | 2024-11-25 15:53:15 UTC | #3

Bringing this back to the top, for awareness. Coming zoon.

-------------------------

MoonBaze | 2024-11-26 15:11:27 UTC | #4

Hello!

I have come up with an implementation for this problem. There will be a system that allows fast zwapping between bridged EVM networks (Ethereum, Supernova).

It is very simple for the end user: they just have to send wZNN / xZNN to the zwapper address on the source network and they will receive the amount minus some fees in the same address on the destination network. There is no need for a complex web interface, just a telegram bot that will offer the required information about each network.

For example, swapping from Ethereum to Supernova. The user will chat with the bot, let's say issue "status" command. The bot will print how many ZNN is on every network. If the Supernova smart contract (destination network) holds 3000 xZNN, the user will be able to swap up to 3000 instantly by just sending the wZNN token to the Ethereum zwapper smart contract address. Otherwise, a fund re-balancing is required, meaning some funds from a network must be unwrapped to NoM and then wrapped to Supernova. 

The are some constraints:

* Each transfer will require a small confirmation time on the source network, a few blocks, after which, the calculated amount will be sent on the destination network.

* An administration fee of about 1% (or more, depending on operational costs) will be deducted from the resulted amount, meaning that zwapping 100 ZNN will result in 99 ZNN on the destination network.

* The fees that will be spent on the destination network in order to make the pay transaction, will be deducted from the amount, calculated based on the price of the token at that time. 
For example, zwapping 100 wZNN from ETH to Supernova, will require to pay a transaction fee on Supernova. If the gas price of the transaction fees is 0.01$ and ZNN price is 1$ on the AMM smart contract, then 0.01 ZNN will be deducted from the amount and the recipient will receive 98.99 xZNN ( 100 - 1 - 0.01).

I will use some of my own funds in the beginning,  but the volume will be low at first because I will have to re-balance the funds often. Of course, a back-end will do it, and the re-balancing will be bundled, not very every zwap amount.

I hope that I will finish the bot this week but wanted to get more feedback from you: should I apply for Accelerator to get some seed funds? This system needs to re-balance funds between networks very often, meaning I have to unwrap to NoM and then wrap and redeem on the destination network each time the smart contract on a network runs out of funds. In this scenario, the zwaps will take more time until funds are available again, otherwise, ~ 1 minute.

https://github.com/MoonBaZZe/zwapper

-------------------------

0x3639 | 2024-11-27 16:59:32 UTC | #5

I want to make sure I understand this.  It looks like this is not a mint / burn bridge.  It's a wallet with xZNN and wZNN?  The bot looks for changes in balances of either asset type and does the exchange from balances in its own wallets.  

Is that correct?  How do you get xZNN in the wallet?

-------------------------

coinselor | 2024-11-28 13:58:28 UTC | #6

I think it's a couple smart contracts on each chain + a rebalancing backend that makes sure the funds get evenly spread out. I assume the rebalancing just uses the wrap/unwrap features of the birdge to go through NoM from one chain to the other.

I support this initiative, it'll come in handy as we deploy more stuff on Supernova to onboard users. 

Only issue I see is zwapper fee not being able to cover for ETH fee spikes.

-------------------------

