Thread: project-zenon-ledger-app
CryptoFish | 2024-03-01 18:13:15 UTC | #1

*Zenon wallet application for Ledger Nano S/X/SP and Stax*

**Team:** [HyperCore-One](https://github.com/hypercore-one)  
**Repository**: [ledger-app-zenon](https://github.com/hypercore-one/ledger-app-zenon)  
**Proposal**: [Accelerator-Z](https://zenonhub.io/accelerator-z/project/e27501710f97bc056dc9024561a3eac4edd7de0d3e26815c592ded296ef283b0)

## Project status
- [x] phase 1 - Unaudited developer mode release - [PR #3](https://github.com/hypercore-one/ledger-app-zenon/pull/3)
- [ ] phase 2 - Developer mode release * (waiting for review)
- [ ] phase 3 - Public release

*) The app submission has been accepted by Ledger and is waiting to be reviewed. You can track the progress of the embedded app from here [Airtable - Integration Board BETA ](https://airtable.com/appIHCUneslDfKjXu/shrqrpH9y9VRorS4J/tblw7wsOQj5Fb2UzA)

## Additional projects
- [x] Ledger Wallet for CLI (dart & .NET) - [PR #43](https://github.com/zenon-network/syrius/pull/43)
- [x] Ledger Wallet for Syrius - [PR #6](https://github.com/zenon-network/znn_cli_dart/pull/6)
- [ ] Pillar migration

See the AZ-proposal for more information on the [additional projects](https://github.com/hypercore-one/ledger-app-zenon/blob/main/az.md#additional-projects-outside-the-scope-of-this-project).

-------------------------

CryptoFish | 2024-01-07 10:05:00 UTC | #2

Much progress has been made with the implementation of the Zenon Ledger App. Zenon's cryptographic security has been implemented and a first simulation trial to sign a transaction has been successful. It won't be long before an on-chain trial can be done.

In this post, using checkboxes, I will periodically update the project's progress on main tasks until it's ready for publishing.

**Transaction signature flow**

[![app-tx-flow](upload://tEglzOAYigam4MxeocBnBISgNMu.png)](https://github.com/hypercore-one/ledger-app-zenon/blob/main/assets/diagrams/app-flow-tx.png)

- [x] **Receive**
- [x] **Parsing**
- [x] **Selection**
- [x] **Display**
- [x] **Signing**

**Anatomy of a transaction**

- [x] Loading the transaction data; 
- [x] Presenting context with the transaction prompt;
- [x] Reviewing the transaction data;
- [x] Signing the transaction;
- [x] and rejecting the transaction.

**High level overview of main tasks**

- [x] Get in touch with the Ledger developer community
- [x] Learn and set up the BOLOS environment
- [x] Learn Ledger framework and SDKs
- [x] Set up repository according to Ledger security guidelines (CICD)
- [x] Design icons
- [x] Design UI flows
- [x] Define and implement APDUs
- [x] Implement transaction signature flow
- [x] Documentation
- [x] Functional tests

-------------------------

aliencoder | 2023-06-23 08:06:34 UTC | #3

Did you manage to connect the Ledger App to Syrius?

-------------------------

CryptoFish | 2023-06-23 11:55:54 UTC | #4

No not yet. First everything wil be developed and tested via Speculos using functional tests, then when the transaction flow is fully implemented it will be tested on the physical devices. Testing through syrius just adds a layer of complexity. Better to make sure the app passes all functional tests before connecting it to Syrius.

-------------------------

aliencoder | 2023-06-23 12:17:48 UTC | #5

I can help you with the Syrius integration.

-------------------------

CryptoFish | 2023-06-23 13:00:04 UTC | #6

I secretly assumed that ;)

As stated in the proposal, the actual integration of Syrius falls outside the scope of this project. I will however run  tests to make sure everything works properly on-chain using specific cli tools.

As for the Syrius integration, I think it's better to look at the SDK first. The wallet of the SDK can be abstracted so that the implementation can be replaced with, for example, a Ledger Wallet implementation and others in the future.

Syrius will then simply use an abstract wallet interface and not even know which specific implementation is being used.

-------------------------

CryptoFish | 2023-06-25 15:29:22 UTC | #7

What do we think of the Zenon icon like this?

Unfortunately, as it is now designed, the icon cannot be placed in the middle. Other attempts where the icon can be placed in the middle do not work well on the slanted side of the Z.


![00005|128x32](upload://dWlW8x3cAWlkrAQSZ6ImxDU5OVh.png)

-------------------------

0x3639 | 2023-06-27 00:10:47 UTC | #8

looks good to me

-------------------------

CryptoFish | 2023-06-29 06:37:35 UTC | #9

Concerning the sign transaction design UI flows.

**Receive transactions**

Unlike other cryptocurrencies, Zenon requires unreceived transactions to be signed. The proposal mentioned that the [send flow](https://github.com/KingGorrin/ledger-app-zenon/blob/main/assets/diagrams/app-flow-send.png) is applicable for both transaction types. This is partially true, because unreceived transactions do not contain the same information. Therefore, the UI flow cannot show the amount and the from address. In order to show this information , a separate "from" transaction needs to be supplied.

The current implementation accepts one transaction for signing, namely the transaction to be signed. Future versions may extend this for unreceived transactions.

This means that the UI flow for signing receive transactions will be different, see below:

send tx = blocktype 2 & 4
receive tx = blocktype 1, 3 & 5

A send transaction has the following flow:

1. Review transaction
1. Type (display send)
1. Amount (display amount and token symbol ZNN, QSR or ZTS)
1. Address (display to zenon address)
1. Approve or Refuse

A receive transaction has the following flow:

1. Review transaction
1. Type (display receive)
1. Hash (display tx hash as hexidecimals)
1. Approve or Refuse

**Blind signing**

The proposal also mentioned the following about blind signing.

> Signing unreceived transactions or interacting with Embedded Smart Contracts will possibly require a [blind signing](https://developers.ledger.com/docs/embedded-app/functional-requirements/) setting.

It turns out that blind signing is not required for both mentioned types of transactions. However, it can be used to sign unknown data formats. For example, if the ledger app doesn't recognise the send tx data, it will hash and display it for approval. The option could be useful if you want to sign something other than transactions.

In order to use the blind signing option it needs to be implemented and enabled by the user. This option is considered a **could have** and is not required for the first version.

**Unattended signing**

Unattended signing signs a transaction without any user (display) interaction. This is a bit controversial and while technically possible, I haven't seen any implementations of it.

I'm currently considering this option as a **won't**.

-------------------------

CryptoFish | 2023-07-03 07:58:33 UTC | #10

The app is functionally ready for the NanoS, NanoS Plus, NanoX and Stax. The code will be soon published, when it is cleaned up and documented.

The app supports two main commands, namely requesting the public key and signing a transaction. 

Below an overview of the UI flow of the NanoS.

![ledger-app-zenon-ui-flow-nanos|570x500](upload://nhuU9Bp2aa4YZz6ak6bj7yzN17v.png)

The app supports ZNN, QSR and ZTS*, bigint and decimals for displaying the amount.

*) ZTS decimals and symbol are not known and cannot displayed in version 1.0.0.

During the implementation, two future features were identified, namely providing the ledger with token info and the receive transaction info.

**Token information command**

The decimal precision and symbol of the ZNN and QSR coins are statically known, but the decimal precision and symbol of a ZTS token are not known in advance. Therefore, the current implementation cannot display decimal precision and the token symbol in the case of a ZTS token when signing a transaction.

Instead, the current implementation shows the amount without decimals and uses the ZTS symbol.

As a future enhancement, the app can include a token info command to supplement the token info. In the case of a ZTS token, the client will first provide the app with the token info by sending the token info command and then have the transaction signed.

The app checks and uses it if appropriate token information is present or falls back to the current implementation.

**Transaction information command**

Like the token-information command, additional transaction information can be provided in case of signing a receive transaction. The details of the receive transaction can be displayed in the same way as when signing a send transaction.

The app checks and uses it if appropriate transaction information is present or falls back on the current implementation (display hash).

-------------------------

aliencoder | 2023-07-03 08:22:52 UTC | #11

CONGRATULATIONS!!! 

The next steps are to implement the `Syrius <-> Ledger` connection, right?

For desktop via `USB` and for mobile I guess we'll need a `Bluetooth` connection.

-------------------------

CryptoFish | 2023-07-03 12:52:09 UTC | #12

Thanks alienc0der.

I've got the app running on a NanoS. I also got a NanoX, but it turns out you need a developer edition to be able to upload custom apps to it in developer mode :angry:

![2023-07-02 19.21.40-1|690x320](upload://8QGmt5eibFWUZY1aXvO9LPV405w.jpeg)

I'm going to write a Flutter plugin for the app. This will allow us to easily setup comms with the device, then I think we have a good basis to start with Syrius implementation.

Mobile is also possible with an USB connection, but you need an USB-C to USB-A adapter. Both are supported.

-------------------------

Chadass | 2023-07-03 14:10:03 UTC | #13

Will there be a way to move pillars onto a Ledger at some point ? Is this even technically possible?

-------------------------

CryptoFish | 2023-07-03 14:21:54 UTC | #14

As mentioned in the proposal:

> **Pillar migration**
> 
> Node operators have expressed the need to able to migrate their addresses. For complete support, node operators will need a way to move pillars from one address to another without dismantling them (and re-burning QSR, etc). Without this all existing pillars will forever stay in hot wallets.

We will do research in a migration feature for pillars in a separate project. Technically it's possible, but at this stage we don't know what implications such a feature will have, if any.

-------------------------

CryptoFish | 2023-07-04 13:40:58 UTC | #15

The source code has been published to the `develop` branch of the [ledger-app-zenon](https://github.com/hypercore-one/ledger-app-zenon/tree/develop) repo.

All checks pass except for APP_LOAD_PARAMS. The task fails because our token is not yet registered in the [ledger-database](https://github.com/LedgerHQ/ledger-app-database) repo. The registration progress is part of phase 2.

The desired app load params are:
```
"ZTS": {
  "appFlags": {"nanos": "0x000", "nanos2": "0x000", "nanox": "0x200", "stax": "0x200"},
  "appName": "Zenon",
  "curve": ["ed25519"],
  "path": ["44'/73404'"]
}
```

Efforts will be made to make a flutter plugin available for integration in Syrius and unit tests and fuzzing will be improved.

Version 1.0.0 will be released once the app has been thoroughly tested by the community.

Instructions for loading the app on a ledger device can be found in the [readme](https://github.com/hypercore-one/ledger-app-zenon/tree/develop#loading-on-a-physical-device). You need a special developer mode edition to upload the ledger app to a NanoX. The NanoS and NanoS Plus are unrestricted.

Identified future features:

- SET_TOKEN command
- SET_FROM_TX command
- SIGN_TX_HASH command
- Advanced mode
- Display contract data

-------------------------

sol | 2023-07-04 12:30:38 UTC | #16

I wish I had a Ledger to test the app. Do you know if I can virtualize the hardware?

I see the fuzzing code in your repo. Nice!

-------------------------

CryptoFish | 2023-07-04 12:36:46 UTC | #17

The functional tests included in the repo contain tests with Speculor. The tests simulates all scenarios on all 4 ledger devices. The display results are captured with a golden run, and consequently used for comparing the resutls of the tests. 

I'm pretty confident that the APDU's communication works accordingly. The fuzzing tests will help to trackle some of the unexpected scenarios. The fuzzing code is not yet complete.

-------------------------

CryptoFish | 2023-07-06 20:05:52 UTC | #18

It is possible to change the backend of the functional tests with a physical device. I've managed to successfully run the functional tests on a Nano S. Not all tests will be able to run with success because some rely on ledger's built-in seed phrase, causing the calculated public key to be different.

The function call in the tests `tests/test_pubkey_cmd.py` needs to be called with a custom mnemonic in other for all tests to succeed.

``` python
custom_mnemonic = "[enter mnemonic here]"

calculate_public_key_and_chaincode(CurveChoice.Ed25519Slip, 
                                   path=path, 
                                   mnemonic=custom_mnemonic)
```

To run the tests on a physical device, change line 90 of `.vscode/tasks.json` to:

`"command": "docker exec -it ${config:container_name} bash -c 'pytest tests/ --tb=short -v --device ${input:model} --backend LedgerWallet'",`

The physical device must be started, with the expected application *installed* and *running*, and connected to the computer through USB.

-------------------------

CryptoFish | 2023-07-07 11:32:00 UTC | #19

I have completed the flutter library for communicating with the ledger. All functions can be controlled using the sample application.

So far, I have only been able to test the library on Windows on a Nano S.

The library is still on my personal account for now. Feel free to fork and improve.

https://github.com/KingGorrin/flutter-ledger-zenon

This library is all you need to complete the ledger implementation for Syrius.

-------------------------

CryptoFish | 2023-07-05 16:35:12 UTC | #20

Check out the [Zenon Ledger Demo](https://www.canva.com/design/DAFnxztm-9k/GoerdZMUjGc-LMczL6CYYg/watch?utm_content=DAFnxztm-9k&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink)

-------------------------

CryptoFish | 2023-07-09 15:27:15 UTC | #21

I've adjusted the example application of the [flutter-ledger-zenon repository](https://github.com/KingGorrin/flutter-ledger-zenon) and connected it to the znn sdk.

The example application uses the `wallet` branch of the [HyperCore-One/znn_dart_sdk](https://github.com/hypercore-one/znn_sdk_dart/tree/feature/wallet). It includes the [Wallet abstraction](https://github.com/hypercore-one/znn_sdk_dart/pull/3) feature as proposed [here](https://github.com/hypercore-one/znn_sdk_dart/issues/2).

The transaction parameters are hard-coded for the moment. It would be better to allow them to be entered through the UI. Uncomment the lines in `main.dart` at line 162 and 172 and change the parameters accordingly.

With the example application you can sign send and receive transactions with a ledger and broadcast them directly to the Zenon network.

below an example to send a tx using the `ZenonLedgerWallet`.
``` dart
// Construct Zenon client
final Zenon znnClient = Zenon();

// Set chain identifier to testnet
chainId = 321;

// Determine account index
var accountIndex = 0;

// Get list of ledger devices
final devices = 
  await LedgerTransport.getLedgerDevices();

// Set default wallet
znnClient.defaultKeyPair = 
  await ZenonLedgerWallet.create(devices[0].path, accountIndex);

// Init connection to node
await znnClient.wsClient.initialize('ws://127.0.0.1:35998');

// Construct block
var toAddress = Address.parse('z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7');
var tokenStandard = znnZts;
var amount = 100000000; // 1 ZNN
var block = AccountBlockTemplate.send(toAddress, tokenStandard, amount);

// Send tx
await znnClient.send(block);

// Close connection to node
znnClient.wsClient.stop();
```

-------------------------

CryptoFish | 2023-07-07 11:10:35 UTC | #22

I am winding down operations of phase 1 of this project and will soon submit the project phase for the work.

I delivered what was promised in AZ's proposal and went even further to offer a complete integration solution for Syrius with a working demo. With the above library and sample code, integration should be a walk in the park.

I will continue to maintain the repo and offer my full support where needed and start work on phase 2.

-------------------------

CryptoFish | 2023-07-16 16:20:16 UTC | #23

# App Submission Process

With the completion of phase 1, we can start the app submission process for the **unaudited developer mode release**.

The app will be made available in Ledger Live (under developer mode) once the sumbission process is complete.

To apply for the unaudited developer mode release, we need to meet the requirements of 1, 2 en 3. All requirements are complete except for the legal entity name and the CoinMarketCap listing, @0x3639 is working on that. The other requirements will be part of phase 2 and 3.

1 - General information

- [x] Embedded app name (Zenon)
- [/] The name of your token as displayed in CoinMarketCap (ZNN)
- [ ] Legal Entity name
- [ ] Postal address
- [ ] Email address

2 - Security (Mandatory for Audited Apps / Recommended for unaudited Apps)

- [x] I have read the security guidelines
- [x] The guideline_enforcer workflow succeeds
- [x] All vulnerabilities have been fixed

3 - Embedded app

- [x] I have read the coding guidelines
- [x] Embedded app source code (GitHub repository) ([Repository](https://github.com/HyperCore-One/ledger-app-zenon))
- [x] My app repository has a test folder that contains the Functional tests and Unit tests
- [x] The App has been fully tested with a companion wallet (CLI or GUI)
- [x] Two icons for the Ledger Stax, Nano and for the Ledger Live Manager in PNG or GIF (see Icons)
- [x] Video of your application running on the Ledger device (for Ledger Nano only) ([Syrius with Ledger Demo](https://www.canva.com/design/DAFoz83Wg2o/ambiWKM2CO6HAkm9M_BAzg/watch?utm_content=DAFoz83Wg2o&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink))
- [ ] The App has a Blind Signing setting (if applicable)
- [x] The Guidelines_enforcer and Build_and_functional_tests workflow succeeds

4 - Companion Wallet

- [ ] A link to the Companion Wallet The wallet must give an option to verify the receiving address on a Ledger device. It should also have an affiliate link next to the “Connect with Ledger” option. You must provide either:
a link to the CLI repository, or
a link to the GUI running on Windows/MacOS/Linux (mandatory for Public release)

5 - Documentation

- [x] Document in the App’s repository the list of the app’s APDUs and status words
- [ ] Link to a Google doc tutorial about how to install and use your app (see Third Party Applications Support)
  - [ ] The doc must include the link to the published tutorial hosted on third party website

6 - Support

- [ ] I have read the support page
- [ ] Main support contact (mail address, Slack/Reddit/Telegram/Discord communities)

7 - Marketing (Mandatory for Public release / Recommended for Audited Apps / Not applicable for Unaudited Apps)

- [ ] I have read the marketing page
- [ ] Marketing plan

8 - Warranty and liability

- [ ] I have read and agree with information laid out the warranty and liability disclaimer

-------------------------

CryptoFish | 2023-07-16 16:20:06 UTC | #24

Made new [Syrius with Ledger Demo](https://www.canva.com/design/DAFoz83Wg2o/ambiWKM2CO6HAkm9M_BAzg/watch?utm_content=DAFoz83Wg2o&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink) video. The implementation is for demo purposes only.

-------------------------

sumamu | 2023-07-17 16:56:43 UTC | #25

Awesome work, @CryptoFish! This is something I didn't even dare to expect.
Can't wait to see everything running in the same syrius release.

-------------------------

CryptoFish | 2023-07-20 14:35:59 UTC | #26

The syrius implementation is a crude and ledger specific hardcoded version. Only to proof the app is working as expected.

The demo is needed for the [App Submission Process](https://forum.hypercore.one/t/project-ledger-zenon-app/112/23#app-submission-process-1). Once the app is submitted it will be possible to install the app with Ledger Live.

This exercise does show that the total scope of the syrius implementation is not very complicated (in terms of wallet functionality) and allowed me to prooftest and finish the [Wallet abstraction](https://github.com/hypercore-one/znn_sdk_dart/pull/3).

-------------------------

CryptoFish | 2023-09-18 07:12:00 UTC | #27

I've released a pre-release version of the [Zenon SDK LedgerWallet for .NET](https://github.com/HyperCore-One/znn_sdk_csharp/tree/ledger) under the `ledger` branch. See [PR #7](https://github.com/HyperCore-One/znn_sdk_csharp/pull/7) for more details.

The library adds on top of the [Wallet abstraction](https://github.com/HyperCore-One/znn_sdk_csharp/tree/wallet) introduced in the `wallet` branch. See [PR #6](https://github.com/HyperCore-One/znn_sdk_csharp/pull/6) for more details.

The library adds cross-platform support for the Ledger Nano S/X/SP and Stax on Windows/Linux/OSX. See the [README](https://github.com/hypercore-one/znn_sdk_csharp/blob/ledger/src/Zenon.Wallet.Ledger/README.md) for more details on how to use the library.

A pre-release version of [Zenon CLI for .NET](https://github.com/HyperCore-One/znn_cli_csharp/tree/bigint-ledger) under the `bigint-ledger` branch utilises the library. This makes it possible to override the default file based wallet by specifying the `-k` switch, followed by the ledger type. For example: `-k nanos`. It will scan and connect the device. The device must be connected and have the [Zenon Ledger App](https://github.com/HyperCore-One/ledger-app-zenon) installed and open. All commands are supported except for the `wallet.dumpMnemonic` command.

A pre-release version for Node v0.0.6+ can be downloaded [here](https://github.com/HyperCore-One/znn_cli_csharp/releases).

## Linux

Follow these instructions here to install the [udev rules](https://github.com/HyperCore-One/znn_sdk_csharp/tree/ledger/udev) on Linux and make sure the [HIDAPI](https://github.com/libusb/hidapi) is insalled.

```
sudo apt install libhidapi-dev
```

-------------------------

CryptoFish | 2023-09-11 20:28:12 UTC | #28

The Ledger Zenon App has been submitted for registration to the Ledger Live app.

For the registration another [demo](https://www.canva.com/design/DAFuKR2DClg/SfXEb2TmoKbrq16M36bmnQ/watch?utm_content=DAFuKR2DClg&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink) has been made using the [Zenon CLI for .NET](https://github.com/HyperCore-One/znn_cli_csharp/tree/bigint-ledger) as the companion wallet.

-------------------------

aliencoder | 2023-09-12 09:00:19 UTC | #29

Rockztar!

-------------------------

CryptoFish | 2023-11-13 11:12:39 UTC | #30

The app submission has been accepted by Ledger and is waiting to be reviewed. You can track the progress of the embedded app from here https://airtable.com/appIHCUneslDfKjXu/shrqrpH9y9VRorS4J/tblw7wsOQj5Fb2UzA

-------------------------

CryptoFish | 2023-11-14 12:11:39 UTC | #31

The documentation of [phase 2](https://github.com/hypercore-one/ledger-app-zenon/blob/main/az.md#phase-2---developer-mode-release) of the AZ proposal has been added to the document.

Although the Embedded App submission has already been submitted, I have updated the AZ proposal to document the latest changes.

While we wait for Ledger to approve the submission, I want to take up the work for the additional projects for the Companion Wallet integration. The Ledger integration has aleady been completed in the Zenon CLI for .NET and I would like to continue the integration work for the s y r i u s desktop wallet and Zenon CLI for Dart.

For this I opened a [PR](https://github.com/zenon-network/znn_sdk_dart/pull/13) in the znn-sdk-dart repository. The PR proposes to add a wallet abstraction layer to the library that allows adding different wallet implementations to the SDK. This is something that is required for the Ledger integration. As this creates a common abstraction layer for future wallet implementations.

Please review and approve the proposal so further work can continue.

-------------------------

CryptoFish | 2023-12-09 15:58:25 UTC | #32

The work to add Ledger support to the Zenon Dart CLI has been completed.

A [PR #6](https://github.com/zenon-network/znn_cli_dart/pull/6) has been opened on the [zenon-network/znn_cli_dart](https://github.com/zenon-network/znn_cli_dart) repo.

The PR has dependencies to two other libraries that where recently added to the hc1 org. These are:
- https://github.com/hypercore-one/ledger_ffi_rs
- https://github.com/hypercore-one/znn_ledger_dart

The idea is to migrate them to the zenon-network org once the PR is approved. The review of this PR should also include a review of both dependent libraries.

I've tried to keep to code changes as clean as possible and the changes follow the changes made to the .NET version. It's quite some code to cover and some parts cannot be tested without a ledger device with the Zenon Ledger Embedded App installed.

I've tested the code on a Ledger Nano S on both Windows and Linux. Support for macOS is not tested, but should work in theory.

We're looking for reviewers and testers with access to a Ledger Nano S/S+. Your support is greatly appreciated.

-------------------------

coinselor | 2023-12-09 18:20:38 UTC | #33

I think I have a spare old nano somewhere. I'll find it. 

Unfortunately, I won't be able to test Mac OS. Will give Linux and Windows a try.

-------------------------

CryptoFish | 2023-12-13 14:41:50 UTC | #34

## Zenon .NET CLI

The .NET version is completely tested, merged and released.

Repositories:

- https://github.com/hypercore-one/znn_sdk_csharp
- https://github.com/hypercore-one/znn_ledger_csharp
- https://github.com/hypercore-one/znn_cli_csharp

Latest versions:

- https://www.nuget.org/packages/Zenon.Sdk
- https://www.nuget.org/packages/Zenon.Wallet.Ledger
- https://github.com/hypercore-one/znn_cli_csharp/releases/tag/v0.4.1

Test runs:
 - [v0.3.28-ledger-gb307912330](https://github.com/hypercore-one/znn_cli_csharp/tree/main/test-runs/v0.3.28-ledger-gb307912330)
 - [v0.3.41-ledger-gddafe6bc0d](https://github.com/hypercore-one/znn_cli_csharp/tree/main/test-runs/v0.3.41-ledger-gddafe6bc0d)

## Zenon Dart CLI

The Dart version still awaits approval of [PR #6 ](https://github.com/zenon-network/znn_cli_dart/pull/6) and some repos will possible be [migrated](https://forum.hypercore.one/t/migrate-ledger-repos-to-zenon-network-on-github/274/5) in the future.

Repositories:

- https://github.com/zenon-network/znn_sdk_dart
- https://github.com/hypercore-one/ledger_ffi_rs
- https://github.com/hypercore-one/znn_ledger_dart
- https://github.com/zenon-network/znn_cli_dart

Latest versions:

- [znn_sdk_dart 0.0.6](https://github.com/zenon-network/znn_sdk_dart)
- [ledger_ffi_rs 0.0.1](https://github.com/hypercore-one/ledger_ffi_rs)
- [znn_ledger_dart 0.0.2](https://github.com/hypercore-one/znn_ledger_dart)
- https://github.com/hypercore-one/znn_cli_dart/releases/tag/v0.0.6-rc.3

Test runs:
 - [v0.0.6-rc.1](https://github.com/hypercore-one/znn_cli_dart/tree/feature/ledger/test-runs/v0.0.6-rc.1)
 - [v0.0.6-rc.2](https://github.com/hypercore-one/znn_cli_dart/tree/feature/ledger/test-runs/v0.0.6-rc.2)
 - [v0.0.6-rc.3](https://github.com/hypercore-one/znn_cli_dart/tree/feature/ledger/test-runs/v0.0.6-rc.3)

-------------------------

CryptoFish | 2024-01-08 09:45:11 UTC | #35

The Zenon app has been included in the [ledger-app-database](https://github.com/LedgerHQ/ledger-app-database/pull/150#pullrequestreview-1808254795). This causes all build tasks to pass.

-------------------------

CryptoFish | 2024-01-09 09:52:26 UTC | #36

The work for [Ledger support in Syrius](https://github.com/zenon-network/syrius/issues/41) has been described and added in an issue. Please review the issue and let me know if there are any objections to the proposed implementation.

-------------------------

CryptoFish | 2024-01-11 19:52:31 UTC | #37

Payment for the Ledger Wallet integration for znn-cli (.NET and Dart) has been submitted. Please review the pending [PR #6](https://github.com/zenon-network/znn_cli_dart/pull/6) for Zenon Dart CLI, so the work can be properly released.

Work on the Ledger Wallet integration for Syrius has been started.

-------------------------

CryptoFish | 2024-01-16 09:11:35 UTC | #38

I'm making good progress on the Ledger Wallet integration for Syrius.

While working on the [Signing Transaction UI](https://github.com/zenon-network/syrius/issues/41) I'm wondering whether or not its wise to implement a dialog screen for signing transactions with a ledger.

The problem statement is as follows. Unlike the KeyStore, opening a connection to the LedgerWallet does not mean it remains available. Because during the session, the Ledger may be disconnected, the Zenon app may not be open, or the Ledger may become locked. The Ledger device can even be accessed by another process, causing any active connections to be invalid.

With this in mind it's best to **not** maintain any long term connection to the LedgerWallet, but to only open and close it when it is needed.

This means exceptions can occur when the LedgerWallet is needed, in a similar way with the KeyStore wallet when trying to send a transaction with an incorrect chainId. Currently Syrius uses notification messages to communicate errors or informational messages to the user.

The easiest implementation would be to handle everything with notification messages. Prompting the user to take action and displaying error messages when something goes wrong. This would be inline with the current implementation, but in my opinion is not the most user friendly method.

The alternative is to open a dialog screen asking the user to connect the device or sign a transaction everytime interaction is needed. The dialog screen guides the user through the process until the issue is solved or cancelled. This implementation would only apply for the LedgerWallet and this dialog screen will appear every time interaction with the device is needed.

Would appreciate some feedback on this. Maybe someone knows a wallet similar to Syrius with Ledger support? So far I've come across Neon Wallet and Ledger Live. Neon Wallet handles everything with notification messages and Ledger Live uses a Dialog screen.

-------------------------

aliencoder | 2024-01-16 15:00:34 UTC | #39

Check out [Leather wallet](https://leather.io/) and [Taho](https://taho.xyz/). Also I would go with notifications because they are simpler to implement.

-------------------------

CryptoFish | 2024-01-17 13:14:31 UTC | #40

Both wallets are browser extensions. I'm actually looking for Desktop wallets with Ledger support. Got any of them?

-------------------------

coinselor | 2024-01-17 15:43:16 UTC | #41

Can't really think of many. Maybe check [Komodo wallet](https://atomicdex.io/en/desktop/). There's a '21 thread about [claiming user rewards](https://forum.komodoplatform.com/t/komodo-active-user-reward-on-hardware-wallets-ledger-trezor/446) with Ledger/Trezor.

-------------------------

CryptoFish | 2024-01-17 19:01:33 UTC | #42

Thanks, will check it out.

-------------------------

aliencoder | 2024-01-18 20:02:10 UTC | #43

[quote="CryptoFish, post:40, topic:112"]
I’m actually looking for Desktop wallets
[/quote]

The Ledger desktop wallet. Check this [Nano Ledger Dart library](https://github.com/RootSoft/ledger-flutter).

-------------------------

0x3639 | 2024-01-19 11:26:29 UTC | #44

[quote="CryptoFish, post:38, topic:112"]
Would appreciate some feedback on this. Maybe someone knows a wallet similar to Syrius with Ledger support?
[/quote]

I do not have experience with another wallet app that integrates with Ledger.  However, intuitively, the idea of a popup window or new window to handle the ledger connection or signing message makes more sense to me.  

The ledger is a 3rd party app so the idea of a dialog box popping up to access an external devices just makes sense.  Also, if you need to go looking for a native notification it could be frustrating for users.  So long as the popup box looks and feels like the syrius experience, my vote would be to use a dialog box.  I like them in the ledger live app.

-------------------------

CryptoFish | 2024-01-19 13:13:42 UTC | #45

That's what I initially thought too, but in retrospect it is better to use Syrius existing notification mechanism.

Better to rework the error handling and notification system as a whole, instead of implementing two separate mechanisms...

I have now completed a working implementation that includes all the features mentioned using the existing notification system. I'm currently writing some manual test cases while I wait for these two [zenon-network/znn_sdk_Dart/PR #14](https://github.com/zenon-network/znn_sdk_dart/pull/14) and [hypercore-one/znn_ledger_dart/PR #6](https://github.com/hypercore-one/znn_ledger_dart/pull/6) to be approved.

Once approved, I'll write a PR for the Syrius work.

-------------------------

CryptoFish | 2024-01-24 13:36:42 UTC | #46

Work on the Ledger Wallet integration for Syrius has been finished.

I've opened a PR for merging the [Hardware Support for Ledger](https://github.com/zenon-network/syrius/pull/43) in the Syrius develop branch.

We will work towards a release candidate once the changes of both the Ledger support and support for dust attacks are merged.

After that testing will start.

-------------------------

CryptoFish | 2024-03-01 17:11:37 UTC | #47

Payment for the Ledger Wallet integration for syrius has been submitted. The [PR](https://github.com/zenon-network/syrius/pull/43) has recently been merged into the [develop](https://github.com/zenon-network/syrius/tree/develop) branch and will be released with [Syrius v0.2.0](https://forum.hypercore.one/t/syrius-0-2-0/328/6).

The pending [PR #6](https://github.com/zenon-network/znn_cli_dart/pull/6) for Zenon Dart CLI has been approved and will soon be merged to create release v0.0.6.

Final preperations for Syrius v0.2.0 are in progress.

-------------------------

0x3639 | 2024-03-01 17:45:10 UTC | #48

I've tested the ledger app with @CryptoFish and it works exactly as expected with no issues to report.  This is well deserved funding.

-------------------------

aliencoder | 2024-03-02 13:37:05 UTC | #49

Awesome work by @CryptoFish so far! Would be very nice to see Ledger Nano integration with the mobile wallet. It seems that this [package](https://pub.dev/packages/ledger_flutter) supports BLE pairing with the Ledger Nano X.

-------------------------

CryptoFish | 2024-03-02 15:05:55 UTC | #50

I've looked at the package, and it seems very suitable for the Mobile Wallet. It only needs the Zenon app APDU implementation. I'll ask Dr Blaze if he wants to collaborate on this.

-------------------------

CryptoFish | 2024-03-05 09:38:12 UTC | #51

[quote="CryptoFish, post:47, topic:112"]
The pending [PR #6](https://github.com/zenon-network/znn_cli_dart/pull/6) for Zenon Dart CLI has been approved and will soon be merged to create release v0.0.6.
[/quote]

The [Zenon CLI for Dart v0.0.6](https://github.com/zenon-network/znn_cli_dart/releases/tag/v0.0.6) has been released.

-------------------------

CryptoFish | 2024-03-11 08:30:43 UTC | #52

The public release registration requires a companion wallet demonstration video. With Syrius v0.2.0 in the final stages of release, all was ready to create the demo.

We have upload both demo's to YouTube for easy access. See below for the URLs:

Zenon Network s y r i u s companion wallet demonstration video for the Ledger Nano S
https://youtu.be/lmbzpjtBE5E?si=kgiGGhw3rGoJyJ2U

Zenon Network CLI Ledger Demo
https://youtu.be/ke1FIDwoLjU?si=AvBV99dS6xVqLKki

-------------------------

CryptoFish | 2024-05-17 05:42:32 UTC | #53

Recently @aliengambler pointed out a [pub cache issue](https://github.com/hypercore-one/znn_ledger_dart/pull/2) with the znn_ledger_dart library.

It couldn't find the znn_ledger_dart library when building the project straight from source. The dynamic lookup has been adjusted to include a  pub cache search.

The updated library has been added to the CLI and the [Zenon CLI for Dart v0.0.7](https://github.com/zenon-network/znn_cli_dart/releases/tag/v0.0.7) has been released.

Syrius will include the new version of the znn_ledger_dart library on its next release.

---

I've discovered a bug in the Ledger app. Sending a tx amount with digits in the hundredths or more place resulted in an app crash.

After some investigation it turned out to be a bug in the BOLOS environment of Ledger. The [BOLOS](https://github.com/LedgerHQ/ledger-secure-sdk) impl. of the [snprintf](https://github.com/LedgerHQ/ledger-secure-sdk/blob/master/src/os_printf.c) function does not support zero left-padding with the **width** sub-specifier.

The details can be read in [PR #15](https://github.com/hypercore-one/ledger-app-zenon/pull/15)

An alternative method has been implemented and [version 1.0.4](https://github.com/hypercore-one/ledger-app-zenon/tree/v1.0.4) has been released.

I've created a [ticket](https://discord.com/channels/885256081289379850/1239480116267057162/1239480116267057162) on the Ledger Discord server for confirmation.

-------------------------

