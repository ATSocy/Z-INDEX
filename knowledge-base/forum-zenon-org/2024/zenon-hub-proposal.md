Thread: zenon-hub-proposal
digitalSloth | 2023-01-23 21:00:10 UTC | #1

Hi everyone,

Im thinking of applying to AZ for [zenonhub.io](https://zenonhub.io) and wanted to get some feedback on the proposal before submitting it officially. Let me know what you think.

---

**Project Name:** Zenon Hub

**Description:** Zenon Hub is an explorer for the Network of Momentum and provides a range of tools for interacting with and building on-top of the Zenon Network.

**URL:** [zenonhub.io](https://zenonhub.io)

> **Features**

The website was launched in October 2022, here is an overview of what has been released:

**Explorer**
* Overview and basic statistics
* Searching, sorting and exporting data
* List and detail pages for:
-- Momentums
-- Transactions
-- Addresses
-- Tokens
-- Staking
-- Fusions

**Pillar pages**
* Overview page with search, filtering and sorting
* Detail page summarising various on chain data

**Accelerator pages**
* Overview page with search and filtering
* Project and phase detail pages

**Tools**
* API Playground - interact with the RPC endpoints of the network
* Node statistics - displays public node distribution data
* Message broadcasting - pillar owners can send a signed message to the forum
* Verify signature - check a message signature is valid and originated from the intended address

**User accounts**
* Notifications for on chain activity:
-- New AZ projects & phases
-- New pillars
-- Pillar updates
-- Voting reminders for pillar owners

**API**
* HTTP endpoints for the RPC endpoints of a public node available

**Public Node**
* Two secure endpoints are available for use:
-- wss://node.zenonhub.io:35998
-- https://node.zenonhub.io:35997

> **Roadmap**

Here is the short term roadmap with an overview of the features currently being worked on:

**Explorer statistics** - *in progress*
* Create snapshots of network data every hour and display the results in various charts
-- Transactions - sent/received/type/value/token
-- ZNN - Sent/received/mint/burn/staked/delegated/locked in pillar & sentinels
-- QSR - Sent/received/mint/burn/fused/locked in sentinel
-- Addresses - Active per snapshot/total active/new
-- Supply - total/available ZNN & QSR

**User accounts upgrades** - *planning*
* Create address/token watchlists
* Custom address labels
* Private notes on tx/momentums/addresses/tokens

**Communities** - *planning*
* Each address gets a social media style feed, addresses can post and others can comment/like/dislike/vote
* Groups of addresses allow users to build communities e.g pillar delegator community

> **Future ideas**

These are some ideas being considered but havent been worked into the roadmap yet:

* Login with syrius browser extension - depends on a [update](https://github.com/DexterLabZ/syrius-extension/issues/20) to the extension
* Explorer discord bot
* API for indexed data
* Webhooks for on chain activity

> **Funding**

**Total Requested Funding**
5,000 ZNN 
50,000 QSR

If accepted I would be applying for the full amount in one go with the intention of spawning a sentinel to help cover the ongoing development and server costs.

[poll type=multiple results=always min=1 max=1 chartType=bar]
* Yes
* No
[/poll]

-------------------------

mehowbrainz | 2023-01-23 21:13:40 UTC | #2

Great work on the explorer! Is the project open sourced?

-------------------------

0x3639 | 2023-01-23 21:40:54 UTC | #3

I've been working with @digitalSloth to test his site from early on.  His original AZ was rejected, but he just built the site anyway.  He added features that I recommended, like signed TX to the forum. He changed the site name, changed colors, added the node site map w/ @sol code, and updated the theme. He is always super responsive and open to new ideas.  We should be really happy to have him in our community. 

I think over time his site will diverge more from zenon.tools and I think features that can be seen in thorchain.net work their way into zenonhub.io.

I support this proposal and hope my delegators do too.

-------------------------

digitalSloth | 2023-01-23 21:42:06 UTC | #4

Thank you. At the moment the Zenon hub code itself is not public but the [PHP SDK](https://github.com/digitalSloth/znn-php) used to build the site is. I had thought about creating a Laravel package containing the indexer but wanted to focus on fine tuning it all first

-------------------------

mehowbrainz | 2023-01-23 21:43:42 UTC | #5

[quote="0x3639, post:3, topic:1197"]
I think over time his site will diverge more from zenon.tools and I think features that can be seen in [thorchain.net](http://thorchain.net) work their way into [zenonhub.io](http://zenonhub.io).
[/quote]

The dev that wrote some of the zenon.org and attribute code, built thorchain.net :) I chat with him every week or so

-------------------------

digitalSloth | 2023-01-23 21:46:08 UTC | #6

Thanks for all your support, its been great working with you I appreciate the vote of confidence

-------------------------

mehowbrainz | 2023-01-23 21:57:38 UTC | #7

[quote="digitalSloth, post:1, topic:1197"]
API for indexed data
[/quote]

I think this'll be extremely valuable. It translates to metrics for marketing.

-------------------------

mehowbrainz | 2023-01-23 22:05:24 UTC | #8

I'd love to see an on-chain data exporter/importer and API integration for https://cointracking.info

Could expose Zenon to 1.28M users, many institutional. ZenonOrg investors use their system for their financial reporting workflow with their accounting firm.

-------------------------

digitalSloth | 2023-01-23 22:16:03 UTC | #9

Data can already be exported from the account details pages in the explorer, theres a button next to the search box under the tabs headings.

Not heard of that site before but looks like it would be valuable to integrate with in the future

-------------------------

sol | 2023-01-23 22:31:41 UTC | #10

I love the work you've done with ZenonHub and I'm really excited to use some of the features you've announced on your roadmap.

I do have a concern about proposals for services being offered by community ZNNAliens.
There's nothing to hold service providers accountable after they've been funded.

For this proposal, can you please share your source code so others can potentially host the platform if you stop providing the service?

-------------------------

digitalSloth | 2023-01-23 23:06:17 UTC | #11

Thank you, its always encouraging to hear feedback like that. 

Thats a fair point I see how it is a concern, I need to tidy a few things up and write a readme for the repo but I'll aim to publish it before the weekend.

-------------------------

sol | 2023-01-23 23:35:36 UTC | #12

[quote="digitalSloth, post:11, topic:1197"]
I’ll aim to publish it before the weekend.
[/quote]

There's no rush or expectation of code delivery at this time. 
But if your proposal is accepted, I hope you do make the code open source.

Thanks for understanding! I hope you get paid for all your hard work! :green_heart:

-------------------------

vilkris | 2023-01-24 09:00:41 UTC | #13

I'd support this proposal. I think in similar types of proposals a requirement has been to open source all the necessary code, so I'd hope to see that before the funds are requested.

I know the funding request is for the work you've already done, and it's well deserved, but what about the future? Are you planning on requesting more A-Z funds in the future, or do you have plans to perhaps monetize the service in some way?

[quote="mehowbrainz, post:5, topic:1197"]
The dev that wrote some of the [zenon.org](http://zenon.org/?_gl=1*1stkx1z*_ga*MjAzMTQ4NDczOS4xNjUwMzQzNzAz*_ga_M2F8KJ59YQ*MTY3NDU0NjIyNi4xNjQuMS4xNjc0NTQ4ODU3LjAuMC4w) and attribute code, built [thorchain.net ](http://thorchain.net) :slight_smile: I chat with him every week or so
[/quote]
Is thorchain.net community run? If so, how is the development funded?

-------------------------

digitalSloth | 2023-01-24 12:34:51 UTC | #14

Thanks for the support vilkris! The code will be open source before any funds are requested, I'll update the original post when there is a public repo. 

Good question, at this stage I cannot say I will never apply to AZ for this project again especially as ideas develop and features grow but its not something I am considering at the moment. I do have some ideas to monetise certain areas, specifically with the user accounts and the index data APIs but nothing is confirmed.

I would also be interested if @mehowbrainz has any insight as to how thorchain.net 
is funded? In an ideal world I would love for this to become my full time job, but at the moment I have to find time around my regular job to work on it.

-------------------------

mehowbrainz | 2023-01-24 14:30:04 UTC | #15

[quote="vilkris, post:13, topic:1197"]
Is [thorchain.net](http://thorchain.net) community run? If so, how is the development funded?
[/quote]

Many projects at THORChain were funded by the treasury, including THORChain.net, but the treasury isn't operated by the community. Founder(s) hold the keys from what I remember. Definitely was no THORNode voting process to fund projects, a few founders (and eventually 9R) decided what got funded and what didn't.

-------------------------

aliencoder | 2023-01-26 18:28:56 UTC | #17

Nice! In my opinion you can deliver a ton of value if you integrate [Wordpress](https://wordpress.org/plugins/), [Drupal](https://www.drupal.org/project/project_module), [Joomla](https://framework.joomla.org/), [Magento](https://marketplace.magento.com/extensions.html) or even [Shopify](https://github.com/Shopify/shopify-api-php) plugins.

Ideas worth considering: ZNN Checkout Plugin, Show price in ZNN, Price tracker

-------------------------

digitalSloth | 2023-01-26 19:26:29 UTC | #18

Thanks for the suggestions about the plugins, will have a look at the option and see if it can be worked into the future roadmap. 

The payment plugin is something I had briefly considered a while ago but never got round to doing a proof of concept, it would definitely add a lot of value to the ecosystem. Could maybe do it as a new gateway for [Omnipay](https://omnipay.thephpleague.com/)

-------------------------

digitalSloth | 2023-01-29 13:19:59 UTC | #19

Thank you all for the feedback and suggestions, its encouraging to hear all the positive comments. Im working on getting the code ready to publish as soon as possible and will update this thread when its released. I'll also submit the initial AZ application later today.

-------------------------

dat_she_pepe | 2023-01-30 17:51:41 UTC | #20

I fully support this and will vote no 🧌🧌🧌🧌

-------------------------

digitalSloth | 2023-02-03 18:31:06 UTC | #21

Quick update, Iv created a new GitHub organisation and released all the code for ZenonHub in this repo [https://github.com/zenonhub-io/zenonhub](https://github.com/zenonhub-io/zenonhub) also made a public [roadmap](https://github.com/orgs/zenonhub-io/projects/1/views/1) so you can see whats being worked on whats next.

Thanks again for all your support with this project :alien:

-------------------------

