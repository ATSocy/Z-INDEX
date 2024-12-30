Thread: syrius-atomic-swap-test-required-wallet-restart
0x3639 | 2023-05-07 20:45:41 UTC | #1

@vilkris Please see issue I encountered below.  Wanted to post here before creating an issue on Github.  

Setup on TESTNET

Alice starts P2P with Bob.  Alice locks 1000 tQSR.
Bob joins and locks 100 tZNN
Alice receives and swaps
Alice receives 100 tZNN.
Bob scans looking for secret.  
After 3-4 minutes Bob did not find the secret.  I had to restart SYRIUS to see the secret.  The issues starts around minute 5 of the video.

Full Video
https://www.youtube.com/watch?v=kI2PLgfyQxk

Allice
Your Address: z1qr7f5qtetr3j2zpsxlk52x47ghy98fpxwnxy8d
Counterparty Address: z1qqtuepp88cwzjrteaa657hxgmgadycwjs7mgg8
Your Deposit ID: 74825e4e6f0b204456efade2ce79d8be588a333759a45e6e6ae8d38c8fc730ab
Counterparty deposit ID: 582ffc4d73fa2be15a21b7ff13f2e3ba6b2b689acaaffd2547aed535b363b874
Hashlock: 50ecefe7e79505a0c830ea66208d079ebb13c6120af0c709c6e213332ac9c3cc
Secret: 237cab8e47e761269e7ea007de596afb334fdd1c26613621c48d9bf33dc1af54

Bob
Your Address: z1qqtuepp88cwzjrteaa657hxgmgadycwjs7mgg8
Counterparty Address: z1qr7f5qtetr3j2zpsxlk52x47ghy98fpxwnxy8d
Your Deposit ID: 582ffc4d73fa2be15a21b7ff13f2e3ba6b2b689acaaffd2547aed535b363b874
Counterparty deposit ID: 74825e4e6f0b204456efade2ce79d8be588a333759a45e6e6ae8d38c8fc730ab
Hashlock: 50ecefe7e79505a0c830ea66208d079ebb13c6120af0c709c6e213332ac9c3cc
Secret: 237cab8e47e761269e7ea007de596afb334fdd1c26613621c48d9bf33dc1af54

-------------------------

vilkris | 2023-05-08 16:01:14 UTC | #2

Thanks for posting this. Has this only happened once? Were the two wallets using the same node?

-------------------------

0x3639 | 2023-05-08 18:23:06 UTC | #3

It only happened once.  I was using my node 

wss://testnet.deeznnutz.com:3598

-------------------------

0x3639 | 2023-05-08 18:49:42 UTC | #4

I just realized that I was using a VPN and maybe that was causing the issue.  Let me try without the VPN and see if that improves things.

-------------------------

0x3639 | 2023-05-08 18:55:30 UTC | #5

Yep, I'm pretty sure the VPN was causing issues.  Both VMs had VPN connections and both were showing strange behavior.  I turned both off and issues have gone away.

-------------------------

vilkris | 2023-05-08 19:13:45 UTC | #6

Okay, I did some investigation and was able to reproduce the problem by intentionally cutting off the node connection while Syrius is scanning for the swap secret. The swap secret scanner does not gracefully handle that situation and terminates. This will have to be fixed.

-------------------------

0x3639 | 2023-05-08 19:28:18 UTC | #7

Got it.  Makes sense.  My VPN seems to be unstable, and drops connections to my node constantly.  Glad I was able to discover this.

-------------------------

vilkris | 2023-05-10 13:26:14 UTC | #8

The latest updates in the P2P swap branch should fix this issue. For some reason Github Actions isn't working so Syrius will have to be built from source.

-------------------------

0x3639 | 2023-05-10 13:54:49 UTC | #9

OK, I'll try to test today.

-------------------------

