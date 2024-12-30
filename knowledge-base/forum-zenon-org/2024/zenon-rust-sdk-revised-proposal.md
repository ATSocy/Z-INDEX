Thread: zenon-rust-sdk-revised-proposal
0x3639 | 2022-04-28 19:18:43 UTC | #1

Reference implementation for Zenon SDK for Rust.  Compatible with Zenon Alphanet - Network of Momentum.  

Funding:  1430 ZNN & 100 QSR

Proposal:  https://github.com/2bonahill/znn_sdk_rust/blob/main/AZ.md
Reference: https://github.com/2bonahill/znn_sdk_rust

[poll type=regular results=always chartType=bar]
* Yes I support this initiative
* No I do NOT support this initiative
[/poll]

-------------------------

0x3639 | 2022-04-28 19:22:54 UTC | #2

I'm happy to see this revised proposal with new details.  Here is some "guidance" from the official medium post regarding SDK projects.  Maybe some of the devs who are working on SDK projects @georgezgeorgez can provide additional clarity on how best to move forward.  

SDK port project:
1. Create an open source repository and implement core functionalities
2. Showcase working demo and implement the remaining functionalities
3. Code coverage (unit tests) for the functionality & showcase final product

For transparency, I voted yes.

-------------------------

Dumeril | 2022-04-28 19:38:52 UTC | #3

Thanks for revisiting your proposal. I think this is totally reasonable now in total. 
Two points: You have 3 days for the crypto primitives and you say in your bio that you are an expert in that field. So maybe that’s possible, that would impress me. Anyway, I would hope you don’t actually do it that way - quick search shows that there are existing crates for all the primitives you mentioned. I would rather see you use existing libraries that are widely used and maybe keep these days as a buffer or add them to testing. I guess that also would be common practice. (After checking your code I see you’re already importing some.)
Second, just a hint. You probably have the endpoints from the api documentation. These aren’t complete (and not in all cases correctly documented). It’s certainly helpful as an overview, but there are a few more endpoints (at least accelerator is missing from your list) or they deliver slightly different results or require slightly different arguments in some cases.

-------------------------

Jeron | 2022-04-28 20:23:26 UTC | #4

The revision looks good @2bonahill

-------------------------

