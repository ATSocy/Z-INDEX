Thread: zenon-hub-1-year-later
digitalSloth | 2023-09-24 21:32:17 UTC | #1

Its almost been a year since the initial launch of Zenon Hub so I thought it would be a good time to give a summary of the project so far, looking at what has been achieved and whats to come going forward.

---

**Looking back**

When the site first launched it didnt even have the explorer, it was just the AZ & Pillar pages with some basic tools, but development continued with new features being added, designs updated and community feedback implemented. Traffic has been growing steadily with an average of 13 unique visitors per day and 3 minutes of engagement time this past week. The most popular page is the account details page, followed by the explorer overview. Code wise there have been 233 deployments to the live site and over 1000 commits since the repo was set to public in February. 

Since the initial AZ application in January there have been lots of developments in the Zenon ecosystem, the bridge has launched, HTLCs have been added, the community has taken over development of Syrius and we've had an accidental fork! I have followed the developments in the network and pushed numerous updates to Zenon Hub keeping it up to date with the latest changes.

---

**Major updates**

Below is an overview of the main features launched since our first AZ application:

**Whale alerts** - https://zenonhub.io/services/whale-alerts
Our whale alerts are available on Twitter, Discord and Telegram they report large transactions of ZNN & QSR.

**Bridge alerts** - https://zenonhub.io/services/bridge-alerts
The bridge alerts service is available on Telegram and Discord, it watches for any actions issued to the bridge or liquidity contracts by the admin or guardians.

**Plasma bot** - https://zenonhub.io/tools/plasma-bot
The plasma bot temporarily fuses QSR to an address allowing the user to receive high, medium or low plasma.

**Public nodes** - https://zenonhub.io/services/public-nodes
Our public nodes are load balanced and offer secure access to the network via HTTPS or WSS connections.

**AZ stats** - https://zenonhub.io/stats/accelerator
The AZ stats page gives a summary of AZ data, allowing you to see the total funding pot, pillar engagement and top contributors.

**Bridge stats** - https://zenonhub.io/stats/bridge
The bridge stats pages gives quick access to the bridge status, orchestrators status, admin actions and security info. 

**Account favorites** - https://twitter.com/zenonhub/status/1678093915612667908
Registered users can save a list of favourite addresses, tokens, transactions and momentums.

**wZNN-wETH-LP-ETH Staking** - https://twitter.com/zenonhub/status/1687895200159481856
Our staking pages were updated to track the wZNN-wETH-LP-ETH tokens.

**HTLC support**
The indexer was updated to decode the HTLC ABI and the API was updated to give access to the new RPC endpoints.

**Bridge support**
The indexer was updated to decode the Bridge & Liquidity ABI and the API was updated to give access to the new RPC endpoints.

**Bigint upgrade** 
The indexer and database were updated to support the bigint node changes. 

---

**Looking forward**

A lot of work goes into this project and I am excited for the future, I plan to continue supporting the site and ensuring its compatible with the latest network changes as well as developing new features. I am always open to feedback and suggestions so if theres anything you want to see let me know.

I have a roadmap of new functionality but due to the other ongoing network development the priorities can change, however a few things I am planning develop include:

- Notifications for favourited addresses
- PTLC contract support
- Governance module support + alerts bot
- Plasma calculator tool (depends on dynamic plasma)
- More statistics pages

---

**Funding request** 

15k ZNN and 150k QSR

The current server setup costs roughly $150 a month and most my free time goes into the project so I plan on apply to AZ again in order to support the costs associated with the project. This application will cover the time since the last AZ application to the current date, I will likely review again in the future but do not have any specific plans for additional funding at the moment.

-------------------------

0x3639 | 2023-09-25 00:26:08 UTC | #2

I can say from first hand experience @digitalSloth has been open to changes and proposed features.  He always seems to be working on the site after hours.  His site is very user friendly and when adoption accelerates the community will expect / appreciate the features offered by the site.  I personally use the site almost every day.  

I believe we should support developers like DS.

-------------------------

dat_she_pepe | 2023-09-25 12:28:34 UTC | #3

I'm not personally comfortable in another funding request. That's a lot of money if we add it all. Let's see what others think.

-------------------------

mehowbrainz | 2023-09-25 13:03:29 UTC | #4

@digitalSloth may you post a link to your first funding request?

-------------------------

digitalSloth | 2023-09-25 13:11:36 UTC | #5

Sure, here is a link to the previous AZ application it was for 5k ZNN & 50k QSR.

https://forum2.zenon.org/t/zenon-hub-proposal/1197

-------------------------

mehowbrainz | 2023-09-25 13:21:30 UTC | #6

@digitalSloth can you estimate the number of hours worked and expenses you incurred since your last funding request?

-------------------------

digitalSloth | 2023-09-25 14:59:58 UTC | #7

I guess somewhere between 650 and 700 hours have been spent on the project along with $900 of server costs since February.

-------------------------

mehowbrainz | 2023-09-25 19:03:21 UTC | #8

Fair enough, valuing your rate at $25-27 per hour. My frontend developer charges $17 per hour, but I guess there is value-add that you're well familiarized with the network and its intricacies.

My only critique is that the community wasn't aware that you'd be billing for additional work considering I quote from your previous proposal:

> If accepted I would be applying for the full amount in one go with the intention of spawning a sentinel to help cover the ongoing development and server costs.

And that the bill comes at ZNN's lowest price levels. Would've been cool to see these bills at various (higher-priced) ZNN levels.

Critique of how AZ is currently organized: I've said it many times before, I think the network should stop accepting big bang proposals, and instead we should be operating like an organization where teams set hourly rates, Pillars approve hiring, and everyone contributes to weekly sprints where they submit their work logs and bills periodically (every 2 weeks or so). This would force Pillars to understand what's being built, by who, why and whether the network needs it or not.

-------------------------

digitalSloth | 2023-09-25 20:24:27 UTC | #9

The typical rate for a backend dev here is roughly $30 per hour and my latest proposal works out to the same $ value as my previous one so I thought it was a fair request given the amount of time spent on the project.

Yes I said I’d apply for the whole amount in one go but that was referring to that proposal, later in the comments I followed up to a question about future funding:

[quote="digitalSloth, post:14, topic:1197"]
at this stage I cannot say I will never apply to AZ for this project again especially as ideas develop and features grow but its not something I am considering at the moment
[/quote]

I appreciate the price of ZNN is at a low point and it would be great if it was higher but given the project is about to hit its one year anniversary I felt it was an appropriate time to submit a new proposal and would have done so regardless of the price.

-------------------------

dat_she_pepe | 2023-09-25 20:26:49 UTC | #10

I can only imagine how the treasury would look like if every developer was sending bills / funding at the bottom. There's a community funding strategy to adopt in order to support a long term development.

I'd suggest to put on a hold anything that's not absolutely necessary and focus on what is.

-------------------------

coinselor | 2023-09-25 23:07:44 UTC | #11

Happy Z Hub Anniversary!

In my personal opinion, DS clearly over delivered, setting a great precedence for the network. It's true that submitting the request at this time benefits him greatly, but at the same time, there was no way to know ahead of time he would be in such a position. To be in his position, he had to commit ahead of time to working and developing new features and provide support/participate with other developers and community members, earning the respect of Pillars in the process. I believe he has earned the right to submit this proposal even at this market rate.

Well played, and good luck!

-------------------------

dat_she_pepe | 2023-09-26 10:54:21 UTC | #12

In my opinion we should manage the A.Z fund with priorities and a better and clearer process in fund distribution. Ex: no more infinite re-aplications. No matter how you look at it this is an amateur way to manage a non infinite chunk of money. What will you do once it's 0? Keep distributing compliments and hope people keep working?

-------------------------

coinselor | 2023-09-26 14:01:04 UTC | #13

We have had ideas of introducing a revenue stream for AZ or redirecting Orbital emissiosn to fund the AZ treasury, that's basically infinite, and most of the benefit early on is to boosttrap the initial liquidity of the network, once it's established, there is no more reason to keep allocating 25% of emissions to liquidity, a much lower or nil % should suffice, imo.

I do agree with your overall take, need to respect the value of the treasury with a much longer time horizon.

-------------------------

dat_she_pepe | 2023-09-26 15:13:04 UTC | #14

We should open discussions about methodology and priorities. Protocols and protocol related projects should come first imo. Accessory tools not so much. The habit of spamming 414 A.Z requests per project should be questioned. And hm, I'm sorry but 15 to 20k for a website is kinda expensive. I'll let other discuss. I talked too much.

-------------------------

digitalSloth | 2023-09-26 16:42:17 UTC | #15

[quote="dat_she_pepe, post:12, topic:1628"]
In my opinion we should manage the A.Z fund with priorities and a better and clearer process in fund distribution
[/quote]
I agree, if the way AZ is currently being run is unacceptable to the pillars then new processes etc should be put in place. But as there is no guidance I followed the example set by past applicants, which was to build first, deliver the product and then seek reimbursement after.

[quote="dat_she_pepe, post:14, topic:1628"]
Protocols and protocol related projects should come first imo. Accessory tools not so much.
[/quote]
It is my understanding that those capable of working on protocol projects already are, so should other projects be put on hold until all protocol work is completed?

[quote="dat_she_pepe, post:14, topic:1628"]
And hm, I’m sorry but 15 to 20k for a website is kinda expensive.
[/quote]
One of my aims for Zenon Hub is to make the network more accessible to everyday users so that when the protocol is fully fleshed out we have a platform that helps people onboard, explore and use the network to its full potential. This project is more than just "a website" thats why it offers public nodes, the plasma bot, alerting services and APIs with more features currently in development.

-------------------------

Stark | 2023-09-28 00:28:58 UTC | #16

With respect and gratitude for DS and his work, I want to try to articulate the complicated sense that may factor into the discussion.

[quote="0x3639, post:2, topic:1628"]
when adoption accelerates
[/quote]

As stated, "when adoption accelerates"... there is some projection and consideration for the future, but the funding request is calculated based upon present market token value.

Thought exercise: If you put in a similar request, would you be of the mindset to sell all of your tokens on the market, at $0.67? 

[quote="digitalSloth, post:15, topic:1628"]
It is my understanding that those capable of working on protocol projects already are, so should other projects be put on hold until all protocol work is completed?
[/quote]

Not sure about "put on hold" but I do think that there should be consideration for timing funding requests in relation to development stages of the project, token price, market conditions.

I do support the dollar amount, but I wonder whether it is right to approve that dollar amount, as paid in ZNN and QSR, today. 

How about putting in a request for $42k when ZNN gets back up to $6.70? 

Sensitive and complicated subject. I respect the opinions and interests of all involved.

-------------------------

zyler9985 | 2023-09-28 11:20:22 UTC | #17

DS is doing important work and it's not his fault the price is so low. Should everyone be paid assuming an imaginary price of $1000 per coin? It should be noted that the road to 1k per coin is not going to happen by itself, it's not even guaranteed to happen, it requires the full effort of builders and DS happens to be a great builder. I'm supportive of the full amount!

-------------------------

sumamu | 2023-09-28 12:19:42 UTC | #18

I'm supporting this AZ application. 

My engagements with @digitalSloth were brief, but enough to convince me he's an awesome alien, willing to discuss things and making himself available to fix anything. ZenonHub is the best explorer we could've asked for and it's been a valuable resource during our development. 

I understand why the timing might be painful to some community members.

-------------------------

SugoiBTC | 2023-09-28 14:30:26 UTC | #19

I am also supporting the application by DS.

DigitalSloth has been actively participating in our network and is communicative. He has contributed by supplying several TG bots and by launching the zenonhub.io website. I find myself frequently using the services that he provides and will continue to do so.

I have faith in that DS will continue to support the network in the future and would love to see him spawn infrastructure to become self-sufficient and to finance the operations of zenonhub.io.

-------------------------

digitalSloth | 2023-09-28 17:30:12 UTC | #20

Thank you all for your comments and support,I realise this is a big ask especially with the current market conditions but for the reasons stated I believe this is a fair amount for a project like this.

[quote="Stark, post:16, topic:1628"]
How about putting in a request for $42k when ZNN gets back up to $6.70?
[/quote]
If I were to wait for the price to recover then apply I wouldnt be able to afford the infrastructure I plan to invest in so would actually become more reliant on AZ which I want to avoid.

This project has ongoing and increasing costs as it grows, and as @dat_she_pepe said infinite re-applications to AZ are not sustainable. But a proposal like this will allow me to invest in the infrastructure needed to support this project going forward.

-------------------------

mehowbrainz | 2023-09-28 18:18:27 UTC | #21

[quote="digitalSloth, post:20, topic:1628"]
But a proposal like this will allow me to invest in the infrastructure needed to support this project going forward.
[/quote]

Just wanted to add that the #HyperGrowth Pillar on its own can't sustain 1 developer full-time, they just don't generate enough in these market conditions...

-------------------------

digitalSloth | 2023-09-28 19:17:30 UTC | #22

Understood, I wouldnt be looking for it to support me full time initially but it would cover the hosting costs and when conditions improve hopefully allow me to go full time

-------------------------

digitalSloth | 2023-10-03 18:03:25 UTC | #23

The AZ applications have been submitted

-------------------------

tapwoot | 2023-10-03 18:03:32 UTC | #24

i voted yes thx for your contribution

-------------------------

0x3639 | 2023-10-05 19:29:12 UTC | #25

I will do the same.

-------------------------

angelo_a_jr | 2023-10-13 09:00:09 UTC | #26

I'm one of the newer Pillar voters here and this was my same logic after seeing the request.

Zenon Hub is amazing quality and should be rewarded handsomely.  That being said, the timing of this request is really difficult to justify.

We are at our lowest historical MCAP so asking full amounts to compensate an equivalent fiat market rate sets a slippery precedent of asking for max A-Z requests at low points. A capital efficient org needs to be thinking in the opposite direction. 

That being said, I do think your work warrants MORE in BTC/fiat equivalent than what you are requesting but only until we can collectively get the price back up to $10+

I'm going to go ahead and vote Yes on 1/3 and No on 2/3 + 3/3 though it seems the consensus is already in.

-------------------------

dat_she_pepe | 2023-10-13 15:52:37 UTC | #27

I voted no and will not even vote to such high funding asks in the future.

-------------------------

