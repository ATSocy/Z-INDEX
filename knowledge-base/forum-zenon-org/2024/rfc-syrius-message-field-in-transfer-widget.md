Thread: rfc-syrius-message-field-in-transfer-widget
sol | 2023-02-08 22:34:57 UTC | #1

Hello ZNNAliens!

I've managed to integrate an optional message (data) field in Syrius. Please review the attached images and let me know if you like/dislike the design changes.
Any feedback is appreciated! :slight_smile: 

I've tested the field and haven't experienced any crashes in various scenarios: empty field, all keyboard chars entered, 10k char payload, etc.

Code can be reviewed here: https://github.com/Sol-Sanctum/syrius/commit/af4b3db82200ecff366e2ed17d5770987cb4d9ce

Send Medium widget
![send_medium|690x444](upload://8aC7BFcAsnRWd0Ea6wvIQPxcbOX.png)

Send Large widget
![send_large|690x260](upload://jRrrpwq0T2svsc34RV3fMWIke6d.png)

Send confirmation message
![send_confirmation|690x101](upload://6C7eUc73UioWAExnBuCDSCzZgA3.png)

-------------------------

cryptocheshire | 2022-07-21 18:39:17 UTC | #2

Wadn't it already possible to sign a transaction and include a message in the process?

-------------------------

sol | 2022-07-22 02:43:41 UTC | #3

Not in the way you're thinking. 
Currently, in Syrius, users can navigate to Settings > Security > Sign to sign an arbitrary message with their address, but that data isn't submitted in a transaction.

Check out [_sendPayment(), line 224](https://github.com/zenon-network/syrius/blob/master/lib/widgets/modular_widgets/transfer_widgets/send/send_medium.dart) for what I'm working on.

I copied the logic used for [line 79  of cli_handler.dart](https://github.com/zenon-network/znn_cli_dart/blob/master/cli_handler.dart) and integrated it in the transfer menu in Syrius. This way, users can submit data/messages on-chain with a (free!) transaction.

-------------------------

cryptocheshire | 2022-07-21 20:27:25 UTC | #4

I see, that's pretty neat! Is there any potential risk to ledger bloating because of this? Just hypothetically

-------------------------

sol | 2022-07-21 20:55:05 UTC | #5

Good question! There may be that risk if some bad actors decide to spam the network. 
znn_cli_dart already provides us with this capability and I don't think anyone has been abusing that. I could be wrong.
I wonder if Professor Z and/or Mr Kaine already addressed this concern somewhere.

I'd welcome input from @georgezgeorgez @Dumeril @0x3639 @romeo re: the hypothetical question Shazz posed. 

We could potentially limit the data payload further (current limit is ~10kb, I think) if we feel this would burden our Sentinels and Pillars with exorbitant storage costs in the future.

-------------------------

0x3639 | 2022-07-21 21:55:09 UTC | #6

Doesn't Plasma already act as an anti-spam mechanism?  You would need to fuse a lot of QSR or do a lot of "computational work" to spam the network with messages on transactions.  

So my guess is we have an antispam mechanism to prevent this.  Not sure about chain bloat.  Mr. Kaine seems to reference this a lot in TG.  

But I do like the idea of adding a signed memo field.

-------------------------

Dumeril | 2022-07-22 18:18:10 UTC | #7

The current limit is 16k. It would be interesting to run some simulations to visualize chain growth depending on tx # and sizes, but generally I guess @0x3639 is correct - plasma is at least meant to prevent chain bloat due to spam; the required amount grows linearly with the data size in an account block.

Btw., it wouldn’t be a storage problem for only sentinels/pillars currently, as every node stores the same data.

-------------------------

0x3639 | 2022-07-24 23:25:38 UTC | #8

No comments on the layout, etc...  I think everything looks great.

-------------------------

zyler9985 | 2022-07-25 08:08:49 UTC | #9

I think it's a great improvement, to be able to add a description and then the confirmation check ... we want everything to be easy and intuitive for the sake of mass adoption

-------------------------

