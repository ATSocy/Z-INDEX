Thread: az-for-syrius-v0-2-0
CryptoFish | 2024-03-11 12:27:58 UTC | #1

**Project Name:**
SYRIUS v0.2.0

**Description:**
This update contains the hardware support for Ledger and multiple improvements and bug fixes that have been developed collaboratively by our developers.

Below a complete list of all changes:

**Features**
- Hardware wallet support for Ledger
- Disable autoreceive feature
- WalletConnect refactor
- Community public nodes
- Seperate plasma from sync
- Updated charts
- Reword `Send Payment` to `Send`
- Position receive widget address above amount
- Delay starting Embedded Node until confirmed
- Reset words when verify incorrect seed
- Change AZ pillar owner filters
- Load community nodes from assets

**Bug fixes**
- Fix wrapping of Pillar revocation time text
- Update app_links and ignore incoming links on Linux
- Fix FormatException when trying to fuse a large amount
- Fix receive amount formatting and QrInputTooLongException
- Fix sentinel detection on a disassembled sentinel address

**Documentation**
- Manual test cases
- Manual test runs

The developers have agreed to submit one AZ for all the time and effort they put into realizing this release.

This AZ includes the following:
- Migrating [alienc0der's v0.0.7 master](https://github.com/alienc0der/syrius/tree/master) branch into separate PRs
- Implementing features and bug fixes, see [post](https://forum.hypercore.one/t/syrius-0-2-0/328) for the complete list of included PRs
- Reviewing and testing PRs
- Preparing manual test cases for community testing
- Bug bounty program for incentivizing community testing

This AZ does not include:
- Ledger Wallet for Syrius (see [AZ proposal](https://zenonhub.io/accelerator-z/project/4c83ec5e3c7646eefc04bfa50213c052ced1b6c2246e9d3e05c4978d66cc7dfd))
- WalletConnect (see [AZ proposal 1/2](https://zenonhub.io/accelerator-z/project/58e711ca182e2a440f3a2645a4f314d2b6d4f69deb46ade32dc6f44cbaf9a1ec) and [AZ proposal 2/2](https://zenonhub.io/accelerator-z/project/cd0398ffec479c7e704ac58545b1859f93188dff8fc8a9da6e9d2992f96942c1))

**Team**
@0x3639
@aliencoder
@CryptoFish
@vilkris
@sol

---

**Funding**

**Total Requested Funding** = 4000 ZNN and 35000 QSR
**Project Duration** = >2 months

**How did you calculate your budget?** 
This project is calculated using roughly 25/250 ZNN/QSR per hour.
@0x3639 = 250/2500
@aliencoder = 150/1500
@CryptoFish = 2500/25000
@vilkris = 450/4500
@sol = 150/1500
Bounty program = 500 ZNN *

*) Note that the remaining funds of the bounty program will be donated back to the AZ funds.

---

**Contributions**

@0x3639 
- Reviewing and testing PRs - 10 hours

@aliencoder
- Reviewing and testing PRs

@CryptoFish 
- Migrating [alienc0der's v0.0.7 master](https://github.com/alienc0der/syrius/tree/master) branch into separate PRs - 24 hours
- Implementing features and bug fixes - 44 hours
- Reviewing and testing PRs - 18 hours
- Preparing manual test cases for community testing - 14 hours
- Community testing

@vilkris 
- Reviewing and testing PRs - 18 hours

@sol 
- Reviewing and testing PRs

-------------------------

CryptoFish | 2024-03-13 22:17:10 UTC | #2

The AZ project has been submitted for voting.

-------------------------

CryptoFish | 2024-04-02 12:50:42 UTC | #3

The payout phase for the AZ project has been submitted. Thank you!

-------------------------

CryptoFish | 2024-04-23 09:49:49 UTC | #4

The AZ has been paid and the following funds have been send to the contributers.

theta aquarii
- 25 ZNN for issue https://github.com/zenon-network/syrius/issues/74

0x3639
- 250/2500 ZNN/QSR
- 25 ZNN for issue https://github.com/zenon-network/syrius/issues/87
- 10 ZNN for issue https://github.com/zenon-network/syrius/issues/86
- 10 ZNN for issue https://github.com/zenon-network/syrius/issues/99

coinselor
- 10 ZNN for issue https://github.com/zenon-network/syrius/issues/85
- 25 ZNN for issue https://github.com/zenon-network/syrius/issues/91
- 10 ZNN for issue https://github.com/zenon-network/syrius/pull/104
- 10 ZNN for issue https://github.com/zenon-network/syrius/pull/106

EverlastingOS
- 10 ZNN for issue https://github.com/zenon-network/syrius/issues/90
- 10 ZNN for issue https://github.com/zenon-network/syrius/issues/108

Dr Greenthumb
- 200 ZNN for syrius promo video

vilkris
- 450/4500 ZNN/QSR

CryptoFish
- 2500/25000 ZNN/QSR

AZ donation (see [TX](https://zenonhub.io/explorer/transaction/b91cbb4a9b82025c84045b673bb7ae776cf0287807e9782d7be1092e7bcf38b6))
- Remaining bounty program (500 - 345 = 155 ZNN)

**Pending:** (waiting for address)

@aliencoder = 150/1500
@sol = 150/1500

-------------------------

0x3639 | 2024-04-24 01:52:00 UTC | #5

thank you very much @CryptoFish for all your hard work on this upgrade.  it's been a pleasure working with you and everyone else that helped make this upgrade possible.  

I miss you @sol !!!

-------------------------

