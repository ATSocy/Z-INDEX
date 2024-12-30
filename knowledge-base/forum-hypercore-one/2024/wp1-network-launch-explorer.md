Thread: wp1-network-launch-explorer
georgezgeorgez | 2024-10-28 15:22:00 UTC | #1

Coordination thread for network launch explorer

-------------------------

georgezgeorgez | 2024-11-10 10:05:06 UTC | #2

The Network Launch explorer work consists of hosting an explorer for the hyperqube_z network that the community can easily use and access.

Ideologically I think AZ requests should be things others can build on top of.
In terms of an explorer, this would mean a open-source option with the ability to be self-hosted. Perhaps even white-labeled.

This is something I pushed for when @vilkris made his AZ for zenon.tools. So we have an open source version of zenon tools currently.

However, I am also practical and given the incentives below, I think it is reasonable to ask for Explorer hosting for a set period of time. I think 6 months is fair.

Once we work on the reusable LaunchKit for extension chains, we WILL need an open-source option that will be included as part of the LaunchKit. Ideally any Explorer work here would be reusable for that effort when the time comes.

The median incentives signaled by the pillars for round 1:

Network Launch Ops
3000 / 80250 Points
561 / 15k ZNN
5607 / 150k QSR

**Disclaimer** : The payment amounts provided herein are intended as guidelines only and do not constitute a binding offer or guarantee of payment. The HyperQube Incubator framework works with Zenon Network Pillars to signal incentives which are subject to change over multiple rounds. Actual payment amounts will be based on Accelerator-Z grants that depend on the voting rules and requirement of Accelerator-Z.

-------------------------

georgezgeorgez | 2024-11-10 10:19:37 UTC | #3

Apparently zenon hub is open source as well:
https://github.com/zenonhub-io

-------------------------

georgezgeorgez | 2024-11-10 10:28:53 UTC | #4

I will nominate @digitalSloth who mentioned in the matrix channel the possibility of hosting another stack of zenon hub. Do you accept this work?

Given that Hub is already open-source. Scope of work would be:
- any commits to make zenonhub stack multi-network or custom network (hyperqube_z)
- hosting of an instance for 6 months

-------------------------

digitalSloth | 2024-11-10 21:29:33 UTC | #6

[quote="georgezgeorgez, post:4, topic:538"]
Do you accept this work?
[/quote]

Yes sir, happy to work on this

-------------------------

digitalSloth | 2024-11-17 20:41:35 UTC | #7

Iv been researching ways of running one copy of Hub which can index both HyperQube and Mainnet with the option to choose which network you want to browse. Still not sure if I'll end up going with this option, it might be that I run two separate copies of the site dedicated to each network. Need to do some more testing and think about the possible side effects of going with this approach.

-------------------------

