Thread: secret-messages-poc
vilkris | 2023-02-10 23:27:03 UTC | #1

I've been thinking of some use cases where it could be useful to be able to send secret messages on-chain (and off-chain) in such a way that only the intended recipient could decrypt the message.

Cryptography isn't exactly my area of expertise but I'm interested in the possibilities cryptography can offer us so I dipped my toes in and made a simple proof-of-concept implementation of sending encrypted on-chain messages using the [Sodium](https://libsodium.gitbook.io/doc/) cryptography library. This PoC allows you to send an encrypted message to a NoM address that can only be decrypted by the address' owner.

Since NoM uses the Ed25519 signature scheme we can convert a keypair into X25519 and then encrypt a message for a public key so that the message can only be decrypted with the corresponding private key.
This allows us to send an encrypted message to a recipient who can decrypt the message using their keypair.

The modified CLI wallet can be found here: https://github.com/vilkris4/znn_cli_dart/tree/secret_messages

The wallet requires the `libsodium` library to work.

On Windows it's easiest to download the pre-built DLL and copy it to the CLI's folder: https://libsodium.gitbook.io/doc/installation#pre-built-libraries (I used ` libsodium-1.0.18-stable-msvc.zip`)
On Mac you can use Homebrew to install `libsodium`: https://formulae.brew.sh/formula/libsodium

## Example

I added two commands to the wallet: `sendEncryptedMessage` and `decryptMessage`

An example of sending an encrypted message to address z1qrgnzs4jh2yfldarepysqgsukgdmwmqw5v0t7c:

> .\znn-cli.exe sendEncryptedMessage z1qrgnzs4jh2yfldarepysqgsukgdmwmqw5v0t7c "This is top secret information."

An example of the recipient decrypting the message:
> .\znn-cli.exe decryptMessage CTZYfOLO1j4ZeMhL4MEgnJ1FRbpcBfpPDwRWE/rvyA9gL0AAmAI91jcWY/IhkH/ExeTUW76Zs8fLr8/6bk3NNHN98b/Pl+YzSoaNc9BgDw==

Output:

> This is top secret information.

In this example the recipient has to get the encrypted message from the explorer by viewing the transaction that has the message and then copying the contents of the data property into the terminal:
![secret|690x440](upload://zMXHW9gCowk4MEm5gE2usj8IZy7.png)


It's worth noting that these encrypted messages can be sent off-chain as well but for this PoC I wanted to make it on-chain.

If someone wants to try it out, DM me your address and I can send you an encrypted message.

-------------------------

0x3639 | 2023-01-17 16:16:52 UTC | #2

I'm going to try this out.  How does the recipient know they received a message?  Does it show as received 0 ZNN?

-------------------------

vilkris | 2023-01-17 17:09:57 UTC | #3

Great, let me know if you need help. There's no "standard" for sending these messages so specifically informing the user of a new encrypted message isn't really possible now. The messages are sent with 0 value and with the empty token standard `zts1qqqqqqqqqqqqqqqqtq587y`.

-------------------------

sol | 2023-01-17 17:18:35 UTC | #4

[quote="vilkris, post:3, topic:1183"]
The messages are sent with 0 value and with the empty token standard `zts1qqqqqqqqqqqqqqqqtq587y`.
[/quote]

I wasn't aware that you could send an AccountBlock with `emptyTokenStandard`.
Thank you for sharing!

Vilkris, do you have a plan for these new functions? 
I suspect there is low usage of znn-cli within the community; did you want to make this more accessible to users?

It seems any address can generate/send these messages... I fear this functionality will be abused.

-------------------------

vilkris | 2023-01-17 17:48:09 UTC | #5

[quote="sol, post:4, topic:1183"]
Vilkris, do you have a plan for these new functions?
I suspect there is low usage of znn-cli within the community; did you want to make this more accessible to users?
[/quote]

Not really any immediate plans. Like I mentioned on Discord these could be used to allow delegators access to services for example but that needs work to turn it into a reality. I'm thinking that some type of messaging system in Syrius would be very nice but I'm not sure if this approach would be the best for that.

[quote="sol, post:4, topic:1183"]
It seems any address can generate/send these messages… I fear this functionality will be abused.
[/quote]
You mean like spam messages? Yeah that could cause some headache.

-------------------------

aliencoder | 2023-01-17 19:25:07 UTC | #6

I think we should really look into a Dart based implementation of the [Signal protocol](https://github.com/MixinNetwork/libsignal_protocol_dart). Afaik Mr. Kaine proposed an off-chain messaging layer based on it. Mixin desktop app [uses it](https://github.com/MixinNetwork/flutter-app) and I also found this social media app [using it](https://github.com/nixrajput/social-media-app-flutter/search?q=libsignal). I'll need to check what Mr. Kaine was proposing a while back. I see that there is a [Rust based implementation](https://github.com/signalapp/libsignal) that's actively maintained by Signal.

Also I don't think on-chain messages are a good idea right now.

-------------------------

aliencoder | 2023-01-17 21:45:50 UTC | #7

Further reading: 

https://www.signal.org/docs/specifications/xeddsa/

https://www.signal.org/docs/specifications/x3dh/

https://www.signal.org/docs/specifications/doubleratchet/

-------------------------

vilkris | 2023-01-17 21:55:42 UTC | #8

Thanks for the links. I'll do some reading on the protocol.

-------------------------

aliencoder | 2023-01-30 20:56:56 UTC | #9

I found a very nice explanation of the [Signal Protocol](https://www.redshiftzero.com/signal-protocol/) worth reading @vilkris 

I think leveraging a robust messaging protocol that has stood the test of time and uses state-of-the-art cryptography can extend the capabilities of NoM greatly in the future.

-------------------------

aliencoder | 2023-02-10 08:58:50 UTC | #10

I was researching state of the art peer to peer protocols and I found [Citadel Protocol](https://github.com/Avarok-Cybersecurity/Citadel-Protocol): "A post-quantum signal-like protocol that makes developing hyper-secure client-to-server and p2p applications easy".

[The guy](https://thomaspbraun.com/) developing it seems interested in [accessing funds](https://thomaspbraun.com/avarok/lusna_teaser.pdf) to cover R&D costs. Maybe we could tell him about AZ and funding an implementation of a blockchain peer-to-peer layer for Zenon.

-------------------------

vilkris | 2023-02-10 09:55:49 UTC | #11

Nice find. Definitely something worth looking into. @mehowbrainz Any thoughts on what would be the best way to approach such a person?

-------------------------

0x3639 | 2023-02-10 10:06:31 UTC | #12

this looks pretty interesting.  I was trying to figure out what LUSNA is exactly.  I don't see a website for it.  

![Screenshot 2023-02-10 at 3.58.34 AM|690x165](upload://ifHRvT4UZ3X3vedsK4ZoXMpdEc3.png)

Maybe LUSNA is the "platform" and [Citadel-Protocol](https://github.com/Avarok-Cybersecurity/Citadel-Protocol) is the protocol for the platform.  

I think we just email him.  I'm happy to do that from my work email so it does not look like some scam.  I could introduce the project and refer him to this link to start a discussion.  I might consider funding this in USD and take the AZ awards myself if he does not want crypto.  Looks like he wants cash.  But you never know. LMK if you guys want me to do this.  @mehowbrainz could do it too.

-------------------------

0x3639 | 2023-02-10 10:08:33 UTC | #13

Worst case is we get elliptical curve security if we follow this recommendation.

![Screenshot 2023-02-10 at 4.07.38 AM|690x200](upload://o2Uc2yKj2hGmuimUl6LLnNt32mD.png)

-------------------------

0x3639 | 2023-02-10 10:55:41 UTC | #14

Check out the [network architecture](https://avarok-cybersecurity.github.io/Citadel-Protocol/docs/#network-architecture).  Wonder if this can be run on our public nodes, rather than rely on one server.  

"Authentication to a central node is required before making peer-to-peer connections. There is both device-dependent auth as well as credentialed authentication backed by the argon2id hashing algorithm."

-------------------------

mehowbrainz | 2023-02-10 16:05:24 UTC | #15

[quote="vilkris, post:11, topic:1183, full:true"]
Nice find. Definitely something worth looking into. @mehowbrainz Any thoughts on what would be the best way to approach such a person?
[/quote]

I could send him an email. Would need some help from technical minds here to writeup a the technical aspects of the pitch. I can fill the rest.

-------------------------

mehowbrainz | 2023-02-10 23:27:31 UTC | #16

Topic moved to #development:funding-staging

-------------------------

aliencoder | 2023-06-16 07:49:45 UTC | #17

@vilkris look at this [Signal Dart library](https://github.com/MixinNetwork/libsignal_protocol_dart).

-------------------------

