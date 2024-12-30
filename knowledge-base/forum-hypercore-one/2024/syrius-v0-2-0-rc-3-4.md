Thread: syrius-v0-2-0-rc-3-4
CryptoFish | 2024-03-15 07:03:55 UTC | #1

This post will be used to collect issues for test round #4.

Download: [Syrius v0.2.0-rc.3](https://github.com/zenon-network/syrius/releases/tag/v0.2.0-rc.3)

Read [this ](https://forum.hypercore.one/t/syrius-v0-2-0/328/7) post for more information about how to test.

The following issues were fixed:
- Pillar type removed from Pillar stepper
- Device name is now used to identify Ledger device
- Allow ZNN **or** QSR donations (does not require to have ZNN balance)
- Rearrangement of Settings card
- Restore connection when rejecting chain id mismatch

-------------------------

coinselor | 2024-03-13 21:08:19 UTC | #2

Trying to finish the tests I started with rc.2 with rc.3 ... lmfao you are gonna have rc.4 before I can finish these tests. 

auto-receive test are all PASS for now, but I've run into an issue. I'm doing a P2P swap:

1. Started swap with rc3
2. Joined swap with unkown version of 0.2.0 (it has auto-receive).
3. Completed swap with rc3 and auto-receive disabled. Everything worked as expected.
4. Swap with unknown syrius is stuck in loop trying to publish a transaction:

![image|690x421](upload://vwqURxYJsIH7ttAlDAPCFWjveMB.png)
I updated to rc3 and tried again. Still same issue. It has published like 10 txs already.
![image|690x432](upload://fDY6ZWwxKQamQgVjUqrmT6n3guy.png)
address: [z1qruuq0aafta69sc5fwdq5zdcnu249n3tg90tkj](https://zenonhub.io/explorer/account/z1qruuq0aafta69sc5fwdq5zdcnu249n3tg90tkj)
sending
deposit id: `507d0e8f0bab12daaca3daa639029c01dd09b4702e9839d12c3ef09550c1db0b`
hashlock: `9e516ea48ed1088470999e0e146d5fe897331c071c0df948306d58743b634e53`
receiving
deposit id: `7a0550a0e5904e46ffee1d55c399405e1dd04be6e60a5c325a542cc3ef288120`
hashlock: `9e516ea48ed1088470999e0e146d5fe897331c071c0df948306d58743b634e53`


Transactions appear
 as unreceived in the HTLC contract, didn't even know that was possible.
https://zenonhub.io/explorer/account/z1qxemdeddedxhtlcxxxxxxxxxxxxxxxxxygecvw

Should you add tests cases for the new stuff i.e donations to AZ?

I think we should strongly consider adding a notification to the "Transfer" tab whenever there are pending transactions, like a phone style notification red dot or similar. Otherwise, we are gonna be explaining to people why they have not received their transactions way too often.

-------------------------

CryptoFish | 2024-03-14 09:36:33 UTC | #3

[quote="coinselor, post:2, topic:407"]
Trying to finish the tests I started with rc.2 with rc.3 … lmfao you are gonna have rc.4 before I can finish these tests.
[/quote]

Sorry about that. I've gotta feeling rc.3 will last longer :crossed_fingers:

[quote="coinselor, post:2, topic:407"]
auto-receive test are all PASS for now
[/quote]
Great, could you post your test-runs on the forum?

[quote="coinselor, post:2, topic:407"]
but I’ve run into an issue. I’m doing a P2P swap:
[/quote]

Vilkris looked into it and had the following to say:
[quote="vilkris"]
Eventually it was the first unlock request that did unlock the funds. Not sure why it would take so long for the funds to be sent
Looking at the Unlock request here: https://zenonhub.io/explorer/transaction/ea0546a04783cd5b538e14a135e9ee8b6fdaa846fc234d852a5273d1bc84b025?tab=json
Unlock tx confirmed at 6844823, HTLC contract verified unlock request also at 6844823 as it should, but then the HTLC contract receive transaction took until 6845226 to be confirmed
So at a quick glance it would appear that the contract receive account block possibly had issues getting propagated to a producing pillar. All the Unlock receive transactions were confirmed in this momentum https://zenonhub.io/explorer/momentum/14b66376edd2842799b897a1aaf47587b24f0645c062e94f830cca7fbcb4ce1a
I don't think the issue was with the HTLC contract, since the Unlock request was verified right away
[/quote]

I did the `auto-receive` test with rc.1 on the HC1 testnet and didn't had any problems with or without `auto-receive`. We don't think this has anything to do with Syrius.

Which nodes were both clients connected to?

[quote="coinselor, post:2, topic:407"]
Should you add tests cases for the new stuff i.e donations to AZ?
[/quote]
I didn't create test cases for everything, feel free to suggest any and I'll add them to the repo.

[quote="coinselor, post:2, topic:407"]
I think we should strongly consider adding a notification to the “Transfer” tab whenever there are pending transactions, like a phone style notification red dot or similar. Otherwise, we are gonna be explaining to people why they have not received their transactions way too often.
[/quote]
We could use badges on the Transfer tab to indicate there are pending transactions.

-------------------------

coinselor | 2024-03-14 10:54:24 UTC | #4

[quote="CryptoFish, post:3, topic:407"]
Which nodes were both clients connected to?
[/quote]

`wss://node.zenonhub.io:35998`

Not sure if this is relevant, but I recently installed [Portmaster](https://safing.io) - a kernel level firewall, in that same machine.

[quote="CryptoFish, post:3, topic:407"]
on the HC1 testnet
[/quote]

Your initial posts share a testnet node for sumamu/bridge team testnet, right? I know because I tried to do the swap tests there initially, and the HLTC contract was not deployed there (syrius gracefully failed with an accurate notification :partying_face: ), and sumamu confirmed it.

-------------------------

coinselor | 2024-03-14 12:21:45 UTC | #5

I just did another swap, it felt like it was going to loop again, but I started messing around with Portmaster and even though it showed 0 blocked connections, and an active connection to node.zenonhub.io, I disabled 'Force Block Incoming Connections' for syrius specifically. 

And it seems that the immediately next tx after was received by the HTLC contract.

I'm just gonna blame @0x3639 for sending me some crazy software to try.

Edit: Did another test reverting Portmaster's settings to see if they had any effect. P2P Swap was completed without issues. Portmaster was probably not the cause of the first failed swap.

-------------------------

CryptoFish | 2024-03-14 11:32:00 UTC | #6

[quote="coinselor, post:4, topic:407"]
Your initial posts share a testnet node for sumamu/bridge team testnet, right? I know because I tried to do the swap tests there initially, and the HLTC contract was not deployed there (syrius gracefully failed with an accurate notification :partying_face: ), and sumamu confirmed it.
[/quote]

Correct, @sumamu should update his `testnet` :laughing:

The hc1 `testnet` cannot be used by the community yet, so the only option left for p2p swaps is `mainnet`.

[quote="coinselor, post:4, topic:407"]
`wss://node.zenonhub.io:35998`

Not sure if this is relevant, but I recently installed [Portmaster](https://safing.io) - a kernel level firewall, in that same machine.
[/quote]

Seems very unlikely because you're not using an embedded node.

-------------------------

coinselor | 2024-03-14 11:56:28 UTC | #7


| Attribute    | Detail                                       |
|--------------|----------------------------------------------|
| Version      | v0.2.0-rc.3                                  |
| Date         | 3/13/2024                                    |
| Environment  | Windows 11 Enterprise Eval 22H2              |
| Tester       | coinselor                                    |



| Test case                                                   | Description                                                                                                                                 | Priority   | Result   |
|:------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------|:-----------|:---------|
| Wallet                                                      |                                                                                                                                          |         |       |
| Create wallet and set auto-receive preference               | Create a wallet and set the auto-receive preference in the node-management screen.                                                          | PRIO1      | PASS     |
| Transactions                                                |                                                                                                                                          |         |       |
| Receive transaction with auto-receive enabled               | Automatically receive a transaction by enabling the auto-receive preference.                                                                | PRIO1      | PASS     |
| Receive transaction with auto-receive disabled              | Manually receive a transaction by disabling the auto-receive preference and manually receive it from the pending transaction list.          | PRIO1      | PASS     |
| P2P Swap                                                    |                                                                                                                                          | | |
| Start & complete native P2P Swap with auto-receive enabled  | Start a native swap, wait for the counterparty to join and complete the swap with auto-receive enabled.                                     | PRIO1      | PASS     |
| Start & complete native P2P Swap with auto-receive disabled | Start a native swap, wait for the counterparty to join and complete the swap with auto-receive disabled.                                    | PRIO1      | PASS     |
| Join & complete native P2P Swap with auto-receive enabled   | Join a native swap and wait for the counterparty to complete the swap with auto-receive enabled.                                            | PRIO1      | PASS     |
| Join & complete native P2P Swap with auto-receive disabled  | Join a native swap and wait for the counterparty to complete the swap with auto-receive disabled.                                           | PRIO1      | PASS     |
| Wallet Options                                              |                                                                                                                                          |         |       |
| Disable auto-receive                                        | Disable the auto-receive preference                                                                                                         | PRIO1      | PASS     |
| Enable auto-receive                                         | Enable the auto-receive preference                                                                                                          | PRIO1      | PASS     |
| Reset wallet and verify auto-receive after confirmation     | Reset and reinitialize the wallet and verify that no transactions are automatically received before confirming the auto-receive preference. | PRIO1      | FAIL     |


I will create an [issue](https://github.com/zenon-network/syrius/issues/91) for the failed case.

-------------------------

coinselor | 2024-03-14 16:49:17 UTC | #8

### Test Details

|Attribute | Detail|
|--- | ---|
|Version | v0.2.0-rc.3|
|Environment | Windows 11 Enterprise Eval 22H2|
|Date | 3/13/2024|
|Tester | coinselor|


### Test Cases

#### Assets

| Test Case                      | Description                                                                                                  | Priority | Result |
|--------------------------------|--------------------------------------------------------------------------------------------------------------|----------|--------|
| Add community nodes            | Add nodes by editing the assets/community-nodes.json file and verify added nodes by restarting syrius        | PRIO1    | PASS   |
| Remove community nodes         | Remove nodes by editing the assets/community-nodes.json file and verify removed nodes by restarting syrius   | PRIO1    | PASS   |
| Invalid community nodes        | Add invalid node urls by editing the assets/community-nodes.json file and verify they are not added by restarting syrius | PRIO1 | PASS   |
| Delete community nodes file    | Delete the assets/community-nodes.json file and verify empty community nodes by restarting syrius            | PRIO2    | PASS   |
| Invalidate community nodes file| Invalidate the assets/community-nodes.json file by using incorrect format and verify empty community nodes by restarting syrius | PRIO2 | PASS   |

#### Node management (onboarding)

| Test Case                   | Description                                                               | Priority | Result |
|-----------------------------|---------------------------------------------------------------------------|----------|--------|
| Verify community nodes list | Verify community node list and corresponding icons                        | PRIO1    | PASS   |
| Confirm community node      | Select and confirm a community node and verify connection                 | PRIO1    | PASS   |
| Add existing node           | Adding an existing node causes a node already exist exception             | PRIO1    | PASS   |
| Shuffle community nodes     | Verify community node list is shuffled each time they are loaded          | PRIO1    | PASS   |

#### Node management (settings)

|Test Case | Description | Priority | Result|
|--- | --- | --- | ---|
|Verify community nodes list | Verify community node list and corresponding icons | PRIO1 | PASS|
|Select community nodes | Select and confirm a community node and verify connection | PRIO1 | PASS|
|Add existing node | Adding an existing node causes a node already exist exception | PRIO1 | PASS|
|Edit existing node | Editing an existing node causes a node already exist exception | PRIO1 | PASS|
|Shuffle community nodes | Verify community node list is shuffled each time they are loaded | PRIO1 | PASS|


Can you explain what do you mean by 'Edit existing node'? There is no edit button inside the 'Node selection' widget.

Minor UX improvement: As the node list expands, there will always be a need to scroll down within the "Node Management" (settings) widget. Currently, there is no scrollbar displayed. I believe it should behave similarly to the 'Latest Transactions' widget, which shows a scrollbar.

-------------------------

CryptoFish | 2024-03-14 16:38:07 UTC | #9

Thank you for the test-run. I will process it and add it to the repo.

[quote="coinselor, post:8, topic:407"]
Can you explain what do you mean by ‘Edit existing node’? There is no edit button inside the ‘Node selection’ widget.
[/quote]

You first have to add a custom node (non community) before you see the edit button.

- Add custom node `wss://node.atsocy.com:35998`
- Edit custom node `wss://node.atsocy.com:35998` to an already existing node

[quote="coinselor, post:8, topic:407"]
Minor UX improvement: As the node list expands, there will always be a need to scroll down within the “Node Management” (settings) widget. Currently, there is no scrollbar displayed. I believe it should behave similarly to the ‘Latest Transactions’ widget, which shows a scrollbar.
[/quote]

Not sure how the scollbars work, but will have a look at it.

-------------------------

coinselor | 2024-03-14 16:48:55 UTC | #10

![image|690x134](upload://ngO4pjOlVFNbdZ4d0cGTW0iCRmZ.png)

Works as expected, added PASS to test, but readability is not great.

-------------------------

CryptoFish | 2024-03-14 16:51:37 UTC | #12

These issues have been resolved in the following PRs:

- https://github.com/zenon-network/syrius/pull/93
- https://github.com/zenon-network/syrius/pull/94
- https://github.com/zenon-network/syrius/pull/95

A new release candidate will be made available.

-------------------------

0x3639 | 2024-03-14 20:36:50 UTC | #13



-------------------------

