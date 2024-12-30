Thread: side-chain-l2-scaling-solution
0x3639 | 2023-05-15 11:16:46 UTC | #1

I want to make sure everyone understands @sumamu and @aliencoder are investigating two different scaling solutions for NoM.

@aliencoder is investigating an [EVM/WASM compatible sidechain](https://forum.hypercore.one/t/extension-chains/52?u=0x3639). I think we should agree on a marketing term for this.  Maybe "sidechain" or "extension chain" as proposed by Alien.

@sumamu is investigating an L2 turing complete zero knowledge general computation [scaling solution](https://forum2.zenon.org/t/implementing-a-smart-contract-runtime-on-nom/462/18?u=0x3639).  This proposed solution would use a new programming language called Cairo.  I believe the contracts are called Starknet Contracts.

-------------------------

0x3639 | 2023-05-15 11:19:41 UTC | #2

@sumamu have you investigated why dYdX moved away from starknet? 

https://thedefiant.io/dydx-chain-cosmos

"dYdX cited performance and centralization concerns about Ethereum L2s as one of the reasons for the move. This undoubtedly comes as a blow to StarkWare, as dYdX is currently the largest protocol utilizing its infrastructure."

-------------------------

sumamu | 2023-05-15 11:21:49 UTC | #3

[quote="0x3639, post:1, topic:1438"]
@sumamu is investigating an L2 turing complete zero knowledge general computation [scaling solution](https://forum2.zenon.org/t/implementing-a-smart-contract-runtime-on-nom/462/18). This proposed solution would use a new programming language called Cairo. I believe the contracts are called Starknet Contracts.
[/quote]

Me and my team were initially going to release an L2 EVM, but since @aliencoder wants to do that, we'll let him do it since we're pretty busy with other stuff at the moment.

So now we're researching Turing complete zero knowledge general computation solutions for implementing such smart contract functionality directly on the L1. But these smart contracts will likely NOT be written in Solidity nor compatible with EVM.

-------------------------

zyler9985 | 2023-05-15 11:38:36 UTC | #4

Are the two solutions mutually exclusive? Or can they both be put into use, if so what for?

-------------------------

0x3639 | 2023-05-15 12:00:31 UTC | #5

tl;dr - these are two different scaling solutions that do different things and can be run together and independently.

Sidechain = compatibility with EVM / WASM
L2 = SC layer that is fast

---

I think they are two different solutions that do different things that can both be used in parallel. The Sidechain will be EVM compatible.  You can simply deploy any Solidity contract on NoM. The L2 being considered uses the Cairo programming language to write contracts and can handle much more throughput than an EVM.   

As @sumamu writes:

> On EVM when a user interacts with a smart contract, all the nodes in the network need to execute the contract and every new node needs to re-execute all the smart contract interactions when it syncs.

On the other hand, the L2 solution that sumamu is investigating:

> Using Cairo + Winterfell, on the other hand, nodes would only need to verify the proof and all the execution is done by the user off-chain, only once.

This means less work on chain to do much more work.

-------------------------

NeoShredder | 2023-05-15 13:06:29 UTC | #6

A L2 that can interoperabe with BITCOIN chain seems more appropriate.
An extension chain with evm and another over btc.  
BTC <=>ZNN<=>ETH

-------------------------

dat_she_pepe | 2023-05-15 13:28:08 UTC | #7

It seems to me that scaling solutions and anything compatible with Bitcoin are entirely different things, but maybe I'm wrong here.

-------------------------

sumamu | 2023-05-15 15:11:03 UTC | #8

[quote="0x3639, post:2, topic:1438"]
@sumamu have you investigated why dYdX moved away from starknet?

https://thedefiant.io/dydx-chain-cosmos
[/quote]

No, but it was probably due to:
- the huge fees
- high transaction confirmation times
- MEVs
- the practice of blacklisting addresses by some ERC20s

It could also be a strategic partnership between dYdX and Cosmos behind the scenes.

-------------------------

