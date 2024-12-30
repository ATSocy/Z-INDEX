Thread: typescript-sdk
dexter703 | 2022-05-04 11:19:51 UTC | #1

Hey fellow alienz, long time no hear. We’ve participated some time ago in Warpdrive to start building a Typescript SDK. 

For those who don't know, Typescript is the programming language for application-scale JavaScript. Basically, Typescript simplifies JavaScript code, making it easier to read and debug. The SDK will streamline the overall front-end development for any sort of products futurely developed within NoM. 

3 months of development later, me and my amazing dev team managed to get this Typescript SDK done. I have to admit that it wasn’t easy because it required a quite profound understanding of both Typescript, Go and also some cryptography knowledge, but it was a great learning journey.

I’ve just created a dedicated Github: https://github.com/dexter703/znn-ts-sdk 
I’ll publish soon the open-sourced repos and we're also prepping a Hyperspace submission.

Thanks in advance!

-------------------------

0x3639 | 2022-05-04 11:31:55 UTC | #2

Thank you sir!!  Look forward to the new submission.

-------------------------

0x3639 | 2022-05-04 11:34:25 UTC | #3

@alien-valley.io wanted to make sure you saw this one.

-------------------------

alien-valley.io | 2022-05-04 12:24:44 UTC | #4

Hi @dexter703 

I wasn't aware that another JS SDK was being developed.
I've created a [Telegram group](https://t.me/+AVnZJpW50ac2NzFk) specific for JS development, if you'd like to join in on the discussion. I'm working closely with PDfust to develop an extension-wallet similar to metamask.

Also, feel free to build on top of the work I've done so far. The repo can be found [here @ znn.js](https://github.com/alien-valley/znn.js)

-------------------------

Dumeril | 2022-05-04 13:26:42 UTC | #5

That’s great news!
Could you announce the status in the warpdrive channel on discord as well, please?
We’ve been using that for progress updates and to organize payouts.
@dexter703

-------------------------

Phuong | 2022-05-04 17:13:34 UTC | #6

Fantastic! Thank you for all of your hard work.

-------------------------

ZNNAYIID | 2022-05-10 14:52:20 UTC | #7

Why submitting another A Z proposal if you were part of wrapdrive? Also we got a Rust sdk for 1430 ZNN and 100 QSR just to let you know.

-------------------------

Dumeril | 2022-05-10 14:53:09 UTC | #8

Yes I was also expecting a proposal that builds on this sdk

-------------------------

0x3639 | 2022-05-10 16:48:18 UTC | #9

Did this project receive compensation for the SDK under warpdrive?

Also, @dexter703 can you please give us a sense of the number of hours spent on the project?

-------------------------

WAGMI | 2022-05-10 17:07:12 UTC | #10

need more details when asking for this much

-------------------------

Dumeril | 2022-05-10 17:28:19 UTC | #11

I’m not sure. We have a channel for coordination of that on discord; they did not use that yet. @Sigli did they receive wd funding already?

-------------------------

Dumeril | 2022-05-10 18:58:40 UTC | #13

Thank you. 

125 qsr isn’t really worth mentioning, that’s true

-------------------------

DrD3 | 2022-05-10 19:16:43 UTC | #14

I agree, a break-up of the amount of hours it would take to build this SDK would be really helpful. I believe the community agreed on a 100$ per hour for the Rust SDK, so once @dexter703  list's his phases out we can better assess how much zennies and qsr this SDK deserve?

@devs would it be fair to have a standard cost for developing an SDK (such as the 1430 zennies for the Rust SDK)? Or does the development of each SDK have to be assessed individually due to difficulty? (non-developer here :P)

-------------------------

Dumeril | 2022-05-10 19:24:56 UTC | #15

The amount of hours is a vague metric as this heavily depends on the qualification of the submitter. 
I like the current rust sdk proposal not only because it is well justified and articulated, but also because he puts a fair price on his own labor: he knows rust and he knows cryptography. So that reduces the hours he needs to get it done but it justifies a price tag of $1k/10h.

-------------------------

7nzalh | 2022-05-10 20:19:43 UTC | #16

And for reference, here's the proposal template by @romeo 
https://forum2.zenon.org/t/zenon-network-accelerator-z-proposal-template/228?u=7nzalh

-------------------------

0x3639 | 2022-05-11 13:46:43 UTC | #17

Just wanted to let everyone know that I’m holding my vote until we get some feedback from @dexter703 on open questions.

-------------------------

0x3639 | 2022-05-14 01:29:46 UTC | #18

I'm still holding my vote until we get some of these outstanding questions answered.  I posted an issue on Github asking for some interaction with us.

https://github.com/dexter703/znn-ts-sdk/issues/1

-------------------------

0x3639 | 2022-05-15 01:08:30 UTC | #19

For now I voted no due to the applicants unwillingness to answer questions about the proposal.  If they start to engage on Github or the forum I'd be happy to reconsider my vote.

-------------------------

sultanofstaking | 2022-05-15 11:27:45 UTC | #20

Same here. People submitting proposals need to realize the majority of projects launched in early days were by people w/ a good idea and little to no community involvement (starl, apsis online, etc etc). Their ideas approved then they never check back in. We need engagement not just from pillars / community but from those submitting proposals. I will always factor that into my decisions.

-------------------------

dexter703 | 2022-05-17 09:24:17 UTC | #21

Greetings everyone!

I know you have many questions, so I’ve decided to compile a summary of everything that’s been going on in hope to answer them and hopefully future ones also.

So let’s begin!

**Who am I?**

You may call me Dexter and in my lab, I’ve got a special place dedicated to the Zenon ecosystem, just as I have a special place in my heart dedicated to the Zenon community.

I’ve been around since the Public Incentivized Testnet, got caught in the hype it created. I’ve been mostly quiet since I’m more used to talking to computers rather than people, but I’ve been following everything that’s been happening.

As soon as the znn_sdk_dart repo has been published, I knew that the TS SDK has to be next. Web3 is truly amazing and it will bring a ton of opportunities and possibilities. I’ve been working with it a lot and my past experience has allowed me to understand the impact it can bring to an ecosystem.

**How did it start?**

This project has started during the warpdrive. I thought it would be possible to have a PoC during that time, but man was I wrong.

It turned out to be quite a bit more complex than I initially thought and it involved hours and hours of research and testing to figure out all the quirks:

- Hierarchical-deterministic wallet

- Cryptography

- User/contract address derivation

- Node connection

- APIs

- ABIs

- Contract interaction (staking, delegating, fusing, sentinel/pillar creation, zts creation and management)

- Plasma mechanism

- Powlinks mechanism

…and many more.

Also, keep in mind that the Syrius code was released just recently, so I only had the Dart SDK and CLI available.

**Was it difficult?**

Overall, I am estimating an investment of around 400 hours over the past 6 months. There were days when I’ve managed to go full-time and days when my attention was needed elsewhere, but I’ve managed to average around 3h/day.

The Zenon codebase is vast and porting an sdk requires a very good understanding of the code that makes everything tick:

- go-zenon (huge repo)

- znn_sdk_dart (beautifully structured, it helped!)

- znn_cli (came in handy for tinkering with every little functionality)

**What’s the progress?**

This is something I’m really excited to share, the SDK is complete, it is a full port of the znn_sdk_dart!

**Where’s the code?**

I put some thoughts into this. At first I wanted to publish the repo, which I can’t wait to do, however, I didn’t want to risk someone else applying and getting the credit for my sweat and tears (of joy, of course). Therefore, for that matter, I’ve decided to publish the code after the project is approved with the community. The phases will come after I’ve published the code.

**What’s next?**

The znn_sdk_ts is just the first piece of the puzzle and I’m already working on the next big thing: a browser extension that works with chrome and firefox. I believe this will really push the zenon ecosystem forward, providing anyone with fast and easy access and giving us Web3 superpowers.

Moving forward, I’ll make myself available to the community and do my best to keep in touch. I prefer to focus on my work as I think that will bring the best results.

-------------------------

alien-valley.io | 2022-05-17 10:13:45 UTC | #22

disclaimer: I find JS & TS to be the same thing. The type system alone is not a big enough difference to justify them being different.

No offence, but both the SDK and the wallet extension are projects that are already worked on by other people as well. Keeping your work private doesn't really help or protect your IP.

**No one would apply with your codebase, since the projects are voted by pillars with due diligence. This can be seen in the startup world a lot (alien valley - silicon valley - startups - it's a joke, see?) where keeping ideas secret is a bad practice. An idea is good & all, but the people behind it are more important.**

At the moment, I'm working on a [JS SDK](https://github.com/alien-valley/znn.js) as well. I've already ported the [pow-links to WASM](https://github.com/alien-valley/znn-pow-links.js) in the same day as the one it has been made open source, so arguably anyone who wanted to use it should consider it as being done (apart that it's impossible to put things in the official GitHub user).

I'd like to reuse any work that you've done so I can focus on improving things further, without thinking that what I'm working on is already deprecated because someone already made it, and I'm just reinventing the wheel. I personally don't take pride in reinventing the wheel but unfortunately I was the first one to do so.

I think that collaborating on this things would be more advantageous for everyone in the long run. I know that it's possible to steal other people's work, but the community will see that & slash any such behaviour.  That being said, I will invite you again to join the [Telegram Channel for JS development](https://t.me/+AVnZJpW50ac2NzFk) and any other developer / builder related community channels.

**Note**: even if the project is accepted, you still require to create a proposal that's accepted as well. You'll need to publish the codebase before the proposal is accepted nonetheless.

-------------------------

dexter703 | 2022-05-17 13:49:27 UTC | #23

Hi, @alien-valley.io!

My main goal here is not the TS SDK itself, but the extension, which I believe to be a game changer in the long run. 

I have seen your work and it was inspiring, in fact I have even used your instructions to create the wasm version for powlinks and use it in a webworker. 

Yes, Javascript and TypeScript are very similar, however developing web apps usually require typescript and what happens is that developers tend to overlook the JS tools that are out there. 

It wasn’t very clear to me why you haven’t applied to A-Z with the JS SDK so far and at times I have wondered about the future objectives of the repo.

I have also used this oportunity to port the SDK as a means to learn more about the inner workings of the network and it has helped me tremendously. 

Collaboration is indeed the best way to move forward and I believe we can find a way to do that.

-------------------------

alien-valley.io | 2022-05-17 14:04:10 UTC | #24

> It wasn’t very clear to me why you haven’t applied to A-Z with the JS SDK so far

I don't think there is a time limit for this things, personally.
I'll apply to AZ after the fact and hope that the community will acknowledge my work, since it's easier to justify a price tag for it that way.

> I have seen your work and it was inspiring, in fact I have even used your instructions to create the wasm version for powlinks and use it in a webworker.

Awesome! I have an [open issue](https://github.com/alien-valley/znn.js/issues/3) at the moment about porting pow links. If you get the code checked in, I'll use your work to get that done. Myself and PDfust have discussed in the past on how to design the SDK to communicate well with the extension

> My main goal here is not the TS SDK itself, but the extension, which I believe to be a game changer in the long run.

That's everyone's goal. That's why is already a work in progress. 

--- 

I'm really happy that you put in the work & all, don't get me wrong. I just don't like the attitude of "I know how to do it better, I know the truth, I'll just do it and publish it and everyone will be so grateful."

We already have a group which is doing that. They are called 'core-developers', and I try to not encourage community members to do the same.

-------------------------

dexter703 | 2022-05-21 19:40:39 UTC | #25

Hi, everyone!

Thanks for the votes, it was close but in the end it went through. 

I just wanted to let you know that I am grateful and I hope you’ll find my contribution to the ecosystem useful. 

I am preparing the repo for publishing and strive to have the code published by Monday. 

Will keep you posted!

-------------------------

SugoiBTC | 2022-05-22 04:54:29 UTC | #26

Great news! I hope you and @alien-valley.io will come to an agreement and work towards a beneficial goal of the NoM...

Good luck!

-------------------------

dexter703 | 2022-05-23 18:00:12 UTC | #27

The code is live! 

Link to repo: https://github.com/dexter703/znn-ts-sdk

-------------------------

