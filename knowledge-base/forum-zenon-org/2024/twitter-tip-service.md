Thread: twitter-tip-service
sol | 2024-03-27 15:19:50 UTC | #1

@0x3639 and I are collaborating on a Twitter tipping service, similar to [z_onum](https://medium.com/@z_onum/z-onum-c5914e72ff85).

At this time, we're considering the implementation of expiring tips.

Example implementation:
- Tips expire after 90 days
- Elon tips 10 ZNN to Jack
- Jack needs to claim his tips in order to receive them
   - One claim for all pending tips
- If Jack doesn't claim his tips, they will eventually expire and be returned to their respective senders.

This deviates from the original design of tips being non-refundable.

I don't mind either way, but refundable tips will require a bit of extra work.

[poll type=regular results=always chartType=bar close=2023-12-02T05:00:00.000Z]
* No refunds
* Tips should expire
[/poll]

Feel free to suggest ideas for the service, though I'm more-or-less aiming for parity with z_onum.

-------------------------

Stark | 2023-11-28 21:51:28 UTC | #2

The claim aspect is interesting... as a tipper, I don't really want to carry the overhead of wondering if my tips are going to be claimed.

Maybe someone will open their tip jar in 20 years and buy a ticket to mars.

-------------------------

0x3639 | 2023-11-29 03:14:53 UTC | #3

The tip jar relies on a centralized server.  if that goes offline with 1m in znn, then what?  The tipor and tipee will never get access to the funds.  

If this was fully decentralized I might feel different, but the tip server is just that, a db on a server that is run by an individual.  When it's shut down at some point in the future what will happen to the tips?  Who owns them.  What if they are worth a lot of $$.

-------------------------

cryptocheshire | 2023-11-29 05:25:38 UTC | #4

Maybe the tip service can be connected to anyone's syrius wallet and each person runs it on their own

-------------------------

sol | 2023-11-29 06:31:51 UTC | #5

Would you all rather a non-custodial tipping service?
It would be more like an address - handle registry, similar to DNS. 

This option means the service provider doesn't ever hold user funds but there's a bit of friction for participants. People that don't register can't receive tips, and tips are generally non-refundable.

I prefer this option but some people I spoke to didn't agree with it.

-------------------------

0x3639 | 2023-11-29 23:27:12 UTC | #6

Need to make this easy and fun.  No one will run infra on their own.  If so, Sol and I will end up tipping each other only.  

The goal should be to have fun and get people to learn about NoM, download the wallet, claim the ZNN and learn about our network.  

my $0.02

-------------------------

coinselor | 2023-11-30 05:47:29 UTC | #7

I agree, it should be an on-boarding vehicle to get people to use syrius. 

I think just having the custodial service periodically send back all non-claimed funds to original tippers would be more than enough. Maybe tipper can chose between:

- Tip and refund if not claimed
- Tip and donate to A-Z if not claimed

-------------------------

0x3639 | 2023-11-30 19:51:36 UTC | #8

[quote="coinselor, post:7, topic:1713"]
Tip and refund if not claimed
Tip and donate to A-Z if not claimed
[/quote]

Great idea!!

-------------------------

