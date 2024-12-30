Title: ZIP:deeZNNutz-0001 Final

URL Source: https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print

Published Time: 2024-03-27T15:20:14+00:00

Markdown Content:
September 8, 2022, 12:15pm  1

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#abstract-1)Abstract
-----------------------------------------------------------------------------------

Inspired by [Laanwj’s thoughts on decentralized Bitcoin core code maintenance and distribution](https://laanwj.github.io/2021/01/21/decentralize.html), we are proposing a web of BIPs hosted by Pillars - the main validator nodes of the Zenon Network of Momentum.

Any Pillar can sponsor and host BIPs that should conform to certain standards. Unlike Bitcoin’s BIP Standard which gives that authority to one central entity, we are proposing to decentralize that central authority to every Pillar that wants to engage. And that web of BIPs is the Zenon Improvement Proposal - ZIP - process.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#motivation-2)Motivation
---------------------------------------------------------------------------------------

Prior to this initiative,

*   An AZ Project to research and present a ZIP process was submitted to the community.
*   That work was completed and presented to the community for input.
*   The process was iterated and presented to the Pillars for a vote.
*   The [Proposed ZIP Process](https://forum2.zenon.org/t/proposal-az-submission-of-first-zip-to-validate-process/925) was approved with 26 yes votes and the community asked Mr. Kaine to setup a ZIP repo in the Official Zenon Network repository. He was unresponsive.

We can only assume Mr. Kaine and his team

*   want the community to own and manage the ZIP process independently
*   want a ZIP format, but not to host the ZIP repo and/or provide centralized editor services

As a result, various community members iteratively developed this new ZIP framework which

*   does not rely on the Founding Team in any way
*   replaces most of the central editor role with decentralized Pillar ZIP sponsorships
*   proposes Spork creation and activation through the AZ address to activate protocol changes, as suggested by the founding developers.

With that background, we propose a more fault-tolerant and decentralized ZIP Process.\*\*

* * *

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#what-is-a-zip-3)What is a ZIP?
----------------------------------------------------------------------------------------------

A Zenon Improvement Proposal (ZIP) is a design document that intends to provide information and justification for a proposed change or improvement to the Network of Momentum (NoM). A ZIP should provide a clear and concise technical specification of the change or feature.

The ZIP process is the primary mechanism for proposing new features, collecting community input or consensus on an issue, and for documenting the design decisions that have gone into the development and growth of the Zenon Network. This document formalizes the standard ZIP process.

* * *

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#zip-principles-4)ZIP Principles
-----------------------------------------------------------------------------------------------

*   ZIPs should not rely on any central editor or repository
*   Indexing of ZIPs should be fault tolerant
*   The ZIP process should be flexible enough to allow for continuous improvement
*   ZIPs should aim to improve the Zenon Network of Momentum in line with its core principle of progressive decentralization

* * *

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#zip-types-5)ZIP Types
-------------------------------------------------------------------------------------

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#informational-zips-6)Informational ZIPs

*   describe procedural guidelines to the Zenon community, e.g. how to write and activate a ZIP (e.g. this ZIP:deeZNNutz-0001)
*   propose a behavioral protocol (or change of such) but do not affect the technical protocol
*   constitute best practices used by the community

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#implementation-zips-7)Implementation ZIPs

*   describe a change in a protocol implementation
*   do not propose a protocol change
*   are done to improve node efficiency or to extend supported programming languages
*   do not require consensus to activate - any node can adopt the proposed change (or not)

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#soft-forks-8)Soft Forks

*   describe backward-compatible network changes
*   require a majority (\>50%) of Pillars to enforce the new rules
*   non-upgrading Pillars will not be forked out but Momentums violating new rules may become invalid
*   do not require any nodes to upgrade to maintain consensus, since all Momentums with the new soft forked-in rules also follow the old rules

> **Spork Creation Threshold (= Pillar Acceptance Vote)**
> 
> *   Pillar Majority (\>50%)
> *   Timeout: 4 weeks after voting begins

> **Spork Activation Threshold (= Pillar Activation Vote)**
> 
> *   Pillar Majority (\>50%)
> *   Timeout: 4 weeks after voting begins

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#hard-forks-9)Hard Forks

*   are non-backward compatible changes that can affect the network protocol, consensus mechanism, ledger architecture, or any change that affects the interoperability of applications using Zenon
*   require a supermajority (67%-90%+) of consensus nodes to upgrade their software to activate
*   non-upgrading Pillars will be forked out

> **Spork Creation Threshold (= Pillar Acceptance Vote)**
> 
> *   Low Pillar Majority (\>67%)
> *   Timeout: 4 weeks after voting begins

> **Spork Activation Threshold (= Pillar Activation Vote)**
> 
> *   High Pillar Supermajority (\>90%)
> *   Timeout: 8 weeks after voting begins

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#miscellaneous-zips-10)Miscellaneous ZIPs

*   ZIPs that don’t fall in the above-mentioned categories
*   e.g. a community-requested change in S Y R I U S to create and activate Sporks
*   The community may signal consensus on a change request to maintainers of public repos

* * *

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#zip-activation-11)ZIP Activation
------------------------------------------------------------------------------------------------

There are two ways to activate ZIPs

1.  **Implicit consensus**  
    Community members individually decide to adopt changes proposed by Informational, Implementation, or Miscellaneous ZIPs.
2.  **Explicit consensus**  
    A majority of Pillars reach a consensus to enforce a protocol change (Soft or Hard Fork) through a Spork.

* * *

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#what-is-a-spork-12)What is a Spork?
---------------------------------------------------------------------------------------------------

A Spork is an embedded on-chain contract that activates a protocol change (Soft or Hard Fork) based on a conditional trigger, e.g. a certain amount of Pillars vote (through an on-chain voting mechanism) to activate the Spork object contained in the upgraded node software.

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#who-can-introduce-a-spork-13)Who can introduce a Spork?

Any community member will be able to create and contribute to the activation of a Spork. As of this date \[September 16th 2022\], however, only one address is allowed to create and activate Spork Objects. It is specified in the genesis file as a hardcoded user address assumed to belong to the founding developers.

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#accelerator-z-the-first-zenon-spork-14)Accelerator Z - The first Zenon Spork

The founding team used the hardcoded Spork address to create the first Zenon Spork to activate the Pillar-governed project funding mechanism “Accelerator Z” (AZ).

The founding developers waited until they were confident that a supermajority (\>67%) of Pillars had upgraded their node software which contained the Spork object to introduce the following conditional logic to the network:

1.  Someone submits an AZ proposal in S Y R I U S
2.  Pillars vote on intermittently locking funds from the Zenon Fabric address as a potential grant for the AZ applicant. The consensus threshold is:

> “**if \>33% of Pillars vote & \>50% of the votes are yes, then accept the AZ grant submission and lock requested funds**”

3.  Upon presenting his/her work, the applicant requests the release of the locked funds by the Pillars who again have to achieve the same consensus on the delivered work being satisfactory.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#creating-activating-sporks-through-the-az-address-15)Creating & activating Sporks through the AZ address
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Based on the founding developers’ indication that network changes could be voted on through AZ, ZIP co-author [@georgezgeorgez](https://forum.zenon.org/u/georgezgeorgez) outlined the following ZIP idea that would allow anyone in the community to create Spork-activated ZIPs:

> Since the original Spork address to create and activate Sporks is hardcoded in the genesis file, it would have to be changed to a different address so that it can be used by the community to create and activate Sporks.
> 
> Accelerator Z already has some functionality to create transactions based on votes. Therefore, the community proposes to change that hardcoded Spork creation address to Accelerator Z contract address.
> 
> This would allow us to then change the Spork Contract so that **only the AZ address** can create and activate Sporks.
> 
> Then we can modify the conditional logic of the AZ contract to something like
> 
> _“When Pillars vote and certain thresholds are met, then the contract sends a transaction to the spork contract to create or activate Sporks.”_
> 
> This would give us community-activated Sporks that can be used for Soft and Hard Forks right from the S Y R I U S wallet through the Accelerator Z tab.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#zip-process-16)ZIP Process
------------------------------------------------------------------------------------------

[![Image 80: image](https://forum.zenon.org/uploads/default/optimized/2X/c/c63332143917f58621af92ec67740799ff9d6d6e_2_690x234.png)](https://forum.zenon.org/uploads/default/original/2X/c/c63332143917f58621af92ec67740799ff9d6d6e.png "image")

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-1-zip-idea-17)Stage 1 - ZIP IDEA
------------------------------------------------------------------------------------------------------

[![Image 81: image](https://forum.zenon.org/uploads/default/optimized/2X/0/020f7ff06090b3f54271500f9e0566ca18655037_2_690x389.png)](https://forum.zenon.org/uploads/default/original/2X/0/020f7ff06090b3f54271500f9e0566ca18655037.png "image")

|  |  |
| --- | --- |
| **Stage Content** | Initial ZIP Proposal & Specification |
| **Exit Criteria** | ZIP proposal including arguments outlining feasibility and logically explaining why it results in an objective improvement of Zenon NoM is published for community discussion. |

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-description-18)Stage Description

The ZIP process begins with a new idea for Zenon NoM. Each potential ZIP must have one or several authors who

*   write the ZIP in a standard format
*   recruit a sponsoring Pillar
*   shepherd the discussions in the appropriate forums
*   implement community feedback
*   build community consensus around the idea.

The ZIP author(s) should first attempt to ascertain whether the idea is ZIP-able. Ideas should be proposed in the [ZIP Category of the forum](https://forum2.zenon.org/c/zenon/zips/22) so they can be found and indexed easily. The author of the idea should solicit feedback from the community and refine the idea. Posting to the main Zenon telegram chat and the [Development & Technical Discussion forum](https://forum2.zenon.org/) is the best way to go about this.

**It is highly recommended that a single ZIP contain a single key proposal or new idea.** The more focused the ZIP, the more successful it tends to be. If in doubt, split your ZIP into several well-focused ones.

Vetting an idea publicly before going as far as writing a detailed ZIP specification is meant to save both the potential author and the wider community time. Asking the Zenon community first if an idea is original helps prevent too much time from being spent on something that is guaranteed to be rejected.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-2-public-debate-revision-19)Stage 2 - PUBLIC DEBATE & REVISION
------------------------------------------------------------------------------------------------------------------------------------

[![Image 82: image](https://forum.zenon.org/uploads/default/optimized/2X/c/cb99a438fd17178e6b7abb4496227984c5135119_2_690x389.png)](https://forum.zenon.org/uploads/default/original/2X/c/cb99a438fd17178e6b7abb4496227984c5135119.png "image")

|  |  |
| --- | --- |
| **Stage Content** | Public discourse on the merit and feasibility of the ZIP proposal. |
| **Exit Criteria** | Author has gauged community interest and support for the proposal has been sufficient to merit finding a sponsoring Pillar. |

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-description-20)Stage Description

The author(s) should gather community feedback to iteratively refine and flesh out their ZIP idea until it can be specified with a sufficiently high degree of conformity with opinions voiced in the community.

The community should reject a ZIP proposal for the following reasons:

*   duplication of effort
*   refusal to refine the ZIP idea based on critical community feedback
*   being too unfocused or too broad
*   being technically unsound
*   not providing proper motivation or addressing backward compatibility
*   not being feasible
*   not in line with the principle of progressive decentralization

For a ZIP to be accepted it must meet certain minimum criteria:

*   It must be a clear and complete description of the proposed enhancement
*   The enhancement must represent a net improvement
*   The proposed implementation, if applicable, must not complicate the protocol unduly

Before drafting an official ZIP, the author will have to identify a Pillar willing to sponsor the ZIP and add it to their ZIP repository for indexing by the Community Pointer repo.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-3-official-zip-proposal-21)Stage 3 - OFFICIAL ZIP PROPOSAL
--------------------------------------------------------------------------------------------------------------------------------

[![Image 83: image](https://forum.zenon.org/uploads/default/optimized/2X/9/9e90369be7d0eb52a6ce193800582eb2dbfb9354_2_690x389.png)](https://forum.zenon.org/uploads/default/original/2X/9/9e90369be7d0eb52a6ce193800582eb2dbfb9354.png "image")

|  |  |
| --- | --- |
| **Stage Content** | \- ZIP publication in sponsoring Pillar’s Git repository  
\- ZIP indexing by Community Pointer Repo  
\- Spork submission through AZ contract  
\- ZIP Finalization in case of Informational (text) or Implementation (code) ZIP |
| **Exit Criteria** | \- Author has found a sponsoring Pillar that has publicly announced ZIP sponsorship by adding the draft ZIP to its public repo.  
\- Informational / Implementation ZIP has been finalized, or Spork has been proposed through the modified AZ contract (the new Spork contract address) |

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-description-22)Stage Description

Once the author has gauged initial community interest, a Pillar must be found to endorse the ZIP through sponsorship by adding the ZIP to its public repository. This ensures the ZIP was critically reviewed by a Pillar holder who is willing to back it with its brand and reputation in the community.

Once a sponsoring Pillar has been found,

1.  the author writes a properly formatted _Draft_ ZIP. The Draft ZIP formatting standards used and outlined in this ZIP should be used as a reference.
    
2.  the sponsoring Pillar publishes the Draft ZIP in its own public Git repository.
    
3.  the author and sponsoring Pillar (the “Sponsors”) inform the community about the draft ZIP publication and endorsement through public channels (Github, IPFS, Gitlab, Telegram, Zenon Forum, etc.).
    
4.  _In case the ZIP proposes a protocol change requiring a _Spork_ (for Soft or Hard Forks), the Sponsors must submit the ZIP proposal for an on-chain vote by Pillars through the (yet to be) modified AZ contract._
    
5.  the Sponsors continue working with the community to solicit and implement feedback via pull requests or through public or private channels.
    

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#decentralizing-central-editors-with-a-community-pointer-repo-23)Decentralizing central editors with a Community Pointer Repo

We propose a repository structure that is fault-tolerant and resilient against censorship from central editors and/or hosting software providers. Pillars who want to sponsor ZIPs should set up a repository that can host the ZIP and accompanying code. Ideally, repositories are established across multiple service providers and sources: Github, Gitlab, Gitea, IPFS, and others.

Sponsoring Pillars must provide a _Proof of Pillar_ (a signed message from the Pillar address) in the repo to prove participation and get indexed by the Central Pointer Repo that is established by the community and maintained at [https://github.com/Zenon-Netowrk-ZIPs](https://github.com/Zenon-Netowrk-ZIPs). This repo simply points to verified Pillar repos as a convenience to those searching for ZIPs.

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#the-role-of-official-editors-in-zenon-24)The role of official editors in Zenon

*   maintain an official pointer repository that indexes pillar repos and the ZIPs in there
*   verify pillar ownership of their ZIP repositories (through signature file)
*   add them as a submodule to the [Zenon Community repo](https://github.com/Zenon-Network-ZIPs/ZIPs)
*   implement redundancy protocols or backups to replace a compromised pointer repo with another

The community pointer repo points to a ZIP folder hosted by each sponsoring Pillar. Anything added to it will appear in the pointer. It’s like a repo with shortcut folders to Pillar repositories.

Each sponsoring pillar maintains its own ZIP numbering while adhering to established formatting standards. The editor repo maintains standard format templates and best practice recommendations for sponsoring Pillars to use.

[![Image 84: image](https://forum.zenon.org/uploads/default/optimized/2X/9/91c1ce421aae1de6b8eb6affee7319a3e5eba5b7_2_633x499.png)](https://forum.zenon.org/uploads/default/original/2X/9/91c1ce421aae1de6b8eb6affee7319a3e5eba5b7.png "image")

Note that individual Pillars can also choose to act as a pointer service by adding the repos of other Pillars as submodules to their own.

The Draft ZIP should be written in standard ZIP style as described below to ensure uniform ZIP proposal formatting across sponsoring Pillars. Sponsoring Pillars assign their own sequential numbering to ZIPs and maintain a list of ZIPs they sponsor(ed).

The ZIP naming and numbering convention must adhere to the following format:

> **\[ZIP-PillarName-PillarZIPNumber\]**

e.g.

> *   “ZIP:deeZNNutz-0001"
> *   “ZIP:deeZNNutz-0002"
> *   “ZIP:ZenonORG-0001”
> *   “ZIP:ZenonORG-0002”

In addition, the sponsoring Pillar will assign a ZIP label “Informational ZIP”, “Implementation ZIP”, “Soft Fork”, “Hard Fork” etc., and give it the status “Draft”, “Accepted”, “Rejected”, “Withdrawn”, “Final”, “Replaced”, or “Active”.

The Community Pointer repo could thus look like this:

| Name | Title | Label | Status |
| --- | --- | --- | --- |
| ZIP:deeZNNutz-0001 | ZIP Process | Informational ZIP | Draft |
| ZIP:deeZNNutz-0002 | Bitcoin<\>Zenon merge mining | Soft Fork | Active |
| ZIP:ZenonORG-0002 | RPC data compression for nodes 2.0 | Implementation ZIP | Replaced |

There are different ZIP statuses.

For Informational ZIPs and Implementation ZIPs which only require **implicit consensus**:

[![Image 85: image](https://forum.zenon.org/uploads/default/optimized/2X/d/d535f64c68de9a63f907dc842080fb099ef26d93_2_517x321.png)](https://forum.zenon.org/uploads/default/original/2X/d/d535f64c68de9a63f907dc842080fb099ef26d93.png "image")

For Sporks that require **explicit consensus** by Pillars to be accepted and activated:

[![Image 86: image](https://forum.zenon.org/uploads/default/optimized/2X/7/71832bb7c452dcf2e8d361b7e616f708a8db4dab_2_517x321.png)](https://forum.zenon.org/uploads/default/original/2X/7/71832bb7c452dcf2e8d361b7e616f708a8db4dab.png "image")

| Status | Description |
| --- | --- |
| Idea | ZIP idea is circulated in the community in no specific format |
| Draft | ZIP idea is published in draft stage, adhering to formatting best practices |
| Rejected | ZIP proposal was rejected by the community |
| Withdrawn | ZIP proposal was withdrawn by the Sponsors |
| Accepted | Spork proposal acceptance vote reached required Pillar quorum |
| Final | Final ZIP implementation published and ready for activation |
| Replaced | ZIP implementation has been replaced by a newer or alternative version |
| Active | ZIP implementation has been activated |

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#zips-relying-on-implicit-consensus-are-finalized-in-step-4-25)ZIPs relying on _implicit_ consensus are finalized in step 4

Once an Informational, Implementation or Miscellaneous ZIP has been iteratively refined, and a reference Implementation in form of text or code published, it can be marked as “**Final**”. Once they are actively used (e.g. this ZIP:deeZNNutz-0001) or a pull request to a public repo (e.g. for a change to the S Y R I U S wallet) has been performed, the ZIP can be marked as “Active”.

### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#zips-relying-on-explicit-consensus-kick-off-in-step-4-26)ZIPs relying on _explicit_ consensus kick off in step 4

On the other hand, ZIPs which propose protocol changes that lead to Soft or Hard Forks, and have to be activated by Pillars via a **Spork**, should pass the Pillar Acceptance vote before the reference implementation is completed.

This ensures that

*   all Pillars are informed about the proposed network change
*   all Pillars are given the opportunity to signal their support for it
*   ZIP sponsors can gauge Pillar support before engaging in significant implementation work

> Reaching a majority quorum in the Pillar Acceptance vote marks a ZIP as “Accepted” and tells the authors there is significant interest for the Spork so that they may begin with the implementation work if it has not already started.

Any ZIP can also be “Rejected” or “Withdrawn” due to lack of community support or explicit opposition. It is important to have a record of this fact for future ZIP authors.

Some Informational ZIPs may also have a status of “Active” if they are never meant to be completed, E.g. this ZIP:deeZNNutz-0001.

* * *

**The ZIP process for Informational, Implementation, and Miscellaneous ZIPs ends here. The following stages only apply for ZIPs leading to Sporks.**

* * *

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-4-spork-creation-27)Stage 4 - SPORK CREATION
------------------------------------------------------------------------------------------------------------------

[![Image 87: image](https://forum.zenon.org/uploads/default/optimized/2X/a/a59cdef6ea0d4ce98d58d4d7ebf3379007c35b57_2_690x389.png)](https://forum.zenon.org/uploads/default/original/2X/a/a59cdef6ea0d4ce98d58d4d7ebf3379007c35b57.png "image")

|  |  |
| --- | --- |
| **Stage Content** | \- Spork creation via AZ address  
\- Community Acceptance signaling via signed messages  
\- ZIP Acceptance Vote via modified AZ contract |
| **Exit Criteria** | Pillar Acceptance quorum reached / not reached within voting timeframe |

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-description-28)Stage Description

Just like when someone submits a new Accelerator Z proposal, the ZIP author submits a Spork creation proposal through the modified AZ contract from within S Y R I U S.

Pillars can then vote on its _Acceptance_. If it passes, the Spork is created and “waits” for the ZIP authors to submit the Spork activation proposal (which is analogous to Pillars voting for an AZ phase, just with different activation criteria).

The point of the Acceptance vote is to

*   “lock in” the creation of a Spork on-chain
*   for a Spork ZIP to pass a first consensus filter
*   give the ZIP supporters the confidence to commit to the Spork activation, start planning for it, and accept that validators who don’t follow might be forked out

By helping Pillars make a qualified decision during the on-chain Acceptance vote, ZIP authors can increase their chances for a successful Spork activation. For this, they should reach out to the community and ask any ZNN holder to sign a message in S Y R I U S, e.g.

> “ACCEPT ZIP:deeZNNutz-0001”

Community-provided signaling trackers (similar to taproot.watch) can record all signed messages, and cross-reference them with the amount of ZNN held in the addresses from which the signatures originated and whether the addresses are used by a “Delegator”, “Staker”, “Sentinel”, or “Pillar”.

This technique allows the **entire** community to indicate their support for a Spork ZIP, thus helping Pillars make a better voting decision while allowing the ZIP Sponsors to get some polling data on the community-wide support of their proposed network change.

If the Acceptance vote fails due to a timeout or too many negative Pillar votes, the ZIP Sponsors are free to choose whether they should redraft or abandon it.

If the Acceptance vote passes, it is a signal to the community developers that Pillars support the initiative and they will run the code after proper vetting. Developers should feel confident in spending time writing code to support the ZIP at this stage.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-5-implementation-distribution-29)Stage 5 - IMPLEMENTATION DISTRIBUTION
--------------------------------------------------------------------------------------------------------------------------------------------

[![Image 88: image](https://forum.zenon.org/uploads/default/optimized/2X/1/1e8ff4c7b1ffc5f78c11e22c99c379789628940e_2_690x389.png)](https://forum.zenon.org/uploads/default/original/2X/1/1e8ff4c7b1ffc5f78c11e22c99c379789628940e.png "image")

|  |  |
| --- | --- |
| **Stage Content** | \- Reference implementation  
\- Downloadable binaries |
| **Exit Criteria** | Reference implementation published on sponsoring Pillar Git repo |

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-description-30)Stage Description

Once the reference implementation has been built, the sponsoring Pillar

*   publishes it on its Pillar Git repo
*   merges the ZIP code into its mainline repo
*   builds the binary and ensures other Pillars will be able to download and install it

The implementation contains the Spork Object whose activation is triggered by the Pillar Activation vote reaching the threshold defined in the paragraph _ZIP TYPES_.

Example: Spork Object for a Hard Fork would contain the following conditional activation trigger:

> “activate if \>90% of Pillars indicate they have updated their node software with the reference implementation of ZIP:deeZNNutz-0002 through the Activation vote”.

Anyone can also merge in the changes into their repo copies and build themselves. People can verify if it’s the same binary through hashes.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-6-community-audit-31)Stage 6 - COMMUNITY AUDIT
--------------------------------------------------------------------------------------------------------------------

[![Image 89: image](https://forum.zenon.org/uploads/default/optimized/2X/5/57efe07041c8b023c787954f8090a8dd9642fd27_2_690x389.png)](https://forum.zenon.org/uploads/default/original/2X/5/57efe07041c8b023c787954f8090a8dd9642fd27.png "image")

|  |  |
| --- | --- |
| **Stage Content** | Audit timeframe & community feedback |
| **Exit Criteria** | Timeout of audit timeframe |

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-description-32)Stage Description

Once the Sponsors announce the publication of the Final ZIP implementation they should include a soft deadline until community audits should be concluded.

Community members may comment on the implementation or directly push changes via pull request to the sponsoring Pillar’s ZIP repo. Once the code is complete and vetted by a process similar to the [Bitcoin Contribution Criteria](https://github.com/bitcoin/bitcoin/blob/master/CONTRIBUTING.md), the ZIP can be marked “Final”.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-7-pillars-upgrade-nodes-vote-33)Stage 7 - PILLARS UPGRADE NODES & VOTE
--------------------------------------------------------------------------------------------------------------------------------------------

[![Image 90: image](https://forum.zenon.org/uploads/default/optimized/2X/9/9a56d59e4a2b88066a76c59482ea4e79e1094756_2_690x389.png)](https://forum.zenon.org/uploads/default/original/2X/9/9a56d59e4a2b88066a76c59482ea4e79e1094756.png "image")

|  |  |
| --- | --- |
| **Stage Content** | Call to Pillars to signal ZIP implementation support |
| **Exit Criteria** | ZIP activation lock-in by reaching the activation vote quorum threshold |

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-description-34)Stage Description

The ZIP Sponsors now submit an activation request for the proposed Spork in S Y R I U S. Pillars now have to upgrade their node software (if not already done so) and then vote on the activation of the Spork. Reaching the voting threshold will trigger the Spork activation transaction.

What happens if the Spork fails to activate in time? ZIP Sponsors will have to assess the reason for it and either extend the activation timeline or revise the ZIP if needed.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-8-spork-activation-35)Stage 8 - SPORK ACTIVATION
----------------------------------------------------------------------------------------------------------------------

[![Image 91: image](https://forum.zenon.org/uploads/default/optimized/2X/1/12ab99bb39f2f86a7dc35bc4e4d78d5a8fba544d_2_690x389.png)](https://forum.zenon.org/uploads/default/original/2X/1/12ab99bb39f2f86a7dc35bc4e4d78d5a8fba544d.png "image")

|  |  |
| --- | --- |
| **Stage Content** | Spork activation is triggered |
| **Exit Criteria** | ZIP is activated |

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#stage-description-36)Stage Description

Once sufficient Pillars have voted to reach the activation threshold the Spork is activated and non-supporting network participants may be forked out until they opt into the protocol change.

To prevent Pillars from voting on the activation without upgrading their node software, the following security mechanism will be implemented as a standard procedure as suggested by [@georgezgeorgez](https://forum.zenon.org/u/georgezgeorgez):

> When a Spork Acceptance vote passes, a Spork gets created with a unique ID. That unique ID gets added to a list in go-Zenon as part of the code change.
> 
> Now, when the Activation vote happens, a Pillar node won’t send the transaction to vote for Sporks unless it knows about it locally, by checking if its ID is in that hardcoded list of spork IDs in go-Zenon.
> 
> It’s like an account whitelisting. In general, the network allows you to send tx to whatever address but you can configure your wallet to only allow sending to preset addresses. Basically, we can do the same thing with spork IDs by configuring S Y R I U S to only allow voting for Sporks in its list. And the list gets updated when they download the new version.

This allows making sure a Pillar doesn’t sign the activation vote unless the upgrade happened.

Upon activation of the Spork, the sponsoring Pillar may now update the ZIP label to “Active” or “Replaced”.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#annex-37)Annex
------------------------------------------------------------------------------

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#conditions-for-realization-38)Conditions for realization:
-------------------------------------------------------------------------------------------------------------------------

*   Modification of Spork Contract and change of Spork Creation Address
*   Spork ID whitelisting mechanism

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#areas-to-improve-and-expand-over-time-39)Areas to improve and expand over time
----------------------------------------------------------------------------------------------------------------------------------------------

*   Emergency ZIPs
*   Acceptance signaling tooling
*   Prepare [contribution criteria for code submission](https://github.com/bitcoin/bitcoin/blob/master/CONTRIBUTING.md)

* * *

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#zip-format-guideline-40)ZIP Format Guideline
------------------------------------------------------------------------------------------------------------

Pillars should try to adhere to the same ZIP format and metadata requirements. The outline below is a guideline and can be used if a Pillars has not established their own.

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#header-41)Header

Each ZIP should contain a header that contains metadata about the ZIP. The headers should appear in the following order.

| Field | Description |
| --- | --- |
| zip | Pillar Name + ZIP number, or “?” when prior to Pillar involvement |
| title | ZIP title |
| author | A comma-separated list of the authors (anon is acceptable) |
| status | Current status of the ZIP (draft, accepted, rejected, withdrawn, final, replaced, active) |
| type | ZIP type (Informational, Minor, Major) |
| acceptance | A minimum quorum threshold for acceptance signaling |
| activation | A minimum quorum threshold for activation of a spork object |
| created | Date created on, in ISO 8601 (yyyy-mm-dd) format |
| license | Each new ZIP must identify at least one acceptable license |
| link | URL to proposal discussion |

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#abstract-42)Abstract

A short description of the technical issue being addressed or feature to be added.

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#motivation-43)Motivation

The motivation should clearly explain why this change or improvement is required or why the existing protocol is inadequate to address the problem that the ZIP solves.

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#specification-44)Specification

The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current Zenon platforms

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#rationale-45)Rationale

The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work. The rationale should provide evidence of consensus within the community and discuss important objections or concerns raised during discussion.

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#implementation-46)Implementation

The actual code implementing the ZIP’s specification or a link to the reference implementation of the ZIP’s specification.

#### [](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#license-47)License

The ZIP should be licensed under GNU General Public License v3.0 to match the Zenon.network license.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#zip-comments-48)ZIP Comments
--------------------------------------------------------------------------------------------

Comments on a ZIP should occur where the draft was posted. There should be no requirement to exchange ideas on a specified medium.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#zip-references-49)ZIP References
------------------------------------------------------------------------------------------------

*   [Bitcoin’s longest-serving Lead Maintainer calls it quits, names no successor](https://protos.com/bitcoins-longest-serving-lead-maintainer-calls-it-quits-names-no-successor/)
*   [AZ ZIP Proposal](https://forum2.zenon.org/t/proposal-az-submission-of-first-zip-to-validate-process/925)
*   [BICH DAO ZIP Framework Comments](https://github.com/orgs/Big-Inches-Club-House/discussions/4#discussioncomment-3511372)
*   [https://forum2.zenon.org/t/zips-and-why-i-believe-pillars-should-sponsor-them/984](https://forum2.zenon.org/t/zips-and-why-i-believe-pillars-should-sponsor-them/984)
*   [ZIP Process Draft - Google Docs](https://docs.google.com/document/d/1gzG3enZkl-rf951OeCIzDDpgwIkNLaXiRx2BgiyfyNg/edit#)

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#zip-license-50)ZIP License
------------------------------------------------------------------------------------------

This ZIP is licensed under GNU General Public License v3.0.

[](https://forum.zenon.org/t/zip-deeznnutz-0001-final/991/print#change-log-51)Change Log
----------------------------------------------------------------------------------------

Is the code implementation decentralised and automated in this kind of implentation ? Proposals could be code, like ethOS ? I’m thinking about Radicle when it comes to decentralized code. It would make ZNN a way to own code and not just tokens.

Can you post a link to what you’re referring with radicle? In the current proposal the code is insofar decentralized as ZIP implementations would be published by sponsoring Pillars in their own repos. How they host these repos is up to them. Although Idk if the pointer service is also able to link to self-hosted repos (then again I wouldn’t know why not). [@0x3639](https://forum.zenon.org/u/0x3639) maybe you know?

[romeo](https://forum.zenon.org/u/romeo) September 9, 2022, 2:10am  5

I’ve gone through it at a high level and my comments are below, in order of the post. No need to respond individually it’s just food for thought. TLDR I think it’s too complicated and requires significant manual intervention and effort at multiple stages.

> acceptance \>50% of Pillars  
> or \>50% delegation weight  
> or \>25% of Pillars AND \>25% of delegation weight

I don’t think letting authors choose the consensus level and mechanism is appropriate. It should be predefined and clear.

> We can only assume Mr. Kaine and his team wants the community to own and manage the ZIP process independently.

This is an assumption and should be excluded

> Before drafting an official ZIP, the author will have to identify a Pillar willing to sponsor the ZIP. Pillars are responsible for upgrading the network and without their support, a ZIP will likely fail to get adopted.

How does one identify a sponsor? How do people get in contact with Pillar operators? Most are not involved in the community currently - you run the risk of ZIPs failing at the first stage unless a small (consistent) sub set of Pillar operators continue to be involved and sponsor. This has a high risk of being a central failure point - relies on small number of active pillar operators who would be required to continue to be engaged and active

> Unlike core protocol changes, small enhancements or patches of Zenon implementations do not require standardization across all validators and public nodes; these don’t need a ZIP

This contradicts earlier statements and the defined ZIP categories: _"The ZIP process is the primary mechanism for proposing new features, for collecting community input or consensus on an issue, and for documenting the design decisions that have gone into the development and growth of the Zenon Network. "_

> The community should reject a ZIP proposal for the following reasons:  
> not in keeping with the Zenon philosophy

what is the zenon philosophy? Is this defined? To me it’s subjective in nature and could lead to proposals failing due to unmeasurable criteria.

> Stage 3

Stage 3 is increasingly handraulic and puts a big onus of effort onto Pillar operators (who already maintain infrastructure and participate in AZ). Pillar participation is currently low, how do you ensure Pillars continue to participate? Many Pillars may not want (or have the skills) to participate in hosting a repo or creating a github account. Can they still “sponsor” the ZIP without any extra effort (that would be a better outcome imo)?

There is also no explanation of which ZIP status relates to what stage (Draft = stage 2 etc.)

> Each sponsoring pillar maintains their own ZIP numbering and there is no strictly enforced ZIP format. However, the editor repo maintains standard format templates and best practice recommendations for sponsoring Pillars to use.

How does the editor ensure linkage between their own numbering/naming standard and whatever is on the Pillars own private repos? What if numerous ZIPs are active at once? Significant interaction required here and could be an avenue for human error. Who is the editor? Who votes them in? Are they reimbursed and if so who covers the cost?

> Stage 4

Stage 4 is unnecessary imo and complicates matters significantly. For starters a 2/3 supermajority of ZNN is near impossible to achieve. How would you ensure voter participation?

> The ZIP author is free to define in the Draft ZIP what is considered a sufficient quorum threshold; it may be lower for Minor or Informational ZIPs. Depending on the type of ZIP

This needs to be defined and not left up to the author (otherwise what’s stopping them from saying a 5% vote is enough)

> To signal acceptance of the ZIP proposal, network participants can sign a transaction in S Y R I U S with a message generated in a community-developed tool (currently in development) with a message in a specific format such as “ACCEPT ZIP:deeZNNutz-0001” before the network reaches a certain predefined momentum, the Acceptance Snapshot Momentum Height.

You’re proposing a ZIP process that currently can’t be successfully undertaken due to this tool not existing

> For Liquidity Providers who hold funds on other networks than Zenon NoM, the ZIP Sponsors should define corresponding block heights for the Acceptance Snapshots. Liquidity Providers will thus use their Private / Public Key Pair of their wZNN holding address to sign a transaction with the corresponding message before the block lapses.

This process is underdefined. Who counts the votes? Who validates that the keypair matches the LP holder? What about the orbital fund etc.? Will the tool automatically achieve all of this?

> If the community has signaled a sufficiently high acceptance to continue pursuing a Major ZIP activation, a reference implementation must be built in the form of code, a patch, or a URL to the same.

What if its not a Major ZIP?

> The sponsoring Pillar will further merge the ZIP code that has a conditional trigger into its mainline repo. Then the sponsoring Pillar owner needs to build the binary and make sure other Pillars will be able to download and install it

What validation occurs at this stage to ensure the safety of the binary? Who informs the Pillars it’s ready and at what date to install it? Who and how follows up with those who haven’t participated?

> The sponsoring Pillar changes the label of the ZIP in their repo from “Draft” to “Final”.

What exactly triggers the change from Draft to Final? What metric has to be met?

Overall I’m concerned this will result in a highly involved process that could be hard to track, enforce and follow. You’ve essentially replaced the role of the editor in other BIP processes to that of the Pillar operators, which has the same drawbacks. I feel it needs to be streamlined and shortened to give it a better chance of success.

I’ve looked at this through the lens of the core teams expected upcoming protocol upgrade - i.e. will they engage to identify a Pillar sponsor and how etc.? How long would this process take to be finalized? Given they haven’t responded to the call to utilize the existing GitHub what makes you think they’ll want to be even more hands on with this process?

Hi [@romeo](https://forum.zenon.org/u/romeo) thank you very much for the extensive feedback! I will still address all of it because it could be valuable for others to see the points you raised discussed.

#1

[![Image 92: image](https://forum.zenon.org/uploads/default/optimized/2X/0/0a7c26bb0b1be2ad486b76a4ac002bdf648bcce2_2_690x164.png)](https://forum.zenon.org/uploads/default/original/2X/0/0a7c26bb0b1be2ad486b76a4ac002bdf648bcce2.png "image")

I would disagree here for a few obvious reasons:

*   different ZIPs need different quora
    
*   overall voting participation can significantly vary depending on the stage of the project and type of participant needed for a quorum (e.g. today, voting participation will probably be relatively low - in the future, this might change. Hence, it’s necessary to stay flexible)
    
*   This ZIP proposes general guidelines for quora thresholds. Generally, majorities should be the goal in any case. For Acceptance votes that affect Informational or Minor ZIPs, a simple majority of Pillars or all addresses (weighted by ZNN balance), may be sufficient. This is what ZIP:deeZNNutz-0001 proposes. For Acceptance votes of Major ZIPs, this threshold should probably be higher. Regarding the Activation of a Spork, a 2/3 supermajority should be the minimum (e.g. in Bitcoin the Taproot upgrade required a \>90% miner participation to lock in) to prevent bad chain splits.
    
*   The fact that authors can choose consensus thresholds forces them to enter a discourse with the community. If the community opposes their proposition, they will have to adjust.
    

#2

[![Image 93: image](https://forum.zenon.org/uploads/default/optimized/2X/b/b97b4829f5fdeb39b92ea6975cd9ea81d3ad77ec_2_690x112.png)](https://forum.zenon.org/uploads/default/original/2X/b/b97b4829f5fdeb39b92ea6975cd9ea81d3ad77ec.png "image")

It’s part of the motivation for this ZIP and it states that it’s an assumption. Removing it would question the motivation for this ZIP.

#3

[![Image 94: image](https://forum.zenon.org/uploads/default/original/2X/1/1124a0f165d563c32172bf5fbbc25d30d9e64242.png)](https://forum.zenon.org/uploads/default/original/2X/1/1124a0f165d563c32172bf5fbbc25d30d9e64242.png "image")

*   How to get in touch with a sponsoring Pillar? By reaching out to Pillar holders through chat or the repos of sponsoring Pillars.
    
*   Pillars are among the most active network participants since they have to maintain infra and vote on proposals. They are also the ones who will ultimately have to upgrade their node software for ZIP activation (esp. Sporks). Pillars have the most skin in the game and they are the type of network participants who are most incentivized to sponsor network improvements. Pillars also need a certain technical savvyness and they tend to have the longest investment horizon among all network participants. Sponsoring ZIPs is also a way of brand-building for them and can help them attract delegators. I don’t see a better alternative tbh. Other network participants don’t have as high an incentive to sponsor ZIPs - and getting rid of sponsors means more responsibility for a central editor (THIS is definitely a central point of failure) or accepting there will be a lot of low-quality ZIP proposals that just waste everyone’s time.
    

#4

[![Image 95: image](https://forum.zenon.org/uploads/default/original/2X/0/042d7284457bab53fdeb29f5aa573aa2037e9763.png)](https://forum.zenon.org/uploads/default/original/2X/0/042d7284457bab53fdeb29f5aa573aa2037e9763.png "image")

Thanks for spotting, that should say “Spork”, not “ZIP”. Edited.

#5

[![Image 96: image](https://forum.zenon.org/uploads/default/original/2X/1/17496bb81f8f305f9f145dfabb3e6ff8a3ef18fc.png)](https://forum.zenon.org/uploads/default/original/2X/1/17496bb81f8f305f9f145dfabb3e6ff8a3ef18fc.png "image")

Fair point, though this was inspired by the BIP standard. We can specify this with e.g. “Going against the principle of progressive decentralization” or other examples. But overall I feel core community members who engage in ZIP debates know this refers to the cypherpunk / bitcoin ethos which Zenon emulates.

#6

[![Image 97: image](https://forum.zenon.org/uploads/default/original/2X/4/4fdeed985fde325456cb2d97c7a77e55e7588d76.png)](https://forum.zenon.org/uploads/default/original/2X/4/4fdeed985fde325456cb2d97c7a77e55e7588d76.png "image")

Given that Pillars know how to run infra I don’t think it’s a big challenge for them to maintain a repo. The editor repo which runs the Pointer Service automatically tracks all sponsoring Pillar repos and changes in it. No extra effort from Pillars is needed beyond signing up on Github and creating a repo with a list of ZIPs they sponsor + give each ZIP a name & number. This is barely more difficult than creating an excel spreadsheet. The downloadable node binaries for major ZIPs can also be provided by the ZIP author, the Pillar just has to upload them into their repo so that the Pointer service can index them.

If the Pillars want to host their Git repo elsewhere than GitHub, more effort is needed.

Regarding Pillar participation: in theory, even a single Pillar is enough to sponsor ZIPs. Over time, the goal is to have multiple so that the ZIP process becomes more decentralized. Again, the key goal is to minimize dependence on central editors as much as possible. Running a pointer service is doesn’t create a single point of failure either.

“There is also no explanation of which ZIP status relates to what stage (Draft = stage 2 etc.)” thanks, will try to clarify this.

#7

[![Image 98: image](https://forum.zenon.org/uploads/default/original/2X/f/f410dd400a1520155340b747d1412247dbb671e8.png)](https://forum.zenon.org/uploads/default/original/2X/f/f410dd400a1520155340b747d1412247dbb671e8.png "image")

The linkage is done by adding sponsoring Pillar repos as submodules to the editor’s Pointer Service repo. Once added, any changes on the Pillar’s repo are automatically synced with the editor’s repo.

The number of simultaneously active ZIPs is irrelevant – the Pointer Repo indexes it all.

There is no manual interaction required beyond adding a Pillar repo to the Pointer repo as a submodule after the editor has verified the Pillar owns that repo through a signed message.

Any dedicated community member can run a Pointer repo or help maintain the existing one. Efforts to do so can be covered through AZ or donations.

#8

[![Image 99: image](https://forum.zenon.org/uploads/default/original/2X/7/7480f5db773e42cd7809b5f625919f1119d04026.png)](https://forum.zenon.org/uploads/default/original/2X/7/7480f5db773e42cd7809b5f625919f1119d04026.png "image")

Stage 4 is critical to get community acceptance for Informational and Minor ZIPs that don’t lead to a Spork. Voter participation depends on awareness creation – just like in every human political system.

The suggested supermajority of 2/3 is for Major ZIPs leading to a Spork which will split the network if the acceptance threshold is set too low. Then again, authors can set the necessary thresholds for Acceptance Votes themselves – this prevents a too rigid framework that imposes arbitrary quora.

With this step we want to ensure EVERY network participant can signal their support for ANY ZIP.

#9

[![Image 100: image](https://forum.zenon.org/uploads/default/original/2X/c/c9cb5acc0a0a3e624d825ecd07fb7b67a0a466ac.png)](https://forum.zenon.org/uploads/default/original/2X/c/c9cb5acc0a0a3e624d825ecd07fb7b67a0a466ac.png "image")

This is why they need a sponsoring Pillar. A 5% acceptance quorum would be way too low and it would be very hard to find a sponsoring Pillar to back it with their name. Also, other community members will oppose the Draft ZIP after publication, preventing the ZIP proposal from getting the support needed.

Unless I’m mistaken, Informational or Minor ZIPs technically don’t need on-chain consensus by a supermajority to activate because they don’t lead to a Spork that can split the chain. Only Major ZIPs need a majority of Pillars (and maybe Sentinels in the future) to upgrade their node software in consensus.

#10

[![Image 101: image](https://forum.zenon.org/uploads/default/original/2X/7/71b342054b0255787c5d312346fbe0b6987daae2.png)](https://forum.zenon.org/uploads/default/original/2X/7/71b342054b0255787c5d312346fbe0b6987daae2.png "image")

As stated in the quote the necessary tools are currently being developed and will be available in a few weeks. We will use this time to improve this Draft ZIP.

#11

[![Image 102: image](https://forum.zenon.org/uploads/default/original/2X/c/c81a0e93321ebd97033d4f605c51edd15e36b263.png)](https://forum.zenon.org/uploads/default/original/2X/c/c81a0e93321ebd97033d4f605c51edd15e36b263.png "image")

While this might not be available from day 1. the tooling for vote counting should eventually be network agnostic and reliably validate/count votes of LPs on other chains too.

#12

[![Image 103: image](https://forum.zenon.org/uploads/default/original/2X/0/0269d5a8d3e9329503317b3b25dd33c73ab68891.png)](https://forum.zenon.org/uploads/default/original/2X/0/0269d5a8d3e9329503317b3b25dd33c73ab68891.png "image")

*   The “Implementation” of Informational ZIPs is not code based but simply the description of the ZIP itself. This is the case for this very ZIP:deeZNNutz-0001
*   The implementation of Minor ZIPs doesn’t lead to a Spork the majority of nodes needs to support in order to become active. Minor ZIPs are more like a soft fork that is backwards compatible and can be supported by any number of nodes. The ZIP author will nevertheless want to know if enough nodes will run his reference implementation before building it.
*   For a Major ZIP it’s critical that a reference implementation is built after acceptance voting because the majority of Pillars have to support it.

#13

[![Image 104: image](https://forum.zenon.org/uploads/default/original/2X/8/8ffa134c8f9026358ee4498c7af5c5b4caccdb91.png)](https://forum.zenon.org/uploads/default/original/2X/8/8ffa134c8f9026358ee4498c7af5c5b4caccdb91.png "image")

The code for the reference Implementation has been published and audited by the community. To ensure that files have not been tampered with you can either sign or hash them ([see here for the description of this process](https://stackoverflow.com/questions/7828053/hashing-vs-signing-binaries)). The answers to your other questions are answered in the subsequent stages.

#14

[![Image 105: image](https://forum.zenon.org/uploads/default/original/2X/5/5ab2122491a7de3ce6552aff9c7e2a435c700497.png)](https://forum.zenon.org/uploads/default/original/2X/5/5ab2122491a7de3ce6552aff9c7e2a435c700497.png "image")

See table in stage 3

Needless to say, the current goal is to improve and streamline the process based on community feedback.

[0x3639](https://forum.zenon.org/u/0x3639)

September 9, 2022, 10:53am  7

I’m going to try a different approach to responding. I’m going to make one post per item. Not sure if that will make it easier to review. But here goes:

Romes States

[![Image 106: image](https://forum.zenon.org/uploads/default/optimized/2X/0/0a7c26bb0b1be2ad486b76a4ac002bdf648bcce2_2_690x164.png)](https://forum.zenon.org/uploads/default/original/2X/0/0a7c26bb0b1be2ad486b76a4ac002bdf648bcce2.png "image")

I wonder if this could be an attack vector. ZIP author proposes a low threshold for a ZIP to be adopted that could fracture the network. For example, a Spork that activates with just 50% of physical Pillars will confuse the network as to which fork is more relevant.

Should we propose a mandatory minimum to spork the network? 90% of functioning pillars (like taproot) or 90% of all Pillar weight (sum of all pillar delegation). Or if 90% is too high, propose another number.

[0x3639](https://forum.zenon.org/u/0x3639)

September 9, 2022, 11:01am  8

Romeo States

[![Image 107: image](https://forum.zenon.org/uploads/default/optimized/2X/b/b97b4829f5fdeb39b92ea6975cd9ea81d3ad77ec_2_690x112.png)](https://forum.zenon.org/uploads/default/original/2X/b/b97b4829f5fdeb39b92ea6975cd9ea81d3ad77ec.png "image")

This assumption is the premises of rethinking the ZIP process. The Community did prepare a ZIP that required Kaine to create a repo and become the editor of that repo. We know specifically that he wants a ZIP process because he asked for it after being absent for months. And to ignore our direct request to create the repo can only lead to one logical conclusion. In addition, the team started to spike LP rewards, as to say, yes, we are here working.

These facts tell me: (1) the team is working, and (2) the team does not want to create and manage a repo in /zenon-network on github.

I do not think we can ignore these signals in creating a ZIP process.

For a Spork to activate in the first place, Pillars must upgrade their node software so that it can activate. If Pillars upgrade their node software that contains a spork element that already activates if 50% of the Pillars run it, they would either be dumb or collude to intentionally split the network.

Note that no ZIP process will ever prevent this collusion from happening hence it’s not possible to enforce minimal thresholds (a central editor à la BIP doesn’t have that power either - miners can collude one way or the other if they want). This is why this ZIP can only provide best practice recommendations for consensus thresholds.

It’s to be assumed that Spork proposals with intentionally low consensus thresholds will simply not be accepted by the majority of Pillars. Leading the ones who do to fork themselves out.

[0x3639](https://forum.zenon.org/u/0x3639)

September 9, 2022, 11:11am  10

Romeo States

[![Image 108: image](https://forum.zenon.org/uploads/default/original/2X/1/1124a0f165d563c32172bf5fbbc25d30d9e64242.png)](https://forum.zenon.org/uploads/default/original/2X/1/1124a0f165d563c32172bf5fbbc25d30d9e64242.png "image")

Pillars who engage in the process will be available through public contact information. We can make that a stated requirement to host a repo.

This proposed process is far more decentralized and resilient than BTC’s BIP process. BIPs concentrate their entire process in one channel and one repo. It’s one failure point.

Our proposed process distributes that load across multiple Pillars. I hope we can get 5 to participate initially. That means we can loose the participation of 4 Pillars before the process fails. It’s resilient and distributed.

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 11:28am  11

This comments approach sucks. I’m just going to add notes below:

Pillars can host repos in any public channel. It does not need to be Github. They could create a wordpress site and host it there. Or a gitbook, IPFS, bittorrent…

I think we should reconsider the minimum vote needed. What if someone tries to attack the network, or just F with it by getting a pillar and passing dumb ZIPs that only require one Pillar to approve it. Imagine some BTC whale maxi who hates us because we improve the lightning watchtowers… he gets a Pillar and makes life hell. something to think about.

Until tooling is available, we can always use an AZ vote temporarily.

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 11:36am  12

I wonder how taproot set the 90% threshold. I will look into how they decided that number.

[zyler9985](https://forum.zenon.org/u/zyler9985) September 9, 2022, 11:57am  13

I’m not as big-brained as you chads, but here’s my 2 cents on this …

I think they spiked LP rewards to reassure people that they are aware of the issue and will fund people fully eventually. We are close to phase 1 and they are probably going flat out, why spend time and energy fixing something when it may just change again anyway when phase 1 happens?

And Kaine ignored the request … did he? Isn’t it fair to speculate that the core team runs pillars, and they may have already voted to approve Romeo’s work? Maybe the timing isn’t right, and if we wait 3 months then Kaine will respond? Long silences are not anything new from the core team, they operate on their own time and want to wean us off of them.

I share romeo’s concerns about pillar participation, it’s unwise to assume that issue will organically disappear over night. And I share romeo’s other concern about the process possibly being convoluted – there’s wisdom in making things as easy and as simple as possible for people and pillars to follow.

And the point about your proposed process for ZIPs being theoretically far more decentralised and resilient than BTC’s BIP process … can this comparison be discussed more? As what you’re comparing is the ZIPs in theory, vs BIPs in practice … is there any real-world examples that already do basically what you’re proposing? Because when you actually try it, there can be unforseen difficulties and issues which you only learn about from doing it. If there are no analogous real-world examples, why not? Is that because it sounds good, but is not practical for some reason?

Finally, I love the ambition of improving on the way Bitcoin does it, my main concern would be on how practical this is, and do we have a list of unforeseen issues we may run into

For GitHub Submodules to work, the repo has to be on Git, no?

Regarding the BTC maxi whale “attack vector”: That’s not how it works. Nothing will happen if just a single Pillar implements e.g. a Spork. They will only fork themselves out. They can also not spam the community with ZIPs. BUT they could spam the Pointer Repo if it doesn’t have some indexation criteria implemented.

If the Pillar implements a non-spork node upgrade (e.g. a Minor ZIP) it will only affect their own node.

The acceptance vote tooling has zero influence on the network either. It’s just used to gauge sentiment.

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 12:08pm  15

Rather than add a submodule, we could add a markdown file with a link to the repo hosted on IPFS, Bittorrent, etc…

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 12:12pm  16

I’m just thinking about the instance where a Pillar does a bunch of informational / Minor ZIPs that are garbage. They would have a repo full of crap that does not follow the process, etc…

I suppose in that case, the Pointer repo would remove them or notify the community they are a spam repo and to ignore it. They could continue to create spam ZIPs, but the network would ignore them. And no author would approach them to host honest ZIPs. I assume this will happen.

I am concerned about the case where there is a controversial spork that gets proposed at 51% of Pillars. And the network fractures. Think BTC block warz.

But that’s only for the downloadable binaries, no? The specs and code would still have to be hosted on Git otherwise the Pointer can’t index and integrate it into the consolidated ZIP list

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 12:23pm  18

Yes, hosting the code on Git and referencing it with a submodule is idea. I don’t think anyone is going to post code in a wordpress blog TBH.

I think in the case of informational and some Minor ZIPs, they can easily be hosted anywhere with a pointer from the Main Pointer Repo.

Also regarding Romeo’s original concern about Pillars having the ability to host repos - Many of the Pillars are technical or coders. And many have repos today. I can think of 4 or 5 pillars that already have github accounts. And so long as we have one pillar repo for ZIPs we are in business. Also, if pillars leave or take down github, we can fork or restore their ZIP repos. As part of this process we plan to run a community backup of all repos. I have setup a test implementation here:

[ToKR](https://forum.zenon.org/u/ToKR) September 9, 2022, 12:33pm  19

I don’t think the voting threshold should be defined by the author of a given proposal. Obvious potential for abuse imo. Low thresholds also seem to lend themselves to an attack by a malicious or  
self serving party. (25% pillars with 25% weight could theoretically be just 25%) Maybe a definition of an “active pillar” would help solve the threshold dilemma? Achieving a 90% quorum of active pillars might be possible.

This is great to know - should we include that in the process as “redundancy protocol” or something like that?

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 12:35pm  21

Does anyone know how BTC makes that choice?

Let’s review this: [https://bitcoinmagazine.com/technical/taproot-activation-and-the-lot-debate](https://bitcoinmagazine.com/technical/taproot-activation-and-the-lot-debate)

Look at the debate. very interesting. They developed BIP8 and BIP9, two methods for activation. Debated the hell out of it. I’m wondering who actually said, we are using BIP8 or BIP9 for activation.

I think the lesson here is there was LOTS of debate over how to activate taproot.

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 12:38pm  22

Ya, I think we can add that. Would be nice for a few community members to do it.

I think this is really the key decision point for this and any future ZIP.

For Acceptance thresholds.  
For Activation thresholds.  
Depending on the type of ZIP.

What is too high or too low now? What will be too high or too low in the future?

[vilkris](https://forum.zenon.org/u/vilkris) September 9, 2022, 2:01pm  24

First of all, thank you for all the effort you guys have put into this. Lots of good ideas. I have a few questions/comments specifically related to Stage 4 and the community vote.

1.  Expecting at least 2/3 of all participating ZNN weight to be active, informed and willing to vote on proposals is quite a tall order. The correct threshold in such a voting process is obviously hard to define but will anyone really respect the vote results if the turnout is way below the threshold on a reasonable proposal?
    
2.  Who has the authority to validate the results of this community vote? What happens if a majority of Pillars signal yes but the majority of the total ZNN weight signals no?
    
3.  I assume that running this tool that determines the signalling results will require you to run a node for every blockchain that ZNN can be bridged to. If we build bridges to multiple other chains the tool could end up requiring a considerable amount of computing power and would not be something that could be easily run by community members.  
    Can the effort required to develop, maintain and run such a tool become a risk for this proposed ZIP process?
    
4.  Will this tool be able to retroactively prove the results? As in will it be able to give the balances of all signalling addresses from all supported chains at the acceptance snapshot height?
    
5.  How exactly are liquidity positions accounted for on different chains? As you know liquidity providers don’t hold wZNN, they hold a token that represents a share of the pools combined funds.
    

These are questions we asked ourselves and so far we didn’t feel comfortable in proposing hard consensus thresholds (for both, acceptance votes and activation). What might be too high of a quorum requirement today might be too low in a year. So unless we keep re-voting on fixed thresholds for different ZIP types and stages repeatedly, it might be better to just offer a general reference framework as guidance and leave it up to the ZIP authors to define what they think are sensible quora.

If they’re too low, the community will likely oppose and not accept the ZIP. If they’re too high, sufficient participation might not be achieved.

Ultimately, the only quora that really matter are those of sporks where full nodes agree to change the network. There, the threshold should be at least a supermajority.

Remember, no ZIP process definition can prevent node collusion hence all we do here is agree on best practices.

Regarding your answers on the tool to track and analyze signed messages, I’ll let [@0x3639](https://forum.zenon.org/u/0x3639) answer that one.

But you’re making good points. Might be a lot more pragmatic to exclude LPs.

[coinselor](https://forum.zenon.org/u/coinselor) September 9, 2022, 3:15pm  26

I don’t think we need to account for cross-chain wZNN versions for governance. What percentage of the supply of Proof-of-Stake chains is really living on other chains? I would say what percentage of BTC is living wrapped in ETH but it’s not like BTC holders get to vote for upgrades. Either way, number should not be big enough to become relevant.

People providing liquidity in other chains are incentivized by Orbital program and I don’t think losing their voting power will significantly hurt Zenon’s liquidity. In the event that they do want their full share of governance, they have the option to break the LPs, bridge back to Zenon, vote, then provide liquidity again when the vote process is over.

I will skip the tool altogether for now. Perhaps a simple version of the tool to also account for LPs network participants and their acceptance/support of the ZIP would suffice, but as an off-chain (to NoM) signaling not to be included in the official vote counting process.

I will have to second ToKR’s position of defining an ‘active pillar’ and trying to achieve a 90% quorum of active pillars as the way to go. As much as my gut is telling me the remaining flexible approach early in for Zenon is the way to go, a flexible quorum defined by ZIP authors seems troublesome.

[Dumeril](https://forum.zenon.org/u/Dumeril) September 9, 2022, 3:17pm  27

I note that Romeos proposal was practical and achievable. He also wanted to build on it, once it’s implemented. I.e. in the spirit of „progressive decentralization“ which is now our network motto. Whereas where you’re going now, finding the optimal solution first before moving, we’re on the realm of theoretical solutions that won’t work in practice, I would guess.

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 3:42pm  28

I think what we are proposing is similar to Romeo’s original proposal, only we are replacing one central editor / repo with multiple editors / repos hosted by Pillars.

So if only one Pillar participated in the process, this is basically the BIP / Romeo process, with the Pillar as the central editor. We have a few unique features in addition to the BIP/Romeo process, but at the core, they are similar.

Do you disagree with that assertion?

[0x3639](https://forum.zenon.org/u/0x3639)

September 9, 2022, 3:49pm  29

The way I’m thinking about the voting tool, until it can be moved on-chain, is the following:

1.  It’s centralized on a website
2.  Someone adds the ZIP number and link to the ZIP into a voting “module” on the website
3.  For a pillar to vote, it’s identical to how you modify your Pillar profile on zenon.tools. The tool creates a random UUID to vote. The Pillar signs a message with that UUID to vote yes or no in syrius and pasts into the site… The Tool can keep a running total of yes/no notes and a weighting (by sum of delegators) updated every 10 minutes or so.

[![Image 109: image](https://forum.zenon.org/uploads/default/optimized/2X/6/67264835343e58e354040b82bcc9d86f873f46b9_2_690x479.png)](https://forum.zenon.org/uploads/default/original/2X/6/67264835343e58e354040b82bcc9d86f873f46b9.png "image")

4.  Once the Block height is achieved, or we hit some threshold for measurement defined in the ZIP, the tool takes a snapshot and reports the final results.

This obviously has holes in it, but without moving the vote on chain, I could not think of a better / faster way of doing this. Open to new ideas!

[DrD3](https://forum.zenon.org/u/DrD3) September 9, 2022, 3:54pm  30

Just to see if I understand correctly, are we employing a ‘Token weighted voting’ system based on the amount of Zenon held by the individual? I’m not the biggest fan of such a system as it grants greater voting power to pillars/sentinels and other large whales. A more decentralized and fair approach imo would be to utilize a ‘One wallet, one vote’ system.

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 3:55pm  31

I was thinking that if we have a weighted vote, the denominator is the sum of all delegation, not the sum of all ZNN.

The numerator would be the sum of all delegated ZNN voting yes

So a weighted yes vote = (Sum of ZNN delegation to Pillars voting yes / Sum of all delegated ZNN)

This would exclude wZNN all together.

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 3:59pm  32

I think we are discussing a weighted voting system based on ZNN delegated to Pillars, NOT ZNN held by wallets.

I hear ya on whale influence. I’m worried it will be hard / impossible to get 90% of Pillars to upgrade and vote on a ZIP. If the vote is 90% weighted based on ZNN delegation, we can achieve upgrades more easily. Let me run some quick calcs are report back.

Agreed on excluding wZNN, but why exclude sentinels and stakers?

[DrD3](https://forum.zenon.org/u/DrD3) September 9, 2022, 4:03pm  34

Alternatively, to ascertain/assess the community’s support for a particular ZIP we could **temporarily** make use of an already existing voting system like [snapshot.org](http://snapshot.org/). Seeing as how wZNN is already compatible with metamask- all it would take is for someone to set up an ENS server and create a “space” on snapashot.

‘Admin’ status can be granted to _pillars_ and ‘author’ status to _ZIP proposers_ who must find pillar support to propose a ZIP to begin with. The advantage here being that everyone owning some ZNN would be able to connect to snapshot through their metamask wallet and vote.

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 4:05pm  35

If we did a weighted total at 90% of ZNN delegated to Pillars, the top 29 or 30 pillars could spork the network.

|  |  | Delegated | Cumm Sum | % Total |
| --- | --- | --- | --- | --- |
| 1 | SultanOfStaking | 237,281 | 237,281 | 6.40% |
| 2 | QSR | 196,874 | 434,155 | 11.71% |
| 3 | ElderZ | 182,959 | 617,114 | 16.64% |
| 4 | tapwoot | 171,197 | 788,311 | 21.25% |
| 5 | ZenDAO | 165,125 | 953,436 | 25.71% |
| 6 | [DeeZNNutz.com](http://deeznnutz.com/) | 162,057 | 1,115,493 | 30.08% |
| 7 | Zed | 161,287 | 1,276,780 | 34.42% |
| 8 | ZenonOG | 150,495 | 1,427,275 | 38.48% |
| 9 | AlienBoyz | 145,059 | 1,572,334 | 42.39% |
| 10 | WaXe | 143,198 | 1,715,532 | 46.25% |
| 11 | apestrongtogether | 135,419 | 1,850,951 | 49.91% |
| 12 | WAGMI | 132,542 | 1,983,493 | 53.48% |
| 13 | bigdickenergy | 122,206 | 2,105,699 | 56.77% |
| 14 | Zygonidz | 121,858 | 2,227,557 | 60.06% |
| 15 | Toker | 117,941 | 2,345,498 | 63.24% |
| 16 | Vopo | 102,947 | 2,448,445 | 66.01% |
| 17 | Elements | 99,253 | 2,547,698 | 68.69% |
| 18 | Shigo | 95,987 | 2,643,685 | 71.28% |
| 19 | SolarSail | 89,194 | 2,732,879 | 73.68% |
| 20 | Asgardians | 74,618 | 2,807,497 | 75.70% |
| 21 | ZenonORG2 | 67,327 | 2,874,824 | 77.51% |
| 22 | ZenonORG | 66,685 | 2,941,509 | 79.31% |
| 23 | AncientPillar | 66,626 | 3,008,135 | 81.11% |
| 24 | EmeraldCap | 66,280 | 3,074,415 | 82.89% |
| 25 | StakeServe | 66,268 | 3,140,683 | 84.68% |
| 26 | Mariposa01 | 66,095 | 3,206,778 | 86.46% |
| 27 | Octopos01 | 66,061 | 3,272,839 | 88.24% |
| 28 | AREA51 | 60,902 | 3,333,741 | 89.88% |
| 29 | Nomverse | 57,742 | 3,391,483 | 91.44% |
| 30 | 707 | 57,498 | 3,448,981 | 92.99% |
| 31 | GreyZ | 46,659 | 3,495,640 | 94.25% |
| 32 | ZenonORG4 | 26,167 | 3,521,807 | 94.95% |
| 33 | Unizen | 25,297 | 3,547,104 | 95.64% |
| 34 | [alien-valley.io](http://alien-valley.io/) | 22,112 | 3,569,216 | 96.23% |
| 35 | ZenonORG3 | 20,670 | 3,589,886 | 96.79% |
| 36 | Zeus | 14,743 | 3,604,629 | 97.19% |
| 37 | Zaulus | 13,799 | 3,618,428 | 97.56% |
| 38 | Milkdromeda | 12,822 | 3,631,250 | 97.91% |
| 39 | Zaurum | 12,360 | 3,643,610 | 98.24% |
| 40 | invictus | 11,996 | 3,655,606 | 98.56% |
| 41 | Zircon | 10,397 | 3,666,003 | 98.84% |
| 42 | Paradox | 8,199 | 3,674,202 | 99.06% |
| 43 | CH405 | 8,178 | 3,682,380 | 99.28% |
| 44 | ZENON.NETWORK | 7,772 | 3,690,152 | 99.49% |
| 45 | XYZ | 7,342 | 3,697,494 | 99.69% |
| 46 | Hybrid21 | 5,302 | 3,702,796 | 99.83% |
| 47 | LT | 3,663 | 3,706,459 | 99.93% |
| 48 | Inception | 1,230 | 3,707,689 | 99.97% |
| 49 | Swagmi | 1,000 | 3,708,689 | 99.99% |
| 50 | SPillar | 243 | 3,708,932 | 100.00% |
| 51 | ChadassCapital | 0 | 3,708,932 | 100.00% |
| 82 | zamiri | 0 | 3,708,932 | 100.00% |

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 4:11pm  36

Good question. When someone delegates to a Pillar they are saying, I support my “representative / Pillar” . Like a local senator. If the Pillar votes in a way the delegator does not like, the delegator can voice opposition by moving to a different Pillar. And that can happen BEFORE a final vote is tallied up.

Stakers are unable to make that signal. So I’m not sure exactly how their vote would be considered. I see them as agnostic. They are indifferent by choosing to not delegate.

Not sure on sentinels. We don’t know how they work exactly, so I excluded them for convenience.

[Dumeril](https://forum.zenon.org/u/Dumeril) September 9, 2022, 4:28pm  37

At the core, you’re trying to define a zip process, so there’s the similarity.  
You’re starting differently though, theoretical not practical. I agree with everyone who said it’s convoluted, and also e.g. doubt that you will achieve 2/3 majority in the foreseeable future.

But I haven’t followed each individual argument here, so maybe you’re over that already, it was just an observation.  
I think it’s beneficial to start with what can work immediately, so I said whatI said to remind you of that; it’s easy to forget over all the discussion of details.

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 4:44pm  38

I agree 100%. I do think we will start with one pillar in this process. So in that regard we will start like the BIP process. We will screw it up, and figure out what does not work. We will fix it after a few iterations. Once we have a process that works, I think other Pillars will join in. And laying out the framework now to allow for other Pillars to join in the future will be easier to implement IMO.

I think we still need to work out how ZIPs get approved.

*   Who sets the threshold approval amount
*   How are votes added up
*   Are votes weighted. If so, how?
*   Etc

replying to shazz’s reply

if it is the case that at least 50% of pillars need to adopt the code (otherwise pillars are forking themselves out of the network), what is the point in allowing for a zip to choose a _passing rate_ of <50%?

seems like in no world would that be a pass, so why let that be an option (referring to \>25% of pillars AND \>25% of delegation weight)

unlike other comments, I’m okay putting some technical onus on pillars, but I don’t like idea that you need a pillar to sponsor a ZIP… anyone should be able to propose a ZIP

lets assume ZNN success beyond our wildest expectations… pillars will be worth hundreds of millions, and there will be a lot of people trying to get their attention… I believe that good ideas can come from anywhere, such that we shouldn’t limit an idea by a requirement of being able to get attention from a pillar

As such, I think anyone should be able to propose a ZIP, and then pillars can choose whether or not to _co-sponsor_ it

We need to differentiate between different zips. Not all of them rely on activation by pillars. Some purely informational zips, like this very first zip, rely on community wide consensus, not just pillar acceptance. And there’s no technical activation for informational zips.

It’s just a process to signal agreement. Hence why most if not all of the community should be able to signal their support through a signed message. The consensus threshold can be lower, in return. But excluding certain entities out of the gate would not be right imo.

For Sporks that rely on pillar activation, I agree, then weighted by delegation could make more sense.

to take a lesson from cosmos community (where they have similar concept of validator and staker), by default, the your vote goes with the validator you stake with… BUT if you don’t like their vote or feel passionately, you can vote directly… the direct vote overrides the vote of the validator

to znnify this, if your delegate to a pillar, you vote with that pillar be default, but you can override that vote by also having the option to vote directly

in most cases, you should be aligned with your validator and therefore let them vote for you, but in some cases, you might want to override it while still delegating to them

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 5:19pm  43

As much as I hate Gov’t structure, I think we can use it to help us form our structure. I believe anyone should be able to come up with a ZIP. Anyone can author, just like in the US, anyone can write a bill. But to introduce a bill to congress a Rep or Senator needs to sponsor and introduce it for consideration. A lobbyist cannot introduce legislation directly for debate.

As the “main” economic actors and representatives of delegators, I do believe Pillars should sponsor ZIPs for consideration. Without a sponsor, how will an author convince Pillars to take it seriously?

Thoughts?

this is age old debate of voting by population weight or voting 1 per state… US decided to go with a hybrid approach

I think for where we are now, we go with pure weighted voting system… yes, whales can influence. yes, control is not fully decentralized as a few can have an out-sized impact. BUT, if you do 1 vote per wallet, whales can just create a ton of wallets as well

ultimately, a decentralized ID service can be built on znn at which point we can discuss a hybrid approach. but for where we are now, we want those with the most at risk to be able to steer the network

Acceptance votes based on ZNN holdings per address (irrespective of staking, delegating, sentinel, pillar) eliminates this issue.

Again, a differentiated approach is needed since e.g. for sporks Pillars are the ones to ultimately activate it. So they should have a higher weight during the Acceptance vote to signal to other Pillars if they’re willing to support Spork activation.

For informational ZIPs on the other hand, the process ends at stage 4 and there is no reason whatsoever to limit voting participation to Pillars and delegators.

[ToKR](https://forum.zenon.org/u/ToKR) September 9, 2022, 6:06pm  46

Seems to me that a 2/3 (by weight) supermajority of pillars should carry the day in terms of making decisions. With a preliminary vote prior to the final to allow people to potentially pull their weight from a given pillar or to pull LP zennies out and delegate for a close final vote.

If I understand correctly for a spork there would also need to be a simple majority of pillars in agreement and willing to accept the change for it to move forward so that would really be the final tally to achieve a successful change.

Excited to see us moving in a common direction.

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 7:00pm  47

Idea, what if we removed the discussion about how a spork gets activated and refer to a to be debated ZIP to address the process. Today, we cannot activate sporks ourselves.

Bitcoin did this with BIP 8 & 9.

This is a difficult topic that requires mechanisms that do not exist today.

agree with this sentiment… if things can’t be done today with current tooling, punt on it, and implement MVP version today

you bring up a good point… if you assume success, at some point you’ll need to filter out proposed ZIPs or there will be hundreds per day

govt does this by requiring a rep or senator to propose their bill

early on, that will work for ZNN as it will be easy enough to get in contact with pillars… what if over time it becomes hard? in cosmos, they have a $ filter… so in order to propose (equivalent of) a ZIP, you have to put up a certain amount of money… if “no with veto” is the result, you lose the money

I like a version of this where there is a $ threshold (risked money) in order to propose a ZIP that anyone can ‘sponsor’… so an individual can put up money themselves or have a group or sentinel/pillar put up for them

that said, in effort to get something in place that will work now, I’m okay with funneling things through pillars, but do worry about its long-term viability

NoM Phase 1 activation will be through a spork iirc.

What are the elements you want to leave out? Better we already discuss and dig deep now than to try and take shortcuts if we have to address them anyway by November, no?

[0x3639](https://forum.zenon.org/u/0x3639) September 9, 2022, 8:30pm  51

I was thinking the core team will activate Phase 1 via the current method - hard coded address. That is the only way a spork can get activated today.

Maybe we can acknowledge that assumption and say we need to discuss and debate a method to remove that hard coded address and come up with a new method for future sporks.

Look at all the debate around BIP8 and 9. That discussion latest years I believe before they settled on a method to adopt Taproot.

Just a serie of observations about how a weighted vote with ZNN could lead 29 out of the 30 top pillars to fork the network:

*   This is a decentralization issue if implemented with a naive approach.
*   A quadratic voting system could mitigate this issue by undermining top pillars power.
*   As it is now it already can be seen as a problem but what would it be if big players with billions join ?
*   I agree with the idea of direct voting in case your pillar doesn’t align with your opinion. Override should be an option.
*   I disagree with the need to emulate a government. Our democracies have been built when the fastest communication system in place was the postman and we had noway to reach a consensus among thousand of people all across the countries. Not the case anymore.
*   Furthermore we could even think about a direct voting on ZIPs coming from anyone but pillars could have a weighted veto here, not a weighted vote. See it as a flipped lutte des classes.
*   If we want to craft a good governance system it could be interesting to see what have been done and what failed before. Direct democracies are utopias deeply rooted in the crypto ethos. There was a project about decentralized identity protocol on Zenon but I can’t find it back. This would deactivate the company shareholders voting style. Vote with your voice, not your coins ; the richest aren’t always the smartest, especially when it comes to protocols upgrades.

Food for thoughts.

It seems likely the team would be very interested in making Phase 1 protocol upgrades thru the community activated spork process instead of how they did it in the past where they control the spork address.

Were coming up on some big changes and a key measure of actual decentralization(also many other factors) nowadays seems to be around the central control of a network so heres the opportunity to prove it imo.

All the discussion about implementation zips or informational is absolutely valuable and i dont mean to be a shit disturber but that honestly seems like its outside the scope of our current problem.

Hate to be the kaine simp here but the last thing he said was,

“We need the ZIP format to advance protocol upgrades”

Not saying we have to blindly follow him i just agree with what he has identified as the problem.

The team being interested in this or that is about assumption and should not matter. Never. They’re just signaling silence and we could as well assume they’re just hard at work and doing they’re thing, as usual.

alright I made a bunch of edits based on community feedback:

*   streamlined the text where possible
*   changed terminology describing different zips
*   included acceptance and activation consensus thresholds for different zips and their respective stages
*   updated graphics

please review

[ToKR](https://forum.zenon.org/u/ToKR) September 10, 2022, 5:57pm  56

Why vote by pillars “and public nodes” for spork? Couldn’t a supermajority of pillars just make a change of their own accord and bypass all of this anyway?

Isn’t governance by pillars outlined in white paper? Pillars should be invested parties who participate in the maintenance of the network. Is there anything to prevent a group of ZNN holders who feel underrepresented from getting together and erecting a pillar.

Sentinels’ role in the network is still undefined as I see it but their contribution is by definition less than that of a pillar. Maybe in the future these parameters can change depending…

No you’re totally right. I just remember that for the last spork kaine said public nodes had to upgrade their software for the fork to activate.

Iirc most public nodes are pillars anyways until sentinels go live.

But yeah I think for the sake of simplicity and also because they have the most skin in the game it should just be pillars. I’ll change it accordingly.

Thanks for pointing this out!

[0x3639](https://forum.zenon.org/u/0x3639) September 10, 2022, 6:22pm  58

ya I think you are right. I had to upgrade my public nodes and pillar last time.

[0x3639](https://forum.zenon.org/u/0x3639) September 10, 2022, 6:25pm  59

I think we should discuss the voting thresholds and who votes. To me it seems more clean for the Pillars to vote and use some weighting system based on delegation. If a delegator / ZNN holder does not like the Pillar’s vote, they can move to a new Pillar for their voice to be heard.

I do think we need to be careful allowing 29 or 30 pillars out of 80+ to fork the network. the Threshold can be a combination of delegation weight + number of pillars.

Something to think about.

I disagree tbh. For three reasons:

1.  Pillars can and do self delegate large amounts and will thus significantly skew the effect you desire
2.  delegators have proven not to care about governance. Their main concern is yield. Remember how many delegated to the passive pillars who never voted for AZ?
3.  Not all ZIPs require activation by Pillars, hence other network participants should have a vote too

[0x3639](https://forum.zenon.org/u/0x3639) September 10, 2022, 6:40pm  61

True. I expect ZNN holder participation to be even lower than Pillars. How would we count their vote in a way that does not require X% participation of ZNN holders to take action?

I have to agree with the delegated weight being a stronger/more reliable long term as a means of showing support.

[0x3639](https://forum.zenon.org/u/0x3639)

September 10, 2022, 6:49pm  63

Throwing out an idea here regarding Informational ZIP voting…. Given each Pillar runs their own “BIP process” we can see each Pillar as their own “central editor”… what if the Pillar decides when they Accept an Informational ZIP only. They mark it Accepted after community debate and revision. Then the Pillar asks the community to vote on it which simply gives it “weight”. The more ZNN / Pillar holders that vote YES on it over time gives the ZIP more weight. We can come up with some weight algo that takes into account, Pillars, Delegators, Sentinals, and ZNN holders.

Thoughts? This would apply to informational ZIPs only. Also, that would allow us to publish some NOW without the voting tool being ready now.

[![Image 110: image](https://forum.zenon.org/uploads/default/optimized/2X/e/e0db49ae5e1dbeec667fc1df5c58db86783d3120_2_690x338.jpeg)](https://forum.zenon.org/uploads/default/original/2X/e/e0db49ae5e1dbeec667fc1df5c58db86783d3120.jpeg "image")

Yeah thats fair, but there was some clear communication on this task so imo its hard to ignore it.

Given the currently relatively low engagement and the fact that informational ZIPs can easily be amended or changed I’d agree with an approach that reduces the bar for acceptance/activation of these kind of zips.

However, I doubt people will have any inclination to vote once a ZIP has been deemed “accepted” unless it’s very easy to do and they’re incentivized to.

On the other hand, if the acceptance threshold is too low, they might even refuse to accept it as a legitimately “voted in” ZIP and simply ignore it.

Since this ZIP potentially defines the general process of any future ZIPs it would be good to have sufficient consensus to prevent it being continuously challenged and ending up in a messy, non-standardized approach to ZIPs.

Just some thoughts

I don’t know if I am sold on delegated weight = voting power at this stage. I was hoping to see some of this when AZ rolled out and was initially disappointed but in retrospect I think the team built AZ approval process to meet the community / pillars where they are - not where they want them to be for the simple goal of not stalling. Also, I am very skeptical that we will ever reach a point where people give up profits because a pillar didn’t vote to their liking (this is just my personal view on human nature). I fully agree the more complex we make this the less people will engage with it. To Dumerils point (I think) we don’t need to make it perfect, just be good enough to move forward and learn from.

[0x3639](https://forum.zenon.org/u/0x3639) September 10, 2022, 10:21pm  67

I think I agree. I don’t think we are ready for delegated weight.

Maybe a modified delegated weight. I am a little concerned we can get 50% of all the online pillars to do anything. Remember the last upgrade? A very large number of Pillars were forced offline somehow in order to upgrade.

I realize this post probably isn’t that helpful… but in general I think a lot of this could be MVP1 MVP2 type thing. Sponsoring pillar is an interesting idea but by no means required for MVP1 to work as an example.

[0x3639](https://forum.zenon.org/u/0x3639) September 10, 2022, 10:23pm  69

What is MVP1?

Maybe we need another block 27070 to knock everyone out so we can get a sense of how many are actually monitoring their pillars ![Image 111: :slight_smile:](https://forum.zenon.org/images/emoji/twitter/slight_smile.png?v=12)

Agile development / story mapping technique. MVP1 minimum viable product to deliver some increment of value and open the feedback loop - MVP2 next highest feature request and so on

[Reeeee](https://forum.zenon.org/u/Reeeee) September 11, 2022, 12:49am  72

I am going to collate some thoughts here:

What is the deal with the spork address?  
Can we get someone to look through the code and do some detailed research on how this works?  
I feel like we are missing something.  
Mr Kaine said everything is already in place for the community to build, so maybe we are just assuming the devs are in control of that address.  
Maybe they are and maybe that changes in Phase 1.

Personally I think they have a user activation method for sporks planned or already in place.  
They have stated in the light paper their goal is for a network that has no single points of failure.  
I think part of their emphasis on users running nodes is because that makes them sovereign network participants, I think the governance consensus is based on this.

So the next thought is, embedded smart contract calls.  
I’d like to know more about the scope and scale. Do we envision a time where there may be hundreds or thousands of these functions implemented at the protocol level? Or are they reserved for specific scenarios?

What are the performance implications? Could a function that behaves unexpectedly cause problems for the broader network or are they encapsulated?  
Could it be that the reason why the nodes are crashing or running up high RAM usage after some time is because an embedded function is causing this?

I think protocol level functions are very cool, in terms of security and performance, but why should the community get to vote if it gets implemented? That seems like unnecessary bureaucracy, unless we have a ceiling on the amount of functions that can run embedded.

What we really need is a test net. If somebody can present their function working and not breaking on a test net there should be no need to go through the lengthy process of zips and voting. We need to make sure we don’t create voting and governance fatigue.

I think we should try to stream-line the process for technical improvement proposals and additions.  
If it doesn’t change fundamentals and does not interfere with existing functionality and can be shown to work on a test-net - why create roadblocks?

If somebody proposes a ZIP that wants to change fundamental constants then we can debate that and have votes and safeguards and all of that.  
But if somebody just wants to implement some functions for the Dex they are building do we really need all this formality?

Anyway that’s just a few thoughts.

Apart from the Pointer Repo and the consensus thresholds, the process described above has been pretty much tried and tested with BIPs. It’s just explained in more detail…

We initially tried to account for potentially low voting participation by leaving it up to the ZIP authors to specify consensus thresholds on a ZIP by ZIP basis. But some people disliked the idea.

I am still in favor of this since it provides the necessary flexibility and prevents the framework from being too rigid.

To prevent misuse, participation thresholds can be set - the lower the necessary quorum the higher the necessary participation threshold, for instance.

BIP process specification also does not impose any consensus thresholds btw.

If we kept that flexibility, the MVP 1- n approach would be possible. After all this informational ZIP isnt enforceable anyway. It’s just a document we can vote on to say we have found an agreement on the standard procedure to do these things.

I would probably mention in the ZIP type description that these thresholds are just recommendations and not mandatory for ZIP authors/sponsors.

[Dumeril](https://forum.zenon.org/u/Dumeril) September 11, 2022, 6:11am  74

There’s a thread somewhere here where I explained how sporks work. The address is defined with genesis. Check out zenon/zenon.go, zenon/config.go and chain/store/gensesis.go.

I think one idea with embedded contracts is exactly to prevent broken contracts from being executed; i.e. it’s safe environment by definition where only known code with known requirements is executed. As long as there’s no defect in those of course. But that’s relatively easy to monitor, compared to potential user level contracts.

[Reeeee](https://forum.zenon.org/u/Reeeee) September 11, 2022, 6:54am  75

I wonder though what the scope is that was intended for the embedded contracts.

On the one hand we will have SC runtimes for user level at some point and then we also have uni-kernals for zApp runtimes.

So in the long run where does that leave embedded contracts ? Considering they require sporks to integrate and be used they will need a zip. I think we need a sub-process that deals entirely just with embedded contracts.

I think the embedded contract may also be used to configure the unikernal

[Dumeril](https://forum.zenon.org/u/Dumeril) September 11, 2022, 7:37am  76

I think unikernel and smart contract runtime (vm) would be mutually exclusive concepts. Zapps would run on the scr, whether that be unikernel tech or wasm or anything else.

Or why do you think unikernels are a distinct concept?

[Dumeril](https://forum.zenon.org/u/Dumeril) September 11, 2022, 8:08am  77

The distinction I make in my head between embedded and non-embedded smart contracts is that the former implements functionality that’s not absolutely necessary for the p2p tx routing and consensus core, but still somewhat protocol level extensions of that. You could say, looking at the network, these contracts implement defining characteristics of zenon, but they are still extensions beyond the pure ledger.

External smart contracts would not have that characteristics; they are user level applications.

There should rarely be the requirement to add another embedded contract. If possible to implement in “user space”, it should never be done in “kernel space”.  
As you hinted at, there’s a big risk involved with these contracts. They are not running in any sort of isolated environment, unlike the potential external smart contract.

I’m not sure if it would be possible to elevate one or the other existing ecs to external contracts at all, but one reason they exist in the first place is probably the simple fact that you don’t need to adapt a vm to implement and run them. Functionally, they could have been bound more directly into the core code, so I guess it was at least in parts an architectural decision of system design to add this concept of embedded vm. And a nice one.  
Following that thought I agree with you when you think ecs should be treat separately. It’s probably a good idea to maintain the structure they gave to the code in every process that’s being designed on top.

[Reeeee](https://forum.zenon.org/u/Reeeee) September 11, 2022, 8:58am  78

I’m not sure, but I think part of the reason for unikernals is to fragment global state for all zApps. Like with EVM there is just one monolithic state, so maybe unikernals is a kind of sharding for global state.  
And maybe they can act as Oracles of sorts too.

I think it said in the whitepaper that a special transaction can be sent to a unikernal to configure it.  
That would probably happen with an embedded contract. Maybe in this way the unikernals can be customized, permissions and runtimes set and even whole programs loaded.

[Phuong](https://forum.zenon.org/u/Phuong) September 11, 2022, 9:42am  79

Not to go off-topic, but I was curious what you guys think about this project’s upgrade process since they have some similarities to Zenon:

[https://medium.com/koinosnetwork/the-worlds-simplest-dao-d6c1f65f8292](https://medium.com/koinosnetwork/the-worlds-simplest-dao-d6c1f65f8292)

[Dumeril](https://forum.zenon.org/u/Dumeril) September 11, 2022, 10:00am  80

I had a quick read and it sounds not so different from what we have. As I understand it, their system is based on sporks as well (which can be both hard- an soft fork in traditional semantics), but the activation method is not fixed and limited to an address hard coded with network inception, but (probably) configured with each individual proposal? I think it’s not stated explicitly in that article, but that is how I understand it.  
That’s a nice twist as well; each spork can be activated by the proposing address or optionally a different one, if configured so.

Regarding votes, they seem to be very optimistic: each non-vote is a no-vote.

[Dumeril](https://forum.zenon.org/u/Dumeril) September 11, 2022, 10:12am  81

Tbh, it’s an interesting thinking and unfortunate that the team does not care to elaborate on how they see the role of unikernels wrt smart contracts / vm implementations now. But to me it currently sounds unnecessary, as I think what you describe could be done with just smart contracts as well. Possible though that I’m not getting the full picture you have in mind.

[0x3639](https://forum.zenon.org/u/0x3639) September 11, 2022, 10:19am  82

A consistent theme in the feedback is keep the process simple. The World’s Simplest DAO framework looks pretty simple. And I like that.

At the core, we are proposing the BIP process. Not sure if that process is “simple” but it’s proven. That process can be run by any pillar who choses to engage. As more Pillars engage, the more complicated it will get BUT will also get more resilient and decentralized.

For me, the voting mechanism is still in question. I feel like Authors should be able to propose the threshold level with some minimum requirements.

Also, I continue to question Informational ZIP approvals. I don’t think they should need a vote. Voters could get vote fatigue IMO. They need rigorous debate, like we are having here. But once that debate is done, why can’t a Pillar publish them without a vote? Like the BIP process. And to prevent Spam, maybe a Pillar needs to donate ZNN to the AZ framework for the community to consider them complete.

[Dumeril](https://forum.zenon.org/u/Dumeril) September 11, 2022, 10:24am  83

These are zips for initiatives that don’t change code in any way right? Then I agree, don’t see the necessity for this category at all in the process.

[0x3639](https://forum.zenon.org/u/0x3639) September 11, 2022, 10:31am  84

Correct. But I do think they have a place. This ZIP Process framework is an informational ZIP. There might be things the community wants to announce to users that need an Informational ZIP.

BIP9 is an informational and technical in nature:

I also think informational BIPs / ZIPs can lead to important code changes.

[Dumeril](https://forum.zenon.org/u/Dumeril) September 11, 2022, 10:35am  85

Ok but then we would want to have consensus on that

[Phuong](https://forum.zenon.org/u/Phuong) September 11, 2022, 10:36am  86

Does being sympatico with the BTC ethos mean we need to follow their upgrade processes? I know it’s tried and true, but is it suitable for where ZNN is at the moment? Just playing devil’s advocate - I won’t pretend to now the answer, but I thought I’d ask.

Another consideration is how to motivate inactive pillars to participate in governance. Maybe it’s something I missed, but where is the proverbial boot to the ass that will get them to join the top 30 or so and actually do stuff?

[0x3639](https://forum.zenon.org/u/0x3639) September 11, 2022, 10:38am  87

OK. So you think voting on these informational type ZIPs is important?

[Dumeril](https://forum.zenon.org/u/Dumeril) September 11, 2022, 10:41am  88

If we consider the zip currently in discussion informational, yes, I think there should be voting on it

[0x3639](https://forum.zenon.org/u/0x3639) September 11, 2022, 10:46am  89

Good point. In all honesty I think we tried to build on the work / research Romeo did. He researched BIPs / EIPs, etc… and I believe his original proposal followed the BIP process generally. So we tried to build on that work but propose a structure that did not need a central editor.

I did not look carefully at the other blockchain improvement procedures. But I’m happy to review any that folks think are relevant!!

[Reeeee](https://forum.zenon.org/u/Reeeee) September 11, 2022, 10:47am  90

Not to get too off topic.  
But I think it’s possible that with unikernals you can bypass the browser for dapps.

Like you have a game written in C++ and it installs with a unikernal module that is customized for the game and then you could have token economies and nfts and maybe other data structures all running natively in the game.

and then this sort of concept could be used for any kind of application.  
Instead of accessing “web 3” through a browser like with other blockchain platforms, unikernals could let applications use web 3 directly without all the constraints that browsers and scripting languages bring.

Just wanted to add that for a voting structure based around the delegated weight i think would help if the top 30 pillar rewards get redistributed more evenly to all pilars. It would help balance out the weight so when delegates want to vote with their coins it could have more impact on a lesser spread accross all pillars.

#Pillardown

[Dumeril](https://forum.zenon.org/u/Dumeril) September 11, 2022, 11:12am  92

Hm but the browser in web3 is needed on the side of the user to interact with the contracts. Unikernels were proposed to be run by the nodes, so it has nothing to do with how the user is able to use the apps.

If we’re talking about the ability to use other languages to build the apps, that’s something that would also be solved with wasm or potentially other stacks, where a library has been built that bridges the gap from user level app to ledger.

But yes, we’re getting off topic

[Dumeril](https://forum.zenon.org/u/Dumeril) September 11, 2022, 2:01pm  93

Fwiw I don’t think Informational is a good label for these kinds of proposals. It’s not just information. Even though it might not be enforceable on protocol level, you want to define a process that’s giving direction to the network, and which you assume, when accepted, will be enforced on the social layer. Don’t know if every possible topic from Informational goes this far (if not, we agree again, why vote on it at all?), but I think Informational is misleading here, and invites to formulation of nonsense zips that don’t need consensus.

Maybe Directional is better?

[0x3639](https://forum.zenon.org/u/0x3639) September 11, 2022, 11:55pm  94

Important Notes from Twitter Spaces:

*   The ZIP framework is simply a roadmap. Community members and economic actors will choose to follow it or not. They do not need to follow it. No one can force them to follow it. They can choose to follow it or create their own process.
*   Informational & Implementation ZIPs should not need a vote. If community members adhere to informational ZIPs over time they will be considered adopted by the community. Maybe we should consider changing “Approved” to “Published” and remove the voting requirement.
*   The intermediate voting steps for Hard and Soft forks are not necessary. The active dialogue about ZIPs and feedback from the community and pillars will give the Author(s) sufficient comfort about support before starting to code. A vote should not be necessary to signal support. The tone of the discussion and feedback publicly from Pillars should be sufficient.
*   [@georgezgeorgez](https://forum.zenon.org/u/georgezgeorgez) recommends that we “recommend” all ZIPs be submitted / introduced a certain way. Similar to the BTC mailing list. We might consider requiring the first submission be on the forum. The forum is run and owned by the community. We can host it ourselves. It’s difficult to take down.
*   Voting for Hard & Soft forks should not be mandated in the ZIP framework. Each update will have different significance, so it’s impossible to know today what should be required. Each ZIP could have a separate discussion about how it will get activated. The Author could propose it but will get debated by the community
*   It’s unclear how Sentinels will play a roll in hard & soft forks and the ZIP process. But their roll will be important as momentums will require PoW links. If a spork activates and Sentinels don’t follow the Spork the momentums will not have Tx in them (did I say that correctly?)
*   The general theme is the network is about opting in. We cannot force anyone to do anything. We should not propose a rigid structure that cannot be enforced.
*   Also, other Pillars can create their own ZIP framework if the one in discussion is too rigid or too lax. Community members might follow it if gets support.
*   Other Pillars can also fork, modify and/or improve the one being proposed now and build community support around it.

[coinselor](https://forum.zenon.org/u/coinselor) September 12, 2022, 12:24am  95

I can see your point about the informational label.

How about procedural? After all, we are establishing the accepted way of doing something.

Made A LOT of edits and updates based on various extensive discussions with community members. Some minor terminology / typo mistakes but should be 98% finalized unless I made some big brain doo-doo

[0x3639](https://forum.zenon.org/u/0x3639) September 18, 2022, 8:10pm  102

Guys if anyone has comments please provide them soon. We are getting ready to post to github next week.

[0x3639](https://forum.zenon.org/u/0x3639) September 23, 2022, 9:38am  103

ZIP:deeZNNutz-0001 published on github for review. We need to clean up the repo and add a pillar signature. Open to comments.

[0x3639](https://forum.zenon.org/u/0x3639)

October 13, 2022, 11:15am  104

Does anyone have an objection to adding this recommendation from [@georgezgeorgez](https://forum.zenon.org/u/georgezgeorgez) to ZIP:deeZNNutz-0001? We can test making a change and updating the change log.

Yes I do tbh. I dont see a reason to add it to the ZIP Process itself, it’s more a general commentary rather than a change or extension of the process. The process is already quite extensive, let’s try not to lengthen it further unless absolutely necessary.

Maybe you can instead cross post it as a comment/reply to the original ZIP post in your git repo.

[0x3639](https://forum.zenon.org/u/0x3639) October 13, 2022, 5:58pm  106

no need to add to the Process. I’ll fork the repo and show you what I’m thinking. Identical to how EIPs do it.
