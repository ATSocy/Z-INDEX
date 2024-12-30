Thread: kb-pow-and-plasma
CryptoFish | 2024-03-27 15:20:02 UTC | #1

The following explanation is an attempt to give some insight in the current implementation of PoW and Plasma.

## Transaction

When preparing a transaction, a call is made to the `getRequiredPoWForAccountBlock` JSON-RPC method.

The method accepts one argument containing the transaction `Address`, `BlockType`, `ToAddress` and `Data` and returns the `AvailablePlasma`, `BasePlasma` and `RequiredDifficulty`.

The following example shows a JSON-RPC request and response for calling the `Pillar.CollectReward` embedded method.

**Request**
``` json
{
  "jsonrpc": "2.0",
  "id": 5,
  "method": "embedded.plasma.getRequiredPoWForAccountBlock",
  "params": [
    {
      "address": "z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7",
      "blockType": 2,
      "toAddress": "z1qxemdeddedxpyllarxxxxxxxxxxxxxxxsy3fmg",
      "data": "r0PT8A=="
    }
  ]
}
```

**Response**


``` json
{
  "jsonrpc": "2.0",
  "id": 5,
  "result": {
    "availablePlasma": 0,
    "basePlasma": 52500,
    "requiredDifficulty": 78750000
  }
}
```

PoW is calculated using a SHA3-256 hash (made by combining the bytes of the `Address` and `FrontierHashBlock`) and the `RequiredDifficulty`. The PoW is only undertaken when `RequiredDifficulty` is not `0`; otherwise a nonce of `0000000000000000` is used.

When the nonce is set, the transaction is hashed, signed and published to the network.

## PoW Calculation

The `getRequiredPoWForAccountBlock` JSON-RPC method does three things:

1. Calculate available plasma
2. Calculate base plasma
3. Calculate difficulty

### Calculate available plasma

The available plasma is calculated by using the total amount of plasma available minus used plasma by unconfirmed blocks. Plasma equals to `fusedPlasma - plasmaUsedByUnconfirmedBlocks`.

### Calculate base plasma

The base plasma is calculated depending on four different scenarios.

1. The base plasma is `0` when send from an embedded address.
2. The base plasma is `AccountBlockBasePlasma` when receiving a transaction.
3. The base plasma is `(blockDataByteLength * ABByteDataPlasma) + AccountBlockBasePlasma` when sending to a non embedded address.
4. The base plasma is calculated according to the [PlasmaTable](#PlasmaTable) when interacting with an embedded contract method.

### Calculate difficulty

The required difficulty is `0` when the available plasma is bigger than the base plasma; otherwise the remaining required plasma is used to caluclate the difficulty by multiplying it by PoWDifficultyPerPlasma `(basePlasma - availablePlasma) * PoWDifficultyPerPlasma`. The result can never be bigger than `MaxPoWPlasmaForAccountBlock`.


## PlasmaTable

The following plasma table shows the required plasma for each embedded contract method.

The values presented below are based on the AcceleratorSpork.

| EmbeddedContract | Method | Plasma |
|--|--|--|
| Accellerator | CreateProject | EmbeddedSimple |
| Accellerator | AddPhase | EmbeddedSimple |
| Accellerator | UpdateEmbeddedAccelerator | EmbeddedWWithdraw |
| Accellerator | UpdatePhase | EmbeddedSimple |
| Common | CollectReward [1] | EmbeddedSimple  |
| Common | DepositQsr | EmbeddedSimple |
| Common | WithdrawQsr | EmbeddedSimple |
| Common | Donate | EmbeddedSimple |
| Common | VoteByName | EmbeddedSimple |
| Common | VoteByProdAddress | EmbeddedSimple |
| Liquidity | UpdateEmbeddedLiquidity | EmbeddedSimple |
| Liquidity | Fund | EmbeddedSimple |
| Liquidity | BurnZnn | EmbeddedSimple |
| Pillars | Register [2] | 2 * EmbeddedSimple |
| Pillars | LegacyRegister [2] | 2 * EmbeddedSimple |
| Pillars | Revoke | EmbeddedWWithdraw |
| Pillars | UpdatePillar | EmbeddedSimple |
| Pillars | Delegate | EmbeddedSimple |
| Pillars | Undelegate | EmbeddedSimple |
| Pillars | UpdateEmbeddedPillar | EmbeddedSimple |
| Plasma | Fuse | EmbeddedSimple |
| Plasma | CancelFuse | EmbeddedWWithdraw |
| Sentinel | RegisterSentinel | EmbeddedSimple |
| Sentinel | RevokeSentinel | EmbeddedWDoubleWithdraw |
| Sentinel | UpdateEmbeddedSentinel | EmbeddedSimple |
| Spork | CreateSpork | EmbeddedSimple |
| Spork | ActivateSpork | EmbeddedSimple |
| Stake | Stake | EmbeddedSimple |
| Stake | CancelStake | EmbeddedWWithdraw |
| Stake | UpdateEmbeddedState | EmbeddedSimple |
| Swap | SwapRetrieveAssets | EmbeddedWDoubleWithdraw |
| Token | Issue | EmbeddedWWithdraw |
| Token | Mint | EmbeddedWWithdraw |
| Token | Burn | EmbeddedSimple |
| Token | UpdateToken | EmbeddedSimple |

1. CollectReward for Pillar, Sentinel and Stake
2. Include burn tx

## Constants

``` dart
AccountBlockBasePlasma = 21000
ABByteDataPlasma       = 68

EmbeddedSimplePlasma    = 2.5 * AccountBlockBasePlasma
EmbeddedWResponse       = 3.5 * AccountBlockBasePlasma
EmbeddedWDoubleResponse = 4.5 * AccountBlockBasePlasma

NumFusionUnitsForBasePlasma = 10
PlasmaPerFusionUnit         = AccountBlockBasePlasma / NumFusionUnitsForBasePlasma
CostPerFusionUnit           = 100000000

PoWDifficultyPerPlasma = 1500

// MaxDataLength defines limit of account-block data to 16Kb
MaxDataLength = 1024 * 16

// MaxPlasmaForAccountBlock defines max available plasma for an account block.
MaxPlasmaForAccountBlock = MaxFusionPlasmaForAccount

MaxPoWPlasmaForAccountBlock  = EmbeddedWDoubleResponse
MaxDifficultyForAccountBlock = MaxPoWPlasmaForAccountBlock * PoWDifficultyPerPlasma

// MaxFusionUnitsPerAccount limits each account to a maximum of 5000 fusion units.
// All units above this will not increase the maximum plasma.
MaxFusionUnitsPerAccount  = 5000
MaxFusionPlasmaForAccount = MaxFusionUnitsPerAccount * PlasmaPerFusionUnit
MaxFussedAmountForAccount = CostPerFusionUnit * MaxFusionUnitsPerAccount
```

-------------------------

TrevorLeahy3 | 2023-03-03 23:39:57 UTC | #2

Thank you for posting this, it helps.

-------------------------

romeo | 2023-03-04 11:23:29 UTC | #3

this is great, can't express how much posts like these are helpful to all in understanding the NoM

-------------------------

romeo | 2023-03-04 11:27:36 UTC | #4

@CryptoFish and if the available plasma is below the base plasma Syrius performs the PoW calcs itself?

Does the code specify in which specific instances insufficient plasma won't result in PoW thus resulting in the tx not confirming?

-------------------------

0x3639 | 2023-03-04 14:57:09 UTC | #5

@CryptoFish are you thinking about dynamic plasma?  This is a very helpful guide.  Thx for posting.

-------------------------

CryptoFish | 2023-03-04 17:28:26 UTC | #6

[quote="romeo, post:4, topic:1325"]
@CryptoFish and if the available plasma is below the base plasma Syrius performs the PoW calcs itself?
[/quote]
When this happens the remaining required plasma is calculated to a PoW difficulty.

[quote="romeo, post:4, topic:1325"]
Does the code specify in which specific instances insufficient plasma won’t result in PoW thus resulting in the tx not confirming?
[/quote]
Insufficient plasma always results in PoW difficulty that will be calculated.

-------------------------

CryptoFish | 2023-03-04 17:30:10 UTC | #7

[quote="0x3639, post:5, topic:1325, full:true"]
@CryptoFish are you thinking about dynamic plasma? This is a very helpful guide. Thx for posting.
[/quote]
I started this post reading your dynamic plasma post. I figured we first need to understand the current implementation, before we can think about changing it.

-------------------------

romeo | 2023-03-04 20:18:31 UTC | #8

[quote="CryptoFish, post:6, topic:1325"]
Insufficient plasma always results in PoW difficulty that will be calculated.
[/quote]

But does a PoW difficulty being calculated always result in PoW being undertaken? I thought there were instances where only fused Plasma would suffice - can't recall which though

-------------------------

CryptoFish | 2023-03-04 23:25:46 UTC | #9

The `getRequiredPoWForAccountBlock` method is straightforward. PoW is undertaken when returned `difficulty` is not `0`. The 3 calculations and  conditions of the method are explained above.

Thus insufficient (fused) plasma, means `availablePlasma < basePlasma`, which in turn means difficulty will be `(basePlasma - availablePlasma) * PoWDifficultyPerPlasma` . The result can never be bigger than `MaxPoWPlasmaForAccountBlock` .

It all boils down to what determines the `basePlasma`. The current impl. uses a couple of simple conditions as explained in Calculate base plasma.

I still have to look deeper into what the `basePlasma` is of the `Common.CollectReward` embedded method.

-------------------------

CryptoFish | 2023-03-05 11:21:52 UTC | #10

[quote="CryptoFish, post:9, topic:1325"]
I still have to look deeper into what the `basePlasma` is of the `Common.CollectReward` embedded method.
[/quote]

The base plasma for the CollectReward method for Pillar, Sentinel and Stake are all EmbeddedSimple. This actually changed since the AcceleratorSpork from `EmbeddedSimple + EmbeddedWWithdraw` to `EmbeddedSimple`.

-------------------------

sol | 2023-03-05 20:58:30 UTC | #11

Thanks for the summary, CryptoFish

Here's [the other thread](https://forum2.zenon.org/t/dynamic-plasma/1211) about dynamic plasma, in case some people aren't aware.

-------------------------

