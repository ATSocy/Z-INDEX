Thread: wp1-pillar-momentum-tracking
georgezgeorgez | 2024-10-28 15:23:06 UTC | #1

Coordination thread for Pillar Momentum Tracking

-------------------------

vilkris | 2024-11-16 14:05:58 UTC | #2

Is anyone working on this? If not I could start working on a solution.

Should the produced momentums be tallied up once when a WP is finished? For example if a WP starts at momentum height 10,000 and is finished at height 110,000 we then sum up how many of those 100k momentums each pillar produced and split the ZNN/QSR according to that.

Or do we want a more consistent stream of incentives so that for example every 30 days 10% of the total momentum production incentives can be claimed until there's 50% left to claim, which can only be claimed after the WP is finished.

If feel like a steady stream of incentives would be nice but it might complicate things too much at least now at the start.

-------------------------

digitalSloth | 2024-11-17 09:12:41 UTC | #3

Just to add a quick note on this, pillar producer address can be changed so whatever solution is provided for this WP needs to account for changed producer addresses

-------------------------

vilkris | 2024-11-18 10:47:44 UTC | #4

Right now I'm thinking whether this should be based on existing solutions, maybe utilizing zenon hub or zenon tools stuff, or should a new solution be created which would better suite this specific use case. I would like for this to be something that all pillars can easily verify themselves, so utilizing existing solutions may come with unwanted complexity for the user.

For example the zenon tools indexer stores the information of momentum producers and the pillar producer addresses into a Postgres DB. But this requires setting up and maintaining the Postgres DB and the indexer, which can be a cumbersome task for users and make it complicated for users to verify the momentum production themselves.

If we don't base this off of existing solutions, then an MVP solution could be a simple program/script that checks the producer address changes and goes through the momentums to check its producer.
This of course will hammer the node with requests which will not scale that well when the chain matures.

A more scalable solution could be something like this:
* Create a service that the user can run alongside their node
* The service continuously stores/indexes momentum producer info and producer address info into an embedded DB
* The service exposes an RPC interface with which the user can request the momentum production breakdown for a specified momentum range

-------------------------

georgezgeorgez | 2024-11-18 14:43:04 UTC | #5

I haven't nominated anyone for this work yet since it can technically be done post network launch.
I think for now, all we need is a way to say:

between X and Y momentums, what is the breakdown of momentum production
in the future, when we implement the incubator on chain, we'll have to figure out the details to do it automatically

-------------------------

georgezgeorgez | 2024-11-18 15:06:22 UTC | #6

Thank you @vilkris. 

Based on round 1 pillar voting medians:

Pillar Tracking
2000 / 80250 Points
374 / 15000 ZNN
3738 / 150000 QSR

**Disclaimer** : The payment amounts provided herein are intended as guidelines only and do not constitute a binding offer or guarantee of payment. The HyperQube Incubator framework works with Zenon Network Pillars to signal incentives which are subject to change over multiple rounds. Actual payment amounts will be based on Accelerator-Z grants that depend on the voting rules and requirement of Accelerator-Z.

Do you accept? If so, this shouldn't be a blocker for network launch so please begin the work at your convenience.

-------------------------

vilkris | 2024-11-18 18:46:41 UTC | #7

Yes I accept.

-------------------------

