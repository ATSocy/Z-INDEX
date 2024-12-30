Thread: roadmap-to-upgrade-the-network-to-support-big-int-changes
0x3639 | 2023-06-23 15:28:11 UTC | #1

## Steps to Upgrade the Network to Support Big Int Changes - TARGET UPGRADE DATE 27 JUNE 2023

**First, what are the big int changes?**  All RPC responses will return big.Int as a `string` to increase compatibility with high decimal tokens.  If you are interested in learning more, read the [ZIP:MoonBazze-0001](https://forum.zenon.org/t/zip-moonbaze-0001/1416).  

### Step 1
The znn-controller and the znn-cli need to be rebuilt with the new Dart SDK with big int support. Aliencoder already added big int support to the [Dart SDK and submitted a PR](https://github.com/zenon-network/znn_sdk_dart/pull/9).

![image|608x241](upload://zJm0dw0e5cvceRdjH61BnU3DKTT.png)

Ideally the Dart SDK should be merged with the official repo before 27 June 2023.

### Step 2
The znn-go-sdk has been updated to support big int. During the next few days, HCT will rebuild the orchestrator with the latest znn-go-sdk (with big int support). HCT will test the the code and others can review it.  The target release date is 27 June 2023.

### Step 3
After tests are complete HCT will announce the new version of the orchestrator and ask bridge participants to **upgrade both go-zenon (v0.0.6) and orchestrator (v0.0.4) at the same time**.  Target announcement is 27 June 2023.  48 hours after the announcement or after 16 orchestrators upgrade the upgrade will be live.  

**DO NOT UPGRADE UNTIL HCT MAKES AN OFFICIAL ANNOUNCEMENT**

### Step 4
Users can upgrade to SYRIUS v0.0.7.  This new version will not be able to access old public nodes running go-zenon v0.0.5.  That means `wss://secure.deeznnodez.com:35998` and   `ws://public.deeznnodez.com:35998` will no longer work with SYRIUS v0.0.7.  We will leave these old nodes in place for 30 days after we announce Step 4.  

Users who are running  SYRIUS v0.0.7 can use the internal node or the public node `wss://my.hc1node.com:35998`.  Preferably users will select the embedded node.

@aliencoder continues to bug fixing SYRIUS v0.0.7 and we hope Zenon_Network will accept his PR before 27 June 2023.  Community members should work to audit and test the code over the coming days.  

## Changelog
- Updated orchestrator in Step 3 from v0.0.3 to v0.0.4.
- Updated orchestrator in Step 3 from v0.0.4 to v0.0.5.
- Updated orchestrator in Step 3 from v0.0.5 to v0.0.4.
- Updated target upgrade date to 27 June 2023

-------------------------

aliencoder | 2023-06-14 17:48:18 UTC | #2

If there are questions about the `BigInt` support in Syrius/Dart SDK, I'm ready to help.

-------------------------

CryptoFish | 2023-06-20 18:36:30 UTC | #3

The Zenon Sdk for .NET BigInt implementation is ready to be merged.

https://github.com/KingGorrin/znn_sdk_csharp/pull/5

-------------------------

CryptoFish | 2023-06-20 18:39:24 UTC | #4

[quote="aliencoder, post:2, topic:114, full:true"]
If there are questions about the `BigInt` support in Syrius/Dart SDK, I’m ready to help.
[/quote]

Are you also planning to add BigInt support for the Htlc, Bridge and Liquidity contracts?

-------------------------

aliencoder | 2023-06-20 18:55:30 UTC | #5

Do we have those contracts in the SDK?

-------------------------

sol | 2023-06-20 19:16:56 UTC | #6

I'm nearly finished with the BigInt integration for Htlc, Bridge, Liquidity.

-------------------------

