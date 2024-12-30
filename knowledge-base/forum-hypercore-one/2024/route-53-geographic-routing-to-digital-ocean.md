Thread: route-53-geographic-routing-to-digital-ocean
0x3639 | 2023-07-20 13:24:08 UTC | #1

Does anyone have experience with AWS Route 53 routing traffic to non-aws resources?  

I'm trying to deploy a latency routing node network with Route 53.  Only, I'm routing traffic to VPSs hosted on Digital Ocean (they are cheaper).  

I can `telnet` to endpoints on 35997 through route 53 but they seem to block curl requests.  Wonder if anyone else has encountered this issue.

-------------------------

