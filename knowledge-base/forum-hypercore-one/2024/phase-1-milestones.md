Thread: phase-1-milestones
0x3639 | 2023-05-22 11:49:23 UTC | #1

I've been thinking about laying out a roadmap to achieve [Phase 1](https://medium.com/@zenon.network/towards-nom-phase-1-global-scale-global-adoption-9046ec78218d).  Kaine wrote that medium article back in 2022 and the scope was pretty expansive.      

Then in April 2023 he went on TG and answered the question, "What is the milestone needed to qualify as phase 1?"

[![Screenshot 2023-05-22 at 6.32.03 AM|690x345](upload://xBW8CCpaYka4IS97vnF6TytHpyw.png)](https://t.me/zenonnetwork/275986)

From what I can gather, Dynamic Plasma is needed before N&T.  @georgezgeorgez is it safe to assume that Sentinels would come before N&T and are Sentinels needed to implement N&T?

@sumamu @aliencoder I understand you are working on Interop Solutions such as a Side Chain, zKRollup, and Multichain Tech.  Should I add anything else to that list?  

@sumamu you implemented libp2p for the orchestrator.  Do you plan to implement that for go-zenon?

From what I can tell, "IBD with zk proofs" is useful for mobile devices and dapps.  very fast download and proof of the blockchain.  I've run and tested [helios](https://github.com/a16z/helios) for an ETH node.  @aliencoder pointed it out to me.  Maybe this tech can be used as the basis of our implementation.  

> Helios is a fully trustless, efficient, and portable Ethereum light client written in Rust.
> 
> Helios converts an untrusted centralized RPC endpoint into a safe unmanipulable local RPC for its users. It syncs in seconds, requires no storage, and is lightweight enough to run on mobile devices.
> 
> The entire size of Helios's binary is 5.3Mb and should be easy to compile into WebAssembly. This makes it a perfect target to embed directly inside wallets and dapps.

-------------------------

sumamu | 2023-05-22 11:54:45 UTC | #2

Good initiative! I was thinking of proposing that we start discussing about the roadmap.

-------------------------

0x3639 | 2023-05-22 12:37:44 UTC | #3

Posting more notes for myself to prepare a roadmap. 

![Screenshot 2023-05-22 at 7.32.10 AM|690x293](upload://i1wZTxN3yRTzYUWLPXrkxge4LJT.png)

-------------------------

