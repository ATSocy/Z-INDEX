Thread: zenon-sdk-status
romeo | 2023-02-08 18:58:29 UTC | #1

Status tracking for SDKs under development or yet to be started:

|Language|Status|Owner|Link|ETA|Updated|Comments|
|---|---|---|---|---|---|---|
| Javascript/typescript | Done | @alien-valley.io | [Github](https://github.com/alien-valley/znn.js) | | 28/11/22 |
| Rust | 80% | @2bonahill | [Github](https://github.com/2bonahill/znn_sdk_rust)|TBD| 29/11/22| Requested update
|Go | Done | @georgezgeorgez, @MoonBaZe | [Github](https://github.com/MoonBaZZe/znn-sdk-go) | | 28/11/22
Java | Done | @CryptoFish | [Github](https://github.com/KingGorrin/znn_sdk_java) | | 28/11/22
| Kotlin | 99% | @Chace | [Github](https://github.com/ItsChaceD/zenon-android) | | 12/12/22 | Needs Publishing to Maven Central
| C/C++ | 20% | NEED DEV | [Github](https://github.com/dumeriz/zenon-sdk-cpp) | | 29/11/22 | On Hold. NEED DEV
| Python | 100% | @roymiller | [Github](https://github.com/millerships/pyznn) | | 28/11/22 |
|Swift | 90% | @Chace | [Github](https://github.com/ItsChaceD/zenon-android) | 31/12/22 | 12/12/22 | Needs Websocket & RPC features & Publishing to SPM
| C# |100% | @CryptoFish | [Github](https://github.com/KingGorrin/znn_sdk_csharp) | | 28/11/22 |
| Common Lisp | 50% | NEED DEV | [Github](https://github.com/dumeriz/cl-zenon) | TBD | 29/11/22 | On Hold? NEED DEV
| Typescript | 100% | @dexter703 | [Github](https://github.com/DexterLabZ/znn.ts) | | 29/11/22 |

-------------------------

Dumeril | 2022-05-01 07:10:00 UTC | #2

C/C++ has been started
https://github.com/dumeriz/zenon-sdk-cpp

Common Lisp (not on the list) has been started (rpc side complete)
https://github.com/dumeriz/cl-zenon

-------------------------

Dumeril | 2022-05-01 07:29:10 UTC | #3

As a side note: having a c++ sdk means that a c-sdk is easy to add. Having a C sdk means support for most languages is easy to add because most languages have support for ffi with C libraries. 
The C++ sdk I began is at a point where it’s trivial to complete the rpc part of api. 
I welcome every help; but note that it’s under gplv3 license and I won’t submit it as an az application.

-------------------------

CryptoFish | 2022-05-02 06:34:21 UTC | #4

I would like to do a throw at a C# implementation of the sdk. I've setup a repository at https://github.com/KingGorrin/znn_sdk_csharp. Will commit initial work when basic functionalities are working and I'll try to follow the dart implementation as much as possible.
Will keep a close eye on other sdk Interpretations as I go along. Feel free to join if you want to help out.

-------------------------

romeo | 2022-05-04 07:11:50 UTC | #5

I've made the top post a wiki post which means anyone should be able to edit, so feel free to update with ETAs or completion status as you see fit @devs

-------------------------

alien-valley.io | 2022-05-04 08:16:16 UTC | #6

Feel free to add a link to the [znn.js](https://github.com/alien-valley/znn.js) SDK
It's not part of any AZ project, but on warpdrive

No ETA ATM and I'm not sure about completion %
Will come w/ more info when available

-------------------------

romeo | 2022-05-18 05:28:14 UTC | #7



-------------------------

romeo | 2022-05-18 05:29:05 UTC | #8

@devs don't forget to jump into the main post here and edit the details and status of your SDK when appropriate and please reach out to the forum community if you need any assistance

-------------------------

2bonahill | 2022-05-20 10:45:26 UTC | #9

Hi. Rust Zenon SDK Phase 1 close to finished. Some last testing happening. Pushed the code. Check it out.

-------------------------

CryptoFish | 2022-05-25 15:04:46 UTC | #10

Implemented 100% functionality of the Zenon .NET SDK. Will try to work towards 100% code coverage and eliminate remaining bugs. All major functions are tested and working.

-------------------------

roymiller | 2022-06-01 20:08:18 UTC | #11

Quick update: Added python repo link. Got through one of the difficult parts of the package, wallet key management. Ensured that my testcases passed the testcases from znn.js and znn_sdk_rust repos.

-------------------------

2bonahill | 2022-06-02 18:32:50 UTC | #12

phase 1 complete. started with pase 2.

-------------------------

CryptoFish | 2022-06-10 13:48:55 UTC | #13

Phase 1 of the Zenon Java SDK has been completed and committed to the GitHub repository.

-------------------------

roymiller | 2022-06-15 06:34:46 UTC | #14

Quick update: Most of the non-trivial core functionalities are done in Python SDK. Working on the right way to create ABI class (playing with eth-abi package) right now to make contract calls. 

Once that is done, I'll start with documentation.

-------------------------

CryptoFish | 2022-06-24 07:01:34 UTC | #15

Phase 2 of the Zenon Java SDK has been completed and committed to the GitHub repository.

-------------------------

0x3639 | 2022-06-24 10:18:46 UTC | #16

@romeo Should we update the summary to 100%.  We have Java and Kotlin on that line.  Do we need to break those out?

-------------------------

CryptoFish | 2022-06-24 10:18:25 UTC | #17

Maybe better to break everything up. Also the go-sdk owner and url info is missing.

-------------------------

roymiller | 2022-06-24 10:30:06 UTC | #18

Okay! I've covered all major functionalities in python sdk now. Will add documentation over the weekend.

-------------------------

romeo | 2022-06-25 22:24:03 UTC | #19

yeah feel free to edit the main post - its a wiki post so most members should be able to edit it themselves.

-------------------------

DrD3 | 2022-06-26 04:58:45 UTC | #20

I edited the Golang's section linking MoonBaZe's github since he picked up from where Georgie left off. @MoonBaZe is the SDK complete? Could you edit the post here if/when you're done?

-------------------------

MoonBaZe | 2022-06-26 13:55:50 UTC | #21

The Go SDK is 100% completed. I will continue to work on it and improve it of course. I edited and put 100% but it does now show up.

-------------------------

DrD3 | 2022-06-26 20:27:01 UTC | #23

Fixed that bit for ya but that is amazing!!!

-------------------------

0x3639 | 2022-06-27 21:26:51 UTC | #24

I broke out Kotlin. I think @Chace is working on it.  I'll update.  Sir I assumed you were 35% compete based on your progress as reported in github.  

https://forum2.zenon.org/t/capacitor-plugin-w-native-mobile-sdks/531

-------------------------

roymiller | 2022-06-28 11:33:23 UTC | #25

The first version of pyznn is published. Check out the Github repo and docs. Feel free to leave feedback or new request.

I’ve worked on both phases in the last 3-4 weeks. Here’s documentation: [PyZNN Docs](https://millerships.github.io/pyznn/)

PS: I like making designs, so went ahead and added some illustrations on home page

-------------------------

CryptoFish | 2022-07-12 10:20:46 UTC | #26

Phase 3 of the Zenon Java SDK has been completed and committed to the GitHub repository.

This completes the project with the first version being released.

-------------------------

2bonahill | 2022-08-04 10:45:50 UTC | #27

Hi everyone. Sorry for the delay, i am finally back in the game. Had some personal and private issues which needed my full attention. Now i am back in action and i have picked up the Rust SDK work again. Phase 2 will be complete zoon. Keep you posted.

-------------------------

0x3639 | 2022-08-28 11:09:09 UTC | #28

All SDKs reported above have been mirrored offsite

https://git.0x3639.com/?repo-search-tab=organizations

-------------------------

dat_she_pepe | 2022-10-06 01:32:06 UTC | #29

Any updates on this ?

-------------------------

CryptoFish | 2022-11-10 08:04:58 UTC | #30

You can add https://github.com/KingGorrin/znn_cli_csharp to the offsite repo backup list.

-------------------------

0x3639 | 2022-11-10 19:17:38 UTC | #31

will do!!

-------------------------

0x3639 | 2022-11-10 19:23:04 UTC | #32

All set

https://git.0x3639.com/KingGorrin/znn_cli_csharp

-------------------------

aliencoder | 2022-11-13 21:30:18 UTC | #33

What is the status with the Kotlin SDK?

-------------------------

0x3639 | 2022-11-14 10:44:47 UTC | #34

@Chace just wanted to ping you on this question from Alien Coder.  

Update: I posted an issue on github asking for an update.  https://github.com/ItsChaceD/zenon-android/issues/1

-------------------------

aliencoder | 2022-11-22 22:29:39 UTC | #35

It would be [very nice](https://kotlinlang.org/lp/mobile/) to have a Kotlin SDK.

-------------------------

zyler9985 | 2022-11-23 03:36:32 UTC | #36

Any idea what's going on with Dumeril's two SDKs he started? I'm not sure if he is just taking a break or has left community, or if he mentioned to anyone about someone taking over them.

-------------------------

cryptocheshire | 2022-11-23 07:10:43 UTC | #37

it seems like he left

-------------------------

CryptoFish | 2022-11-28 19:36:46 UTC | #39

Zenon Sdk and Cli for .NET and Zenon Sdk for Java have been updated to reflect recent htlc api changes.

-------------------------

aliencoder | 2022-11-28 23:36:15 UTC | #40

I think we should update the status of each SDK to reflect current progress and reevaluate what languages we should focus on.

-------------------------

0x3639 | 2022-11-28 23:41:25 UTC | #41

Good idea.  I'm happy to start that.  Maybe someone else can help out?  I think @romeo created the list.  I can work top down and will add an updated column.

-------------------------

0x3639 | 2022-11-29 00:27:02 UTC | #42

@2bonahill we are in the process of updating the status of all SDKs. Would you be willing to give us a quick update?

https://github.com/2bonahill/znn_sdk_rust/issues/2

https://zenon.tools/accelerator/2acf48da2bcc420b4d997299807d8b50b4229871214069c9afc39bdad0e27a76

-------------------------

0x3639 | 2022-11-29 02:02:26 UTC | #43

I cleaned everything up.  I'll start contacting more devs for an update tomorrow.

-------------------------

0x3639 | 2022-11-29 14:15:20 UTC | #44

I reached out to @Dumeril on TG for an update on lisp and C/C++.  Some time ago he gracefully bowed out of the community.  I suspect these are on hold, but let's see if he gives us an update.

-------------------------

aliencoder | 2022-11-29 15:00:02 UTC | #45

I would also add Dexter's [Typescript SDK](https://github.com/DexterLabZ/znn.ts) to the list.

-------------------------

0x3639 | 2022-11-29 15:15:19 UTC | #46

Just added and did another update.  We are waiting for feedback from @Dumeril @2bonahill and @Chace 

- Rust looks to be through phase 3 of 5 phases.  Update requested  
- I've heard that Chace is still working but not 100% sure.
- Dumeril bowed out a few months ago unfortunately and I think someone will need to pick up C/C++ and Lisp. But I've asked for an update on TG.

-------------------------

0x3639 | 2022-11-29 19:42:55 UTC | #47

I updated the list. Looks like Dumeril has confirmed he stopped work on lisp and C/C++.  We need to find a new developer to pick up that work.

-------------------------

Chace | 2022-12-13 17:15:58 UTC | #48

Here is the Kotlin SDK: https://github.com/ItsChaceD/zenon-android. 

Note this is primarily developed for use with Android / Native. If you want to use it with Kotlin multiplatform, some additional logic may be needed to be implemented.

-------------------------

0x3639 | 2022-12-14 12:14:54 UTC | #49

Looks like you update the table.  Thank you!!

-------------------------

aliencoder | 2022-12-14 20:20:59 UTC | #50

Nice. I think we should try to target multi-platform, but it's good that we have the foundation.

-------------------------

Chace | 2022-12-15 01:32:55 UTC | #51

My proposal will allow for multi-platform development with web technologies through the use of Capacitor. This will allow for any web app (new or existing) to be deployed to web, Android, and iOS without any additional logic. It also is language agnostic, so you can use any web framework (Angular, React, Vue, etc.). 

The Capacitor plugin that I'm developing will do all of the logic under the hood based on the platform that the device is running. For example, if the user is on Android, the Capacitor plugin will utilize native technologies by routing into the Kotlin SDK. If the user is on iOS, it will automatically utilize the Swift SDK.

The reason for not targeting Kotlin multi-platform is:
1. Can't deploy to the web.
2. Although some of the business logic is shared, you would still need to write the UI separately on Android and iOS.
3. It is likely that the platform-specific implementation for features like Cryptography functions (SHA 3, Ed25519, Argon2), JSON RPC 2.0, Websockets, etc would need to be re-written in Swift anyways.
4. The Capacitor plugin relies on SDKs that target native Android & iOS.

-------------------------

zyler9985 | 2023-02-08 17:54:41 UTC | #52

Bump. Looks like we still have unfinished SDKs ...

-------------------------

mehowbrainz | 2023-02-08 18:56:11 UTC | #53



-------------------------

mehowbrainz | 2023-02-08 18:57:31 UTC | #54



-------------------------

mehowbrainz | 2023-03-15 22:25:31 UTC | #55

What do SDK developers think of implementing a developers.zenon.org using the [Readme.com](https://readme.com/documentation) platform?

Developers would have access to maintain their technical documentations in a space optimized for it. Common documentation patterns for SDKs.

Example: https://developers.intercom.com/intercom-api-reference/reference/identifyadmin

Been seeing many developer portals use this platform.

[poll type=multiple results=always min=1 max=1 chartType=bar]
* Yay
* Nay
[/poll]

-------------------------

DrD3 | 2023-04-30 20:01:58 UTC | #56

Hey Toby hope you're keeping well! Is there any update on the Rust SDK- I remember it was near completion last time-round?

-------------------------

aliencoder | 2023-05-17 18:22:27 UTC | #57

I'm updating the Dart SDK to support `BigInt`. It's almost ready.

-------------------------

aliencoder | 2023-06-07 12:18:51 UTC | #58

The Dart SDK has `BigInt` support now.

-------------------------

CryptoFish | 2023-06-09 07:30:46 UTC | #59

Why are the `usedPlasma` and `basePlasma` converted to string in the `toJson` method, while they are expected to be read as integers?

https://github.com/zenon-network/znn_sdk_dart/blob/2e445add298e841bf5a5bec2e3525e5c77fd0278/lib/src/model/nom/account_block.dart#L28

https://github.com/zenon-network/znn_sdk_dart/blob/2e445add298e841bf5a5bec2e3525e5c77fd0278/lib/src/model/nom/account_block.dart#L43

https://github.com/zenon-network/znn_sdk_dart/blob/2e445add298e841bf5a5bec2e3525e5c77fd0278/lib/src/model/nom/account_block.dart#L61

Also the `AmountUtils` class is not used anymore. Should it be removed?

-------------------------

aliencoder | 2023-06-09 10:27:52 UTC | #60

I moved the `AmountUtils` to Syrius codebase. Applications should handle decimals and precision stuff separately.

I followed @MoonBaZe's `BigInt` implementation.

I returned those values as `String` because maybe we'll treat them as `BigInt` in the future when dynamic Plasma will be implemented. For the moment `int` is enough, but you never know.

-------------------------

aliencoder | 2023-07-01 16:18:57 UTC | #61

Updated [Dart SDK dependencies](https://github.com/alienc0der/znn_sdk_dart/commit/e0b39b696c23ba3cd964df59d743e070b84a5f81) to latest version.

-------------------------

mehowbrainz | 2023-07-06 14:38:12 UTC | #62

[quote="romeo, post:1, topic:414"]
|Swift|90%|@Chace|[Github ](https://github.com/ItsChaceD/zenon-android)|31/12/22|12/12/22|Needs Websocket & RPC features & Publishing to SPM
[/quote]

Is this the link for Swift accurate?

-------------------------

aliencoder | 2023-08-01 21:04:02 UTC | #63

I have fixed the [unit tests](https://github.com/alienc0der/znn_sdk_dart/commit/46d25e61eff70bedf3fc098a1efb88d0501e631e) for the Dart SDK. [I've submitted a PR](https://github.com/zenon-network/znn_sdk_dart/pull/11) containing these changes and the `collection` downgrade for Syrius  `v0.0.7` compatibility.

-------------------------

sol | 2023-09-19 15:40:01 UTC | #64

The Dart SDK has been updated to support the HTLC, Bridge, and Liquidity contracts.

Check out [the PR](https://github.com/zenon-network/znn_sdk_dart/pull/12) for details.

-------------------------

