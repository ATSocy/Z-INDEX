Thread: az-for-syrius-v0-0-6
sol | 2023-06-17 23:50:19 UTC | #1

**Project Name:** 
SYRIUS v0.0.6 Improvements

**Description:** 
This update is momentous in Zenon's history, marking the first time community developers collaborated to produce a release since the wallet was open-sourced.
For over six months, the team implemented new features, added bugfixes, supplied resources, and spent many hours discussing and testing solutions.

The developers have agreed to submit one AZ for all the time and effort they put into this release, and this proposal does not include [Aliencoder's Github Actions](https://forum2.zenon.org/t/az-github-actions-on-all-zenon-network-repos-various-fixes/1360).

**URL:** https://forum2.zenon.org/t/az-for-syrius-v0-0-6/1489

**Team:** 
@0x3639 
@aliencoder 
@CryptoFish 
@[mik3mast3rs](https://github.com/mik3mast3rs)
@sol 
@ZNNAYIID 

-----

**Funding**

**Total Requested Funding** = 4,500 ZNN and 45,000 QSR
**Current Market Value** = $9,000 - $18,000
**Project Duration** = >6 months


**How did you calculate your budget?** 
This AZ covers on-boarding and development times, cost of testing resources, and opportunity cost.
Every team member had to spend dozens of hours learning the codebase without any documentation and mostly in isolation.
Each developer persisted through the barrier to entry, committed additional time identifying areas of improvement, and delivered solutions.

We will be requesting one payout for the full amount and dividing the amount among ourselves.

-------

**Contributions**
@0x3639 
- Rented @sol a cloud mac computer for 2 months at $100 per month.
- Spent approximately 5 hours testing various builds, building versions of SYRIUS with @sol, tested the .dmg creation tool (before @aliencoder automated with GhA)

@aliencoder and @mik3mast3rs

Over 150 commits in total spanning several branches
* Added multi-address widget
* Added node info icons
* [feat: added Dart logger](https://github.com/alienc0der/syrius/commit/620e0f16bde5cbb4823ec9948636ec43ca6192d0)
* [Feat: Allow user to manually change the chain id](https://github.com/alienc0der/syrius/commit/7ed530572767f36921471b95c59df50261c0f8f7)
* [Added possibility to open directory](https://github.com/alienc0der/syrius/commit/1ec006d6344966f6bb0d08ada01a72fbe16577a1)
* added tray_manager
* Added desktop notifications
* [Add launch_at_startup dependency and set it up](https://github.com/alienc0der/syrius/commit/9b640b01ed27814736796687e6975c3a9cd1d931)
* [Migrating to Material 3](https://github.com/alienc0der/syrius/commit/f4b92604577556a1bcea60b0174c8a10c2d86ef1)
* [Feat: added save, share QR for receiving address](https://github.com/alienc0der/syrius/commit/7612fa045fd18c24cbde49e25207cc4a06c91e90)
* Dependency updates
* Many other bug fixes
* Heavy refactoring

@CryptoFish 
Syrius
* [Windows Git metadata](https://github.com/KingGorrin/syrius/tree/win-git-metadata) - 2 hours
* [Linux Git metadata](https://github.com/KingGorrin/syrius/tree/linux-git-metadata) - 2 hours
* [Fix rf overflow](https://github.com/KingGorrin/syrius/tree/fix-rf-overflow) - 2 hours
* [Fix context menu](https://github.com/KingGorrin/syrius/tree/fix-context-menu) - 3 hours
* [Fix realtime graph](https://github.com/zenon-network/syrius/pull/7) - 2.5 hours
* [Fix realtime y-axis](https://github.com/zenon-network/syrius/pull/8) - 1 hour
* [Fix Get-It dispose](https://github.com/zenon-network/syrius/pull/9) - 1 hour
* [Fix fusing address select](https://github.com/zenon-network/syrius/pull/10) - 1 hour
* [Fix fusing address reset](https://github.com/zenon-network/syrius/pull/11) - 3 hours
* [Fix account stats max rpc error](https://github.com/zenon-network/syrius/pull/12) - 2 hours
* [Fix AZ listing and filtering](https://github.com/zenon-network/syrius/pull/13) - 2.5 hours
* [Feature AZ filter on all addresses](https://github.com/zenon-network/syrius/pull/14) - 1 hour
* [Fix realtime statistics refresh](https://github.com/zenon-network/syrius/pull/15) - 1 hour
* [Fix metadata escaping](https://github.com/hypercore-one/syrius/pull/8)
* [Fix realtime statistics refresh (2)](https://github.com/hypercore-one/syrius/pull/17)
* [Fix fuse button stays disabled](https://github.com/hypercore-one/syrius/pull/18)
* [Feature AZ filter on all addresses](https://github.com/hypercore-one/syrius/pull/10)

Zenon CLI for .NET

* [Github Actions (GhA) to build and release for Windows, Linux and macOS](https://github.com/KingGorrin/znn_cli_csharp/pull/2) - 4 hours

@sol 

* 1 hour - Dynamic chain identifier
* 1 hour - Updated Community links + icons
* 2 hours - Second undelegate widget
  * Technical debt: Planning to re-write this code based on Vilkris’ feedback
* 2 hours - Updated UI for multiple address + node select widgets
   * Technical debt: based on user feedback, some parts will need to be updated in the future due to poor visibility for certain elements
* 2 hours - Github actions Release info - tag, message
* \>30 hours - Implemented Linux support
* \>30 hours - Updated build process to dynamically copy libs to correct output
* \>30 hours - Updated MacOS .dmg background image
   * Assisted by 0x, Layiid, and Aliencoder

@ZNNAYIID 
- [ Updated MacOS .dmg background image](https://github.com/zenon-network/syrius/blob/master/macos/dmg/background.png) - 3 hours
---

-------------------------

TrevorLeahy3 | 2023-06-15 23:21:12 UTC | #2

This is a cool milestone and seems like great value imo.

-------------------------

romeo | 2023-06-16 02:17:15 UTC | #3

Great proposal and effort all around

-------------------------

crack | 2023-06-16 02:51:23 UTC | #4

I love the budget calculation, clear and logic.

-------------------------

DrD3 | 2023-06-16 08:38:42 UTC | #5

It has been quite the collaborative task to get to this point- thank you all your efforts. I don't have a pillar to case a vote but  ![image|192x262](upload://cEycXuUWT5HOURIRfzJNhCyWKK7.jpeg)

-------------------------

digitalSloth | 2023-06-17 15:33:21 UTC | #6

Great achievement for all involved and a very clear thought out proposal. Thanks for all the work everyone has put in

-------------------------

