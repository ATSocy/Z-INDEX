Thread: current-list-of-pillars-who-are-bridge-orchestrators
0x3639 | 2023-07-01 10:00:40 UTC | #1

![2023-07-01 04.30.29|213x500](upload://fHB3l1zt2Q2b27YvcxacNuWZ1IB.jpeg)

-------------------------

SultanOfStaking | 2023-07-01 11:09:34 UTC | #2


![Sad Season 9 GIF by The Office|480x400](upload://b8DIA5sZWpkQNu6nOiSojGJfo58.webp)

-------------------------

Chadass | 2023-07-01 15:18:08 UTC | #3

Same face here. I'm not in. Question to Sumamu; could the bridge be allowed to be faster with more orchestrators online?

-------------------------

Shazz | 2023-07-01 17:10:46 UTC | #4

Legends

-------------------------

aliencoder | 2023-07-01 20:10:07 UTC | #5

[quote="Chadass, post:3, topic:140"]
could the bridge be allowed to be faster with more orchestrators online?
[/quote]

In general, adding more nodes == more message complexity => more processing time required for those messages (that are zero knowledge proofs actually) => it will get slower

Also we are limited by the speed of the connected blockchain(s). Ethereum has `~15s` block time, but you cannot consider a transaction final after just a few blocks. That's why an upper limit must be set in order to avoid deep reorgs.

@sumamu please correct me if I'm wrong (recently read a paper about the magic of `TSS`)

-------------------------

Chadass | 2023-07-01 22:07:52 UTC | #6

Just lemme in

-------------------------

SultanOfStaking | 2023-07-01 23:56:00 UTC | #7

Yeah but we’re faster

-------------------------

sumamu | 2023-07-17 18:37:21 UTC | #8

[quote="Chadass, post:3, topic:140, full:true"]
Same face here. I’m not in. Question to Sumamu; could the bridge be allowed to be faster with more orchestrators online?
[/quote]

As @aliencoder explained:

[quote="aliencoder, post:5, topic:140"]
In general, adding more nodes == more message complexity => more processing time required for those messages (that are zero knowledge proofs actually) => it will get slower
[/quote]

The orchestrators are actually quite fast: they're signing most swaps in under 2 minutes.

The slowness of the bridge is intentional and it's also necessary for the security of the bridge. In short, we've sacrificed some of the speed for the security.

However, even if signing the swaps might get slower, we should strive to increase the number of bridge participants for 2 reasons:
- security - more nodes means it'll be less likely for a majority of nodes to collude and mishandle the funds (to put it lightly)
- redundancy - a super majority of the bridge participants (66% + 1) is required to produce a VALID signature. With the current numbers (22 participants), 15 participants must be online to sign a swap, which means the bridge will work just fine even with 7 offline participants. If we had 60 participants, we'd need 41 online (which is higher), but we could also afford 19 offline participants.

## Why is the bridge so slow?
It's waiting ~30 minutes for confirmations, to make sure the transactions are (very) final.

There's also an extra waiting time between the first redeem (this one merely registers the swap onchain) and the second redeem (this one actually releases the funds). 

This is called a timechallenge and it's purpose is to give the orchestrators time to check registered swaps (the first redeem) and halt the bridge in case an invalid transaction is detected, BEFORE the funds are released (second redeem)

-------------------------

