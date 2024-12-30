Thread: bitcoin-light-clients
aliencoder | 2023-09-10 19:12:17 UTC | #1

I've played with [Neutrino](https://github.com/lightninglabs/neutrino), a light client written in Go for Bitcoin.

It's a library used by the `lnd` lightning network node.

We can integrate it into NoM and unlock more use cases such as P2P swaps for example.

-------------------------

aliencoder | 2023-09-09 17:49:55 UTC | #2

Another Bitcoin light client worth watching:

https://github.com/cloudhead/nakamoto

-------------------------

aliencoder | 2023-09-10 19:10:01 UTC | #3

I've fully synced the `nakamoto` light client on Bitcoin *mainnet* in under 20 minutes on a Macbook with M2 Pro.

You'll need [Rust](https://www.rust-lang.org/tools/install) installed on your system. Steps to run the binary:

```
git pull https://github.com/cloudhead/nakamoto
cd nakamoto
cargo build --release
cd target/release/
./nakamoto-node
```

-------------------------

georgezgeorgez | 2023-09-10 20:18:30 UTC | #4

https://twitter.com/ZeroSync_/status/1700574841714196523

-------------------------

0x3639 | 2023-09-11 12:27:44 UTC | #5

cool!

-------------------------

0x3639 | 2023-09-11 12:37:40 UTC | #6

Could we use something like this run in the side chain that will work with SYRIUS and the P2P work @vilkris is exploring with BTC atomic swaps?

This took about 2 seconds to load.  

![Screenshot 2023-09-11 at 7.37.23 AM|690x411](upload://xIskcbBJEh5YPdYqu2lKZO8tdrx.png)

-------------------------

sol | 2023-09-11 13:54:19 UTC | #7

Neutrino seems like a viable candidate for a LN node. Its fast header sync and GetUtxo function are valuable properties for our context.
Can nakamoto perform similar queries on L1?

-------------------------

aliencoder | 2023-09-11 14:11:33 UTC | #8

[quote="0x3639, post:6, topic:201"]
This took about 2 seconds to load.
[/quote]

Yes because it only proves/verifies the block headers. Nothing more, nothing less.

But we'll keep an eye on them.

[quote="sol, post:7, topic:201"]
Neutrino seems like a viable candidate for a LN node
[/quote]

It is already integrated as a library in `lnd`. We can integrate it pretty easily in `go-zenon`.

[quote="sol, post:7, topic:201"]
Can nakamoto perform similar queries on L1?
[/quote]

`nakamoto` is the same thing. A library written in Rust. From what I've tested so far, it's faster than `Neutrino`.

[quote="sol, post:7, topic:201"]
Can nakamoto perform similar queries on L1?
[/quote]

No only that, but you can also [send transactions](https://github.com/cloudhead/nakamoto/issues/91) through it.

-------------------------

