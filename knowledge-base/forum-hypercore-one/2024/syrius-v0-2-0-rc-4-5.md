Thread: syrius-v0-2-0-rc-4-5
CryptoFish | 2024-03-15 07:02:14 UTC | #1

This post will be used to collect issues for test round #5.

Download: [Syrius v0.2.0-rc.4](https://github.com/zenon-network/syrius/releases/tag/v0.2.0-rc.4)

Read [this ](https://forum.hypercore.one/t/syrius-v0-2-0/328/7) post for more information about how to test.

The following issues were fixed:

v0.2.0-rc.0
- [Unable to transact on first start](https://github.com/zenon-network/syrius/issues/74)
- https://github.com/zenon-network/syrius/pull/76

v0.2.0-rc.1
- https://github.com/zenon-network/syrius/pull/78

v0.2.0-rc.2
* https://github.com/zenon-network/syrius/pull/82
* https://github.com/zenon-network/syrius/pull/83
* https://github.com/zenon-network/syrius/pull/84
* https://github.com/zenon-network/syrius/pull/88
* https://github.com/zenon-network/syrius/pull/89

v0.2.0-rc.3
- https://github.com/zenon-network/syrius/pull/93
- https://github.com/zenon-network/syrius/pull/94
- https://github.com/zenon-network/syrius/pull/95

-------------------------

CryptoFish | 2024-03-15 11:38:29 UTC | #2

This [issue](https://github.com/zenon-network/syrius/issues/86) has been resolved.

-------------------------

CryptoFish | 2024-03-15 15:50:03 UTC | #3

Created this [PR](https://github.com/zenon-network/syrius/pull/98) to update the QR child image.

-------------------------

0x3639 | 2024-03-16 20:05:05 UTC | #4

|Version: Syrius v0.2.0-rc.4 |Environment: macOS M1 |||
|---|---|---|---|
|Date: 16/3/24|Tester: 0x3639|||
|Test case|Description|Priority|Result|
|New wallet||||
|Create new wallet using 12 word seed phrase|Create a new wallet using a 12 word seed phrase|PRIO1||
|Create new wallet using 24 word seed phrase|Create a new wallet using a 24 word seed phrase|PRIO1||
|Import wallet||||
|Import wallet using 12 word seed phrase|Import a wallet using a 12 word seed phrase|PRIO1||
|Import wallet using 24 word seed phrase|Import a wallet using a 24 word seed phrase|PRIO1||
|Import wallet using key store wallet file|Import a wallet using a backup wallet file|PRIO2||
|Hardware Wallet||||
|Scan devices with no devices connected|Scanning for devices when no Ledger devices are connected, returns an empty result.|PRIO1|PASS|
|Scan devices with one device connected|Scanning for devices when one Ledger device is connected, returns 1 result.|PRIO1|PASS|
|Scan devices with more than one device connected|Scanning for devices when more than one Ledger device is connected, returns multiple results.|PRIO1||
|Select device with device disconnected|Selecting a disconnected Ledger device after it has been scanned, displays an error message.|PRIO1||
|Select device with device connected/locked|Selecting a connected/locked Ledger device, displays an error message.|PRIO1||
|Select device with device connected/unlocked and wong app open|Selecting a connected/unlocked Ledger device with the wrong app open, displays an error message.|PRIO1||
|Select device with device connected/unlocked and app open|Selecting a connected/unlocked Ledger device with the Zenon app open, displays the address and enables the continue button.|PRIO1||
|Create hardware wallet|Create a hardware wallet using a Ledger Nano S/S+ device.|PRIO1|PASS|
|Unlocking||||
|Lock/unlock keystore wallet|Lock and unlock a keystore wallet with a password.|PRIO1||
|Lock/unlock hardware wallet with device disconnected|Unlocking a hardware wallet with a password does not require the device to be connected.|PRIO1||
|Discreet mode keystore wallet|Enable and disable discreet mode on a keystore wallet.|PRIO2||
|Discreet mode hardware wallet with device disconnected|Enable and disable discreet mode on a hardware wallet.|PRIO2||
|Transactions||||
|Send transaction on keystore wallet|Send a transaction on a keystore wallet.|PRIO1||
|Receive transaction on keystore wallet|Receive a transaction on a keystore wallet.|PRIO1||
|Send and confirm transaction on hardware wallet|Send and confirm a transaction on a hardware wallet.|PRIO1|PASS|
|Receive and confirm transaction on hardware wallet|Receive and confirm a transaction on a hardware wallet.|PRIO1|PASS|
|Send and reject transaction on hardware wallet|Send and reject a transaction on a hardware wallet.|PRIO1|PASS|
|Receive and reject transaction on hardware wallet|Receive and reject a transaction on a hardware wallet.|PRIO1|PASS|
|P2P Swap||||
|Swap history migration on existing keystore wallet|Open an existing keystore wallet with swap history and verify the migration of the swap history.|PRIO1||
|Swap history on keystore wallet after password change|Change the password on a keystore with swap history and verify that the swap history is not lost.|PRIO1||
|Swap history on keystore wallet after delete cache|Delete cache on a keystore with swap history and verify that the swap history is not lost.|PRIO1||
|Verify swap history on hardware wallet after password change|Change the password on a hardware wallet with swap history and verify that the swap history is not lost.|PRIO1||
|Verify swap history on hardware wallet after reset cache|Reset cache on a hardware wallet with swap history and verify that the swap history is not lost.|PRIO1||
|WalletConnect||||
|Wrap/unwrap assets on keystore wallet|Wrap and unwrap assets on a keystore wallet.|PRIO1||
|Wrap/unwrap assets on hardware wallet|Wrap and unwrap assets on a hardware wallet.|PRIO1||
|Addresses||||
|Add 1 address on keystore wallet|Add and confirm 1 address on a keystore wallet.|PRIO1||
|Add 1+ addresses on keystore wallet|Add and confirm 1+ address on a keystore wallet.|PRIO1||
|Add and confirm 1 address on hardware wallet|Add and confirm 1 address on a hardware wallet with device connected/unlocked and app open.|PRIO1|PASS|
|Add and confirm 1+ addresses on hardware wallet|Add and confirm 1+ address on a hardware wallet with device connected/unlocked and app open.|PRIO1|PASS|
|Add and reject 1 address on hardware wallet|Add and reject 1 address on a hardware wallet with device connected/unlocked and app open.|PRIO1|PASS|
|Add and reject 1+ addresses on hardware wallet|Add and reject 1+ address on a hardware wallet with device connected/unlocked and app open.|PRIO1|PASS|
|Security||||
|Change password of keystore wallet|Change the password of a keystore wallet and verify the change.|PRIO1||
|Change password of hardware wallet with device disconnected|Change the password of a hardware wallet with the device disconnected and verify the change.|PRIO1||
|Sign message using keystore wallet|Sign a message using a keystore wallet.|PRIO1||
|Sign message using hardware wallet|Signing a message on a hardware wallet is not supported and raises an unsupported exception.|PRIO2|PASS|
|Sign file using keystore wallet|Sign a file using a keystore wallet.|PRIO1||
|Sign file using hardware wallet|Signing a file on a hardware wallet is not supported and raises an unsupported exception.|PRIO2|PASS|
|Wallet Options||||
|Delete cache and unlock keystore wallet|Delete cache and unlock a keystore wallet.|PRIO1||
|Delete cache and unlock hardware wallet with device disconnected|A hardware wallet with deleted cache needs to be initialized with a device; otherwise an error message is shown.|PRIO1|PASS|
|Delete cache and unlock hardware wallet with device connected/locked|A hardware wallet with deleted cache needs to be initialized with a device; otherwise an error message is shown.|PRIO1|PASS|
|Delete cache and unlock hardware wallet with device connected/unlocked and app closed|A hardware wallet with deleted cache needs to be initialized with a device; otherwise an error message is shown.|PRIO1|PASS|
|Delete cache and unlock hardware wallet with device connected/unlocked and wrong app open|A hardware wallet with deleted cache needs to be initialized with a device; otherwise an error message is shown.|PRIO1|PASS|
|Delete cache and unlock hardware wallet with device connected/unlocked and app open|A hardware wallet with deleted cache needs to be initialized with a device; otherwise an error message is shown.|PRIO1|PASS|
|Backup||||
|Backup keystore wallet|Backup a keystore wallet.|PRIO1||
|Dump mnemonic of keystore wallet|Dump mnemonic of a keystore wallet.|PRIO1||
|Verify backup wallet button disabled on hardware wallet|The backup function is not supported on a hardware wallet and therefor disabled.|PRIO2|PASS|
|Verify dump mnemonic button disabled on hardware wallet|The dump mnemonic function is not supported on a hardware wallet and therefor disabled.|PRIO2|PASS|

**Notes:** 
- With ledger, reject address produces error message Ledger.Error.responseError(statusWord: deny).  Consider making it human readable.  Also the message cannot be dismissed.  You need to navagate to a different page and then come back to make it go away.  Conside improving the UX.  
- When you add 2 addresses you are required to approve each address with the ledger
- when you reject 2 addresses it fails with that error only once.  Is that the expected behavior?
- should we disable sign message / file with a hardware wallet?  Or add tip or change the error message. Current error message is "Error while signing message".  Should we change error to "Signing messages not supported with hardware wallet"
- When you reject the receipt of a TX you get the message, "Error while receiving transaction".  Should we change that to "Transaction rejected"

-------------------------

CryptoFish | 2024-03-16 19:07:51 UTC | #5

Thank for testing the ledger tests. Much appreciated.

I think the fails passed.

[quote="0x3639, post:4, topic:408"]
With ledger, reject address produces error message Ledger.Error.responseError(statusWord: deny). Consider making it human readable. Also the message cannot be dismissed. You need to navagate to a different page and then come back to make it go away. Conside improving the UX.
[/quote]

Correct, this is by design and can definitly be improved.

[quote="0x3639, post:4, topic:408"]
When you add 2 addresses you are required to approve each address with the ledger
[/quote]
Correct, I believe that's the point.

[quote="0x3639, post:4, topic:408"]
when you reject 2 addresses it fails with that error only once. Is that the expected behavior?
[/quote]
Yes, the error handling can be improved.

[quote="0x3639, post:4, topic:408"]
should we disable sign message / file with a hardware wallet? Or add tip or change the error message. Current error message is “Error while signing message”. Should we change error to “Signing messages not supported with hardware wallet”
[/quote]
All errors have details, the detail message shows the exact reason.
The sign functions are left operation on purpose. This way we only have to change and implement  the znn_ledger_dart the functions to support it.

[quote="0x3639, post:4, topic:408"]
When you reject the receipt of a TX you get the message, “Error while receiving transaction”. Should we change that to “Transaction rejected”
[/quote]
The error detail message shows the exact reason.

-------------------------

0x3639 | 2024-03-16 20:13:19 UTC | #6

[quote="CryptoFish, post:5, topic:408"]
I think the fails passed.
[/quote]
Yes, I changed them to PASS.

[quote="CryptoFish, post:5, topic:408"]
definitly be improved.
[/quote]
Maybe for another release.  After this release I can go through and provide a comprehensive list of proposed messages to change.  

Is there some map of error to human readable?  Or do we provide the actual error message?  Maybe this is something I can work on myself.

-------------------------

CryptoFish | 2024-03-18 10:20:18 UTC | #7

These issues have been resolved in the following PRs:

- https://github.com/zenon-network/syrius/pull/98
- https://github.com/zenon-network/syrius/pull/100
- https://github.com/zenon-network/syrius/pull/101

A new release candidate will be made available.

-------------------------

0x3639 | 2024-03-19 10:25:07 UTC | #8



-------------------------

