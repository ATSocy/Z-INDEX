Thread: musig2-implementation
aliencoder | 2023-08-01 20:34:01 UTC | #1

I've found a Go implementation of the [MuSig2 protocol](https://medium.com/blockstream/musig2-simple-two-round-schnorr-multisignatures-bf9582e99295):

https://gitlab.com/yawning/musig2-voi

Mirror:

https://github.com/Yawning/musig2-voi

@georgezgeorgez might be of interest

@0x3639 the dev seems pretty smart. Maybe we can engage him and propose to apply for an AZ grant: "No, this has not been audited. Fuck you, pay me."

Also check out this:

https://github.com/MixinNetwork/multi-party-sig

-------------------------

sol | 2023-08-01 20:43:40 UTC | #2

Someone has to greenpill @yawning. He'll fit right in.

-------------------------

0x3639 | 2023-08-02 22:27:04 UTC | #3

[quote="aliencoder, post:1, topic:170"]
I’ve found a Go implementation of the [MuSig2 protocol ](https://medium.com/blockstream/musig2-simple-two-round-schnorr-multisignatures-bf9582e99295):
[/quote]

How are you planning to use this code?  I will see if he is interested.

-------------------------

aliencoder | 2023-08-03 07:00:44 UTC | #4

[quote="0x3639, post:3, topic:170"]
How are you planning to use this code?
[/quote]

Maybe we'll integrate it somehow into the future.

[quote="0x3639, post:3, topic:170"]
I will see if he is interested.
[/quote]

He might be interested. Check out his [anti-censorship repo](https://github.com/Yawning/obfs4) inspired by [ScambleSuit](https://www.cs.kau.se/philwint/scramblesuit/).

-------------------------

0x3639 | 2023-08-06 10:44:55 UTC | #5

These guys too.  They are based AF.

https://twitter.com/SamouraiWallet/status/1687896997615882241

-------------------------

