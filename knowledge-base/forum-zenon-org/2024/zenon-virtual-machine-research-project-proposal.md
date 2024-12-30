Thread: zenon-virtual-machine-research-project-proposal
Jeron | 2022-05-12 21:45:19 UTC | #1

This details our (@Jeron, @Dumeril) proposal and application to Accelerator-Z for a funded research initiative to lay the groundwork of a virtual machine implementation for NoM to enable use of smart contacts on the network (beyond the current but limited embedded functionality).

## Motivation

Prevailing feedback on our initial announcement (https://forum2.zenon.org/t/implementing-a-smart-contract-runtime-on-nom/462) regarding this proposal was positive, but also cautious, in saying that inclusion of members from the core team would be good or even necessary.

As a thought exercise, let’s consider the worst case:

* Mr. Kaine and the core team consider their work complete, the community strong enough to build on the existing code. With a bit of luck MK drops in once in a while to stimulate ideas or directions. We are now a community-only project.

While this may or may not be true, we should be prepared for this and plan accordingly. We can die a slow death as a bsc shittoken, or we can try and move forward, building on the solid but incomplete base of a feeless L1, that we inherited.

Every bit of support, cooperation or ongoing work from Mr. Kaine or the team is an obvious positive. However, in our opinion, in our own best interest, we should assume the worst and hope for the best. We will continually try to mobilize better interaction between the community and core team.

That’s the proposition on which we formulate the present proposal.

In the initial and current phase of Accelerator-Z, Hyperspace, interoperability is a main focus. There are several ways to achieve interoperability, but few that do it are trustless.

Smart contracts would greatly improve our options for trustless bridges but would also open countless possibilities to drive adoption and build upon our feeless base layer in the form of decentralized ZApps.

To support creation of smart contracts, we require a virtual machine, a built-in execution environment for external code.

As already described and discussed in our first announcement of this proposal, we see this as a multiple-stage initiative. This proposal is about the first three stages - research and analysis.

## Project Phases

These initial and preparatory stages are probably the most important. They won’t enable smart contract facilities yet, there will (probably) be no code, but it will allow the community to make an informed decision about the available technological options, make a qualified suggestion and hopefully describe a possible path to its realization. We’ll work on Phases I and II simultaneously, so the order is not important here. Phase III builds upon the results of the preceding phases.

During all phases, we commit to actively seek feedback from the core team and transparently include potential interactions and their results in the reports. Additionally, we will aim to make our ongoing progress available to the community and seek discussions whenever possible.

We acknowledge that at this early stage we might not even fully appreciate the required work, scope and output of these initial phases, so their definition might be subject to change. This obviously is especially true for the third phase.

For all phases, we aim to provide high quality and easily digestible information that will make our research results available to everyone interested in the inner workings of NoM and the landscape of virtual machine technologies.

### Phase I: Internal analysis

This phase will include an assessment of the current NoM design, the current embedded SCs and how consensus is reached, potential anchor points for the runtime and a generalized approach for how to implement a runtime on NoM.

Deliverables are:

* An architectural overview of NoM as it exists currently;
* A description of embedded smart contract implementations, their integrations with the consensus layer and their limitations;
* An overview of the transactional model and data storage facilities of NoM;
* Initial analysis and potentially early ideas about connection points and data flow mechanics between NoM and a VM extension.

### Phase II: External Analysis

This phase will be an assessment of available runtimes, including WASM, with a discussion of pros/cons with respect to performance, security, flexibility etc. and a recommendation on which runtime to implement.

Deliverables are:

* A detailed list of existing and prominent runtimes, their characteristics, limitations, fields of application and requirements on the base layer.
* An extended list of runtimes we choose to not integrate into our research and why.
* A detailed and justified recommendation on which runtime to implement.
* If applicable, an overview of limitations of our solution wrt other solutions.

Positive voting results on this phase would mean that the community supports our choice.

### Phase III: Implementation Proposal

With this phase we build on the preceding phases to generate a more detailed architectural overview for implementation, showing how the vm would fit into the code, how and where it would interact with the existing structures, information flow, storage.

Deliverables are vague as of yet, as we require the output from Phases I and II:

* An updated architectural overview of NoM, that would now include the vm.
* Descriptions of data flow between vm and consensus layer.
* An early draft of an instruction set supported by the proposed vm.
* Early analysis and suggestions on how guarantees on smart contract execution limitations might be implemented (halting guarantees, contract spam prevention etc.). A fee model?
* Possibly some test implementations in a network fork as a very early poc. This would require availability of a testnet.
* An estimate on the required man hours needed for implementation.
* A summary and analysis of the completed research, what we missed, the problems we identified etc.

## Estimated duration

We think this early stage is vital and should not be rushed, as it not only builds the knowledge required for implementation of a vm, but also serves to inform and educate the community about the existing network. To do it properly, we estimate that each phase will take at least 5-7 days of full-time work for each of us (ie 10-14 days total), with Phase III possibly taking longer. As we both have full-time jobs already, we can only work on it sporadically, so completion of all phases will require some time. We hope to get it done in 3 months.

## Funding

We ask for the maximum amount of 5k ZNN and 50k QSR. As already stated, we don’t do this for the money. However, it’s important that a project like this is not underestimated in its scope and importance. While we want to provide value and further the development of our ecosystem, we also want the community to value research tasks like this accordingly.

To work our way out of this dilemma, we ask for funding that hopefully remains realistic for the time estimate given above. We’ll need that time and make sure to put it in. It’s possible that it will take longer; in that case we’ll work for free to generate the expected results.

We will publicly disclose the addresses receiving the funds, where each payment of ZNN will be locked in when received, for one year of staking. Each month, the accumulated staking rewards will flow back to the community or the project in some manner. At this point we are considering channeling the QSR back to the AZ public donation address, but we may come up with other ideas to benefit the community. Details will be announced in time.

One thing we discussed is the possibility that smart contract usage should probably require gas (as described in the whitepaper); the QSR could then potentially be used to grant the community a period of subsidized SC usage to bootstrap SC activity.

In summary:

* We’ll ask for 1.5k ZNN and 15k QSR each for both Phase I and II (3K ZNN and 30K QSR total).
* The remainder of 2K ZNN / 20k QSR will be requested upon completion of Phase III.

-------------------------

romeo | 2022-05-12 22:56:40 UTC | #2

This is an essential piece of work IMO - and I hope it gets voted in without issue.

Don't get caught up in the fact its a max funding ask - it's well worth the investment for the future of the network. I'm keen to see the output of Phase 1, particularly the architectural oversights.

I assume you will also be able to onboard new participants to the proposal as it moves along?

-------------------------

0x3639 | 2022-05-13 01:32:34 UTC | #3

I’m in 100% support.  I will vote yes tomorrow when I return from travels. Thank you guys for taking the time to think through this very carefully and propose a well thought out proposal.

-------------------------

cryptocheshire | 2022-05-13 04:03:34 UTC | #4

Great and important initiative, thank you @Jeron and @Dumeril !

-------------------------

Dumeril | 2022-05-13 04:30:25 UTC | #5

Thank you and yes. Initially we hoped to assemble a team of ~4 before we make that proposal. But we figured we can as well just begin right away.
We haven’t thought about the exact way to do it yet, but we hope to have output throughout the phases that can maybe spark discussions or feedback from the team or interest others to join us.

-------------------------

Ppaesch | 2022-05-13 07:45:38 UTC | #6

Phase I alone is incredible valuable in terms of supporting future devs which may join this network.

-------------------------

DrD3 | 2022-05-13 07:53:38 UTC | #7

I really believe Mr. Kaine & Co., if they read through the forum, are smiling as their dream of the community taking ownership of developing the network becomes reality. This project definitely play a pivotal role in providing an overarching understanding of NOM's current architecture (which is priceless imo) kinda acting as a spiritual successor to the White Paper.

Really hope we can get feedback from Mr. Kaine and the Core Team and get SCs enabled asap

-------------------------

dat_she_pepe | 2022-05-13 22:51:46 UTC | #8

I will vote for that.

-------------------------

vopo111 | 2022-05-17 04:18:05 UTC | #9

I  vote "YES" for this. Hope this help.
Thank you.

-------------------------

