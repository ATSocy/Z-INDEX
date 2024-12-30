Thread: network-fork-at-block-6606106
0x3639 | 2024-02-14 00:49:02 UTC | #1

Looks like we encountered an issue with the Staking Embedded contract at block [6606105](https://zenonhub.io/explorer/momentum/554762afe5495dbd83515ab401b886b0a6a55478480f9808e6cda92c6dadf613). This caused a fork at block 6606106.

We believe the `sort.Slice` function caused the fork, identical to what happened with the AZ fork.  If you want to read about that issue, see [this post](https://github.com/zenon-network/go-zenon/pull/26#issuecomment-1674697126).  

We fixed this last time by changing to Stable Sort.  @sumamu is looking into this.  I hope we can test and deploy a fix quickly.

I think most pillars are on the main chain, which is why many people have not noticed.  I've reached out to a few Pillars who I know are forked out.  I have several nodes that are forked out, but the public node `wss://my.hc1node.com:35998` is on the main chain.

Until we get things sorted out I recommend not bridging assets, but when @sumamu reads this tomorrow he might have different advice.  @digitalSloth was the first person to notice it and since then we've been investigating most of the day. 

If you operate a node or pillar run `sudo tail -f /var/log/syslog | grep "znnd"` to see if you are processing blocks.  If you are forked you will be stuck on 6606105 and you won't see any new momentums in the logs.  The `znnd` process will reboot every few minutes.  

Stay tuned for more info zoon(tm).

-------------------------

mehowz | 2024-02-14 01:38:18 UTC | #2

ZenonORG and HyperGrowth Pillars are processing blocks.

-------------------------

