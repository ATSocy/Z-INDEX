Thread: zenon-website-loading-duration
cagri | 2024-01-15 15:44:20 UTC | #1

Today I've shared the website link with some of my friends and got the same response:
`Website is not working`

The loading phase of the main website is too long, we should load the main page faster.

You can see the response time for favicon below, it's too much. What are the servers we use, what could be reason of this? It took 24.82 to load only main page

![image|690x383](upload://vK7VAFO0eOjbxKkqtdCN0FWtaDn.png)

-------------------------

0x3639 | 2024-01-15 17:36:24 UTC | #2

We have mixed-content errors too.  API for price feed is slow too.  I can fix these two.  Not sure about favicon.  Site is hosted by github on gh pages.  

![image|690x42](upload://owQaWr4cMEvKdbRvhn1BuSacWVz.png)

Need feedback on this request to fix the api speed.  https://forum.zenon.org/t/syrius-wallet-mobile-app/659/152?u=0x3639

-------------------------

digitalSloth | 2024-01-15 20:20:27 UTC | #3

The 'dna' animation is 17mb and the intro animation is 3mb, this will be slowing down the initial load of the site but if we want to keep the animations Im not sure what we can do about it. 

![Screenshot 2024-01-15 at 8.15.40 pm|690x269](upload://2gsoZFbkUHaxrGSSwu7Bj8AOkQZ.png)

-------------------------

coinselor | 2024-01-15 21:01:10 UTC | #4

Remove animation on mobile/4g connections? 

Doesn't Apple do this? Load a huge amount of pictures on desktop, but minimal amount of pics on mobile and bad network connections.

-------------------------

digitalSloth | 2024-01-15 21:21:03 UTC | #5

I'll have a look at the docs and see if its possible, this is the animation library:

https://github.com/LottieFiles/lottie-player

-------------------------

0x3639 | 2024-01-15 23:17:37 UTC | #6

[quote="digitalSloth, post:3, topic:1763"]
The ‘dna’ animation is 17mb and the intro animation is 3mb,
[/quote]

I wonder if the best option is to try and compress these?  Or render at lower resolution possibly?

-------------------------

digitalSloth | 2024-01-16 16:55:19 UTC | #7

They're actually .json files so I dont think we can compress them. 

Iv not seen an option for disabling them only on mobile/slower connections in the docs

-------------------------

cagri | 2024-01-16 21:51:26 UTC | #8

What is the purpose of using json files for an animation?

-------------------------

coinselor | 2024-01-17 01:24:13 UTC | #9

Check it out yourself: https://lottiefiles.com

-------------------------

0x3639 | 2024-01-17 10:47:53 UTC | #10

https://github.com/zenon-network/zenon.network/pull/12

-------------------------

cagri | 2024-01-18 14:41:39 UTC | #11

I've compressed video and updated Lottie file, please check.

https://github.com/zenon-network/zenon.network/pull/14

-------------------------

cagri | 2024-01-19 09:53:24 UTC | #12

Can you check these as well?

![image|690x64](upload://xlmKULenTCocLVOBdixnHX0KZJZ.png)

-------------------------

