Thread: syrius-sig-collaboration
CryptoFish | 2024-09-01 10:18:13 UTC | #1

Since the release of version v0.2, a number of minor changes have been picked up and implemented in the `develop` branch. Major changes such as redesigning the layout, multi wallet, address managment or notarization support require a more organized approach.

A big hurdle at the moment is the dependency on the `SliverStaggeredGrid` widget, which prevents us from using the latest flutter version. The widget is deprecated and used throughout the application and needs to be replaced with another layout widget.

There have been attempts in the past to design a new layout. Given the issues surrounding the deprecated layout, this would be a great opportunity to collaborate and redesign the layout and pickup other features along the way.

This is one such attempt, showing multi level navigation:

![multi-level-navigation|690x365](upload://ud9Bn1rRdZSlxRIjjPNSwP4AEfX.png)

But, before going any further. The main purpose of this post is to gauge interest in collaborating for this project. Ideally we would to set up a team of 2 or 3 devs who can regularly work on syrius for a certain amount of time.

You will need to be familiar with flutter/dart and will be able to pickup tasks to implement according to your skill level.

A Syrius Special Interest Group will be setup If their is enough interest and a chairman will be appointed with the following responsibilities:

- Exploring the frontier of possible work
- Getting it defined and scoped out in a trackable way
- Facilitating discussion about different options
- Helping other contributors pick up the work and see it to completion

Ideally, some record keeping would be great as well, both for internal and external purposes. Especially when it comes to attribution of work and incentives.

Please reply with your current skillset and the amount of time you're available if interested.

-------------------------

0x3639 | 2024-09-01 16:47:08 UTC | #2

I am happy to join to help with testing and "consumer" design & feedback of the UI / UX.  I will not be able to offer any coding assistance.

@sol we miss you!

-------------------------

_Warrior | 2024-09-04 21:04:12 UTC | #3

I am happy to join to help with developing the product as flutter developer.
But before start working, I suggest you about React Native Expo.

-------------------------

CryptoFish | 2024-09-05 07:57:55 UTC | #4

Hello @_Warrior, great to hear that you're interested in helping out. Can you tell something more about your experience with flutter or as a developer in general?

Syrius is a Desktop application written in flutter by the original creators of Zenon. As far as I can tell Expo is a framework for developing universal apps for Android, iOS and web.

> Create universal native apps with React that run on Android, iOS, and the web. Iterate with confidence.

This project aims to maintain and improve the codebase of the original project and not to rewrite it completely in a different environment.

-------------------------

