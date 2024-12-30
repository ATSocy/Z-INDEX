Thread: atomic-swap-between-btc-and-zenon-network
0x3639 | 2023-04-28 13:37:37 UTC | #1

@sol let's coordinate this swap here.  What do I need to get setup?  Would you be willing to be my counterparty?  

Maybe we swap 1 ZNN with 0.00003414 BTC

What do I need to get started?  Let's use the same CLI tool so it's easy to share commands.

-------------------------

0x3639 | 2023-04-28 13:39:31 UTC | #2

BTW - I've run several BTC nodes.  This one is the best IMO.

https://umbrel.com/

And it's super easy to setup and run.

-------------------------

Chadass | 2023-04-28 14:15:09 UTC | #3

I have everything ready whenever you want to swap.

-------------------------

sol | 2023-04-28 15:22:19 UTC | #4

Thanks for the offer, 0x :slight_smile: 

During testing, I noticed that the [btcatomicswap CLI tool](https://github.com/decred/atomicswap) prevented me from creating P2SH contracts with low BTC amounts. I think the lowest I could send was 0.0007 BTC (~10 ZNN?) on BTC Testnet, limited by a fee calculation. It might be different on BTC Mainnet.

Is it okay if we use BTC Testnet for the initial swap? Once you've completed that, I'd feel more comfortable trying it on Mainnet.

Either way, the instructions are similar. You'll need:
- access to a BTC (pruned or full) node with RPC enabled
  - Enable RPC: `server=1` in bitcoin.conf
  - full node: `txindex=1` in bitcoin.conf
   - pruned node: `txindex=0` in bitcoin.conf + prune-related settings in bitcoin-cli / bitcoin-qt
   - Testnet: `testnet=1` in bitcoin.conf
   - My [bitcoin.conf file for Testnet](https://pastebin.com/b2mpHwQD)
   - Here's a page with [bitcoin.conf reference material](https://riptutorial.com/bitcoin/example/26000/node-configuration)
- access to a BTC wallet with funds (~0.005 BTC is a good amount)
   - [This Testnet faucet](https://coinfaucet.eu/en/btc-testnet/) dispenses 0.01 BTC
- [bitcoin-core](https://bitcoin.org/en/bitcoin-core/)
- [btcatomicswap](https://github.com/decred/atomicswap)
   - Dependency: [Go](https://go.dev/doc/install)
   - Instructions
     - `git clone https://github.com/decred/atomicswap && cd atomicswap`
     - `cd cmd/btcatomicswap && go install`
     - `btcatomicswap`
       - If that fails, you can `go build` and it will create an executable in the same directory


Once you have all that, we can proceed with the instructions for the cross-chain swap.

@Chadass feel free to participate, if you want.

-------------------------

Chadass | 2023-04-28 14:38:25 UTC | #5

Do we swap tBTC or real BTC ?

-------------------------

sol | 2023-04-28 15:02:55 UTC | #6

We can swap either one, depending on which network we want to use.

I'm proposing we initially test with tBTC, then we can do a swap with real coins once we have everything setup.

-------------------------

0x3639 | 2023-04-28 15:11:14 UTC | #7

I recommend we start with testnet.  When I did this with Crypto Fish on NoM i screwed it up like 3x.  So probably better to do on testnet.   I will review everything and get things setup for a test this weekend if that works @sol.

-------------------------

0x3639 | 2023-04-28 20:58:24 UTC | #8

[quote="sol, post:4, topic:33"]
access to a BTC (pruned or full) node with RPC enabled
[/quote]

Did you use a trusted RPC, or sync yourself?  What node software did you use?

-------------------------

0x3639 | 2023-04-28 21:07:17 UTC | #9

Atomic Swap Tool Commands

```
 # Commands:
initiate <participant address> <amount>
participate <initiator address> <amount> <secret hash>
redeem <contract> <contract transaction> <secret>
refund <contract> <contract transaction>
extractsecret <redemption transaction> <secret hash>
auditcontract <contract> <contract transaction>
```

Instructions look pretty straight forward: https://github.com/decred/atomicswap#example

-------------------------

0x3639 | 2023-04-28 21:09:41 UTC | #10

@sol could you jump on a call today to review everything I need to setup?  I think I can just use the bitcoin core wallet and sync.  But wanted to confirm.

-------------------------

sol | 2023-04-28 21:26:35 UTC | #11

[quote="0x3639, post:8, topic:33"]
Did you use a trusted RPC, or sync yourself? What node software did you use?
[/quote]

I downloaded Bitcoin Core, configured bitcoin.conf, and synced my own node using bitcoin-qt.

[quote="0x3639, post:10, topic:33"]
could you jump on a call today to review everything I need to setup? I think I can just use the bitcoin core wallet and sync.
[/quote]

I'm afk for the next few hours. I might be available around 9pm EST, though. I'll ping you on Discord.

I primarily used the Bitcoin core wallet (bitcoin-qt) and it's easy to confirm which network it's connected to, sync status, balance, etc.

-------------------------

0x3639 | 2023-04-28 21:36:51 UTC | #12

OK I think that is all I need.  I'll get going on the sync.  No need to talk tonight (I don't think).

-------------------------

Chadass | 2023-04-28 23:29:05 UTC | #13

I'm synced.

-------------------------

0x3639 | 2023-04-28 23:51:17 UTC | #14

did you sync testnet and mainnet or can you only select one at a time?

-------------------------

sol | 2023-04-29 00:33:58 UTC | #15

I synced both separately, and only one can be in use at any time.

-------------------------

0x3639 | 2023-04-29 17:17:10 UTC | #16

I'm syncing testnet now.  says 5 hours to sync.  @sol will you be around for a swap at 6 or 7 PM your time?  ...as if you don't have better things to do.  If tonight does not work we can reschedule to anytime that works for you.

-------------------------

sol | 2023-04-29 17:20:13 UTC | #17

Sure, just ping me when you're ready

-------------------------

0x3639 | 2023-04-29 19:19:16 UTC | #18

[quote="sol, post:4, topic:33"]
0.0007
[/quote]

@sol can I use the C# CLI?  Do you have any ZNN on your testnet?  If C# is OK, I will create a wallet with it and Share Address

What is your testnet RPC?

-------------------------

sol | 2023-04-29 20:05:50 UTC | #19

[quote="0x3639, post:18, topic:33"]
can I use the C# CLI?
[/quote]

Yes, it should work, though I haven't tried it in a few months.
Feel free to use that or the Dart znn-cli (branch: [spork_htlc](https://github.com/Sol-Sanctum/znn_cli_dart/tree/spork_htlc)).

[quote="0x3639, post:18, topic:33"]
What is your testnet RPC?
[/quote]

RPC: ws://node.zenon.fun:36998
Explorer: http://149.56.108.141:36997

Faucet
```
curl -X POST http://node.zenon.fun:36999/faucet -H 'Content-Type: application/json' -d '{"address":"z1qr3uww8uqh75qnsuxqajegvwaesqynfglrare2"}'
```

The faucet dispenses 100 tZNN and 100 tQSR.
I can manually send you funds if you need.

-------------------------

0x3639 | 2023-04-29 22:08:22 UTC | #20

Let's party!!

![image|690x103](upload://OWrqsZFwnnhTZyebbxGq3rgqle.png)

-------------------------

Bzed | 2023-06-06 15:09:42 UTC | #21

Any thoughts on the main chain swap demo?

-------------------------

0x3639 | 2023-06-06 15:42:54 UTC | #22

SYRIUS cannot be used on main chain yet.  Once it's live I can do a demo for sure.

-------------------------

0x3639 | 2023-06-06 19:24:41 UTC | #23

@Bzed Sorry I misunderstood.  We do not have a timeline to integrate BTC swaps into SYRIUS.  @vilkris and @sol have spent considerable time investigating it.  And their research is not done yet.  Right now I think other "things" are taking a priority.

-------------------------

