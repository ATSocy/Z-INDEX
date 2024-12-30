Thread: dart-sdk-cli-updates
sol | 2023-02-08 22:34:59 UTC | #1

Hi everyone,

I've updated the [Dart SDK](https://github.com/Sol-Sanctum/znn_sdk_dart/tree/spork_htlc) and [Dart CLI](https://github.com/Sol-Sanctum/znn_cli_dart/tree/spork_htlc) with support for Sporks and HTLC.
I'm requesting community testing to ensure the implementations are accurate and ready for production.

For HTLC-related content, check out:
- @CryptoFish's [C# CLI](https://github.com/KingGorrin/znn_cli_csharp/tree/htlc) 
- @georgezgeorgez's [go-zenon](https://github.com/Big-Inches-Club-House/go-zenon/tree/htlc)
- @CryptoFish's [HTLC Scenarios for C# CLI](https://github.com/KingGorrin/znn_cli_csharp/blob/htlc/docs/tutorials/htlc.md)
- BICH DAO's [HTLC Discussion](https://github.com/orgs/Big-Inches-Club-House/discussions/1)

Below are instructions to get you started, along with scenarios to test some of the new functions in Dart CLI.
Feel free to try the[ other HTLC functions](https://github.com/Sol-Sanctum/znn_cli_dart/blob/spork_htlc/init_znn.dart#L83) that aren't mentioned in this post.
Please let me know if you encounter any issues.

**Setting up the environment**

[details="Details"]
1. Follow @CryptoFish's [Windows](https://github.com/KingGorrin/znn_cli_csharp/blob/htlc/docs/tutorials/setup-devnet-win10-x64.md) or [Linux](https://github.com/KingGorrin/znn_cli_csharp/blob/htlc/docs/tutorials/setup-devnet-linux-x64.md) tutorials for setting up devnet 
    -   Omit the remaining instructions when you reach "Zenon CLI for .NET" and follow the steps below to test functionality in Dart
12. You may instead use my devnet node if you don't want to set one up
     - Append ```--url ws://node.zenon.fun:36998``` to all commands
     - Send me a DM if you need tokens
     - Explorer [details](https://forum2.zenon.org/t/syrius-improvements/578/38)

2. [Install Dart](https://dart.dev/get-dart)
3. ```git clone -b spork_htlc https://github.com/Sol-Sanctum/znn_cli_dart.git && cd znn_cli_dart```
4. Depending on your OS:
   - Windows: ```make windows```
   - Linux: ```make linux```
5. ```cd build```
6. Depending on your OS:
   - Windows: ```znn-cli.exe```
   - Linux: ```./znn-cli```
[/details]


**Setting up wallets**

[details="Details"]

> The primary address of Alice is **z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7**

> The primary address of Bob is **z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4**

Create Alice wallet with password `secret`
```
znn-cli wallet.createFromMnemonic "route become dream access impulse price inform obtain engage ski believe awful
 absent pig thing vibrant possible exotic flee pepper marble rural fire fancy" secret Alice
```

Create Bob wallet with password `secret`
```
znn-cli wallet.createFromMnemonic "alone emotion announce page spend eager middle lucky frame craft junk artefact upper finger drive corn version slot blade picnic festival wealth critic silver" secret Bob
```

Fuse Plasma to both addresses

```znn-cli plasma.fuse z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7 5000 -k Alice```
```znn-cli plasma.fuse z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 5000 -k Alice```

Optional - Send Bob some tokens

```znn-cli send z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 100 ZNN -k Alice```
```znn-cli send z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 100 QSR -k Alice```
[/details]

**HTLC Scenarios** (Copied from [here](https://github.com/KingGorrin/znn_cli_csharp/blob/htlc/docs/tutorials/htlc.md))

[details="Alice wants to buy something from Bob"]
Alice wants to buy something from Bob. She will give Bob 1 hour the time to deliver her the goods in exchange for 100 ZNN.

Alice checks her balance to make sure she has enough funds.

```znn-cli balance -k Alice```

Alice locks 100 ZNN for Bob for 1 hour, generating a random preimage.
**Keep the preimage for a future step.**

```znn-cli htlc.create z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 ZNN 100 3600 -k Alice```

Example output:
> Creating htlc with amount 100.00000000 tZNN using preimage IDPF68R3VjI2vR1HlhbUpvwoW
 Can be unlocked by z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 with hashlock 4c4b3f1e4ba60c3b35a644a5535375ce6114d4f1369a9b8171ca66f603cd5b79 hashtype 0

Alice makes sure the HTLC is created and the funds have been deducted from her account before notifying Bob.

```znn-cli htlc.timeLocked z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7```
```znn-cli balance -k Alice```

Alice notifies Bob for him to inspect the HTLC.

```znn-cli htlc.hashLocked -k Bob```

Bob inspects the HTLC and agrees to the conditions and writes down the HTLC hash id.

Bob has 1 hour the time to do his part of the deal. Once finished, Alice will reveal the pre-image to Bob so that he can unlock the 100 ZNN.

```znn-cli htlc.unlock [hash id]  [preimage] -k Bob```

Bob has unlocked the 100 ZNN which the contract has send to his wallet. Bob needs to receive the unreceived transactions.

```znn-cli receiveAll -k Bob```

Bob checks his balance to make sure everything is fine.

```znn-cli balance -k Bob```
[/details]

[details="Atomic Swapping"]
Two users want to swap tokens in a trust-less manner. 
Alice will send 10 ZNN to Bob; Bob will send 100 QSR to Alice.
For this scenario, Alice will need two terminals and Bob will need one.
- Note: we're assuming both parties already have these assets and fused QSR for plasma.

1. Alice locks 10 ZNN for Bob for 1 hour, generating a random preimage.
```znn-cli htlc.create z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 ZNN 10 3600 -k Alice```
- **Save the randomly-generated preimage**
- Assuming hashLockType: 0

2. Alice will send Bob the hashLock.
   - Doesn't matter how, Alice sends the hashLock by email, SMS, instant message, etc.

3. Bob receives the hashLock from Alice and locks his 100 QSR using the same hashLock.
```znn-cli htlc.create z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7 QSR 100 3600 [hashLock] -k Bob```

4. Bob confirms that the HTLC was created.
```znn-cli htlc.timeLocked z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4```
or
```znn-cli htlc.hashLocked z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7```

5. Bob notes the hltcId and sends it to Alice.
   - Note: he merely needs to inform Alice that it's been created. She can check the details herself (Step 7).
6. Shortly after Step 5, Bob starts monitoring the all HTLCs associated with his address.
```znn-cli htlc.monitorAll -k Bob```
7. Alice confirms that Bob has configured the HTLC with the correct hashLock.
```znn-cli htlc.timeLocked z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4```
or
```znn-cli htlc.hashLocked z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7```

8. For the sake of this demo, Alice decides to monitor all HTLCs associated with her address, as well.
In Terminal 1: 
```znn-cli htlc.monitorAll -k Alice```
9. Alice is ready to unlock Bob's funds
In Terminal 2:
```znn-cli htlc.unlock [Bob's htlcId] [preimage] -k Alice```

Alice's Terminal 2: htlc is unlocked, funds ready to be received.
Alice's Terminal 1: after a few momentums, Bob will discover the preimage, unlock Alice's HTLC automatically, and Alice will see a confirmation of that result

Bob's Terminal: Bob will discover the preimage and unlock Alice's HTLC automatically
 
Both parties need to run `znn-cli receiveAll -k [keystore]` to receive their funds.


> Alice did not need to trust that Bob had the funds; they were locked in escrow with a hashLock that she could unlock.
> Bob did not need to trust that Alice had the funds; they were locked in escrow before he submitted his transaction.

[/details]
 

**Sporks**

[details="High level process"]
1. A new feature is implemented in go-zenon, tested in devnet, and is ready to be deployed to mainnet.
2. The owner of the [spork address](https://github.com/zenon-network/znn_sdk_dart/blob/master/lib/src/model/primitives/address.dart#L21) creates a new spork, signaling to network participants that a soft-fork is potentially going to occur.
3. The devs [add the spork's hash id to go-zenon](https://github.com/zenon-network/go-zenon/blob/master/common/types/spork.go) and release the updated code to users
4. After most network participants have adopted the new code, the owner of the spork address activates the spork, disabling any nodes that did not install the new code.
[/details]


[details="Scenario"]
A new feature is being deployed! We need to create and activate a [spork](https://forum2.zenon.org/t/zip-deeznnutz-0001-final/991) in order for the feature to go live.

Note: we will need to make a few changes in order to achieve this since we do not control the spork address.

For this scenario, you will setup your own devnet.
1. Follow @CryptoFish's [Windows](https://github.com/KingGorrin/znn_cli_csharp/blob/htlc/docs/tutorials/setup-devnet-win10-x64.md) or [Linux](https://github.com/KingGorrin/znn_cli_csharp/blob/htlc/docs/tutorials/setup-devnet-linux-x64.md) tutorials but also do the following:
   - Before `make znnd`
Edit this [file](https://github.com/zenon-network/go-zenon/blob/master/vm/embedded/implementation/spork.go) in your local repository: 
Comment the `block.Address` checks at lines 34 and 97
      ```
      //if block.Address != *types.SporkAddress {
      //	return constants.ErrPermissionDenied
      //}
      ```
   - Omit the remaining instructions when you reach "Zenon CLI for .NET"
2. [Install Dart](https://dart.dev/get-dart)
3. ````git clone -b spork_htlc https://github.com/Sol-Sanctum/znn_cli_dart.git && cd znn_cli_dart````
4. Depending on your OS:
   - Windows: ```make windows```
   - Linux: ```make linux```
5. ```cd build```
6. Depending on your OS:
   - Windows: ```znn-cli.exe```
   - Linux: ```znn-cli```
7. Display a list of sporks on the network 
   -  ```znn-cli spork.list ```
8. Create a new "Example-spork" spork
   - ```znn-cli spork.create "Example-spork" "Acta Non Verba" -k Alice```
9. Save the new spork's `Hash` for the next step
   - ```znn-cli spork.list```
10. Now the network participants need to update znnd/libznn with that spork
    - Edit this [file](https://github.com/zenon-network/go-zenon/blob/master/common/types/spork.go) in your local repository
    Update the `var` with two changes:
      - Add a new spork:
        ```ExampleSpork     = NewImplementedSpork("Hash from Step 7")```

      - Include it in the ImplementedSporksMap: 
        ```ExampleSpork.SporkId: true,```

11. Now `make znnd` again and run the new binary on all participating network infrastructure (pillars and nodes)
   - For this example, we just need to run it on the pillar.
12. After the pillar starts producing momentums, return to znn_cli_dart and run:
    - ```znn-cli spork.activate <Hash from Step 7> -k Alice```
13. Display a list of sporks on the network 
    -  ```znn-cli spork.list ```
    - `Example-spork` should be `Activated`
[/details]

-------------------------

dat_she_pepe | 2022-12-17 21:46:10 UTC | #2

When I try to build with make linux or make windows on the first scenario I get the following spaghetti 

![image-12|690x413](upload://jisBZeHmctVs6gmPOcnqDoBR09m.png)

-------------------------

sol | 2022-12-17 22:10:02 UTC | #3

What happens if you run:
`dart run .\cli_handler.dart`

-------------------------

dat_she_pepe | 2022-12-17 23:26:14 UTC | #4

It worked. Some little issues in your tutorial. 

- at the wallet creation it's not "" and not the ““ you used. Like this actually:

./znn-cli wallet.createFromMnemonic "route become dream access impulse price inform obtain engage ski believe awful absent pig thing vibrant possible exotic flee pepper marble rural fire fancy" secret Alice

- When Alice notifies Bob, address should be included.

- For Linux your commands should start with ./ ? At least it has to for me.

- In your second scenario Bob had no QSR. I reversed ZNN and QSR from Alice and Bob

- htlc.monitorAll has to be stopped with CTRL+C 


Everything else seems to work so just little tweaks in your tutos to be done but the code seems solid ser.


I only tested the htlc scenario though.

-------------------------

sol | 2022-12-18 00:01:20 UTC | #5

I appreciate the feedback :slight_smile: 

1. The quotes for the wallet creation step were wrong? I manually edited them now.

2. "When Alice notifies Bob, address should be included."
I assume Alice and Bob inform each other of their address before commencing. But once an HTLC is created, the other party can check for all HTLCs tied to their address, as well.

3. htlc.monitorAll will continue running until all monitored HTLCs are resolved (unlocked or reclaimed). Otherwise, you're right.

I updated some steps to reflect the Linux CLI notation and funding Bob with QSR.

Were you able to resolve the `make` issue?

-------------------------

dat_she_pepe | 2022-12-18 03:01:32 UTC | #6

Yep perfect :)

-------------------------

0x3639 | 2022-12-18 21:14:10 UTC | #7

[quote="sol, post:1, topic:1166"]
znn-cli wallet.createFromMnemonic “route become dream access impulse price inform obtain engage ski believe awful
absent pig thing vibrant possible exotic flee pepper marble rural fire fancy” secret Alice
[/quote]

Get the following error (testing [this](https://github.com/alienc0der/znn_cli_dart/tree/cicd) release) from @aliencoder 

```
./znn-cli wallet.createFromMnemonic “route become dream access impulse price inform obtain engage ski believe awful absent pig thing vibrant possible exotic flee pepper marble rural fire fancy” secret Alice
Incorrect number of arguments. Expected:
wallet.createFromMnemonic "mnemonic" passphrase [keyStoreName]
```

-------------------------

sol | 2022-12-18 21:20:50 UTC | #8

Could be the quotes. I think the forum formatting changes those characters.

-------------------------

0x3639 | 2022-12-18 23:39:46 UTC | #9

on `make linux`  I get a long list of errors, starting with

```
x3639@ubuntu:~/sol/znn_cli_dart$ make linux
mkdir -p build
dart compile exe cli_handler.dart -o build/znn-cli
Info: Compiling with sound null safety
Error: Couldn't resolve the package 'bip39' in 'package:bip39/bip39.dart'.
Error: Couldn't resolve the package 'dcli' in 'package:dcli/dcli.dart'.
Error: Couldn't resolve the package 'path' in 'package:path/path.dart'.
Error: Couldn't resolve the package 'random_string_generator' in 'package:random_string_generator/random_string_generator.dart'.
Error: Couldn't resolve the package 'collection' in 'package:collection/collection.dart'.
Error: Couldn't resolve the package 'znn_sdk_dart' in 'package:znn_sdk_dart/znn_sdk_dart.dart'.
Error: Couldn't resolve the package 'znn_sdk_dart' in 'package:znn_sdk_dart/src/abi/abi.dart'.
Error: Couldn't resolve the package 'logging' in 'package:logging/logging.dart'.
cli_handler.dart:5:8: Error: Not found: 'package:bip39/bip39.dart'
```
Full error log: https://pastebin.com/6VynY7bj

-------------------------

sol | 2022-12-18 23:59:54 UTC | #10

I updated the makefile.
`dart pub get` needs to be executed first.

-------------------------

0x3639 | 2022-12-19 01:27:46 UTC | #11

[quote="0x3639, post:7, topic:1166"]
`./znn-cli wallet.createFromMnemonic “route become dream access impulse price inform obtain engage ski believe awful absent pig thing vibrant possible exotic flee pepper marble rural fire fancy” secret Alice`
[/quote]

that worked

-------------------------

0x3639 | 2022-12-19 01:39:29 UTC | #12

Just to follow up on this command, for some reason when you paste into a bash terminal, the parentheses are changed somehow.  You need to delete them and type them manually from your keyboard for the command to work correctly.   

```
./znn-cli wallet.createFromMnemonic "route become dream access impulse price inform obtain engage ski believe awful absent pig thing vibrant possible exotic flee pepper marble rural fire fancy" secret Alice
```

-------------------------

0x3639 | 2022-12-19 19:28:03 UTC | #13

[quote="sol, post:1, topic:1166"]
znn-cli wallet.createFromMnemonic “route become dream access impulse price inform obtain engage ski believe awful
absent pig thing vibrant possible exotic flee pepper marble rural fire fancy” secret Alice
[/quote]

I see what is wrong w/ this command.  You need to insert the command in a code box.  then it will NOT change the " ".

https://discourse.stonehearth.net/t/discourse-guide-code-formatting/30587

-------------------------

sol | 2022-12-19 02:14:52 UTC | #14

Thanks for the tip! I updated the original post and the quotes should be correct now.

-------------------------

sol | 2022-12-23 05:27:46 UTC | #15

@vilkris has submitted some code changes for znn_cli_dart, primarily updating the way preimages are generated.
I've tested all htlc functions again and everything is working well.

Still requesting community feedback :)

-------------------------

vilkris | 2022-12-23 11:03:29 UTC | #16

I think the change I made to use hex encoding for the preimage now makes the Dart CLI and the C# CLI incompatible with each other. @CryptoFish would you mind taking a look if you have any thoughts on that?

-------------------------

sol | 2022-12-23 20:10:19 UTC | #17

A quick check that I did indicates that both CLIs are mostly compatible, though the user experience is not entirely the same.

Main issue
- Dart CLI now generates a 64-char preimage, exceeding C# CLI's htlc.KeyMaxSize of 32 to unlock an htlc. If this check is removed or updated, both CLIs should be able to unlock HTLCs created with the other application.

Other differences
- Dart CLI's createHash does not allow users to enter their own preimage.
- Dart CLI's htlc.create auto-generates a random preimage, while C# CLI allows users to enter their own. The resulting hashlocks are still calculated the same way.
- Dart CLI's monitor function auto-reclaims expired HTLCs.
- Dart CLI does not require a chainId parameter to be passed with the command
- Dart CLI creates HTLCs based on the node's time instead of relying on the user's local time.

I probably missed some stuff. This will require some more interoperability testing.

-------------------------

CryptoFish | 2022-12-25 14:48:29 UTC | #18

The `KeyMaxSize` can be specified when creating the htlc. The default `KeyMaxSize` is 32.

`znn-cli htlc.create --help`

``` Powershell
  hashLockedAddress (pos. 1)              Required.
  tokenStandard (pos. 2) [ZNN/QSR/ZTS]    Required.
  amount (pos. 3)                         Required.
  expirationTime (pos. 4)                 Required. Total seconds from now.
  hashLock (pos. 5)                       Required. The hash lock as a hexidecimal string.
  hashType (pos. 6)                       (Default: 0) 0 = SHA3-256, 1 = SHA-256
  keyMaxSize (pos. 7)                     (Default: 32) Maximum size of the pre-image.
```

When unlocking the htlc, the `KeyMaxSize` is checked in the CLI, but enventually also in the htlc contract.

> I think the change I made to use hex encoding for the preimage now makes the Dart CLI and the C# CLI incompatible with each other.

The `hashlock` argument of the `htlc.create` command accepts a hex encoded string. Is it the size of the preimage or the format causing the incompatibality?

Or is it because the Dark CLI's htlc.create auto.generates a random preimage with a 64-char preimage?

I haven't had the time to look into the Dart htlc implementation yet, but it would be nice to have an consensus on the preferred implementation.

-------------------------

vilkris | 2023-01-03 11:02:47 UTC | #19

[quote="CryptoFish, post:18, topic:1166"]
When unlocking the htlc, the `KeyMaxSize` is checked in the CLI, but enventually also in the htlc contract.
[/quote]
Isn't the `KeyMaxSize` in the embedded contract referring to byte array length, not string length? This is where the incompatibility stems from with the Dart CLI. The C# CLI checks the preimage string length, not the preimage length as a byte array. Also, the C# CLI doesn't handle the preimage input as a hex string when unlocking the HTLC.

In my opinion the user should not be allowed to specify their own preimage because of safety reasons. In the C# CLI you can use a preimage of any length but you'd have to manually set the `KeyMaxSize` when creating the HTLC if the preimage length is over 32 bytes. This wouldn't be an issue if the client generates the preimage.

Maybe the user could specify an optional `KeySize` argument instead of  `KeyMaxSize` which would create a preimage of that size and set the  `KeyMaxSize` accordingly when creating the HTLC.

In the Dart CLI there's a hardcoded variable `int hashLockLength = 32;` which is used to set `KeyMaxSize` when creating the HTLC. This is misleading as we're setting the max length of the preimage, not the hashlock length.

-------------------------

CryptoFish | 2023-01-04 15:46:52 UTC | #20

[quote="vilkris, post:19, topic:1166"]
Isn’t the `KeyMaxSize` in the embedded contract referring to byte array length, not string length?
[/quote]
Correct, the `KeyMaxSize` is referring to the byte array length of the array.

[quote="vilkris, post:19, topic:1166"]
The C# CLI checks the preimage string length, not the preimage length as a byte array. Also, the C# CLI doesn’t handle the preimage input as a hex string when unlocking the HTLC.
[/quote]
The `htlc.unlock` does this indeed. This will need to be changed.

[quote="vilkris, post:19, topic:1166"]
In my opinion the user should not be allowed to specify their own preimage because of safety reasons. In the C# CLI you can use a preimage of any length but you’d have to manually set the `KeyMaxSize` when creating the HTLC if the preimage length is over 32 bytes. This wouldn’t be an issue if the client generates the preimage.
[/quote]
In the case of the Atomic Swap scenario Bob needs to create an htlc with a hashlock that already exists. How would Bob be able to supply the hashlock if the htlc.create command generates the preimage?

According to @georgezgeorgez the `KeyMaxSize` was introduced to prevent [Secret Size Attacks](https://gist.github.com/markblundeberg/7a932c98179de2190049f5823907c016). It puts a guarantee on max size of the unlock tx. For other networks there is tx size limit. We have to pay plasma per byte. 
So the bounded size ensures that Bob knows he’ll be able to redeem his, if Alice redeems hers.

-------------------------

vilkris | 2023-01-05 20:15:08 UTC | #21

[quote="CryptoFish, post:20, topic:1166"]
In the case of the Atomic Swap scenario Bob needs to create an htlc with a hashlock that already exists. How would Bob be able to supply the hashlock if the htlc.create command generates the preimage?
[/quote]

In the Dart CLI the htlc.create command has an optional hashlock parameter. If it's provided it'll use that as the hashlock and won't generate a preimage.

[quote="CryptoFish, post:20, topic:1166"]
According to @georgezgeorgez the `KeyMaxSize` was introduced to prevent [Secret Size Attacks](https://gist.github.com/markblundeberg/7a932c98179de2190049f5823907c016). It puts a guarantee on max size of the unlock tx. For other networks there is tx size limit. We have to pay plasma per byte.
So the bounded size ensures that Bob knows he’ll be able to redeem his, if Alice redeems hers.
[/quote]
Thanks for the context, wasn't aware of this. Looks like it's best to add an optional KeyMaxSize param to the htlc.create command in the Dart CLI as well.

-------------------------

CryptoFish | 2023-01-05 20:55:21 UTC | #22

[quote="vilkris, post:21, topic:1166"]
In the Dart CLI the htlc.create command has an optional hashlock parameter. If it’s provided it’ll use that as the hashlock and won’t generate a preimage.
[/quote]

Right, got it. I'll update the C# CLI accordingly and remove the incompatibility issues.

-------------------------

sol | 2023-01-06 18:28:54 UTC | #23

[quote="vilkris, post:19, topic:1166"]
In the Dart CLI there’s a hardcoded variable `int hashLockLength = 32;` which is used to set `KeyMaxSize` when creating the HTLC. This is misleading as we’re setting the max length of the preimage, not the hashlock length.
[/quote]

I'll update this, but I think we should also [check the length of the hashLock](https://github.com/Big-Inches-Club-House/go-zenon/blob/htlc/vm/embedded/implementation/htlc.go#L25).

The variables htlcPreimageMinLength (32) and htlcPreimageMaxLength (32) aren't enforced in either znn_sdk_dart or go-zenon. I was able to create a 99-byte preimage and unlock an HTLC with it.

Any suggestions for lower/upper boundaries or should we enforce 32/32?

-------------------------

CryptoFish | 2023-01-07 11:22:47 UTC | #24

I don't see the problem with the [check the length of the hashLock](https://github.com/Big-Inches-Club-House/go-zenon/blob/htlc/vm/embedded/implementation/htlc.go#L25).

The `hashLock` length is determined by the output size of the `hashType`. Both hash types supported use a 256 bit output size. The `hashLock` is not valid if it does not equal 32 bytes in length.

[quote="sol, post:23, topic:1166"]
Any suggestions for lower/upper boundaries or should we enforce 32/32?
[/quote]

How the preimage is generated is determined by the implementation of the calling application. I'm not sure what the benefits would be by enforcing its length.

The Dart CLI htlc.unlock command uses an extra hashType argument to do a preimage check. Wouldn't it be easier to just use the `hashType` already available in the retrieved htlc object?

-------------------------

sol | 2023-01-07 13:14:37 UTC | #25

[quote="CryptoFish, post:24, topic:1166"]
I don’t see the problem with the [check the length of the hashLock ](https://github.com/Big-Inches-Club-House/go-zenon/blob/htlc/vm/embedded/implementation/htlc.go#L25).
[/quote]

Right, no issues in go-zenon. I should have specified -- I'd like to add matching client-side input validation in znn_cli_dart and syrius.

[quote="CryptoFish, post:24, topic:1166"]
How the preimage is generated is determined by the implementation of the calling application.
[/quote]

We probably don't want to allow weak preimages; I'd imagine some actors will try to bruteforce active swaps.
I guess we don't need to enforce the limit in the protocol (go-zenon) but it could help to do so in order to align all SDK/client applications with the same rule.

[quote="CryptoFish, post:24, topic:1166"]
Wouldn’t it be easier to just use the `hashType` already available in the retrieved htlc object?
[/quote]

Yes, it would be easier but I found that is error-prone. If a user submits a pre-generated SHA-256 hashlock but forgets to enter the type in htlc.create, their type will default to 0. This optional flag in hltc.unlock allows them to recover the funds without having to wait for the swap to expire.

-------------------------

CryptoFish | 2023-01-07 14:25:21 UTC | #26

[quote="sol, post:25, topic:1166"]
Right, no issues in go-zenon. I should have specified – I’d like to add matching client-side input validation in znn_cli_dart and syrius.
[/quote]

Doesn't this already happen when creating the `hash` object from the Zenon Sdk which indirectly enforces the length of the hashLock. The `parse` and `fromBytes` methods perform a validation on the length.

[quote="sol, post:25, topic:1166"]
We probably don’t want to allow weak preimages; I’d imagine some actors will try to bruteforce active swaps.
I guess we don’t need to enforce the limit in the protocol (go-zenon) but it could help to do so in order to align all SDK/client applications with the same rule.
[/quote]

Whether weak preimages are used depends on the client implementation. It makes sense to make recommendations on how to generate preimages. Also users of x client need to know that the preimages the client generates are considered secure. This should prevent weak preimages from being created, unless one creates them directly using the sdk.

Enforcing the limit in the client won't stop someone from bruteforce active swaps. Again, one could easily use the sdk directly.

I guess if it makes sense to enforce the limits it has to be done in the protocol.

[quote="sol, post:25, topic:1166"]
Yes, it would be easier but I found that is error-prone. If a user submits a pre-generated SHA-256 hashlock but forgets to enter the type in htlc.create, their type will default to 0. This optional flag in hltc.unlock allows them to recover the funds without having to wait for the swap to expire.
[/quote]

I see, good thinking.

-------------------------

sol | 2023-01-07 15:30:18 UTC | #27

[quote="CryptoFish, post:26, topic:1166"]
Doesn’t this already happen when creating the `hash` object from the Zenon Sdk which indirectly enforces the length of the hashLock. The `parse` and `fromBytes` methods perform a validation on the length.
[/quote]

I checked the code again; you're probably right and doing a client-side length check seems redundant.

[quote="CryptoFish, post:26, topic:1166"]
Also users of x client need to know that the preimages the client generates are considered secure.
[/quote]

Just want to be sure we're all on the same page.
The protocol and SDKs will not have any preimage length restrictions.
Clients like znn-cli and syrius will impose min/max preimage lengths.

What should the min/max be? I was assuming 32/32 until yesterday.

-------------------------

CryptoFish | 2023-01-07 17:17:52 UTC | #28

[quote="sol, post:27, topic:1166"]
Just want to be sure we’re all on the same page.
[/quote]

We're on the same page :slight_smile: 

I personally don't think the limits add much, but if we add them 32/32 seems like the most sensible limit.

-------------------------

CryptoFish | 2023-01-08 11:36:40 UTC | #29

[quote="sol, post:25, topic:1166"]
Yes, it would be easier but I found that is error-prone. If a user submits a pre-generated SHA-256 hashlock but forgets to enter the type in htlc.create, their type will default to 0. This optional flag in hltc.unlock allows them to recover the funds without having to wait for the swap to expire.
[/quote]

Let me get back on this one. The htlc unlock contract creates a SHA3-256 hashlock of the supplied preimage which will never match the SHA-256 hashlock. So I fail to see how someone could recover the funds without having to wait for the swap to expire.

```
// Alice creates a SHA-256 hash
znn-cli createHash 1
```

Preimage: c770b3160b83f6e3a7e45e961da8aaafbdc1557bb2f4dee3ae16d370e10fe16d
Hash: 3b6e7bfafa188dff9f50b12be1143c751653453a27097cd297f2f283e7e804f3

```
// Alice creates a htlc with a pre-generated SHA-256 hashlock, but forgets to specify the hashtype
znn-cli htlc.create z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 ZNN 100 3600 3b6e7bfafa188dff9f50b12be1143c751653453a27097cd297f2f283e7e804f3 -k Alice
```

Creating htlc with amount 100,00000000 tZNN
   Can be reclaimed in 01:00:00 by z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7
   Can be unlocked by z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 with hashlock 3b6e7bfafa188dff9f50b12be1143c751653453a27097cd297f2f283e7e804f3 hashtype 0
Done

```
// Bob checks the hash locked htlc's
znn-cli htlc.hashLocked -k Bob
```

Htlc id b1fdbd1888a689538587d273b18778bc26ae2dc8387669da8bad29c80ead4cb0 with amount 100,00000000 tZNN
   Can be reclaimed in 00:59:24 by z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7
   Can be unlocked by z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 with hashlock 3b6e7bfafa188dff9f50b12be1143c751653453a27097cd297f2f283e7e804f3 hashtype 0

```
// Bob unlocks the htlc and specifies the correct hash type.
znn-cli htlc.unlock b1fdbd1888a689538587d273b18778bc26ae2dc8387669da8bad29c80ead4cb0 c770b3160b83f6e3a7e45e961da8aaafbdc1557bb2f4dee3ae16d370e10fe16d 1 -k Bob
```

Unlocking htlc id b1fdbd1888a689538587d273b18778bc26ae2dc8387669da8bad29c80ead4cb0 with amount 100,00000000 tZNN
Done
Use receiveAll to collect your htlc amount after 2 momentums

```
// Bob checks the hash locked htlc's and notices the htlc is not unlocked by the contract
znn-cli htlc.hashLocked -k Bob
```

Htlc id b1fdbd1888a689538587d273b18778bc26ae2dc8387669da8bad29c80ead4cb0 with amount 100,00000000 tZNN
   Can be reclaimed in 00:57:20 by z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7
   Can be unlocked by z1qpsjv3wzzuuzdudg7tf6uhvr6sk4ag8me42ua4 with hashlock 3b6e7bfafa188dff9f50b12be1143c751653453a27097cd297f2f283e7e804f3 hashtype 0

-------------------------

vilkris | 2023-01-08 12:02:09 UTC | #30

[quote="sol, post:23, topic:1166"]
htlcPreimageMinLength (32) and htlcPreimageMaxLength (32)
[/quote]
Where are these variables?

[quote="sol, post:27, topic:1166"]
Just want to be sure we’re all on the same page.
The protocol and SDKs will not have any preimage length restrictions.
Clients like znn-cli and syrius will impose min/max preimage lengths.

What should the min/max be? I was assuming 32/32 until yesterday.
[/quote]
The HTLC embedded contract stores the `KeyMaxSize` variable in a `uint8` so the max preimage length the protocol supports is 255 bytes. I think that should be enforced by clients. There's no min preimage length and I'm not sure if there's much benefit in enforcing one client-side.

-------------------------

sol | 2023-01-08 16:23:18 UTC | #31

[quote="CryptoFish, post:29, topic:1166"]
`// Bob checks the hash locked htlc's and notices the htlc is not unlocked by the contract`
[/quote]

Was this with Dart CLI or C# CLI?

[quote="vilkris, post:30, topic:1166"]
Where are these variables?
[/quote]

In [go-zenon](https://github.com/Big-Inches-Club-House/go-zenon/blob/0cd866f3dba69064651187d0335998b59babfe24/vm/constants/embedded.go#L84) and [znn_sdk_dart](https://github.com/Sol-Sanctum/znn_sdk_dart/blob/spork_htlc/lib/src/embedded/constants.dart#L57).

[quote="vilkris, post:30, topic:1166"]
I’m not sure if there’s much benefit in enforcing one client-side.
[/quote]

What's your ideal default user experience for znn-cli and syrius?

Should znn-cli permit 0/255, default 32?
And should syrius present similar options?

-------------------------

CryptoFish | 2023-01-08 17:58:33 UTC | #32

[quote="sol, post:31, topic:1166"]
Was this with Dart CLI or C# CLI?
[/quote]

I tried both

Also, I get the following error when using the `verbose` flag.


```
Unhandled exception:
Unsupported operation: Please set "hierarchicalLoggingEnabled" to true if you want to change the level on a non-root logger.
#0      Logger.level= (package:logging/src/logger.dart:123)
#1      initZnn (file:///d:/repos/sol-sanctum/znn_cli_dart/init_znn.dart:137)
#2      main (file:///d:/repos/sol-sanctum/znn_cli_dart/cli_handler.dart:17)
#3      _delayEntrypointInvocation.<anonymous closure> (dart:isolate-patch/isolate_patch.dart:295)
#4      _RawReceivePortImpl._handleMessage (dart:isolate-patch/isolate_patch.dart:192)
```

-------------------------

sol | 2023-01-09 00:06:45 UTC | #33

I've pushed [some changes to my repo](https://github.com/zenon-network/znn_cli_dart/commit/62d16f3a5a368d4c3a9489f62bd16bb535a74cf8). 
The `verbose` parameter should work now, though I haven't tested this thoroughly.

As for the scenario you pointed out, you're right.[ It won't work](https://github.com/Big-Inches-Club-House/go-zenon/blob/0cd866f3dba69064651187d0335998b59babfe24/vm/embedded/implementation/htlc.go#L256).
I've adjusted the htlc.unlock function accordingly.

znn-cli: default keyMaxSize = 32, with the possibility of calling `createHash` to generate a preimage of [1, 255] bytes.

-------------------------

CryptoFish | 2023-01-09 10:07:01 UTC | #34

Great work, but there's still a problem with the `htlc.create` function.

The `keyMaxSize` is always `32`, even when supplying a `hashlock` based on a pre-image with a larger size.

Thinking about the `keyMaxSize`. I think it's best to always set it to `255`. The only reason it's there is because of the [Secret Size Attacks](https://gist.github.com/markblundeberg/7a932c98179de2190049f5823907c016). Settings it to the max allowed pre-image size, prevents the attacks and allows the creation of pre-images between `1` and `255`, using a default of `32`.

The following line in the `createHash` function needs to be an or statement; otherwise the condition is never met.
```
if (keyMaxSize > htlcPreimageMaxLength && keyMaxSize < 1) {
```

-------------------------

CryptoFish | 2023-01-09 15:20:36 UTC | #35

Just updated the following work:

* added Spork support to the C# SDK 
* added Spork support to the Java SDK
* removed all incompatibility issues from the C# CLI and matched the impl. of the Dart CLI
* updated the tutorial
* tested all Htlc and Spork commands

-------------------------

sol | 2023-01-09 23:04:48 UTC | #36

[quote="CryptoFish, post:34, topic:1166"]
The following line in the `createHash` function needs to be an or statement
[/quote]

That's embarassing :melting_face: 
Should be fixed by these commits: [SDK](https://github.com/zenon-network/znn_sdk_dart/commit/bb7126bac65731f0acf4db6a3fa526b53462d3f0) and [CLI](https://github.com/zenon-network/znn_cli_dart/commit/05df33c384b1b7ec29b69b0961c1a8ab0ec2eb1b)
I *think* I'm done making changes now.

I think you brought down my devnet with your spork test. :laughing: 
It's back up now.

-------------------------

CryptoFish | 2023-01-10 08:28:24 UTC | #37

Great, looks good to me :+1:

[quote="sol, post:36, topic:1166"]
I think you brought down my devnet with your spork test. :laughing:
It’s back up now.
[/quote]

Yeah, I thought that might be the case . That means the activation worked 😄

I will try to be more carefull next time :sweat_smile:

-------------------------

vilkris | 2023-01-10 21:09:29 UTC | #38

[quote="sol, post:31, topic:1166"]
What’s your ideal default user experience for znn-cli and syrius?

Should znn-cli permit 0/255, default 32?
And should syrius present similar options?
[/quote]

I guess the CLI can permit anything between 0-255 but for Syrius I'm not sure. For ZTS <> ZTS swaps the 32 byte preimage should be fine and not something the user needs to care about but for cross-chain swaps the length might have to be specified by the user.

-------------------------

vilkris | 2023-01-11 21:39:00 UTC | #39

[quote="sol, post:31, topic:1166"]
In [go-zenon ](https://github.com/Big-Inches-Club-House/go-zenon/blob/0cd866f3dba69064651187d0335998b59babfe24/vm/constants/embedded.go#L84) and [znn_sdk_dart](https://github.com/Sol-Sanctum/znn_sdk_dart/blob/spork_htlc/lib/src/embedded/constants.dart#L57).
[/quote]

Maybe I missed something but what is the purpose of these variables in go-zenon?

-------------------------

sol | 2023-01-11 21:48:13 UTC | #40

I don't think they're being used in go-zenon.

-------------------------

CryptoFish | 2023-02-22 11:01:15 UTC | #41

About the Spork implementation.

Creating and activating Sporks using the SDK is probably a very unlikely scenerio. This would bypass community-activated Sporks and only one wallet owner would be able to actually use it.

The ZIP process states the following.

> Since the original Spork address to create and activate Sporks is hardcoded in the genesis file, it would have to be changed to a different address so that it can be used by the community to create and activate Sporks.
> 
> Accelerator Z already has some functionality to create transactions based on votes. Therefore, the community proposes to change that hardcoded Spork creation address to Accelerator Z contract address.
> 
> This would allow us to then change the Spork Contract so that **only the AZ address** can create and activate Sporks.
> 
> Then we can modify the conditional logic of the AZ contract to something like
> 
> *"When Pillars vote and certain thresholds are met, then the contract sends a transaction to the spork contract to create or activate Sporks."*
> 
> This would give us community-activated Sporks that can be used for Soft and Hard Forks right from the S Y R I U S wallet through the Accelerator Z tab.

There would be no need for the contract methods if the Accelerator Z contract is used for the creation and activation of sporks. Only the API `getAll` method would be usefull.

-------------------------

sol | 2023-04-27 03:52:36 UTC | #42

[quote="CryptoFish, post:41, topic:1166"]
Creating and activating Sporks using the SDK is probably a very unlikely scenerio.
[/quote]

This is true on mainnet. It could be used on other networks.
If you feel strongly about not including it in the znn-cli, I can remove it before submitting my PR.

---

I haven't been able to confirm that any SDKs will be updated to support the new bridge and liquidity functions, so I've [started the implementation in Dart](https://github.com/Sol-Sanctum/znn_sdk_dart/tree/bridge_liquidity).
I hope to finish this in a few weeks.

If anyone wishes to assist, send me a DM.

-------------------------

sumamu | 2023-04-27 05:11:37 UTC | #43

[quote="sol, post:42, topic:1166"]
I’ve [started the implementation in Dart](https://github.com/Sol-Sanctum/znn_sdk_dart/tree/bridge_liquidity).
[/quote]

Awesome! 

Indeed, we haven't used nor updated the Dart SDK, our focus was on the GO and TS SDKs.

-------------------------

CryptoFish | 2023-04-27 11:01:49 UTC | #44

I've kept the Spork implementation in the latest release, maybe we'll need to change it once Spork governance is in place.

I've also started looking at the bridge implementation. Maybe we can coordinate the cli impl. to keep it in line with eachother.

-------------------------

aliencoder | 2023-07-01 16:35:53 UTC | #45

Updated the [Dart CLI](https://github.com/alienc0der/znn_cli_dart/releases/tag/master):

- Added `chainId` option
- Added `BigInt` support
- Updated dependencies

[quote="CryptoFish, post:44, topic:1166"]
I’ve also started looking at the bridge implementation. Maybe we can coordinate the cli impl. to keep it in line with eachother.
[/quote]

Feel free to open a PR (please target the `master` branch).

-------------------------

sol | 2023-07-01 16:55:30 UTC | #46

I updated the Dart CLI and SDK as well, based on your BigInt-supporting branches.

[Dart SDK](https://github.com/Sol-Sanctum/znn_sdk_dart/tree/wip/v0.0.5)
- Added support for HTLC, Spork, Bridge, Liquidity contracts

Dart [znn-cli](https://github.com/Sol-Sanctum/znn_cli_dart/tree/wip_v0.0.5)
- Refactored to align with the [C# znn-cli](https://github.com/KingGorrin/znn_cli_csharp)
- Added support for HTLC, Spork, Bridge, Liquidity contracts
- Added admin-only functionality (Bridge/Liquidity)
- Added ability to donate to AZ and query Stats RPC
- Added chainId option (default, auto, manual)
- Updated menu

-----------

I'm waiting for Mr Kaine to accept the existing Dart SDK and Syrius PRs before submitting my work. In the future, we should develop a process that doesn't rely on his quiet, opaque reviewing methods. He doesn't even announce when he refuses work; we have to infer it from his silence.

The community needs to manage this in a more transparent, iterative, collaborative manner. HyperCore One is already working on this.

-------------------------

