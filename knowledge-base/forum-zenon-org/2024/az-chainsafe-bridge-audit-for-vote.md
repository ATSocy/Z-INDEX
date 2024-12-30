Thread: az-chainsafe-bridge-audit-for-vote
0x3639 | 2023-04-26 17:22:31 UTC | #1

@romeo and @sumamu and I are talking to the ChainSafe team to audit the Solidity contract ONLY.  They have proposed the following.

--- 

Estimate: 1 eng-week @ USD$17,000/week (Which includes their discounted rate)
Duration: 1 week
Start date: TBD (We have an available slot for next week, or after mid-June)

Note: Our service involves two auditors independently checking code before coming together to compare results and produce a report. We then give you the opportunity to fix changes, followed by the compilation of a final report after those changes are made.

--- 

We asked for an additional discount and are waiting feedback.  [ChainSafe](https://chainsafe.io/)  seems to have a very good reputation and @aliencoder recommended them over Certik.  We also asked for them to tweet their report after we make recommended changes.  

You can see some of the ChainSafe Clients here: https://chainsafe.io/audits

I am prepared to fund this with my own money and seek reimbursement from AZ at an exchange rate of $1.20 / $0.12 for every USD.  I will not negotiate this rate.  I need to form an LLC to sign this contract.  I will need to file a tax return, claiming the income and expense and expose myself to audit.  

If anyone else wants to take this on and bid a higher exchange rate (1.21 / 0.121 for example), please do so.  Otherwise what does the community think about his proposal?

[poll type=regular results=always chartType=bar]
* Yes I support this
* No I do NOT support this
* Yes I support this but bid a higher rate below
[/poll]

## UPDATED 24 April 23

ChainSafe is under contract.  We have agreed to a lower price than 17K but there could be additional engineering time if they find any critical bugs.  The community clearly support this initiative given the vote results.  I am going to submit (2) AZs that total up to $17,000 USD per the terms above.  Once approved and the assignment is complete, I will request funding for the actual cost spent.  I will document and support those costs.

AZ#1 = $12,000 USD
4,157 ZNN @ 1.20 = $4,988
50,000 QSR @ 0.12 = $6,000

AZ#2 = $5,000 USD
10 ZNN @ 1.20 = $12
50,000 QSR @ 0.12 = $6,000

AZ1 + AZ2 = $17,000
$10,988 + $6,012 = $17,000

-------------------------

tapwoot | 2023-04-18 22:13:55 UTC | #2

security is important, def pays for itself

-------------------------

Jeron | 2023-04-19 08:23:42 UTC | #3

It'd be great to get the solidity contract audited. 

Do they have the capability/willingness to audit the NoM code updates as well? Any idea on price for this?

I assume it would cost quite a bit more, but may be worthwhile given the potential impact of a bridge hack.

-------------------------

romeo | 2023-04-19 09:30:16 UTC | #4

We haven't asked yet for anything else, need to solve a few issues first before moving ahead with this audit (KYC, payment etc) and then see where it goes

-------------------------

sumamu | 2023-04-19 14:08:56 UTC | #5

This is exactly the kind of community initiative that moves the entire project forward. I'm backing @0x3639 and I think the sooner we get it done, the better. There was an opening next week and if we'd manage to get that one we might even have the bridge audited before it's even launched.

As I mentioned on TG, [ChainSafe even developed a bridge (Sygma)](https://github.com/ChainSafe/chainbridge-solidity) so they must have the necessary experience to audit one.

-------------------------

0x3639 | 2023-04-19 14:19:27 UTC | #6

Awesome.  Thank you.  I'm ready to go once they get back to us on a final price.  We can have them signed up by tomorrow.

-------------------------

dat_she_pepe | 2023-04-19 20:05:08 UTC | #7

I support that even if I still think Gorg is Mr. Kaine

-------------------------

0x3639 | 2023-04-20 13:10:37 UTC | #8

looks like everyone supports this.  I'm trying to work out final details today.  Will report back.

-------------------------

0x3639 | 2023-04-20 21:24:26 UTC | #9

We come to an agreement.  I will be signing the agreement and they will start work on Monday next week.  They have agreed to a lower price but I might be subject to a confi, so I need to read that before sharing the number.  It's less than the 17K approved in the vote above.  

FYI - @sumamu @aliencoder

-------------------------

0x3639 | 2023-04-21 00:51:58 UTC | #11

I removed the Scope of Work.  I want to double check it's not confidential.

-------------------------

DrD3 | 2023-04-21 06:57:23 UTC | #12

Thank you for your services ser!! 

Since Chainsafe's going to be initiating the bridge's audit on Monday- wouldn't it be more reasonable to push the launching of Sumamu's bridge until they give the green-light?

-------------------------

sumamu | 2023-04-21 08:30:57 UTC | #13

Absolutely, the deployment of the bridge solidity contract will be postponed until after the audit is completed and all vulnerabilities are resolved (if there are any).

The network upgrade featuring the bridge embedded contract should stay on course.

-------------------------

mehowbrainz | 2023-04-21 23:10:53 UTC | #14

I think this topic should've been in #operations:funding-staging category otherwise we can make a new major category for security. It's not entirely a development task while it does touch the subject. If that's okay, I'd like to move it. Also the #az tag used is not what we use here to highlight an AZ candidate, we use the staging sub-categories cc @SugoiBTC

-------------------------

0x3639 | 2023-04-24 10:47:14 UTC | #15

AZs submitted for approval.

https://www.zenon.info/az-for-chainsafe-audit/

![image|435x499](upload://mJ45WGotYE9ZK2Gu15Qoe651o43.jpeg)

![image|432x500](upload://hTtI2ixP3jDK35BIiy92d7BrI4N.jpeg)

-------------------------

vilkris | 2023-04-24 16:19:00 UTC | #16

Thank you for pushing this forward 0x, great work. Did I understand correctly that ChainSafe may bill more than the estimated $20k if they find a critical bug they need to investigate?
If the actual expenses go over $20k, I'm assuming you'd make a third AZ request to cover them?

-------------------------

DrD3 | 2023-04-24 19:07:40 UTC | #17

It's only fair.

-------------------------

0x3639 | 2023-04-24 21:32:56 UTC | #18

The actual cost is less than 20K.  I'll DM you the amount.  By asking for up to 20K we should have enough to code the audit, filing fees, and time to research 1 or 2 critical bugs.  If we exceed 20K I would need to ask for a 3rd AZ to cover that cost, but I don't think we will blow that budget.

-------------------------

zyler9985 | 2023-04-25 08:28:24 UTC | #19

It'd be good if we can link the results of the audit here in this thread (in addition to whereever else it's being posted). I'm making a thing which discusses the bridge, and my link about the chainsafe audit goes to this forum post.

-------------------------

romeo | 2023-04-25 09:40:37 UTC | #20

We'll create a dedicated topic and pin it when the results are in I think, will give newcomers confidence when searching info about the bridge hopefully

-------------------------

0x3639 | 2023-04-25 20:55:01 UTC | #21

I just made the first payment to ChainSafe - $7500.

-------------------------

mehowbrainz | 2023-04-26 17:25:40 UTC | #22

Topic moved to #operations:funding-submissions

-------------------------

NeoShredder | 2023-05-03 11:04:12 UTC | #24

@0x3639 any update from chainsafe?

-------------------------

0x3639 | 2023-05-03 15:50:20 UTC | #25

We expect the final report today or tomorrow.

-------------------------

aliencoder | 2023-05-05 19:40:20 UTC | #26

What's happening? Any news?

-------------------------

sol | 2023-05-05 19:51:30 UTC | #27

https://www.zenon.info/chainsafe-zenon-network-bridge-audit/

-------------------------

aliencoder | 2023-05-06 07:01:14 UTC | #28

@sumamu congrats for all your hard work!

-------------------------

NeoShredder | 2023-05-10 16:43:46 UTC | #29

Did chainsafe finalize the audit? They made only 1 tweet. How much social media coverage will they do? I think we paid about 7k for social media didn't we ?

-------------------------

romeo | 2023-05-10 05:39:33 UTC | #30

Audit is finished and delivered. We didn't pay for any social media (that was a different company and quote).

They've agreed to tweet now that it is finished though, we are just working on specifics with them.

@0x3639 made a blog post about the audit results

-------------------------

cryptocheshire | 2023-05-10 08:06:56 UTC | #31

Will they list the audit on their website, though?

-------------------------

romeo | 2023-05-10 09:09:20 UTC | #32

We've asked for it to go on that audit landing page where they list the other customers too, waiting to hear back from their comms guy

-------------------------

aliencoder | 2023-05-10 13:29:45 UTC | #33

We're live, boyz!!

https://chainsafe.io/audits

Maybe @ZNNAYIID can help with a nice cover image for the post.

-------------------------

cryptocheshire | 2023-05-10 17:45:14 UTC | #34

Nice! And yeah, definitely need a cover image

-------------------------

ZNNAYIID | 2023-05-10 19:50:02 UTC | #35

![image|690x378](upload://ebdMyarTSOxJFX8QBogubLtn6sf.png)
![image|690x384](upload://gQAjA9JDAxH9n90TzLJanA5vDZE.png)

[poll type=regular results=always chartType=bar]
* ZENON NETWORK
* ZN LOGO
* NONE
[/poll]

-------------------------

0x3639 | 2023-05-10 19:51:43 UTC | #36

Guys,

I'm requesting reimbursement for the ChainSafe Audit.  I will leave this here for questions for 24 hours, and then I will request payment from AZ.  

$15,000 Audit
$150 LLC Filing Fees
$1,128 ETH to Deploy Contracts
$16,278 TOTAL

Request tabulation and evidence of payment below.

## Reimbursement
AZ#1 = $10,000 USD
3,333 ZNN @ 1.20 = $4,000
50,000 QSR @ 0.12 = $6,000

AZ#2 = $6,277 USD
231 ZNN @ 1.20 = $277
50,000 QSR @ 0.12 = $6,000

## Check
AZ1 + AZ2 = $15,150
$10,000 + $6,277 = $16,277


Payment #1
https://etherscan.io/tx/0xe325aea2797fa8326b66fce48a3a367d87ceab0f8ddc5dc8597d2da9476bc3f6

![image|531x500](upload://g1kVDxM6NgUs23hAmz0PJSHtSaC.png)


Payment #2
https://etherscan.io/tx/0xc7184b145dd26452989407f16eb4cc1e8fabb07d6023958c19e9fc64a4f12572

![image|552x500](upload://8LGc6nqnHB09e04fh5ICxYeIWbA.png)

Payment #3 - IL LLC Filing Fee

![image|690x273](upload://sknZw7OHyFL86yFkmb88gc9FyXd.png)

Payment #4 - 0.61 $ETH to deploy Contracts
at $1850 x 0.61 = $1,128.50 
This address has a surplus amount of 0.11 ETH.  We can leave it there for future use.  

Evidence of payment
https://etherscan.io/address/0x073a8c4c668c3a42cf5df61ec84a7e83872902f8

-------------------------

romeo | 2023-05-11 05:59:09 UTC | #37

Layiid can you send me the file on TG and I'll forward it to chainsafe ?

-------------------------

0x3639 | 2023-05-12 16:31:03 UTC | #38

I just submitted (2) Phases for reimbursement for costs incurred per the summary above.  

![image|690x429](upload://a9R5AhUT3cTzM1GqxH4NJtQM3JP.png)

![image|690x348](upload://jkIlinYbgdndmTOnzlYYzr8jRnN.png)

-------------------------

dat_she_pepe | 2023-05-12 21:19:33 UTC | #39

Voted no because my dungeon & dragon dice said so

-------------------------

0x3639 | 2023-05-12 21:56:42 UTC | #40

sir...  I just spent 17K USD on the audit to benefit the network.  Everyone supported this decision.  I understand you might be joking, but this sets a bad example for others to do the same.  I hope you reconsider your vote for the benefit of future contributors.  

![Screenshot 2023-05-12 at 4.54.22 PM|690x230](upload://qHnnvLsZc4J9iWQnr7CSoptCK6B.png)

-------------------------

dat_she_pepe | 2023-05-13 11:24:08 UTC | #41

Another troll which worked flawlessly AHAHAHAHAHAHHAHAHAHAHA I AM INEVITABLE


(I obviously voted yes you giga boomer)



(btw I don't care what others do, or what they think is an exemple. This community is 90% made of people I can't stand so what they vote is non of my business.)

-------------------------

