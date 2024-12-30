Thread: combined-sdk-and-znn-cli-updates-net-and-dart
sol | 2023-10-06 18:48:32 UTC | #1

**Project Name:** 
Combined SDK and znn-cli Updates (.NET and Dart)


**Description:** 
Both SDKs and znn-cli have been updated to support all the protocol changes since Alphanet was launched. 

This includes:
  - HLTC, Spork, Bridge, Liquidity (embedded contracts)
  - BigInt (type change for variables that handle transaction amounts)

.NET: SDK v0.6.6 and znn-cli v0.3.3
Dart: SDK v0.0.5 and znn-cli v0.0.5

Since we collaborated on these changes, both sets of projects were updated in similar manners.

**Team:** @CryptoFish, @sol

---

**Funding**

**Total Requested Funding** = 5K ZNN and 50K QSR
**Project Duration** = +200 hours

**How did you calculate your budget?** 

Each of us have spent over 100 hours updating these projects, testing, and reviewing each other's work. 

**Requests**
- CryptoFish: 2,500 ZNN and 25,000 QSR
- Sol Sanctum: 2,500 ZNN and 25,000 QSR

---

**Code**

Our work can be found in the following Github branches/PRs:

## CryptoFish
* [znn-sdk-csharp](https://github.com/KingGorrin/znn_sdk_csharp)
  - PR #4 - [Support for ZIP: sumamu-0001 aka NoM Multi-chain](https://github.com/KingGorrin/znn_sdk_csharp/pull/4)
  - PR #5 - [Support for ZIP: MoonBaZe-0001 aka BigInt](https://github.com/KingGorrin/znn_sdk_csharp/pull/5)
  - PR #14 - [Fix encoding empty strings](https://github.com/hypercore-one/znn_sdk_csharp/pull/14)
  - PR #15 - [Refactored AmountUtils and added unit tests](https://github.com/hypercore-one/znn_sdk_csharp/pull/15)

* [znn-cli-csharp](https://github.com/KingGorrin/znn_cli_csharp)
  - PR #5 - [Support for Bridge/Liquidity/Bigint](https://github.com/KingGorrin/znn_cli_csharp/pull/5)
    - Support for HLTC, Spork, Liquidity, Bridge contracts, including admin and guardian functions
    - Support for Stats RPC
    - Refactor: code re-organization and simplification
    - Added -chainId options (default, auto, manual)
  - PR #6 - [Update Zenon SDK to version 0.6.4](https://github.com/hypercore-one/znn_cli_csharp/pull/6)
  - PR #7 - [ Update Zenon SDK to version 0.6.6](https://github.com/hypercore-one/znn_cli_csharp/pull/7)

## Sol Sanctum

* [znn-sdk-dart](https://github.com/zenon-network/znn_sdk_dart)
  - PR #5 - [v0.0.5](https://github.com/zenon-network/znn_sdk_dart/pull/12)
    - Support for: HTLC, Spork, Liquidity, Bridge

* [znn_cli_dart](https://github.com/zenon-network/znn_cli_dart)
  - PR #12 - [v0.0.5](https://github.com/zenon-network/znn_cli_dart/pull/5)
    - Refactored to align with the [znn_cli_csharp](https://github.com/hypercore-one/znn_cli_csharp)
    - Added support for HTLC, Spork, Bridge, Liquidity contracts
      - Added admin and guardian functions (Bridge/Liquidity)
    - Added ability to donate to AZ and query Stats RPC
    - Added `chainId` option (default, auto, manual)
    - Updated menu, including an admin-only menu
      - Updated `verbose` flag to display a brief description for commands
      - Updated `help` flag to display all options for a category
    - Updated Makefile: bugfix + support for Windows

---

**Technical Debt**

Dart/.NET CLI
- Some [orchestrator-specific](https://github.com/hypercore-one/znn_cli_dart/blob/feature/v0.0.5/lib/orchestrator.dart) functions were not implemented due to low value/increased complexity.

---

-------------------------

0x3639 | 2023-10-06 19:11:07 UTC | #2

Thank you guys for all your hard work.  You deserve this and much more IMO.

-------------------------

angelo_a_jr | 2023-10-13 09:04:43 UTC | #3

Yes from me!

-------------------------

