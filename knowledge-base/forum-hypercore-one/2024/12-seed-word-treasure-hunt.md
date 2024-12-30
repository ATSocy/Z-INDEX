Thread: 12-seed-word-treasure-hunt
0x3639 | 2024-03-23 10:14:47 UTC | #1

Let's use this thread to document the 12 seed word treasure hunt created by the alphanet devs

## Problem

Find the last 4 words to a seed phrase.

Seed Phrase:
`oblige dilemma hurry disorder happy spoil shiver key`
The last 4 words to the seed phrase are missing.  

Resulting Address:
`z1qrn3jeapt848zxg3akf2ewhrxxwsa945sj798s`

Hints:

```
;tVMd3L1CKM4wFmyxEEEUV2bY;
;BynQtpeUyWTXKGTrGhdV2Q==;
,vtv3f5aKY0jGQglP9a1AGw==,
;4Fdzw1k=zzzzzzzzzzzzzzzz;
```
Support:

[@zenon_network Tweet Nov 12, 2021](https://twitter.com/Zenon_Network/status/1461013302369132544)
> Day 2
> Treasure hunt clue: Quantum computers can't break it.
> 
> Solve the puzzle and get 4.745.134 $PP!
> #AlphanetBigBang $ZNN $QSR

[@zenon_network Tweet Nov 15, 2021](https://twitter.com/Zenon_Network/status/1460240120309760010)
> Day 4
> Never doubt you can make history.
> You already have.
> 
> #Bitcoin #Taproot $ZNN

[@zenon_network Tweet Nov 14, 2021](https://twitter.com/Zenon_Network/status/1459863534330957825)
> Day 5
> The key to #Bitcoin smart contracts is _______
> 
> Look for the final piece of the puzzle in block 709.632 to unlock the 4.745.134 $PP reward.
> 
> The winner takes it all!
> #AlphanetBigBang  $ZNN $QSR

[@zenon_network Tweet Dec 11, 2021](https://twitter.com/Zenon_Network/status/1469733266093588483)
> Treasure hunt deadline
> 
> On 21st of December the $QSR quest prize will be burned.
> 
> ➡️ Recap the clues 
> ➡️ Be the first to find the missing words
> ➡️ Secure the reward

[@zenon_network Tweet Dec 23, 2021](https://twitter.com/Zenon_Network/status/1474087562142785537)
> The community decided to burn the 4.745,134 $QSR prize.
> 
> Quest address:
> z1qrn3jeapt848zxg3akf2ewhrxxwsa945sj798s
> 
> The mystery of the Taproot activation block remains unsolved until some brave #ZNNAliens will uncover the answer.




https://twitter.com/TheDev1776/status/1722450829158883699
https://twitter.com/crypto_culture_/status/1460002976907595779
https://mempool.space/block/0000000000000000000687bca986194dc2c1f949318629b44bb54ec0a94d8244

https://www.reddit.com/r/Bitcoin/comments/qtk492/someone_tried_to_put_some_ascii_art_into_the/

-------------------------

CryptoFish | 2024-03-23 12:46:38 UTC | #2

The `nonce` and `password` seem to be the only variables needed to decrypt the last puzzle.

```
// tVMd3L1CKM4wFmyxEEEUV2bYBynQtpeUyWTXKGTrGhdV2Q==
var cipherData = "0xb5531ddcbd4228ce30166cb11041145766d80729d0b69794c964d72864eb1a1755d9";
// vtv3f5aKY0jGQglP9a1AGw==
var salt = "0xbedbf77f968a6348c642094ff5ad401b";
// 4Fdzw1k=zzzzzzzzzzzzzzzz
var nonce = "0xe05773c35900000000000000";

var password = "taproot";
```

-------------------------

coinselor | 2024-03-25 02:47:20 UTC | #3

Are you just assuming the encryption algo used is AES-256?

-------------------------

CryptoFish | 2024-03-25 07:38:31 UTC | #4

Actually, I'm assuming a lot a things, but aes-256 would be the most logical choice if I had to pick one. But then again, it could be a lot of things.

-------------------------

