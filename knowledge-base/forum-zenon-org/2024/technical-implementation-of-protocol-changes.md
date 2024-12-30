Thread: technical-implementation-of-protocol-changes
romeo | 2022-07-27 01:01:10 UTC | #1

I made a post in the ZNN category surrounding next steps for the ZIP framework from a community perspective, but inline with those recommendations @dexter703 made a good point around the need for more information on the technical implementation of protocol level changes.

Previously the core developers have deployed these changes to the network without any involvement from the community, and we expect them to also make the next protocol change themselves (NoM Phase 1).

After Phase 1 however - how would we as a community deploy changes to the codebase?

Have any of the @devs mapped out how this works yet?

Is there a logical flow for deploying the code? Do Pillars have to manually update every time? How many do we need to update before the change is live? How does the code get to them?

Perhaps we will get a good insight into the process if the core devs complete a ZIP with the implementation plan detailed for NoM Phase 1 - but I imagine it also already exists within the code.

Lets use this thread as an opportunity to discuss and document it.

-------------------------

0x3639 | 2022-07-27 09:18:51 UTC | #2

I have experience with THORChain upgrades and consensus.  

Devs write the code and offer it on Github (Gitlab).  Nodes can chose to adopt it or not.  If a certain % adopt the code it becomes adopted.  For the code to run all active nodes need to be upgraded.  If they don't upgrade within a 2 or 3 day period (can't remember), they are kicked out of consensus and no longer earn rewards.  And, if they are running an active node (doing consensus and signing transactions) and do shitty work, the are penalized.  Shitty work meaning node goes down, don't sign transactions or dishonest actor.  Nodes cannot participate in consensus (after getting kicked out) unless they are running the latest software.  

This system works well and the community has node trackers that report what version each node is running.  Nodes can secure relay messages to the community to voice support / opposition to code upgrades. 

Last upgrade Core did something to kick out the nodes who did not upgrade.  Not sure what they did, but we need to remove that "feature" obviously.  Or make it official....  Like if code is approved by the community, the Pillars / Sentinals have 3 days to upgrade or they are kicked out of consensus and don't earn rewards.

-------------------------

romeo | 2022-07-28 06:42:09 UTC | #3

Some additional points:

- Logically the ZIP repository on GitHub should reside under the official Zenon-Network account. We'll have to ask Sigli to request it be created.

- We need to have a vote to identify the first Editor/s will be and the core team will have to give them the appropriate rights within GitHub

-------------------------

0x3639 | 2022-07-28 12:58:19 UTC | #4

[quote="romeo, post:3, topic:877"]
We need to have a vote to identify the first Editor/s will be and the core team will have to give them the appropriate rights within GitHub
[/quote]

o boy....  Wonder if they will do that.

-------------------------

romeo | 2022-07-28 13:22:13 UTC | #5

Well we could always vote in the core team to be the editors too, for at least a period of time, assuming they would be willing to fulfil the role (they kinda do already now)

-------------------------

Dumeril | 2022-07-28 14:44:05 UTC | #6

Regarding the implementation side, we can look at the changes they made to activate the accelerator. It required a spork, and I know there’s a few places where activation is checked now in the code, so that should be a good example. 
I can look at that in a few days and try to break it down to the logical steps, unless  anyone else can already describe it.

-------------------------

romeo | 2022-08-01 00:00:37 UTC | #7

Thanks Dumeril, if you can provide any insight it would be appreciated.

I'm going to propose the following, I'll create a new vote for it on the forum before moving to a formal on-chain vote:

1) Core Devs create ZIPs under official Zenon repo
2) Core Devs fill editor role for a period of 6 months (after which we look to transition to community editors)
3) Core Devs submit a ZIP for the protocol upgrade and follow the Stage 1 workflow (forum vote followed by an A-Z vote, then manually added to the ZIP repo and distributed to Pillars for implementation)
4) Clarify implementation/Spork steps and document the process

-------------------------

Dumeril | 2022-08-01 04:48:20 UTC | #8

I suggest, before working on plans potentially requiring cooperation from kaine & co, we ask them if they would agree to play along

-------------------------

romeo | 2022-08-01 04:53:59 UTC | #9

I've messaged MrK on Tele and provided questions to the team via Sigli recently (in relation to the above) - waiting for a response :pray:

-------------------------

Dumeril | 2022-08-02 20:02:11 UTC | #10

I’ve looked at the code regarding accelerator activation. Turns out, most of the code was already there since first release. But it doesn’t  matter, the important part is the activation which happened later. 
So let’s say we’re interested in the way sporks work. In lack of an official definition for spork, I simply consider it a software update that leads to a fork which may extend the existing protocol, in which case it’s not backwards compatible to pre-spork states. In this way it can have the characteristics of a soft fork or a hard fork. The important thing is, it is activated at some later time by a transaction with specific properties. If that’s not a correct definition, please correct me anyone. 

In go-zenon a spork is activated in multiple stages:
- an account block is sent to the embedded spork contract
- a code update references the corresponding transaction hash as id for this spork (see common/types/spork.go); for accelerator this was done twice (v0.0.3 and v0.0.4). The first wasn’t activated. 
- the CreateSporkMethod from the embedded spork contract is executed (I’m not entirely sure currently if that is triggered by the same tx from step 1 - not important now), creating a spork instance in the database (just some meta data)
- at a later point the ActivateSporkMethod from the same contract is executed (also triggered by a transaction), storing the spork as activated in the database. 

6 blocks later the spork is active (that’s a hard-coded delay). 

Using the spork id (the hash we added to the code earlier) it is now possible to execute code conditionally: pre spork-height vs. post spork-height. For the accelerator, this is done in three places currently (check for IsAcceleratorSporkEnforced), which were added with v0.0.3. 
I’m not sure if we could change everything with these conditionals (e.g. constants? Probably not), but I think we could code a way around everything. 

That looks easy enough so far, but the important part is: spork creation and activation is only possible from the spork address, which is defined with genesis. 
It would be possible to change that or add allowed addresses with a spork, but currently only a single unknown entity can activate changes.

-------------------------

