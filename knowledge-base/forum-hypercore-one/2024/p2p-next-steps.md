Thread: p2p-next-steps
georgezgeorgez | 2023-09-05 03:34:44 UTC | #1

We now have the best in class P2P swap experience but it is limited to ZTS-ZTS and meant for the everyday user.
Next steps for real liquidity:

**Native Bitcoin Wallet in Syrius** 
* Don't need comprehensive wallet features, but should support an end-to-end flow:
* Be able to receive, hodl, send, and htlc swap
* Is it safe to reuse the same entropy from our eddsa keystores to generate bitcoin wallets?
* Ideally support P2TR and HTLC through tapscript MAST
* Support connection to Bitcoin Core node

**P2P Market Making Clients**
* Can't rely on everyday users keeping Syrius open to trade in chat rooms, need to support market makers with dedicated tooling
* First build out for NoM native ZTS-ZTS, and can extend to BTC when ready
* There are some big advantages to P2P market making:
* Over CEX, no custodial risk obviously
* Over DEX, infinite flexibilty, e.g concentrated liquidity (like Uniswap v3), but also custom curves, don't have to use constant product
* Biggest downside is lack of aggregation and need for matchmaking
* Not sure we can fix aggregation, but great matchmaking renders it less important
* I would not build out a protocol from scratch for matchmaking, possible regulatory landmines
* Use generic/dumb communication protocols and smart clients
* I think Nostr is a good candidate
* Can we integrate with Hummingbot?

**PTLC**
* Better than HTLC for a couple of reasons
* But a little more complicated
* I need to rebase my PTLC work
* Intending to get it on-chain after governance work is done, so that the feature is truly bought in by the community

-------------------------

aliencoder | 2023-09-07 22:14:30 UTC | #2

Hey. I can do the Bitcoin integration into Syrius. I think we're safe reusing the wallet entropy to generate Bitcoin keys.

Resources:

https://pub.dev/packages/bdk_flutter


https://github.com/MohsenHaydari/bitcoin_base

-------------------------

georgezgeorgez | 2023-09-07 22:39:00 UTC | #3

Using BDK would be a great story

-------------------------

georgezgeorgez | 2023-09-07 22:43:18 UTC | #4

https://github.com/LtbLightning/bdk-flutter/issues/94#issuecomment-1638967332

That repo may not be mature enough for our usecase. It is likely that we will need to contribute to those repos in any case.

-------------------------

georgezgeorgez | 2023-09-07 22:49:12 UTC | #5

**Developer Acquisition**
NoM developers contribute to libraries we use.
AZ pays out for it because those libraries then get used for NoM.
Offer ZNN tip to library maintainers and mention decentralized grants.
See who bites.

Once we have PTLCs, we might be able to tip directly on NoM to an existing bip340 pubkey of theirs.

-------------------------

vilkris | 2023-09-08 10:07:53 UTC | #6

I'm also interested in doing the Bitcoin integration into Syrius if we want to focus on that next. I would first create and design a UX for it and present and discuss it with the community before starting the implementation. Similarly to how the P2P swaps UX was done.

The design would consider the full experience from using the BTC wallet to conducting cross-chain P2P swaps with Bitcoin.

With that said, I want to note that in terms of ZTS <> BTC P2P swaps, I don't think we necessarily need to integrate a BTC wallet into Syrius where the user stores/sends/receives funds. If you're coming from Bitcoin into the Zenon ecosystem, it's an extra step for you to have to first send your BTC into Syrius to swap it. Syrius would use one-time BTC keypairs on a per-swap basis to manage the swap, so from the user's perspective they don't need to send BTC in and out of Syrius to swap.

So is a full BTC wallet integration needed right now considering most bitcoiners will probably want to store and manage their BTC in their wallet of choice?

Another option for ZTS <> BTC swaps would be to create a webapp mimicing a "Uniswap experience". This would require the automated market making clients that George mentioned. Since we now have WalletConnect in Syrius the full UX of the swap could be done in the webapp.

If done correctly this could result in a simple Uniswap-like interface where the user is directly swapping with the automated market making clients without knowing it. From their perspective they're just magically swapping ZTS and BTC. The same idea could be used for ZTS <> ZTS swaps.

Such a system would of course be much trickier to create since the market making clients and the matchmaking system would have to be developed, and without a doubt there are many pitfalls there.

-------------------------

georgezgeorgez | 2023-09-08 15:40:30 UTC | #7

[quote="vilkris, post:6, topic:196"]
So is a full BTC wallet integration needed right now considering most bitcoiners will probably want to store and manage their BTC in their wallet of choice?
[/quote]

Well what's stopping Syrius from eventually being their BTC wallet of choice?
Our long term advantage is that we have a native funding model for wallet development.
Not sure how other wallets are being monetized.

Between BTC <-> NoM <-> Extension Chains, the more fluid the experience the better
Wallet hopping breaks the immersion of a single ecosystem

Of course, short term it's too much
But that's why I suggested critical flow for now, only supporting modern scripts etc

If you want to have an experience like we have with ZTS-ZTS, then the bitcoin wallet will need to connect to a nom node to verify the htlc, and vice versa
one user will also need to scan the other chain for preimages
there is some design consideration when it comes to who locks first, in particular because of variance in PoW block tines
that complexity might be better managed in a single spot

even with the idea of single use btc keypairs, what happens to those utxos if the swap does not complete? btc fees are real

another consideration as well is that most htlcs in the bitcoin ecosystem are not base layer
they usually happen in payment channels/lightning
from a systematic standpoint, building the base layer capability would make sense, but from an adoption/trend standpoint, integrating with lightning first may be better

mr kaine mentioned civkit before
which users nostr as a decentralized bulletin board of offers
a UI could connect to multiple of these boards and 
matchmaking is somewhat taken care of, but with any p2p system, you then have the challenge of trust/reputation when it comes to things like locking first

-------------------------

sol | 2023-09-08 16:22:30 UTC | #8

`bitcoin_base` seems viable, though it was only published a month ago. We should perform a security evaluation for any such dependencies, as well as rigorous testing to confirm compatibility.

`bdk_flutter` doesn't support desktop.

-------------------------

Chadass | 2023-09-08 17:02:06 UTC | #9

To your first question I'll answer with one simple fact related to marketing : it's several orders of magnitudes to onboard users if you don't force them to change their habits. Don't let ideology blur your judgement. Allow more paths and more possibles. Don't alienate userbases. If I use Bitcoin core singe 7 years, I won't change just because Syrius is fancy. I love it. It's part of my environment. A lot of people are like that.

-------------------------

georgezgeorgez | 2023-09-08 17:22:03 UTC | #10

In the long run, people will go to the wallets that are best maintained, which will eventually mean best funded. 

In the short term, we wouldn't even consider BTC in Syrius at this stage if other wallets provided the functionality we needed.

-------------------------

Chadass | 2023-09-09 12:51:59 UTC | #11

We want to onboard, not bet on our wallet being better than others when it's unnecessary. You're right about the functionalities but ideology doesn't change how psychology work. Marketing wise, letting people decide work orders of magnitude better than enforcing unneeded things. ex:People doesn't use Matrix because they already use TG and Discord.

-------------------------

georgezgeorgez | 2023-09-09 15:47:48 UTC | #12

I understand your point. I am saying there are technical reasons. The only way to let them stay completely within their wallets of choice is to add NoM node connections to it. That is probably nonstarter for other wallets. Even if we write the code, doubt it would get merged in.

-------------------------

aliencoder | 2023-09-09 17:14:03 UTC | #13

[quote="georgezgeorgez, post:3, topic:196, full:true"]
Using BDK would be a great story
[/quote]

[quote="georgezgeorgez, post:4, topic:196"]
That repo may not be mature enough for our usecase. It is likely that we will need to contribute to those repos in any case.
[/quote]

The Rust library can be cross-compiled for desktop. They're making progress in this direction. We can contribute for sure.

-------------------------

vilkris | 2023-09-11 06:29:17 UTC | #14

What I'm saying is that in the short term if we want a quick path to BTC <> ZTS swaps we don't necessarily need to spend time focusing on a Bitcoin wallet UX inside Syrius.

I just want to make sure we discuss what the short term goal is before we start implementing a Bitcoin wallet for holding/sending/receiving BTC into Syrius just because.

If such a Bitcoin wallet is integrated, then I would like to see UI designs for how the Bitcoin wallet functions within Syrius from the user's perspective before implementation is started.

[quote="georgezgeorgez, post:7, topic:196"]
that complexity might be better managed in a single spot

even with the idea of single use btc keypairs, what happens to those utxos if the swap does not complete? btc fees are real
[/quote]
The complexity would be managed in a single spot, in Syrius. Syrius still needs the capability to create BTC keypairs and needs a connection to a BTC node, but the HTLC contract's P2SH address can be funded from the user's BTC wallet of choice instead of a BTC wallet inside Syrius.

If the swap is unsuccessful, the user can recover their deposit with Syrius with the swap's one-time keypair. The user inputs the address they want to receive the recovered funds on. This should work unless I'm missing something.

[quote="georgezgeorgez, post:7, topic:196"]
from a systematic standpoint, building the base layer capability would make sense, but from an adoption/trend standpoint, integrating with lightning first may be better
[/quote]
Base layer vs lightning I'm not sure. That's up for debate which makes more sense for us. Would base layer have more volume/liquidity?

[quote="sol, post:8, topic:196"]
`bitcoin_base` seems viable, though it was only published a month ago. We should perform a security evaluation for any such dependencies, as well as rigorous testing to confirm compatibility.
[/quote]
When I tried out `bitcoin_base` it had some obvious issues, so it doesn't seem production ready yet at least.

-------------------------

0x3639 | 2023-09-11 12:26:54 UTC | #15

[quote="vilkris, post:14, topic:196"]
Base layer vs lightning I’m not sure. That’s up for debate which makes more sense for us. Would base layer have more volume/liquidity?
[/quote]

I read something on twitter recently that Lightning has 5000 BTC on there.  So not much.  I personally find it hard to use the lightning layer.  My recommendation is we use the base layer.

-------------------------

sol | 2023-09-11 13:45:29 UTC | #16

[Lightning Stats](https://1ml.com/statistics)

Eventually, we should support both L1 and LN.
Each has their pros and cons in this context, but we can appeal to a larger audience if we prioritize L1.

-------------------------

georgezgeorgez | 2023-09-11 15:46:25 UTC | #17



Hmm.. We need to dive into what the actual utxo scripts and unlocking process would be. I'm not 100% sure.

When I say "btc fees are real" I mean that we should not rely on making actual txs to organize utxos into the right wallets. Importing keys is also a pain for the average user.

---

Let's say Alice starts with a single utxo "A" that is managed by an existing BTC wallet. She is swapping for Bob's ZNN.

**Case 1: Alice locks first.**
1. Bob must provide Alice a BTC address/keypair to send to. Alice provides Bob a ZNN address. They agree to swap timing parameters.
2. Alice generates a preimage secret.

3. Alice broadcasts a BTC tx that looks roughly like:
Inputs
A - must be signed by the existing wallet
Outputs
B - htlc script: within a certain number of blocks, only Bob's provided key can unlock if he provides preimage to specified hashlock. After that number of blocks, can be can unlocked by Alice's existing wallet. (I think this script should be possible right?)
A' - Change that can be unlocked by the existing wallet

Note: Unlike in NoM, Alice does not need to explicitly reclaim her funds if the timelock expires. In fact she shouldn't as that would require an unnecessary on-chain tx.
Alice's BTC wallet must be able create such a TX, and recognize utxo B as under its ownership if the timelock should expire. Ideally it should be able to generate/manage preimages as well, or it must be able to easily accept a preimage as a param when creating the htlc. Not sure if we can assume that most wallets have these capabilities.

4. Alice must inform Bob of the tx she just created or Bob must be scanning the BTC chain. In any case, Bob must be able to interpret the script of B and verify that it is what he and Alice agreed to.

5. Bob creates an HTLC on NoM using the same hashlock and an expiration time (NOT BLOCK HEIGHT) that is expected to expire before the BTC "time"lock (blockheight lock) expires. This should be the subject of a whole other discussion.

6. Bob must either inform Alice of the nom htlc or Alice must scan. This is the same as the ZTS-ZTS and the htlc lookup by id can be used. Alice must verify the parameters.

7. Alice can then unlock Bob's htlc on NoM. She will need to use the preimage she used for the BTC htlc. How smooth this is would depend on her wallet(s) support for preimage management.

8. Bob needs to scan NoM for preimages. And then once it finds it, he needs to get it over to his bitcoin wallet, so that it can sweep output B. Again how smooth this is depends on his wallet(s) support for preimage management.

---

I will do the same analysis in a bit for Case 2: Bob locks first
I think it will be similar but need to be thorough.

[quote="vilkris, post:14, topic:196"]
The complexity would be managed in a single spot, in Syrius. Syrius still needs the capability to create BTC keypairs and needs a connection to a BTC node, but the HTLC contract’s P2SH address can be funded from the user’s BTC wallet of choice instead of a BTC wallet inside Syrius.

If the swap is unsuccessful, the user can recover their deposit with Syrius with the swap’s one-time keypair. The user inputs the address they want to receive the recovered funds on. This should work unless I’m missing something.
[/quote]

Can you explain your understanding of the funding step a little more?

Are you saying that first we will do a simple BTC send to an address managed by Syrius which will then create the BTC HTLC?
It's an extra transaction which has tx fees ($$)
If we don't want the extra tx, we either need outside wallets to have direct support for HTLCs.
Even if those wallets can broadcast a raw tx templated by Syrius (not a great ux), I'm not sure they will recognize htlc utxos.

For reclaim/recover, it seems like you are broadcasting an extra tx on chain ($$) which you don't need to simply for the sake of wallet organization, instead of managing keys.

-------------------------

vilkris | 2023-09-11 20:23:23 UTC | #18

[quote="georgezgeorgez, post:17, topic:196"]
Note: Unlike in NoM, Alice does not need to explicitly reclaim her funds if the timelock expires. In fact she shouldn’t as that would require an unnecessary on-chain tx.
Alice’s BTC wallet must be able create such a TX, and recognize utxo B as under its ownership if the timelock should expire. Ideally it should be able to generate/manage preimages as well, or it must be able to easily accept a preimage as a param when creating the htlc. Not sure if we can assume that most wallets have these capabilities.
[/quote]
While this is technically true I don't think it's practical to implement. The expired HTLC can only be spent with the refund script, for which you need the HTLC's details if the script has to be reconstructed. You also need the funding tx's data. How do we back up that information? If they import their keys to any other wallet they will not have access to the funds.

In the case of an automated market making client this could make sense to manage and backup the expired HTLCs so they could be used as inputs directly, since that BTC wallet and client would be used for one purpose only and managing the refund details could be feasible.

[quote="georgezgeorgez, post:17, topic:196"]
Can you explain your understanding of the funding step a little more?

Are you saying that first we will do a simple BTC send to an address managed by Syrius which will then create the BTC HTLC?
It’s an extra transaction which has tx fees ($$)
If we don’t want the extra tx, we either need outside wallets to have direct support for HTLCs.
Even if those wallets can broadcast a raw tx templated by Syrius (not a great ux), I’m not sure they will recognize htlc utxos.
[/quote]
Syrius creates the HTLC script which is converted to a P2SH address that can be funded from any wallet. Outside wallets don't need HTLC support, they're just sending a regular transaction to the P2SH address - no extra transactions.

-------------------------

georgezgeorgez | 2023-09-11 22:04:32 UTC | #19

Can we use P2TR instead of P2SH?

And good point with P2SH - Scipt HASH.. External wallet doesn't need the full script. Just the hash which will be generated by Syrius. Spender will need to provide the script. I was thinking in terms of raw scripts, doh.

So you're right that even to spend the "reclaimed" utxo you would need the script, and it couldn't be reconstructed unless you had the full details of the htlc. But is backing up that data in Syirus much complex than backing up preimages in Syrius which we probably have to do in some way already? I guess with preimages, we have things like preimage hash chains. 

If you're doing anything more complex than a p2pkh, won't there usually be additional data that has to be backed up by the wallet? I wonder if miniscript can help. https://bitcoin.sipa.be/miniscript/

If blockspace is increasingly competitive, the additional transaction does make a difference. But yeah I see your point.

-------------------------

vilkris | 2023-09-12 08:05:41 UTC | #20

[quote="georgezgeorgez, post:19, topic:196"]
Can we use P2TR instead of P2SH?
[/quote]
Probably yes, but if we're using vanilla HTLC scripts I don't think there will be big difference in tx fees. There are very few examples utilizing P2TR, so it would require a deep understanding of taproot and BTC transactions in general to get it right.

[quote="georgezgeorgez, post:19, topic:196"]
But is backing up that data in Syirus much complex than backing up preimages in Syrius which we probably have to do in some way already?
[/quote]
For ZTS swaps we store preimages in a local database, but that db is just available for that instance of Syrius. This doesn't really matter on NoM because you can always recover your funds from the smart contract with your address and the HTLC's ID.

With BTC you need the refund script in order to recover. In case the client's data storage is wiped out, I've seen two ways of managing this in existing HTLC swap clients:
1. Give the user the option to export the refund script + the swap's private key into a text file for later use.
2. Store the refund script encrypted in some external storage that can be accessed and decrypted by a keypair held by the user.

[quote="georgezgeorgez, post:19, topic:196"]
If you’re doing anything more complex than a p2pkh, won’t there usually be additional data that has to be backed up by the wallet? I wonder if miniscript can help. https://bitcoin.sipa.be/miniscript/
[/quote]
Output descriptors are used in some cases but I'm not sure if they work for this use case. https://github.com/bitcoin/bitcoin/blob/master/doc/descriptors.md

[quote="georgezgeorgez, post:19, topic:196"]
If blockspace is increasingly competitive, the additional transaction does make a difference. But yeah I see your point.
[/quote]
Yes it's a downside but if the swap is funded from an internal BTC wallet inside Syrius, then the user will have to make an extra transaction to first fund the Syrius BTC wallet. If the swap is funded from an external wallet then at least in the happy case scenario it will only require both parties to pay for one BTC tx.

If the user imports their BTC keys into Syrius, then we couldn't use the NoM keypair's entropy to deterministically create the BTC wallet.

-------------------------

georgezgeorgez | 2023-09-12 14:04:24 UTC | #21

[quote="vilkris, post:20, topic:196"]
Yes it’s a downside but if the swap is funded from an internal BTC wallet inside Syrius, then the user will have to make an extra transaction to first fund the Syrius BTC wallet.
[/quote]

Unless Syrius becomes their daily driver. In the future, I think we will need a full BTC wallet in Syrius that can send, receive, and transparently interact with NoM. I would need to research what exactly we would need to support to be viable as a production wallet. If we want to grow the community, our target consumer must be the sovereign individual, and not the NoM bagholder lmao.

But ok, let's get an MVP for just the atomic swap. 


[quote="vilkris, post:20, topic:196"]
There are very few examples utilizing P2TR, so it would require a deep understanding of taproot and BTC transactions in general to get it right
[/quote]

Tapscript is the same as script but with a few tweaks particularly around multisig.
https://bitcoinops.org/en/topics/tapscript/

https://river.com/learn/terms/m/merkelized-alternative-script-tree-mast/

There is also MAST which is a big improvement.
Basically you commit the root node of a merkle tree, where the leaves are different spending scripts.
To spend you only have to reveal the script you are actually using and the merkle path to the root. The unspent scripts are never revealed.

For example in our case we have 2 spending paths: the htlc unlock and the reclaim. H() is the hash function.
H(htlc script) = X
H(reclaim script) = Y
H(X,Y) = R

The PT2R would just publicly commit to R
To unlock: I would need to provide the following data.
htlc script sig, htlc script, Y

The chain would then be able to verify the htlc script sig unlocks the htlc script.
It would be able to hash htlc script to produce X, and then do the combined H(X,Y) to get R.
Reclaim script is never revealed.

Likewise, reclaiming would be the same.
You only need:
reclaim script sig, reclaim script, X

P2TR is basically just being able to pay to Schnorr sig or MAST.

Schnorr, Tapscript, MAST, P2TR = Taproot
https://river.com/learn/what-is-taproot/

-------------------------

vilkris | 2023-09-15 06:53:28 UTC | #22

I made a sequence diagram of how I see an MVP ZTS <> BTC swap working in Syrius. This is the happy case flow.

![flow|609x500](upload://wBLAZKLOQwToXchCu42rNgIRY5N.png)

Someone will probably wonder why Bob has to send the counter HTLC's details manually to Alice, since this is not the case with ZTS <> ZTS swaps. While it would probably be possible to scan all BTC transactions looking for an HTLC script that matches what Alice is expecting to see, there are two reasons I don't think this should be done.

 1. I suspect it will be technically fairly challenging to implement such a scanner.

 2. From a UX standpoint it can be argued that it is better that Bob has to explicitly notify Alice when the BTC HTLC is ready to be reviewed. This is because, depending on how many confirmations we require, the BTC TX can take 30 to 60 minutes to be confirmed. If Bob has to notify Alice, then Alice doesn't have to actively keep monitoring her client waiting for the BTC TX to be confirmed. Once Bob notifies Alice, Alice can continue the swap right away.

To utilize proxy unlock and watchtowers it would make sense to always start the swap on the NoM side.

-------------------------

0x3639 | 2023-09-15 10:47:18 UTC | #23

I have a few questions.

During this step, will Alice provide a BTC address managed by a different wallet?

![Screenshot 2023-09-15 at 5.39.18 AM|690x175](upload://jWsp7RybjWpRv6t4j7xKIMdKfmu.png)

It looks like Bob sends the BTC to the P2SH address, not the address provided by Alice.  How does the BTC get into the address that Alice provided? 
![Screenshot 2023-09-15 at 5.44.49 AM|690x132](upload://yFDqsUA7BXDMCM52eRWCcWRvkDg.png)

-------------------------

vilkris | 2023-09-15 13:05:32 UTC | #24

[quote="0x3639, post:23, topic:196"]
During this step, will Alice provide a BTC address managed by a different wallet?
[/quote]
Yes.

[quote="0x3639, post:23, topic:196"]
It looks like Bob sends the BTC to the P2SH address, not the address provided by Alice. How does the BTC get into the address that Alice provided?
[/quote]
The BTC is held in the P2SH address. Alice can unlock the funds with her preimage and the public key that was created for the swap. When she unlocks the funds the receiving address is set to the address she specified in the first step.

-------------------------

0x3639 | 2023-09-15 13:07:07 UTC | #25

I see.  Makes sense.

-------------------------

sol | 2023-09-15 14:45:38 UTC | #26

2. I believe it would be better for Alice to assess tx confirmation and unlock when she feels it is sufficient or when block confirmation = 6, whichever comes first.

-------------------------

sol | 2023-10-05 15:18:10 UTC | #27

For anyone interested, this developer is working on Solana<-> BTC/LN swaps.
- https://github.com/adambor/SolLightning-readme
   - Including a [PoC](https://github.com/adambor/SolLightning-readme#test-the-poc)
- https://github.com/adambor/btcrelay-libs
- https://github.com/adambor/crosslightning-libs

-------------------------

vilkris | 2023-10-05 19:20:17 UTC | #28

Good find. Definitely good reference material. There are similarities with our ideas for cross-chain swaps and apparently they're using PTLCs. Since they're using a relay, the protocol only requires three on-chain transactions. They also have the watchtower and proxy unlock idea and the watchtowers are incentivized by small fees to unlock the user's funds.

-------------------------

0x3639 | 2023-10-05 19:28:08 UTC | #29

[quote="vilkris, post:28, topic:196"]
watchtowers are incentivized by small fees to unlock the user’s funds.
[/quote]

Where does that fee come from?  When they make the initial P2P swap?

-------------------------

vilkris | 2023-10-05 19:41:53 UTC | #30

[quote="0x3639, post:29, topic:196"]
Where does that fee come from? When they make the initial P2P swap?
[/quote]
This is from the [documentation](https://github.com/adambor/SolLightning-readme/blob/main/sol-onchain-swaps.md#watchtowers):

> We can reduce the trust aspect by using multiple watchtowers, further we can incentivize watchtowers by letting them claim the Solana in a PTLC PDA (needed for the account to be rent exempt ~0.0027 SOL). We can then merge this watchtower implementation with BTC Relay implementation, allowing the relayers to earn fees by claiming the swaps on behalf of the clients.

I'm not sure how exactly that mechanism works on Solana.

In a sense these are P2P swaps, but the swap protocol relies on "intermediaries", which are individual liquidity providers running servers that basically work as automated counterparties for the swap. They need to have liquidity on both chains. The documentation suggests the intermediaries have a reputation that is stored on the Solana blockchain and the reputation is dependent on successful/unsuccessful swaps.

-------------------------

