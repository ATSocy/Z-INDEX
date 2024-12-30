Thread: tutorial-hashed-timelocked-contract-htlc
CryptoFish | 2024-03-27 15:20:06 UTC | #1

Some time ago George published his work on [BTC Atomic Swaps via HTLC: Cope Edition](https://github.com/Big-Inches-Club-House/bich/discussions/1). I've been wanting to look at the code and create the necessary tools to interact with the contract. 

For this I've recently published the [C# version of the Zenon CLI](https://github.com/KingGorrin/znn_cli_csharp) and created a htlc branch for interacting with George's code changes.

In order to make it more accessible for everyone I also created a tutorial I believe even the most non-tech savvy among us can follow.

The tutorial can be found here [Tutorial: Hashed Timelocked Contact (HTLC)](https://github.com/KingGorrin/znn_cli_csharp/blob/htlc/docs/tutorials/htlc.md)

Have fun and let me know what you think.

-------------------------

0x3639 | 2022-10-24 17:16:42 UTC | #2

what do the following variable do?

0
32
"all your znn belong to us"

![image|690x133](upload://46JAbe2nbNtWaiox3iWM1lfxsmW.png)

also, how does Alice reclaim her ZNN after an HTLC expires and Bob does not claim the funds?  I want to try that scenario.

-------------------------

crypto_iverson | 2022-10-24 17:04:26 UTC | #3

wtf lol

-------------------------

CryptoFish | 2022-10-27 18:18:04 UTC | #4

Hi 0x3639,

first off, you can get a list of all commands by typing in `znn-cli.exe` or a detailed help of the command by typing in `znn-cli.exe [command]`.

For example, to get the detailed help info for the `htlc.create` command, just type: `znn-cli.exe htlc.create`.

This will give you the following help info:

```
-p, --passphrase                        Use this passphrase for the keyStore or enter it manually in a secure way
-k, --keyStore                          Select the local keyStore (defaults to "available keyStore if only one is present")
-i, --index                             (Default: 0) Address index
-n, --netId                             (Default: 1) Specify the network id to use
-u, --url                               (Default: ws://127.0.0.1:35998) Provide a websocket znnd connection URL with a port
--help                                  Display this help screen.
--version                               Display version information.
hashLockedAddress (pos. 1)              Required.
tokenStandard (pos. 2) [ZNN/QSR/ZTS]    Required.
amount (pos. 3)                         Required.
expirationTime (pos. 4)                 Required. Total seconds from now
hashType (pos. 5)                       Required. 0 = SHA3-256
keyMaxSize (pos. 6)                     Required.
preimage (pos. 7)
```
So, the last three arguments mean:

0 = hashType (currently only hash type 0 is supported)
32 = keyMaxSize (determines the maximum pre-image size).
"all your znn belong to us" = pre-image (currently only tekst is supported. Looking to add option to add base64)

If the lock is expired Alice can reclaim her funds by calling.

`./znn-cli htlc.reclaim [hash id]`

and receive all unreceived transactions, just like Bob did in the toturial.

Hope this answers your question.

-------------------------

0x3639 | 2022-10-24 18:04:33 UTC | #5

Yes, that is helpful.  wanted to confirm the command would be

```./znn-cli htlc.reclaim [hash id] -k Alice -n 321```

I tried this after the contract expired and got the following error:

```Error data bib existent```

Then I ran the following command

```./znn-cli htlc.timeLocked -k Alice -n 321```

And the expired contract was not there.  I can see the ZNN is not in Bob or Alice's wallets.  Any thoughts?
thx

-------------------------

CryptoFish | 2022-10-24 18:08:55 UTC | #6

Do you have any unreceived transactions?

`./znn-cli unreceived -k Alice -n 321`

-------------------------

0x3639 | 2022-10-24 18:11:20 UTC | #7

yes.  Looks like the hash has changed.  Does that seem right?  

```Unreceived 100.00000000 tZNN from z1qxemdeddedxhtlcxxxxxxxxxxxxxxxxxygecvw. Use the hash 5da40a52b824efe63f87d2784e84569a0d20639fd7426c2aac72b32358241c7d to receive```

-------------------------

CryptoFish | 2022-10-24 18:14:39 UTC | #8

Seems like you reclaimed the htlc. The contract send the funds back and creates an transaction.

But you have to receive it first to get the funds in your wallet.

./znn-cli receiveAll -k Alice -n 321

-------------------------

0x3639 | 2022-10-24 18:15:34 UTC | #9

[quote="CryptoFish, post:8, topic:1087"]
./znn-cli receiveAll -k Alice -n 321
[/quote]

I see.  that received it.  thanks.  I'm going to write up a few additional test scenarios.  thx!

-------------------------

CryptoFish | 2022-10-26 17:45:56 UTC | #10

I've made some changes to the CLI and added scenario 2 for creating an atomic swap.

The changes include:

* added createHash command
* added htlc.inspect command
* added htlc.monitor command
* added htlc.monitorAll command
* removed preimage argument from htlc.create command
* added hashLock argument to htlc.create command
* improved formatting

-------------------------

cryptocheshire | 2022-10-27 20:52:09 UTC | #11

Thank you for all this invaluable work

-------------------------

CryptoFish | 2022-11-09 21:48:18 UTC | #12

Updated the tutorial and integrated the Linux version made by 0x3639.

-------------------------

CryptoFish | 2022-11-14 08:48:56 UTC | #13

George implemented support for the sha-256 hashing algoritme. I've updated the tools and integrated the functionality.

To try it out, you can either remove the existing builds and follow the tutorial from scratch or follow the instructions below to update and rebuild both repositories.

## Linux

### BICH go-zenon

``` bash
cd ~/repos/go-zenon
git config pull.rebase false
git pull
git merge origin/htlc
make znnd
```

### Zenon CLI for .NET 

``` bash
cd ~/repos/znn_cli_csharp
git config pull.rebase false
git pull
dotnet build --runtime linux-x64 src/ZenonCli/ZenonCli.csproj
```

## Windows

### BICH go-zenon

``` powershell
cd ~/repos/go-zenon
git config pull.rebase false
git pull
git merge origin/htlc
go build -o build/libznn.dll -buildmode=c-shared -tags libznn main_libznn.go
go build -o build/znnd.exe main.go
```
### Zenon CLI for .NET 

``` powershell
cd ~/repos/znn_cli_csharp
git config pull.rebase false
git pull
dotnet build ./src/ZenonCli/ZenonCli.csproj
```

## Usage

Use the `createHash` command to create a sha-256 hash.

`./znn-cli createHash "all your znn belong to us" 1`

Don't forget to specify the hash type when creating a htlc, by default it uses the sha3-256 hashing algoritme. Use the following command to display the help information for command.

`./znn-cli htlc.create --help`

-------------------------

0x3639 | 2022-11-13 19:53:08 UTC | #14

[quote="CryptoFish, post:13, topic:1087"]
```
git pull
```
[/quote]

When you go `git pull` you get the following error.  

```
x3639@x3639-virtual-machine:~/repos/go-zenon$ git pull 
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint: 
hint:   git config pull.rebase false  # merge (the default strategy)
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint: 
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```

We merged htlc into origin previously.  And now we are trying to pull an update to go-zenon.  I'm not a git expert, but looks like we should merge the code?  

`git config pull.rebase false`

-------------------------

0x3639 | 2022-11-13 19:54:36 UTC | #15

here is what I tried:

```
x3639@x3639-virtual-machine:~/repos/go-zenon$ git config pull.rebase false

x3639@x3639-virtual-machine:~/repos/go-zenon$ git pull
Merge made by the 'ort' strategy.
 app/action_devnet.go | 121 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++--
 1 file changed, 118 insertions(+), 3 deletions(-)



```

-------------------------

0x3639 | 2022-11-13 20:29:20 UTC | #16

Also note in this command, you need to insert a "1" in the hashType to use the sha-256

```
./znn-cli htlc.create z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 ZNN 100 3600 de543a6cab8db5bdc086d1720b97b0f097458841cd0264d789350e3b07587f5b [hashType] -k Alice -n 321
```

-------------------------

0x3639 | 2022-11-14 10:36:20 UTC | #17

HTLC Scenario 1 & 2 work with the new code using sha-256

-------------------------

CryptoFish | 2022-11-14 08:48:02 UTC | #18

[quote="0x3639, post:14, topic:1087"]
`git config pull.rebase false`
[/quote]

You're right, my settings were already set to `git config pull.rebase false`.

-------------------------

CryptoFish | 2022-11-28 19:36:11 UTC | #19

Zenon Sdk and Cli for .NET have been updated to reflect htlc api changes.

-------------------------

CryptoFish | 2023-02-16 08:40:36 UTC | #20

The [tutorial](https://github.com/KingGorrin/znn_cli_csharp/blob/htlc/docs/tutorials/htlc.md) has been updated to reflect @georgezgeorgez latest [BTC Atomic Swaps via HTLC: Cope Edition](https://github.com/Big-Inches-Club-House/bich/discussions/1) changes.

-------------------------

0x3639 | 2023-02-16 15:32:08 UTC | #21

should we test again?

-------------------------

CryptoFish | 2023-02-16 15:41:48 UTC | #22

Sure, although not much funtionality has changed. Because the get info methods are removed you can now only monitor and retrieve by htlc id. I did a walkthrough through the tutorial and managed to succesfully complete it.

I believe @georgezgeorgez is still considering the functionality to let anyone unlock a htlc. This requires a further change to the monitor and get commands to remove the hashLocked address validations.

-------------------------

