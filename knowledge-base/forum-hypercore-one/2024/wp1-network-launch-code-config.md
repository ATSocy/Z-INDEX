Thread: wp1-network-launch-code-config
georgezgeorgez | 2024-10-28 15:17:46 UTC | #1

Coordination thread for the code/config

-------------------------

georgezgeorgez | 2024-11-08 00:55:46 UTC | #2

Acceptance criteria:

Repo with a fork of go-zenon and the following changes:
* UTIL-Z and UTIL-Q tokens replacing ZNN and QSR
* Tune network constants for appropriate throughput
  * Exact parameters TBD
* Change pillar election from weight based to be round robin
  * Since we are incentivizing momentum production as part of Work Packages, this ensures that pillars do not try and use UTIL-Z and UTIL-Q to try and get more momentums.

Genesis file
* pillars from sign up
* genesis sporks for AZ and HTLC
  * bridge spork will be activated when we work on connecting mainnet and L2

Round 1 incentives based on median pillar votes

Network Launch Code & Config
6000 / 8025 Points
1121 / 15000 ZNN
11215 / 150000 QSR

**Disclaimer** : The payment amounts provided herein are intended as guidelines only and do not constitute a binding offer or guarantee of payment. The HyperQube Incubator framework works with Zenon Network Pillars to signal incentives which are subject to change over multiple rounds. Actual payment amounts will be based on Accelerator-Z grants that depend on the voting rules and requirement of Accelerator-Z.


We may need to use Network Launch Bonus/Placeholder to incentive review

-------------------------

georgezgeorgez | 2024-11-08 00:57:24 UTC | #3

I will nominate myself for this work since I want to make sure this is done right.
If there are no objections, I will begin the work.

-------------------------

0x3639 | 2024-11-08 01:55:45 UTC | #4

no objection.  

[quote="georgezgeorgez, post:2, topic:536"]
bridge spork will be activated when we work on connecting mainnet and L2
[/quote]

To be clear, initially there will be no connection between the L1 and L2.  Just want to make sure everyone understands that.

-------------------------

georgezgeorgez | 2024-11-18 14:49:25 UTC | #5

Sorry for the late update. Been traveling full time last week and this week.
I think I can have the code done by EOM.
Can also have the genesis templated out waiting for pillar sign up work.

-------------------------

georgezgeorgez | 2024-11-30 00:15:25 UTC | #6

hyperqube_z node code is coming along. I have an extra goal to make the code backwards compatible with mainnet.
Binary will probably be called hqzd
Main features/differences from mainnet/znnd
1.  custom zToken and qToken, selected through first and second genesis tokens. Also a new rpc endpoint `ledger.meta` which dumps `chainId`, `zToken`, `qToken` to allow for wallets to easily configure themselves depending on the chain.
2. uniform random pillar election. this is to discourage the native tokens from having value since pillar momentums are incentivized. still deciding how to trigger switching the election algo, probably through genesis extradata field for now which is fairly flexible for future things too
3. configurable throughput, probably again through genesis extradata

Long term, in a future work package, I want to make many of these things defined in genesis directly, and changeable through governance

As a note, the go-zenon codebase uses some global/package level variables, e.g. `types.ZnnTokenStandard`. For hyperqube_z we'll probably want to get rid of that over time.

I should have another update this weekend. Operational support work will be able to start soon.

-------------------------

georgezgeorgez | 2024-12-01 03:56:53 UTC | #7

Will push some code tomorrow after updating the readme and doing some basic smoke tests.

I will also update nomctl generate-devnet command with a flag to generate a a hyperqube_z compatible genesis.json so that others can test locally. Will also update nomctl to take advantage of the `ledger.meta` endpoint.

When it comes to configurable throughput and lowering the hardware requirements for hyperqube_z, it would ostensibly be simple to just adjust the hardcoded plasma per momentum cap. However currently on mainnet, most momentums are empty and still some nodes struggle.

I've gone the more complicated route of adjusting BlockTime. I think we will go with 60 seconds, a momentum a minute, instead of mainnet's 10 seconds. I'm not sure what the overhead of networking is, but otherwise this should reduce the node load/requirements by a factor of 6.

It seems to be working as intended, but the relevant config is not straightforward, and it's hard to be sure with such an invasive change without further testing.

-------------------------

georgezgeorgez | 2024-12-01 04:04:07 UTC | #8

One thing I am considering adding is a section in config for whitelisted addresses.
When producing a momentum, pillars would first check the whitelisted addresses for transactions. Currently it is random.

This would ensure that even with low throughput, as long as pillar is producing, they will be able to get in their incubator votes.

-------------------------

georgezgeorgez | 2024-12-01 14:19:09 UTC | #9

https://github.com/hypercore-one/hyperqube_z/pull/1

-------------------------

vilkris | 2024-12-02 14:48:58 UTC | #10

Is there something we need to consider regarding pillar registration in the embedded contract? Are non-mainnet backed pillars allowed to be launched?

-------------------------

georgezgeorgez | 2024-12-02 14:54:37 UTC | #11

Ah! Good call out. I forgot I was supposed to disable that pillar registration method.

-------------------------

georgezgeorgez | 2024-12-02 21:29:18 UTC | #12

I will get the devnet code out first so that people can begin testing the current changes. Then I will fix the pillar registration.

-------------------------

georgezgeorgez | 2024-12-06 02:26:02 UTC | #13

Will push out some more code tomorrow and then we will have a test launch planned out over the weekend for next week.

-------------------------

georgezgeorgez | 2024-12-10 22:29:27 UTC | #14

Sorry for the delay. Pushed some more commits for https://github.com/hypercore-one/hyperqube_z/pull/1.
A few rabbit holes. Some concluded. Others tabled.

Some notes: moved the 	`applyHyperQubeConfig(config)` call before CheckGenesis to make sure tokens are changed before checks such as https://github.com/hypercore-one/hyperqube_z/blob/429e853ba038be1eddc5c0708cb26cff79610101/chain/genesis/shared_tests.go#L91 run.

Used a spork to trigger pillar registration deactivation.

Hyperqube_z will activate htlc spork at genesis but will not activate bridge spork until it is time to integrate hyperqube_z with mainnet. This required a change to the logic which determines available embedded methods.

The existing code is hardcoded for mainnet where htlc is activated after bridge is activated. Future refactors will likely be needed.

I will migrate go-zdk and nomctl into hypercore-one organization.
A few more tweaks to those repos and they will have some updates pushed as well.

-------------------------

georgezgeorgez | 2024-12-10 23:27:19 UTC | #15

go-zdk migrated and now supports `ledger.meta` endpoint with a utility to create a client connection from it

https://github.com/hypercore-one/go-zdk/commit/71c9daf1857b3ae764ecffb81105d96af16106bd

-------------------------

georgezgeorgez | 2024-12-10 23:37:52 UTC | #16

Oops forgot to stage all changes
https://github.com/hypercore-one/go-zdk/commit/3fe36eafc057b784d1728fb2fc8f4434beaf9fbf

-------------------------

georgezgeorgez | 2024-12-10 23:42:12 UTC | #17

At some point, it will probably make sense to add Spork dependency logic.  E.g, you can't activate spork B unless spork A is active. Also in the future, I am thinking of having on-chain feature flags and other dynamic configuration.

-------------------------

georgezgeorgez | 2024-12-11 00:18:42 UTC | #18

I am being a bit fast and loose with my changes to go-zdk and nomctl repos.
I figure it shouldn't impact anyone.

I'll make it easy to review all the changes.
And once hyperqube_z is launched, now that the repos are under hypercore-one org, will go through proper code review for all changes.

-------------------------

georgezgeorgez | 2024-12-12 02:21:25 UTC | #19

When big int was activated, i think several rpc unmarshalling bugs were introduced in go-zenon.
No one ever hits them because syrius uses the dart sdk with its own logic.

Let me see how far we can get without addressing them...

-------------------------

georgezgeorgez | 2024-12-12 02:35:48 UTC | #20

https://github.com/hypercore-one/hyperqube_z/blame/master/rpc/api/embedded/plasma.go#L149

This one is an easy fix. Will make an MR right now.

-------------------------

georgezgeorgez | 2024-12-12 02:52:37 UTC | #21

https://github.com/zenon-network/go-zenon/issues/48

-------------------------

georgezgeorgez | 2024-12-12 17:39:22 UTC | #22

This definitely needs future cleanup but it's good enough from a client perspective to get us going.

https://github.com/hypercore-one/nomctl/pull/46

-------------------------

georgezgeorgez | 2024-12-12 23:08:27 UTC | #23

LOCAL TESTING

1. Clone and build `nomctl`
2. Create local hyperqube_z devnet
```
git clone git@github.com:hypercore-one/nomctl.git
cd nomctl
git checkout hyperqube_z
make nomctl
./build/nomctl -hq generate-devnet -ez
```

3. Copy key into nomctl directory. On mac, the directory will be `~/Library/hqzd/wallet`. On linux, it should be `~/.hqzd/wallet`. The `nomctl` command looks for keys in the `~/.nomctl/wallet` directory.
```
# Adjust as needed
cp ~/.hqzd/wallet/<KEYFILE> ~/.nomctl/wallet/
```
4. In a new terminal session, clone hyperqube_z and run the node
```
git clone git@github.com:hypercore-one/hyperqube_z.git
cd hyperqube_z
git checkout hyperqube_z
make hqzd
./build/hqzd
```
5. You should have a running local cluster now. Go back to the `nomctl` terminal and run a few commands for testing. Make sure to always use the `-hq` flag. If you have used nomctl before with another network, you will need to use the `--keyStore`, `-k` flag to choose the right key. The default password for the devnet is `Don'tTrust.Verify`
```
./build/nomctl -hq znn-cli -p "Don'tTrust.Verify" balance
./build/nomctl -hq znn-cli -p "Don'tTrust.Verify" plasma.list
# this example shows that utilQ is correctly taking the role of QSR
# I should make address default to the key
./build/nomctl -hq znn-cli -p "Don'tTrust.Verify" plasma.fuse <ADDRESS> 1000
```

-------------------------

0x3639 | 2024-12-12 22:07:29 UTC | #24

[quote="georgezgeorgez, post:23, topic:536"]
`make nomctl`
[/quote]

getting this error

```
go build -o build/nomctl
# github.com/zenon-network/go-zenon/p2p/discover
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/p2p/discover/node.go:223:27: undefined: secp256k1.RecoverPubkey
# github.com/zenon-network/go-zenon/vm/embedded/implementation
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/bridge.go:47:30: undefined: secp256k1.RecoverPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/bridge.go:1155:20: undefined: secp256k1.DecompressPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:40:26: undefined: secp256k1.CompressPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:61:30: undefined: secp256k1.Sign
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:74:30: undefined: secp256k1.Sign
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:135:36: undefined: secp256k1.RecoverPubkey
make: *** [Makefile:4: nomctl] Error 1
```


![image|681x500](upload://ioso1MsiEhwVwTKVRlCrkRo8Drp.png)

-------------------------

georgezgeorgez | 2024-12-12 22:27:20 UTC | #25

what os are you using?
and what is your `go version`?

-------------------------

0x3639 | 2024-12-12 22:36:36 UTC | #26

`go version go1.23.4 linux/amd64`

Ubuntu 22.04.5 LTS - Desktop

-------------------------

georgezgeorgez | 2024-12-12 22:43:41 UTC | #27

Hmm it's a bit strange


https://github.com/hypercore-one/hyperqube_z/blob/429e853ba038be1eddc5c0708cb26cff79610101/vm/embedded/implementation/bridge.go#L47
https://github.com/hypercore-one/hyperqube_z/blob/429e853ba038be1eddc5c0708cb26cff79610101/vm/embedded/implementation/bridge.go#L15

https://github.com/hypercore-one/hyperqube_z/blob/714b2282baad9a837d0ed8518c634225b7f0ad16/go.mod#L8


https://pkg.go.dev/github.com/ethereum/go-ethereum@v1.10.22/crypto/secp256k1

v1.10.22 has all those functions

Can you run `go mod download` and then trying `make nomctl` again?

-------------------------

0x3639 | 2024-12-12 22:45:55 UTC | #28

[quote="georgezgeorgez, post:27, topic:536"]
make nomctl
[/quote]

```
x3639@0x3639-NoM:~/nomctl$  go mod download
x3639@0x3639-NoM:~/nomctl$ make nomctl
go build -o build/nomctl
# github.com/zenon-network/go-zenon/p2p/discover
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/p2p/discover/node.go:223:27: undefined: secp256k1.RecoverPubkey
# github.com/zenon-network/go-zenon/vm/embedded/implementation
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/bridge.go:47:30: undefined: secp256k1.RecoverPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/bridge.go:1155:20: undefined: secp256k1.DecompressPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:40:26: undefined: secp256k1.CompressPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:61:30: undefined: secp256k1.Sign
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:74:30: undefined: secp256k1.Sign
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:135:36: undefined: secp256k1.RecoverPubkey
make: *** [Makefile:4: nomctl] Error 1
```

-------------------------

0x3639 | 2024-12-12 22:47:33 UTC | #29

i'm on the correct branch

```
x3639@0x3639-NoM:~/nomctl$ git branch
* hyperqube_z
  master
```

-------------------------

0x3639 | 2024-12-12 22:54:03 UTC | #30

tried this

note the version: `go: downloading github.com/ethereum/go-ethereum v1.14.12`  

```
x3639@0x3639-NoM:~/nomctl$ go clean -modcache
x3639@0x3639-NoM:~/nomctl$ go mod tidy
go: downloading github.com/ethereum/go-ethereum v1.14.12
go: downloading github.com/hypercore-one/go-zdk v0.1.1-0.20241212163241-b71304db9eb2
go: downloading github.com/shopspring/decimal v1.3.1
go: downloading github.com/tyler-smith/go-bip39 v1.1.0
go: downloading github.com/urfave/cli/v2 v2.25.7
go: downloading github.com/hypercore-one/hyperqube_z v0.0.0-20241212025544-714b2282baad
go: downloading golang.org/x/term v0.27.0
go: downloading golang.org/x/crypto v0.31.0
go: downloading github.com/cpuguy83/go-md2man/v2 v2.0.2
go: downloading github.com/xrash/smetrics v0.0.0-20201216005158-039620a65673
go: downloading github.com/pkg/errors v0.9.1
go: downloading github.com/prometheus/tsdb v0.10.0
go: downloading github.com/rs/cors v1.8.2
go: downloading github.com/inconshreveable/log15 v2.16.0+incompatible
go: downloading github.com/syndtr/goleveldb v1.0.1-0.20210819022825-2ae1ddf74ef7
go: downloading github.com/btcsuite/btcd/btcutil v1.1.6
go: downloading google.golang.org/protobuf v1.35.2
go: downloading github.com/deckarep/golang-set v1.8.0
go: downloading github.com/gorilla/websocket v1.5.3
go: downloading gopkg.in/natefinch/npipe.v2 v2.0.0-20160621034901-c1b8fa8bdcce
go: downloading golang.org/x/sys v0.28.0
go: downloading github.com/russross/blackfriday/v2 v2.1.0
go: downloading gopkg.in/natefinch/lumberjack.v2 v2.2.1
go: downloading github.com/hashicorp/golang-lru v1.0.2
go: downloading github.com/decred/dcrd/dcrec/secp256k1/v4 v4.3.0
go: downloading github.com/shirou/gopsutil v3.21.11+incompatible
go: downloading github.com/holiman/uint256 v1.3.2
go: downloading github.com/huin/goupnp v1.3.0
go: downloading github.com/jackpal/go-nat-pmp v1.0.2
go: downloading github.com/davecgh/go-spew v1.1.1
go: downloading github.com/google/gofuzz v1.2.0
go: downloading github.com/stretchr/testify v1.9.0
go: downloading github.com/go-stack/stack v1.8.1
go: downloading github.com/mattn/go-colorable v0.1.13
go: downloading github.com/onsi/ginkgo v1.14.0
go: downloading github.com/onsi/gomega v1.10.3
go: downloading golang.org/x/exp v0.0.0-20241210194714-1829a127f884
go: downloading github.com/google/go-cmp v0.6.0
go: downloading github.com/go-kit/kit v0.9.0
go: downloading github.com/decred/dcrd/crypto/blake256 v1.0.1
go: downloading golang.org/x/sync v0.10.0
go: downloading github.com/tklauser/go-sysconf v0.3.14
go: downloading github.com/yusufpapurcu/wmi v1.2.4
go: downloading github.com/pmezard/go-difflib v1.0.0
go: downloading gopkg.in/yaml.v3 v3.0.1
go: downloading github.com/golang/snappy v0.0.5-0.20220116011046-fa5810519dcb
go: downloading github.com/mattn/go-isatty v0.0.20
go: downloading github.com/golang-collections/collections v0.0.0-20130729185459-604e922904d3
go: downloading gopkg.in/karalabe/cookiejar.v2 v2.0.0-20150724131613-8dcd6a7f4951
go: downloading github.com/go-ole/go-ole v1.3.0
go: downloading github.com/tklauser/numcpus v0.9.0
go: downloading github.com/go-logfmt/logfmt v0.3.0
go: downloading golang.org/x/net v0.24.0
go: downloading golang.org/x/xerrors v0.0.0-20200804184101-5ec99f83aff1
go: downloading gopkg.in/yaml.v2 v2.4.0
go: downloading github.com/nxadm/tail v1.4.4
go: downloading github.com/kr/logfmt v0.0.0-20140226030751-b84e30acd515
go: downloading gopkg.in/tomb.v1 v1.0.0-20141024135613-dd632973f1e7
go: downloading github.com/fsnotify/fsnotify v1.6.0
go: downloading golang.org/x/text v0.21.0
x3639@0x3639-NoM:~/nomctl$ go mod download
x3639@0x3639-NoM:~/nomctl$ make nomctl
go build -o build/nomctl
# github.com/zenon-network/go-zenon/p2p/discover
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/p2p/discover/node.go:223:27: undefined: secp256k1.RecoverPubkey
# github.com/zenon-network/go-zenon/vm/embedded/implementation
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/bridge.go:47:30: undefined: secp256k1.RecoverPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/bridge.go:1155:20: undefined: secp256k1.DecompressPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:40:26: undefined: secp256k1.CompressPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:61:30: undefined: secp256k1.Sign
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:74:30: undefined: secp256k1.Sign
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:135:36: undefined: secp256k1.RecoverPubkey
make: *** [Makefile:4: nomctl] Error 1
```

-------------------------

georgezgeorgez | 2024-12-12 23:07:36 UTC | #31

I switched to my linux machine and can't replicate.
Also I need to update the instructions to use `~/.hqzd` instead of `~/hqzd` for linux
```
george@nom:~/testing$ git clone git@github.com:hypercore-one/nomctl.git
cd nomctl
git checkout hyperqube_z
make nomctl
./build/nomctl -hq generate-devnet -ez
Cloning into 'nomctl'...
remote: Enumerating objects: 97, done.
remote: Counting objects: 100% (97/97), done.
remote: Compressing objects: 100% (62/62), done.
remote: Total 97 (delta 56), reused 68 (delta 33), pack-reused 0 (from 0)
Receiving objects: 100% (97/97), 79.10 KiB | 1.98 MiB/s, done.
Resolving deltas: 100% (56/56), done.
branch 'hyperqube_z' set up to track 'origin/hyperqube_z'.
Switched to a new branch 'hyperqube_z'
go build -o build/nomctl
go: downloading go1.22.5 (linux/amd64)
go: downloading github.com/hypercore-one/hyperqube_z v0.0.0-20241212025544-714b2282baad
go: downloading github.com/hypercore-one/go-zdk v0.1.1-0.20241212163241-b71304db9eb2
go: downloading github.com/ethereum/go-ethereum v1.14.12
go: downloading golang.org/x/term v0.27.0
go: downloading golang.org/x/crypto v0.31.0
go: downloading golang.org/x/sys v0.28.0
go: downloading github.com/btcsuite/btcd/btcutil v1.1.6
go: downloading google.golang.org/protobuf v1.35.2
go: downloading github.com/gorilla/websocket v1.5.3
go: downloading github.com/huin/goupnp v1.3.0
go: downloading github.com/mattn/go-isatty v0.0.20
go: downloading golang.org/x/sync v0.10.0
go: downloading github.com/holiman/uint256 v1.3.2
go: downloading golang.org/x/exp v0.0.0-20241210194714-1829a127f884
go: downloading github.com/tklauser/go-sysconf v0.3.14
go: downloading github.com/tklauser/numcpus v0.9.0
george@nom:~/testing/nomctl$ go version
go version go1.22.5 linux/amd64
```

-------------------------

0x3639 | 2024-12-12 23:08:49 UTC | #32

I installed go with snap.  Let me try a fresh install

-------------------------

0x3639 | 2024-12-13 01:07:10 UTC | #33

Im in

```
Loaded a valid genesis config from path '/home/x3639/.hqzd/genesis.json'
Initialized NoM. Height: 1, Hash: bf1658dff419ec7175d6c045c068b52d7f12e1eccf2a545db1f4eecc5357b5f9
Producing momentum ...
[Momentum inserted] Height: 2, Hash: 5cf4d30a5a551368b4144dbe722851c4366788ac7a1a6a3cd6c7d303be6607b3, Timestamp: 1734051900, Pillar producer address: z1qzxza5uqe7q096yzj254fllzj3ne5g08at59gh, Current time: 2024-12-12 19:05:02, Txs: 0
hqzd successfully started
*** Node status ***
* Producer address detected: z1qzxza5uqe7q096yzj254fllzj3ne5g08at59gh
Producing momentum ...
[Momentum inserted] Height: 3, Hash: c2102467ec7c570ae1abfbc285e41279198404cc5541c20a666bd5b67848a393, Timestamp: 1734051960, Pillar producer address: z1qzxza5uqe7q096yzj254fllzj3ne5g08at59gh, Current time: 2024-12-12 19:06:00, Txs: 0
```

```
./build/nomctl -hq znn-cli -p "Don'tTrust.Verify" plasma.fuse z1qzxza5uqe7q096yzj254fllzj3ne5g08at59gh 1000
Using the default keyStore z1qzxza5uqe7q096yzj254fllzj3ne5g08at59gh
Fusing 1000 QSR to z1qzxza5uqe7q096yzj254fllzj3ne5g08at59gh
Done
```

-------------------------

0x3639 | 2024-12-13 01:24:43 UTC | #34

no idea what was causing that issue.  I switched to a different ubuntu VM 22.04 desktop and it worked.

-------------------------

georgezgeorgez | 2024-12-13 01:25:20 UTC | #35

so note the time in between momentums is a minute
and if you run the balance command you should see utilZ and utilQ

the cli still uses ZNN and QSR in its messages in some places, which I'll fix later

-------------------------

0x3639 | 2024-12-13 01:25:27 UTC | #36

cool.  I'll let it run a while

-------------------------

georgezgeorgez | 2024-12-13 01:27:02 UTC | #37

i'll put some instructions together for it
but basically one thing to try is

activate the spork to deactivate pillar registration
make a new address
send funds to it
try to register a new pillar
get a failure

-------------------------

vilkris | 2024-12-13 13:28:42 UTC | #38

I tested hqzd locally but I’m having issues generating momentums. Running on macOS with M1. Go version is 1.23.4.

Findings:

When trying to generate a momentum the producer event is discarded because `“current time is before start time”`. This is caused by the producer event being fired before the event should start. The producer event is consistently being fired between 1 to 3 milliseconds too early. Sometimes it will fire the event on the correct time and the momentum will be generated.

I narrowed down the problem to [this line](https://github.com/hypercore-one/hyperqube_z/blob/714b2282baad9a837d0ed8518c634225b7f0ad16/consensus/consensus.go#L174) in `consensus.go`. For whatever reason either the `time.After` method or the `time.Sub` method is inaccurate and the resulting imprecision causes the producer event to be fired slightly too soon. As a quick fix adding an additional 10 millisecond delay here ensures that the event is not fired too soon.

The hqzd changes do not touch this area of the code and I can’t think of a reason why the hqzd changes would cause this. I didn’t have to time to test if this same issue happens on a mainnet devnet yet.

Edit: Not able to reproduce this issue on a mainnet devnet in the otherwise same environment.

-------------------------

georgezgeorgez | 2024-12-13 16:32:54 UTC | #39

I've seen that same issue when running hqzd devnet. It only seemed to happen occasionally for me.
It could be a race condition that with a 10s blocktime, it's busy with something and technically a little behind always.

-------------------------

georgezgeorgez | 2024-12-13 17:04:32 UTC | #40

https://pkg.go.dev/time

> If Times t and u both contain monotonic clock readings, the operations t.After(u), t.Before(u), t.Equal(u), t.Compare(u), and t.Sub(u) are carried out using the monotonic clock readings alone, ignoring the wall clock readings. If either t or u contains no monotonic clock reading, these operations fall back to using the wall clock readings.

-------------------------

georgezgeorgez | 2024-12-13 17:04:25 UTC | #41

@vilkris did you let your computer sleep at all?
i think i might have only seen the issues when my laptop slept but i kept the node running

> On some systems the monotonic clock will stop if the computer goes to sleep. On such a system, t.Sub(u) may not accurately reflect the actual time that passed between t and u. The same applies to other functions and methods that subtract times, such as [Since](https://pkg.go.dev/time#Since), [Until](https://pkg.go.dev/time#Until), [Before], [After](https://pkg.go.dev/time#After), [Add], [Sub], [Equal] and [Compare]. In some cases, you may need to strip the monotonic clock to get accurate results.

-------------------------

georgezgeorgez | 2024-12-13 18:12:29 UTC | #42

Yeah I think I was able to reproduce by telling my laptop to sleep

```
Producing momentum ...
[Momentum inserted] Height: 350, Hash: abc09b5e43e490481d2599360b0b48b537b5463a5548f142d8f7e978e45e392f, Timestamp: 1734110975, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:29:35, Txs: 0
Producing momentum ...
[Momentum inserted] Height: 351, Hash: 7b7c7fb34bb4853b040e0cf4db5033ca87f2fd0f2078c94cd0d708868fd948a3, Timestamp: 1734111035, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:30:35, Txs: 0
Producing momentum ...
[Momentum inserted] Height: 352, Hash: 788baf76cdc75fa5a52d8d2af9d98b83730db2bbabcda5a4a974fb0a248331e3, Timestamp: 1734111095, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:31:35, Txs: 0
Producing momentum ...
[Momentum inserted] Height: 353, Hash: cbf7a745c62d88fe841011cf0128a9273248373935572ea183ee004472944fd8, Timestamp: 1734111155, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:32:35, Txs: 0
Producing momentum ...
[Momentum inserted] Height: 354, Hash: 708844703035efd936be47ca385a4af5d9156414e77c18e1ccf7185b1a09832c, Timestamp: 1734111215, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:33:35, Txs: 0
Producing momentum ...
[Momentum inserted] Height: 355, Hash: d8a5d322e845bc0eb6cece6822469376b6ca1b76f0234943a44cde08904314e2, Timestamp: 1734111275, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:34:35, Txs: 0
Producing momentum ...
[Momentum inserted] Height: 356, Hash: 42de37b26518275c19186cc0b8e6b09fbc9e45262b832ba46e079fc0ee828b0a, Timestamp: 1734111335, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:35:35, Txs: 0
Producing momentum ...
[Momentum inserted] Height: 357, Hash: 939ca8f89974f23e9d2a51507e3846e042f6c0fdc0bc1376d3b7e2dce3895a4a, Timestamp: 1734111395, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:36:35, Txs: 5
Producing momentum ...
[Momentum inserted] Height: 358, Hash: f0294126a11b780f6d15213240adde573e746eac26a04e61e4d9185b5b801100, Timestamp: 1734111455, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:37:35, Txs: 5
Producing momentum ...
[Momentum inserted] Height: 359, Hash: 25e7fd0511df32b6bb9784d70e4cac2cae363a41a61f5d3db16292de73481de8, Timestamp: 1734111515, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:38:35, Txs: 0
Producing momentum ...
[Momentum inserted] Height: 360, Hash: 04425a68a99b3c5a4a1efedf1d75aacaa488804dda486f3a7b72b3bad05ece29, Timestamp: 1734111575, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:39:35, Txs: 0
Producing momentum ...
Producing momentum ...
[Momentum inserted] Height: 361, Hash: cf900f4fef5bf3afba3354847185e57c172ff5120dad731f2dccaae617bbde5e, Timestamp: 1734112055, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:47:35, Txs: 0
Producing momentum ...
[Momentum inserted] Height: 362, Hash: c066dd49839e1108b463b65aba435e748b249d7807a93d98588901ba6c687500, Timestamp: 1734112115, Pillar producer address: z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh, Current time: 2024-12-13 12:48:35, Txs: 0
Producing momentum ...
Producing momentum ...

```

```
t=2024-12-12T20:49:34-0500 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-12 20:49:35 -0500 EST EndTime:2024-12-12 20:50:35 -0500 EST Producer:z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh Name:Local}" reason="current time is before start time"
t=2024-12-13T12:47:23-0500 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 12:40:35 -0500 EST EndTime:2024-12-13 12:41:35 -0500 EST Producer:z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh Name:Local}" reason="current time is after the event's finish time time"
t=2024-12-13T13:04:40-0500 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 12:49:35 -0500 EST EndTime:2024-12-13 12:50:35 -0500 EST Producer:z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh Name:Local}" reason="current time is after the event's finish time time"
t=2024-12-13T13:07:02-0500 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 13:05:35 -0500 EST EndTime:2024-12-13 13:06:35 -0500 EST Producer:z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh Name:Local}" reason="current time is after the event's finish time time"
t=2024-12-13T13:07:34-0500 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 13:07:35 -0500 EST EndTime:2024-12-13 13:08:35 -0500 EST Producer:z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh Name:Local}" reason="current time is before start time"
t=2024-12-13T13:08:34-0500 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 13:08:35 -0500 EST EndTime:2024-12-13 13:09:35 -0500 EST Producer:z1qpeql04cww98g5qczqkgxxjgdtwmyjfn3x0adh Name:Local}" reason="current time is before start time"
```

You can see where I slept the computer yesterday night.
And these messages only show up again right after the double `Producing momentum...` which is when I put the computer to sleep

-------------------------

vilkris | 2024-12-13 20:54:05 UTC | #43

[quote="georgezgeorgez, post:41, topic:536"]
@vilkris did you let your computer sleep at all?
i think i might have only seen the issues when my laptop slept but i kept the node running
[/quote]
Nope, no sleeping. The issue starts immediately once I start the node. Not sure how much time we want to spend on this right now, since the root cause may be hard to figure out and fix.

Adding something like this would solve the problem in my environment:
```diff
diff --git a/consensus/consensus.go b/consensus/consensus.go
index 1c86bad..ec061fd 100644
--- a/consensus/consensus.go
+++ b/consensus/consensus.go
@@ -172,6 +172,13 @@ func (cs *consensus) work() {
                        case <-cs.closed:
                                return
                        case <-time.After(event.StartTime.Sub(time.Now())):
+                               // In some cases the time awaited by time.After is slightly incorrect.
+                               // This loop ensures the event is not broadcast too soon.
+                               for {
+                                       if time.Now().Unix() >= event.StartTime.Unix() {
+                                               break
+                                       }
+                               }
                        }
```

-------------------------

georgezgeorgez | 2024-12-13 22:09:30 UTC | #44

I agree. Let's not dwell on it.
Does it stop all momentum production or only make it unreliable for you?

I am hesitant to make a patch for everyone if we don't understand the behavior.
It sounds like your current env is a laptop. I think we should first see if you or others have the same issue on the actual servers they will run the hqzd node on.

-------------------------

vilkris | 2024-12-14 09:33:50 UTC | #45

[quote="georgezgeorgez, post:44, topic:536"]
Does it stop all momentum production or only make it unreliable for you?
[/quote]
It doesn't stop completely but it makes it unreliable and sometimes it can go a long time without being able to generate momentums. Then at other times it will generate momentums with no problems for a while. See the logs here, this happened shortly after I started the node and computer was not in sleep mode:
```
t=2024-12-13T09:47:42 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 09:47:43 EndTime:2024-12-13 09:48:43 Producer:z1qqzsrnzpfev0dvu5eqge2t8kx4uzpmq30hpzpr Name:Local}" reason="current time is before start time"
t=2024-12-13T09:48:42 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 09:48:43 EndTime:2024-12-13 09:49:43 Producer:z1qqzsrnzpfev0dvu5eqge2t8kx4uzpmq30hpzpr Name:Local}" reason="current time is before start time"
t=2024-12-13T09:49:42 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 09:49:43 EndTime:2024-12-13 09:50:43 Producer:z1qqzsrnzpfev0dvu5eqge2t8kx4uzpmq30hpzpr Name:Local}" reason="current time is before start time"
t=2024-12-13T09:50:42 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 09:50:43 EndTime:2024-12-13 09:51:43 Producer:z1qqzsrnzpfev0dvu5eqge2t8kx4uzpmq30hpzpr Name:Local}" reason="current time is before start time"
t=2024-12-13T09:51:42 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 09:51:43 EndTime:2024-12-13 09:52:43 Producer:z1qqzsrnzpfev0dvu5eqge2t8kx4uzpmq30hpzpr Name:Local}" reason="current time is before start time"
t=2024-12-13T09:52:42 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 09:52:43 EndTime:2024-12-13 09:53:43 Producer:z1qqzsrnzpfev0dvu5eqge2t8kx4uzpmq30hpzpr Name:Local}" reason="current time is before start time"
t=2024-12-13T09:53:42 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 09:53:43 EndTime:2024-12-13 09:54:43 Producer:z1qqzsrnzpfev0dvu5eqge2t8kx4uzpmq30hpzpr Name:Local}" reason="current time is before start time"
t=2024-12-13T09:54:42 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 09:54:43 EndTime:2024-12-13 09:55:43 Producer:z1qqzsrnzpfev0dvu5eqge2t8kx4uzpmq30hpzpr Name:Local}" reason="current time is before start time"
t=2024-12-13T09:55:42 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-13 09:55:43 EndTime:2024-12-13 09:56:43 Producer:z1qqzsrnzpfev0dvu5eqge2t8kx4uzpmq30hpzpr Name:Local}" reason="current time is before start time"
```

[quote="georgezgeorgez, post:44, topic:536"]
I am hesitant to make a patch for everyone if we don’t understand the behavior.
[/quote]
Fair enough. We can table this discussion for now. I'm using a Mac mini, but you're right that the main environment will be Linux distributions. I'll spin up a VPS to test it there.

-------------------------

vilkris | 2024-12-14 12:48:20 UTC | #46

[quote="georgezgeorgez, post:37, topic:536"]
but basically one thing to try is

activate the spork to deactivate pillar registration
make a new address
send funds to it
try to register a new pillar
get a failure
[/quote]

I ran this sequence and it is working as expected. Pillar does not get registered and the following message is shown in the log:
```
t=2024-12-14T12:32:43+0000 lvl=info msg="generated embedded-block" module=pillar submodule=worker send-block-header="{Address:z1qqzsrnzpfev0dvu5eqge2t8kx4uzpmq30hpzpr HashHeight:{Hash:9d3a17fafa8fe4bb8e79cf9b0b8d19076dc65cc47c2ce6a928a513d0acb1eeee Height:10
}}" identifier="{Address:z1qxemdeddedxpyllarxxxxxxxxxxxxxxxsy3fmg HashHeight:{Hash:5b17fdc01ee060eba2df37a0cad59d6ad6dbbd08a636b4534f1434ed038a5f54 Height:4}}" send-block-hash=9d3a17fafa8fe4bb8e79cf9b0b8d19076dc65cc47c2ce6a928a513d0acb1eeee returned-error="a
ddress cannot call this method" 
```

Is it the plan to activate the no pillar spork via genesis config on hqz?

Also, no momentum production issues to report on Ubuntu 22.04.

-------------------------

georgezgeorgez | 2024-12-14 17:14:25 UTC | #47

Yes we will activate it using genesis config for the actual network.
I figured having it on devnet for now as an explicit spork activation would help explain how its working.

-------------------------

CryptoFish | 2024-12-14 17:29:07 UTC | #48

I ran into no problems when executing these commands.

-------------------------

coinselor | 2024-12-16 08:02:52 UTC | #49

Managed to build and run it on an ubuntu 24 VM. However, it got stuck at height 2. I submited a plasma.fuse tx to see if that would move it, but didn't help.

![image|690x387](upload://ihTphUxK8guqmMPCF1mZiOGaXPa.png)

btw the repo is public but I had to use https to clone it, so maybe safer to use that for future tutorials :sweat_smile:

Update: Height 3 happened 19 minutes later. Tx showed up, plasma.list updated correctly.

![image|690x187](upload://zt8IiX7j0bRGryxCe8KJa0DqAuT.png)

-------------------------

georgezgeorgez | 2024-12-16 08:48:16 UTC | #50

what are the specs of this vm?

-------------------------

coinselor | 2024-12-16 15:14:04 UTC | #51

![image|690x309](upload://zpUjKt6S1LwDg36WZvwhBatdDDS.png)


This is a fresh install. It's possible this is going to sleep on idle somehow. It's up to height 6, but the multiple "Producing momentum ..." lines are not normal right?

Update: This is printing exactly one momentum each 30 minutes... ? I restarted the node at height 8 to see if it would help. It pretty much printed height 9 instantly then print slowly.

![image|526x500](upload://ylrO3X9KmeZHbyBRZLJOMqZCeNt.png)

-------------------------

georgezgeorgez | 2024-12-16 17:40:20 UTC | #52

Can you dump log/zenon.log and the error.log as well?

-------------------------

vilkris | 2024-12-16 18:57:06 UTC | #53

I'm having issues getting all unit tests to pass and this is happening with the go-zenon codebase as well, so probably not related to hqzd changes. I can reproduce the problem with Ubuntu and macOS.

Can anyone confirm that all unit tests are passing for them? Running `go test -run ./...` in the project's root will run the tests.

-------------------------

georgezgeorgez | 2024-12-16 19:03:19 UTC | #54

Which tests?
I have had this issue before.

One thing I have urgently for future work packages is to baseline the code.

-------------------------

vilkris | 2024-12-16 20:10:33 UTC | #55

These embedded pillar tests:
```
TestConsensus_1
TestConsensus_2
TestPillar_RegisterRevokeRegisterPillar
```
And then most embedded sentinel and embedded stake tests are failing.

The weird thing is that if I run the tests via VSCode then the tests pass. Downgraded Go to 1.22.10 but same results.

In any case this a bit off topic since it's not caused by the hqzd changes.

-------------------------

coinselor | 2024-12-17 13:38:47 UTC | #56

zenon.error.log
```
t=2024-12-16T07:36:04+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:d9ccdca74382fd098ca346f842a11e8b4389b2c8fe74c94b5c333cfb8586e601 Height:2}" reason=too-late
t=2024-12-16T07:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:3b3d9a31fdaebc49101dfae712d5bda0e745633aa1e42d11e155af909cdaee16 Height:3}" reason=too-late
t=2024-12-16T08:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:b5572903d74c77009a1bdf2c3dbc7e8a4faa0e61a2802dc63209e943ef3ebf31 Height:4}" reason=too-late
t=2024-12-16T08:39:44+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:da534816fb75e17b1446003c2810e651d9fcf35ed998e6bb9acc213275db7cf9 Height:5}" reason=too-late
t=2024-12-16T08:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:e6719d6c1400458997fb263f2cb0e42eef78c55c69b8172c50c2cd74faf592fa Height:5}" reason=too-late
t=2024-12-16T10:14:53+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:271db8d005646f1049fc4897e67adce490e1d258c990b5530efd626c81f6cbef Height:6}" reason=too-late
t=2024-12-16T10:25:23+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:2e133a6b31e1a968f72168f2c77d82c18a7d1e1e2faaea32135f56f520340b5c Height:6}" reason=too-late
t=2024-12-16T10:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:68fc19e0e7913f481deba3b44514568071d071b62fa6fc96c15e766b21f5be37 Height:7}" reason=too-late
t=2024-12-16T11:25:23+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:dfc1c6c01a64d6faf99a43c28f95e49b5fb347ebcc30fed4840dfeec2dd248ab Height:8}" reason=too-late
t=2024-12-16T11:32:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:6d154188e46c4ae7dc86a4046d3e0adc132c91f33726d2cebef52012bb8cab4d Height:9}" reason=too-late
t=2024-12-16T11:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:656ae1783db5bc0d6f7f315b6b99bdac637726effefb0cbfe690306d455bc986 Height:10}" reason=too-late
t=2024-12-16T12:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:b7a6947a78eaad02f0d4eae6215605bc3e51ff095ba5d1086091a07c30a99a9b Height:11}" reason=too-late
t=2024-12-16T12:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:ac9c019e9a50cadb21a5297361a96babbeec063e38614f0e51d47411e840c475 Height:12}" reason=too-late
t=2024-12-16T13:25:23+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:5adde345639ca999417eea888e9445fd709754471272c815c7900fa9f36d4b90 Height:13}" reason=too-late
t=2024-12-16T13:25:23+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:5adde345639ca999417eea888e9445fd709754471272c815c7900fa9f36d4b90 Height:13}" reason=too-late
t=2024-12-16T13:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:d7bb77034996825d2a376bc8220138f7317271033b2cb05cbd7682686cc76b81 Height:14}" reason=too-late
t=2024-12-16T14:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:e5876d73d401d450e22a7664245c0d6954cd348396fd37cf397ee6b82374056b Height:15}" reason=too-late
t=2024-12-16T14:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:e48169a4e4a0330507dab5a1f4f6c785b1ae538fc8c9b03ccc2025b993362bb1 Height:16}" reason=too-late
t=2024-12-16T15:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:b97c64cb2ee39449b010370601aeb29a8f68ff22f9f20483f53d4a039bdaf901 Height:17}" reason=too-late
t=2024-12-16T15:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:14cef4b36d741623b51beb8a99863561f54a98c80296e00bfae0f8f5d5ee5a2b Height:18}" reason=too-late
t=2024-12-16T16:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:5bdc8feec1782f9588db45e8f969c660f0ba68007566df3ed4535f365e318b32 Height:19}" reason=too-late
t=2024-12-16T16:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:7decfba0401ac07b1b5a450361f5e95b082cbee802ca95e1c3663318d1e69ac6 Height:20}" reason=too-late
t=2024-12-16T17:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:7b92a29d8cdb6bfd0ad9967f9344b59390fd66df9a3c4ad7c28c4c51bd090b9a Height:21}" reason=too-late
t=2024-12-16T17:55:23+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:1f862c5a0d0cada146cabd4c634f67de0a3deb0c6f2ba887f925132a67e73655 Height:22}" reason=too-late
t=2024-12-16T18:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:72f752e83513621251eee6bb9b131204e76e8724a6eddf90597ae657d7ff6cbc Height:23}" reason=too-late
t=2024-12-16T18:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:8202c58f12ad9656cc6a2cfea48a7153b6679d3c722924f10c43567e8783dffc Height:24}" reason=too-late
t=2024-12-16T19:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:8df5a66caa946cc6df8e6e52829777e6f7c6de56b511b2407823cb759a2c0ff6 Height:25}" reason=too-late
t=2024-12-16T19:55:23+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:92e84f16589fbbf1b5c26c67df696856a048ced1d4cb8f6d99b083bd8ed32520 Height:26}" reason=too-late
t=2024-12-16T19:55:23+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:92e84f16589fbbf1b5c26c67df696856a048ced1d4cb8f6d99b083bd8ed32520 Height:26}" reason=too-late
t=2024-12-17T09:07:43+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:da356c800350590c1ec8f81e891d1984bd0bb72303d4c5eb1d4ce30bf01b8a4c Height:27}" reason=too-late
t=2024-12-17T09:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:5d2c4ab64f0348914e61fc958e7cedf4f840c8de327b72759ab98b19547827a4 Height:27}" reason=too-late
t=2024-12-17T09:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:72a6a314bc836c15f4b6698c7fb9b99df947b9a3f92f8a2561248c29d67960f2 Height:28}" reason=too-late
t=2024-12-17T10:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:561f239a611becfb420b695e0fc393ba250489325f860d1d1775a92d4c603603 Height:29}" reason=too-late
t=2024-12-17T10:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:cf61f44d3606ec004f889a134605c7ab8cf74b704b37b6878eb81bbb88d7ba72 Height:30}" reason=too-late
t=2024-12-17T11:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:a9774a97d2e928cad602d5ce97c503dc027b358dc76f253219d99abb6002d48d Height:31}" reason=too-late
t=2024-12-17T11:40:57+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:ab945f818166612a9f1363c086a09525f1a111cfd33e6da5732d2602f76e9598 Height:32}" reason=too-late
t=2024-12-17T11:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:1b4a58ebb5dbdb451dd123fead2c8bb5dbaa9d6b59c81d24985c36c20fa77eb5 Height:32}" reason=too-late
t=2024-12-17T12:25:23+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:c4e2c7444531ac722afc5307f76b60602d69924f98cbbf9ff972bd4a77fc1786 Height:33}" reason=too-late
t=2024-12-17T12:55:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:f5c6f6c4faf2a6a5aa27abe645af56ad2eaac8f2569046b61772201b4843c1db Height:34}" reason=too-late
t=2024-12-17T13:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:0ba4444452a46c7d23d77a56b9497bebeaddbc24ae25fcdc08e505bb223458db Height:35}" reason=too-late
```

zenon.log
```
t=2024-12-17T13:13:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:13:24 +0000 WET EndTime:2024-12-17 13:14:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:14:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:14:24 +0000 WET EndTime:2024-12-17 13:15:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:15:23+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:15:24 +0000 WET EndTime:2024-12-17 13:16:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:16:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:16:24 +0000 WET EndTime:2024-12-17 13:17:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:17:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:17:24 +0000 WET EndTime:2024-12-17 13:18:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:18:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:18:24 +0000 WET EndTime:2024-12-17 13:19:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:19:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:19:24 +0000 WET EndTime:2024-12-17 13:20:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:20:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:20:24 +0000 WET EndTime:2024-12-17 13:21:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:21:23+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:21:24 +0000 WET EndTime:2024-12-17 13:22:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:22:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:22:24 +0000 WET EndTime:2024-12-17 13:23:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:23:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:23:24 +0000 WET EndTime:2024-12-17 13:24:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:24:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:24:24 +0000 WET EndTime:2024-12-17 13:25:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:25:22+0000 lvl=info msg="momentum producer triggered" module=pillar submodule=manager event="{StartTime:2024-12-17 13:24:24 +0000 WET EndTime:2024-12-17 13:25:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}"
t=2024-12-17T13:25:22+0000 lvl=info msg="producing momentum" module=pillar submodule=worker event="{StartTime:2024-12-17 13:24:24 +0000 WET EndTime:2024-12-17 13:25:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}"
t=2024-12-17T13:25:22+0000 lvl=eror msg="do not broadcast own momentum" module=pillar submodule=worker identifier="{Hash:0ba4444452a46c7d23d77a56b9497bebeaddbc24ae25fcdc08e505bb223458db Height:35}" reason=too-late
t=2024-12-17T13:25:22+0000 lvl=info msg="start creating autoreceive blocks" module=pillar submodule=worker
t=2024-12-17T13:25:22+0000 lvl=info msg="checking if can update contracts" module=pillar submodule=worker
t=2024-12-17T13:25:22+0000 lvl=info msg="momentum producer trigger finished" module=pillar submodule=manager event="{StartTime:2024-12-17 13:24:24 +0000 WET EndTime:2024-12-17 13:25:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}"
t=2024-12-17T13:25:24+0000 lvl=info msg="momentum producer triggered" module=pillar submodule=manager event="{StartTime:2024-12-17 13:25:24 +0000 WET EndTime:2024-12-17 13:26:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}"
t=2024-12-17T13:25:24+0000 lvl=info msg="producing momentum" module=pillar submodule=worker event="{StartTime:2024-12-17 13:25:24 +0000 WET EndTime:2024-12-17 13:26:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}"
t=2024-12-17T13:25:24+0000 lvl=info msg="broadcasting own momentum" module=pillar submodule=worker identifier="{Hash:391f7d150fdf78146b9a700a3040065d939bb1da5de87b66e511e417594d2109 Height:35}"
t=2024-12-17T13:25:24+0000 lvl=info msg="creating own momentum" module=handler submodule=broadcaster identifier="{Hash:391f7d150fdf78146b9a700a3040065d939bb1da5de87b66e511e417594d2109 Height:35}"
t=2024-12-17T13:25:24+0000 lvl=info msg="inserting new momentum" module=chain submodule=momentum-pool identifier="{Hash:391f7d150fdf78146b9a700a3040065d939bb1da5de87b66e511e417594d2109 Height:35}"
t=2024-12-17T13:25:24+0000 lvl=info msg="computed producers" module=consensus submodule=uniform-election-manager proof-hash=b4465b4de809da61911cea5d19fd07a73a158d628ddff8447546636f2c01fe4a proof-height=34 delegations=[Local@0] producers="[z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369]"
t=2024-12-17T13:25:24+0000 lvl=info msg="broadcasting own momentum" module=handler submodule=broadcaster identifier="{Hash:391f7d150fdf78146b9a700a3040065d939bb1da5de87b66e511e417594d2109 Height:35}"
t=2024-12-17T13:25:24+0000 lvl=info msg="propagated momentum to peers" module=handler num-peers=0 momentum-identifier="{Hash:391f7d150fdf78146b9a700a3040065d939bb1da5de87b66e511e417594d2109 Height:35}"
t=2024-12-17T13:25:24+0000 lvl=info msg="announced momentum to peers" module=handler num-peers=0 momentum-identifier="{Hash:391f7d150fdf78146b9a700a3040065d939bb1da5de87b66e511e417594d2109 Height:35}"
t=2024-12-17T13:25:24+0000 lvl=info msg="start creating autoreceive blocks" module=pillar submodule=worker
t=2024-12-17T13:25:24+0000 lvl=info msg="finish broadcasting momentum" module=rpc module=subscribe_api identifier="&{Hash:391f7d150fdf78146b9a700a3040065d939bb1da5de87b66e511e417594d2109 Height:35}" elapsed=2.143µs stats="&{NumNotify:0 NumUninstalls:0}"
t=2024-12-17T13:25:24+0000 lvl=info msg="checking if can update contracts" module=pillar submodule=worker
t=2024-12-17T13:25:24+0000 lvl=info msg="momentum producer trigger finished" module=pillar submodule=manager event="{StartTime:2024-12-17 13:25:24 +0000 WET EndTime:2024-12-17 13:26:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}"
t=2024-12-17T13:26:23+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:26:24 +0000 WET EndTime:2024-12-17 13:27:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:27:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:27:24 +0000 WET EndTime:2024-12-17 13:28:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:28:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:28:24 +0000 WET EndTime:2024-12-17 13:29:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:29:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:29:24 +0000 WET EndTime:2024-12-17 13:30:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:30:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:30:24 +0000 WET EndTime:2024-12-17 13:31:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:31:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:31:24 +0000 WET EndTime:2024-12-17 13:32:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:32:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:32:24 +0000 WET EndTime:2024-12-17 13:33:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:33:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:33:24 +0000 WET EndTime:2024-12-17 13:34:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
t=2024-12-17T13:34:22+0000 lvl=info msg="do not process current event" module=pillar submodule=manager event="{StartTime:2024-12-17 13:34:24 +0000 WET EndTime:2024-12-17 13:35:24 +0000 WET Producer:z1qq4ghtxdvmcdm5rdue6ut95n9hplx7fsh8d369 Name:Local}" reason="current time is before start time"
```

Seems like I'm getting that same issue vilkris had with the time, and then there's that "do not broadcast own momentum".

-------------------------

georgezgeorgez | 2024-12-20 03:28:32 UTC | #57

Just some ramblings:

```
func (ea *uniformElectionAlgorithm) uniformRandom(groupA []*types.PillarDelegation, context *AlgorithmConfig) []*types.PillarDelegation {
	var result []*types.PillarDelegation
	total := int(ea.group.NodeCount)
	sort.Sort(types.SortPDByWeight(groupA))

	seed := ea.findSeed(context)
	for len(result) < total {
		random1 := rand.New(rand.NewSource(seed))
		arr := random1.Perm(len(groupA))
		for _, index := range arr {
			result = append(result, groupA[index])
		}
	}
	return result[:total]
}
```

In my testing with 5 pillars, I am getting a consistent 5 min time between blocks by the same pillar. Well obviously with the seed being set once, random1 will always produce the same permutation. 

The following code should be functionally the same:

```
func (ea *uniformElectionAlgorithm) uniformRandom(groupA []*types.PillarDelegation, context *AlgorithmConfig) []*types.PillarDelegation {
	var result []*types.PillarDelegation
	total := int(ea.group.NodeCount)
	sort.Sort(types.SortPDByWeight(groupA))

	seed := ea.findSeed(context)
	random1 := rand.New(rand.NewSource(seed))
	arr := random1.Perm(len(groupA))
	for len(result) < total {
		for _, index := range arr {
			result = append(result, groupA[index])
		}
	}
	return result[:total]
}
```
This consistent permutation should be fine for our purposes for now, but I wonder if we should hash the seed or something to produce a new permutation each go around.

-------------------------

georgezgeorgez | 2024-12-20 03:39:37 UTC | #58

https://github.com/hypercore-one/nomctl/pull/47/files

Added a `nomctl generate-hyperqube-genesis -qubepad-csv <FILE>` command to use exported CSV from qubepad.

-------------------------

georgezgeorgez | 2024-12-20 15:01:23 UTC | #59

![Screenshot 2024-12-20 at 10.00.24 AM|690x276](upload://iwYxZ0LOyJsLyghajwdrNjAIAat.png)

-------------------------

georgezgeorgez | 2024-12-20 18:01:35 UTC | #60

[genesis.json|attachment](upload://svdgCBtU1P1eztzvOM2e0vsu7CB.json) (9.4 KB)

for testnet
genesis timestamp dec 21 noon est

-------------------------

georgezgeorgez | 2024-12-20 19:15:26 UTC | #61

[quote="georgezgeorgez, post:60, topic:536"]
genesis.json
[/quote]

```
curl -L https://forum.hypercore.one/uploads/short-url/svdgCBtU1P1eztzvOM2e0vsu7CB.json -o ~/.hqzd/genesis.json
```

-------------------------

georgezgeorgez | 2024-12-20 20:03:05 UTC | #62

```
  "Net": {
    "ListenHost": "0.0.0.0",
    "ListenPort": 45995,
    "MinPeers": 4,
    "MinConnectedPeers": 4,
    "MaxPeers": 60,
    "MaxPendingPeers": 10,
    "Seeders": [
	    "enode://763935dbbdd2ed59e64d2263884887abf865165129f18af9fb1cd0e961b936405144970e7363e6be3d0f0bc3d1e4a0e2ac22306335b8102941728718e063777b@45.77.193.218:45995"
    ]
  }
```

-------------------------

georgezgeorgez | 2024-12-26 16:33:10 UTC | #63

In terms of testing, I have not used AI much for coding so dipping my toe in, I got it to spit out:

```
#!/bin/bash

# Set the interval time in seconds (configurable)
INTERVAL=5  # Default to 5 seconds

# Check if a custom interval is provided as a command-line argument
if [ ! -z "$1" ]; then
    INTERVAL=$1
fi

# Configurable URL (set the URL you want to use for the -u flag)
URL="http://127.0.0.1:35997" 

# Check if a custom URL is provided as a command-line argument
if [ ! -z "$2" ]; then
    URL=$2
fi

# Define the array of addresses (customizable)
ADDRESSES=("address1" "address2" "address3")  # Replace with actual addresses

# The constant part of the receive command with the -hq, -u, -k, and -p flags
RECEIVE_COMMAND="./build/nomctl -hq znn-cli -u $URL -k hqz -p Don'tTrust.Verify receiveAll"

# The constant part of the send command with the -hq, -u, -k, and -p flags
SEND_COMMAND="./build/nomctl -hq znn-cli -u $URL -k hqz -p Don'tTrust.Verify send"

# Loop indefinitely
while true; do
    # Execute the receive command first
    $RECEIVE_COMMAND
    echo "Executed: $RECEIVE_COMMAND"

    # Loop through the addresses and execute the send command
    for ADDRESS in "${ADDRESSES[@]}"; do
        # Execute the send command with the current address
        $SEND_COMMAND "$ADDRESS" 1 "zts1utylzxxxxxxxxxxx6agxt0"
        
        # Optional: print the command being executed for debugging purposes
        echo "Executed: $SEND_COMMAND $ADDRESS 1 zts1utylzxxxxxxxxxxx6agxt0"
        
        # Wait for the specified interval before repeating the command
        sleep $INTERVAL
    done
done

```

-------------------------

georgezgeorgez | 2024-12-26 16:37:31 UTC | #64

Here's an updated script so that the receiveAll command is only run once a min

```
#!/bin/bash

# Set the interval time in seconds (configurable)
INTERVAL=5  # Default to 5 seconds

# Check if a custom interval is provided as a command-line argument
if [ ! -z "$1" ]; then
    INTERVAL=$1
fi

# Configurable URL (set the URL you want to use for the -u flag)
URL="http://127.0.0.1:35997"  # Default URL is now set to localhost

# Check if a custom URL is provided as a command-line argument
if [ ! -z "$2" ]; then
    URL=$2
fi

# Define the array of addresses (customizable)
ADDRESSES=("address1" "address2" "address3")  # Replace with actual addresses

# The constant part of the receive command with the -hq, -u, -k, and -p flags
RECEIVE_COMMAND="./build/nomctl -hq znn-cli -u $URL -k hqz -p Don'tTrust.Verify receiveAll"

# The constant part of the send command with the -hq, -u, -k, and -p flags
SEND_COMMAND="./build/nomctl -hq znn-cli -u $URL -k hqz -p Don'tTrust.Verify send"

# Variable to track when to run the receive command
LAST_RECEIVE_TIME=0
SECONDS_IN_MINUTE=60

# Loop indefinitely
while true; do
    # Get the current time in seconds
    CURRENT_TIME=$(date +%s)
    
    # If one minute has passed since the last receive command, run the receive command
    if ((CURRENT_TIME - LAST_RECEIVE_TIME >= SECONDS_IN_MINUTE)); then
        # Execute the receive command
        $RECEIVE_COMMAND
        echo "Executed: $RECEIVE_COMMAND"
        
        # Update LAST_RECEIVE_TIME to the current time
        LAST_RECEIVE_TIME=$CURRENT_TIME
    fi

    # Loop through the addresses and execute the send command
    for ADDRESS in "${ADDRESSES[@]}"; do
        # Execute the send command with the current address
        $SEND_COMMAND "$ADDRESS" 1 "zts1utylzxxxxxxxxxxx6agxt0"
        
        # Optional: print the command being executed for debugging purposes
        echo "Executed: $SEND_COMMAND $ADDRESS 1 zts1utylzxxxxxxxxxxx6agxt0"
        
        # Wait for the specified interval before repeating the command
        sleep $INTERVAL
    done
done
```

-------------------------

0x3639 | 2024-12-26 20:19:21 UTC | #65

Public testnet node `ws://172.245.234.82:35998`

-------------------------

0x3639 | 2024-12-27 10:29:20 UTC | #66

If you get this error you need to install `build-essential`

```
go build -o build/nomctl
# github.com/zenon-network/go-zenon/p2p/discover
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/p2p/discover/node.go:223:27: undefined: secp256k1.RecoverPubkey
# github.com/zenon-network/go-zenon/vm/embedded/implementation
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/bridge.go:47:30: undefined: secp256k1.RecoverPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/bridge.go:1155:20: undefined: secp256k1.DecompressPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:40:26: undefined: secp256k1.CompressPubkey
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:61:30: undefined: secp256k1.Sign
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:74:30: undefined: secp256k1.Sign
../go/pkg/mod/github.com/hypercore-one/hyperqube_z@v0.0.0-20241212025544-714b2282baad/vm/embedded/implementation/swap_utils.go:135:36: undefined: secp256k1.RecoverPubkey
make: *** [Makefile:4: nomctl] Error 1
```


`sudo apt-get install -y build-essential pkg-config`

-------------------------

0x3639 | 2024-12-30 12:03:50 UTC | #67

I want to test a new sentrify setup when we go live.  Been working with the `go-zenon` code.  Looks like we have some options in `config.json`

```
// Discovery specifies whether the peer discovery mechanism should be started
// or not. Disabling is usually useful for protocol debugging (manual topology).
Discovery bool

// Static nodes are used as pre-configured connections which are always
// maintained and re-connected on disconnects.
StaticNodes []*discover.Node
``` 

The sentrify tool from @MoonBaze sets the static peers in the `Seeders`.  I wonder why we don't do something like this below in `config.json`.  We can allow traffic between the Sentry and Pillar, allow DNS and NTP, and block all other traffic.  I'm looking to test a sentrify setup with a private subnet.  In the `SENTRY_IP` section below I will use a private IP address.  

@georgezgeorgez do you see any issues with this setup?

```
  },
  "Net": {
    "ListenHost": "0.0.0.0",
    "ListenPort": 45995,

    "Discovery": false,
    "StaticNodes": [
      "enode://763935dbbdd2ed59e64d2263884887abf865165129f18af9fb1cd0e961b936405144970e7363e6be3d0f0bc3d1e4a0e2ac22306335b8102941728718e063777b@SENTRY_IP:45995"
    ],

    "MinPeers": 4,
    "MinConnectedPeers": 4,
    "MaxPeers": 60,
    "MaxPendingPeers": 10
  }
```

-------------------------

0x3639 | 2024-12-30 12:39:49 UTC | #68

I'm actually going to extend this test.  On the sentry I'm going to only allow connections from the known peer list.  

https://raw.githubusercontent.com/0x3639/znn-node-parser/refs/heads/master/data/seeders.txt

This data is scraped and updated every 6 hours.  I forked Sol's code here: https://github.com/0x3639/znn-node-parser

This way someone needs to run a node, get in the list, and then try to attack the network.  We will see the traffic and block them.  So I'm going to test this setup.

-------------------------

