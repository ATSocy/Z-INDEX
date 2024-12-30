Thread: syrius-v0-2-0-rc-5-6
CryptoFish | 2024-03-19 10:08:49 UTC | #1

> :exclamation: This will be the last round if no further issues are found until end of march.

This post will be used to collect issues for test round #6.

Download: [Syrius v0.2.0-rc.5](https://github.com/zenon-network/syrius/releases/tag/v0.2.0-rc.5)

Read [this ](https://forum.hypercore.one/t/syrius-v0-2-0/328/7) post for more information about how to test.

The following issues were fixed:


[details="v0.2.0-rc.0"]
- [Unable to transact on first start](https://github.com/zenon-network/syrius/issues/74)
- https://github.com/zenon-network/syrius/pull/76
[/details]

[details="v0.2.0-rc.1"]
- https://github.com/zenon-network/syrius/pull/78
[/details]

[details="v0.2.0-rc.2"]
* https://github.com/zenon-network/syrius/pull/82
* https://github.com/zenon-network/syrius/pull/83
* https://github.com/zenon-network/syrius/pull/84
* https://github.com/zenon-network/syrius/pull/88
* https://github.com/zenon-network/syrius/pull/89
[/details]

[details="v0.2.0-rc.3"]
- https://github.com/zenon-network/syrius/pull/93
- https://github.com/zenon-network/syrius/pull/94
- https://github.com/zenon-network/syrius/pull/95
[/details]

[details="v0.2.0-rc.4"]
- https://github.com/zenon-network/syrius/pull/98
- https://github.com/zenon-network/syrius/pull/100
- https://github.com/zenon-network/syrius/pull/101
[/details]

-------------------------

0x3639 | 2024-03-19 21:01:28 UTC | #2


|Date: 19/3/24|Tester: 0x3639|||
|---|---|---|---|
|Test case|Description|Priority|Result|
|New wallet||||
|Create new wallet using 12 word seed phrase|Create a new wallet using a 12 word seed phrase|PRIO1||
|Create new wallet using 24 word seed phrase|Create a new wallet using a 24 word seed phrase|PRIO1||
|Import wallet||||
|Import wallet using 12 word seed phrase|Import a wallet using a 12 word seed phrase|PRIO1||
|Import wallet using 24 word seed phrase|Import a wallet using a 24 word seed phrase|PRIO1||
|Import wallet using key store wallet file|Import a wallet using a backup wallet file|PRIO2||
|Hardware Wallet||||
|Scan devices with no devices connected|Scanning for devices when no Ledger devices are connected, returns an empty result.|PRIO1||
|Scan devices with one device connected|Scanning for devices when one Ledger device is connected, returns 1 result.|PRIO1||
|Scan devices with more than one device connected|Scanning for devices when more than one Ledger device is connected, returns multiple results.|PRIO1||
|Select device with device disconnected|Selecting a disconnected Ledger device after it has been scanned, displays an error message.|PRIO1||
|Select device with device connected/locked|Selecting a connected/locked Ledger device, displays an error message.|PRIO1||
|Select device with device connected/unlocked and wong app open|Selecting a connected/unlocked Ledger device with the wrong app open, displays an error message.|PRIO1||
|Select device with device connected/unlocked and app open|Selecting a connected/unlocked Ledger device with the Zenon app open, displays the address and enables the continue button.|PRIO1||
|Create hardware wallet|Create a hardware wallet using a Ledger Nano S/S+ device.|PRIO1||
|Unlocking||||
|Lock/unlock keystore wallet|Lock and unlock a keystore wallet with a password.|PRIO1||
|Lock/unlock hardware wallet with device disconnected|Unlocking a hardware wallet with a password does not require the device to be connected.|PRIO1||
|Discreet mode keystore wallet|Enable and disable discreet mode on a keystore wallet.|PRIO2||
|Discreet mode hardware wallet with device disconnected|Enable and disable discreet mode on a hardware wallet.|PRIO2||
|Transactions||||
|Send transaction on keystore wallet|Send a transaction on a keystore wallet.|PRIO1||
|Receive transaction on keystore wallet|Receive a transaction on a keystore wallet.|PRIO1||
|Send and confirm transaction on hardware wallet|Send and confirm a transaction on a hardware wallet.|PRIO1||
|Receive and confirm transaction on hardware wallet|Receive and confirm a transaction on a hardware wallet.|PRIO1||
|Send and reject transaction on hardware wallet|Send and reject a transaction on a hardware wallet.|PRIO1||
|Receive and reject transaction on hardware wallet|Receive and reject a transaction on a hardware wallet.|PRIO1||
|P2P Swap||||
|Swap history migration on existing keystore wallet|Open an existing keystore wallet with swap history and verify the migration of the swap history.|PRIO1||
|Swap history on keystore wallet after password change|Change the password on a keystore with swap history and verify that the swap history is not lost.|PRIO1||
|Swap history on keystore wallet after delete cache|Delete cache on a keystore with swap history and verify that the swap history is not lost.|PRIO1||
|Verify swap history on hardware wallet after password change|Change the password on a hardware wallet with swap history and verify that the swap history is not lost.|PRIO1||
|Verify swap history on hardware wallet after reset cache|Reset cache on a hardware wallet with swap history and verify that the swap history is not lost.|PRIO1||
|WalletConnect||||
|Wrap/unwrap assets on keystore wallet|Wrap and unwrap assets on a keystore wallet.|PRIO1||
|Wrap/unwrap assets on hardware wallet|Wrap and unwrap assets on a hardware wallet.|PRIO1|PASS|
|Addresses||||
|Add 1 address on keystore wallet|Add and confirm 1 address on a keystore wallet.|PRIO1||
|Add 1+ addresses on keystore wallet|Add and confirm 1+ address on a keystore wallet.|PRIO1||
|Add and confirm 1 address on hardware wallet|Add and confirm 1 address on a hardware wallet with device connected/unlocked and app open.|PRIO1||
|Add and confirm 1+ addresses on hardware wallet|Add and confirm 1+ address on a hardware wallet with device connected/unlocked and app open.|PRIO1||
|Add and reject 1 address on hardware wallet|Add and reject 1 address on a hardware wallet with device connected/unlocked and app open.|PRIO1|PASS|
|Add and reject 1+ addresses on hardware wallet|Add and reject 1+ address on a hardware wallet with device connected/unlocked and app open.|PRIO1||
|Security||||
|Change password of keystore wallet|Change the password of a keystore wallet and verify the change.|PRIO1||
|Change password of hardware wallet with device disconnected|Change the password of a hardware wallet with the device disconnected and verify the change.|PRIO1||
|Sign message using keystore wallet|Sign a message using a keystore wallet.|PRIO1||
|Sign message using hardware wallet|Signing a message on a hardware wallet is not supported and raises an unsupported exception.|PRIO2||
|Sign file using keystore wallet|Sign a file using a keystore wallet.|PRIO1||
|Sign file using hardware wallet|Signing a file on a hardware wallet is not supported and raises an unsupported exception.|PRIO2||
|Wallet Options||||
|Delete cache and unlock keystore wallet|Delete cache and unlock a keystore wallet.|PRIO1||
|Delete cache and unlock hardware wallet with device disconnected|A hardware wallet with deleted cache needs to be initialized with a device; otherwise an error message is shown.|PRIO1||
|Delete cache and unlock hardware wallet with device connected/locked|A hardware wallet with deleted cache needs to be initialized with a device; otherwise an error message is shown.|PRIO1||
|Delete cache and unlock hardware wallet with device connected/unlocked and app closed|A hardware wallet with deleted cache needs to be initialized with a device; otherwise an error message is shown.|PRIO1||
|Delete cache and unlock hardware wallet with device connected/unlocked and wrong app open|A hardware wallet with deleted cache needs to be initialized with a device; otherwise an error message is shown.|PRIO1||
|Delete cache and unlock hardware wallet with device connected/unlocked and app open|A hardware wallet with deleted cache needs to be initialized with a device; otherwise an error message is shown.|PRIO1||
|Backup||||
|Backup keystore wallet|Backup a keystore wallet.|PRIO1||
|Dump mnemonic of keystore wallet|Dump mnemonic of a keystore wallet.|PRIO1||
|Verify backup wallet button disabled on hardware wallet|The backup function is not supported on a hardware wallet and therefor disabled.|PRIO2||
|Verify dump mnemonic button disabled on hardware wallet|The dump mnemonic function is not supported on a hardware wallet and therefor disabled.|PRIO2||

Notes: Reject address w/ hardware wallet error is fixed

-------------------------

coinselor | 2024-03-22 15:28:52 UTC | #3

### WalletConnect Test Report

**Version:** 0.2.0-rc.5  
**Environment:** macOS Big Sur v11.7.10  
**Date:** 3/22/2024  
**Tester:** coinselor

#### Pairing

| Test case                                | Description                                                      | Priority | Result |
|------------------------------------------|------------------------------------------------------------------|----------|--------|
| Create pair with wc url                  | Create a walletconnect pair by manually connecting to a wc url.  | PRIO1    | PASS   |
| Create pair with on-screen QR scanner    | Create a walletconnect pair by scanning a QR with the on-screen QR scanner. | PRIO2 | PASS   |
| Create pair with camera QR scanner       | Create a walletconnect pair by scanning a QR with the camera QR scanner. | PRIO2  | FAIL   |
| Disconnect a pairing from syrius         | Disconnect a pairing by removing it from the WalletConnect Pairing List. | PRIO1   | PASS   |
| Disconnect a pairing from third-party app| Disconnect a pairing by removing it from third-party application and verify its removal from the Pairing List. | PRIO1 | PASS |
| Expired pairing                          | An expired pairing cannot be used to start a session.             | PRIO1    |        |

#### Sessions

| Test case                          | Description                                                                  | Priority | Result |
|------------------------------------|------------------------------------------------------------------------------|----------|--------|
| Approve session                    | Approve a session and verify the acknowledged session in the WalletConnect Sessions List. | PRIO1 | PASS   |
| Reject session                     | Reject a session and verify inactive pairing.                               | PRIO1    | PASS   |
| Expired session                    | An expired session cannot be used to send requests.                         | PRIO1    |        |

#### Requests

| Test case       | Description                                         | Priority | Result |
|-----------------|-----------------------------------------------------|----------|--------|
| Approve request | Approve a request and verify it has been approved.  | PRIO1    |        |
| Reject request  | Reject a request and verify it has been rejected.   | PRIO1    |        |

#### Miscellaneous

| Test case                                          | Description                                                               | Priority | Result |
|----------------------------------------------------|---------------------------------------------------------------------------|----------|--------|
| Pairings and sessions are deleted on delete cache  | Delete cache and verify pairings and sessions are deleted.               | PRIO2    |        |
| Pairings and sessions are deleted on wallet reset  | Reset and reinitialize wallet and verify pairings and sessions are deleted. | PRIO2   |        |


A few pointers:

- I could not get this Macbook Air A1466 camera to read a QR code. I tried pointing at another monitor and at a mobile screen. 
- Is there a hacky way to make the pairing expire faster? lol
- I'm confused with the pairings/sessions/requests exact definitions. The first modal is clear, it's a pairing. Is the next modal (the one asking for node/etc) a session? And when doing a tx is it a request?

-------------------------

CryptoFish | 2024-03-23 13:09:56 UTC | #4

Thank for the test run. I guess this means we'll have another RC :sweat_smile:

[quote="coinselor, post:3, topic:411"]
I could not get this Macbook Air A1466 camera to read a QR code. I tried pointing at another monitor and at a mobile screen.
[/quote]

@aliencoder is looking at the issue.

[quote="coinselor, post:3, topic:411"]
Is there a hacky way to make the pairing expire faster? lol
[/quote]
Not that I'm aware of.

[quote="coinselor, post:3, topic:411"]
I’m confused with the pairings/sessions/requests exact definitions. The first modal is clear, it’s a pairing. Is the next modal (the one asking for node/etc) a session? And when doing a tx is it a request?
[/quote]
Pairing is the process of initiating the connection and sharing cryptographic keys, while the session represents the ongoing communication channel established between the wallet and the dApp.

The confirmation for node/etc is a request, and confirmation is required in order to continue. I believe this is implementation specific and not necessarily related to WalletConnect.

-------------------------

aliencoder | 2024-03-24 09:25:37 UTC | #5

[quote="coinselor, post:3, topic:411"]
* I could not get this Macbook Air A1466 camera to read a QR code. I tried pointing at another monitor and at a mobile screen.
[/quote]

I've [fixed the bug and updated the dependency](https://github.com/zenon-network/syrius/tree/bugfix/walletconnect-camera-scanner) to the latest version. Try again now.

[quote="coinselor, post:3, topic:411"]
* Is there a hacky way to make the pairing expire faster? lol
[/quote]

You have an "X" button in the `WalletConnect Pairing List`

[quote="CryptoFish, post:4, topic:411"]
I believe this is implementation specific and not necessarily related to WalletConnect.
[/quote]

Pairing = initial handshake between the `dApp` and the `wallet`
Session = communication channel between the `dApp` and the `wallet`
Request = the `dApp` requests certain actions (signing, collecting info such as addresses, etc.) from the paired `wallet`

-------------------------

CryptoFish | 2024-03-24 10:43:11 UTC | #6

These issues have been resolved in the following PRs:

- https://github.com/zenon-network/syrius/pull/103
- https://github.com/zenon-network/syrius/pull/104

A new release candidate will be made available.

-------------------------

0x3639 | 2024-03-24 10:49:35 UTC | #7



-------------------------

