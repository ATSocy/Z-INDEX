Thread: embedded-governance-design
georgezgeorgez | 2023-06-19 16:43:15 UTC | #1

Following up from: https://www.zenonzealot.xyz/10/

This thread will be used to facilitate the open and incentivized planning and design phase to enable the community to do things such as use pillar votes to create/activate sporks and take over admin functions for the bridge and liquidity embedded contracts. I hope to timebox this for 2 weeks ending July 4th.

I welcome all to participate: developers and non-developers. I have created an AZ proposal to ask the pillars to set aside 5k ZNN, 50k QSR for this planning and design phase. I need to work out the specifics, but at the end of the timebox, I will ask the pillars to assign votes to contributors so that we can fairly distribute those funds.

I don't want to dominate the discussion and want to allow others to make a contribution first, so I will wait until tomorrow before I start posting my thoughts.

Please refrain from adding comments of support or disagreement that do not further the conversation. I will likely moderate these out. For example, "Great idea!". If there is an approach you like, the best way to show support is to further develop the conversation in that direction.

-------------------------

georgezgeorgez | 2023-06-19 16:47:54 UTC | #2

I'm debating with myself whether or not to facilitate this initial process trial run for free or not.
I will let the community decide.
If the process is successful I will ask for 10% of the earmarked funds.
500 ZNN, 5000 QSR.

Regardless of the vote however, I will see this through.

-------------------------

sol | 2023-06-22 02:36:36 UTC | #3

Thanks for kicking off this topic, George. Here are some of my thoughts.

----

**What is the governance model trying to achieve?**
- The ability to manage runtime variables and call embedded functions as the administrator
- This includes creating and activating sporks, and executing functions related to the bridge and liquidity contracts


**Scope of change**
- go-zenon -- write/test the governance embedded contract
- go-zenon 
  -- update all variables that we wish to define dynamically
  -- consider variables that are defined by a combination of other variables -> may need to simplify
- SDKs -- update all the same variables to dynamically source values from contract's db
- clients -- update any remaining variable references the same way as the SDKs
- clients -- ability to interact with the governance contract 
   -- Syrius implementation will be different from znn-cli


**Governance contract interface**

- **Functions**
createPoll()
endPoll()
getPolls()
getVariable()
updateVariable() -- includes creating/deleting variables
executeFunction(function, params, execution height)

- **Variables**
variableDb
pollDb
pollFee
pollOptions
pollDuration
pollQuorum


**Incentives**
Since we're discussing the implementation for a new voting system, I propose that we consider updating participant incentives.
I've written a [post about this](https://forum.zenon.org/t/proposal-apply-decay-multiplier-for-pillars-who-do-not-vote/504/14), but it didn't garner much attention.
I'll summarize the arguments here: 
- Poll spammers should be penalized
- Pillars should be rewarded for casting votes
- Valid poll submissions should not incur penalties

We can achieve these objectives with the following policy adjustments:
1. Poll initiators must lock **pollFee** ZNN in the contract
2. Spam polls meet the following criteria: 
   - if spamVotes > sum(yes, no, abstain) after **pollDuration** or if spamVotes == **pollQuorum**
        - donate locked ZNN to AZ
        - delete the poll from **pollDb**
3. All other poll outcomes are valid ---> refund the initiator when the poll completes

Pillar yields or some other reward can be subject to a voting participation multiplier, but I think this point should be reserved for a separate discussion.
Pillars will already be incentivized to vote if they want changes applied to mainnet.


**Execution Flow**

A user will submit a poll to the governance contract
  - They will enter a json payload that the contract executes if the poll is accepted
  - The poll costs **pollFee** to submit, locking the funds for **pollDuration**
  - The poll ends after **pollDuration**

Pillars will submit their votes. 
- Options for the poll will include: Yes, No, Abstain, Spam
- They may re-cast their votes while the poll is still active.

After **pollDuration**, the poll will finish.
- If **pollQuorum** is met and yesVotes > sum(no, abstain, spam) -> execute the json payload 


[details="Example of a json payload for a poll"]
```
{
  "<poll-id>": {
    "variables": [
      {
        "pollDuration": "604800",
        "activationHeight": "4321000"
      },
      {
        "pollFee": "30000000",
        "activationHeight": "4321000"
      },
      {
        "bridgeAdministrator": "z1qxemdeddedxg0vernancexxxxxxxxxxxklyh23",
        "activationHeight": "4321000"
      },
      {
        "liquidityAdministrator": false,
        "activationHeight": "4321000"
      }
    ],
    "functions": [
      {
        "function": "embedded.spork.CreateSpork",
        "parameters": [
          "<spork name>",
          "<spork description>"
        ],
        "executionHeight": "4200040"
      },
      {
        "function": "embedded.spork.ActivateSpork",
        "parameters": [
          "<spork id>"
        ],
        "executionHeight": "4321000"
      }
    ]
  }
}
```
[/details]
In this example, we would be:
- updating four runtime variables -- three value changes and one deletion
- creating a spork and activating it two weeks later
Note: realistically, we may want two separate votes for spork creation and activation.

**Limitations**
- Only predefined functions in the governance contract can be executed. 
A spork would be required to change these. 
This is because I don't see a way to define a variable with another variable.
  - The challenge I faced here: 
instead of passing abstracted function names and params, can we pass the parameters to build AccountBlocks directly in the poll?
   - Seems like we also need to pass the ABI for the specific method we're calling. 
Perhaps we can rely on clients to pre-format these `data` values?
   - I can't dynamically define these `function -> ABI method` associations so they will need to be manually configured in the contract.

**Other considerations**
- We'll need to sanitize the json payload input to ensure [only valid characters](https://en.wikipedia.org/wiki/IDN_homograph_attack) are passed to the rest of the system.

---

PS: I think 5k/50k is expensive for any discussion/planning phase.

-------------------------

georgezgeorgez | 2023-06-20 01:53:32 UTC | #4

Thanks for being the first to contribute!
I am still holding off until tomorrow to begin sharing my ideas.

[quote="sol, post:3, topic:129"]
PS: I think 5k/50k is expensive for any discussion/planning phase.
[/quote]

So I guess I will first ask for leniency given that this is a trial run of the process.
I want to make sure that there are enough incentives to go around for anyone who has a good or interesting idea to share.

As mentioned in my ZenonZealot post, in the future we'll need some way to determine what the appropriate amount to earmark for planning/design should be. Of course, it should be variable based on how important the work is. Since these funds are not earmarked for me, but will be subject to pillar vote, even if we are possibly overpaying for this trial, I don't think it will be towards anyone in particular. I'm optimistic about participation.

Next, I will directly challenge the idea that it won't ever be worth that amount. A thorough design phase goes a long way in ensuring that we get the best price for implementation, and in better timeframes.

At least from personal experience, a lot of my hesitation when it comes to development, comes from a fear that I'll have to scrap it later on. Removing this hesitation gets us faster deliveries.

And without a open process, there is incentive/pressure to "claim" work by producing some semblance of code for it. In that situation, I highly doubt that the design will be what is best for the community. In some cases, the cost of correcting or improving the design in the future, will far outweigh any investment into upfront open and collaborative design.

There are likely also many contributors, especially newer or potential community members, who can't do the end-to-end delivery, but who can deliver a well defined piece of work. A good planning/design phase opens up the door to much greater competition.

I can envision scenarios where work that a single team would ask for 2 or more AZ proposals to cover could instead first undergo a proposal for open design and then end up with a competitive set of implementation proposals that overall saves us money.

On a longer horizon, as code generation/AI assisted development becomes more mature, the line between design and implementation will blur. In the future, design will be the brunt of the work.

After this first trial run, I think it will be a good idea to open up a discussion on how to determine the right amount to set aside for planning/design.

-------------------------

coinselor | 2023-06-20 16:20:51 UTC | #5

I am grateful for the thoughtful and insightful discussions taking place and the services provided by the hc1 crew. I would like to contribute some of my thoughts, which, while not groundbreaking and probably already accounted for, have not been mentioned yet:

1. **Transparency and Accountability:** It's crucial that our governance model is both transparent and accountable. To ensure this, I am sure to be just echoing our intent to:
  * Maintain a comprehensive log of all changes enacted through the governance contract.
  * Make these logs easily accessible to all members of our community, enabling any member to review past decisions and understand the rationale behind them.
2. **Delay Period:** We should consider implementing a delay period between when a proposal is accepted and when the changes are implemented. I think this should be different than the time until the activation height. The benefits of this delay would include:
  * Allowing community members time to digest and respond to approved proposals.
  * Ensuring that decisions are made collectively and aren't rushed.
  * Act as a time-constraint security measure, similar to what sumamu implemented in the bridge.

In regards to Sol's points, here are some more thoughts:

3. **Variable Management:** Sol proposed the `updateVariable()` function, which implies creating and deleting variables. My understanding is that we are planning to replace hardcoded values with variables that we can later adjust through on-chain voting, not introduce new variables. This approach keeps our system flexible while mitigating the risks associated with adding new variables and/or logic.

4. **Naming Conventions:** Sol's proposed names are concise, but I suggest we prioritize clarity, even if it means slightly longer names. For instance:
  * `pollDb` could be renamed to `pollDatabase`.
  * `pollFee` could be renamed to `pollSubmissionFee`.

I'll let the on-chain experts decide if this is worth it in terms of chain/binary bloat. Makes me wonder, is there even a thing as minifying the go contract like what they do with js for websites? 


5. **Defining Governance Framework:** While Sol clearly addressed the module interface and what it's trying to achieve i.e creating sporks, altering runtime variables, changing the bridge admin key. I think that rather than focusing on the specific actions or functions, it might be beneficial to take a step back and define the theoretical objectives of our governance module. To this end, it could be worthwhile to work on outlining a clear governance framework that describes the principles, goals, and limitations of what the module should and should not be able to achieve. This framework would serve as a guiding document for the design and implementation of our governance module and could be adjusted over time as the needs of the community evolve. I believe this is what George is kinda trying to achieve with the discussions, and not just the technical implementation details.

Looking forward to hearing your thoughts on these suggestions and continuing the productive dialogue.

-------------------------

aliencoder | 2023-06-20 19:02:13 UTC | #6

[quote="georgezgeorgez, post:4, topic:129"]
At least from personal experience, a lot of my hesitation when it comes to development, comes from a fear that I’ll have to scrap it later on.
[/quote]

There are too many things to build. That's why we need to carefully plan and prioritize any amount of work. I've already mentioned in the other forum that the Governance Embedded should be a top priority for everyone.

The Governance Embedded should be simple and follow the principles behind AZ's embedded.

I think at this stage we need to iterate pretty fast. We are still lacking many critical components that can drive value to the network.

-------------------------

georgezgeorgez | 2023-06-20 19:39:00 UTC | #7

I think we'll have to iterate on the governance embedded.
But I want us to be conscious and transparent about what we are putting off until later.
My personal goal is to have the first iteration ready to ship by end of July.

**Scopes**

So I want to first delineate 3 different scopes:

1. We currently have existing centralized admin functions. We need to quickly mitigate the possible harm without getting rid of any possible benefits.

2. It is likely that future embedded contracts will adopt an admin pattern as well so that it doesn't have to duplicate governance logic. We should think about what a scalable solution looks like and consider different options in terms of sophistication vs delivery time.

3. A good on-chain governance system could be extended to many areas and applications. For example, as reflected in Sol's post, we have had discussions before about how we can turn what are currently hard-coded constants into dynamic on-chain values which can be subject to governance. I'm also thinking with extension chains and chain relay that higher layers can utilize governance from the root chain.

**Governance Framework: Theory**

In terms of theory and a governance framework, we can look at real world governance systems and the balance of power. We have the legislative branch which writes the law, the executive branch which applies the law, and the judicial branch which interprets the law.

I think it's useful to think about how these concepts and concerns translate to decentralized networks overall and in particular to NoM. Maybe later, we can talk about pillar burn vs delegation in terms of governance.

But in terms of actionable discussion, I want to point out that legislatures are often slow to act, if they can come to agreement to at all. However in many situations, e.g. war, quick and decisive action is needed. So legislatures often have means to grant additional temporary executive power.

And I think we will have to design with this as a consideration, especially given the maturity of our current pillar set.

**Possible Implementations**

z1qxemdeddedxg0vernancexxxxxxxxxxxvmwpcx

To solve for the first scope, we can very quickly create an embedded contract with a set of pass through functions, for each admin interface.
For example, an embedded governance contract that has a CreateSpork, ActivateSpork, bridge/liq methods, which creates proposals for voting and that calls the relevant downstream functions if the proposal passes.
The main design question here would be what are the specific parameters for voting? E.g. time period, quorum, majority vs super-majority. Do different methods have different voting params?

Some possible concerns/limitations:
It gets into a slightly different topic of inactive pillars, but what happens if proposal can never reach quorum?
What if there's an urgent bugfix where the time period doesn't make sense?
Here, some sort of admin could make sense, likely the existing spork address to start.

As alluded to by scope 2, a possible downside to this simple approach is that every new embedded contract requiring admin functionality requires an extension of the governance contract interface.

A generic approach could be having the governance embedded expose one method "SendTx" which takes in the arguments of destination and downstream data. Maybe also fields to attach ZTS to the transaction.

However, this would make it more challenging to have different voting parameters for different types of transactions.

The most sophisticated and scalable option imho, is a templating system. It could expose two functions: ProposeTemplate, SendTemplate

The propose template method would take in a data structure defining a tx template, which fields are variable, and voting parameters. It's like another layer of ABI.
The template would then undergo a vote for acceptance by the pillars. This voting threshold is defined by the governance contract.
If accepted, the template is stored on-chain/in the local db and given an ID.

The send template function would take in a template id and the parameters to render the template. It would then undergo a vote for acceptance by the pillars. This voting threshold is defined by the template.

A system like this likely would not need to be adjusted as new governance capabilities became available.

In terms of the the third scope, I have some ideas on how to migrate hardcoded constants to be on-chain data. But I want to first develop the first two scopes and get a sense of how much harder a sophisticated but scalable system would be over the simple option.

-------------------------

georgezgeorgez | 2023-06-20 19:52:54 UTC | #8

At the very least I want to enable the pillars to take over Spork Creation/Activation asap if they are ready for it. Once we have that, we can iterate at whatever pace the pillars want.

So maybe getting a simple pass through of spork methods, with hardcoded voting params, deployed as quickly as possible should be the first iteration.

For bridge and liquidity, we have the guardian system in place for some level of mitigation so I don't think it's as urgent. Although as I've said elsewhere, the guardian clients don't exist yet.

-------------------------

Shazz | 2023-06-20 20:14:30 UTC | #9

Would rather have non-embedded smart contract enabled first tbh

Pretty sure Kaine is not going to prevent any sporks if they offer benefits to the community

Or sentinels too

-------------------------

georgezgeorgez | 2023-06-20 20:16:32 UTC | #10

I just remembered that we've done some exploration on the ZIP process before which covers some possible voting parameters.
Linking for reference

https://github.com/deeZNNutz-com/ZIP.deeZNNutz/blob/main/0001.md

-------------------------

Shazz | 2023-06-20 20:22:38 UTC | #11

Indeed, will be critical to have eventually for sure. But is the community ready to cut the umbilical cord?

-------------------------

georgezgeorgez | 2023-06-20 20:31:24 UTC | #12

Maybe @aliencoder can expound on why he believes this is a top priority.
Here is the other thread he mentioned for reference
https://forum.zenon.org/t/governance-embedded-for-nom/1474

I think for the HyperCore One developers, we are in agreement that this is a priority.
There is an aspect of risk mitigation, e.g compromised spork address key can halt the network right now.
But I believe more consequentially, greater community ownership, real and perceived, will drive higher levels of collaboration and ultimately productive output.

-------------------------

aliencoder | 2023-06-20 20:35:24 UTC | #13

[quote="georgezgeorgez, post:12, topic:129"]
Maybe @aliencoder can expound on why he believes this is a top priority.
[/quote]

Decentralization. Mr Kaine already said that this is one of the top priorities among dynamic plasma and extension chains.

-------------------------

georgezgeorgez | 2023-06-20 20:36:08 UTC | #14

For reference:
https://t.me/zenonnetwork/289618

-------------------------

georgezgeorgez | 2023-06-20 22:17:27 UTC | #15

[quote="sol, post:3, topic:129"]
* – Syrius implementation will be different from znn-cli
[/quote]

I think we should start planning the Syirus interface.
If there are any design decisions that need to be made upfront, we should identify what those are.
Otherwise, there's no reason why clients and embedded can't be worked on in parallel.

I'm starting to reconcile your thoughts with my own now:

[quote="sol, post:3, topic:129"]
* They will enter a json payload that the contract executes if the poll is accepted
[/quote]

So I like the idea of being able to batch multiple changes together in one vote. I hadn't considered that. I was mostly thinking about a single downstream function call since this can allow for a very generic interface. But it's very likely that some changes only make sense when done together.

In terms of where to store the variable. As in which address's database.
It's probably easiest in the governance contract itself. Part of me thinks it makes more sense to store it with the relevant embedded contracts that will be using the variable, but then every embedded contract needs an UpdateVariable method callable by an admin (the governance) address.

[quote="sol, post:3, topic:129"]
* creating a spork and activating it two weeks later
Note: realistically, we may want two separate votes for spork creation and activation.
[/quote]

One thing I had considered was being able to define some sort of "workflow" or different state machines for different processes. But this seems like we would have to tailor it for every single process. (or define the state machine as on-chain data) That's one reason why I liked the idea of voting on generic transaction sending.

[quote="sol, post:3, topic:129"]
Only predefined functions in the governance contract can be executed.
[/quote]

This is what my templating idea is meant to address.
A two tiered system. First vote on what can be governed and their parameters
Then vote on specific executions

[quote="sol, post:3, topic:129"]
Seems like we also need to pass the ABI for the specific method we’re calling.
Perhaps we can rely on clients to pre-format these `data` values?
[/quote]

For simple passthrough voting, the governance contract likely does not even need to interpret the data at all. It will just store the bytes and use it when it makes then downstream tx. It can be interpreted client side for UI purposes.

-------------------------

georgezgeorgez | 2023-06-20 22:52:52 UTC | #16

Happy to see your participation!

[quote="coinselor, post:5, topic:129"]
1. **Transparency and Accountability:** It’s crucial that our governance model is both transparent and accountable. To ensure this, I am sure to be just echoing our intent to:

* Maintain a comprehensive log of all changes enacted through the governance contract.
* Make these logs easily accessible to all members of our community, enabling any member to review past decisions and understand the rationale behind them.
[/quote]

On-chain is public, so just like with AZ you'll be able to see who votes for what.
In terms of rationale and , not sure that data belongs on chain. Feeless doesn't mean that blockspace doesn't have value.
Of course we are certainly finding ways to be able to put it on chain. I'm just saying from the perspective of process, not sure putting rationale on chain should be part of it.

So regarding transparency, I guess it would mostly be around the transparency for off-chain governance processes. Open Planning and Design processes (this thread) hopefully addresses what you're asking for.

[quote="coinselor, post:5, topic:129"]
2. **Delay Period:** We should consider implementing a delay period between when a proposal is accepted and when the changes are implemented. I think this should be different than the time until the activation height. The benefits of this delay would include:
[/quote]

So I imagine, unless it's for a critical bug, we'll want to have a minimum voting durations. In my templating system, this could be defined as a parameter. At least when it comes to sporks, especially if it's under pillar governance, I equate Spork creation to acceptance, and activation obviously as activation.

The spork creation/activation process is needed to allow clients to modify the binary to activate using the spork id. For something like changing a variable, where clients already know how to use the value, a create / activation process is not strictly needed. But agree that changes should provide time for the community to digest.

[quote="coinselor, post:5, topic:129"]
I’ll let the on-chain experts decide if this is worth it in terms of chain/binary bloat. Makes me wonder, is there even a thing as minifying the go contract like what they do with js for websites?
[/quote]

For stuff like variables in code, the compiler's job is to put it into efficient machine language.
For on-chain data, you're starting to get into things like gRPC and leveldb compression. Sol and I touched upon it during htlc work I think, but not something we need to worry about right now.

[quote="coinselor, post:5, topic:129"]
I think that rather than focusing on the specific actions or functions, it might be beneficial to take a step back and define the theoretical objectives of our governance module.
[/quote]

This process should definitely include both the WHY and the HOW.
As mentioned in a previous post, when it comes to governance, we have a lot of historical ideas and concerns we can draw from. We'll have to apply them to our context, but human behavior is pretty consistent across contexts.

-------------------------

sol | 2023-06-21 05:28:22 UTC | #17

[quote="georgezgeorgez, post:7, topic:129"]
The main design question here would be what are the specific parameters for voting? E.g. time period, quorum, majority vs super-majority. Do different methods have different voting params?
[/quote]

Let's outline some of the obvious functions and discuss the different requirements.
- Activate Spork (acceptance implies spork creation)
- Update variable -- some may be more critical than others
- There are many admin functions for the Bridge and Liquidity contracts, I won't list them all here yet
   - Bridge: Set Token Pair
   - Bridge: Unhalt
   - Bridge: Set Allow Keygen
   - Liquidity: Set Additional Rewards
   - Liquidity: Set Is Halted
   - Liquidity: Set Token Tuple

[quote="georgezgeorgez, post:7, topic:129"]
It gets into a slightly different topic of inactive pillars, but what happens if proposal can never reach quorum?
[/quote]

Disaster scenario: half the pillars are unable to access the global internet. 
Should we limit quorum to those that signed momentums in the last x period?


[quote="georgezgeorgez, post:7, topic:129"]
What if there’s an urgent bugfix where the time period doesn’t make sense?
Here, some sort of admin could make sense, likely the existing spork address to start.
[/quote]
Could we eventually create a multisig address that acts as an admin?
We could adopt the guardians concept, but network-wide. A group of individuals that would respond quickly to an urgent situation.

An emergency poll is created and if a low threshold of non-guardian pillars vote in favor, it will temporarily give executive power to the multisig, which could require half or more of the guardians to sign transactions.

[quote="georgezgeorgez, post:7, topic:129"]
The propose template method would take in a data structure defining a tx template, which fields are variable, and voting parameters. It’s like another layer of ABI.
[/quote]
I was trying to describe this but I don't have enough experience with go-zenon to articulate the right suggestion.

[quote="georgezgeorgez, post:15, topic:129"]
For simple passthrough voting, the governance contract likely does not even need to interpret the data at all. It will just store the bytes and use it when it makes then downstream tx. It can be interpreted client side for UI purposes.
[/quote]
I don't understand how this is possible. Are there any examples in go-zenon or would this be new functionality?

[quote="georgezgeorgez, post:8, topic:129"]
So maybe getting a simple pass through of spork methods, with hardcoded voting params, deployed as quickly as possible should be the first iteration.
[/quote]
I would prefer the template solution but I understand if we want to solve the immediate problem with haste.

[quote="coinselor, post:5, topic:129"]
Make these logs easily accessible to all members of our community, enabling any member to review past decisions and understand the rationale behind them.
[/quote]

I envision a similar process to AZ submissions.
Title, brief description, link to external discussion topic, along with the function calls/data changes payload.

[quote="georgezgeorgez, post:15, topic:129"]
In terms of where to store the variable. As in which address’s database.
It’s probably easiest in the governance contract itself.
[/quote]

Yeah, I'm not sure which way is best. Are there any really good reasons for either storage method?

As for the Syrius UI, it might be better to delay that conversation a little bit.
I propose that we flesh out most of the gov contract details/functionality first, then try to design UI/UX. We wasted a ton of cycles when we worked on HTLC because the contract changed a few times.

-------------------------

SultanOfStaking | 2023-06-22 00:47:01 UTC | #18

Maybe radical but what about penalization for pillars that do not vote.

Im trying to get all the bad ideas out so the good ones will come later

-------------------------

SultanOfStaking | 2023-06-22 00:03:00 UTC | #19

[quote="georgezgeorgez, post:7, topic:129"]
quorum, majority vs super-majority. Do different methods have different voting params?
[/quote]

This is tough because the pillar tracker would suggest there are a handful of people with multiple pillars. Conviction voting could offset this but what is conviction based on? Delegated weight another option?

-------------------------

SultanOfStaking | 2023-06-22 00:04:02 UTC | #20

I like the idea of masking results until time has expired to offset voting based on momentum

-------------------------

sol | 2023-06-22 01:14:57 UTC | #21

[quote="SultanOfStaking, post:18, topic:129"]
penalization for pillars that do not vote.
[/quote]
[quote="sol, post:3, topic:129"]
Pillar yields or some other reward can be subject to a voting participation multiplier, but I think this point should be reserved for a separate discussion.
[/quote]
We can discuss it here if you want.
Suggestions:
- Negative: Yield **decay** increases with each missed vote
- Positive: Yield **growth** increases with each cast vote
or
- Negative: Vote weight **decays** with each missed vote
- Positive: Vote weight **grows** with each cast vote
[quote="SultanOfStaking, post:19, topic:129"]
Conviction voting
[/quote]
Interesting concept. I like how it can deter last-minute swing voting.


[quote="SultanOfStaking, post:20, topic:129"]
masking results until time has expired
[/quote]
I really like this and I think it's possible.

-------------------------

georgezgeorgez | 2023-06-22 02:02:23 UTC | #22

[quote="SultanOfStaking, post:19, topic:129"]
This is tough because the pillar tracker would suggest there are a handful of people with multiple pillars. Conviction voting could offset this but what is conviction based on? Delegated weight another option?
[/quote]
People with multiple pillars isn't really an issue to me.
Burn based voting is much more secure and long term aligned than delegation based voting.
Strict Delegation weight based voting gives exponential voting power which is the problem of single coin PoS networks.

The immediate goal of this thread is to come up with the design for the embedded governance contract, which is on-chain. But I think it is worthwhile to discuss the governance needs that can happen off-chain as well. At the very least to be explicit about what we aren't including.

We need ways for pillars to signal to each other off-chain, more options than just YES, NO, ABSTAIN
Stuff like, "I need more info", "good work, bad price", "prioritize this"

And we need ways for delegators to communicate with their pillars.

[quote="SultanOfStaking, post:20, topic:129, full:true"]
I like the idea of masking results until time has expired to offset voting based on momentum
[/quote]

By momentum I'm assuming you mean, just voting based how others are voting. I would agree that it seems most of our pillars are just doing this.

Preventing this is possible through a commit/reveal scheme.
It's a 2 round process
Instead of simply posting something like "proposal id, vote" on chain.
The first round you have to post "hash(proposal id, vote, random salt)" on chain. This is committing to your vote on chain without revealing it.
Then after that round is up, you post the unhashed vote data. People can verify that it matches what you posted in the first round.

It's possible, not everyone will reveal though. But in this case, you could just count the revealed votes.

In oracle systems, the goal is to collectively determine the value of something off-chain.
In a decentralized system, you have to incentive telling the truth.
So they do stuff like rewarding the participants who chose the most popular option.
The idea is that if the participants are decentralized enough, then they can't collude to make a false option the most chosen, so instead each participant will just choose the true value.
If a false option already has visible momentum however, then they might be incentived to choose the false option. So a commit/reveal scheme can be used.

For AZ though, there isn't an objective truth. It's subjective evaluation.

-------------------------

georgezgeorgez | 2023-06-22 02:06:10 UTC | #23

[quote="SultanOfStaking, post:19, topic:129"]
Conviction voting could offset this but what is conviction based on?
[/quote]

https://blog.giveth.io/conviction-voting-a-novel-continuous-decision-making-alternative-to-governance-aa746cfb9475

Is this what you are referring to by the way?

-------------------------

SultanOfStaking | 2023-06-22 02:20:13 UTC | #24

Thinking of Polkadot governance. Locking your coins with the vote- longer lock more weight.

-------------------------

sol | 2023-06-22 02:31:02 UTC | #25

[quote="georgezgeorgez, post:22, topic:129"]
It’s possible, not everyone will reveal though. But in this case, you could just count the revealed votes.
[/quote]

I was thinking of a different system involving ephemeral private keys.

- User submits a poll to the contract
- The contract generates a pubkey/privatekey pair for each poll and publishes the pubkey
- Poll participants submit encrypted votes
- While the poll is active, the contract can only reveal the number of participants
- When the poll is completed, the private key is revealed, allowing everyone to verify the votes

-------------------------

georgezgeorgez | 2023-06-22 03:03:05 UTC | #26

[quote="sol, post:25, topic:129"]
* The contract generates a pubkey/privatekey pair for each poll and publishes the pubkey
[/quote]

Can you elaborate on how this would work?

This sounds somewhat like Threshold Encryption, which can prevent MEV, but also momentum based voting.

A contract is not it its own entity. It's logic that runs all nodes. It can't generate/store a secret on its own. I'm guessing you could do something like, initiate a poll, then have the pillars construct a threshold multisig key for that poll. Then each submit their own contribution to the decryption.

-------------------------

georgezgeorgez | 2023-06-22 03:04:49 UTC | #27

https://docs.skale.network/technology/intro-threshold

-------------------------

sol | 2023-06-22 03:21:54 UTC | #28

[quote="georgezgeorgez, post:26, topic:129"]
It can’t generate/store a secret on its own.
[/quote]

I wasn't sure if it was possible, thanks for confirming.
A threshold scheme could work. 

I'm wondering if we should defer secret voting and adjusted incentives to a future iteration of the governance module.

-------------------------

georgezgeorgez | 2023-06-22 03:31:21 UTC | #29

[quote="sol, post:28, topic:129"]
I’m wondering if we should defer secret voting and adjusted incentives to a future iteration of the governance module.
[/quote]

Yeah definitely not a first iteration kind of thing haha.
First iteration, we really just need to be able to create/activate on our own, and then we can go as fast as we can build+educate the community and pillars.

-------------------------

georgezgeorgez | 2023-06-22 14:20:51 UTC | #30

Okay let's try and make some progress on an actual interface.

From `vm/embedded/definition/spork.go`, we can take the ABI


```
	jsonSpork = `
	[
		{"type":"function","name":"CreateSpork","inputs":[{"name":"name","type":"string"},{"name":"description","type":"string"}]},
		{"type":"function","name":"ActivateSpork","inputs":[{"name":"id","type":"hash"}]},

		{"type":"variable", "name":"sporkInfo", "inputs":[
			{"name":"id", "type":"hash"},
			{"name":"name", "type":"string"},
			{"name":"description", "type":"string"},
			{"name":"activated", "type": "bool"},
			{"name":"enforcementHeight", "type": "uint64"}
		]}
	]`
```
Let's use this as a starting point for possible ABIs.

For people who aren't familiar with this structure, **functions** determine the transactions that people can make to interact with the contract, and **variables** are mostly for deciding how data should be stored.

For read-only functions, there the RPC interface. We should design that too, but I think it's more straightforward and easier once the ABI is there.
There's also plasma requirements and of course the actual logic, but ABI is a good place to start imo.

From `vm/embedded/definition/accelerator.go` we can see that items that can be voted on have a status and some timestamps, which i'm guessing are used validate that votes are within voting period

```
		{"type":"variable","name":"project","inputs":[
			{"name":"id", "type":"hash"},
			{"name":"owner","type":"address"},
			{"name":"name","type":"string"},
			{"name":"description","type":"string"},
			{"name":"url","type":"string"},
			{"name":"znnFundsNeeded","type":"uint256"},
			{"name":"qsrFundsNeeded","type":"uint256"},
			{"name":"creationTimestamp","type":"int64"},
			{"name":"lastUpdateTimestamp","type":"int64"},
			{"name":"status","type":"uint8"},
			{"name":"phaseIds","type":"hash[]"}
		]},

		{"type":"variable","name":"phase","inputs":[
			{"name":"id", "type":"hash"},
			{"name":"projectId", "type":"hash"},
			{"name":"name","type":"string"},
			{"name":"description","type":"string"},
			{"name":"url","type":"string"},
			{"name":"znnFundsNeeded","type":"uint256"},
			{"name":"qsrFundsNeeded","type":"uint256"},
			{"name":"creationTimestamp","type":"int64"},
			{"name":"acceptedTimestamp","type":"int64"},
			{"name":"status","type":"uint8"}
		]}
```

So if we wanted to start with a very quick passthrough spork contract with pillar voting, it could look something like:

```
	jsonSpork = `
	[
		{"type":"function","name":"ProposeCreateSpork","inputs":[{"name":"name","type":"string"},{"name":"description","type":"string"}]},
		{"type":"function","name":"ProposeActivateSpork","inputs":[{"name":"id","type":"hash"}]},

		{"type":"variable", "name":"proposedSporkInfo", "inputs":[
			{"name":"id", "type":"hash"},
			{"name":"name", "type":"string"},
			{"name":"description", "type":"string"},
			{"name":"proposalTimestamp","type":"int64"},
			{"name":"creationTimestamp","type":"int64"},
			{"name":"activationTimestamp","type":"int64"},
			{"name":"lastUpdateTimestamp","type":"int64"},
			{"name":"status", "type": "uint8"},
		]}
	]`
```

`status` can be an enum, of Proposed, Created, Activated
Need to keep in mind that the id used for the ProposeActivateSpork function will be different that the Proposal Id which will be used for voting.
We might not need all of the timestamps, but just putting them there to start.

From `vm/embedded/definition/common.go`, we can take the common voting ABI

```
		{"type":"variable","name":"pillarVote","inputs":[
			{"name":"id","type":"hash"},
			{"name":"name","type":"string"},
			{"name":"vote","type":"uint8"}
		]},
		{"type":"variable","name":"votableHash","inputs":[
			{"name":"exists","type":"bool"}
		]},
		{"type":"variable","name":"pillarVote","inputs":[
			{"name":"id","type":"hash"},
			{"name":"name","type":"string"},
			{"name":"vote","type":"uint8"}
		]},
		{"type":"variable","name":"votableHash","inputs":[
			{"name":"exists","type":"bool"}
		]},
```

We should break down exactly how these work.
and we likely need Update functions to trigger vote tallying

```
		{"type":"function","name":"Update", "inputs":[]},
		{"type":"variable","name":"lastUpdate","inputs":[{"name":"height","type":"uint64"}]},
		{"type":"variable","name":"lastEpochUpdate","inputs":[{"name":"lastEpoch", "type": "int64"}]},
```

Please ask questions if any part of this doesn't make sense.
We need to work with our pillars who want to understand.

-------------------------

georgezgeorgez | 2023-06-22 14:28:59 UTC | #31

Oh I forgot to store the created spork's id
note the addition of spork id

```
	jsonSpork = `
	[
		{"type":"function","name":"ProposeCreateSpork","inputs":[{"name":"name","type":"string"},{"name":"description","type":"string"}]},
		{"type":"function","name":"ProposeActivateSpork","inputs":[{"name":"id","type":"hash"}]},

		{"type":"variable", "name":"proposedSporkInfo", "inputs":[
			{"name":"id", "type":"hash"},
			{"name":"sporkId", "type":"hash"},
			{"name":"name", "type":"string"},
			{"name":"description", "type":"string"},
			{"name":"proposalTimestamp","type":"int64"},
			{"name":"creationTimestamp","type":"int64"},
			{"name":"activationTimestamp","type":"int64"},
			{"name":"lastUpdateTimestamp","type":"int64"},
			{"name":"status", "type": "uint8"},
		]}
	]`
```

So this interface basically implements a state machine for proposedSporkInfo

I think it would be good to design what a transaction focused ABI would look like to compare

-------------------------

georgezgeorgez | 2023-06-22 15:33:00 UTC | #32

We could do something like

```
	jsonSpork = `
	[
		{"type":"function","name":"ProposeCreateSpork","inputs":[{"name":"name","type":"string"},{"name":"description","type":"string"}]},
		{"type":"function","name":"ProposeActivateSpork","inputs":[{"name":"id","type":"hash"}]},

		{"type":"variable", "name":"proposedTransactionInfo", "inputs":[
			{"name":"id", "type":"hash"},
			{"name":"address", "type":"address"},
			{"name":"tokenStandard", "type":"tokenStandard"},
			{"name":"amount", "type":"uint256"},
			{"name":"data", "type":"bytes"},
			{"name":"proposalTimestamp","type":"int64"},
			{"name":"lastUpdateTimestamp","type":"int64"},
			{"name":"status", "type": "uint8"},
		]}
	]`

+ Update Logic
+ Voting Logic
```

The ProposeCreateSpork and ProposeActivateSpork functions would fill out the ProposedTx fields

And the status might just be a boolean, to indicate if the tx has been sent or not

-------------------------

georgezgeorgez | 2023-06-22 15:06:50 UTC | #33

Storing Proposed Transactions gets us in the direction we want to go I think.
Could add another layer on top so that voting happens on a list of transactions.

And it leaves room to build out a generic templating system. So that Propose* -> proposedTransactionInfo mappings could be defined as on-chain data.

-------------------------

Chadass | 2023-06-22 16:48:54 UTC | #34

I'm not familiar with the process so my question might be odd but will it looks like:

1) Proposals are made on forums + GitHub then the vote signals opinions before a pull request is accepted on GitHub then merged before we all update?

Or

2) Proposals include the code that force an update to the variables, all happening onchain without spork and the GitHub process?

-------------------------

georgezgeorgez | 2023-06-22 18:20:15 UTC | #35

So there are a few things to keep in mind when it comes to protocol changes.
Nodes verify that that transactions are valid. When we change the protocol we change the definition of valid transactions.

Nodes need to be able to verify the entire chain, from start to end, for initial block download.
That means that the node software needs to keep around logic to validate transactions based on current and previous definitions of the protocol.

In the future there might be multiple clients for nom. Not just go-zenon.
For example, bitcoin has bitcoin-core and btcd, ethereum has geth and reth now.

No matter what the client is, they all have to activate the logic at the same time. Or else a fork will happen. So this is what the on-chain spork contract is for.

When you create a spork, all you do is get an ID. Then the node software maintainers can use that ID to put logic into the node that once that spork id is activated, to use the new logic.

Right now the spork contract is controlled by an address owned by the founding devs.
What we're doing right now is making it controlled by the community/pillars.

Not all protocol changes require new code though that has to be merged. If it's just changing a variable and not the logic that handles it. We're trying to design a governance contract that can (eventually) accommodate both.

-------------------------

aliencoder | 2023-06-22 21:17:20 UTC | #36

[quote="georgezgeorgez, post:35, topic:129"]
If it’s just changing a variable and not the logic that handles it
[/quote]

If you change a variable that is not identical in other nodes, the rest of the network will ignore (and drop your node/blacklist it) your change (eg changing Bitcoin's `maxSupply` variable).

-------------------------

georgezgeorgez | 2023-06-22 21:29:21 UTC | #37



[quote="georgezgeorgez, post:33, topic:129"]
Could add another layer on top so that voting happens on a list of transactions.
[/quote]

Just playing with some possibilities

```
	jsonSpork = `
	[
		{"type":"function","name":"TemplateCreateSpork","inputs":[{"name":"name","type":"string"},{"name":"description","type":"string"}]},
		{"type":"function","name":"TemplateActivateSpork","inputs":[{"name":"id","type":"hash"}]},

		{"type":"variable", "name":"templatedTransactionInfo", "inputs":[
			{"name":"id", "type":"hash"},
			{"name":"address", "type":"address"},
			{"name":"tokenStandard", "type":"tokenStandard"},
			{"name":"amount", "type":"uint256"},
			{"name":"data", "type":"bytes"},
		]},

		{"type":"function","name":"ProposeTransactions","inputs":[{"name":"txlist","type":"bytes"}]},

		{"type":"variable", "name":"proposalInfo", "inputs":[
			{"name":"id", "type":"hash"},
			{"name":"txlist", "type":"bytes"},
			{"name":"creationTimestamp","type":"int64"},
			{"name":"status","type":"uint8"},
		]},
+ Voting
+ Update

	]`
```
Two phase process
First call the relevant Template function and get a templated Tx info Id
Then call ProposeTransactions functions using the id
Pillar votes are on the list of txs

txlist just a list of hash ids appended to each other
we are start getting into the realm of custom abis

-------------------------

georgezgeorgez | 2023-06-22 21:31:36 UTC | #38

[quote="aliencoder, post:36, topic:129"]
If you change a variable that is not identical in other nodes, the rest of the network will ignore (and drop your node/blacklist it) your change (eg changing Bitcoin’s `maxSupply` variable).
[/quote]

Yeah which is why we would move certain variables out of the binary and into on-chain state where a change would have an activation height like a spork.

-------------------------

aliencoder | 2023-06-22 22:28:57 UTC | #39

[quote="georgezgeorgez, post:38, topic:129"]
move certain variables out of the binary and into on-chain state
[/quote]

Interesting idea. That applies only for mutable variables (non-constants)?

-------------------------

georgezgeorgez | 2023-06-22 22:51:01 UTC | #40

[quote="aliencoder, post:39, topic:129"]
That applies only for mutable variables (non-constants)
[/quote]

Could you give an example of what you mean by mutable vs constant?

I think there are items in both:
`https://github.com/zenon-network/go-zenon/blob/master/vm/constants/embedded.go`
`https://github.com/zenon-network/go-zenon/blob/master/vm/constants/plasma.go`
that could make to sense to be changeable via governance.

-------------------------

aliencoder | 2023-06-23 07:32:25 UTC | #41

[quote="georgezgeorgez, post:38, topic:129"]
Yeah which is why we would move certain variables out of the binary and into on-chain state where a change would have an activation height like a spork.
[/quote]

We already have [this](https://github.com/zenon-network/go-zenon/blob/73dd5b24f303e4d5cea2cf7b0321820363a131af/vm/embedded/embedded.go#L220) feature.

*If you move certain variables on-chain, you need to sync the chain first to read those variables. And I mean sync the entire chain first before processing it, because you need to be **sure** that you're not on a fork.*

Can you give me an example of on-chain variable vs binary hardcoded?

[quote="georgezgeorgez, post:40, topic:129"]
Could you give an example of what you mean by mutable vs constant?
[/quote]

Constant = "eternally" hardcoded constant values that appear in the codebase (another example is the `COINBASE_MATURITY` constant that is hardcoded to `100` - I [highly doubt it will ever change](https://bitcoin.stackexchange.com/questions/110085/why-coinbase-maturity-is-defined-to-be-100-and-not-50) to another value in the future)

Mutable = the Plasma example you showed earlier; they are marked as constants but in reality they should be mutable (for dynamic Plasma)

The [deployment status](https://github.com/bitcoin/bitcoin/blob/master/src/deploymentstatus.h) idea can be interesting, too.

-------------------------

georgezgeorgez | 2023-06-23 13:20:25 UTC | #42

It's hard to say what is eternally hardcoded for our network. We have design direction from Kaine that implies big changes, likely that will introduce new values and obsolete others.

[quote="aliencoder, post:41, topic:129"]
We already have [this](https://github.com/zenon-network/go-zenon/blob/73dd5b24f303e4d5cea2cf7b0321820363a131af/vm/embedded/embedded.go#L220) feature.
[/quote]

Sporks are flexible in that they can allow for any type of logic change. But the cost of this flexibility is the off-chain upgrade process and losing nodes that haven't upgraded when the spork is activated.

Once the dynamic on-chain variable subsystem is setup, changes to variables that have existing logic won't need changes to the binary. So there won't be any off-chain upgrade process required. The process will be entirely on-chain.

[quote="aliencoder, post:41, topic:129"]
*If you move certain variables on-chain, you need to sync the chain first to read those variables. And I mean sync the entire chain first before processing it, because you need to be **sure** that you’re not on a fork.*
[/quote]

This is true of verifying any on-chain data. You can't confirm any transaction unless you're synced to its height.

[quote="aliencoder, post:41, topic:129"]
Can you give me an example of on-chain variable vs binary hardcoded?
[/quote]

So what matters is backwards compatibility with the protocol.
Meaning, that all validators at any given height, agree on the set of valid and invalid transactions.

To the protocol, what data is stored in the code/binary (program's memory allocation at runtime) vs what data is stored locally on disk/level db is irrelevant. That's an implementation detail.

One thing we might want to change in the future is the emission rate.
*(Whether we actually want to is a different discussion)*
Right now emission rate is defined in the code/binary. We can change this with the spork process every time we want to change emissions, but it is cumbersome since each change requires adding new if/else logic to the binary in order to remain backwards compatible. And binary upgrades require the off-chain upgrade process.

What we can do instead is introduce a new system in the codebase to check the value of a dynamic variable at a given height it knows about. The current hardcoded values can be moved to genesis config to seed the associated database. We then modify the protocol for a new UpdateVariable contract method on the governance module which nodes see on-chain and use to modify the associated local database. Putting the initial config values in genesis would also allow testnets to use different values without requiring a patched binary.

-------------------------

0x3639 | 2023-06-23 18:02:11 UTC | #43

Should our Embedded Governance Design take into account the need for our project to be able to enter into agreements with 3rd parties in the real world.  For example, we need an apple developer account in order to [notarize](https://support.apple.com/guide/security/protecting-against-malware-sec469d47bd8/web) our macOS code.   

https://forum.zenon.org/t/publish-syrius-wallet-on-appstores/1481/31?u=0x3639

Should we form a Wyoming DAO LLC on behalf of the pillars so that entity can open an Apple Developer account?

Should the embedded governance contract include a voting mechanism to grant individual pillars the authority to take action on behalf of the DAO, like open an Apple Developer Account on behalf of an Organization?

If we do not consider this possibility, the burden could fall on individuals for critical infrastructure.

-------------------------

Chadass | 2023-06-23 18:31:49 UTC | #44

This is bounding us to U.S.A shchizophrenic regulators so why bothering. If Zenon succeed, they'll come after us all through your LLC. Don't make it easier for them. I'm not for this kind of risk. It's unnecessary, even if you're old self love regulators.

-------------------------

0x3639 | 2023-06-23 18:34:44 UTC | #45

Agree the US is not a good place to start this.  I'm not familiar with other international jurisdictions.  I did research Singapore yesterday and you need a local presence and director.  I'm assuming that will be the case with all of them.  

But maybe not the Bahamas or others.   Has anyone formed an international crypto entity without a local presence?

-------------------------

Chadass | 2023-06-23 18:35:30 UTC | #46

Why do we need a LLC to put a governance contract in place anyway?

-------------------------

0x3639 | 2023-06-23 18:59:24 UTC | #47

We need an LLC for the network.  Like to open an Apple Developer Account.  I'm proposing that this responsibility should not fall on an individual (like me).  I'm not even writing the code.  

So the only logical "organization" to do this assuming no individual wants that responsibility should (could) be the pillars.  Needing an LLC will continue to come up.  Each one of these app stores will want an LLC.  So the issue is not going away soon unfortunately.

-------------------------

Chadass | 2023-06-23 21:02:30 UTC | #48

Sure but don't bring all pillars into it. I'd, for exemple, wish to opt out.

-------------------------

aliencoder | 2023-06-24 07:32:18 UTC | #49

![](upload://imFHLfCkGCXyXAMfwrbec82omzj.png)

-------------------------

coinselor | 2023-06-25 02:51:34 UTC | #50

We can learn from others who had a similar issue:

https://forum.sushi.com/t/recommendation-for-sushi-legal-structure/11158

-------------------------

Chadass | 2023-06-25 04:28:17 UTC | #51

Or how to make it centralized

-------------------------

Bzed | 2023-06-25 14:28:04 UTC | #52

I guess from a high level it just seems so important to keep the whole model minimized and simple but obviously it's a tough balance with many variables and scenarios to account for. I also agree that the AZ model is a simple base for this process to build on, in particular if we are just going to focus on getting  community spork activation out the door asap.

So i'm clear, is there anything this model/process cannot do with respect to changing the codebase? The replies around constants sounds like there are no actual hard coded values in the code, is this a fair conclusion? If something is going to be eternally constant is that in reality purely up to the governance?

Gotta say I strongly agree with the idea of an incentivized design process as a step in the building. Rewarding those who make the effort to share their ideas and get feedback in public should negate some of the knee jerk reactions by the peanut gallery. There is clearly a need for more discussion, depending on the topic, so the amount of funding/motivation would reflect the magnitude and direction of the proposal. Then even without rewards, having a polling mechanism for community wide discussion could be valuable, maybe even be a job for sentinels.

Right now we reward the top 30 pillars heavily but there is no real feedback loop for the discussion on governance so I have to say that the model seems like an opportunity to have some signalling built in to show the views from other network actors.
For V1.0 would it be realistic for the embedded contract to include some function for polling other layers and/or participants of the network? Maybe it's a future iteration but it also seems like a strong step from day one to have some capability for this scalable/layered governance set up. George, is this one direction related to your comment expanding the model to other applications? The network is meant to scale in layers, though we are not there yet, it would be valuable imo to see the governance have some capability to match.

Another thing I was looking for clarity on is where/how the line is drawn for the guardians/admin functions. Bridge contracts, Liquidity contracts and future extension chains seem to need some flexible reaction times and ability to address edge cases, unlike the more deliberate process of a Spork Approval/Activation. I see with the Bridge Contract there are specific functions that the admin is able to call. Is this the way all embedded contracts will work?  Are these capabilities only ever predefined? Wondering about the odds of future capture of this admin role and what sort of vulnerabilities could be exposed through it. If we are setting up a multi sig address for this type of responsibility does it include an election process to decide the individuals to take this role? Is it as simple as a nomination and voting process every fixed time interval to keep things relevant? 

Basically, I have a respect for the QSR burn by pillar operators but also wonder about the role other participants in the network could offer on chain to add resilience or support to the decisions being made, maybe this is a focus for future iterations though. 

As far as the voting process goes, I will also add to the growing consensus that masked voting is an important step based on the way pillars have voted in the past. Next, thinking about voting parameters..

Thanks for the ongoing effort to include people in this work

-------------------------

Chadass | 2023-06-25 14:34:26 UTC | #53

Sentinels

-------------------------

georgezgeorgez | 2023-06-27 00:49:41 UTC | #54

Okay, so we have 1 week left for our timebox.
Let's try and put together a full spec for the embedded contract.

(I'll make a post later, just been a bit busy today)

-------------------------

georgezgeorgez | 2023-06-28 17:54:32 UTC | #55

So my goal is to have a system that can quickly fill our short terms needs while also providing enough of a framework to scale for future needs.

At a high level, I think we want to have a comprehensive and flexible Proposal datatype which can account for the nuances of governance. And we want our voting process to use the parameters of the Proposal regarding things such as vote duration, quorum, majority vs super-majority.

If we get that right, we can then iterate on the methods that can create proposals.
For the most flexible methods, we should have the most restrictive voting parameters.
But the governance system may want to allow itself more lenient voting for certain pre-approved items, which is where a templating system can be used.

For transactions we use the ABI for performance, but for low frequency items that require flexibility, a json data structure might be easier. In theory we could do this by defining new ABI, but not sure it's worth it.

So let's first start with a wrapper ABI to store our proposal json and some relevant fields for update/vote checking.

```
		{"type":"variable", "name":"proposalInfo", "inputs":[
			{"name":"id", "type":"hash"},
			{"name":"proposal", "type":"bytes"},
			{"name":"creationTimestamp","type":"int64"},
			{"name":"updatedTimestamp","type":"int64"},
			{"name":"status","type":"uint8"},
		]},
```

Let's then define a json schema for a Proposal datatype
We will have some fields for the voting parameters.
And another for the transactions to be sent.
We can come up with a json-schema later for client validation, but here's an example.

```
{
  "voteType" : 0,
  "voteParams" : {
    "duration": 14,
    "quorum": 0,
    "threshold": 50
  },
  "transactions": [
    {
      "address": "z1qxemdeddedxsp0rkxxxxxxxxxxxxxxxx956u48",
      "tokenStandard": "zts1znnxxxxxxxxxxxxx9z4ulx",
      "amount": "0",
      "data": "SporkCreationDataInBase64"
    },
    {
      "address": "z1qxemdeddedxg0vernancexxxxxxxxxxxvmwpcx",
      "tokenStandard": "zts1znnxxxxxxxxxxxxx9z4ulx",
      "amount": "0",
      "data": "UpdateVariableDataInBase64"
    }
  ]
}

```

This is actually pretty similar to the example payload that Sol explored.
His example supported dynamic constants and contract method calls as first class concepts.
His example also mixed voting params with dynamic variables.

I think we should separate out the voting parameters as that cannot be set by the proposer.
And we should treat transactions as the first class concept. It is much more flexible.
Contract methods are just used to render tx data, and dynamic constants can be done with a transaction interface.

In this example, we have a proposal for the embedded governance address send two transactions, one to the spork address, and another to itself. We need to understand the consequences of sending to itself, and the risks of recursion, so we may need to limit what can be sent to itself. Or we handle self sends with special internal logic instead of actually creating transactions.

Let's go over the different fields.

`transactions` is obvious.
An earlier post of mine describes a layer of indirection between rendered transactions and proposals.
That is really only useful to save bandwidth if rendered transactions are going to be reused. I think transaction templates will be reused, and these operations will be infrequent in either case.

`voteType` is used to signify which ruleset to use to evaluate if a proposal has passed.
For example, a `voteType` of `0` can be used to indicate pillar vote, and `voteType` of `1` could be used for single address admin vote.

Different `voteType`s have different `voteParam` requirements.
In the case of a pillar vote, we need the duration, threshold, and maybe quorum.
Quorum is a little strange because even with hidden votes, there are incentives to not vote to possibly prevent an otherwise successful vote from meeting quorum.

A quorum makes sense in systems where you need to gather enough voters into a session together to all vote at once. In a distributed system, it seems to make less sense. So I think we should allow a 0 value for no quorum.

One modification we should consider where quorum actually becomes useful is a layered voting system. Instead of:
```
  "voteType" : 0,
  "voteParams" : {
    "duration": 14,
    "quorum": 0,
    "threshold": 50
  },
```
We could do something like:
```
"governanceChain": [
  {
    "voteType" : 0,
    "voteParams" : {
      "duration": 14,
      "quorum": 33,
      "threshold": 50
    },
  {
    "voteType" : 1,
    "voteParams" : {
      "duration": 7,
      "address": "z1qpxswrfnlll355wrx868xh58j7e2gu2n2u5czv"
    },
]

```

For each sequence in the governance chain, there are 3 outcomes, PASS, FAIL, INVALID
If the sequence is INVALID, it initiates the next vote type in the sequence.
What this system doesn't capture is the possibility for parallel voting, but not sure if we want that.

In the above example, there would first be a pillar vote for 2 weeks. If it reached quorum of >33% of pillars, that result would count. If it didn't reach the quorum it would then move to an admin vote by a single address.

Okay now that we have our flexible proposal datatype which can be voted on, we need a way to create these. Let's first start with simplest ones.

```
		{"type":"function","name":"ProposeTransaction","inputs":[
			{"name":"address", "type":"address"},
			{"name":"tokenStandard", "type":"tokenStandard"},
			{"name":"amount", "type":"uint256"},
			{"name":"data", "type":"bytes"},
		]}
		{"type":"function","name":"ProposeTransactions","inputs":[
			{"name":"txs", "type":"bytes"},
		]}
```

`ProposeTransaction` is simpler and somewhat redundant if `ProposeTransactions` (plural) exists.
Both methods would create a proposalInfo variable, with a hardcoded governance chain and the relevant tx(s) in the transaction list. In the case of `ProposeTransactions`, the `txs` field would directly map to the `transactions` field of the proposal data.

To actually make this contract work of course as before we need the actual methods for voting, updating, and probably a way to fund/donate fund the contract as well.

In terms of scaling and allowing for ohter governanceChains, in the future we can have other methods such as, ProposeTemplate, ProposeTemplateDeletion, ProposeRenderedTemplates

ProposeTemplate and ProposeTemplate deletion would be meta-proposals that use a strict (e.g supermajority) vote to allow for different/more flexible governance chains for certain types of proposed transactions.

Ideas such as Sol's spam prevention mechanism can be added as well, but that is just another instance of FAIL outcome with different rules.

-------------------------

georgezgeorgez | 2023-06-28 17:58:51 UTC | #56

So for example if you called the `ProposeTransaction` method with the following parameters

```
      "address": "z1qxemdeddedxsp0rkxxxxxxxxxxxxxxxx956u48",
      "tokenStandard": "zts1znnxxxxxxxxxxxxx9z4ulx",
      "amount": "0",
      "data": "SporkCreationDataInBase64"
```

And our default governance chain was 
```
"governanceChain": [
  {
    "voteType" : 0,
    "voteParams" : {
      "duration": 14,
      "quorum": 33,
      "threshold": 50
    },
  {
    "voteType" : 1,
    "voteParams" : {
      "duration": 7,
      "address": "z1qpxswrfnlll355wrx868xh58j7e2gu2n2u5czv"
    },
]
```

It would create a `proposalInfo` variable in database state
where the `proposal` field would be
```
{
"governanceChain": [
  {
    "voteType" : 0,
    "voteParams" : {
      "duration": 14,
      "quorum": 33,
      "threshold": 50
    },
  {
    "voteType" : 1,
    "voteParams" : {
      "duration": 7,
      "address": "z1qpxswrfnlll355wrx868xh58j7e2gu2n2u5czv"
    },
],
"transactions": [
    {
      "address": "z1qxemdeddedxsp0rkxxxxxxxxxxxxxxxx956u48",
      "tokenStandard": "zts1znnxxxxxxxxxxxxx9z4ulx",
      "amount": "0",
      "data": "SporkCreationDataInBase64"
    }
]
```

-------------------------

georgezgeorgez | 2023-06-28 18:28:25 UTC | #57

I don't think it's a good idea to connect any sort of legal entity to the network as a whole.
Having a legal entity doesn't remove the burden on individuals. Someone still has to keep it in compliance.

The best way to handle this is through AZ.
We can provide incentives to community members and teams who take on this risk.

-------------------------

georgezgeorgez | 2023-06-28 18:33:21 UTC | #58

Having some sort of legal structure for HyperCore.One is something I'm still thinking about.

The free and open source licenses should give us some level of protection when it comes to the codebase. But exactly for the purposes of publishing apps on gated ecosystems, we should consider it.

However, I think that is out of scope for the embedded governance design which is mainly about on-chain authority. Any generic polling mechanism could be used to signal "off-chain" authority. But it's meaningless unless it's recognized.

-------------------------

0x3639 | 2023-06-28 18:53:50 UTC | #59

Agree.  This was a bad idea.

-------------------------

georgezgeorgez | 2023-06-28 19:02:16 UTC | #60

[quote="Bzed, post:52, topic:129"]
I guess from a high level it just seems so important to keep the whole model minimized and simple but obviously it’s a tough balance with many variables and scenarios to account for.
[/quote]

My goal is to have something shippable by end of July which covers our initial simple use cases.
I don't want to get into proposals yet though until the design phase is over.

[quote="Bzed, post:52, topic:129"]
So i’m clear, is there anything this model/process cannot do with respect to changing the codebase?
[/quote]
Hmm so the spork creation/activation process is about changes to the consensus protocol. This protocol sits on top of other protocols such as the p2p communication protocol. Mr Kaine has mentioned a switch to libp2p, but this isn't really something related to consensus. I think the way to handle this would be to have a transition phase where nodes are broadcasting to the old p2p network and the new p2p network.

In terms of consensus, I think the spork process is very flexible.
Consensus is just about what txs are valid/invalid. Individuals node can do whatever they want locally as long they set of valid transactions stay the same.
So changes to stuff like internal database and rpc, don't really need a spork.

[quote="Bzed, post:52, topic:129"]
Gotta say I strongly agree with the idea of an incentivized design process as a step in the building. Rewarding those who make the effort to share their ideas and get feedback in public should negate some of the knee jerk reactions by the peanut gallery.
[/quote]

Hopefully the community finds it valuable as well.
If not, I will just do this exercise internally for HyperCore.One proposals as part of our own implementations. And the costs will be bundled into a larger proposal.
It's actually more of a competitive advantage at this stage if I do that and I don't think I will design for free anymore.
But I want the best result for our community and am willing to try and create collaboration and competition where appropriate even if it's against myself.

[quote="Bzed, post:52, topic:129"]
Right now we reward the top 30 pillars heavily but there is no real feedback loop for the discussion on governance so I have to say that the model seems like an opportunity to have some signalling built in to show the views from other network actors.
[/quote]

My personal view is that for an efficient L1, polls that do nothing but signal don't really belong. We're using AZ for that purpose right now but it's not the best tool for the job. We need a strong ecosystem of off-chain communication. (I maybe have some work related to this in progress.)
But the extension chain conversation makes this harder to judge. 

[quote="Bzed, post:52, topic:129"]
The network is meant to scale in layers, though we are not there yet, it would be valuable imo to see the governance have some capability to match.
[/quote]

If we have extension chains, then polls that only signal on L1, might have very strong consequences on higher layers if there is a tight integration (e.g chain relay)

[quote="Bzed, post:52, topic:129"]
Another thing I was looking for clarity on is where/how the line is drawn for the guardians/admin functions. Bridge contracts, Liquidity contracts and future extension chains seem to need some flexible reaction times and ability to address edge cases, unlike the more deliberate process of a Spork Approval/Activation.
[/quote]

The design I posted above goes into layered voting.
But what you are describing is more like parallel voting, separation of powers, checks and balances. In my design all that logic could be built into a new voteType, but having a way to define building blocks and compose them might be nice.

[quote="Bzed, post:52, topic:129"]
Basically, I have a respect for the QSR burn by pillar operators but also wonder about the role other participants in the network could offer on chain to add resilience or support to the decisions being made, maybe this is a focus for future iterations though.
[/quote]

In terms of pure pure of stake weight vs pillar burn, this is similar in my view to states' rights vs direct democracy in irl. The way we balance it right now is by having momentum production based on delegation while votes based on burn.
In term of other participants such as sentinels, if they are a core part of network resilience, then they definitely need to have an influence. What that influence should look like, I'm not sure.
In terms of my design above, maybe we need a future voteType that requires a pillar and sentinel vote to both pass.

[quote="Bzed, post:52, topic:129"]
As far as the voting process goes, I will also add to the growing consensus that masked voting is an important step based on the way pillars have voted in the past. Next, thinking about voting parameters…
[/quote]

I'm not sure if we need to handle masked voting specifically for governance or if we can handle it generically for the entire network with threshhold encryption. Governance is not the only area where we'll want this capability.

-------------------------

georgezgeorgez | 2023-06-28 19:03:20 UTC | #61

But an important discussion nonetheless.
We should be comfortable with just sharing any idea and talking it through.

-------------------------

sol | 2023-06-30 01:25:29 UTC | #62

I agree with your suggestions so far. 
I wanted to suggest something similar to your transactions idea.

[quote="georgezgeorgez, post:55, topic:129"]
```
 "transactions": [
    {
      "address": "z1qxemdeddedxsp0rkxxxxxxxxxxxxxxxx956u48",
      ...
      "data": "SporkCreationDataInBase64"
    },
    {
      "address": "z1qxemdeddedxg0vernancexxxxxxxxxxxvmwpcx",
      ...
      "data": "UpdateVariableDataInBase64"
    }
  ]
```
[/quote]

[quote="georgezgeorgez, post:15, topic:129"]
[quote="sol, post:3, topic:129"]
Seems like we also need to pass the ABI for the specific method we’re calling.
Perhaps we can rely on clients to pre-format these `data` values?
[/quote]

For simple passthrough voting, the governance contract likely does not even need to interpret the data at all. It will just store the bytes and use it when it makes then downstream tx. It can be interpreted client side for UI purposes.
[/quote]

If I'm reading this correctly, it sounds like you're expecting clients to format transaction inputs (arbitrary data -> specific contract ABI -> b64 -> gov contract) correctly. 
I disagree with this approach -- we cannot trust a client to pass valid data to the governance contract. 
Imagine completing a poll only to discover that the data wasn't formatted correctly and the transaction was refused downstream by the next contract.

I was going to propose that the governance contract unpacks these values and does some input validation. If it fails, at least we don't need to wait `duration` time to discover a mistake.
Maybe you already accounted for this. Is it a non-issue?

-----------------

I had not considered parallel voting. What if we permitted this but constrained polls to unique transaction types/functions?
Example: cannot submit a poll to create a second spork while one is still being voted on.

-------------------------

georgezgeorgez | 2023-06-30 16:06:07 UTC | #63

[quote="sol, post:62, topic:129"]
If I’m reading this correctly, it sounds like you’re expecting clients to format transaction inputs (arbitrary data → specific contract ABI → b64 → gov contract) correctly.
I disagree with this approach – we cannot trust a client to pass valid data to the governance contract.
Imagine completing a poll only to discover that the data wasn’t formatted correctly and the transaction was refused downstream by the next contract.

I was going to propose that the governance contract unpacks these values and does some input validation. If it fails, at least we don’t need to wait `duration` time to discover a mistake.
Maybe you already accounted for this. Is it a non-issue?
[/quote]

Seems like client vs server side validation
Where here the client itself is another smart contract.

The `ProposeTransaction` method I suggested is meant to handle our initial use case but also provide something extremely flexible to handle any possible situation with strict voting. You are right that it doesn't do any validation, so the data could be bogus. I am relying a bit on off-chain verification before voting. Don't vote on what you don't understand (or what your client can't process).

I remember when we tested sending an htlc to an embedded smart contract, and then proxy unlocking it. It failed and the htlc entry still existed. I'm guessing it would be a similar result if a poll with bogus data succeeded.

In terms of adding verification:
I mainly want to avoid having to modify the governance contract itself every time we have new embedded functionality. Some validation can be done on-chain through a templating system. But I think it would only go so far as ABI validation. I don't think we want to duplicate logic for constraints on the client side.

I'll make a post later about what that could look like.

Also need to start digging into the actual voting/update functionality.
I think next few days, will start writing pseudocode for all the methods.

-------------------------

georgezgeorgez | 2023-06-30 16:31:25 UTC | #64

[quote="sol, post:62, topic:129"]
I had not considered parallel voting. What if we permitted this but constrained polls to unique transaction types/functions?
[/quote]

Well I think polls can be voted on independently.
Each will have it's own ID that will be referenced like with AZ.
I don't see an issue with multiple sporks being voted on at the same time.

By parallel voting I mean, that for a particular issue, there are parallel paths to resolution.
Basically a logical OR.
But a logical AND could be useful as well.

My governanceChain idea is mostly about what happens if a voteType fails to resolve.
But within a single vote type, maybe we want to say:
"This will pass if 2/3 of pillars AND 2/3 of sentinels vote YES."
or maybe
"This will pass if either Group A votes for it OR Group B votes for it"
which could model some of the admin vs guardian safety measures where we don't want to wait for one group to either act or not, before allowing another group to.

Ideally we could have some config that composes together these building blocks.
maybe a future voteType 2, could be a meta vote type where the voteParam takes in a flexible config of building block voteTypes

again my goal is to have something that takes care of us now, while being designed in a way that it doesn't have to be torn down in the future if we do have more complex needs

-------------------------

sumamu | 2023-06-30 20:05:10 UTC | #65

Please wait for me. I've been busy with the affiliate program, but I've got some ideas to share about the governance module.

A lot of interesting concepts have been shared around, however they are too complex.

The governance module should be a simple AZ fork with some minor changes and that's it. Easy to implement and already battle-tested. 

Any other option will require a ton of unit-tests and manual testing. Not to mention development.

I'm speaking from experience when I say new embedded designs require a LOT of work.

Don't make that mistake.

-------------------------

georgezgeorgez | 2023-06-30 20:43:37 UTC | #66

The purpose right now is to explore the design space as much as we can within our timebox ending July 4.
What are all the different high level approaches and the trade-offs for them?

What actually gets implemented is up to proposers.
Development complexity is certainly a trade-off to consider.

We've already considered what a simple pass-through implementation could look like.
The trade-off with that is it means all future admin functionality will require additional work on the governance embedded.
I don't think it's going to be as simple as implementing sporks, bridge, and liquidity admin functions and then the problem is solved.

The requirements for governance are also more complex than AZ. What if we have to quickly spork for a critical bug fix? Remember that a spork that gets activated without implementation halts the network.
We also see possible issues with the existing mechanism of AZ. E.g notably that there are incentives to simply not vote at times. And there are some discussion to change how AZ works.

I agree there are more urgent things than accounting for all these nuances right now.
But I think maybe we can create an iterative path or approach that can quickly fit out immediate needs, but that also leaves enough of an interface for us to grow without having to rip out the old system.

My personal goal is to have something shippable by end of July.
**But I will consult the pillars about what they want.**

My own experience with developing embedded contracts is that once the requirements are clear, implementing them is just busy work and a matter of time spent.

If we take a very simple approach right now and kick a more sophisticated approach down the road, maybe doing them as separate embedded would make sense, if the underlying mechanisms are not compatible.

-------------------------

georgezgeorgez | 2023-06-30 21:16:37 UTC | #67

As part of this design phase, I'll whip up a simple implementation this weekend.
Will be a good exercise for me to better understand the voting / update mechanism.

If people think it's enough, then anyone can propose to productionalize it.
Or it can serve as a base for something more sophisticated if we want to go that direction.

-------------------------

georgezgeorgez | 2023-06-30 21:38:09 UTC | #68

@sol btw
https://github.com/zenon-network/go-zenon/blame/master/vm/embedded/definition/common.go#L23

There is already a VoteNotValid vote type

edit: oh but it seems just to be used for error handling

-------------------------

georgezgeorgez | 2023-06-30 21:49:37 UTC | #69

And also I forgot that we can use stuff like "hash[]" as the type for ABI
Can use that to limit or eliminate our need for flexible json
better to vaildate with the abi than with json-schema if we can

-------------------------

sol | 2023-06-30 22:05:18 UTC | #70

Can we use [GetEmbeddedMethod](https://github.com/zenon-network/go-zenon/blob/master/vm/embedded/embedded.go#L213)?

-------------------------

aliencoder | 2023-07-01 19:54:31 UTC | #71

[quote="sumamu, post:65, topic:129"]
Please wait for me.
[/quote]

And for me. Been busy with other dev stuff. I will review the discussion on Monday and share my thoughts about the `governance` embedded.

-------------------------

georgezgeorgez | 2023-07-01 20:18:15 UTC | #72

How about we push the discussion timebox out a week ending July 10?

-------------------------

georgezgeorgez | 2023-07-01 22:37:52 UTC | #73

Making good progress on the PoC
Will have something to show tomorrow or day after

-------------------------

sumamu | 2023-07-03 10:22:47 UTC | #74

[quote="georgezgeorgez, post:72, topic:129, full:true"]
How about we push the discussion timebox out a week ending July 10?
[/quote]

I love this!

-------------------------

georgezgeorgez | 2023-07-05 15:31:11 UTC | #75

[quote="georgezgeorgez, post:73, topic:129"]
Will have something to show tomorrow or day after
[/quote]

Didn't touch my computer for the last two days (wasn't feeling great lol) so still need to finish up.

But as I've been doing my PoC, I'm thinking about a great point @coinselor brought up:

[quote="coinselor, post:5, topic:129"]
2. **Delay Period:** We should consider implementing a delay period between when a proposal is accepted and when the changes are implemented. I think this should be different than the time until the activation height. The benefits of this delay would include:
[/quote]

One design consideration is that different type of governance actions have different delay needs. Spork Creation likely does not need any delay after the voting period. But Spork Activation definitely needs one as people who voted NO have to decide whether to upgrade or fork out.

My PoC uses a similar mechanism to AZ, but one thing that AZ does is during contract updates, it sends transactions without a delay period. To account for this, there needs to be another status type, where the Vote has succeeded, but the transactions still need to be sent.

-------------------------

sumamu | 2023-07-11 14:00:39 UTC | #76

I still haven't gotten to this, yet, so I'm just going to share some thoughts here:
- pillars produce the momentums, so in case of a spork activation, we'd still need most of them to run the new binary
- contrary to the popular belief in the community that pillars are not active, may I point out that pillars have a very high uptime and more than 50% of them managed to run the orchestrator in ~1 week


The governance module should be both simple and versatile
- it's primary purpose should to activate sporks
- secondary purposes to govern any embeddeds

It can achieve that by simply publishing an AccountTemplate that is included in the proposal.

Changing variables and other values in the network should not be included in the governance embedded, but a separate embedded which is governed by it.

-------------------------

Bzed | 2023-07-15 15:50:05 UTC | #77

[quote="sumamu, post:76, topic:129"]
Changing variables and other values in the network should not be included in the governance embedded, but a separate embedded which is governed by it.
[/quote]

May i ask what is the motivation to add a seperate embedded for changing a constant to a variable?

-------------------------

sumamu | 2023-07-15 17:21:04 UTC | #78

The responsibilities of the governance module should be kept to a minimum. Having a separate embedded contract for changing the network settings helps us keep the governance module simple and it also means we can focus on delivering it faster, since we can do the network settings embedded later.

At the moment, the governance module is mainly needed for:
- activating sporks
- governing the Orbital
- governing the Bridge

-------------------------

coinselor | 2023-07-25 19:21:03 UTC | #79

I would love for more than one (George) dev to drop their version of the embedded governance contract, especially if it's only pseudocode. I'm sure we have more than one capable dev, and this is a critical infrastructure for the network.

Sure, we can wait for George to drop his version, and improve upon it together. However, I believe having two or more separate concept versions would make the final results a lot better.

Remember that George is advocating for more flexibility down the line, while others like sumamu prefer a strictly minimal implementation for the first iteration.

-------------------------

sumamu | 2023-07-28 11:54:27 UTC | #80

How's it going so far? I'm willing to follow along if the code's public on GH.

There are lots of things to do for this ecosystem, so resources should be used efficiently. 

Having more devs work on the same thing means they're not working on other stuff.

-------------------------

georgezgeorgez | 2023-08-01 17:21:09 UTC | #81

zoonish

-------------------------

sumamu | 2023-08-02 18:36:33 UTC | #82

bullish

-------------------------

aliencoder | 2023-09-13 08:08:11 UTC | #83

Ping.

-------------------------

georgezgeorgez | 2023-09-20 23:26:01 UTC | #84

I like to walk away and forget about the work and then come back to it.
It's undergoing a refactor for readability/maintainability now. Turning spaghetti into production ready.
Most pulling things into separate functions/interfaces so that the top level update function is easy to follow.

-------------------------

