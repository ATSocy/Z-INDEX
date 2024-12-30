Thread: zenon-wall-zenon-fun
sol | 2024-03-27 15:20:19 UTC | #1

Hi everyone!

I decided to join the fun and make my own Zenon-themed website! I've got a few ideas for applications that don't require smart contracts so I decided to try making one.

Inspired by the [Bitcoin Eternity Wall](https://eternitywall.it/), I wanted us to have a similar place to share our messages with the world, permanently written in NoM blocks! 
Messages should be posted to the wall within 5 minutes.

Check out my new site: https://www.zenon.fun/
The Zenon Wall is located at https://www.zenon.fun/wall/
Instructions can be found here: https://www.zenon.fun/wall/info

All the code is available at https://github.com/Sol-Sanctum/sol-sanctum.github.io

![68747470733a2f2f692e696d6775722e636f6d2f444e7044796f712e706e67|690x444](upload://hgIo70zFb9jQYpgTd5BtzOElR4N.png)

-------------------------

romeo | 2022-05-05 06:27:22 UTC | #2

This is a great initiative, I can't get to the URLs at the moment though @sol 

Keen to have a look around!

-------------------------

DrunkenMoose | 2022-05-05 11:05:36 UTC | #3

nice, didn't know it was possible to send more info on a transaction! Do you know if it works with the CLI?
I see no messages so let me know ^^

-------------------------

sol | 2022-05-05 20:02:57 UTC | #4

@romeo I've had a bit of trouble with DNS and SSL but the site has been loading on all my devices.
I should be able to get SSL working today.
Do you see an error when trying to access the site?

@DrunkenMoose Yeah, I discovered it earlier this week after George mentioned it on Telegram.
znn-cli is used to submit the transaction and I have a script that scrapes momentums for messages beginning with "ZW".
Check out the [instructions here](http://zenon.fun/wall/info)

Here's an example command: 
```
.\znn-cli.exe -u ws://127.0.0.1:35998 -k <keystore> send <dest-address> 0.01 ZNN "ZW Hello ZNNAliens!"
```

Also, there should be a message on the wall. I'm surprised you don't see it...

-------------------------

romeo | 2022-05-05 20:49:57 UTC | #5

I'm getting DNS errors too

DNS_PROBE_FINISHED_NXDOMAIN

-------------------------

sol | 2022-05-05 22:54:31 UTC | #6

I've switched DNS providers and everything seems to be working on my end now.
Please let me know if it's still an issue for you.

-------------------------

romeo | 2022-05-06 00:40:28 UTC | #7

working correctly now :+1:

-------------------------

