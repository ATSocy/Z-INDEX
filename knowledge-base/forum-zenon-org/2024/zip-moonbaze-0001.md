Thread: zip-moonbaze-0001
MoonBaZe | 2024-03-27 15:20:05 UTC | #1

|Field |Description|
|---|---|
|zip |ZIP: MoonBaZe-0001|
|title | convert big.Int to string on RPC responses|
|author | @MoonBaZe |
|status |Draft|
|type |Implementation ZIP|
|acceptance |upon usage by the community|
|activation |upon usage by the community|
|created |2023-05-03|
|license |GPL v3.0|
|url|[go-zenon-big-int-string-repository](https://github.com/MoonBaZZe/go-zenon)


`Motivation`

As the network evolves and increases its interoperability, there is a natural need to support tokens with a number of decimals that would overflow uint64. This requirement was also pointed out by Mr. Kaine.

`Implementation`

Each struct that contains a `big.Int` field and is returned by RPC now has two additional methods: `MarshalJSON` and `UnmarshalJSON`. These methods override the default behavior in `json-rpc` when marshaling a struct to create an RPC response. The object will now be returned as before, but the `big.Int` field is returned as a string.

In every test, the changes include wrapping each `big.Int` inside \" \". For getDepositedQsr and getQsrRegistrationCost, a new variable was included because the newly returned type is a string. In pillar_test, a few extra expects were added. Each test runs smoothly.

These changes do not affect consensus or the way nodes communicate or synchronize and can be considered a soft fork. However, it is considered a hard fork for every application (such as Syrius or web apps) that is using an older version of the `SDK` which does not contain these changes. `SDK` developers would need to update them, and all apps should be recompiled using the new `SDK`.

-------------------------

sumamu | 2023-05-03 19:11:17 UTC | #2

Awesome! That combination of JSON and BigInt was creating issues for most SDKs.

-------------------------

aliencoder | 2023-05-03 20:31:37 UTC | #3

I've started working on Syrius and the Dart SDK.

-------------------------

0x3639 | 2023-05-06 10:48:12 UTC | #4

I proposed grammar edits to this post.  they can be tracked / seen by clicking in the upper right corner of the post

![Screenshot 2023-05-06 at 5.46.33 AM|282x186](upload://hQv4gDqj1iAHOjeiPS40T7TvBPf.png)

-------------------------

