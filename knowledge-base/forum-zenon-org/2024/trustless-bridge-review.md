Thread: trustless-bridge-review
0x3639 | 2023-02-16 22:26:10 UTC | #1

As I'm sure all of you are aware, @sumamu and his team recently posted the bridge code for the community to review.  

@sol and I are working with him to setup the testnet so we can try out the code.  I'm sure everyone is busy working on SYRIUS, HTLC, PTLC, and Atomic Swaps. 

Once everyone burns through their current work, I'm curious how we plan to review this code.

1) Should he submit a PR while the community audits it?
2) Should we audit it and then submit a PR?
3) Should we have a discussion about the architecture before doing anything?
4) Do we think this needs a ZIP?

I hope we can give @sumamu some feedback on general expectations.  If we need a ZIP I'm happy to help with that process.  Here is the repo.  

https://github.com/HyperCore-Team

My hope is we can avoid a situation where sumamu submits the PR, it gets approved, and the Pillars are not ready to adopt it.  Which is why I'm posting now to try and avoid that.

-------------------------

sol | 2023-02-16 22:45:21 UTC | #2

I think we should follow this order of operations:
1. Community-wide architectural review + confirming the code works
2. Code review
3. Code audit
4. ZIP
5. PR

I *really* want to avoid a "trust me bro, it works" situation.
Any mistake in this project can be devastating for Zenon.
We need to be especially careful with the bridge.

-------------------------

aliencoder | 2023-02-18 16:09:11 UTC | #3

I already started to contribute and setup the Github Actions [cicd pipeline](https://github.com/alienc0der/orchestrator/tree/cicd)

`orchestrator` releases here: https://github.com/alienc0der/orchestrator/releases/tag/v0.0.1-testnet

-------------------------

0x3639 | 2023-02-27 10:06:54 UTC | #4

@sumamu wanted to share some community feedback on the bridge

![Screenshot 2023-02-27 at 4.05.53 AM|690x318](upload://r1IYtl71c1sArS50oQvVBLp371m.png)

-------------------------

