Thread: proof-of-pillar-or-sentinel
0x3639 | 2024-03-27 15:20:17 UTC | #1

I’m thinking about how pillars and sentinels can prove ownership so when people talk to them they know for sure they are talking to a “real” owner.  THORChain has a tool like this where they relay signed messages directly from the node to Discord.   The message is signed and certain to have come from the node.  The devs can interact with real “node” operators this way.  

As proposals come in I hope to interact with the community to get feedback.  But how does the community know I or anyone else actually runs a node?  And how does a Pillar owner know they are interacting with someone who delegates to them or owns ZNN?  

Do you think this basic proof of ownership would be a valuable tool?  This could eventually extend into a more robust tool in the wallet where pillars and delegator could interact.

-------------------------

romeo | 2022-04-26 13:25:48 UTC | #2

This is actually a really important aspect for when the community grows to a larger footprint - there will no doubt be instances of people trying to masquerade as infrastructure owners. Can the signing function within Syrius be used to achieve this?

-------------------------

0x3639 | 2022-04-22 01:41:56 UTC | #3

@georgezgeorgez said yes but we need some code to convert the public key into a wallet address.  We can either do this as a small A Z project or I can fund and hope to seek reimbursement from A Z.

-------------------------

romeo | 2022-04-22 03:27:49 UTC | #4

if there are a few more "small" bits like that we can maybe pool them together as a single A-Z proposal.

-Covert public key for signing: 200znn
-Code discourse plugin for Syrius integration: 200znn

for example - even if a dev hasn't been identified yet to deliver it - as long as it gets approved then we can find someone

-------------------------

vilkris | 2022-04-22 06:38:31 UTC | #5

How is this done on THORChain? Is it some centralized service that relays the signed messages to Discord or is it directly integrated into a wallet or something? What options does the user have when posting to Discord via the relayer?

I'm not sure how you can turn the public key into a wallet address without the private key or if it's even possible but maybe @georgezgeorgez has looked more into this.
A workaround for this would be to query the address's last account block and get its public key from there. The caveat is that this would only work for addresses that have created at least one transaction - of course all pillars, sentinels and delegators meet this requirement.

Right now you could sign your entire message and provide the signature and public key in your post and anyone could use syrius to prove you wrote the message and then use the public key to query the node to verify you own the pillar's address. This could be streamlined and made more user friendly by doing some updates to syrius.

-------------------------

0x3639 | 2022-04-22 12:02:14 UTC | #6

[quote="vilkris, post:5, topic:202"]
How is this done on THORChain?
[/quote]
I believe they have a centralized relayer that is hosted by 9 Relms

[quote="vilkris, post:5, topic:202"]
I’m not sure how you can turn the public key into a wallet address without the private key or if it’s even possible but maybe @georgezgeorgez has looked more into this.
[/quote]
George indicated it is possible.  The account is hashed and "truncated" in the public key.  He said his last code review discussed addresses  https://t.me/zenon_wiki_code_review_club/489

![image|417x499](upload://rI3Pu3I5RAUtcSIEU7zlTAovxx7.png)

[quote="vilkris, post:5, topic:202"]
use the public key to query the node to verify you own the pillar’s address.
[/quote]
I think this is the part that is missing.  How do we go from public key to address?  I'm cool with this being manual initially.  We need to give people badges in the forum.  If we can manually confirm pillar owners we can give them badges.  Once they have badges we can put them in a Pillar group.  Eventually this needs to be included in the wallet so pillars can communicate authentically with delegators. etc..

-------------------------

vilkris | 2022-04-22 19:47:17 UTC | #7

Okay George was right. I took another look at it and indeed the address can be derived from the public key. I updated the test endpoint I have running that can now be used to validate ownership of an address.

If you want to use it to manually validate a pillar owner you can use it here (input the data in the "Content" tab and press send):
https://reqbin.com/7pdoxmxx

-------------------------

0x3639 | 2022-04-22 19:51:04 UTC | #9

Awesome.  I'm testing this now

-------------------------

0x3639 | 2022-04-22 19:59:12 UTC | #10

This works perfectly!!  @romeo we can use this to verify pillar owners and assign badges?  I should not verify myself.  I can see how something like this could get integrated into a bunch of stuff.  

@vilkris let me know if you want me to pay you for this or we should add to the A Z proposal we are making for the forum.

```
{
  "message": "deeZNNutz.com",
  "address": "z1qrztagl9rukq3ltdflnvg4zrvpfp84mydfejk9",
  "publickey": "88c0ebc7de1aa0b6e1958b4ead1f43df15f2e92f3f876c564005ee38da9a77f0",
  "signature": "24b719f5209bbf653d27445e8c298a4cd4f4f5a1c384e079de9945516d4b999a5acc57dca49a6778110176f409144db645243fc7f88550e0f42b93bb17ed190e"
}
```

-------------------------

vilkris | 2022-04-22 20:05:29 UTC | #11

No need. Everything was already set up and some better solution will have to be made down the line anyway.

-------------------------

romeo | 2022-04-22 21:35:21 UTC | #12

let me play around with this today! awesome

-------------------------

0x3639 | 2022-04-27 08:57:10 UTC | #13

@vilkris we are starting to use this tool now. Our goal is to create a Pillar group in the forum so we can communicate with all pillars.  I'm wondering if you can add one more step in your script.  Can you automatically check the "address": "" against the list of pillar address?  If the signed message came from the provided address AND the address is a registered pillar, then return TRUE.  If address fails or know pillar address fails, then return FALSE.  

Can we open source this too so Pillars can see the code?  Thanks so much!

-------------------------

vilkris | 2022-04-27 19:17:56 UTC | #14

The endpoint has now been updated and will check if the address is a pillar or sentinel.
It will respond with the following:
```
{"is_valid_signature": true, "is_pillar": true, "pillar_name": "DeeZNNutz.com", "is_sentinel": false}
```

If it is a pillar address the pillar's name will also be returned for easier verification.

I'll upload the source code to github tomorrow.

-------------------------

0x3639 | 2022-04-27 19:28:18 UTC | #15

Amazing!!!  thank you so much.  

@romeo Check this out.  No more manual checking the getALL function.  We should create a Sentinel Group too (with a label).  What do you think?

-------------------------

vilkris | 2022-04-28 10:32:23 UTC | #16

The source code is now available [here]( https://github.com/zenon-tools/verify-nom-address). The endpoint is just a wrapper for this program and the program can be run locally on your PC so you don't necessarily need to trust the endpoint.

-------------------------

0x3639 | 2022-04-28 16:35:10 UTC | #17

thank you so much for doing this.  I will try locally.

-------------------------

sol | 2022-05-10 17:23:46 UTC | #18

I didn't know you had written this when I worked on the same problem! 😅
Thanks for sharing your solution!

-------------------------

