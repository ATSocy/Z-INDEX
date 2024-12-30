Thread: github-com-zenon-network
sumamu | 2023-07-28 19:21:27 UTC | #1

> With great power comes great responsibility

Now that some of us have maintainer roles for the Github repos, let's start transferring or forking relevant repos to the organization so that other builders can find everything in one place.

This will also fix one of out greatest issues, which is having a Github with almost no activity, which might make outside visitors see NoM as a ghost chain.

We should also figure out who are the maintainers, since all repos require at least 2 approvals and the go-zenon repo requires 3 approvals to get a PR merged. (to the best of my knowledge)

-------------------------

sumamu | 2023-07-28 19:05:20 UTC | #2

I've got the following repos:
- go-zenon
- znn-pow-links-cpp
- argon2_ffi
- znn_swap_utility
- znn_controller_dart
- znn_cli_dart
- bridge.zenon.network
- znn-wiki

-------------------------

0x3639 | 2023-07-28 20:15:42 UTC | #3

Guys, it looks like I've been given admin roles and have some additional rights.  I can see the maintainers on each repo.  I will post them here below.

I'm open to any discussion about how my admin rights should be limited and/or checked.  

Org
![image|690x159](upload://9Cxiwg4RvwrmNhGMFUMkk1TG8BK.png)

go-zenon
![image|690x321](upload://e8T8ibpyw8FfkQ3UN4Zyt3qK7st.png)

znn-pow-links-cpp
![image|670x500](upload://mBGvCJZlk8mCASUyiF6eMG15ODB.png)

argon2_ffi
![image|668x499](upload://vByKdbHISpYA5eaWfRNmMPxoi96.png)

znn_swap_utility
![image|672x499](upload://wxLdkKwkvk3KznCjF07U84vLQiH.png)

znn_controller_dart
![image|600x499](upload://lwKE3VCx1BYFC0qQyKDHAUO9dT4.png)

znn_cli_dart
![image|597x500](upload://jNaVniVKY2cvXRUdE6FXG987hEB.png)

bridge.zenon.network
![image|690x325](upload://sHN1EGwehO1rnfJ45ByJtNrBKL8.png)

znn-wiki
![image|453x500](upload://kou4HKCul2IQJsJ6G1wTxU1MrF2.png)

SYRIUS
![image|690x333](upload://rcCn3hLuuicFtFJdKjl1ZXLoO5y.png)

Twitter
I'm not an admin

Zenon.network
![image|690x394](upload://bjfLcOTwgbkdtT0lAYHYDTw93kl.png)

-------------------------

aliencoder | 2023-07-28 19:35:47 UTC | #4

Where I am maintainer so far:

* go-zenon
* znn-pow-links-cpp
* argon2_ffi
* znn_controller_dart
* znn_cli_dart
* znn_swap_utility
* znn-wiki

I'll update the list accordingly. I'm now a little busy upgrading some dependencies for Syrius and the Dart SDK.

-------------------------

sol | 2023-07-28 19:43:53 UTC | #5

Wow! I'm shocked by this revelation.

Who has access to the syrius, websites, twitter repos?

-------------------------

coinselor | 2023-07-28 19:46:45 UTC | #6

is sumoshi21's Write role a missclick? 

It might be the first recorded case of a Mr. Kaine missclick.

-------------------------

0x3639 | 2023-07-28 19:51:44 UTC | #7

[quote="sol, post:5, topic:160"]
Who has access to the syrius, websites, twitter repos?
[/quote]

Updated

-------------------------

0x3639 | 2023-07-28 19:51:56 UTC | #8

[quote="coinselor, post:6, topic:160"]
is sumoshi21’s Write role a missclick?
[/quote]

Not sure.

-------------------------

0x3639 | 2023-07-28 23:12:15 UTC | #9

So we have the following main repos

/zenon-network
/hypercore-one
/hypercore-team

And several personal repos.  Early on when we established the ZIP process we envisioned keeping code repositories separate in order to avoid centralized power in one admin or core maintainers.  Moreover, @georgezgeorgez has envisioned node software in different languages.  So if we blow up go-zenon and nodes stop working, "dart-zenon" will continue to make blocks and the network persists.  

1) Should all the "main" code base live in /zenon-network? go-zenon, syrius, orchestrator, side-chain?
2) Should we develop code in /hc1 and /hct and reference it from /z-n with submodules or a mirror? 
3) If we move code to /z-n how do we prevent the centralized github drama that bitcoin has experienced?
4) It would be nice to show activity in the /z-n repo because it's a marketing tool.  But if we can reference / mirror other repos where code is advanced would that serve the marketing purpose?

I think we should discuss some of these big picture questions before forking / moving / creating new repos in /z-n.

Any thoughts?

-------------------------

sol | 2023-07-29 01:12:06 UTC | #10

At the very least, independent participants should be mirroring (e.g. gitea) all three accounts you listed.

I'm still not sure if all AZ-funded software should live in the /z-n account. 
Perhaps we'll even reduce its scope of responsibility and transfer certain projects to dedicated teams.

-------------------------

sumamu | 2023-07-30 09:58:43 UTC | #11

Maybe move everything that's directly related to the network?
For example the orchestrator and the extension chain are third-party solutions, so they could stay on separate orgs

-------------------------

