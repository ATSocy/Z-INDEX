Thread: syrius-v0-1-0-release-candidate-1-ready-for-community-testing
0x3639 | 2023-05-24 17:04:49 UTC | #1

## SYRIUS v0.1.0 Release Candidate 1 Ready for Public Testing

The {H}ypercore.one community development team is releasing [SYRIUS v0.1.0 Release Candidate 1](https://github.com/hypercore-one/syrius/releases) for immediate community testing.  This Release Candidate (RC) includes the following:

**Improvements**
- [PR 11](https://github.com/hypercore-one/syrius/pull/11) - Peer to Peer (P2P) swap functionality which utilizes the recently adopted [HTLC contract](https://github.com/zenon-network/go-zenon/pull/11).   

**Bug Fixes**
- [PR 8](https://github.com/hypercore-one/syrius/pull/8) - Fix metadata escaping
- [PR 9](https://github.com/hypercore-one/syrius/pull/9) - Real time statistic refresh

Community members can test this release candidate and P2P swaps on the recently deployed community TESTNET. 
All normal Syrius functions will continue to work on mainnet except for P2P swaps. 
We ask for community testing and feedback. 

---
## Quickstart tl;dr Guide

1) Download and install SYRIUS [v0.1.0-rc.1](https://github.com/hypercore-one/syrius/releases/tag/v0.1.0-rc.1) 
2) Change "Client chain identifier selection" to `321` . 
3) Add node `wss://testnet.deeznnutz.com:3598` and connect to it. 
4) Visit the faucet at https://faucet.hypercore.one/

--- 

## Steps to Setup SYRIUS v0.1.0 rc1

1) Download SYRIUS [v0.1.0-rc.1](https://github.com/hypercore-one/syrius/releases/tag/v0.1.0-rc.1)
2) Extract and install SYRIUS on your platform of choice.  
Follow this "[How to Upgrade SYRIUS](https://www.youtube.com/watch?v=UZy_m8u5nK8)" video if you have any questions.
3) Under settings "Client chain identifier selection" type `321`.  Please note the yellow icon on the right side of the image below.  If you mouse over you should see `Non-alphanet chain identifier`
![image|690x144](upload://ihWz36qjYu0oFOGAzzcnZm6luBg.png)
4) Add node `wss://testnet.deeznnutz.com:3598` and connect to it.  
    Note: the `3598` is correct.
![image|690x149](upload://bh2uWIJmhYI6lREHQIm1NyYscdS.png)
5) Take note of your ZTS TESTNET address
6) Visit the faucet at https://faucet.hypercore.one/  where you can provide the ZTS TESTNET address and receive 15 tZNN and 150 tQSR

[![image|690x477](upload://9R9ZHES4Sq62dmL0e6mNZe4T87x.png)](https://faucet.hypercore.one/ )

---

## Steps to Test Atomic Swaps with SYRIUS v0.1.0 RC 1 on TESTNET

Follow these simple instruction

https://www.youtube.com/watch?v=wUzMh5DXkLY

TESTNET Explorers can be found at:
  * [https://testnet.zenon.info](https://testnet.zenon.info/) (automatic)
  * https://explorer.zenon.network/ (requires manual connection)
    - Node = [https://node.zenon.fun:35997 ](https://node.zenon.fun:35997/)
    - Node = [https://testnet.deeznnutz.com:3597](https://testnet.deeznnutz.com:3597/)

---

## Additional Notes and Tooling

In the unlikely event a P2P swapper fails to complete their transaction, don't worry, your funds are SAFU.  {H}ypercore.one has deployed [HTLC watchtowers](https://github.com/hypercore-one/htlc-watchtower) to unlock fully approved swaps on behalf of recipients in the event they are unable to do so.  

If you want to use the command line to receive a faucet disbursement, follow the instruction below:

### Linux Faucet Terminal Command
Note: Replace `ZTS ADDRESS` with your testnet wallet address
```
curl -X POST https://node.zenon.fun:35999/faucet -H 'Content-Type: application/json' -d '{"address":"ZTS ADDRESS"}'
```

### Windows Faucet CMD Command
Note: Replace `ZTS ADDRESS` with your testnet wallet address. Make sure to leave all the `\` characters.
```
curl -X POST "https://node.zenon.fun:35999/faucet" -H "Content-Type: application/json" -d "{\"address\":\"ZTS ADDRESS\"}"
```

Follow this [short video](https://www.youtube.com/watch?v=PfJ7zTZCt-0) if you need help on using the command line instruction above to receive TESTNET tZNN and tQSR.

### TESTNET Status
- Check TESTNET status and uptime here: https://status.hypercore.one/status/testnet

### Additional TESTNET RPCs
- wss://node.zenon.fun:35998

-------------------------

