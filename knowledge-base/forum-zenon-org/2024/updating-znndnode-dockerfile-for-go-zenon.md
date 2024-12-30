Thread: updating-znndnode-dockerfile-for-go-zenon
0x3639 | 2023-04-15 21:48:06 UTC | #1

@aliencoder I'm looking at your GhA.  What is `libznn` used for and is it necessary to run `znnd`?  I'm trying to update the Dockerfile for znndNode and the build process has changed for the Dockerfile based on the latest updates to go-zenon.

https://github.com/zenon-network/go-zenon/blob/master/.github/workflows/znn_builder.yml

-------------------------

0x3639 | 2023-04-16 01:53:47 UTC | #2

I was able to make corrections to the Dockerfile and got go-zenon to build correctly.

-------------------------

aliencoder | 2023-04-16 18:09:51 UTC | #3

[quote="0x3639, post:1, topic:1371"]
What is `libznn` used for and is it necessary to run `znnd`?
[/quote]

No. `libznn` is basically `znnd` that can be used as a library in other projects.

Interesting design choice: can be integrated into any project that can call a "C" functions.

-------------------------

0x3639 | 2023-04-16 18:04:41 UTC | #4

got it.  Make sense.

-------------------------

