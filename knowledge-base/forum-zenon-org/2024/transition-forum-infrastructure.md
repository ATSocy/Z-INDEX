Thread: transition-forum-infrastructure
0x3639 | 2023-10-14 14:39:09 UTC | #1

I've been assessing the amount of "control" that I personally have for this project and it's too high.  I'm a single point of failure and I think we need to change that.  Today I have the following "controls":

- forum.zenon.org - admin & hosting provider
- forum.hypercore.one - admin & hosting provider
- TG main - owner
- TG Community - Owner
- Github - Admin

I also run a number of bots, chat things, antispam stuff.  The list goes on and on.  It's too much.  And I engage in risky sports.  I was hit by a car this year and could have died.  

I would like to start by transitioning forum.zenon.org to @mehowbrainz and the TG Community channel to a 3rd party.   To be clear, I'm not going anywhere.  My commitment to this project has never been higher.  I just cannot have this much control.  

The forum takes:
- vps
- mailgun for email
- stackpath for CDN
- s3 for backup

How does everyone feel about this?  This is not a rug.  I am not turning anything off.  George knows who I am.  I'm just worried about my level of control.  I hope everyone thinks I've been a good and honest actor.  I plan to transition stuff that way too.

-------------------------

mehowbrainz | 2023-10-14 14:35:55 UTC | #2

ZenonOrg is okay to take over the forum under its existing infrastructure. Let me coordinate this with the infrastructure engineer.

-------------------------

0x3639 | 2023-10-14 14:39:57 UTC | #3

Cool.  I think you have AWS.  They have a CDN but I've never gotten it to work as well as Stackpath.  AWS also has a mail delivery service but I don't have experience with it.  

If you set this up with AWS <> S3 on AWS <> Stackpath <> Mailgun it will be much easier and the configs will transfer very easily.  If you decide to change any of those, I won't have experience setting them up.  And the CDN stuff can get very tricky.

-------------------------

NeoShredder | 2023-10-14 14:58:09 UTC | #4

[quote="0x3639, post:1, topic:1656"]
* [forum.zenon.org](http://forum.zenon.org) - admin & hosting provider
* forum.hypercore.one - admin & hosting provider
* TG main - owner
* TG Community - Owner
* Github - Admin
[/quote]

And public node

-------------------------

0x3639 | 2023-10-14 15:04:11 UTC | #5

ha, right.  Node(S).  Current and legacy nodes.

-------------------------

NeoShredder | 2023-10-14 15:14:52 UTC | #6

I am willing to run a public node.

-------------------------

0x3639 | 2023-10-14 15:17:33 UTC | #7

That would be great.  I highly encourage you to do that.

-------------------------

NeoShredder | 2023-10-14 16:17:51 UTC | #8

I tried that once. Followed your steps. I got stuck. Is there any way I cud get it up and running?

-------------------------

0x3639 | 2023-10-14 16:19:33 UTC | #9

ya something happened with the docker compose file.  I tried to fix it and then the network forked and got sidetracked.  I'll try to fix it in the coming days.

-------------------------

0x3639 | 2023-10-14 17:02:09 UTC | #10

Here is the updated list so everyone knows the exposure. 

* [forum.zenon.org](http://forum.zenon.org/) - admin & hosting provider
* [forum.hypercore.one](https://forum.hypercore.one) - admin & hosting provider
* TG main - Owner
* TG Community - Owner
* Github - Admin
* [zenon.info](https://zenon.info) - Owner
* @learn_zenon twitter - Owner
* @zenon_network - Maintainer
* learn_zenon youtube - Owner
* my.hc1node.com - Owner
* legacy.hc1node.com - Owner
* (2) HTLC Watchtowers
* Main and community TG Spam Bots
* TG bot that does forum lookups
* various api keys

I am seeing the discussion on TG questioning my desire to reduce exposure.  I hope this list helps explain why.  It should be clear this is too much for a small project.

-------------------------

0x3639 | 2023-10-17 20:04:48 UTC | #11

Just wanted to provide an update.  I've provided all the config files and a test backup.  I've also provided a proposed transition plan.  The engineer is evaluating everything.  We have plenty of time.  The site is working great and there is no need on my end to move quickly or make a mistake.

-------------------------

romeo | 2023-10-23 22:07:05 UTC | #12

part of the original AZ proposal for the forum included provisions for moving to a more decentralized hosting outcome (i.e. not relying on 0x so much)

-------------------------

mehowbrainz | 2023-12-31 05:43:12 UTC | #13

The forums have been transitioned to the ZenonOrg operated infrastructure. Login with GitHub has been added. Let's give a round of thank you's to @0x3639 for running this infrastructure over the last few years. Will be in good hands until we transition to a more decentralized hosting solution in some future, as outlined by @romeo.

-------------------------

mehowbrainz | 2023-12-31 07:49:01 UTC | #14

If images aren't loading for you, please leave a note here. We had faced the issue in a trial transition and resolved it, though @cryptocheshire reported that the images aren't loading for him. The infra engineer is rebuilding discourse to resolve the issue.

-------------------------

cryptocheshire | 2023-12-31 08:26:57 UTC | #15

I cleared the cache, issue still persists for me (tried with both my accounts)

-------------------------

mehowbrainz | 2023-12-31 17:33:09 UTC | #16

The issue was resolved, may you confirm on your end @cryptocheshire

-------------------------

cryptocheshire | 2024-01-01 09:05:41 UTC | #17

Works now 👍

-------------------------

mehowbrainz | 2024-01-01 22:05:37 UTC | #18

Some email addresses aren't receiving password reset emails etc (gmail addresses seem to work). We've identified the issue and tagged the infra engineer to resolve it asap. Thanks for your patience while we iron out the kinks of this transition.

-------------------------

mehowbrainz | 2024-01-02 07:21:13 UTC | #19

Email issues have been resolved.

-------------------------

