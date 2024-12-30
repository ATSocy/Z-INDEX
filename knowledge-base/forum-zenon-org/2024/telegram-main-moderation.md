Thread: telegram-main-moderation
0x3639 | 2024-03-27 15:19:49 UTC | #1

We are discussing ways to improve the Main Telegram channel.  Big picture thoughts:

1) Improve the experience of a new community members in TG Main
2) Direct traffic to the interested channel ASAP

## Improve TG Experience
The general experience in TG Main is not inviting to new contributors.  How does everyone feel about implementing more strict guidelines to prevent this soft of behavior?  If community members want to have "fun" in TG we can do that in the TG Community Channels.  

I personally think this is needed.  We continue to get feedback from new users that TG Main is toxic and does not welcome new participants.  

## Direct Traffic
TG Main could be used to onboard new community members / contributors and then we can direct them to different channels for more specific interactions.  If someone wants to participate in marketing, they can request to join the Slack channel.  If someone wants to get involved with development, they can request to join matrix.  Etc.

Thoughts?

-------------------------

cryptocheshire | 2023-11-06 22:18:49 UTC | #2

Good idea. We'll have to hire mods.

-------------------------

0x3639 | 2023-11-06 23:09:01 UTC | #3

Personally I think we can implement this with the community we have today.  As we grow and get more new people I think we will need help.  But until then, I think we can impose some "rules" on our community and improve the user experience many times.

-------------------------

mehowbrainz | 2023-11-07 02:49:02 UTC | #4

I think we should make this a paid role to get consistent contribution. I'd think we need a few to cover the various timezones. 

If you vote to pay the mods, post your thoughts on the daily value paid to each mod. Preferably in USD value converted to ZNN. We don't want to be paying today, what's equivalent to $500 per day down the line.

If we can't find someone from community, I can find someone within hours via a paid job post.

[poll type=multiple results=always min=1 max=1 chartType=bar]
* Pay the mods
* Don't pay the mods
[/poll]

-------------------------

ImperiumBNC | 2023-11-07 06:21:48 UTC | #5

Great idea, thanks for bringing up the subject.

-------------------------

aliencoder | 2023-11-07 08:21:34 UTC | #6

I can't believe paying the mods is really an option. We have so many active community members in Telegram.. an outsider won't bring any value compared to an OG community member.

-------------------------

SugoiBTC | 2023-11-07 08:39:47 UTC | #7

[quote="0x3639, post:3, topic:1673, full:true"]
Personally I think we can implement this with the community we have today. As we grow and get more new people I think we will need help. But until then, I think we can impose some “rules” on our community and improve the user experience many times.
[/quote]

I agree with this. As of now our community is still fairly small and has remained the same over the years, but if we want to make our main TG channel more welcoming to newcomers, we will need to moderate it more by keeping off-topic banter in the community channels. 

I'm an advocate for free speech, and the only thing that would worry me is that long term community members get "muted" for behaving as they always do, setting up strict guidelines could alienate them. But if we want to be seen as more professionally, having stricter guidelines is necessary in order to grow.

For now it feels like keeping it NoM related should suffice in the Main TG channel, and if there's a need for more moderation I'm happy to contribute (with the community's blessing of course).

-------------------------

0x3639 | 2023-11-07 13:32:43 UTC | #8

[quote="aliencoder, post:6, topic:1673, full:true"]
I can’t believe paying the mods is really an option. We have so many active community members in Telegram… an outsider won’t bring any value compared to an OG community member.
[/quote]

Let's be honest.  There are a few people who make the environment bad.  We need to establish rules to prevent that behavior and enforce it.  We have 3 admins in there today.  We are all on different time zones.  It does not take too much effort to hit "ban" once a day.  

For example, when someone answers a question wrong on purpose to confuse or mock a new community member, that should be insta delete / ban.   

And, if we "hire" a mod how will they keep track of the alts and alts of alts.  We will need to establish rules for a 3rd party to enforce regardless.  

My recommendation is we spend time to establish simple rules and try to enforce with the admins we have today.  When those admins cannot handle the workload, we outsource.

-------------------------

mehowbrainz | 2023-11-07 14:34:26 UTC | #10

If a few community members are up for the responsibility then great, but we should be consistent with efforts. Most admins are already spread thin. I'm the type to put in place low-cost paid mods and not have to worry about the problem anymore. Plus I think anyone who is consistent deserves some reward for efforts, whether now or a promise for payment in the future once ZNN is more valuable.

-------------------------

mehowbrainz | 2023-11-08 19:42:13 UTC | #12

Or we hire a dev to write 2 GPT bots for us, one for Telegram and another for Discord. Feed it the moderation and enforcement rules. A one time cost that'll never ask for a raise.

-------------------------

cryptocheshire | 2023-11-08 19:43:54 UTC | #13

Wholeheartedly support this. Humans are not the best mods

-------------------------

mehowbrainz | 2023-11-08 20:03:56 UTC | #14

https://github.com/SoulNaturalist/AutoModeratorTelegramChatGPT should test it out.

> The AutoModeratorTelegramChatGPT is designed to automate the moderation of Telegram chats using OpenAI's GPT. The bot offers the following functions:

> 1. Spam filtering through OpenAI's ChatGPT model.
> 2. Customization of moderation rules according to user needs.
> 3. Translation of messages for moderation in non-English chats.
> 4. Deletion of messages identified as spam.
> 5. Optional banning of users who send spam messages.

> This bot is implemented in Python and uses the aiogram library to interact with the Telegram API, the googletrans library for translation, and the OpenAI API to generate responses from ChatGPT. It can be easily configured to suit different moderation needs and languages, making it a versatile tool for community management on Telegram.

-------------------------

sol | 2023-11-08 20:44:51 UTC | #15

We can probably avoid a costly dependency on OpenAi if we train our own model.
Huggingface already has [some for spam detection](https://huggingface.co/ZachBeesley/Spam-Detector).

It should be pretty simple to build these bots for Telegram and Discord, if they're not already available.

-------------------------

Stark | 2023-11-08 22:45:47 UTC | #16

AI combined with a number of experienced community volunteers should keep the individual workload very light, and with continuous coverage.

-------------------------

mehowbrainz | 2023-11-09 00:02:55 UTC | #17

AI bots for moderation aren't widely available yet, at least I couldn't find anything great (other than the one posted above). If the OpenAI credits < paying a salary = win.

-------------------------

romeo | 2023-11-12 08:29:34 UTC | #18

I think we should roll with stricter main rules with the community mods we have now and just direct off-topic posts to the original community channel (unofficially associated with main) - purely due to number of users already in that chat.

Also we need to introduce a response bot ASAP, even if just for a few prompts (/ca for the Eth contract address, /wallet for links to Syrius, and maybe /az for the 3 latest AZ proposals)

-------------------------

