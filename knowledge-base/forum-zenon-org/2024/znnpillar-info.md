Thread: znnpillar-info
digitalSloth | 2023-02-08 00:17:19 UTC | #1

Hi everyone! I have been lurking here for a while trying to figure out how to apply my skills to the Zenon ecosystem and have come up with the following AZ proposal. Im looking for feedback and opinions before I formally submit it. Please have a look over and let me know what you think, happy to answer any questions you may have. 

---

**Project Name:** ZNNPillar.info

**Description:** The idea is to create a site that monitors a pillars activities, initially voting and reward changes and provide an easy to use interface for viewing AZ projects and a pillars voting history. Users will be able to sign in and pick favourite pillars, subscribe to receive updates regarding reward changes and voting. Pillars will have a page where they can post messages and updates regarding their aims and ethos, this will be achieved via signed messages.

I believe it is vital for everyday users to have easy access to on chain data, this site provides a platform for to facilitate this.

**URL:** [znnpillar.info](http://znnpillar.info) | https://github.com/digitalSloth/znn-php

**Team:** I am a backend PHP developer with a keen interest in crypto. I have worked in the web industry for 8 years now and have been involved with a range of projects from property management systems to e-commerce shops. I am keen to venture further down the crypto rabbit hole and start looking at web3.

> **Phases**

**What is your high-level roadmap?**

I have broken this down into 5 main phases, beginning with the release of the PHP SDK and finishing with a fully functioning site as described in the following phases:

**Phase 1**

High level overview of main tasks:

* Finalise and release ZNN PHP SDK

Completion of Phase 1 will be measured by:

* Fully open sourced PHP SDK wrapping all RPC endpoints

**Phase 2**

High level overview of main tasks:

* Main website lunch
* List and details for each AZ Project and its phases
* A list and search for all pillars voting history

Completion of Phase 2 will be measured by:

* The functionality of the website

**Phase 3**

High level overview of main tasks:

* Charts for historic pillar data - reward changes, uptime and voting participation
* Pillar ratings - taking into account the metrics above create a rating system for pillars
* Notifications - new AZ projects and updates, phase voting reminders

Completion of Phase 3 will be measured by:

* The functionality of the website

**Phase 4**

High level overview of main tasks:

* User login - favourite pillars, notifications for reward changes
* Pillar login - signed message will allow pillars to manage content on their pages

Completion of Phase 4 will be measured by:

* The functionality of the website

**Phase 5**

High level overview of main tasks:

* Public HTTP API endpoints - provide access to the RPC endpoints and the historic data collected by ZNNPillar.info
* Public node

Completion of Phase 5 will be measured by:

* The availability of the API and node

> **Funding**

**Total Requested Funding** = 5,000 ZNN and 50,000 QSR

**Project Duration** = 4-6 months

**How did you calculate your budget?** I estimate this project to take about 200 hours. The additional QSR is so I can spawn a sentinel, this will ensure I can afford the on going costs of the server and provide continued improvements beyond the scope of this proposal. I do not want this to become a forgotten side project so by having a way of funding future improvements and maintenance I hope this becomes a cornerstone of the Zenon ecosystem.

**Project and Payment Milestones:**

**Phase 1**

Funding Request: 20% (1,000 ZNN and 10,000 QSR)

Duration: 2 weeks

**Phase 2**

Funding Request: 20% (1,000 ZNN and 10,000 QSR)

Duration: 1.5 month

**Phase 3**

Funding Request: 20% (1,000 ZNN and 10,000 QSR)

Duration: 1 months

**Phase 4**

Funding Request: 20% (1,000 ZNN and 10,000 QSR)

Duration: 1 months

**Phase 5**

Funding Request: 20% (1,000 ZNN and 10,000 QSR)

Duration: 2 months

> **Other Information**

**Risks, Assumptions, Known Issues, Dependencies:** The only external dependency is for the signed message verification.

**Have you previously submitted a proposal (either in Acclerator-Z or Incubator)?** No this is the first submission.

-------------------------

0x3639 | 2022-05-24 23:02:08 UTC | #2

Love the idea.  Am in full support and don’t have any comments.   Happy to help with testing and beta usage.  Also want to point out to the community @digitalSloth is delivering a PHP SDK too.  So this is a twofer.

-------------------------

alien-valley.io | 2022-05-25 08:07:44 UTC | #3

Regarding phase 4, I would suggest to wait for some extension wallet (or similar). This would allow users to keep their ZNN identity, without needing to create a system for login.

Regarding Phases 2 & 3, personally, I'd much rather like to see them integrated in something existing like the explorer/zenon.tools

-------------------------

digitalSloth | 2022-05-25 12:23:35 UTC | #4

@0x3639 Thanks for the support! I should point out the PHP SDK is not a full SDK like some of the others being developed, it will not support any sending/receiving/wallet functionality as this would require sending sensitive data to a remote server.

@alien-valley.io The idea of using a wallet for identity is great, Id be happy to work with this idea instead although the notifications would require an email address anyway so maybe its best to have both a traditional email/password and wallet authentication?

Regarding integrating phases 2 and 3 into the existing sites I dont see the harm in having the information available in multiple difference places if they wanted to add something similar but currently they seem focussed on different information hence I felt the need for a separate website.

-------------------------

shaimo | 2022-05-25 13:14:56 UTC | #5

I know your experience is mostly php, but any chance to do it with a more modern framework like react/js? It sounds like a great tool and it would be a shame to write it with an obsolete language, only to have to rewrite it again later…

-------------------------

vilkris | 2022-05-25 14:13:25 UTC | #6

I also don’t see it as a bad thing that information is available on different places but I am a bit curious about this in the context of AZ. I did a post of the current status of Zenon Tools and what’s in development now (some features are pretty much the same): https://forum2.zenon.org/t/zenon-tools-wrapping-up-warpdrive-and-whats-next/580

I don’t know yet if I’ll be applying for AZ funding, but if I did and your proposal has already passed by then how would a new proposal that aims to solve some of the same issues be treated by the community?

-------------------------

digitalSloth | 2022-05-25 14:37:10 UTC | #7

Hi @vilkris 

Firstly thanks for all the work you have put into zenon.tool its a great resource. Iv just read your post and didnt realise you are working on some of the same features mentioned in this proposal, apologies if it looks like Im taking your ideas and passing them off as my own that was not my intention. Since the launch of AZ I have been a bit frustrated that the only way to see projects was via a telegram channel so I began to form the idea of this new site.

If you want to apply for AZ funding I am happy to rework my proposal leaving out features you already have planned so we avoid duplication.

-------------------------

digitalSloth | 2022-05-25 14:45:03 UTC | #8

Hi @shaimo, I have to disagree that PHP is obsolete, yes there are more modern languages out there but as a backend for a website and API I believe PHP is still a powerful language to use. The frontend could be built on react but unfortunately thats beyond my capabilities at the moment and would slow the project down but its something to consider for the future.

-------------------------

0x3639 | 2022-05-25 15:18:02 UTC | #9

Just saw this post and wanted to share here: https://forum2.zenon.org/t/zenon-tools-wrapping-up-warpdrive-and-whats-next/580 

@digitalSloth wanted to make sure you saw the progress and potential overlap.

-------------------------

vilkris | 2022-05-25 16:08:48 UTC | #10

Yeah it's no surprise many people come up with the same ideas at the same time - I share you frustration about the difficulty with keeping up to date with AZ.

Like I said I'm not sure if I'll be applying for AZ right now and I can't really guarantee I'll be implementing all the same features you've outlined. Overlapping will happen in some areas but that's not a bad thing in my view. I'll be at least implementing the stuff I presented in my forum post.

-------------------------

digitalSloth | 2022-05-27 16:38:49 UTC | #11

@vilkris Glad to see you've applied to AZ, best of luck with the application.

Im going to rework my application a bit over the weekend and focus less on the features you are planning for zenon.tools so there is less of an overlap. 

However this got me thinking... the info on your pillar profile pages, do you have any plans to create an API so others can access this? As more sites start to popup lots of this info could end up being repeated and it might become a problem for pillars to update multiple websites with the same info. If there was one trusted source with a public API pillars could provide social link, bios, news etc without having to submit it in multiple places.

-------------------------

vilkris | 2022-05-27 17:27:42 UTC | #12

[quote="digitalSloth, post:11, topic:576"]
Glad to see you’ve applied to AZ, best of luck with the application.
[/quote]
Thank you :pray:
[quote="digitalSloth, post:11, topic:576"]
do you have any plans to create an API so others can access this?
[/quote]
All the Zenon Tools pillar off-chain info is available at this endpoint right now: https://api.zenon.tools/pillars-off-chain
At least for now I haven't had any requests from others to use the endpoint but if anyone wants to use the endpoint for their site or app just shoot me a DM. 

I agree that having pillars needing to update multiple places with their information is not ideal and probably one centralized API isn't the best solution either in the long run. Assuming we'll eventually have a VM for smart contracts maybe we could have a SC handle the information in one place?

-------------------------

digitalSloth | 2022-05-30 15:20:46 UTC | #13

Thanks for the link to your API endpoint, will drop you a DM about using it.

Agreed a SC is probably the best solution for this in the future but until then I think an API is better than having multiple different sources of information, unless there are other ideas out there?

-------------------------

sultanofstaking | 2022-06-01 15:03:40 UTC | #14

Have been under the weather so apologies if I have missed some things along the way but I am not sure what this brings in addition to the existing Zenon tools site?

-------------------------

digitalSloth | 2022-06-01 16:38:35 UTC | #15

Hi! Admittedly there are a lot of similarities with zenon.tools given the latest updates and planned features, however I was unaware of these when developing this idea so decided to go with it anyway and let the community decide. The main differences are:

* Email notifications systems (reward changes, AZ updates, phase voting reminders)
* User logins and ability to favourite pillars
* Pillar ratings
* HTTP endpoints for the zenon node
* APIs for the historic data (rewards, uptime, voting) collected by the site
* PHP SDK

-------------------------

sultanofstaking | 2022-06-02 18:59:02 UTC | #16

Got it - at this funding I am going to vote no. I do think we need to expand beyond one single source for this info but think we can use the funds for other work now.

-------------------------

digitalSloth | 2022-06-05 13:57:06 UTC | #17

No problem, thanks for the feedback. I'll still try and get the site running over the next few months despite the AZ proposal not getting approved.

-------------------------

0x3639 | 2022-06-05 14:00:54 UTC | #18

Maybe submit for the PHP SDK?  No one is working on that yet.

-------------------------

DrD3 | 2022-06-06 07:51:36 UTC | #19

Appreciate your willingness to contribute to the network in spite of your proposal not being approved. I for one am looking forward to this site (and who knows maybe once the community sees its value and utility you can apply again in retrospect?)

-------------------------

digitalSloth | 2022-06-07 19:10:30 UTC | #20

Good suggestion, will get that submitted soon

-------------------------

