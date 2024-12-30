Thread: pillar-cage-mechanism
MoonBaze | 2024-03-19 11:15:30 UTC | #1

I see there is a list of pillars (Unizen, 222, bonsai, theone, zamiri) that have not produced any momentums in a while. This results in skipped momentums that lower overall network performance related to transactions per second. I was thinking we could introduce a mechanism where pillars that do not produce any momentum or have a really low ratio of produced / expected momentums in e period of time to become inactive and so skipped from the algorithm which chooses the next pillars to produce in the next 30 momentums. They could reactivate themselves later by calling a method (e.g. Activate) which enables them to be selected to produce again.

What do you think about this? If you agree, what period of time or ratio threshold do you think of?

We could even go further with slashing but that's more complex in terms of logic and implementation but ideas are welcomed.

-------------------------

0x3639 | 2024-03-19 14:19:08 UTC | #2

I think this is a great idea.  Maybe we should adopt this in phases.

## Pillar Cage Proposal

### Phase I
If you don't produce a momentum for 2 weeks you are put into a cage and removed from the list of Pillars who can produce momentums.  

If you produce a "low" rate (25% of the expected rate) of momentums for 4 weeks you are put into a cage and removed from the list of Pillars who can produce momentums.  

Pillars can reactive themselves by calling the Activate function, but needs to pay a penalty that deposits 100 ZNN into the AZ contract. 

### Phase II
Evaluate what happens in Phase I and consider options for slashing.  Maybe we can consider expanding this to AZ voting too, but I don't want to make your good proposal more controversial with something like this.

-------------------------

aliencoder | 2024-03-19 15:04:56 UTC | #3

I like this idea. It incentivizes honest behavior. We should focus on implementing Narwhal and Tusk next rather than improvising upon this placeholder consensus algorithm.

[quote="MoonBaze, post:1, topic:412"]
They could reactivate themselves later by calling a method (e.g. Activate) which enables them to be selected to produce again.
[/quote]

What happens if a Pillar calls Activate, but doesn't produce momentums afterwards?

For example, if I don't want to run Pillar infrastructure I would call this function daily to avoid getting into the cage. I suppose only Pillars are able to call this function with a valid *producer* address.

[quote="0x3639, post:2, topic:412"]
but needs to pay a penalty that deposits 100 ZNN into the AZ contract.
[/quote]

Pillars already are penalized by not getting rewards from missed momentums.

-------------------------

0x3639 | 2024-03-19 19:49:44 UTC | #4

[quote="aliencoder, post:3, topic:412"]
Pillars already are penalized by not getting rewards from missed momentums.
[/quote]

Maybe the fine will make them think about staying online and working?  It appears the 4 or 5 today that are not producing don't really care about missed momentums.  It's easy to hit "Activate" then stop caring again.  But if they hit "Activate" and pay 100 ZNN maybe they will think about staying online.  

I don't think the fine is necessary, but could help.

-------------------------

aliencoder | 2024-03-19 20:48:01 UTC | #5

[quote="0x3639, post:4, topic:412"]
I don’t think the fine is necessary, but could help.
[/quote]

We can't penalize them twice. What we can do is what @MoonBaze is proposing: excluding them from the active validator set. I've read the proposal again and that's why I've changed my mind with the monetary punishment. 

We can add the following condition for the Activate function: only callable once every 3 epochs. This way the Pillar operator will think twice before calling the function because he will miss 2 epochs worth of rewards if he fails to maintain uptime for the Pillar.

I know you're trying to get AZ funded, but we need a more sustainable way to do it for the long run.

-------------------------

0x3639 | 2024-03-20 09:50:48 UTC | #6

[quote="aliencoder, post:5, topic:412"]
We can add the following condition for the Activate function: only callable once every 3 epochs. This way the Pillar operator will think twice before calling the function because he will miss 2 epochs worth of rewards if he fails to maintain uptime for the Pillar.
[/quote]

I think this will achieve a similar outcome too.  Do you know the current time for an epoch?  For some reason I have 1 minute in mind, but that does not sound right in this context.

-------------------------

aliencoder | 2024-03-20 09:53:32 UTC | #7

[quote="0x3639, post:6, topic:412"]
Do you know the current time for an epoch?
[/quote]

1 epoch = 1 day

-------------------------

MoonBaze | 2024-03-20 10:49:07 UTC | #8

I would add a delay between Activate calls instead of fines. For example 5 days. If you call Activate but still don't produce the required minimum, you will become not eligible again at the next update at the end of the next epoch (not current epoch because you could call activate at the end and maybe have 0/0). You will have 3 more days to wait before you could call it again so a pillar could not abuse this mechanism.

It's a simple logic, I would not complicate this feature for now. I will publish a branch in the following days with the PoC implementation and tests.

-------------------------

MoonBaze | 2024-03-20 15:34:56 UTC | #9

Here is the PoC, you can run `TestPillar_Eligibility`  test in `vm/embedded/tests/pillar_test.go`. One can see that pillar 1 becomes not eligible and is not elected anymore. Once it calls the Activate method it starts to be elected again and produces.
The code is not complete and still needs work, I am thinking to create a ZIP and see the community's opinion.

https://github.com/MoonBaZZe/go-zenon/tree/cage

-------------------------

edgepillar | 2024-03-27 21:49:12 UTC | #10

I am definitely supporting expanding this to AZ voting.

-------------------------

