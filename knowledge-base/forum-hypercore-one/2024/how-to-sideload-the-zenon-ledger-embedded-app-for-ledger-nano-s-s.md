Thread: how-to-sideload-the-zenon-ledger-embedded-app-for-ledger-nano-s-s
CryptoFish | 2024-02-11 16:44:50 UTC | #1

This post explains the process of sideloading the Zenon Ledger Embedded App from pre-compiled binaries on a Ledger Nano S/S+ device.

The Zenon community is currently in the process of registering the [Zenon Ledger Embedded App](https://forum.hypercore.one/t/project-zenon-ledger-app/112/9) for admittance to the [Ledger Live](https://www.ledger.com/ledger-live) application. Once approved the Zenon Ledger Embedded App will be available for installation in the Ledger Live application.

The Zenon Ledger Embedded App can be installed directly on a device. This process is called sideloading and should be used for testing purposes only. Sideloading is only possible with a Ledger Nano S/S+ device and requires you to trust a not genuine application.

# Before you start
- Initialize your [Ledger Nano S](https://support.ledgerwallet.com/hc/en-us/articles/360000613793) or [Ledger Nano S Plus](https://support.ledger.com/hc/en-us/articles/4416927988625)
- Install the latest firmware on your [Ledger Nano S](https://support.ledgerwallet.com/hc/en-us/articles/360002731113) or [Ledger Nano S Plus](https://support.ledger.com/hc/en-us/articles/4445777839901)
- Download and install [Python](https://www.python.org/downloads/)

# Download binaries

1. Download the latest release of the [Zenon Ledger Embbeded App](https://github.com/hypercore-one/ledger-app-zenon/releases)
1. Verify the checksum and extract the contents of the archive to a directory

# Sideload app

1. Open terminal
1. Change directory to contents of the extracted `ledger-app-zenon` archive
1. Change directory to `nanos` for Ledger Nano S or `nanos2` for ledger Nano S Plus
1. Type command in terminal: `python -m pip install ledgerblue`
1. Connect the Ledger device to USB port and unlock with pin
1. Type command in terminal: `python -m ledgerblue.runScript --scp --fileName bin/app.apdu --elfFile bin/app.elf`
1. Follow instructions on the Ledger device and approve
1. The Zenon app should now be available on your device

-------------------------

