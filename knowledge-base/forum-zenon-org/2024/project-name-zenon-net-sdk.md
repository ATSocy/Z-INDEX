Thread: project-name-zenon-net-sdk
0x3639 | 2023-04-22 13:01:11 UTC | #1

@CryptoFish how did you bang this out so fast?  Thank you very much for this contribution.  

https://github.com/KingGorrin/znn_sdk_csharp

-------------------------

CryptoFish | 2022-05-17 11:40:45 UTC | #2

Hi, thanks, but it's still in alpha. I'm currently trying to get as much code coverage as possible, collecting test data and writing the tests, fixing bugs. Wallet impl. also still needs te be done.
Testing takes a lot more time than the actual port. Hope to have it finished by the end of this month.

-------------------------

DrD3 | 2022-05-17 15:05:52 UTC | #3

Thank you for you efforts ser, you are a gentleman and a scholar!

-------------------------

CryptoFish | 2023-01-16 12:28:21 UTC | #4

Organized the unit tests and brought it in line with the Java SDK. Overall code coverage is now about 60%.

-------------------------

CryptoFish | 2023-02-16 08:37:01 UTC | #5

Updated the [htlc](https://github.com/KingGorrin/znn_sdk_csharp/tree/htlc) branch with @georgezgeorgez [latest](https://github.com/Big-Inches-Club-House/bich/discussions/1) htlc changes.

-------------------------

CryptoFish | 2023-04-22 12:42:35 UTC | #6

# What?

Add support for the following Embedded Contracts

- Spork Contract
- Hashed Timelocked Contract

# Why?

As of go-version v0.0.4 the Embedded Hashed Timelock Contract has been added and activated at Momentum Height 4188199.

The SDK needs to support the contracts to be able to interact with it.

# How?

By implementing the contract RPC methods.

https://github.com/KingGorrin/znn_sdk_csharp/pull/3

-------------------------

CryptoFish | 2023-05-22 14:06:24 UTC | #7

# What?

Add support for the following Embedded Contracts

- Bridge Contract
- Liquidity Contract

# Why?
As of go-version v0.0.4 the Hyperspace Program Cross-chain Bridge has been added and activated at Momentum Height 4188207.

The SDK needs to support the contracts to be able to interact with it.

# How?

By implementing the contract RPC methods.

https://github.com/KingGorrin/znn_sdk_csharp/pull/4

-------------------------

sumamu | 2023-05-22 14:10:44 UTC | #8

Awesome!
Also check MoonBazze's bigint changes, the SDK might need to be adjusted accordingly:
https://github.com/MoonBaZZe/go-zenon

-------------------------

CryptoFish | 2023-05-22 14:14:50 UTC | #9

They are in the `bigint` branch and will be merged once officially merged in go-zenon.

-------------------------

CryptoFish | 2023-08-02 07:27:46 UTC | #10

Version 0.6.1 with BigInt support has been released.

This [PR](https://github.com/KingGorrin/znn_sdk_csharp/pull/5) contains the Zenon Sdk for .NET implementation of the [ZIP: MoonBaZe-0001](https://forum2.zenon.org/t/zip-moonbaze-0001/1416) proposal that has been implemented on the [go-zenon](https://github.com/zenon-network/go-zenon) repository following [PR#20](https://github.com/zenon-network/go-zenon/pull/20).

All big.Int RPC responses are now parsed as strings and converted to [BigInteger](https://learn.microsoft.com/en-us/dotnet/api/system.numerics.biginteger?view=net-6.0).

-------------------------

CryptoFish | 2023-09-12 11:23:54 UTC | #11

The [Zenon SDK for .NET](https://github.com/hypercore-one/znn_sdk_csharp) repository on Github has been migrated to the [{H}yperCore-One](https://github.com/hypercore-one) organization.

From this moment on, updates about this project will take place on the [{H}yperCore-One](https://forum.hypercore.one/) forum.

@ZenonORG could you please update to the Github links on the https://zenon.org website to reflect these changes.

-------------------------

