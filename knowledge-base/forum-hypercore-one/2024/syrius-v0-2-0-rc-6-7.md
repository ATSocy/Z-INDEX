Thread: syrius-v0-2-0-rc-6-7
CryptoFish | 2024-03-27 06:16:40 UTC | #1

> :exclamation: This will be the last round if no further issues are found until end of march.

This post will be used to collect issues for test round #7.

Download: [Syrius v0.2.0-rc.6](https://github.com/zenon-network/syrius/releases/tag/v0.2.0-rc.6)

Read [this ](https://forum.hypercore.one/t/syrius-v0-2-0/328/7) post for more information about how to test.

The following issues were fixed:

[details="v0.2.0-rc.0"]
- [Unable to transact on first start](https://github.com/zenon-network/syrius/issues/74)
- https://github.com/zenon-network/syrius/pull/76
[/details]

[details="v0.2.0-rc.1"]
- https://github.com/zenon-network/syrius/pull/78
[/details]

[details="v0.2.0-rc.2"]
- https://github.com/zenon-network/syrius/pull/82
- https://github.com/zenon-network/syrius/pull/83
- https://github.com/zenon-network/syrius/pull/84
- https://github.com/zenon-network/syrius/pull/88
- https://github.com/zenon-network/syrius/pull/89
[/details]

[details="v0.2.0-rc.3"]
- https://github.com/zenon-network/syrius/pull/93
- https://github.com/zenon-network/syrius/pull/94
- https://github.com/zenon-network/syrius/pull/95
[/details]

[details="v0.2.0-rc.4"]
- https://github.com/zenon-network/syrius/pull/98
- https://github.com/zenon-network/syrius/pull/100
- https://github.com/zenon-network/syrius/pull/101
[/details]

[details="v0.2.0-rc.5"]
- https://github.com/zenon-network/syrius/pull/103
- https://github.com/zenon-network/syrius/pull/104
[/details]

-------------------------

coinselor | 2024-03-25 16:11:44 UTC | #2

I just tested it, Camera QR Scanner is now working fine :). Will try to do the missing tests and add them here for completeness.

-------------------------

coinselor | 2024-03-25 17:20:29 UTC | #3

### WalletConnect Test Report

**Version:** 0.2.0-rc.6  
**Environment:** macOS Big Sur v11.7.10  
**Date:** 3/25/2024  
**Tester:** coinselor

#### Pairing

| Test case                                | Description                                                      | Priority | Result |
|------------------------------------------|------------------------------------------------------------------|----------|--------|
| Create pair with wc url                  | Create a walletconnect pair by manually connecting to a wc url.  | PRIO1    | PASS   |
| Create pair with on-screen QR scanner    | Create a walletconnect pair by scanning a QR with the on-screen QR scanner. | PRIO2 | PASS   |
| Create pair with camera QR scanner       | Create a walletconnect pair by scanning a QR with the camera QR scanner. | PRIO2  | PASS   |
| Disconnect a pairing from syrius         | Disconnect a pairing by removing it from the WalletConnect Pairing List. | PRIO1   | PASS   |
| Disconnect a pairing from third-party app| Disconnect a pairing by removing it from third-party application and verify its removal from the Pairing List. | PRIO1 | PASS |
| Expired pairing                          | An expired pairing cannot be used to start a session.             | PRIO1    | PASS       |

#### Sessions

| Test case                          | Description                                                                  | Priority | Result |
|------------------------------------|------------------------------------------------------------------------------|----------|--------|
| Approve session                    | Approve a session and verify the acknowledged session in the WalletConnect Sessions List. | PRIO1 | PASS   |
| Reject session                     | Reject a session and verify inactive pairing.                               | PRIO1    | PASS   |
| Expired session                    | An expired session cannot be used to send requests.                         | PRIO1    |    PASS    |

#### Requests

| Test case       | Description                                         | Priority | Result |
|-----------------|-----------------------------------------------------|----------|--------|
| Approve request | Approve a request and verify it has been approved.  | PRIO1    |        |
| Reject request  | Reject a request and verify it has been rejected.   | PRIO1    |   PASS     |

#### Miscellaneous

| Test case                                          | Description                                                               | Priority | Result |
|----------------------------------------------------|---------------------------------------------------------------------------|----------|--------|
| Pairings and sessions are deleted on delete cache  | Delete cache and verify pairings and sessions are deleted.               | PRIO2    |    PASS    |
| Pairings and sessions are deleted on wallet reset  | Reset and reinitialize wallet and verify pairings and sessions are deleted. | PRIO2   |   FAIL     |


[Issue](https://github.com/zenon-network/syrius/issues/106): **Resetting the wallet does not remove the pairings/sessions**. I was able to import a different priv key, and even the bridge front end was showing and recognizing the addresses of the different private key when I switched them in settings. 

Interestingly, I resetted the wallet once again, and went back to the previous priv key that completed the initial pairing. Pairing was still there, but the bridge front end was showing an error in console log and not updating the addreses anymore (using bridge.staging.zenon.community): 

![image|489x500](upload://4i6BF3GXZO3CyGvhduUc2kFWceW.png)


I also had a few hiccups where the Camera QR scanner detected the code but created a Name Empty, URL Empty pairing. See screenshots:

![image|690x431](upload://13NfXofiCSdPJoKvAn6LN1IjrpS.png)

![image|690x431](upload://1mKgMMO0ED1IO2LDhQbzVppaP05.png)

Note: Didn't test the 'Approve a request' one because I didn't feel like wrapping one ZNN, lol. Didn't we have a wallet connect demo site live somewhere?

-------------------------

CryptoFish | 2024-03-25 19:29:20 UTC | #4

[quote="coinselor, post:3, topic:425"]
Resetting the wallet does not remove the pairings/sessions
[/quote]
Please test this [build](https://github.com/zenon-network/syrius/actions/runs/8425666991#artifacts) by downloading the binaries from the artifacts.

[quote="coinselor, post:3, topic:425"]
I also had a few hiccups where the Camera QR scanner detected the code but created a Name Empty, URL Empty pairing. See screenshots:
[/quote]
@aliencoder can you look at this?

[quote="coinselor, post:3, topic:425"]
Note: Didn’t test the ‘Approve a request’ one because I didn’t feel like wrapping one ZNN, lol. Didn’t we have a wallet connect demo site live somewhere?
[/quote]

You can use the testnet to test the bridge.

Chain Id: 3
Node: wss://syrius-testnet.zenon.community:443
Bridge: https://bridge.staging.zenon.community/
Ethereum: Sepolia

-------------------------

CryptoFish | 2024-03-26 14:04:34 UTC | #5

[quote="coinselor, post:3, topic:425"]
I also had a few hiccups where the Camera QR scanner detected the code but created a Name Empty, URL Empty pairing. See screenshots:
[/quote]

The syrius log should contain some entries under the `WalletConnectCameraCard` process name that might give some more insight in the issue.

-------------------------

coinselor | 2024-03-26 16:11:47 UTC | #6

[quote="CryptoFish, post:5, topic:425"]
WalletConnectCameraCard
[/quote]

I'm not sure which log corresponds to the Empty/Empty issue. But should be in one of these.

```
INFO WalletConnectCameraCard onScannerStarted 2024-03-25 16:09:23.771887: null null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:09:33.057026: Instance of 'StoreSyncEvent' null
INFO WalletConnectCameraCard pairing info 2024-03-25 16:09:33.116588: {topic: dddcc244bb3f9a038189cf310cd82718ae1ade74fb468cb5fdd2767c755f7f73, expiry: 1711383273, relay: {protocol: irn, data: null}, active: false, peerMetadata: null} null
INFO WalletConnectCameraCard onDispose 2024-03-25 16:09:33.384200: null null
INFO WalletConnectService _onSessionProposal event 2024-03-25 16:09:33.845344: {id: 1711382961528190, expiry: 1711383273, relays: [{protocol: irn, data: null}], proposer: {publicKey: a79526d921ee0d365f3b53dc0faadfeb30d5e5e865f81b5ae0a782f3dd538676, metadata: {name: NoM Multichain, description: Bridge tokens, add and stake liquidity, url: bridge.staging.zenon.community, icons: [https://bridge.staging.zenon.community/static/media/zenon-big.d3e07dfc52d3a619fa99.png]}}, requiredNamespaces: {zenon: {chains: [zenon:1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange]}}, optionalNamespaces: {}, pairingTopic: dddcc244bb3f9a038189cf310cd82718ae1ade74fb468cb5fdd2767c755f7f73} null
dressChange])}, optionalNamespaces: {}, pairingTopic: dddcc244bb3f9a038189cf310cd82718ae1ade74fb468cb5fdd2767c755f7f73, sessionProperties: null, generatedNamespaces: null)) null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:09:42.561104: Instance of 'StoreSyncEvent' null
cc244bb3f9a038189cf310cd82718ae1ade74fb468cb5fdd2767c755f7f73, expiry: 1713974982) null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:09:42.566380: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionConnect triggered 2024-03-25 16:09:42.619003: SessionConnect(session: SessionData(topic: b7227008fc0ee19e125cb00e642e7e0ae6bb665faafecb32281f0ff71a832561, pairingTopic: dddcc244bb3f9a038189cf310cd82718ae1ade74fb468cb5fdd2767c755f7f73, relay: Instance of 'Relay', expiry: 1711987782, acknowledged: false, controller: 821ed657f973999dbd3a7867890a54233ad3f00f8adb75823f90eb8a93002755, namespaces: {zenon: Namespace(accounts: [zenon:1:Address 2, zenon:1:Address 1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange])}, requiredNamespaces: {zenon: RequiredNamespace(chains: [zenon:1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange])}, optionalNamespaces: {}, sessionProperties: null, self: ConnectionMetadata(publicKey: 821ed657f973999dbd3a7867890a54233ad3f00f8adb75823f90eb8a93002755, metadata: PairingMetadata(name: s y r i u s, description: A wallet for interacting with Zenon Network, url: https://zenon.network, icons: [https://raw.githubusercontent.com/zenon-network/syrius/master/macos/Runner/Assets.xcassets/AppIcon.appiconset/Icon-MacOS-512x512%402x.png], redirect: null)), peer: ConnectionMetadata(publicKey: a79526d921ee0d365f3b53dc0faadfeb30d5e5e865f81b5ae0a782f3dd538676, metadata: PairingMetadata(name: NoM Multichain, description: Bridge tokens, add and stake liquidity, url: bridge.staging.zenon.community, icons: [https://bridge.staging.zenon.community/static/media/zenon-big.d3e07dfc52d3a619fa99.png], redirect: null)))) null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:09:42.620924: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:09:42.928037: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionRequest triggered 2024-03-25 16:09:51.834918: SessionRequestEvent(id: 1711382993123074, topic: b7227008fc0ee19e125cb00e642e7e0ae6bb665faafecb32281f0ff71a832561, method: znn_info, chainId: zenon:1, params: null) null
WARNING BaseBloc addError 2024-03-25 16:20:44.543093: Bad state: The client closed with pending request "stats.syncInfo". 
INFO ZNN-SDK Websocket connection successfully restarted 2024-03-25 16:20:44.711122: null null
l
INFO WalletConnectService _onPairingDelete triggered 2024-03-25 16:22:31.174910: PairingEvent(id: null, topic: dddcc244bb3f9a038189cf310cd82718ae1ade74fb468cb5fdd2767c755f7f73, error: null) null
INFO WalletConnectService _onRelayClientError triggered 2024-03-25 16:22:31.233850: Instance of 'ErrorEvent' null
INFO WalletConnectService _onRelayClientConnect triggered 2024-03-25 16:22:31.421021: null null
INFO WalletConnectService _onRelayClientError triggered 2024-03-25 16:22:31.430762: Instance of 'ErrorEvent' null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:22:31.433138: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionDelete triggered 2024-03-25 16:22:31.435378: SessionDelete(topic: b7227008fc0ee19e125cb00e642e7e0ae6bb665faafecb32281f0ff71a832561, id: null) null
INFO WalletConnectCameraCard onScannerStarted 2024-03-25 16:28:22.402513: null null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:28:33.155641: Instance of 'StoreSyncEvent' null
INFO WalletConnectCameraCard onDispose 2024-03-25 16:28:33.490472: null null
INFO WalletConnectCameraCard onScannerStarted 2024-03-25 16:29:58.301581: null null
INFO WalletConnectCameraCard onDispose 2024-03-25 16:30:28.628096: null null
INFO WalletConnectCameraCard onScannerStarted 2024-03-25 16:30:33.445010: null null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:30:42.283893: Instance of 'StoreSyncEvent' null
INFO WalletConnectCameraCard onDispose 2024-03-25 16:30:42.611031: null null
```

```
INFO WalletConnectService _onPairingDelete triggered 2024-03-25 16:31:40.426938: PairingEvent(id: null, topic: c8a5f9164963eb5f864bc380ed27a9ee89ac291192ee5d8a233157fd439f3dd1, error: null) null
INFO WalletConnectService _onPairingDelete triggered 2024-03-25 16:31:42.256400: PairingEvent(id: null, topic: d5ad569f239fa5106a144b5adbd081dbe1c1a3734f4d0de4a4e8aa2ae73be1d8, error: null) null
INFO WalletConnectCameraCard onScannerStarted 2024-03-25 16:31:45.471866: null null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:31:54.089202: Instance of 'StoreSyncEvent' null
INFO WalletConnectCameraCard pairing info 2024-03-25 16:31:54.151770: {topic: d5ad569f239fa5106a144b5adbd081dbe1c1a3734f4d0de4a4e8aa2ae73be1d8, expiry: 1711384614, relay: {protocol: irn, data: null}, active: false, peerMetadata: null} null
INFO WalletConnectCameraCard onDispose 2024-03-25 16:31:54.426029: null null
INFO WalletConnectService _onSessionProposal event 2024-03-25 16:31:54.870632: {id: 1711384230958729, expiry: 1711384614, relays: [{protocol: irn, data: null}], proposer: {publicKey: d7aa82030dac1713a993e9126983bd13d4476093233db5e04f93431e6551796c, metadata: {name: NoM Multichain, description: Bridge tokens, add and stake liquidity, url: bridge.staging.zenon.community, icons: [https://bridge.staging.zenon.community/static/media/zenon-big.d3e07dfc52d3a619fa99.png]}}, requiredNamespaces: {zenon: {chains: [zenon:1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange]}}, optionalNamespaces: {}, pairingTopic: d5ad569f239fa5106a144b5adbd081dbe1c1a3734f4d0de4a4e8aa2ae73be1d8} null
dressChange])}, optionalNamespaces: {}, pairingTopic: d5ad569f239fa5106a144b5adbd081dbe1c1a3734f4d0de4a4e8aa2ae73be1d8, sessionProperties: null, generatedNamespaces: null)) null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:32:02.849739: Instance of 'StoreSyncEvent' null
d569f239fa5106a144b5adbd081dbe1c1a3734f4d0de4a4e8aa2ae73be1d8, expiry: 1713976322) null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:32:02.851544: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:32:02.908880: Instance of 'StoreSyncEvent' null
ata(topic: 06b64a01f08c7dd92a8fcff7bf9d1877e2377933294a5aba64e326d995d08c0d, pairingTopic: d5ad569f239fa5106a144b5adbd081dbe1c1a3734f4d0de4a4e8aa2ae73be1d8, relay: Instance of 'Relay', expiry: 1711989122, acknowledged: false, controller: c00033da9b0c8c3bb424ddab93ed5da89019bb9ef7a61b4c7aacadf5c812bd30, namespaces: {zenon: Namespace(accounts: [zenon:1:Address 2, zenon:1:Address 1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange])}, requiredNamespaces: {zenon: RequiredNamespace(chains: [zenon:1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange])}, optionalNamespaces: {}, sessionProperties: null, self: ConnectionMetadata(publicKey: c00033da9b0c8c3bb424ddab93ed5da89019bb9ef7a61b4c7aacadf5c812bd30, metadata: PairingMetadata(name: s y r i u s, description: A wallet for interacting with Zenon Network, url: https://zenon.network, icons: [https://raw.githubusercontent.com/zenon-network/syrius/master/macos/Runner/Assets.xcassets/AppIcon.appiconset/Icon-MacOS-512x512%402x.png], redirect: null)), peer: ConnectionMetadata(publicKey: d7aa82030dac1713a993e9126983bd13d4476093233db5e04f93431e6551796c, metadata: PairingMetadata(name: NoM Multichain, description: Bridge tokens, add and stake liquidity, url: bridge.staging.zenon.community, icons: [https://bridge.staging.zenon.community/static/media/zenon-big.d3e07dfc52d3a619fa99.png], redirect: null)))) null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:32:02.910418: Instance of 'StoreSyncEvent' null
INFO WalletConnectCameraCard onScannerStarted 2024-03-25 16:33:15.391192: null null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:33:40.782395: Instance of 'StoreSyncEvent' null
INFO WalletConnectCameraCard pairing info 2024-03-25 16:33:40.841198: {topic: 1fab911f459502c4309b313b82ca24b5eeaebead1414f2fb7f880702da3cebb0, expiry: 1711384720, relay: {protocol: irn, data: null}, active: false, peerMetadata: null} null
INFO WalletConnectCameraCard onDispose 2024-03-25 16:33:41.106670: null null
INFO WalletConnectService _onSessionProposal event 2024-03-25 16:33:41.524211: {id: 1711384391144107, expiry: 1711384721, relays: [{protocol: irn, data: null}], proposer: {publicKey: fd7b7b4d5c7a4bff58b38362d7ed69c4495b127a81245b021a20837b2f72ce23, metadata: {name: NoM Multichain, description: Bridge tokens, add and stake liquidity, url: bridge.staging.zenon.community, icons: [https://bridge.staging.zenon.community/static/media/zenon-big.d3e07dfc52d3a619fa99.png]}}, requiredNamespaces: {zenon: {chains: [zenon:1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange]}}, optionalNamespaces: {}, pairingTopic: 1fab911f459502c4309b313b82ca24b5eeaebead1414f2fb7f880702da3cebb0} null
dressChange])}, optionalNamespaces: {}, pairingTopic: 1fab911f459502c4309b313b82ca24b5eeaebead1414f2fb7f880702da3cebb0, sessionProperties: null, generatedNamespaces: null)) null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:33:46.502576: Instance of 'StoreSyncEvent' null
b911f459502c4309b313b82ca24b5eeaebead1414f2fb7f880702da3cebb0, expiry: 1713976426) null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:33:46.508973: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionConnect triggered 2024-03-25 16:33:46.566577: SessionConnect(session: SessionData(topic: 179aba0f6efccb845c8df5881fe31a0cb77a1623062c1cec61a1133710381d8e, pairingTopic: 1fab911f459502c4309b313b82ca24b5eeaebead1414f2fb7f880702da3cebb0, relay: Instance of 'Relay', expiry: 1711989226, acknowledged: false, controller: 3b0319d67a26ccc2aa1476b9a2440bd7f7edff14b3b44b31381aed99f16e2a75, namespaces: {zenon: Namespace(accounts: [zenon:1:Address 2, zenon:1:Address 1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange])}, requiredNamespaces: {zenon: RequiredNamespace(chains: [zenon:1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange])}, optionalNamespaces: {}, sessionProperties: null, self: ConnectionMetadata(publicKey: 3b0319d67a26ccc2aa1476b9a2440bd7f7edff14b3b44b31381aed99f16e2a75, metadata: PairingMetadata(name: s y r i u s, description: A wallet for interacting with Zenon Network, url: https://zenon.network, icons: [https://raw.githubusercontent.com/zenon-network/syrius/master/macos/Runner/Assets.xcassets/AppIcon.appiconset/Icon-MacOS-512x512%402x.png], redirect: null)), peer: ConnectionMetadata(publicKey: fd7b7b4d5c7a4bff58b38362d7ed69c4495b127a81245b021a20837b2f72ce23, metadata: PairingMetadata(name: NoM Multichain, description: Bridge tokens, add and stake liquidity, url: bridge.staging.zenon.community, icons: [https://bridge.staging.zenon.community/static/media/zenon-big.d3e07dfc52d3a619fa99.png], redirect: null)))) null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:33:46.568277: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:33:46.866388: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionRequest triggered 2024-03-25 16:33:59.669299: SessionRequestEvent(id: 1711384437100901, topic: 179aba0f6efccb845c8df5881fe31a0cb77a1623062c1cec61a1133710381d8e, method: znn_info, chainId: zenon:1, params: null) null
WARNING NotificationUtils sendNotificationError 2024-03-25 16:35:12.210630: WalletConnectError(code: 5000, message: User rejected., data: null) null
INFO WalletConnectService _onSessionRequest triggered 2024-03-25 16:35:12.404965: SessionRequestEvent(id: 1711384508294151, topic: 179aba0f6efccb845c8df5881fe31a0cb77a1623062c1cec61a1133710381d8e, method: znn_send, chainId: zenon:1, params: {fromAddress: z1qrapzmtcvl32wt4wmp59sz0hhanz58s9rxvwgk, accountBlock: {version: 1, chainIdentifier: 1, blockType: 2, hash: 0000000000000000000000000000000000000000000000000000000000000000, previousHash: 0000000000000000000000000000000000000000000000000000000000000000, height: 0, momentumAcknowledged: {hash: 0000000000000000000000000000000000000000000000000000000000000000, height: 0}, address: z1qqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqsggv2f, toAddress: z1qxemdeddedxdrydgexxxxxxxxxxxxxxxmqgr0d, amount: 100000000, tokenStandard: zts1znnxxxxxxxxxxxxx9z4ulx, fromBlockHash: 0000000000000000000000000000000000000000000000000000000000000000, data: YdIkvAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAqMHhjYmVkZDQwZTI3MzVkZTMwNDQwMGIwMjQ2NjhlOWNjOTExYzk4MzkyAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA==, fusedPlasma: 0, difficulty: 0, nonce: , publicKey: , signature: }}) null
INFO WalletConnectService _onPairingDelete triggered 2024-03-25 16:35:52.915525: PairingEvent(id: null, topic: d5ad569f239fa5106a144b5adbd081dbe1c1a3734f4d0de4a4e8aa2ae73be1d8, error: null) null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:35:53.067182: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionDelete triggered 2024-03-25 16:35:53.069925: SessionDelete(topic: 06b64a01f08c7dd92a8fcff7bf9d1877e2377933294a5aba64e326d995d08c0d, id: null) null
WARNING NotificationUtils sendNotificationError 2024-03-25 16:36:08.047323: WalletConnectError(code: 5000, message: User rejected., data: null) null
INFO WalletConnectService _onSessionRequest triggered 2024-03-25 16:36:08.242690: SessionRequestEvent(id: 1711384567822207, topic: 179aba0f6efccb845c8df5881fe31a0cb77a1623062c1cec61a1133710381d8e, method: znn_send, chainId: zenon:1, params: {fromAddress: z1qrapzmtcvl32wt4wmp59sz0hhanz58s9rxvwgk, accountBlock: {version: 1, chainIdentifier: 1, blockType: 2, hash: 0000000000000000000000000000000000000000000000000000000000000000, previousHash: 0000000000000000000000000000000000000000000000000000000000000000, height: 0, momentumAcknowledged: {hash: 0000000000000000000000000000000000000000000000000000000000000000, height: 0}, address: z1qqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqsggv2f, toAddress: z1qxemdeddedxdrydgexxxxxxxxxxxxxxxmqgr0d, amount: 100000000, tokenStandard: zts1znnxxxxxxxxxxxxx9z4ulx, fromBlockHash: 0000000000000000000000000000000000000000000000000000000000000000, data: YdIkvAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAqMHhjYmVkZDQwZTI3MzVkZTMwNDQwMGIwMjQ2NjhlOWNjOTExYzk4MzkyAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA==, fusedPlasma: 0, difficulty: 0, nonce: , publicKey: , signature: }}) null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:36:43.552293: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionDelete triggered 2024-03-25 16:36:43.556022: SessionDelete(topic: 179aba0f6efccb845c8df5881fe31a0cb77a1623062c1cec61a1133710381d8e, id: null) null
INFO WalletConnectCameraCard onScannerStarted 2024-03-25 16:37:03.290211: null null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:37:11.106189: Instance of 'StoreSyncEvent' null
INFO WalletConnectCameraCard pairing info 2024-03-25 16:37:11.165897: {topic: cd78db1a44efeafeb7c2b4e4269aac549e0f9f606cf47e1937d13423971f0453, expiry: 1711384931, relay: {protocol: irn, data: null}, active: false, peerMetadata: null} null
INFO WalletConnectCameraCard onDispose 2024-03-25 16:37:11.440845: null null
INFO WalletConnectService _onSessionProposal event 2024-03-25 16:37:11.823435: {id: 1711384613166648, expiry: 1711384931, relays: [{protocol: irn, data: null}], proposer: {publicKey: 9ec64875948f050fae4f25ac43e45f087982f1025ea049292646da7651d84959, metadata: {name: NoM Multichain, description: Bridge tokens, add and stake liquidity, url: bridge.staging.zenon.community, icons: [https://bridge.staging.zenon.community/static/media/zenon-big.d3e07dfc52d3a619fa99.png]}}, requiredNamespaces: {zenon: {chains: [zenon:1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange]}}, optionalNamespaces: {}, pairingTopic: cd78db1a44efeafeb7c2b4e4269aac549e0f9f606cf47e1937d13423971f0453} null
dressChange])}, optionalNamespaces: {}, pairingTopic: cd78db1a44efeafeb7c2b4e4269aac549e0f9f606cf47e1937d13423971f0453, sessionProperties: null, generatedNamespaces: null)) null
INFO WalletConnectService _onPairingActivate triggered 2024-03-25 16:37:19.794278: PairingActivateEvent(topic: cd78db1a44efeafeb7c2b4e4269aac549e0f9f606cf47e1937d13423971f0453, expiry: 1713976639) null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:37:19.797950: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:37:19.852623: Instance of 'StoreSyncEvent' null
ata(topic: f1209447b6891bbf664564b05269df893760b95c9a5ad3f7cd038c0a94ba69fe, pairingTopic: cd78db1a44efeafeb7c2b4e4269aac549e0f9f606cf47e1937d13423971f0453, relay: Instance of 'Relay', expiry: 1711989439, acknowledged: false, controller: 6d7e420d6cbe06ef91da60c03745a0320d4c33584adcb449d4efebdcd088b774, namespaces: {zenon: Namespace(accounts: [zenon:1:Address 2, zenon:1:Address 1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange])}, requiredNamespaces: {zenon: RequiredNamespace(chains: [zenon:1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange])}, optionalNamespaces: {}, sessionProperties: null, self: ConnectionMetadata(publicKey: 6d7e420d6cbe06ef91da60c03745a0320d4c33584adcb449d4efebdcd088b774, metadata: PairingMetadata(name: s y r i u s, description: A wallet for interacting with Zenon Network, url: https://zenon.network, icons: [https://raw.githubusercontent.com/zenon-network/syrius/master/macos/Runner/Assets.xcassets/AppIcon.appiconset/Icon-MacOS-512x512%402x.png], redirect: null)), peer: ConnectionMetadata(publicKey: 9ec64875948f050fae4f25ac43e45f087982f1025ea049292646da7651d84959, metadata: PairingMetadata(name: NoM Multichain, description: Bridge tokens, add and stake liquidity, url: bridge.staging.zenon.community, icons: [https://bridge.staging.zenon.community/static/media/zenon-big.d3e07dfc52d3a619fa99.png], redirect: null)))) null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:37:19.856031: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:37:20.161007: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionRequest triggered 2024-03-25 16:37:30.027632: SessionRequestEvent(id: 1711384650402422, topic: f1209447b6891bbf664564b05269df893760b95c9a5ad3f7cd038c0a94ba69fe, method: znn_info, chainId: zenon:1, params: null) null
INFO WalletConnectService _onRelayClientDisconnect triggered 2024-03-25 16:37:36.929858: null null
INFO WalletConnectService _onRelayClientConnect triggered 2024-03-25 16:37:37.133912: null null
```


```
INFO WalletConnectCameraCard onScannerStarted 2024-03-25 16:39:25.388604: null null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:39:50.810715: Instance of 'StoreSyncEvent' null
INFO WalletConnectCameraCard pairing info 2024-03-25 16:39:50.873538: {topic: a9a0b79f35c652e0e90f1b3114ceaec67625b07594e96a08b7404f0d1d7b596b, expiry: 1711385090, relay: {protocol: irn, data: null}, active: false, peerMetadata: null} null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:39:51.093768: Instance of 'StoreSyncEvent' null
INFO WalletConnectCameraCard onDispose 2024-03-25 16:39:51.133583: null null
INFO WalletConnectService _onSessionProposal event 2024-03-25 16:39:51.540844: {id: 1711384779035263, expiry: 1711385091, relays: [{protocol: irn, data: null}], proposer: {publicKey: e403d75a3b3efb83db0be20d269e1a84853c9595d734181e87104046c228d327, metadata: {name: NoM Multichain, description: Bridge tokens, add and stake liquidity, url: bridge.staging.zenon.community, icons: [https://bridge.staging.zenon.community/static/media/zenon-big.d3e07dfc52d3a619fa99.png]}}, requiredNamespaces: {zenon: {chains: [zenon:1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange]}}, optionalNamespaces: {}, pairingTopic: a9a0b79f35c652e0e90f1b3114ceaec67625b07594e96a08b7404f0d1d7b596b} null
dressChange])}, optionalNamespaces: {}, pairingTopic: a9a0b79f35c652e0e90f1b3114ceaec67625b07594e96a08b7404f0d1d7b596b, sessionProperties: null, generatedNamespaces: null)) null
INFO WalletConnectService _onPairingActivate triggered 2024-03-25 16:39:58.068435: PairingActivateEvent(topic: a9a0b79f35c652e0e90f1b3114ceaec67625b07594e96a08b7404f0d1d7b596b, expiry: 1713976798) null
INFO WalletConnectService _onPairingsSync triggered 2024-03-25 16:39:58.071954: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:39:58.140543: Instance of 'StoreSyncEvent' null
ata(topic: 5a9b9e25c53214735f939642f4923518d8b6e27d8755af751ce4984a67ab3e2d, pairingTopic: a9a0b79f35c652e0e90f1b3114ceaec67625b07594e96a08b7404f0d1d7b596b, relay: Instance of 'Relay', expiry: 1711989597, acknowledged: false, controller: 2cc1a11153295690ac8cc21944756075261b4308ac88497cfda081730c5d8c7b, namespaces: {zenon: Namespace(accounts: [zenon:1:Address 1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange])}, requiredNamespaces: {zenon: RequiredNamespace(chains: [zenon:1], methods: [znn_sign, znn_info, znn_send], events: [chainIdChange, addressChange])}, optionalNamespaces: {}, sessionProperties: null, self: ConnectionMetadata(publicKey: 2cc1a11153295690ac8cc21944756075261b4308ac88497cfda081730c5d8c7b, metadata: PairingMetadata(name: s y r i u s, description: A wallet for interacting with Zenon Network, url: https://zenon.network, icons: [https://raw.githubusercontent.com/zenon-network/syrius/master/macos/Runner/Assets.xcassets/AppIcon.appiconset/Icon-MacOS-512x512%402x.png], redirect: null)), peer: ConnectionMetadata(publicKey: e403d75a3b3efb83db0be20d269e1a84853c9595d734181e87104046c228d327, metadata: PairingMetadata(name: NoM Multichain, description: Bridge tokens, add and stake liquidity, url: bridge.staging.zenon.community, icons: [https://bridge.staging.zenon.community/static/media/zenon-big.d3e07dfc52d3a619fa99.png], redirect: null)))) null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:39:58.141613: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionsSync triggered 2024-03-25 16:39:58.435993: Instance of 'StoreSyncEvent' null
INFO WalletConnectService _onSessionRequest triggered 2024-03-25 16:40:08.460151: SessionRequestEvent(id: 1711384808685260, topic: 5a9b9e25c53214735f939642f4923518d8b6e27d8755af751ce4984a67ab3e2d, method: znn_info, chainId: zenon:1, params: null) null
```

-------------------------

coinselor | 2024-03-26 18:42:38 UTC | #7

[quote="CryptoFish, post:4, topic:425"]
Please test this [build ](https://github.com/zenon-network/syrius/actions/runs/8425666991#artifacts) by downloading the binaries from the artifacts.
[/quote]

New build works as expected.

-------------------------

CryptoFish | 2024-03-26 22:09:11 UTC | #8

These issues have been resolved in the following PRs:

- https://github.com/zenon-network/syrius/pull/107
- https://github.com/zenon-network/syrius/pull/109

A new release candidate will be made available.

-------------------------

0x3639 | 2024-03-26 22:22:32 UTC | #9



-------------------------

