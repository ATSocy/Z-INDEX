Thread: zenon-public-rpc-node-database-repo
0x3639 | 2024-02-28 17:46:54 UTC | #1

As a follow up to this post: https://forum.hypercore.one/t/public-rpc-nodes-in-syrius-v0-2-0/385/3?u=0x3639

I'm discussing this idea with @CryptoFish.  We have come up with an idea to create a file called `mainnet-rpc-node-db.json` that would live in a new `/zenon-network` repo.  See the proposed repo here:  https://github.com/KingGorrin/zenon-node-database.

In this `.json` file we could include a list of Public RPC Nodes like this:

```
{
  "HyperCore-One": {
    "url": "wss://my.hc1node.com:35998"
  },
  "Zenon Hub": {
    "url": "wss://node.zenonhub.io:35998"
  }
}
```
When we build `syrius` and other applications, they can pull in this file and use it when we build the binary.  Putting this information in a separate repo and easily accessible file will make it "ez" for the community to see it and propose changes.  

In addition, we can also expand this idea to include more information, like what is proposed below: 

```
"name":"Zenon Mainnet",
"chain":"ZNN",
"icon":"zenon",
"infoURL":"https://zenon.network",
"shortName":"znn",
"chainId":1,
"networkId":1,
"rpc":[
	"wss://my.hc1node.com:35998",
	"wss://node.zenonhub.io:35998"
],
"faucets":[],
"nativeCurrency":{"name":"Zenon","symbol":"ZNN","decimals":18},
"explorers":[{"name":"Zenon Explorer","url":"https://explorer.zenon.org"}]

```

The alternative is to hard code the Public RPC Nodes into the code or create a `.json` for each application, but that could be hard to manage and duplicate information needed in multiple apps.  

Do you guys have any opinions on this idea?  If not, we will move forward as proposed.

-------------------------

CryptoFish | 2024-03-01 07:44:55 UTC | #2

I think it's better to the json file as basic as possible. Just a list of strings representing the rpc urls.

This [PR](https://github.com/zenon-network/syrius/pull/69) contains a working example in which the node file is copied by the workflow and loaded as an asset by syrius.

Currently using [HyperCore-One:zenon-node-database](https://github.com/hypercore-one/zenon-node-database) as the central repository because of permission limitations on zenon-network.

-------------------------

0x3639 | 2024-02-29 18:18:26 UTC | #3

[quote="CryptoFish, post:2, topic:386"]
I think it’s better to the json file as basic as possible. Just a list of strings representing the rpc urls.
[/quote]

this makes sense to me too.

[quote="CryptoFish, post:2, topic:386"]
This [PR ](https://github.com/zenon-network/syrius/pull/69) contains a working example in which the node file is copied by the workflow and loaded as an asset by syrius.
[/quote]

By doing this users can modify this file locally themselves after installing `syrius`.

-------------------------

