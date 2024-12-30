Thread: znnplayground-play-around-with-the-api-endpoint
DrunkenMoose | 2024-03-27 15:20:20 UTC | #1

Hey,

Here's some info related to the ZNN playground. This is my first ZNN related project to get a better understanding on the NoM process. I am using the Alien Valley JS SDK and added all the API end-calls to the source. Currently it only works on HTTP as secure calls to the public nodes are not available currently. (so HTTPS and WSS doesn't work)

Most of the functions can be called with only a node configured, some need to have your personal address so you would need to upload the key JSON file with the password used. (you can also create a test wallet and/or download the project locally)

If a message contains JSON then you can click on it to have a fullscreen popup with the JSON formatted in a better way.

link:
[http://znnplayground.com/](http://znnplayground.com/)

API endpoint info:
[https://github.com/zenon-network/znn-wiki/blob/master/api.md](https://github.com/zenon-network/znn-wiki/blob/master/api.md)

ZNN.js github:
[https://github.com/alien-valley/znn.js](https://github.com/alien-valley/znn.js)

screenshot:
![znnplayground|689x432](upload://oJkT8jSF77i2E5TPHchg1SKxT98.png)

Hope you guys find it useful, good luck with A/Z ^^

-------------------------

romeo | 2022-04-22 11:09:03 UTC | #2

saw this when you posted it on the Telegram, very cool

-------------------------

Jeron | 2022-04-23 00:13:01 UTC | #3

This is a great way to learn about the API. Thanks for building this!

-------------------------

romeo | 2022-04-27 11:34:44 UTC | #4

@DrunkenMoose I used this in anger today to dump a list of all pillars, we are using the ownerAddress to validate Pillar owners via signed messages. Very helpful

-------------------------

DrunkenMoose | 2022-04-27 12:35:00 UTC | #5

Yea I can make python scripts etc. but it's hard for me to understand what is handy and how the overal structure is. So if you need anything like that then let me know and how it should work ^^

One of the ideas I had is to make a custom wallpaper in "Wallpaper Engine" that displays all the real-time nodes as an interactive network map with their status and how the peers are connected with each other. Would be funny to implement the znn.js SDK to have NoM data inside a wallpaper i.e. 

You have the function "stats.networkInfo" that shows all the peers, so I guess you can connect to each peer and call the function again to make a data structure. But currently I don't know how it's structured. I just want to make any kind of structure, perhaps I can do a pillar overview or something like that.

-------------------------

