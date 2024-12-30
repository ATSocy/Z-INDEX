Thread: zenon-tools-wrapping-up-warpdrive-and-whats-next
vilkris | 2024-03-27 15:20:16 UTC | #1

Now that WarpDrive is coming to an end and the defined milestones have been met, Zenon Tools is looking to continue building new features that aim to provide value to the Zenon community.

Here is a short overview of the WarpDrive deliverables:
* The https://zenon.tools website ([source code](https://github.com/zenon-tools/zt-frontend))
* The API server for zenon.tools ([source code](https://github.com/zenon-tools/zt-server))
* An indexer for NoM written in Dart ([source code](https://github.com/zenon-tools/nom-indexer))
* A rudimentary [demo](https://zenon-tools-portfolio-demo.netlify.app/) of the portfolio tool that utilizes the data from the indexer ([source code](https://github.com/zenon-tools/portfolio-dashboard-demo))

## New version live
https://zenon.tools has been updated to a new version which features UI improvements and some additional functionality for the reward calculator - you can now customize the price of ZNN and QSR and duplicate the calculator to easily compare different participation strategies.

If you notice any issues with the new version please DM me here on the forum or on Telegram (@vilkris).

## What's next
The groundwork done and feedback gathered during WarpDrive will allow for new features to be delivered at a relatively quick pace. Here is an overview of features that are currently in development that are planned to be delivered next.

### 1. Pillar profile page

A dedicated view for all Pillars that will showcase who they are, what their metrics are, how they’ve voted, their reward sharing history, and more.

![Artboard – 9|690x416](upload://pk8QZWi4MB1cr6uadwIoQPfll7p.jpeg)

![Web 1920 – 14|690x359](upload://fc6DMtugikm6PiBb2FXwUqvmca2.jpeg)

### 2. Pillar profile management
A dedicated page for Pillar owners to manage their avatar, social links, and Pillar description text. This information will be displayed in the Pillar list and on the dedicated Pillar profile page.

A Pillar’s information can only be updated with a valid signature.

![Artboard – 7|487x499](upload://4dNvTE4JpfsaxjiosUQZqaVvEYh.png)

### 3. Accelerator-Z showcase
A showcase of A-Z projects showing their general information, voting breakdown, phases, etc.

![Artboard – 9|690x352, 100%](upload://kvCKf64vCWaL1T776Fjp0YLE0Oz.png)

Please comment if you have ideas or questions related to the upcoming features.

-------------------------

cryptocheshire | 2022-05-25 14:16:59 UTC | #2

Woaah that is awesome

-------------------------

cakoincap | 2022-05-25 14:47:49 UTC | #3

Really looking forward for the Accelerator-Z showcase feature.

Zenon tool is my favorite project no doubt

-------------------------

0x3639 | 2022-05-25 15:15:06 UTC | #4

wow this is great.  Really excited to see this roll out.  On the Pillar signature section, do you provide a random character string to sign?  Looks like all you need is the signature on the GUI.  

Thanks so much for working on this.

-------------------------

coinselor | 2022-05-25 15:26:24 UTC | #5

Outstanding job, Vilkris. 

I hope the zenon.tools brand in the future (when we reach 1 billion users) keeps being a staple within the Zenon ecosystem. :innocent:

-------------------------

7nzalh | 2022-05-25 15:47:03 UTC | #6

Amazing work @vilkris ! Thank you for all your contributions to the project and community.

-------------------------

vilkris | 2022-05-25 15:50:51 UTC | #7

You can click the image twice to see it in full resolution. At least initially the idea is to request pillars to sign a predefined text like "zenon.tools" for example. It should be instructed that the signature used here is like a password and should not be revealed to anyone. All the verification will then be done on the backend.

-------------------------

vilkris | 2022-05-25 15:52:22 UTC | #8

Thank you everyone for the kind words :pray:

-------------------------

0x3639 | 2022-05-25 16:24:06 UTC | #9

Only comment, I think this should be a random UUID.  I've been thinking about this for the Pillar signing plugin for the forum.  that way a signed string cannot be saved and reused.

-------------------------

vilkris | 2022-05-25 16:10:25 UTC | #10

Yes that is true. I'll have to consider it.

-------------------------

