Thread: atomic-swap-pros-and-cons-whats-next
dat_she_pepe | 2024-03-27 15:20:09 UTC | #1

Food for thoughts.

Atomic swap as implemented on Bitcoin forks and others through HTLC it all great and I cheer at George and other's work but from a product ready and users perspective it has quite a few cons in the way atomic swap as been implemented so far ;

- It's slow.
- Liquidity isn't great.
- Liquidity relies in poor incentive design.
- Liquidity relies on complex setups. No LP's here.
- It's not efficient.

All of the above makes it feel like a P2P market, not a financial one. As a user I don't want nor want to see myself clicking 50 times to find the right supplier, to check on fee, to swap, wait, and eventually get my zBTC.

This approach while necessary and all great groundwork might need further steps on the UX and design to be adopted by other solutions and users.

Uniswap isn't successful for nothing. It's simple. It's a money market, and it's efficient. 

Maybe there's a way to build a liquidity market on top of HTLC implementations, I didn't look further in that direction but Thorchain comes to mind.

What do you think ?

-------------------------

0x3639 | 2022-09-10 22:13:05 UTC | #2

I remember having a conversation with @georgezgeorgez and @cryptocheshire  about this.  They thought we could build an order book on top of HTLC. But I cannot remember how that is possible.  Wish I could be more helpful…

-------------------------

cryptocheshire | 2022-09-11 04:48:40 UTC | #3

HLTC is just the settlement process, order matching and execution can and should probably happen independently

-------------------------

