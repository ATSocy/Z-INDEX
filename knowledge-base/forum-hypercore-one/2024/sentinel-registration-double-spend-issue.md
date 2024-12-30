Thread: sentinel-registration-double-spend-issue
CryptoFish | 2023-06-19 12:28:00 UTC | #1

A community member encountered a peculiar situation during the Sentinel registration process through the s y r i u s Desktop wallet.

The user accidentally sent 2x 50K QSR during the registration process. The Sentinel was registered but the extra 50K QSR was still in the Sentinel contract. Even after the Sentinel was revoked, the extra QSR amount was not returned.

The procedure below outlines how it happened and offers a solution in case other community members encounter the problem. Hopefully we can avoid the situation altogether in future s y r i u s releases.

# Sentinel registration process

The registration process of a Sentinel consists of 4 steps, namely:

1. Plasma check
2. QSR management
3. ZNN management
4. Registry Sentinel

The Sentinel registration requires 5K ZNN and 50K QSR. It is not possible to send both funds in one transaction, therefore it is done in two separate transactions. First the required QSR amount is sent (step 2) and then the required ZNN amount is checked and sent (steps 3 and 4).

The Sentinel contract uses two methods for the registration, namely:

- `DepositQSR`
- `Register`

The `DepositQSR` method is called in step 2 of the registration process. As the name of the method indicates, this deposits QSR. This method can be used multiple times until there is 50K QSR or more in the contract.

The `Register` method is called in step 4 of the registration process. This sends the ZNN amount. The method also checks whether the 50K QSR has been deposited in order to register the Sentinel.

In case more than 50K QSR is deposited into the contract, the remaining amount remains in the contract. The deconstruction of the Sentinel will not return this amount. The Sentinel contract has a separate method for this, namely:

- `WithdrawQSR`

This method returns the deposited QSR amount not allocated to a Sentinel.

# Double spend situation

Because it takes a while for the DepositQSR transaction to be processed by the network, he process may be restarted during processing.  When this happens the registration checks whether the required QSR amount has been deposited and since the transaction has not yet been processed, the registration process will ask to deposit 50K QSR again.

# Solution

It is not yet possible to call the `WithdrawQSR` method in s y r i u s v0.0.5. This is currently only possible via the CLI (Command Line Interface). The procedure below describes how it works.

## Zenon CLI for .NET

Step 1 - Download the latest version from the [Zenon CLI for .NET repository](https://github.com/KingGorrin/znn_cli_csharp/releases).

Step 2 - Extract the contents of the downloaded archive to a directory.

Step 3 - Open up a [Command Prompt](https://superuser.com/questions/728810/how-do-you-open-the-command-prompt-in-windows-7-with-a-shortcut-key/1218563) and navigate to the directory where you extracted the files.

Step 4 - Execute the following command

`znn-cli sentinel.withdrawQsr -k WalletAddress -u wss://secure.deeZNNodez.com:35998`

> Replace WalletAddress with you Zenon address.

Step 5 - Open s y r i u s after executing the command to see if any QSR was returned.

-------------------------

sol | 2023-06-19 12:38:50 UTC | #2

If I remember correctly, the pillar registration process has a withdraw button. I guess we need to do something like that for sentinel registration.
Let's create a ticket and one of us will fix this soon.

-------------------------

sumamu | 2023-06-19 15:39:42 UTC | #3

Good catch! Indeed, simply duplicating the `Withdraw QSR` UI from the pillar deployment flow should fix this.

-------------------------

CryptoFish | 2023-06-19 18:00:03 UTC | #4

Sounds like fun and easy to implement, I think I will give it a try.

-------------------------

