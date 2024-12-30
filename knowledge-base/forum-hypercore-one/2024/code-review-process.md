Thread: code-review-process
sol | 2023-07-20 17:09:22 UTC | #1

Starting a thread to discuss a more formal process to review, test, and accept code that is submitted to the zenon-network repos. 

Everyone is welcome to participate.

-------------------------

sumamu | 2023-07-28 11:37:58 UTC | #2

So... now what? :smile:

-------------------------

sol | 2023-07-29 18:44:31 UTC | #3

I wanted to give everyone the opportunity to voice their opinions without my influence, but...

Anyways, after [informing us about his plan](https://t.me/zenonnetwork/303962), Mr Kaine [sent invitations to many community developers](https://forum.hypercore.one/t/github-com-zenon-network/160/3) to help maintain or administrate the official /zenon-network Github repos. 

Congratulations to everyone involved! 

Now, we need to come to an agreement on code governance. 
We cannot expect anyone to override maintainer consensus, even if they have the power to do so.


-----------------------

Each project has an x of n threshold for code acceptance.
To my knowledge, they all require 2 of n maintainers to approve PRs.
The exception is go-zenon, which requires 3 of n approvals.

Consider the [Contributing Guidelines](https://github.com/zenon-network/syrius/blob/master/CONTRIBUTING.md) and [Code of Conduct](https://github.com/zenon-network/syrius/blob/master/CODE_OF_CONDUCT.md).

Developers should hold each other accountable for delivering high quality, functional, valuable improvements. Of course, these goals are subjective. As the subject matter expert in your own domain, I know you'll do your best to ensure the codebase is maintained well.

I think there should be an expressed desire for a particular change before it's implemented. 
This can come from a community member, any developer, anyone; as long as there seems to be a need, we can probably justify the change.
This expression can be made on any social media, though I would prefer if it's captured in a Github issue to simplify the tracking of progress.
We can also use Github Project boards.

Some updates will take hours to validate and test. We should try to respect each others' time; be sure that your code is complete and in working condition before asking others to review it. 

We may want to adopt a rule that the person who submits a PR cannot also approve it.

When reviewing a PR, try to submit feedback that is more verbose than 'lgtm', though it's probably acceptable in some circumstances, like one-line PRs or text changes.
Use your best judgment and express yourself if you think something should be different.

I'm of the opinion that PRs should be small in size, easy to digest and test, simple to roll back.
There will still be exceptionally large PRs for more complex initiatives, but I ask that we strive to reduce the burden of validation by making incremental code changes.
It's much easier to verify ten lines of code than 500 or 5000.

I would like us to disclose test plans with our PRs.
This is to keep ourselves accountable for quality assurance, and to inform others that a certain test scope has been covered. We may need multiple participants to validate a PR before it's accepted into production.

---------

These are all suggestions for how we should proceed. 

Try to see this from the perspective of a developer that just discovered Zenon.
* Who is able to answer their questions?
* What can they work on?
* Where can they find more information?
* How do they contribute?

Some of these questions are out of scope for this topic but we still need to answer them.

-------------------------

sol | 2023-07-28 22:58:50 UTC | #4

If anyone wants insight re: how Bitcoin Core developers have solved this: https://www.youtube.com/watch?v=CJLxwmwL-fw

-------------------------

0x3639 | 2023-07-29 09:32:33 UTC | #5

[quote="sol, post:4, topic:158"]
Bitcoin, Explained 63: The Bitcoin Core development process - YouTube
[/quote]

I listened to this.  The one take away (for me) is I think we should consider a #zenon-core-dev meeting on matrix.  Maybe we can link audio to the meeting too so people can participate by audio and chat.

-------------------------

0x3639 | 2023-07-29 09:35:49 UTC | #6

https://bitcoincore.org/en/meetings/

Here is the next #bitcoin-core-dev meeting (CST).  I'm going to attend to see how they go.

![Screenshot 2023-07-29 at 4.35.04 AM|690x408](upload://f7g3OreuICpDdtQAap9EGKTWS2V.png)

-------------------------

sol | 2023-07-31 20:50:35 UTC | #7

I consulted Chat GPT and two points stood out.

1. **Avoid Nitpicking**: Prioritize major issues over minor style nitpicks, unless coding standards dictate otherwise.

2. **Use Review Tools**: Utilize code review tools or platforms to streamline the process and keep track of comments.

Do we have any suggestions for coding standards and tools that can assist with code reviews?

-------------------------

sumamu | 2023-08-01 11:53:42 UTC | #8

I'm sure we'll find our way as we start creating, reviewing and merging PRs.

-------------------------

0x3639 | 2023-08-01 16:43:24 UTC | #9

how do you guys feel about a #zenon-dev meeting to discuss development?  

1hr max.  Voice text options.  Host on matrix.

-------------------------

sol | 2023-08-01 17:02:22 UTC | #10

Sure, we can give it a try. I'm not sure what to discuss yet, but voice chat tends to be productive.

-------------------------

0x3639 | 2023-08-01 17:04:10 UTC | #11

[quote="sol, post:10, topic:158"]
not sure what to discuss yet
[/quote]

We can publish an agenda beforehand.  I'm sure we will find things to discuss.  I'm going to listen to the BTC meeting this thursday for inspiration.

-------------------------

aliencoder | 2023-08-01 20:26:11 UTC | #12

I agree we need an agenda. There are so many things to do right now.

-------------------------

0x3639 | 2023-08-02 16:27:00 UTC | #13

[quote="aliencoder, post:12, topic:158"]
agenda.
[/quote]

Example agenda.  There is a meeting today starting in 40 minutes.  I will try to join.

https://bitcoincore.reviews/28122

-------------------------

0x3639 | 2023-08-02 19:36:56 UTC | #14

Here is what a Bitcoin PR review meeting looks like.  I cut this off at 5 minutes.  Pretty straight forward.  There is no audio.  Text only.  Would you guys like text and audio?  

https://www.youtube.com/watch?v=lunf6xUFVaA

-------------------------

sumamu | 2023-08-02 20:15:49 UTC | #15

I'd prefer text only. Otherwise we might end up having to do speech-to-text in order to figure out what's been discussed.

-------------------------

0x3639 | 2023-08-03 09:10:32 UTC | #16

here is the output of that meeting yesterday

https://bitcoincore.reviews/28122

-------------------------

0x3639 | 2023-10-06 18:41:33 UTC | #17

Bringing this topic back based on our Dev meeting today.

Here is an article that was shared a few months ago on how to contribute Pull Requests to Bitcoin Core.  

https://jonatack.github.io/articles/how-to-contribute-pull-requests-to-bitcoin-core

-------------------------

0x3639 | 2023-10-06 18:43:12 UTC | #18

Another useful post 

https://github.com/bitcoin/bitcoin/blob/master/CONTRIBUTING.md

-------------------------

