Thread: telegram-plasma-bot
0x3639 | 2023-06-08 19:07:14 UTC | #1

Some time ago Alien Valley submitted an AZ for 50,000 QSR to be used with the [Telegram Plasma Bot](https://forum2.zenon.org/t/telegram-plasma-bot-improvements/488).  The bot was used by the community, but the bot has some issues.  It fails frequently.  I cannot get the code to run.  Unfortunately, @alien-valley.io cannot support the bot at this time and he gave me the private key to the 50,000 QSR

What do you want me to do with this 50,000 QSR?

[poll type=regular results=always chartType=bar]
* Hold onto the 50,000 QSR and wait for someone to fix the bot
* Unfuse all plasma and return the 50,000 QSR to the AZ fund
[/poll]

-------------------------

0x3639 | 2023-05-14 00:49:04 UTC | #2

I think it's 50K.  TBH I have not looked.

-------------------------

romeo | 2023-05-14 02:14:10 UTC | #3

Would be good to get the bot back up and running, can we run a bounty (like 10% of the qsr) as reward for someone to get it running and support it? Then the rest can be used for fusing

-------------------------

sol | 2023-05-14 07:41:17 UTC | #4

@sumamu does this work?
https://github.com/HyperCore-Team/testnet-telegram-faucet

-------------------------

sumamu | 2023-05-14 09:54:12 UTC | #5

Barely, but it wont be appropriate for the plasma bot anyway.
GPT-4 might be able to fix the plasma bot.
Try feeding the code into it and then asking it to fix the issues.

-------------------------

0x3639 | 2023-05-14 10:40:42 UTC | #6

good idea.  I'll try that.

-------------------------

rexznn | 2023-05-14 23:22:04 UTC | #7

@0x3639 if you're busy w other things I don't mind taking a look at it too. No guarantee I figure it out though.

-------------------------

0x3639 | 2023-05-15 00:55:46 UTC | #8

That would be great. I do think this is a useful tool.  If you can get it working I'm happy to run on my infrastructure. I also think the fix would be eligible for an AZ.  

I think we should consider adding a function that removes plasma automatically:
1) Either remove it automatically after X hours, or
2) FIFO when we run out of QSR.  For example, once we have fused X QSR and are left with Y QSR left, we should automatically unfuse the first ZTS address in the DB allowing new users to fuse plasma.  

Right now I think it just runs out of QSR and stops working.  @coinselor and I were never able to get it to run.  I'll look for our prior conversations and post them here.

https://github.com/alien-valley/plasma-bot

-------------------------

sumamu | 2023-05-15 09:20:09 UTC | #9

[quote="0x3639, post:8, topic:1434"]
* Either remove it automatically after X hours, or
[/quote]

You can only cancel a fuse entry after 10 hours. So we could just make a thread that checks every hour and cancels all fuse entries that are cancellable.

This information should be included in the message sent to the user after a successful fuse: your plasma will expire in 10 hours. Come back if you need more.

-------------------------

0x3639 | 2023-05-15 09:50:48 UTC | #10

I tried bard to fix it.  It was 100% WRONG.

![Screenshot 2023-05-15 at 4.50.02 AM|690x194](upload://81kq8LwfhiC0O89Zv2zrvM3S2Al.png)

-------------------------

NeoShredder | 2023-05-15 11:25:12 UTC | #11

May be the prompt needs to be more specific
It's written in typescript isn't?
Maybe gpt4 is more helpful

-------------------------

sumamu | 2023-05-15 15:04:02 UTC | #12

Try feeding the index.ts file to GPT4. Sometimes when you ask it to access a link directly, it just says it can access it, but it actually can't unless you're using a plugin.

-------------------------

0x3639 | 2023-05-15 15:06:15 UTC | #13

From ChatGPT 4.0

Your TypeScript code seems to be mostly correct and well-organized. I can't see any syntax errors or any issues that would cause immediate failures. However, without the context of the external modules and the database, it's hard to definitively say if there are logical errors, data inconsistency issues, or potential runtime errors.

Here are a few general tips to improve the code:

1. Type Assertion: You use `msg.from!.id.toString()` to convert the ID into a string. Here, you are asserting that `msg.from` is not undefined or null. This is dangerous if the `from` field is missing for any reason, as it will cause a runtime error. You should check if `msg.from` exists before accessing its properties.
2. Promise Handling: In the `main` function, you are creating a new Promise that never resolves. This might not be what you want. If you want to keep the script running indefinitely, you can just remove the `await new Promise(() => {})` line.
3. Error Handling: The code could benefit from more robust error handling. For example, if any of the `await` statements fail, it could lead to unhandled promise rejection warnings. Consider wrapping your `await` statements in try-catch blocks to handle any errors that could be thrown.
4. Commenting: Although your code is quite self-explanatory, adding more comments, especially for complex logic, would improve maintainability and readability.
5. Data Validation: Validate the incoming data before processing it. For example, when parsing the address and amount in the `fuse` function, if either is invalid, you simply return an error message. It would be better to check if they're valid before trying to parse them.
6. Code Redundancy: In the `list` function, you are looping through `user.entries` twice. This could be optimized to a single loop.

Remember, these are just suggestions and may not necessarily apply depending on your exact use case or requirements. Always test your code thoroughly in various scenarios to ensure it behaves as expected.

-------------------------

0x3639 | 2023-05-15 15:06:53 UTC | #14

maybe I can try in Github autopilot.  I'll try that next.

-------------------------

sumamu | 2023-05-15 15:12:46 UTC | #15

But which part of the code isn't working? It is probably a logical error, so GPT4 won't be able to identify it, but if we'd know the issue and described it to GPT4, it could implement the changes.

-------------------------

0x3639 | 2023-05-15 15:29:30 UTC | #16

I need to go back through the old posts.  We cannot even get it to run.  It throws multiple error messages.  We will dig in and report back.

-------------------------

sumamu | 2023-05-15 16:32:27 UTC | #17

That is usually caused by an incompatible version of NodeJS. I recommend using NVM (Node Version Manager) and giving the following LTS versions of NodeJS a try: 12, 14, 16, 18.

-------------------------

coinselor | 2023-05-20 01:51:39 UTC | #18

I got it "running" using NVM to install NodeJS 16.20.0. 

![image|690x128](upload://yzytvoIH3EASxXjXv6iCOAV0umf.png)

Haven't tried any functionality yet. Waiting for node to sync (trying MoonBaze's znnd + newest chrome extension big int patch).

What I've done:

- Install NVM `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash`
- clone plasmabot repo
- run `nvm install 16`
- pm @BotFather /netbow to get the TELEGRAM_TOKEN
- add token and rename .env.template to .env
- add scripts property to package.json so we could "npm start" as suggested by GPT-4 :stuck_out_tongue: 
```
"scripts": {
  "start": "ts-node src/index.ts",
  "test": "echo \"Error: no test specified\" && exit 1"
}
```

- run znnd
- run `npm start` 


There are a lot of deprecated issues everywhere, but should be functional regardless.

-------------------------

0x3639 | 2023-05-20 10:15:11 UTC | #19

awesome.  I'll try this out today.

-------------------------

mehowbrainz | 2023-05-22 14:45:57 UTC | #20

The zenon.org dev will give it a try as well.

-------------------------

digitalSloth | 2023-05-24 20:12:45 UTC | #21

Iv been working on an alternative solution to this, but given @coinselor has figured out the existing telegram bot not sure it'll be needed, let me know what you think.

This is a web based bot rather than telegram but it could be extended to support telegram and discord. You can select the level of plasma you want and the time its fused for varies depending on the level so low = 48 hours, medium = 24 hours and high = 12 hours. Its not quite finished yet but wont take too long to finish if theres a need for it.

![Screenshot 2023-05-24 at 9.08.37 pm|690x495](upload://I60HjbGb7HTFMCPUYTjoco7m2I.png)

![Screenshot 2023-05-24 at 9.09.09 pm|690x408](upload://2FTE4nO9TvbTXyQMV98xYYnOeCg.png)

![Screenshot 2023-05-24 at 9.09.21 pm|613x500](upload://w3Xil3bpini9o3osnTN4zAc9aLI.png)

-------------------------

0x3639 | 2023-05-25 14:00:51 UTC | #22

This is awesome.  The current bot is very dumb and has zero functionality.  Request QSR and it stays there until it runs out and then crashes.  If you do this I can see your site become a hub for a QSR marketplace.  I highly recommend you finish this b/ it could be a revenue center to help support your site!

-------------------------

mehowbrainz | 2023-05-24 23:53:40 UTC | #23

Well done! When are you planning to release this?

-------------------------

digitalSloth | 2023-05-25 07:02:56 UTC | #24

Thanks! I'll aim to get it live early next week, just a few things to tidy up but the main functionality is working. If anyone wants to test it let me know

-------------------------

0x3639 | 2023-05-25 14:02:39 UTC | #25

I'm happy to test.  And, if the community / pillars support it I can send the QSR to you.  Maybe we submit a 1 ZNN for AZ and I request the approval to send the QSR to you.

-------------------------

digitalSloth | 2023-05-25 16:07:28 UTC | #26

Thanks, will DM when it’s ready for testing. Good idea submitting a AZ to get approval for sending the QSR, will update this thread when the bot is finished and go from there

-------------------------

sol | 2023-05-28 18:13:25 UTC | #27

Great work, zir! 
Do you have any strategies to mitigate botting?

-------------------------

digitalSloth | 2023-05-28 19:48:56 UTC | #28

Good question, currently the logic prevents the same address getting plasma while there is already an active entry on the address but I can also add IP based rate limiting and a captcha to the form.

-------------------------

0x3639 | 2023-05-28 21:02:41 UTC | #29

I tried that.  And it worked.

-------------------------

digitalSloth | 2023-05-29 14:45:54 UTC | #30

The plasma bot tool is available for testing: https://zenonhub.io/tools/plasma-bot

Rate limiting has been set to 1 successful request per minute per IP address and theres hidden honeypot fields in the form to prevent bot submissions.

It has 1000 QSR available at the moment but if everyone is happy I'll coordinate with @0x3639 to submit an AZ application to request the transfer of the 50K QSR from the old bot, when thats received I'll transfer the initial 1000 QSR out of the bot and let it run with the 50K.

These are the current QSR levels for the different options: 
 - Low = 20 for 48 hours
 - Medium = 80 for 24 hours
 - High = 120 for 12 hours

-------------------------

mehowbrainz | 2023-05-29 15:02:13 UTC | #31

Epic, we can finally put the Telegram bot to rest. Congrats on this tool.

-------------------------

romeo | 2023-05-29 22:32:54 UTC | #32

great work - I would argue an AZ just to cover the transfer of QSR isn't needed. It was originally voted in to provide the bank for the plasma bot - community sentiment here/TG should suffice

-------------------------

0x3639 | 2023-05-30 12:53:19 UTC | #33

@digitalSloth do you have an address where you would like the funds sent?  If you can post that here I'll submit the AZ requesting approval.  We should probably do that just to be safe.  Even though it makes logical sense to do it.  I would feel more comfortable if we got approval.

-------------------------

digitalSloth | 2023-05-31 07:31:59 UTC | #34

Sure the address is:

z1qzzavvq2zywv77ts2e9yntc3y24qetjh0x0aj4

-------------------------

TrevorLeahy3 | 2023-06-05 10:59:14 UTC | #35

Plasma Bot working great here.

-------------------------

mehowbrainz | 2023-06-08 16:57:59 UTC | #36

Just realized that the tool isn't linked from your navigation menu.

-------------------------

digitalSloth | 2023-06-08 17:24:55 UTC | #37

I wanted to let it run for a bit before linking it incase there were any issues, but it looks to be working well so I'll get the nav updated soon

-------------------------

mehowbrainz | 2023-06-08 17:36:05 UTC | #38

Topic moved to #development:funding-staging

-------------------------

digitalSloth | 2023-06-08 18:43:54 UTC | #39

Iv submitted an AZ requesting the transfer of funds from the old bot

https://zenonhub.io/accelerator-z/project/65b69f2f1b634b23dfe19fa7fd2647c06c2d1303af49d4441f12b0c910b42207

-------------------------

mehowbrainz | 2023-06-08 19:07:01 UTC | #40

Topic moved to #development:funding-submissions

-------------------------

dat_she_pepe | 2023-06-08 22:41:20 UTC | #41

Voted yes

-------------------------

