Thread: public-rpc-node-incentives
sol | 2023-07-05 19:04:18 UTC | #1

There is clearly a demand for public nodes and not enough supply. Those service providers bear the costs of bandwidth, compute, and resource management.

At least, the current set of operators capable of supplying the service aren't jumping at the opportunity to be altruistic.

In my situation, it would cost me an additional ~$25/month to host a public node, but I'm not receiving any sort of compensation.

----------

Today, I propose an incentive model that introduces a new dynamic in our current delegation order. Those who embrace this incentive will likely rise to the top 30 pillars while the others could lose weight, especially as we onboard new aliens in the ecosystem.

I've PoC'd* a websocket proxy in Golang that can intercept Zenon client RPC requests and selectively return data based on any criteria. Service providers can choose which RPC calls they want to allow or deny. 

Examples of aforementioned criteria:
- Return data only for addresses that have delegated X amount to a specific pillar for Y days
- Return data based on an arbitrary allow-list
   - only for your small Discord community
   - only paying subscribers
   - only orchestrators or other node operators can use it
- Drop data based on request type or source address


We can productize this solution to simplify the criteria selection process for less technical pillars.
They can reduce the rewards they share in order to offset the cost for this service.

For example, if a non-delegator makes a request to query their account balance in Syrius, they will see a spinning wheel. Only delegators would have unrestricted access to all RPC calls.
Pillars can get creative with their offerings.
Non-pillars could potentially adopt this by finding other ways to receive compensation for their service.

Eventually, we could have a page like [this one](https://publicnodes.somenano.com/), displaying node capabilities, current status, etc.

\* the PoC is rough but could be worth pursuing if the community supports the idea.

----------
> inb4 Trust. Don't Verify.

Until we have a process to validate which nodes are acting honestly, the community will have to trust the nodes they connect to. Given pillars are incentivized to maintain a good relationship with their delegators, they will likely provide truthful data.

We can also work towards the goal of node validation. There are some objective sources of truth that we can leverage, minimizing the amount of trust required to use them. Eventually, we'll solve this problem too.

----------

Some scenarios

- Service providers bear all the costs
  - Not scalable -- little participation to date
  - Not sustainable for anyone that isn't generating income for this service
- Public nodes are subsidized by AZ
  - Not scalable to many service providers
  - May not be sustainable or a good use of funds
- Freemium model
  - A subset of functionality is free or rate-limited
  - Criteria is defined for "paying" subscribers
    - These could be delegators
  - Premium access is less/not limited
- Public nodes as a premium service
   - Privately-funded, dedicated infrastructure for subscribers
   - Scalable and sustainable

-------------------------

Chadass | 2023-07-05 14:23:05 UTC | #2

[quote="sol, post:1, topic:148"]
Chadass will get all the delegootoors
[/quote]

So if I run a public node I finally can get weight ? Good

-------------------------

0x3639 | 2023-07-05 15:02:20 UTC | #3

!wen PoC beta testing?  Great idea BTW @sol

-------------------------

Shazz | 2023-07-05 17:29:45 UTC | #4

Great idea

-------------------------

georgezgeorgez | 2023-07-05 18:34:59 UTC | #5

@sol can you clarify the title to reflect that this is for RPC
as public protocol nodes fall under sentinels

-------------------------

aliencoder | 2023-07-05 18:52:16 UTC | #6

[quote="sol, post:1, topic:148"]
* * These could be delegators
[/quote]

Brilliant idea Sol! Public facing nodes are a vital component for scaling the user base in the future.

One thing that I would address is onboarding new Syrius desktop users. Most of them will be non-technical people that don't even know what a node is and will go with the default option in Syrius after creating their wallet.

This is not good, as they won't be able to make any transactions until the embedded node is fully synced. I've already highlighted the problem [here](https://forum.zenon.org/t/syrius-improvements/578/140?u=aliencoder).

How can we address this issue?

-------------------------

coinselor | 2023-07-05 19:29:03 UTC | #7

I understand that the requirements to run a Nostr relay are significantly less than a public NoM node. However, the point still stands that running a nostr relay is not free, yet there are a great number of people running them and coming up with ways to monetize them. Isn't what you are describing basically the same thing? 

It's easier to see after your great explanation that pillars are the most trustworthy public node operators, and the free market is already showing promise of going in that direction (i.e deeznnutz offering public infra since day one). 

I think your PoC is great and will significantly increase the number of pillars that choose to incentivize delegating to them or coming up with their own ideas for value add by offering reliable public nodes.

-------------------------

sol | 2023-07-05 19:30:46 UTC | #8

[quote="aliencoder, post:6, topic:148"]
How can we address this issue?
[/quote]

I would prefer to implement a dynamic solution in Syrius.

Option A
- We hard-code specific nodes in Syrius source code
- List is difficult to maintain, slow reaction when a node is no longer available

Option B
- Trusted entities manage their own list of valid nodes and permit Syrius to download that list dynamically
- We would have to hard-code these trusted entity endpoints into Syrius but hopefully this won't need to change frequently

Examples
   - https://zenon.org/nodes.json (dynamic, less reliable)
   - https://hypercore.one/nodes.json (dynamic, less reliable)
   - ipfs://nfdosibnodfsbdsfob/nodes.json (constant or dynamic, more (?) reliable)
   - https://ubd92139723d.arweave.net/u2dhb9d23u/#/nodes.json (constant, permanent)
   - znn://10e08ab7e98c68975283523 (constant, permanent -- requires an active node connection to retrieve the data)

My main concerns are flexibility and availability. 
Maybe Syrius can do a ping check before establishing a connection to verify availability.
We already have a way to inform users when the connected node's chainId is not mainnet (1).

Other concerns: privacy, data integrity, performance, operational honesty. These can be evaluated by the groups that curate dynamic lists.
 

-----

I'm open to other suggestions. I haven't done extensive research on this topic.

-------------------------

aliencoder | 2023-07-05 21:43:17 UTC | #9

[Option C](https://nostr.info/relays/)

- Implement a Nostr client into Syrius
- Public nodes will host relays and will advertise their availability

-------------------------

sol | 2023-07-05 22:08:13 UTC | #10

I appreciate the suggestion. I'm trying to assess how it's different/better than Option B, though there is the argument of [redundancy](https://t.me/zenonnetwork/228370).

Wouldn't Syrius still need to connect to a centralized relay that keeps track of all available nodes?
This reminds me of the IBD [initialization problem](https://t.me/zenonnetwork/231456).

-------------------------

aliencoder | 2023-07-06 13:54:34 UTC | #11

Idk, but we need a solution for new users that are installing Syrius.

-------------------------

sol | 2023-07-06 14:27:27 UTC | #12

Are you opposed to Option B for the initial implementation?
Option C is more complex and I'm not sure if it's better in any way.

Shouldn't take much time to develop this solution, but I'd like to give everyone time to suggest alternatives before committing to this.

-------------------------

aliencoder | 2023-07-06 14:39:10 UTC | #13

[quote="sol, post:12, topic:148"]
Are you opposed to Option B for the initial implementation?
[/quote]

Not at all.

-------------------------

0x3639 | 2023-07-06 15:22:16 UTC | #14

Option B looks good.  LMK the format of the json and I will test it out with zenon.info/nodes.json

-------------------------

aliencoder | 2023-07-06 15:46:13 UTC | #15

[quote="0x3639, post:14, topic:148"]
I will test it out with zenon.info/nodes.json
[/quote]

I wouldn't hardcode zenon.info in Syrius.

-------------------------

sol | 2023-07-06 16:15:07 UTC | #16

[quote="aliencoder, post:15, topic:148"]
I wouldn’t hardcode zenon.info in Syrius.
[/quote]

Which trusted entities would you add to Syrius?

0x is a respected member of the community. I don't see a problem here...

I'm hoping we have multiple data providers and users can choose who they trust.

Perhaps we can poll the community to see who wants to be a data provider and have another poll to see which ones are most trusted to provide curated data?

I'm almost willing to give all devs a pass as long as they want to participate.

-------------------------

0x3639 | 2023-07-06 16:59:16 UTC | #17

how do we determine the trusted entities to provide /nodes.json?

deeZNNutz == 0x == zenon.info

Is one URL better / worse than the other?

-------------------------

aliencoder | 2023-07-06 18:49:19 UTC | #18

[quote="aliencoder, post:15, topic:148"]
I wouldn’t hardcode zenon.info in Syrius.
[/quote]
Sorry, didn't want to sound negative at all.

[quote="sol, post:8, topic:148"]
* ipfs://nfdosibnodfsbdsfob/nodes.json (constant or dynamic, more (?) reliable)
[/quote]

In my opinion `ipfs` is one of the best options if we go with `Option B`.

We also have `Option D`: hardcode the [seed list](https://github.com/alienc0der/go-zenon/blob/4276148de65e9b943a23d3ba261ee9ce897a60c3/p2p/config.go#L30) from `go-zenon`, parse it and discover nodes that satisfy the following requirements:

- Have `wss` configured
- Respond in a certain amount of time

-------------------------

sol | 2023-07-06 19:19:41 UTC | #19

I considered Option D but didn't want to use nodes that aren't explicitly consenting to this procedure. 
We could say there's already consent since they configured a public service but I'm not sure if we should be promoting them automatically.

Also, this option doesn't support testnets.

afaik there are only three public nodes that use wss at the moment. I'm hoping this increases soon.

-------------------------

0x3639 | 2023-07-06 19:57:30 UTC | #20

what if we setup some repos on github

/zenon-network/nodes/nodes.json
/hypercore-one/nodes/nodes.json
/hypercore-team/nodes/nodes.json

Community members can submit PRs to add their nodes to the list.  Devs will need to diligence the requests.

-------------------------

aliencoder | 2023-07-06 20:26:35 UTC | #21

[quote="sol, post:19, topic:148"]
I considered Option D but didn’t want to use nodes that aren’t explicitly consenting to this procedure.
[/quote]

You are consenting if you have `wss` properly configured. I think we can retrieve more info.

[quote="sol, post:19, topic:148"]
Also, this option doesn’t support testnets.
[/quote]

If you're a pro-user, you will be able to use the Node Management interface to add your testnet node.

[quote="sol, post:19, topic:148"]
afaik there are only three public nodes that use `wss` at the moment.
[/quote]

We can create an incentive structure: if you want to remain connected to this node, consider donating `X` amount of `ZNN` or `QSR`. This can be hardcoded into the wallet. I've used the term `donate` because you cannot request funds without compromising privacy.

-------------------------

sol | 2023-07-07 13:19:05 UTC | #22

[quote="aliencoder, post:21, topic:148"]
You are consenting if you have `wss` properly configured.
[/quote]

If we agree with this statement, then I think Option D might be the way to go, though there could be some end-user confusion if there are gated/paid nodes displayed in the list.

Honestly, I'm between Options B and D.
Maybe we do both.

Also, consider setups that load balance. I have trouble mapping 0x's wss service automatically with my node crawling algo.

-------------------------

0x3639 | 2023-07-06 23:03:49 UTC | #23

[quote="sol, post:22, topic:148"]
Also, consider setups that load balance. I have trouble mapping 0x’s wss service automatically with my node spider algo.
[/quote]

Do I need to change something?

-------------------------

sol | 2023-07-06 23:13:59 UTC | #24

[quote="0x3639, post:23, topic:148"]
Do I need to change something?
[/quote]

I'll have to confirm some IPs with you this week.
Or you could provide an overview of your setup. 

Do you think your load-balancer IP is directly peering with other Zenon nodes?

-------------------------

0x3639 | 2023-07-06 23:20:39 UTC | #25

The LB only handles 35997 and 35998.  The nodes only receive 35997,8 from the LB.

35995 is handled by the nodes directly.  They both have their own public IP and TCP and UDP are open directly to the nodes.  35995 does not run inbound or outbound through the LB.

-------------------------

sol | 2023-07-07 13:18:41 UTC | #26

[quote="0x3639, post:25, topic:148"]
35995 does not run inbound or outbound through the LB.
[/quote]

I'm not sure if any crawling algo will be able to find your wss endpoint automatically.

-------------------------

0x3639 | 2023-07-15 16:22:39 UTC | #27

Guys, I think we should have some public nodes available to SYRIUS.  We will eventually figure out how to incentivize them.  @sumamu has a pretty good idea to do that.  In the meantime, why don't we offer a list of nodes in syrius. Maybe it pulls from a json file that is hosted on HC1 and HCT.  Nodes need to submit a PR to those repos to be added to the list.  

We can add a disclaimer about selecting a public node.  And we can add a link to zenon.info that explains the nodes, the importance of running their own node or using the embedded node in SYRIUS.  But giving people an EZ button will help adoption IMO.  

Thoughts?

-------------------------

coinselor | 2023-07-16 01:36:28 UTC | #28

I don't see an issue with adding these as an optional syrius setting, not the default behavior, obviously. That said, I can also see the argument against it. Mainly, most users will be probably using either a chrome extension or the syrius mobile wallet, which should probably come with a list of public nodes built in, and a public node as a default setting, removing the need for desktop syrius to include them.

-------------------------

sumamu | 2023-07-17 16:54:49 UTC | #29

[quote="0x3639, post:27, topic:148"]
@sumamu has a pretty good idea to do that.
[/quote]

Indeed, the Affiliate Program will start providing Incentives for public nodes soon. 
ETA: next week.

-------------------------

aliencoder | 2023-08-05 13:56:09 UTC | #30

I've [added support](https://forum.zenon.org/t/syrius-improvements/578/159?u=aliencoder) for community public nodes.

Users will be able to connect to a "trusted" community node instead of waiting for the embedded node to sync.

We can still sync the embedded node in the background and switch to it after it's fully synced for a better user experience.

How to add your public node?

- Open `lib/utils/global.dart`
- Add your node in the `kDefaultCommunityNodes` list
- Open a [Pull Request](https://github.com/zenon-network/syrius)

If **2/2 reviewers** accept the PR, your node will appear in Syrius in the `Node Management` section.

Notes:
- Your node must support Secure WebSockets `wss://`
- Your node must have `>99%` uptime
- Your node must have enough resources to serve a large number of users

[quote="sumamu, post:29, topic:148"]
the Affiliate Program will start providing Incentives for public nodes soon
[/quote]

I've also added a `shuffle` before showing the nodes in order to prevent unfair competition.

-------------------------

0x3639 | 2023-08-06 11:48:00 UTC | #31

[quote="aliencoder, post:30, topic:148"]
We can still sync the embedded node in the background and switch to it after it’s fully synced for a better user experience.
[/quote]

BIG BIG BIG brain!!!

Looks like the HC1 node is in your v0.0.7 repo.  

![Screenshot 2023-08-06 at 5.54.04 AM|690x207](upload://zpkseUcfcK8cviQ3MSDrNl6p8dL.png)

To be clear, I think your latest SYRIUS PR needs to be accepted before users can add their node.  I think a few devs are looking at the code now.

-------------------------

aliencoder | 2023-08-06 11:47:01 UTC | #32

[quote="0x3639, post:31, topic:148"]
to be accepted before users can add their node
[/quote]

Only devs can populate the `kDefaultCommunityNodes` list and it must be approved by 2 reviewers to get into the final release. Same goes for removing nodes from that list.

-------------------------

sumamu | 2023-08-08 19:49:56 UTC | #33

Nice work here!

-------------------------

sol | 2023-08-10 18:28:44 UTC | #34

[quote="aliencoder, post:30, topic:148"]
We can still sync the embedded node in the background and switch to it after it’s fully synced for a better user experience.
[/quote]

Is this the configured behavior in your branch?
Can users opt out?

-------------------------

Stark | 2023-08-10 19:33:02 UTC | #35

IIRC Sparrow requires node configuration upon first run. That type of UX seems suitable.

I'd be leary of setting public node as default. Perhaps that type of UX could be default for a "third party" wallet that has it's own brand?

-------------------------

aliencoder | 2023-08-10 20:50:23 UTC | #36

No. The embedded node must be manually started.

-------------------------

aliencoder | 2023-08-10 20:53:06 UTC | #37

[quote="Stark, post:35, topic:148"]
Perhaps that type of UX could be default for a “third party” wallet that has it’s own brand?
[/quote]

If we want to onboard new users we must do it with what we already have. Development pace is already slow and dev time is limited. We don't want to waste it.

-------------------------

digitalSloth | 2023-08-29 16:49:09 UTC | #38

Can the Zenon Hub nodes be included with the upcoming release or should I wait and make a PR after it’s been merged?

The nodes are:
`wss://node.zenonhub.io:35998`
`https://node.zenonhub.io:35997`

-------------------------

mehowz | 2023-08-29 17:57:32 UTC | #39

Those are for syrius 0.0.7 right? Can I include them in the zenon.org list?

![Screen Shot 2023-08-29 at 1.57.18 PM|690x307](upload://eCQLinaVSQEcbKGdQTw5G223suc.png)

-------------------------

0x3639 | 2023-08-29 19:02:59 UTC | #40

@digitalSloth I just requested the addition of mine into SYRIUS

https://github.com/zenon-network/syrius/pull/27

-------------------------

digitalSloth | 2023-08-29 19:39:59 UTC | #41

@mehowz Yes they are for Syrius >= 0.0.7. Please feel free to add them to the list on zenon.org, I have a https node as well: 

```
https://node.zenonhub.io:35997
```

More info can be seen on this page: https://zenonhub.io/nodes

@0x3639 The array Aliencoder mentioned is not in the master branch yet, I think your PR is updating the wrong list, see https://github.com/alienc0der/syrius/blob/release-v0.0.7/lib/utils/global.dart it should be a variable called `kDefaultCommunityNodes`

-------------------------

0x3639 | 2023-08-29 23:21:45 UTC | #42

yep, you are right.  My oversight.  I closed that PR.

-------------------------

aliencoder | 2023-08-30 10:01:54 UTC | #43

[quote="digitalSloth, post:38, topic:148"]
Can the Zenon Hub nodes be included with the upcoming release
[/quote]

That's exactly why I've added this feature.

[quote="digitalSloth, post:38, topic:148"]
should I wait and make a PR after it’s been merged?
[/quote]

I think you should wait for the PR to be merged first.

-------------------------

aliencoder | 2023-08-30 10:02:48 UTC | #44

I would list only the latest Syrius version.

-------------------------

sumamu | 2023-11-29 22:30:00 UTC | #45

The referral program is now incentivizing public nodes at https://bridge.staging.zenon.community

The staging environment is running on mainnet. We should test until Monday and then Dexter will deploy it to production.

-------------------------

Blueginger | 2023-11-30 10:53:02 UTC | #46

Am willing to run a public node. But I need a guide or tutorial.

-------------------------

Chadass | 2023-11-30 14:02:48 UTC | #47

Why Sentinels can't act as public nodes?

-------------------------

aliencoder | 2023-11-30 16:09:18 UTC | #48

[quote="Blueginger, post:46, topic:148"]
But I need a guide or tutorial.
[/quote]

We can start a new thread for this.

[quote="Chadass, post:47, topic:148, full:true"]
Why Sentinels can’t act as public nodes?
[/quote]

They will. But there won't be enough of them. There is an upper limit that the network can support given the circulating supply (5k ZNN/50k QSR you can do the math).

-------------------------

0x3639 | 2023-11-30 19:27:18 UTC | #49

Sorry I have not been able to help.  I'm getting hammered at work.  It's on my list.

-------------------------

