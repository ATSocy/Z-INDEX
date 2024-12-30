Thread: syrius-improvements
romeo | 2023-02-09 17:36:46 UTC | #1

The BICH DAO newsletter started putting together a list of potential wallet improvements, I thought I would copy those here and add my own suggestions, feel free to add some more even if it's wish list stuff:

There are many improvements to Syrius wallet that can be worked on immediately which will create great value for the entire community.  


- Bugfixes (in general)
- Address Book
- Tooltips/Tutorial
- Autoreceive Options
- Basic NFT Support
- Mobile and QR code support
- Merchant mode/invoicing
- Hide 0 cost transactions from history
- Improve A-Z interface for Pillar owners (introduce a voting table with summary of each projects voting)
- Introduce a hide function in A-Z
- Some form of auto-sign function for messages
- Increase font size/location of total ZNN and QSR in wallet
- Ability to copy wallet balances
- Ability to switch wallets without having to go to settings (gear icon) – perhaps some more accessible dropdown that’s always visible somewhere?
- Show total balances across all addresses
- Claim all delegation rewards from all (relevant) addresses in a single click
- Ledger integration
- More feedback from SYRIUS when spawning Sentinel/Pillar
- Hardware ledger support
- Scrollbar is only visible when hovering over it. It isn’t immediately apparent how to scroll down or up. Especially with a mouse without scrollwheel.
- A way to disable or filter notifications
- Undelegate from all pillars button/can't undelegate from a pillar that has been dismantled (confirmed possible via cli)
- Ability to hide/unhide addresses and sort them by ZNN / QSR balance
- Address whitelisting for auto receive
- Feature to disable s y r i u s automatic behavior of receiving all transactions in order to filter out unsolicited inbound transactions.
- Ability to paste with Command + V on MacOS (currently requires to right click + select paste).
- Introduce a ZIP voting tab in SYRIUS (similar to AZ)

anything else?

-------------------------

sol | 2022-05-26 20:36:43 UTC | #2

Not sure if I'm alone in this, but it would be nice to have more support re: compiling Syrius. If others have encountered issues with the process and found solutions, we could have a sort of FAQ for new devs to consult.

Apart from that, I totally agree with you, there are lots of QoL improvements we can integrate.
One I considered was implementing optional messages in transactions.

-------------------------

OGZenon | 2022-05-26 21:03:36 UTC | #3

- Ability to copy wallet balances
- Ability to switch wallets without having to go to settings (gear icon) -- perhaps some more accessible dropdown that's always visible somewhere?

-------------------------

0x3639 | 2022-05-26 21:14:35 UTC | #4

Better messaging in Sentinel spawning.  It's not 100% clear that once you post QSR you need to close and reopen the Sentinel page in the syrius wallet.

-------------------------

OGZenon | 2022-05-26 21:18:14 UTC | #5

Happens for pillar spawning as well.

-------------------------

shaimo | 2022-05-27 01:40:26 UTC | #6

- Show total balances across all addresses
- Claim all delegation rewards from all (relevant) addresses in a single click
- Ledger integration

-------------------------

0x3639 | 2022-05-27 01:48:18 UTC | #7

[quote="shaimo, post:6, topic:578"]
Claim all delegation rewards from all (relevant) addresses in a single click
[/quote]

This request would be very helpful!

-------------------------

romeo | 2022-05-28 10:27:00 UTC | #8

have updated the main post with all of the suggestions so far, keep them coming

-------------------------

CryptoFish | 2022-05-29 11:33:59 UTC | #9

- Hardware ledger support
- Scrollbar is only visible when hovering over it. It isn't immediately apperent how to scroll down or up. Especially with a mouse without scrollwheel.
- A way to disable or filter notifications

-------------------------

OGZenon | 2022-06-02 14:18:13 UTC | #10

- Ability to paste with Command + V on MacOS (currently requires to right click + select paste).

-------------------------

CryptoFish | 2022-06-02 18:39:38 UTC | #12

- No way to undelegate when the delegating pillar was removed from the pillar list.

-------------------------

OGZenon | 2022-06-02 17:49:21 UTC | #14

What’s a workaround in the meantime out of curiosity?

-------------------------

CryptoFish | 2022-06-02 18:39:14 UTC | #15

You can use the znn-cli tool to undelegate.

-------------------------

romeo | 2022-06-03 00:01:06 UTC | #16

anyone have the cli command handy?

-------------------------

sol | 2022-06-03 00:58:28 UTC | #17

.\znn-cli -u ws://node.zenon.fun:35998 pillar.undelegate -k \<keystore>

-------------------------

CryptoFish | 2022-07-16 14:49:06 UTC | #18

What is the status on the improvements? I've got some time to spare and want to sign up to take some items off the list.

-------------------------

romeo | 2022-07-16 22:36:44 UTC | #19

I'm not sure if any effort has been directed towards Syrius improvements yet, @devs can anyone comment?

-------------------------

Dumeril | 2022-07-17 05:15:43 UTC | #20

@cryptocheshire and I tried to sponsor some improvements to the az tab and general list representation, but the dev that signed up for it is busy with real-life things. Other than that I don’t know about any efforts.

-------------------------

sol | 2022-07-19 03:16:44 UTC | #21

Has anyone compiled it from source? 
I've tried several times on Windows and Linux but haven't been successful yet.

-------------------------

Dumeril | 2022-07-19 15:32:55 UTC | #22

I compiled it on Linux but then there was a problem during runtime; I can’t remember exactly which and haven’t looked into it since, I think after the splash or during login?
What’s your problem?

-------------------------

coinselor | 2022-08-14 00:46:04 UTC | #23

Discussed in telegram, figured I would add it here for reference.

Feature to disable s y r i u s automatic behavior of receiving all transactions in order to filter out unsolicited inbound transactions.

Relevant with what's happening in ETH with Tornado's eth.

-------------------------

cryptocheshire | 2022-08-14 06:39:40 UTC | #24

+ address whitelisting for auto receive

-------------------------

aminazgol | 2022-08-20 06:17:13 UTC | #25

I'm also trying to build Syrius in Ubuntu, but couldn't. I opened an issue on GitHub and would appreciate any help.
https://github.com/zenon-network/syrius/issues/4

-------------------------

Dumeril | 2022-08-20 07:08:00 UTC | #26

@DrBlaze_21  can you share how you did it?

-------------------------

cryptocheshire | 2022-08-20 12:25:12 UTC | #27

Ability to hide/unhide addresses and sort them by ZNN / QSR balance

-------------------------

sol | 2022-08-23 02:41:39 UTC | #28

Hi Amin,
I've [responded to your issue on Github](https://github.com/zenon-network/syrius/issues/4#issuecomment-1223451140) with some tips for compiling Syrius on Linux.
If you're interested in developing on Windows, I've made a post [here](https://forum2.zenon.org/t/syrius-issue-when-building-from-source-on-windows/459/6?u=sol_sanctum).
Hope it helps!


[quote="Dumeril, post:22, topic:578"]
What’s your problem?
[/quote]
This whole time, it was [Wakelock's lack of Linux support](https://pub.dev/packages/wakelock) that was causing the error. We can either patch it out for Linux or find an alternate solution.

-------------------------

CryptoFish | 2022-08-24 12:19:23 UTC | #29

Now that we've figured out how to setup the development environment (thank you @sol for breaking it down), we can work on some of the items on the list. I figure we would need to fork the repository in order to setup a team of contributors.
We could also break down the list in work items under the GitHub repository and use DoWork for bounties?

-------------------------

romeo | 2022-08-24 22:03:12 UTC | #30

I've updated the main post with all of the suggestions to date

-------------------------

aminazgol | 2022-08-27 04:17:38 UTC | #31

Thanks to @sol straightforward explanation, I could run Syrius on Ubuntu. It would be nice to have a release of Syrius on Snapd. I hope the team considers it.

-------------------------

sol | 2022-11-09 04:32:50 UTC | #32

Given I'm more of a visual person and I like seeing progress being displayed on a board, @0x3639 has setup an instance of Mattermost for us.

I've started populating the Syrius board with the suggestions from this thread and we'll be tackling them one at a time.

Feel free to contribute by:
- submitting tasks/bugs
- updating the contents of any ticket
- taking on a ticket and seeing it through

Your help is most appreciated!

https://mm.0x3639.com/boards/workspace/bjqwiwqxqtnb8xf1mab1fnu8ua/bdw6atoqxgirqjcuuz5ckxu3naa/vqsgy3jdce7f3bcqapjnstz86xh

-------------------------

CryptoFish | 2022-11-09 21:44:13 UTC | #33

Would like to help out, see you guys on Mattermost!

-------------------------

aliencoder | 2022-11-11 16:42:52 UTC | #34

Possibility to add multiple addresses simultaneously
Possibility to switch between networks (netid)

-------------------------

sol | 2022-11-11 22:30:29 UTC | #35

Hi everyone, I've made some changes to the syrius code and I'm requesting community testing for these branches:
- [dynamic_netId](https://github.com/Sol-Sanctum/syrius/tree/dynamic_netId)
- [add_message_field](https://github.com/Sol-Sanctum/syrius/tree/add_message_field)
- [linux_poc](https://github.com/Sol-Sanctum/syrius/tree/linux_poc)

Some notes about each branch:
* dynamic_netId and add_message_field require you to manually supply the Zenon library files in the build output directory. Some info about this [can be found here](https://github.com/zenon-network/syrius/issues/4#issuecomment-1223451140).
* linux_poc has an updated build process for Windows and Linux, automatically sourcing those ^ libraries and dropping them in the build output directory. I'm still working on the MacOS build process with @0x3639.
* dynamic_netId allows you to switch between any Zenon network automatically, depending on the node you've connected to.
If you want to try the netId branch, you may use these nodes:
  * netId 1 == wss://node.zenon.fun:35998
  * netId 321 == ws://node.zenon.fun:36998
  * DM me your 321 test address and I'll fund you with some tZNN/tQSR
* add_message_field updates the transaction widget to allow users to submit optional messages with their tx.

I've tested all these and am satisfied with the results, but I'd like community feedback in case I made a mistake.
After a brief period of time, I'll submit each of these as a PR to the official git repo.

-------------------------

0x3639 | 2022-11-12 01:09:49 UTC | #36

I plan to continue my work on this Saturday & Sunday between kid stuff.

-------------------------

CryptoFish | 2022-11-13 10:19:13 UTC | #37

@sol do you happen to have a http adres for the devnet node to connect the Zenon Explorer? http://node.zenon.fun:35997 does not seem to work.

-------------------------

sol | 2022-11-13 15:54:36 UTC | #38

Since I haven't enabled HTTPS/WSS for the devnet node, we'll need an HTTP explorer.

You may use: http://explorer.zenon.fun
With node: http://149.56.108.141:36997

-------------------------

aliencoder | 2022-11-26 21:20:20 UTC | #39

Dynamic netid is cool, but it would be also very helpful to be able to manually set it. I would make a separate Settings card with all options (Add/edit netid and dynamic netid).

-------------------------

sol | 2022-11-14 00:40:57 UTC | #40

Is there a reason for a Client-Node netId mismatch scenario? I don't think this would really work for anything...

Example: Syrius connects to node with netId 1, but I've statically set netId 321 in Syrius, I won't be able to interact with either netId 321 or netId 1. Syrius will still be able to see netId 1 chain data.

-------------------------

aliencoder | 2022-11-22 22:17:45 UTC | #41

Zenon uses `ChainIdentifier` and `netId`, while Ethereum uses `chainId` and `networkId`. You can find a list with `chainId` information [here](https://chainlist.org).

`chainId` is used to prevent replay attacks and `neworkId` is used in the p2p communication and you usually want both to be the same value and different from other networks (localnet/devnet/testnet/etc).

In syrius:
Zenon Node network identifier: `generalStats.frontierMomentum.chainIdentifier.toString()`
Client network identifier: `netId.toString()`

We definitely don't want Client-Node `chainId` mismatch (because the Client will sign tx only valid for that specific `chainId` when sending them for broadcast to the node that is connected to)  and `netId` is really used only by the node to connect to other nodes from the p2p network and we should just inform the user.

It's a bit [misleading](https://github.com/zenon-network/znn_sdk_dart/blob/367ddc7fbfefb6484d7553d9ac7e4532003a7008/lib/src/model/nom/account_block_template.dart#L61) and I think this is a confusion that we should address in the next update. More info on this [over here](https://medium.com/@pedrouid/chainid-vs-networkid-how-do-they-differ-on-ethereum-eec2ed41635b).

-------------------------

CryptoFish | 2022-11-23 09:20:13 UTC | #42

@sol sending transactions with an optional message seems to work.

The UI doesn't enforce any limitation on the maximum data length. So when entering a very large message the the API creates an exception based on two conditions.

`"JSON-RPC error -32000: account-block data field is too big"`
When sending an account-block with data larger than 16384 characters

`"JSON-RPC error -32000: forbidden parameter"`
When the account doesn't have the required plasma.

```
// MaxDataLength defines limit of account-block data to 16Kb
MaxDataLength = 1024 * 16
```

Would be nice if the UI prevents large messages. Maybe even limiting the max allowed data size of 16Kb?

-------------------------

aliencoder | 2022-11-23 17:55:04 UTC | #43

I've created [a new branch for the Dart SDK](https://github.com/alienc0der/znn_sdk_dart/tree/chainid) with distinct fields for `chainId` and `netId`.

From my [research](https://github.com/ethereum-lists/chains) both `chainId` and `netId` fields should be equal and different from mainnet (Alphanet) where both are [hardcoded](https://raw.githubusercontent.com/zenon-network/go-zenon/master/chain/genesis/embedded_genesis_string.go) to `1`.

Maybe we'll have only `chainId` in the SDKs as `netId === chainId` and `netId` is a variable bounded to the node. What do you think?

-------------------------

sol | 2022-11-25 00:52:20 UTC | #44

Thanks for the feedback! I agree, we can leverage client-side validation to avoid RPC errors.

I've [updated my add_message_field branch](https://github.com/zenon-network/syrius/commit/d1ae89d97011804b09737fba484f28e52fa6979c):
- enforces a MaxDataLength limit for the message field
- displays a notification error if PoW Plasma max limit is reached for a transaction

Users will no longer see those JSON-RPC errors.

-------------------------

aliencoder | 2022-11-26 21:19:55 UTC | #45

@sol I've [combined](https://github.com/zenon-network/syrius/commit/d706b7f16c30f244fad7d4ecafff4428c4ea7116) your dynamic chainid with my previous Dart SDK commit and also displayed additional info in the Node Management tab.

![embedded|690x225, 75%](upload://vy7gDJ0N0CsoeB9YkP66kOpadA2.png)

![znnfun|690x233, 75%](upload://cCNxjPhoH9eWcqMAGJEJ37GYWn5.png)

-------------------------

sol | 2022-11-26 22:03:14 UTC | #46

That's awesome! I wouldn't merge this in to syrius until the Dart SDK is officially updated.
What does the tooltip display when the node is added but offline? Example: wss://peers.zenon.network:443

Will you be submitting a PR for your SDK changes?

-------------------------

sol | 2022-11-26 22:49:29 UTC | #47

Quick update
- [New branch](https://github.com/Sol-Sanctum/syrius/tree/updated_links) with updated links in the Information widget
- Updated [linux_poc branch](https://github.com/Sol-Sanctum/syrius/tree/linux_poc) with two .sh scripts to package a .dmg file after generating a Release build. Thank you @ZNNAYIID  for the [new background image](https://github.com/Sol-Sanctum/syrius/blob/linux_poc/macos/DmgResources/backgroundImage.png)! :pray: 

I'd appreciate anyone with a Mac to give the new build process a try. Please provide feedback if you run into any issues.

Check out @0x3639's thread to [setup the MacOS dev tools](https://forum2.zenon.org/t/how-to-compile-syrius-for-macos/1116).

```
Instructions
1. git clone -b linux_poc https://github.com/Sol-Sanctum/syrius.git
2. cd syrius
3. flutter build macos --release
4. brew install create-dmg
5. cd macos
6. ./generateDmgRelease.sh
   - or ./generateDmgRelease-new.sh
7. Navigate to /path-to-syrius/build/macos/ and double-click the .dmg
```

Future syrius update process could involve package managers, but at least now we have an end-to-end process for devs to produce Release builds for each OS.

```
Windows - chocolatey??
Mac - brew
Linux - brew or snap
```
or
```
1. Press the Update button in syrius
2. download latest Release file from git
3. shutdown the app
4. replace files and re-launch syrius
??
```

Note: the Linux build does not have an icon for the ELF file. We'll almost certainly need to support a package manager like `snap` in order to have that.

-------------------------

aliencoder | 2022-11-27 16:09:02 UTC | #48

Yes, I can handle that, thank you!

-------------------------

aliencoder | 2023-01-11 17:22:50 UTC | #49

I think we should revive this thread.

I'm working with a friend on some improvements for the Syrius wallet and wanted to ask for some feedback regarding the following features:

* [Tray manager](https://pub.dev/packages/tray_manager) :white_check_mark:
* Desktop notifications :white_check_mark:
* Launch on startup :negative_squared_cross_mark:
* Deep linking :negative_squared_cross_mark:

-------------------------

sol | 2023-01-11 17:17:02 UTC | #50

Are those available in a release or branch? Is the tray manager code [working](https://github.com/alienc0der/syrius/actions/runs/3891572980/jobs/6641956896#step:9:21)?

-------------------------

aliencoder | 2023-01-11 17:21:12 UTC | #51

They are available here: [cicd branch](https://github.com/alienc0der/syrius/tree/cicd). Still work in progress.

-------------------------

0x3639 | 2023-01-11 19:06:23 UTC | #52

Are you asking us to test this or give an opinion on the features?

- Tray manager is a great idea.  Would be nice to add
- Desktop notifications would also be great to add
- Launch on start up is good so long as we can disable the feature
- What is "Deep linking"?

-------------------------

coinselor | 2023-01-11 19:12:17 UTC | #53

From google: " Deep links are **a type of link that send users directly to an app instead of a website or a store** . They are used to send users straight to specific in-app locations, saving users the time and energy locating a particular page themselves – significantly improving the user experience."

This is really useful, think of a button in deeznnuts.com that says 'delegate now' and when you click it syrius opens up in the pillar tab and already scrolled down to your pillar row. #magic

-------------------------

0x3639 | 2023-01-11 19:14:53 UTC | #54

wow.  First I've ever heard of this concept.  Should have googled myself.  This seems like a useful feature for sure.  Might be something @mehowbrainz should be aware of.

-------------------------

sol | 2023-01-11 19:18:34 UTC | #55

I told him about the post. I'm curious to see how this deeplinking approach differs from Vilkris' URI PoC.

-------------------------

aliencoder | 2023-01-11 20:45:33 UTC | #56

He's already aware of this feature. But let's not push Syrius tracking capabilities into this discussion :grinning:

-------------------------

sol | 2023-01-16 22:28:11 UTC | #57

First impressions of the tray icon change:

- Works on Windows, will be testing on Linux and MacOS soon
- Tray icon options work as expected
- Some users may find the notifications annoying.
   - Can we please have a toggle to disable notifications?

-------------------------

CryptoFish | 2023-01-17 09:01:53 UTC | #58

I haven't seen this one on the list yet, but at what stage do we want to update the package dependencies used by s y r i u s? I imagine some might have known vulnerabilities and/or bugs. They are getting old and outdated and I know a couple of UI packages require a rewrite because of major changes in the interface. On the other hand, updating the packages can also introduce new bugs.

I would like to step up for this one and make an attempt to map out all the differences.

-------------------------

aliencoder | 2023-01-17 10:08:13 UTC | #59

I've updated the majority of packages and it runs just fine. We can update the remaining packages after we submit the `v0.0.6` PR and it's merged in production.

-------------------------

CryptoFish | 2023-01-17 10:13:48 UTC | #60

Nice, good to know. I'm not sure, but I recall a major update of the `fl_chart` package caused some compatibility issues.

-------------------------

0x3639 | 2023-01-19 02:25:05 UTC | #61

I tested the latest syrius build for mac.  Everything works great.  I was able to send / receive tokens, generate plasma, fuse plasma for myself and a 3rd party address.  Only issue is the attached.  The bottom is cut off.  I will unfuse the plasma tomorrow and report back.  Great work guys.  

![Screenshot_2023-01-18_at_8.06.28_PM|563x413](upload://mmynPT1czavn5LLeIhTaRvS1Ulk.png)

-------------------------

sol | 2023-01-19 04:52:20 UTC | #62

Will be fixed soon.
Left axis could have equal spacing for the top and second value but we can fix that next version.
![image|545x405, 50%](upload://lbOjypE3x0IihU22Kh9IaCuVQhp.png)

-------------------------

CryptoFish | 2023-01-19 08:21:58 UTC | #63

As discussed with @sol in Discord.

The 'My projects' filter tag, filters on all user addresses, but as a non-pillar owner the result set gets filtert down in the `_filterProjectsAccordingToPillarInfo` function to all active projects or projects owned by the selected address.

https://github.com/zenon-network/syrius/blob/9a394eb7a0f21306e90a2dea86f33276d58f874f/lib/blocs/accelerator/project_list_bloc.dart#L159

A non-pillar user has to switch the selected address to see its own projects on another address. While a pillar user sees its own projects on all addresses.

For example:
User A has 3 addresses
Address 1 has a pillar registration and 3 projects
Address 2 has 1 project
Address 3 has 1 project

- When address 1 is selected, the user sees all 5 projects when activating the 'My projects' filter tag.
- When address 2 or 3 is selected, the user only sees project 1 when activating the 'My projects' filter tag.

So when address 1 is selected the user is considerd a pillar user, otherwise a non-pillar user.

With the following change the situation would be equal to that of a pillar user and the user would not have to change the selected address to see all his owned projects.

`kDefaultAddressList.contains(project.owner.toString())`

So far I've not been able to detect any side-effects.

-------------------------

0x3639 | 2023-01-19 10:04:56 UTC | #64

this seems like a good improvement.

-------------------------

sol | 2023-01-20 00:35:34 UTC | #65

[quote="CryptoFish, post:29, topic:578"]
We could also break down the list in work items under the GitHub repository and use **DoWork for bounties**?
[/quote]

I forgot about this
https://app.dework.xyz/zenon

Unfortunately, they don't support native ZNN. We could revisit this when the multi-chain bridge is deployed.

I've updated the [Mattermost board](https://mm.0x3639.com/boards/workspace/bjqwiwqxqtnb8xf1mab1fnu8ua/bdw6atoqxgirqjcuuz5ckxu3naa/vqsgy3jdce7f3bcqapjnstz86xh) with most of the remaining tasks from the original post.
Please continue providing feedback so we can add it to the funnel. :)

-------------------------

DrD3 | 2023-01-21 17:15:17 UTC | #66

I believe @angelo_a_jr returned most of the ZNN received back to AZ. If you guys are planning on reviving Dework for paying bounties then @SugoiBTC and Angelo might have to submit another proposal on AZ.

https://forum2.zenon.org/t/proposal-rapid-bounty-deployment-discovery-on-dework-wznn-multisig/640/9?u=drd3

-------------------------

aliencoder | 2023-01-22 10:52:10 UTC | #67

[quote="CryptoFish, post:63, topic:578"]
So far I’ve not been able to detect any side-effects.
[/quote]

I can [merge it](https://github.com/alienc0der/syrius/pull/14) right away if eveyone is OK with the fix.

I'll wait for more feedback for this one: [Fix fusing address reset #13](https://github.com/alienc0der/syrius/pull/13) .

-------------------------

CryptoFish | 2023-01-22 18:40:26 UTC | #68

I'll need to complete some extra tests on the cicd branch to be sure. Will let you know when they're ready.

-------------------------

CryptoFish | 2023-01-23 11:30:14 UTC | #69

Fully tested PR 13 and PR 14 on the cicd branch. Could not find any problems. However, we do need to make a design decission on PR 14. See PR for more info.

https://github.com/alienc0der/syrius/pull/14

-------------------------

aliencoder | 2023-01-23 21:09:41 UTC | #70

`The "create phase" will only be visible when the address of the project owner is selected.`

I think this is a good approach, as you must know in advance where you'll receive the funds for your project.

Waiting for more feedback, but I think we're good. [PR #13 is already merged](https://github.com/alienc0der/syrius/pull/13).

-------------------------

aliencoder | 2023-01-28 20:49:20 UTC | #71

I've patched a potential problem with getting the `chainId` from a remote node.

I've also added some git info (`branchName` and git `commitHash`) for Syrius in order to be easier for users to verify this information directly from `Info Tab` -> `About Card`.

-------------------------

aliencoder | 2023-01-28 20:53:14 UTC | #72

We are approaching `v0.0.6` release candidate for Syrius.

Next week the community will be able to test the wallet before submitting the Pull Request to integrate all the changes into the official repository.

-------------------------

0x3639 | 2023-01-28 22:44:55 UTC | #73

Atomic Swaps and Wallet Connect in v0.0.7?  Is anything else getting pushed to the next release?

Look forward to testing everything.

-------------------------

aliencoder | 2023-01-29 10:43:23 UTC | #74

[quote="0x3639, post:73, topic:578"]
Look forward to testing everything.
[/quote]

Thank you! Testing is very important during early stage development and maybe in the future we'll start integrating an automatic testing framework.

Now let's focus on delivering `v0.0.6` that's around the corner and has a ton of improvements already and then we'll start working on `v0.0.7`.

-------------------------

vilkris | 2023-01-29 20:50:11 UTC | #75

Are you planning on submitting one big PR or will there be multiple PRs in smaller self-contained chunks?

-------------------------

aliencoder | 2023-01-30 09:19:11 UTC | #76

A big PR containing all the changes.

-------------------------

aliencoder | 2023-01-30 10:05:10 UTC | #77

Merged [material-3](https://github.com/alienc0der/syrius/tree/material-3) branch into `cicd`.

Flutter [Material 3 / Material You](https://docs.flutter.dev/development/ui/material3-updates)

[Demo Material 3](https://flutter.github.io/samples/web/material_3_demo/#/)

-------------------------

vilkris | 2023-01-30 10:10:19 UTC | #78

Maybe I missed something but why only one big PR? Why not self-contained PRs of bugfixes and new features to make reviewing and discussion easier? There's a lot of new code and changes in your branch and I'm worried it will be hard to review if everything is in one PR.

-------------------------

aliencoder | 2023-01-30 12:57:53 UTC | #79

When the branch is fully tested and we're approaching the release of `v0.0.6` we'll decide on how to submit the pull request(s).

-------------------------

vilkris | 2023-01-30 14:09:57 UTC | #80

Why not submit separate PRs for features/bugfixes as they get finished? More time to review and discuss before the deadline.
A single PR with thousands of lines of code changes related to different features is hard to effectively review, so I'm not sure I agree with the approach to make large PRs containing a full release.

-------------------------

aliencoder | 2023-01-30 14:58:26 UTC | #81

I agree, but let's see how we can do it efficiently.

-------------------------

sol | 2023-01-30 15:49:38 UTC | #82

The community should be given every opportunity to analyse individual code proposals, test, provide feedback, and consent to specific changes. 
Some community members won't compile code so the proposals should include a visual component, like a screenshot, or a description if applicable.

Having a massive PR is not conducive to this approach. It's difficult to see what code/commits are specific to which features/bugfixes, reducing the community's ability to veto certain proposals.

It's one thing to combine all prospective code changes into a repo for testing, but I think we should break out the individual fixes and features into smaller PRs in order to be more surgical about what gets merged.

Once the community is satisfied with what's been merged, we can have a small PR to increment version numbers.

-------------------------

ZNNAYIID | 2023-01-30 16:12:20 UTC | #83

I agree with Sol and Vilkris.

-------------------------

zyler9985 | 2023-01-30 16:15:08 UTC | #84

Agree, it's an important acknowledgement that not all of our validators are technical ppl, so including screenshots and descriptions is a great way to bridge the gap between technical and non-technical ppl for optimal brainstorming of feedback. 

I actually think a team of translators could be made, with the sole purpose of using their technical skills to provide clarity to all of the pillars in as objective and non biased way as possible.

-------------------------

cryptocheshire | 2023-01-30 16:24:09 UTC | #85

I agree with Sol and Vilkris

-------------------------

coinselor | 2023-01-30 16:50:51 UTC | #86

I'm also in favor of smaller chunks for PRs. It seems a lot easier for others to digest, analyze and test. 

I've been learning flutter for a while now in order to start contributing. I also try to follow the dev threads and help testing whenever there are new releases. Looking at other open source projects, they seem to have detailed SOPs for submitting a PR, including style guides for both documentation and code. 

I understand we are still in our early days of development, and we should prioritize getting code out over dedicating time into coming to a consensus on best practices for our network. However, we should not lose sight of what I consider to be an important matter. For example, I've seen developers raise concerns for stuff like:

- coordinate the exact development environment 
- working off a branch controlled by a single developer
- sizes of PRs

We can start panting our own "how to contribute" document with a broad brush, you all know better than me what issues are more important.

From the flutter project, they give high importance to filing an issue before every PRs, with an emphasis on writing tests and keeping the PRs as minimal as possible, isolating a single issue, so if the PR needs to get undone, you don't lose extra work/features put into it. 

> Tests
> 
> Every change in the flutter/engine, flutter/flutter, flutter/plugins, and flutter/packages repos must be tested, except for PRs that:
> 
> * only remove code (no modified or added lines) to remove a feature or remove dead code. (Removing code to fix a bug still needs a test.)
> * only affect comments (including documentation).
> * only affect code inside the `.github` directory, `.cirrus.yml` or `.ci.yaml` config files.
> * only affect `.md` files.
> * are generated by automated bots (rollers).
> * have an *explicit* exemption (a message from Hixie starting with `test-exempt:`).

My humble two cents.

https://github.com/flutter/flutter/wiki/Style-guide-for-Flutter-repo#formatting
https://github.com/flutter/flutter/wiki/Tree-hygiene

-------------------------

0x3639 | 2023-01-30 23:14:25 UTC | #87

This seems like a very logical approach.  I hope some of the other community contributors who are a little less technical can help with some of these recommendations, such as a “how to contribute” document.  

Submitting smaller PR that can be undone w/out rolling back other valuable changes also make sense to me.  I'm sure we can iterate and improve as we move forward on next versions.

-------------------------

aliencoder | 2023-01-31 09:51:13 UTC | #88

* Removed the `KeyboardFixer` patch (tested and it works without it on Flutter versions > `3.3.7` 
* Updated the `RemoveOverscrollEffect` for `Material 3`, removed it from various places where it was unnecessary (you'll end up with a heavy rendering tree) and enabled it globally inside `MaterialApp`

-------------------------

aliencoder | 2023-02-01 21:55:21 UTC | #89

New feature :dizzy: 

Added the possibility to `Save QR` or `Share QR` for a particular address.

![test|690x343, 75%](upload://s1tJPe5OT2z8kLJtYZiPrwtXobn.png)

-------------------------

sol | 2023-02-02 17:28:25 UTC | #90

[quote="aliencoder, post:81, topic:578"]
let’s see how we can do it efficiently.
[/quote]

Do you have a counter-proposal? We need to come to a consensus about this soon.

-------------------------

aliencoder | 2023-02-03 17:19:15 UTC | #91

[quote="sol, post:90, topic:578"]
Do you have a counter-proposal? We need to come to a consensus about this soon.
[/quote]

I'll need to think and come up with a solution. How many PRs do you see for `syrius` and `znn_sdk_dart`? For `go-zenon` I've opened just 1 PR.

-------------------------

CryptoFish | 2023-02-03 19:39:19 UTC | #92

In the last 5 days I've created 2198 QSR transactions. Now I get the following error when looking at my account stats under the settings tab.

![s y r i u s 3-2-2023 18_12_24 (2)|374x500](upload://vcXfTOiDBSSV4pIuDJRwRJFGGjS.png)

The AccountChainStatsBloc calls the `getAccountBlocksByHeight`, but an error is thrown when the account reaches a total height of bigger than 1024.

The go-zenon rpc method has the following check.

https://github.com/zenon-network/go-zenon/blob/c0f931d3cd9844a487ae08ed15f5c52896a9bb44/rpc/api/ledger.go#L126

The widget calls the `getAccountBlocksByHeight` method to show the first or last block hash and total numbers of each block type.

This could be solved by dividing the total block count by 1024 and calling the method in batches of 1024 blocks.

-------------------------

CryptoFish | 2023-02-03 17:34:09 UTC | #93

@aliencoder 

I've set my Client chain identifier selection to 321.

I'm connected to my local devnet with Node chain identifier 321. No warning icon is shown in the node selection.

No warning is issued when changing from my local devnet node to public node with node chain identifier 1. Warning icon is show in the node selection. Chain identifier mismatch. Client chain identifier: 321, Node chain identifier: 1.

The following warning is issued when changing from the public node with node chain identifier 1 to my local devnet node with node chain identifier 321. No warning icon is shown in the node selection.

![s y r i u s 3-2-2023 18_19_27 (2)|690x193](upload://cswUYfd0LjmaXIJLIq7czTy5UhA.png)

Shouldn't the warning be issued when changing to the public node instead of the local node that matched the client chain identifier?

-------------------------

aliencoder | 2023-02-03 17:59:04 UTC | #94

Another issue is the `const int rpcMaxPageSize = 1024;` from the Dart SDK `lib/src/client/constants`.

We need to fix both @CryptoFish

-------------------------

aliencoder | 2023-02-03 18:02:19 UTC | #95

[quote="CryptoFish, post:93, topic:578"]
I’m connected to my local devnet with Node chain identifier 321. No warning icon is shown in the node selection.
[/quote]

Works as intended as you client chain identifier `321` matches with the chain identifier of the node `321`.

[quote="CryptoFish, post:93, topic:578"]
No warning is issued when changing from my local devnet node to public node with node chain identifier 1. Warning icon is show in the node selection. Chain identifier mismatch. Client chain identifier: 321, Node chain identifier: 1.
[/quote]

I agree that we should also check and show the warning dialog.

-------------------------

CryptoFish | 2023-02-03 20:28:32 UTC | #96

[quote="aliencoder, post:95, topic:578"]
I agree that we should also check and show the warning dialog.
[/quote]

But do you not agree, that the warning message shown in the picture is not correct. I'm connecting to the local node, but the node chain identifier is 321 not 1 and therefore no warning should be shown.

-------------------------

aliencoder | 2023-02-03 21:43:51 UTC | #97

Can you please explain me again the scenario?

Possible scenarios:

Embedded node <- Web Sockets -> Syrius
Local node <- Web Sockets -> Syrius
Remote node <- Web Sockets + SSL -> Syrius

Please note that the embedded node can have `chainId != 1`, it doesn't necessarily be on mainnet. That's why it should be mandatory to show a warning dialog regardless of the `chainId` of the node you're connecting to. The embedded node is currently a `safer` option, but not the `safest` until we implement something like [this](https://reproducible-builds.org/).

The whole idea is to empower the user to enforce the `chainId` in their wallet because it is used in transaction signing.

-------------------------

aliencoder | 2023-02-07 13:31:40 UTC | #98

New improvements :partying_face:

* Updated the chain identifier selection process
* Dependency cleanup:
Updated dependencies to latest version: `fl_chart`, `flutter_svg`, `flip_card`, `package_info_plus`, `device_info_plus`
Replaced `file_selector_platform_interface` with `file_selector`
Removed unnecessary dependencies: `network_info_plus`, `file_selector_windows`, `file_selector_windows`, `file_selector_macos`, `file_selector_linux`
Added new dev dependency: `dependency_validator`

-------------------------

aliencoder | 2023-02-07 21:05:03 UTC | #99

We really need a good `logging` solution for Syrius with disk persistency.

Started implementing the [recommended logging library](https://github.com/dart-lang/logging) for Dart into Syrius. 

There are over 100 files where we should be able to log the errors and I bet it will very helpful for future debugging.

-------------------------

CryptoFish | 2023-02-08 11:56:35 UTC | #100

[quote="CryptoFish, post:92, topic:578"]
In the last 5 days I’ve created 2198 QSR transactions. Now I get the following error when looking at my account stats under the settings tab.
[/quote]

Created PR #30 to fix the account stats issue.

 https://github.com/alienc0der/syrius/pull/30

-------------------------

aliencoder | 2023-02-08 17:39:12 UTC | #101

[New improvements](https://github.com/alienc0der/syrius/commit/620e0f16bde5cbb4823ec9948636ec43ca6192d0) :partying_face:
* Implemented [Dart logging](https://github.com/dart-lang/logging)
* [Dart format](https://dart.dev/tools/dart-format) applied to the repository

-------------------------

aliencoder | 2023-02-09 09:11:18 UTC | #102

New improvements :partying_face:
* Merged @CryptoFish's [pull request](https://github.com/alienc0der/syrius/pull/30)

-------------------------

