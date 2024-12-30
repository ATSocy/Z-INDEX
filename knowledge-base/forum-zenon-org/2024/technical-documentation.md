Thread: technical-documentation
aliencoder | 2023-07-01 16:19:36 UTC | #1

What we need right now is a good technical documentation explaining how the network works, how to create embedded contracts, how to setup nodes and what developer tools are readily available. 

I think this is *mandatory for onboarding* more developers to come and build on NoM.

I like this template from [Avalanche](https://docs.avax.network/).

Structure:

- **Learn about Zenon**: Network of Momentum novel architecture and consensus protocol
- **Become an active participant**: spawn a Pillar (validator), Sentinel, or start staking, delegating, and staking liquidity
- **Builders zone**: get started and experiment with the ZNN SDKs
- **NoM Multichain technology**: expanding the NoM universe to new horizons
- **How to launch extension chain**: bring new capabilities to NoM
- **Builders lounge**: get in touch with devs already building on NoM

What do you think?

-------------------------

angelo_a_jr | 2023-06-29 09:29:50 UTC | #2

Yes, was discussing this with @mehowbrainz the other day and he mentioned some plans that leverage Intercom with ZenonOrg materials but we also do have a Docs page already that just needs a lot of TLC.

https://docs.zenon.org/hypercore/

Avalanche one looks great.  Despite their downfall, I always thought Terra was really professional with product and docs (https://docs.terra.money/learn/station/)

Unfortunately I do not have docs experience but I would very gladly support an A-Z proposal for anyone who has docs experience that wants to take the lead here.

-------------------------

aliencoder | 2023-06-29 13:59:05 UTC | #3

[quote="angelo_a_jr, post:2, topic:1529"]
https://docs.zenon.org/hypercore/
[/quote]

Where is this hosted? Can I modify it? 

[quote="angelo_a_jr, post:2, topic:1529"]
I always thought Terra was really professional with product and docs
[/quote]

I'll take a look.

[quote="angelo_a_jr, post:2, topic:1529"]
I would very gladly support an A-Z proposal for anyone who has docs experience that wants to take the lead here
[/quote]

I will definitely need some help, but I can start a documentation right away.

It is *very* important to have it *asap* in order to be able to onboard new developers.

-------------------------

angelo_a_jr | 2023-06-29 14:16:42 UTC | #4

[quote="aliencoder, post:3, topic:1529"]
Where is this hosted? Can I modify it?
[/quote]

cc: @mehowbrainz.

I can contribute to a wallet tutorial section.

-------------------------

sol | 2023-06-29 14:44:54 UTC | #5

This is probably a good starting point.
I think it could be re-organized to help new devs get started.

https://wiki.zenon.network/#!index.md

HC1 has discussed requirements to onboard new devs. It's not a simple problem to solve but good documentation is part of the solution.

-------------------------

aliencoder | 2023-06-29 15:24:20 UTC | #6

[quote="sol, post:5, topic:1529"]
good documentation is part of the solution
[/quote]

Imo good documentation solves 80% of the problem. 

If you know what's going on, and some clear instructions & objectives, you have half of the problem solved.

-------------------------

angelo_a_jr | 2023-06-29 15:26:44 UTC | #7

Can we migrate the relevant pieces of this to the Zenon Docs page to start consolidating?  GitBook docs are a more polished/professional finish

-------------------------

mehowbrainz | 2023-06-30 00:13:47 UTC | #8

My recommendation is the following structure:

Technical documentation: I originally thought we could use Intercom to unify Marketing/Sales/Developer support under one platform while onboarding, but I think the [ReadMe](https://readme.com) platform is more robust for developers, so I'm okay to branch it out from Intercom. Intercom themselves even use it [for their developer / technical documentation](https://developers.intercom.com/intercom-api-reference/reference/identifyadmin). I like how they have a good UX for API versioning too. Feels more organized compared to Gitbook IMO.

Support documentation: Intercom's [Help Centre product](https://www.intercom.com/articles?on_pageview_event=articles_footer). We got access to a startup program as mentioned [here](https://forum2.zenon.org/t/support-documentation/1531/2?u=mehowbrainz).

We intend to use Intercom in all of the zenon.org funnels and landing pages, with automation/bots/human support by community. Will primarily use Intercom by Marketing, Sales and Support.

I can get both setup as:

* docs.zenon.org or developers.zenon.org (using [ReadMe](https://readme.com))
* support.zenon.org (using Intercom [Help Centre](https://www.intercom.com/articles?on_pageview_event=articles_footer))

Please vote on 2 options for devs/support:

[poll type=multiple results=always min=1 max=2 chartType=bar]
* docs.zenon.org using ReadMe
* developers.zenon.org using ReadMe
* support.zenon.org using Intercom's Help Centre
* docs.zenon.org using Gitbook
* developers.zenon.org using Gitbook
[/poll]

If developers.zenon.org replaces the current docs.zenon.org, I will likely create marketing.zenon.org under some platform/tooling (maybe Intercom). The idea will be to organize and host the variety of assets marketing/sales teams could use for campaigning. Or the whole marketing docs could get organized under the attribute.zenon.org family since all marketing tools will be built on that brand.

-------------------------

sol | 2023-06-30 03:58:23 UTC | #9

I'm concerned about ownership and control of the documentation, as well as cost.

I don't particularly like the idea of subscribing to and relying on a third-party service to maintain our documentation. Please correct me if I'm wrong about what you're suggesting, @mehowbrainz.

At this time, I would prefer to keep costs low, decentralize hosting (multiple mirrors), and allow anyone to contribute. Worst case, anyone can fork the repo and maintain their own documentation.

-------------------------

mehowbrainz | 2023-06-30 04:42:12 UTC | #10

[quote="sol, post:9, topic:1529"]
I don’t particularly like the idea of subscribing to and relying on a third-party service to maintain our documentation.
[/quote]

Gitbook seats aren't free, ZenonOrg paid for them until this point. Self-hosted solutions still give the control to the infra admin re: database. The forum is an example.

[quote="sol, post:9, topic:1529"]
Worst case, anyone can fork the repo and maintain their own documentation.
[/quote]

I guess that this vote then applies to whoever wants to contribute to a ZenonOrg hosted technical documentation. I'm fine with whichever option, whether it's ReadMe or Gitbook, though I'm unsure how to fork Gitbook documentation.

I think regardless of the Pillar opting to provide such a service to the community, the problem of control will exist. The only solution I thought for a future was fragmented ownership of domains (which will require a brand new service/system), or like you mention forks/mirrors.

The ZenonOrg brand believes in a streamlined experience for onboarding newcomers/participants, and hence it proposes ideas which unifies services from a domain, ux, design, branding, flow perspective -- with visions to progressively decentralize the trust the community puts into the brand.

-------------------------

mehowbrainz | 2023-06-30 04:55:43 UTC | #11

If Gitbook can't be forked, then the other alternative would be a Github repo for content, but that's not as friendly UX-wise. Can look for other reliable alternatives.

-------------------------

mehowbrainz | 2023-06-30 05:01:08 UTC | #12

Another platform is [Docusaurus](https://docusaurus.io), which is a static site generator designed for building documentation websites. It's typically integrated with version control systems like GitHub, so you could fork the GitHub repository where the Docusaurus site's files are hosted.

I think @aliencoder's example uses Docusaurus.

[quote="aliencoder, post:1, topic:1529"]
I like this template from [Avalanche ](https://docs.avax.network/).
[/quote]

-------------------------

aliencoder | 2023-06-30 07:47:32 UTC | #13

I like [Docusaurus](https://docusaurus.io/) and [mdBook](https://rust-lang.github.io/mdBook/).

They're 100% free.

-------------------------

angelo_a_jr | 2023-06-30 14:29:04 UTC | #14

Seems to be a lot of ways to skin the cat.  

Given that @mehowbrainz is driving the majority of this effort coupled with his experience/track record to show for it, I'm happy to defer to what tools he feels most comfortable executing on even if a bit different from poll outcomes.

Let us know where to add all the things.

-------------------------

sol | 2023-06-30 15:57:33 UTC | #15

I understand your vision and I know you have good intentions. 
I'm not even against any of the solutions you're proposing, but I think we should initially strive for one that benefits the entire community and minimizes the risk of data loss/gating.

The path of least resistance is forking znn-wiki and maintaining versions that are synced/hosted by multiple community members.

Anyone could take that information, transform it however they wish, and present it in a nicer way.

-------------------------

mehowbrainz | 2023-06-30 17:41:28 UTC | #16

developers.zenon.org repo [has been created](https://github.com/ZenonOrg/developers) and the domain has been assigned using Github Pages. Anyone who wants write/maintain permissions DM me your GitHub handle.

@aliencoder would you like to push Docusaurus?

-------------------------

mehowbrainz | 2023-06-30 17:12:10 UTC | #17

[quote="sol, post:5, topic:1529"]
https://wiki.zenon.network/#!index.md
[/quote]

The alternative option is to install Docusaurus in this repo. Though we'll have to wait for admins to review PRs. It depends if we want to go through them, or manage docs ourselves via a new portal like developers.zenon.org ourselves.

-------------------------

sol | 2023-06-30 17:28:14 UTC | #18

Please, not another repo that is controlled by Mr Kaine.

I strongly believe that Mr Kaine should only be entitled to control the spork address, to be used as a contingency measure when governance fails.

Everything else, including znnd, can/should/will be managed by the community.

[quote="mehowbrainz, post:17, topic:1529"]
manage docs ourselves via a new portal like [developers.zenon.org](http://developers.zenon.org) ourselves.
[/quote]

HyperCore One will host a mirror of the documentation, as well.
All participants will need to align on a process to synchronize versions.

-------------------------

mehowbrainz | 2023-06-30 17:49:14 UTC | #19

Whenever ready, I can help theme the site.

-------------------------

aliencoder | 2023-06-30 17:59:11 UTC | #20

[quote="mehowbrainz, post:16, topic:1529"]
@aliencoder would you like to push Docusaurus?
[/quote]

Yes, please.

-------------------------

DrBlaze_21 | 2023-06-30 19:37:13 UTC | #21

A comprehensive documentation is a must!

-------------------------

mehowbrainz | 2023-06-30 21:23:47 UTC | #22

[quote="sol, post:18, topic:1529"]
All participants will need to align on a process to synchronize versions.
[/quote]

If you fork a repository on GitHub, the standard way to get your contributions incorporated back into the parent repository is through a pull request. Here are the general steps:

1. **Fork the repository**: Click the 'Fork' button at the top right of the parent repository's main page. This will create a copy of the repository under your own GitHub account.
2. **Clone the forked repository to your local machine**: Open your terminal, navigate to the directory where you want the repository, and use the `git clone` command with the URL of your forked repository.
3. **Create a new branch**: It's generally a good practice to create a new branch for each set of changes you want to make. You can do this with the command `git checkout -b branch-name`.
4. **Make changes**: Make the changes to the code on your local machine.
5. **Commit the changes**: Once you're satisfied with the changes, commit them using `git add .` to stage all changes, then `git commit -m "Commit message"` to commit the changes. Be sure to write a descriptive commit message.
6. **Push the changes**: Push the changes to your remote forked repository with the command `git push origin branch-name`.
7. **Open a pull request**: Go to your forked repository on GitHub and click on 'Pull request'. Choose the branch you just pushed from the 'compare' dropdown. Review the changes, then click 'Create pull request'. Write a descriptive title and comments to help the maintainers of the parent repository understand your changes.

At this point, the maintainers of the parent repository will be able to see your proposed changes. They can review them, discuss potential modifications, and ultimately decide whether to merge your changes into the parent repository.

If the parent repo's maintainer wants to merge some specific contributions from a forked repo, they can do this manually by checking out the changes in the forked repo, applying them to their own codebase, and then committing that as their own changes. However, this method does not recognize the original contributor in the commit history. Thus, pull requests are a more favorable method as they maintain a clear history of contributions and contributors.

Source: GPT

-------------------------

aliencoder | 2023-07-01 18:38:44 UTC | #23

https://githubnext.com/projects/copilot-for-docs

-------------------------

mehowbrainz | 2023-07-02 14:57:14 UTC | #24

Will sign up for the waiting list.

-------------------------

0x3639 | 2023-07-06 13:57:21 UTC | #25

good example of SDK docs from millerships

https://millerships.github.io/pyznn/

-------------------------

sol | 2023-07-09 22:25:54 UTC | #26

Lots of different solutions. 

Another suggestion: fork [this](https://github.com/bitcoin-dot-org/developer.bitcoin.org) and rebrand.

Could be beneficial because:
1. it's proven documentation structure
2. it appeals to bitcoiners and devs

If we don't fork it, maybe we can strive for the same completeness.

-------------------------

mehowbrainz | 2023-07-14 21:35:28 UTC | #27

@aliencoder @sumamu is this for the technical documentation? https://hypercore-team.github.io/intro/introduction.html

-------------------------

aliencoder | 2023-07-14 21:37:38 UTC | #28

This is related only to the bridge, but yes, we can extract valuable info from it.

-------------------------

mehowbrainz | 2023-07-14 21:37:53 UTC | #29

Cool are you planning to develop technical docs for other topics of the network?

-------------------------

