Thread: syrius-v0-2-0-rc-0-1
CryptoFish | 2024-03-15 07:04:58 UTC | #1

This post will be used to collect issues for test round #1.

Download: [Syrius v0.2.0-rc.0](https://github.com/zenon-network/syrius/releases/tag/v0.2.0-rc.0) 

Read [this](https://forum.hypercore.one/t/syrius-v0-2-0/328/7?u=cryptofish) post for more information about how to test.

-------------------------

theta-aquarii | 2024-03-08 14:48:24 UTC | #2

I found a bug and submitted [issue](https://github.com/zenon-network/syrius/issues/74).

I cannot upload files, so will post results here.

```
Version: v0.2.0-rc.0,Environment: Windows 10,,
Date: 8.3.2024,Tester: theta-aquarii,,
,,,
Test case,Description,Priority,Result
New wallet,,,
Create new wallet using 12 word seed phrase,Create a new wallet using a 12 word seed phrase,PRIO1,PASS
Create new wallet using 24 word seed phrase,Create a new wallet using a 24 word seed phrase,PRIO1,PASS
,,,
Import wallet,,,
Import wallet using 12 word seed phrase,Import a wallet using a 12 word seed phrase,PRIO1,PASS
Import wallet using 24 word seed phrase,Import a wallet using a 24 word seed phrase,PRIO1,PASS
Import wallet using key store wallet file,Import a wallet using a backup wallet file,PRIO2,PASS
,,,
Hardware Wallet,,,
Scan devices with no devices connected,Scanning for devices when no Ledger devices are connected, returns an empty result.,PRIO1,PASS
Scan devices with one device connected,Scanning for devices when one Ledger device is connected, returns 1 result.,PRIO1,
Scan devices with more than one device connected,Scanning for devices when more than one Ledger device is connected, returns multiple results.,PRIO1,
Select device with device disconnected,Selecting a disconnected Ledger device after it has been scanned, displays an error message.,PRIO1,
Select device with device connected/locked,Selecting a connected/locked Ledger device, displays an error message.,PRIO1,
Select device with device connected/unlocked and wong app open,Selecting a connected/unlocked Ledger device with the wrong app open, displays an error message.,PRIO1,
Select device with device connected/unlocked and app open,Selecting a connected/unlocked Ledger device with the Zenon app open, displays the address and enables the continue button.,PRIO1,
Create hardware wallet,Create a hardware wallet using a Ledger Nano S/S+ device.,PRIO1,
,,,
Unlocking,,,
Lock/unlock keystore wallet,Lock and unlock a keystore wallet with a password.,PRIO1,PASS
Lock/unlock hardware wallet with device disconnected,Unlocking a hardware wallet with a password does not require the device to be connected.,PRIO1,
Discreet mode keystore wallet,Enable and disable discreet mode on a keystore wallet.,PRIO2,PASS
Discreet mode hardware wallet with device disconnected,Enable and disable discreet mode on a hardware wallet.,PRIO2,
,,,
Transactions,,,
Send transaction on keystore wallet,Send a transaction on a keystore wallet.,PRIO1,PASS
Receive transaction on keystore wallet,Receive a transaction on a keystore wallet.,PRIO1,PASS
Send and confirm transaction on hardware wallet,Send and confirm a transaction on a hardware wallet.,PRIO1,
Receive and confirm transaction on hardware wallet,Receive and confirm a transaction on a hardware wallet.,PRIO1,
Send and reject transaction on hardware wallet,Send and reject a transaction on a hardware wallet.,PRIO1,
Receive and reject transaction on hardware wallet,Receive and reject a transaction on a hardware wallet.,PRIO1,
,,,
P2P Swap,,,
Swap history migration on existing keystore wallet,Open an existing keystore wallet with swap history and verify the migration of the swap history.,PRIO1,PASS
Swap history on keystore wallet after password change,Change the password on a keystore with swap history and verify that the swap history is not lost.,PRIO1,PASS
Swap history on keystore wallet after delete cache,Delete cache on a keystore with swap history and verify that the swap history is not lost.,PRIO1,FAIL
Verify swap history on hardware wallet after password change,Change the password on a hardware wallet with swap history and verify that the swap history is not lost.,PRIO1,
Verify swap history on hardware wallet after reset cache,Reset cache on a hardware wallet with swap history and verify that the swap history is not lost.,PRIO1,
,,,
WalletConnect,,,
Wrap/unwrap assets on keystore wallet,Wrap and unwrap assets on a keystore wallet.,PRIO1,PASS
Wrap/unwrap assets on hardware wallet,Wrap and unwrap assets on a hardware wallet.,PRIO1,
,,,
Addresses,,,
Add 1 address on keystore wallet,Add and confirm 1 address on a keystore wallet.,PRIO1,PASS
Add 1+ addresses on keystore wallet,Add and confirm 1+ address on a keystore wallet.,PRIO1,PASS
Add and confirm 1 address on hardware wallet,Add and confirm 1 address on a hardware wallet with device connected/unlocked and app open.,PRIO1,
Add and confirm 1+ addresses on hardware wallet,Add and confirm 1+ address on a hardware wallet with device connected/unlocked and app open.,PRIO1,
Add and reject 1 address on hardware wallet,Add and reject 1 address on a hardware wallet with device connected/unlocked and app open.,PRIO1,
Add and reject 1+ addresses on hardware wallet,Add and reject 1+ address on a hardware wallet with device connected/unlocked and app open.,PRIO1,
,,,
Security,,,
Change password of keystore wallet,Change the password of a keystore wallet and verify the change.,PRIO1,PASS
Change password of hardware wallet with device disconnected,Change the password of a hardware wallet with the device disconnected and verify the change.,PRIO1,
Sign message using keystore wallet,Sign a message using a keystore wallet.,PRIO1,PASS
Sign message using hardware wallet,Signing a message on a hardware wallet is not supported and raises an unsupported exception.,PRIO2,
Sign file using keystore wallet,Sign a file using a keystore wallet.,PRIO1,PASS
Sign file using hardware wallet,Signing a file on a hardware wallet is not supported and raises an unsupported exception.,PRIO2,
,,,
Wallet Options,,,
Delete cache and unlock keystore wallet,Delete cache and unlock a keystore wallet.,PRIO1,PASS
Delete cache and unlock hardware wallet with device disconnected,"A hardware wallet with deleted cache needs to be initialized with a device, otherwise an error message is shown.",PRIO1,
Delete cache and unlock hardware wallet with device connected/locked,"A hardware wallet with deleted cache needs to be initialized with a device, otherwise an error message is shown.",PRIO1,
Delete cache and unlock hardware wallet with device connected/unlocked and app closed,"A hardware wallet with deleted cache needs to be initialized with a device, otherwise an error message is shown.",PRIO1,
Delete cache and unlock hardware wallet with device connected/unlocked and wrong app open,"A hardware wallet with deleted cache needs to be initialized with a device, otherwise an error message is shown.",PRIO1,
Delete cache and unlock hardware wallet with device connected/unlocked and app open,"A hardware wallet with deleted cache needs to be initialized with a device, otherwise an error message is shown.",PRIO1,
,,,
Backup,,,
Backup keystore wallet,Backup a keystore wallet.,PRIO1,PASS
Dump mnemonic of keystore wallet,Dump mnemonic of a keystore wallet.,PRIO1,PASS
Verify backup wallet button disabled on hardware wallet,The backup function is not supported on a hardware wallet and therefor disabled.,PRIO2,
Verify dump mnemonic button disabled on hardware wallet,The dump mnemonic function is not supported on a hardware wallet and therefor disabled.,PRIO2,
```

-------------------------

CryptoFish | 2024-03-08 16:58:41 UTC | #3

Thank you for testing! Your test run has been processed.

You are eligible for a `medium` bug bounty, the bug has an easy workaround but is severe enough to disable all wallet functionality.

The bounty will be send once testing is concluded.

-------------------------

CryptoFish | 2024-03-09 18:00:37 UTC | #4

Another [issue](https://github.com/zenon-network/syrius/issues/75) has been found.

I'm not eligible for bounties, so this one is one the house.

A new release candidate will be made available in which both issues are fixed.

-------------------------

0x3639 | 2024-03-10 11:01:50 UTC | #5



-------------------------

