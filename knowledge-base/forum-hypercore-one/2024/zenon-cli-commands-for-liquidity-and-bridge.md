Thread: zenon-cli-commands-for-liquidity-and-bridge
CryptoFish | 2023-06-14 06:09:12 UTC | #1

I would like to propose a list of possible cli commands for interacting with the liquidity and bridge api and contract methods. Some of these commands probably don't have to be implemented, because they represent internal contract methods. I've included them all to make the list as complete as possbile. The command names follow a namespace principle to keep the actual commands short and similar to each other like `get`, `info`, `list`, `set`, `listBy` etc and to avoid command names like `getAllWrapTokenRequestsByToAddressNetworkClassAndChainId`.

I'm not aware if any other devs are currently working on the cli, but it might be helpful to discuss and share a common command interface before implementing one to avoid creating different interfaces.

Liquidity commands

`liquidity.info` Get the liquidity information
`liquidity.security` Get the liquidity security information
`liquidity.timeChallenges` List all liquidity time challenges
`liquidity.emercency` Put the liquidity contract in emercency mode. Can only be called by the administrator.
`liquidity.halt` Halt liquidity operations. Can only be called by the administrator.
`liquidity.unhalt` Unhalt liquidity operations. Can only be called by the administrator.
`liquidity.burn`
`liquidity.fund`
`liquidity.donate`
`liquidity.update` Update the liquidity contract.

`liquidity.stake` Stake liquidity
`liquidity.stake.list` List all stakes by address
`liquidity.stake.cancel` Cancel staked liquidity
`liquidity.stake.unlock` Unlock liquidity staking for a zts that is no longer allowed.

`liquidity.reward.list` List all liquidity reward history by address
`liquidity.reward.get` Get uncollected reward by address
`liquidity.reward.collect`  Collect liquidity rewards
`liquidity.reward.setAdditional` Set additional liquidity rewards. Can only be called by the administrator
`liquidity.reward.setToken` Set token and corresponding reward percentages. Can only be set by the administrator.

`liquidity.admin.nominate` Nominate liquidity guardians. Can only be called by the administrator.
`liquidity.admin.propose` Propose liquidity administrator. Can only be called by a guardian if the liquidity contract is in emergency mode.
`liquidity.admin.change` Change liquidity administrator. Can only be called by the administrator.

Bridge commands

`bridge.info`                    Get the bridge information
`bridge.security`           Get the bridge security information
`bridge.timeChallenges`     List all bridge time challenges
`bridge.emercency`               Put the bridge contract in emercency mode. Can only be called by the administrator.
`bridge.halt`                    Halt bridge operations.
`bridge.unhalt` Unhalt bridge operations. Can only be called by the administrator.
`bridge.enableKeyGen` Enable bridge key generation. Can only be called by the administrator.
`bridge.disableKeyGen` Disable bridge key generation. Can only be called by the administrator.
`bridge.setMetadata` Set the bridge metadata. Can only be called by the administrator.
`bridge.setRedeemDelay` Set the bridge redeem delay in momentums Can only be called by the administrator..
`bridge.changePubKey` Change bridge TSS ECDSA public key. Can only be called by the administrator.

`bridge.wrap.list`               List all wrap token requests
`bridge.wrap.listByAddress`      List all wrap token requests by address
`bridge.wrap.listUnsigned`       List all unsigned wrap token requests
`bridge.wrap.get`                Get wrap token request by id
`bridge.wrap.update`             Update wrap token request
`bridge.wrap.token`              Wrap assets.

`bridge.unwrap.list`             List all unwrap token requests
`bridge.unwrap.listByAddress`    List all unwrap token requests by address
`bridge.unwrap.get`              Get unwrap token request by hash and log index
`bridge.unwrap.token`            Unwrap assets.
`bridge.unwrap.revoke`           Revoke unwrap request.

`bridge.orchestrator.info`       Get the orchestrator information
`bridge.orchestrator.set`        Set the orchestrator information

`bridge.network.list`            List all available bridge netwoks
`bridge.network.get`             Get the current bridge network information
`bridge.network.set`             Add or edit an existing bridge network
`bridge.network.remove`          Remove an existing bridge network
`bridge.network.setMetadata`     Set the metadata for a bridge network

`bridge.admin.nominate`          Nominate bridge guardians. Can only be called by administrator.
`bridge.admin.propose`           Propose bridge administrator. Can only be called by a guardian if the bridge contract is in emergency mode.
`bridge.admin.change`            Change bridge administrator. Can only be called by administrator.

-------------------------

sol | 2023-05-10 17:03:26 UTC | #2

Thank you for being the first to take on this work. I've used your code as reference material for the Dart SDK and I'm in the process of testing these functions.

I'm considering adding these to the Dart znn-cli as well, though I might have to refactor that code first. Its current design doesn't scale well when we introduce so many new changes.

It would be helpful to write C# and/or Dart applications like the [z_bridge_test.go](https://github.com/HyperCore-Team/go-zenon/blob/embedded-bridge/vm/embedded/tests/z_bridge_test.go) and z_bridge_liquidity.go files that step through the process of activating/using the new functionality.
I'm not sure if you plan to do this. I might do that after I finish the znn-cli work.

-------------------------

CryptoFish | 2023-05-10 19:02:43 UTC | #3

I think the SDK is complete. I have not yet had the opportunity to fully test all methods on-chain. If the documentation is correct, everything should be fine.

As for the CLI implementation. That is mainly a one-to-one impl. of the methods. I wanted to understand the bridge better before adding business logic to it.

The methods with a time challenge can in any case be checked. I will adjust the nominate command to check for active time challenges.

The suggested command names above have not yet been fully implemented in the CLI code, but it is my intention to use the suggested names. Feel free to suggest any changes if you don't like some of them.

-------------------------

