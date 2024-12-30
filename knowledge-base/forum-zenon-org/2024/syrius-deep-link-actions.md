Thread: syrius-deep-link-actions
aliencoder | 2023-06-14 20:03:07 UTC | #1

I've started this thread to discuss what can we achieve with the Deep Linking integration in Syrius.

I've already created custom deep links as follows:

Staking: `syrius://stake`
Delegating: `syrius://delegate`
Fusing: `syrius://fuse`
Sentinels: `syrius://sentinel`
Pillars: `syrius://pillar`

@sol suggested adding the `Transfer` action:

Transfer: `syrius://transfer`

The deep link is basically an `URI` object with the following elements:

1. Scheme/protocol: `syrius://`
2. Authority/host: the action to be performed e.g. `stake`, deploy `pillar`, etc.
3. Query Parameters: the query params that are required to perform the action e.g. `amount`, `duration`, etc.

For example, a deep link for staking would look like this:

`syrius://stake?amount=100&duration=3`

In Syrius we can parse this information accordingly and redirect/display a dialog to the user.

We can even add tracking by adding relevant information e.g. `&utm_source=attributeme&utm_medium=website&utm_campaign=znnmarketing`, but I wouldn't add this functionality into Syrius.

We can avoid this by listening for `staking` events that match the query params (`100 ZNN` and `3 months`) after the user clicks on the deep link. If no event is registered within a time interval, you can assume no conversion was made.

-------------------------

mehowbrainz | 2023-06-14 20:00:39 UTC | #2

[quote="aliencoder, post:1, topic:1480"]
We can even add tracking by adding relevant information e.g. `&utm_source=attributeme&utm_medium=website&utm_campaign=znnmarketing`, but I wouldn’t add this functionality into Syrius.
[/quote]

Yes this would require some telemetry within syrius, which we're trying to avoid.

Zenon.Org landing pages will be able to track deeplink clicks with GA events within its funnels, so we'll be able to determine the success of a funnel using such methods. No need to add telemetry within syrius.

-------------------------

vilkris | 2023-06-16 10:50:10 UTC | #3

I know that the syrius scheme is in use with walletconnect, but should a generalized approach be considered for these other functionalities. Instead of syrius, it could be zenon, to allow any client application to implement support.

References from other chains:
https://en.bitcoin.it/wiki/BIP_0021
https://developer.algorand.org/docs/get-details/transactions/payment_prompts/
https://zips.z.cash/zip-0321

-------------------------

aliencoder | 2023-06-16 12:22:18 UTC | #4

The `syrius://` scheme is different from the `zenon:` or `znn:` URI scheme.

Deep link actions don't cover payment requests (bip-0021):

"The purpose of this URI scheme is to enable users to easily make payments by simply clicking links on webpages or scanning QR Codes."

I agree we can create a new ZIP and copy BTC/ALGO's URI scheme for payment requests.

-------------------------

vilkris | 2023-06-16 12:47:53 UTC | #5

My point is that if another wallet wants to react to the deep links, it will have to register a protocol handler for the syrius scheme. Naming could be more generic

-------------------------

mehowbrainz | 2023-06-17 00:09:52 UTC | #6

@aliencoder are there a custom deep link for collecting rewards?

-------------------------

aliencoder | 2023-06-17 09:13:36 UTC | #7

No, but I can do that.

-------------------------

aliencoder | 2023-06-21 21:00:03 UTC | #8

I had some issues with the deep linking actions integration, but we'll have a complete implementation in 1-2 days.


```
// Deep link query parameters
String queryAddress = '';
String queryAmount = ''; // with decimals
int queryDuration = 0; // in months, for staking
String queryZTS = ''; // ZNN and QSR are defaults
String queryPillarName = ''; // for delegation
Token? token;
```

-------------------------

aliencoder | 2023-06-22 10:48:15 UTC | #9

The [Deep Link Actions](https://github.com/alienc0der/syrius/commit/173dac276b0c097d06613e3267cd0d50463248c3) integration is now complete. :alien:

Download the [latest build](https://github.com/alienc0der/syrius/releases/tag/v0.0.7-alphanet) and test it.

Parameter names are listed below. You can combine them in any order to create a valid deep link.

```
'amount' // the address with decimals
'zts' // the ZTS to transfer custom tokens; default ZNN/znn/QSR/qsr
'address'
'duration' // the duration in months, required for staking
'pillar' // the Pillar's name required for delegation
```

Deep link actions example:

```
syrius://transfer?amount=1&address=z1q...&zts=ZNN

syrius://delegate?pillar=DeeZNNutz.com

syrius://stake?amount=1&duration=2

syrius://fuse?amount=120&address=z1q...

syrius://pillar

syrius://sentinel
```

Pillar & Sentinel deep link actions are only used to redirect the user to their respective tabs within the wallet.

-------------------------

