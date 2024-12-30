Thread: telegram-plasma-bot-improvements
alien-valley.io | 2023-02-08 22:34:57 UTC | #1

**Project Name:** Telegram Plasma Bot Improvements

**URL:** [GitHub code](https://github.com/alien-valley/plasma-bot) & [Telegram bot](https://t.me/alien_valley_plasma_bot)

**Description:** The Telegram Plasma Bot is a telegram channel where users can send their Zenon address and plasma will be fused to it. It has helped over 400 users as of now to have a better time in the ZNN ecosystem. We want to update the experience for the users & allow other donors to participate as well, in an open scenario. The end goal would be allow any participant to become a bot-operator, thus decentralizating the whole process. The process will be open source and it'll serve as a great example & starting ground for future projects. 

*This projects seeks ZNN to incentivise the development of the Plasma Bot. We split it into 2 projects in order to streamline & keep simple the AZ process.* 

**Team:** The Alien Valley team has been running & funding the Plasma Bot for some time. We think that the fact that we are a proud builder pillar should encourage others to trust us with this endeavour. 

> > Improvements

The Plasma Bot is an existing product, which already helps 400 users. All these improvements will make the overall product better, more scalable & decentralised.

> Codebase

At the moment the application interacts with the Zenon CLI to communicate with the Zenon Network. Making the plasma bot a native JS App, which uses the znn.js SDK, instead of calling the CLI, will serve as a great example of Telegram + Zenon native app for future developers.
The documentation & codebase will cover:
- how to make a telegram bot in JS
- how to interact with the Zenon network in JS
- how to keep a local state deduced from the NoM

> User Experience
* Give each Telegram User a virtual wallet containing 50 QSR
* can fuse do all the operations as if the QSR was theirs*
  * when talking about fuse operations
  * they can't send the QSR to other accounts
* can select where to fuse the QSR & how much 
  * ex: 20 QSR to z1qq, 10 QSR to z1pq and 10 QSR to z1pp
  * or 50 QSR to z1qq 
* can cancel existing fuse entries (if older than 10 hours - to respect protocol rules)

> Capital Efficiency

When the system will run out of QSR, it'll start to cancel **the oldest entries**
* it's possible that all entries are non-cancelable - that's bad luck
* if a user will have it's entry canceled they can re-do it, canceling another one and so on
  * this will not result in a chain reaction since users are not active 24/H
* users will receive a notification when their fuse entry was canceled 
  * can be turned off
  * useful to not encounter scenarios like 
  * what happened 
  * why it's not working anymore
  * RUGPULL

> Donations

This feature will allow anyone to put to use their idle QSR, if they want. The'll essentially send their QSR to a **Bot Operator** and the operator will use the QSR to fuse incoming requests.

- each user can request a unique deposit address from a bot-operator
  - similar to how a CEX operates
  - QSR will be send to that address & that address only
- the address requires to have 50 QSR fused to it beforehand
  - this must be done by the donor
  - not having the QSR will not enable a receive TX & future fuse transactions
- the funds will not leave the wallet
  - **does not happen in CEX scenarios**
  - they will not be send to a 'cold wallet' or similar
  - the bot operator will only do fuse entries from that address
- the owner can force the pillar to stop any future fuse operations from this address
  - this means that in **at most 10 hours** all fuse entries can be canceled 
- only the owner can operate the address
  - can withdraw any funds from it (QSR & other ZTS if people donated to it)
  - can force-cancel all active fuse entries

> Marketplace

Add a new layer between the Telegram Application & the Plasma Bot, the marketplace. The marketplace should behave just like a [Load Balancer](https://en.wikipedia.org/wiki/Load_balancing_(computing)). *"In computing, load balancing refers to the process of distributing a set of tasks over a set of resources (computing units), with the aim of making their overall processing more efficient."*

In this way, each Pillar Owner (for example) can start a Plasma Bot, which would connect to the marketplace. All requests for plasma will go through the marketplace, and be server by willing bots.
This would allow users to spin up their own bot and put the idle plasma to good use, without trusting anyone to hold their funds. In this process the market will not be fractioned (there won't be 2 faucets for plasma)

The marketplace is the most unsure idea of them all, and more of a proof of concept at this time. The idea of incentives to provide plasma to users can be addressed as well. Some examples might include:
- users could pay a ZNN fee upfront for a 10 H fuse entry
- pillars can provide plasma to delegators
- operators can provide free plasma if someone holds a specific ZTS

-------------------------

