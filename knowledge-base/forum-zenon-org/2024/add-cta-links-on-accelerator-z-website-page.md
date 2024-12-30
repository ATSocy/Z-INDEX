Thread: add-cta-links-on-accelerator-z-website-page
John-Z | 2023-02-09 14:08:14 UTC | #1

Hey there, Z community! 

I was testing different platforms & campaigns to kick off some ads to grow the community of devs, but we're quite limited in terms of tracking & examining data from the official website.

Currently, I don't have a place to redirect new traffic, and the Accelerator-Z page (https://zenon.network/accelerator.html)  would be the best place to redirect new users, but unfortunately, there is not so much to do from that page, everything is just informative. 

The goal should be to direct them in the community directly... So, there I want to modify the A-Z page and put the links toward the community on the CTA (calls to action) from the last section of the page. 

Thus, I am requesting from you the public links to enter on the Marketing, Tech & Sales TG channels and I can help with the website edits. Let me know!

-------------------------

0x3639 | 2022-05-30 17:14:44 UTC | #2

Meaning, you want to add CTA buttons on the official webpage that directs devs to community links that allow them to submit an AZ proposal (for example)?

-------------------------

John-Z | 2022-05-31 06:36:17 UTC | #3

Yes, starting with the smallest change we can do, add the TG links to these buttons: 

![Screenshot 2022-05-31 at 09.31.35|690x244](upload://bfsjrZDcQXgVQF1s6YKhojVkggA.jpeg)

In the future, it would be ideal if we can connect somehow Syrius with the website allowing new visitors to create a Syrius account on the website & maybe apply to A-Z.

-------------------------

romeo | 2022-05-31 08:47:05 UTC | #4

@Sigli is this something you could pass onto the team to update? Seems like a no-brainer

-------------------------

0x3639 | 2022-05-31 12:58:48 UTC | #5

@ZenonORG @mehowbrainz Wanted to make sure you guys saw this request.  I know you guys are thinking about marketing at this level.  

I think a CTA could be a link from the website “Apply for a Grant”  to the forum which describes the program and how to apply:  https://forum2.zenon.org/t/zenon-network-grants-hyperspace-x-accelerator-z/439

-------------------------

OGZenon | 2022-05-31 17:07:47 UTC | #6

The CTA's link should have UTM parameters in them so that we can track the origin of the traffic (although likely won't know whether users actually signup to the forums, the Discourse dashboard doesn't support the setup of GA events).

Here is the UTM builder: https://ga-dev-tools.web.app/campaign-url-builder/

-------------------------

John-Z | 2022-06-01 11:47:52 UTC | #8

Guyz, yes, we should obviously track the traffic and start using some analytics framework for the entire website, but let's be honest, the core team won't assume something like Analytics because it comes with google authentication & KYC. 

Thus, I think we can take over this process that isn't hard nor too technical. 

1. let's get the links for each TG group (Marketing, Tech & Sales if there's any sales group), we get those through the Campaign URL Builder, add them to the open-sourced website,  make a pull request on Github and see if they accept. 

2. If they accept, I think we can go bolder by supporting someone to apply within A-Z with setting up the entire analytics framework: Google Analytics, Hotjar for heatmaps & user recordings to understand where the bottlenecks are, and other plugins we decide to be relevant.

Implementing this is not rocket science, we should just clarify who is willing to drive this process.  
What do think? @romeo @OGZenon @Sigli @0x3639

-------------------------

OGZenon | 2022-06-01 13:36:01 UTC | #9

Btw the campaign links with UTM parameters don't need a Google Analytics account from the core devs. If the referring URL (CTA) has its parameters set, the forums would see the data in the zenon.org analytics account. Like you mentioned, as long as the website is open-sourced we can make a PR with changes to some CTAs :)

As for the analytics framework, sounds great. To make the GA data public, I would also be able to get Zenon.Network added to Attribute.me (just like @mehowbrainz got THORChain.org added). This would allow us to publicly display 9 dimensions of data, giving everyone a chance to see/export GA data without having to login to GA (or request some privileges... less management for Admins of that GA account).

-------------------------

0x3639 | 2022-06-02 22:11:45 UTC | #10

This all makes sense to me.  

Guys - I have an idea.  Before we waste a bunch of time, let's do a PR to add a comment like

```
Zenon Network is an independent entity
```

Just to see if they will accept it.  If so, then let's party!  

Thoughts?

PS: I was looking at current PR and they have not done anything with them:  https://github.com/zenon-network/znn_controller_dart/pulls

-------------------------

0x3639 | 2022-06-02 22:29:52 UTC | #11

what's up bitches!!!  Let's see if they accept my YUGE pull request!  Gotta start somewhere.  

https://github.com/zenon-network/zenon.network/pull/1

-------------------------

OGZenon | 2022-06-03 15:10:56 UTC | #12

https://twitter.com/ZenonOrg/status/1532741095054098432

-------------------------

John-Z | 2022-06-08 18:23:02 UTC | #14

Congratz, let's put the bigger plan in motion 👽 

I'll put the TG links in the campaign URL builder and make a pull request out of it. 

We should also make a plan & an analysis to see what tools or plug-ins are needed for analytics. 

I would go with Google Analytics & Hotjar for a start.

-------------------------

