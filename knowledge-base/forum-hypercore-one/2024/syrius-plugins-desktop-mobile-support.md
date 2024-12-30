Thread: syrius-plugins-desktop-mobile-support
aliencoder | 2023-09-13 20:08:49 UTC | #1

Inspired by **Metamask Snaps**, I want to bring into attention **Syrius Plugins**. Web apps directly integrated into Syrius that can request signatures, initiate transactions and more via the `Javascript` bridge.

Since for mobile is trivial to integrate a `webview`, we needed a viable solution for desktop. Now we have a good candidate:

https://pub.dev/packages/desktop_webview_window

I've tested this solution and the good part is that it opens a *separate* window where it can load web content from the Internet.

We can leverage the `JS` [bridge](https://github.com/MixinNetwork/flutter-plugins/blob/77f03330001941f0ac303de6276dd2380f5bcc7e/packages/desktop_webview_window/example/lib/main.dart#L67) to facilitate the communication between the `Dart` code and the `Javascript` code.

-------------------------

sol | 2023-09-14 23:17:11 UTC | #2

Do you have any use cases in mind? 
I'm wondering if this will introduce complexity and compatibility issues that outweigh the benefits.

-------------------------

aliencoder | 2023-09-16 10:19:24 UTC | #3

[quote="sol, post:2, topic:210"]
Do you have any use cases in mind?
[/quote]

Extending the capabilities of Syrius with web applications.

[quote="sol, post:2, topic:210"]
I’m wondering if this will introduce complexity and compatibility issues that outweigh the benefits.
[/quote]

It will *reduce* complexity and compatibility issues because all the web app logic will be contained in the `webview` instance.

Instead of writing Dart code directly into the Syrius codebase (that will be compiled and shipped alltogether), plugin developers will be able to interact with Syrius from a familiar web app. We can create a Plugin Store as a web app and list only pre-approved plugins.

Also plugins can list what features they need to run (`sign transactions`, `get wallet balance`, etc.).

Think of it like `Syrius` <-> `WalletConnect` <-> `Browser` except the `webview` aka `browser` is built into `Syrius`: 

`Syrius` <-> `JS bridge` <-> `webview`

-------------------------

