Thread: march-pr-deadline
0x3639 | 2023-03-13 23:53:21 UTC | #1

Just wanted to remind everyone of the March target for PR submissions.  @aliencoder @sumamu @DrBlaze_21 we would love to jump on a Discord chat before the deadline to discuss your work and give the community an opportunity to ask questions.  We can do them separately.      

https://twitter.com/Learn_Zenon/status/1635427336240742404?s=20

-------------------------

sol | 2023-03-14 01:45:10 UTC | #2

I'm hoping we can submit the Syrius PRs to:
- disable the bridge
- setup automatic releases (Github Actions / cicd)

I think @aliencoder is working on this?

-------------------------

CryptoFish | 2023-03-14 09:22:00 UTC | #3

The bug fixes which have been published to the forum can be submitted as seperate PR's.

More details can be found on the forum under the following posts:

https://forum2.zenon.org/t/syrius-az-my-projects-filter/1324/1
https://forum2.zenon.org/t/syrius-account-statistics-max-rpc-exception/1323
https://forum2.zenon.org/t/syrius-fusing-address-select/1322/1
https://forum2.zenon.org/t/syrius-realtime-graph-has-overlapping-y-axis-values/1321/1
https://forum2.zenon.org/t/syrius-main-dispose-causes-exception/1320/1
https://forum2.zenon.org/t/syrius-realtime-graph-not-rendering-a-graph/1181/11
https://forum2.zenon.org/t/syrius-some-proposals-not-displaying-when-only-accepted-is-toggled/1182/10
https://forum2.zenon.org/t/syrius-bug-fusing-widget-resets-address-field/1185/7

I'm open to discuss the work when needed.

-------------------------

sol | 2023-03-14 12:52:12 UTC | #4

I'm definitely considering these as well. My main concern is the amount of testing/review required.

I'll ask the testers if they have the time to validate these.

-------------------------

digitalSloth | 2023-03-18 19:14:50 UTC | #5

Hey @sol and @CryptoFish great work on the PRs! 

Just been testing them on a Mac and wanted to post feedback, some branches I'm unable to test due to the specific condition required to replicate the issue but if theres test accounts or ways to setup the wallet as required Im happy to test them as well. 

---

**Sol-Sanctum/disable_bridge** - Much better with the form being removed completely, all works as expected.

**KingGorrin/fix-fusing-addr-select** - Works well, unable to replicate the original issue.
**KingGorrin/fix-rt-stats** - Looks good, the graph loads both ZNN and QSR stats.
**KingGorrin/fix-rt-yaxis** - Not sure exactly what was broken but could not spot anything wrong.
**KingGorrin/fix-fusing-addr-select** - Works well, unable to replicate the original issue. 

---

I noticed two bits of visual distortion throughout all the branches

1st The copy/paste/select all popup alignment is messed up:
![disable_bridge - 1|690x414, 75%](upload://2c95PkCxbPJNl0h9AzQV7BHZJvA.png)

![Screenshot 2023-03-18 at 6.25.34 pm|690x265, 75%](upload://y9R2RNcDaBL09K9ZbGjoWnLCLWc.png)

2nd the delegation stats widget, this only showed when Syrius is in a small window when i resized it it disappeared.
![disable_bridge - 2|690x399, 75%](upload://uZXmSilFSG0JGO3thLY05Wily54.png)

Final point, copy/paste keyboard shortcuts dont work on a Mac, this is also an issue with the current official release, not sure if its Mac specific or on other platforms as well.

-------------------------

coinselor | 2023-03-19 01:15:04 UTC | #6

copy/paste/select all popup bug was addressed here: 
https://github.com/alienc0der/syrius/pull/27

I also noticed it and checked his fix, works well:
![image|576x288](upload://2udKfUagiAqeyP5OGAuGW3I1bp3.png)

__________________________________

Tested on Windows 10:

**Sol-Sanctum/disable_bridge** [ :white_check_mark: ]
**KingGorrin/fix-fusing-addr-reset** [ :white_check_mark: ]

-------------------------

CryptoFish | 2023-03-19 13:32:05 UTC | #7

Thank you for testing .

[quote="digitalSloth, post:5, topic:1333"]
2nd the delegation stats widget, this only showed when Syrius is in a small window when i resized it it disappeared.
[/quote]

There's a fix for that one too, but both the 'Fix context menu' and 'Fix RenderFlex overflow' still depends on `cicd` branch. You can find it here.

https://github.com/alienc0der/syrius/pull/21

I don't know exactly how you are testing, but seems like you're using the build based on the `cicd` branch.

A better way of testing would be to isolate each and individual branch and build it from source. Using the official s y r i u s client as reference.

The `cicd` branch compounds a lot of changes which makes isolating the issue or feature hard.

I used the following procedure for testing my branches that are based on the Zenon_Network\master branch.

1. md Zenon_Nework
2. cd Zenon_Network
3. git clone https://github.com/zenon-network/syrius.git
4. cd syrius
5. git remote add KingGorrin https://github.com/KingGorrin/syrius.git
6. git pull KingGorrin `$branch`
7. flutter build `$os`
8. copy `argon2_ffi_plugin.dll`,` libpow_links.dll`,` libznn.dll` to .\build\$OS\runner\Release
9. execute .\build\$OS\runner\Release\syrius.exe
10. test and compare changes with the official client

Replace `$branch` with one of my branch names posted [here](https://forum2.zenon.org/c/development/bugs/33) and `$os` with `linux`, `windows` or `macos` based on your operating system.

You can copy the missing dll files from the official s y r i u s client. Also make sure you have flutter installed.

-------------------------

digitalSloth | 2023-03-19 16:45:06 UTC | #8

Thanks for the links to those extra branches, just tested both and the issues have been resolved. 

Iv been testing by checking out each of the feature branches and building a new copy of syrius for each one.

-------------------------

