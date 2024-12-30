Thread: bitvm-compute-anything-on-bitcoin
0x3639 | 2023-10-09 16:13:36 UTC | #1

https://bitvm.org/bitvm.pdf

### SUMMARIZED BY CHATGPT
The paper titled "BitVM: Compute Anything on Bitcoin" authored by Robin Linus and published on October 9, 2023, introduces BitVM, a computing paradigm that enables Turing-complete Bitcoin contracts without necessitating changes to the network’s consensus rules. Here's a detailed summary based on the extracted content:

### Abstract

* **BitVM** is a computing paradigm designed to express Turing-complete Bitcoin contracts without altering the network’s consensus rules.
* Computations are not executed on Bitcoin but are verified, akin to optimistic rollups.
* A prover claims that a given function evaluates for specific inputs to a particular output. If the claim is false, a verifier can perform a succinct fraud proof and punish the prover.
* This mechanism allows any computable function to be verified on Bitcoin.
* Committing to a large program in a Taproot address requires significant off-chain computation and communication, but the resulting on-chain footprint is minimal.
* Complex, stateful off-chain computation can be performed without leaving any trace in the chain, as long as both parties collaborate.
* On-chain execution is only required in case of a dispute.

### Introduction

* **BitVM** creates a novel design space for more expressive Bitcoin contracts and off-chain computation.
* Potential applications include games (Chess, Go, Poker), verification of validity proofs in Bitcoin contracts, bridging BTC to foreign chains, building a prediction market, and emulating novel opcodes.
* The model is limited to a two-party setting with a prover and a verifier and requires significant off-chain computation and communication for both parties.

### Architecture

* BitVM is based on fraud proofs and a challenge-response protocol, similar to Optimistic Rollups and the MATT proposal.
* It doesn’t require changes to Bitcoin’s consensus rules and is primarily based on hashlocks, timelocks, and large Taproot trees.
* The prover commits to the program bit-by-bit, and the verifier performs a sequence of challenges to succinctly disprove a false claim of the prover.
* A sequence of challenge-and-response transactions is pre-signed by the prover and verifier, which they can later use to resolve any dispute.
* The model illustrates that this approach allows for universal computations on Bitcoin.

### Bit Value Commitment

* The bit value commitment allows the prover to set the value of a particular bit to either “0” or “1”.
* It contains two hashes, hash0 and hash1, and the prover sets the bit’s value by revealing the preimage of one of the hashes.
* Revealing both preimages allows the verifier to use them as a fraud proof and take the prover’s deposit, which is termed equivocation.
* This commitment is binding due to the ability to punish equivocation, making it an “incentive-based commitment”.

### Logic Gate Commitment

* Any computable function can be represented as a Boolean circuit, with the NAND gate being a universal logic gate.
* The implementation of a NAND gate commitment contains two bit commitments representing the two inputs and a third bit commitment representing the output.
* The Script computes the NAND value of the two inputs to ensure that it matches the committed output bit.

### Binary Circuit Commitment

* NAND gate commitments can express any circuit by composing gate commitments.
* Every step of the execution is committed to in a Tapleaf, all combined into the same Taproot address, enabling the prover to execute any gate in the circuit.

### Challenges and Responses

* Committing to a circuit is not enough to disprove an incorrect claim, so the verifier must be able to challenge the prover’s statement.
* This is facilitated by pre-signing a sequence of transactions during setup, linked like challenge → response → challenge → response, etc.

-------------------------

Chuckerboy | 2023-10-10 01:24:50 UTC | #2

We need your brain @georgezgeorgez

-------------------------

Chuckerboy | 2023-10-11 01:42:34 UTC | #4

https://x.com/robin_linus/status/1711757377983086894?s=20

Robin Linus made a Telegram group for BitVM discussions

-------------------------

0x3639 | 2023-10-11 08:32:22 UTC | #5

Good summary and explanation

https://twitter.com/BobBodily/status/1711942512603181145

-------------------------

0x3639 | 2023-10-11 13:51:59 UTC | #6

Another good post on BitVM

https://twitter.com/BobBodily/status/1711581484254192013

-------------------------

Chadass | 2023-10-11 21:01:37 UTC | #7

And the only part that catches my eyes 

"5. BitVM is in its VERY early stages. In the EVM you have the full power of Solidity. In the BitVM we have a single function that can check whether a string is all 0’s or not. That’s it. A single function (h/t Super Testnet!). Obviously many brilliant devs are working on additional functionality, but for now, we basically just have a white paper and a single function."

-------------------------

Stark | 2023-10-12 15:49:41 UTC | #8

The sense I'm getting from following this topic is that BitVM is a theoretical example that "things like this can be done."

One dev in the spaces with Leonidas yesterday spoke words to the effect of, "It will probably take me about a year to get something actually running as BitVM and I fully suspect that within that timeframe, someone else will come up with something better than BitVM."

[The spaces is available on Leonidas's Twitter.](https://x.com/leonidasnft/status/1712234993039401415?s=46)

I think the immense value of BitVM is in making people ask "why tf would i use bitcoin for this?" and thus evaluating how valuable decentralization is, and how unscaleable these store and compute are, on Bitcoin. 

Eventually people will start looking. And we won't be hiding.

-------------------------

