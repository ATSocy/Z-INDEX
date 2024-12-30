Thread: steganography-nft-what-can-it-be-used-for
aminazgol | 2024-03-27 15:19:52 UTC | #1

This post is a follow-up to the [official Zenon medium post](https://medium.com/@zenon.network/the-new-nft-standard-when-cryptography-meets-steganography-9e356007dcaa) on Steganography NFTs. In this post, I would like to open a discussion on the possible applications that Steganography enables in an NFT ecosystem.

It is important to understand the difference between Steganography and Cryptography from a use-case standpoint. Then you can argue that some of the use-cases for Steganography are actually possible to do with Cryptography.

Steganography is basically a higher level of security compared to Cryptography. When two parties are using cryptography, a third party can be aware of communication happening but they cannot reveal the actual messages being communicated. But Stegonagraphy is used when parties what to conceal the fact that communication is taking place and no third party can have a clue that some messages had been exchanged.

![ZTS NFT (4)|690x388](upload://oMJAzFYsCFLlVFcCXchW1b5KfVo.jpeg)

Steganography is expected to be a more resource-intensive process compared to cryptographic methods as it’s working with multimedia objects. So it is not logical to do an application using Steganography if it’s possible to be done by cryptography.

**Examples:**

**Treasure hunt:** An artist claims that in his next collection, only one of the NFTs contains a secret steganography text which is a 12 word phrase of a wallet with 1 BTC in it.

The fact that everyone **knows** that one NFT contains a message, makes it convenient to do this use-case by cryptography rather than Steganography.

For this case, we know that NFTs have metadata and the artist can add a `reward` attribute to the metadata of the NFT in a form of a cryptographic text and that `reward` is only unlockable by the owner’s private key. This attribute is `empty` for all the NFTs in the collection except for the one that is a treasure.

Some other examples of lottery, access to secret communities, discount codes, in-game items, and easter eggs, can similarly be done with cryptographic metadata.

The following is another example that also can be done with cryptography but I thought it’s cooler to do it with Steganography:

**Multi Image NFT:** An artist can list an NFT and claims it contains 5 arts in one file. If you buy it, you can unlock the file but you’ll only see 1 art out of 5. Depending on how many times this NFT had been passed on from one owner to another, the art content changes.

![Screenshot from 2022-08-18 12-36-17|690x188](upload://rkjdhyKcXQ0gg8cg2NTUATq5s7w.png)

So in this forum, I wanted to ask the community to brainstorm on this matter and suggest use-cases for Steganography. I understand that sometimes we make doing things possible and we will be surprised by how creatively people will use it. But I think it’s worth raising the question at this stage.

What can we do with Steganography?

-------------------------

0x3639 | 2022-08-18 09:01:20 UTC | #2

Maybe some in game assets (NFTs), like a sword or gun, that have "programable" power.  Maybe the power can be morphed or augmented by the player based on certain traits of the player.  Basically smart objects in games.

-------------------------

Zashounet | 2022-08-18 09:08:14 UTC | #3

A lot of cool and fun things can be done with all the mysteries Zenon has.
I have a few ideas cooking in my head, can’t wait to start working on this!

-------------------------

aminazgol | 2022-08-18 13:14:48 UTC | #4

I get the idea, having a game object embedded within the NFT image. But this example also doesn't have to be implemented with Steganography (the in-game object doesn't have to be encoded into the image pixels) and could be implemented as a separate file linked to the NFT, therefore we avoid the intensive process of merging in the in-game object and the NFT image.

-------------------------

coinselor | 2022-08-18 13:39:58 UTC | #5

From the original article, the use case that stands out the most to me is this:

## Use-case: Embedded Unlockable Content

I have been a victim, and I have to admit I have also benefitted, from pirated media content. The reason anything can be pirated (and it's the same reason bitcoin should have not existed) is that anything digital, just represents binary data that can be copied. Bitcoin was able to solve the issue for money. 

Can the Zenon NFT standard solve the issue for everything else? This is what I'm extremely interested in. The article claims counterfeits become obsolete. But how exactly?

Let's say I mint a numbered series of 100 NFTs that contain a 20min video course on how to sharpen a knife. I publish the first edition on Youtube for everyone to see publicly. Each holder of the NFT can also do some cryptgraphy + steganography wizardry in s y r i u s to unlock the content of another 20 minutes of secret pro tricks on knife sharpening.

Why can't the person just 'save as' the content as he is watching it?

-------------------------

aminazgol | 2022-08-18 15:15:02 UTC | #6

Well, to answer your last question I must say nothing stops them to 'save as' your content.
I explain my take on the article's claim. quote from the article:

> Moreover, adopting the Virtual Hologram will eradicate counterfeiting, the “Save as” method would be useless, as only the NFT holder will be able to authenticate the NFT using its embedded Virtual Hologram.

What this means is that there is something hidden inside the NFT that is only unlockable by the owner, so if other people 'save as' the NFT file they still cannot access the hidden content inside it. So that is why 'save as' is useless. But nothing is stoping the owner to copy the unlocked content.
So in your case, if someone buys the NFT and unlocks the video inside it, there's nothing that can stop him/her from 'save as' or screen record your content and copy it somewhere else.

Now you mentioned it I did too think that this method can stop people from copying others' NFTs as we can embed some information inside the pixels of the image/video that the network recognizes and deny any duplication of that image/video. But it's obvious that editing the image is also as simple as copying it, so the virtual hologram can easily vanish if the person copying the file just changes the pixel saturation by 0.01 percent. So this is not possible to do with steganography!

-------------------------

coinselor | 2022-08-18 16:26:49 UTC | #7

Perhaps there is a clever workaround to the issue if we think about it from the consumer side; instead of a fix to counterfeiting content we could mitigate it.

Would it be possible to stack two steganography layers on the same file? Meaning, the first layer unlocks the embedded content to the user, and the second layer hides the information like public address of owner, issue number, etc...

Once the unlockable content gets copied and redistributed, we could apply the same steganography techniques to figure out some information about the entity who did the copyright infringement.

Makes me wonder if there are current DRM techniques that employ cryptography/steganography in a similar way, and whether it's effective or not.

It also makes me wonder what limiting factors applications would have with a 'smart contract' embedded in a virtual hologram if the owner is the only person capable of interacting with it.

-------------------------

aminazgol | 2022-08-19 06:45:47 UTC | #8

It is possible to embed two layers of steganography on the same file. But regardless, current steganography algorithms are done in a very precise bit mapping approach. It means that if an image file has some steganography information inside, by changing only one bit (for example make one pixel of the image black) the whole steganography information inside the file will become unreadable.

-------------------------

sol | 2022-11-12 23:04:10 UTC | #10

I would like to revive this conversation by addressing some points from [the article](https://medium.com/@zenon.network/the-new-nft-standard-when-cryptography-meets-steganography-9e356007dcaa) and providing my perspective for achieving this milestone.

I think that it's possible to implement the NFT standard as it's described in the Medium article; however, I also think that the focus has largely been on the way steganography is applied to specific file types today. Feel free to correct me if I'm wrong about anything.

I'll be adding my own commentary to the points made in the article. Skip to the end for my suggestions on how we can proceed with an implementation.

The goal:

> Cryptography will be used for encryption and authentication purposes, while steganography will be used to insert it into the NFT.

------

> Cryptography is the practice and study of techniques that enable authentication, confidentiality, data integrity, and non-repudiation.

Authentication: the act of proving an assertion; the process of verifying an identity.
Confidentiality: a set of rules that limit access to certain types of information.
Data integrity: the assurance of data accuracy and consistency over its entire life-cycle.
Non-repudiation: a service that provides proof of the integrity and origin of data.

Modern cryptography provides us with the tools to implement a solution that meets all these criteria.
* Authentication: a token is attributed to a single address, which can only be controlled by the entity holding its private key.
* Confidentiality: the NFT standard must include a protocol that grants certain applications the ability to decrypt a token's embedded payload with the the token owner's private key.
* Data integrity: the NFT standard must include a protocol that proves a given token is in fact the correct token (i.e. has not been swapped out for a different token or value.) Additionally, we will leverage the Zenon ledger to reinforce data integrity.
* Non-repudiation: the NFT standard must include a protocol that proves all of the above has not been modified in any way without the token owner's consent (i.e. a proof for all other proofs.)

----

> Steganography on the other hand is the practice and study of techniques that enable one to conceal a message within another message and communicate **without the knowledge of any third parties.**

This is where things get a bit complicated. 
Modern steganography solutions are limited in this respect. Even a determined security analyst can identify the presence of a concealed message.
*We cannot realistically achieve this goal with open-source software.* 
If the algorithm for concealing a message is auditable by anyone, it can certainly be reverse-engineered to permit the discovery of an embedded message. 

Summarized examples of steganography from the article:
1. tattooing a message on a clean-shaven scalp then waiting for the hair to grow back
2. painting four microscopic characters on a famous painting
3. a famous painting superimposed over a portrait that can only be revealed with XRF spectroscopy
4. lines and dots amidst an array of symbols were actually a message written in morse code

All of these eventually failed the criteria of communicating a message without third-party discovery. 
*It's a matter of when, not if.*

------

Examples of Digital Steganography

> * Least Significant Bit
For every type of image file format, one can change the lowest bits to hold message data.

> * Bit Plane Complexity Segmentation
BPCS uses multiple bit-planes, and so can embed a much higher amount of data (than LSB), though this is conditional on the individual image.

The next paragraph states:

> Most NFTs are in the form of digital media content such as images, music, or videos. 
With the help of digital steganography, the on-chain information can be cryptographically linked and embedded into the actual NFT using the techniques presented earlier.

As far as I know, the examples provided can only be applied to image, audio, and video files.
In order to embed a message in existing media, the application performing this task must be able to transcode each supported media type, preferably producing a result with the original encoding scheme. 
For example: .avi input -> embed cryptography proof -> .avi output
This requires a unique solution per media type.

Also, these approaches do not apply to other common file types, such as text documents. A steganography solution for PDF files will not apply to DOCX files, or presentation files, or plaintext files.
Each of these will require their own solutions outside the examples provided by the article.

Note: I think it's impossible to hide content in a plaintext file.

----

Use-case: Embedded Unlockable Content
>The Virtual Hologram concept can be extended to support a novel use case: embedded unlockable content, while obsoleting counterfeits at the same time.

>When you create an NFT, you should have the option to add additional content that can only be revealed by the NFT holder.

>The “Save as” method would be useless, as only the NFT holder will be able to authenticate the NFT using its embedded Virtual Hologram.

The goal is to be able to unlock hidden, encrypted content that only the NFT holder can access. 
The data carrier will be publicly accessible, publicly verifiable, and privately unlockable.

If digital media is publicly accessible, one cannot prevent others from "Saving As", though the true value of the NFT will still remain obfuscated.
Should someone find a way to remove the embedded data, they will nevertheless only have the publicly accessible media, which may not be worth anything without the hidden counter-piece.


---

The recommended implementations:
>Virtual Hologram implementation: minting should automatically insert the Virtual Hologram using a steganographic method

>Spectral Attestation implementation: extract the Virtual Hologram and validate it using on-chain data

These will be slightly challenging to implement but absolutely possible given the current capabilities of the Syrius wallet and the Dart/Flutter SDKs.
Part of the challenge involves a design decision for integrating the steganographic method. I hope we can all reach an agreement for a preferred method soon in order to begin this work.

----

Some other considerations:
1. The off-chain host for the data carrier must be trusted to provide a high degree of data integrity and availability.
2. Alternatively, if the NFT payload is just encrypted text, it could be hosted on-chain.
3. Is the unlockable content static or dynamic? If someone purchases an NFT and consumes its content, will it still have value? 
4. Will the content be time-sensitive, like Time-based One-time Passwords (TOTP)?
5. Is the unlockable content a key to a particular event or digital forum? Why not make the ownership of the token the key, instead?

----

Suggestions for implementations

All that to say, we need to decide how we want to implement *steganography*. There are probably many ways to achieve this; some will be research-intensive and may result in a cumbersome wallet engine while others might be more lightweight and scalable.

Here's what I'm proposing:
1. We implement the solutions are they're literally presented in the article. This will require individual transcoding capabilities for each file format that we want to support. This solution does not scale quickly and could lead to a slow NFT creation process for larger files.
   * For what purpose, if the discovery of the embedded payload is inevitable? Permanent obfuscation is impossible given this project is open-source.
   * Are we trying to create a functional replica of a file with an embedded payload that is non-trivial to remove? 
*Are we aiming for something like DRM?*
   * The algorithm will inevitably be reverse-engineered to remove that payload, if there is value in doing so.
2. We implement an alternate solution that achieves a similar result -- file functionality and an embedded, encrypted payload -- with any file format *today*. This can be achieved by appending arbitrary bytes to any file such that we don't break any existing magic byte structures that are currently in use.
   * The goal is to leverage cryptography to unlock a hidden embedded payload.
   *  It should not be overly complicated to verify that there is an embedded payload. This reduces the bar for anyone to confirm that a Zenon NFT *is in fact a Zenon NFT*, not some random file.
   * "Hidden embedded payload" means that upon launching the file normally, a user would not suspect there is anything hidden in the file. Upon deeper, byte-level analysis, one may surmise -- or even conclude -- that there is indeed something more to this file.

---

Keep in mind, we need a protocol that Syrius can apply to each file that we want to tokenize, whether that's appending bytes or re-encoding a file entirely. The file *must* pass through Syrius before being uploaded to a file-hosting service.

Shameless plug -- [here's what I'm proposing as a proof of concept](https://github.com/Sol-Sanctum/Zenon-PoCs/tree/main/stego_example) for option number 2 and it scales to any file type (as far a I know) with little processing overhead. 

Second plug -- [here's the task in our Mattermost board.](https://mm.0x3639.com/boards/workspace/bjqwiwqxqtnb8xf1mab1fnu8ua/bdw6atoqxgirqjcuuz5ckxu3naa/vqsgy3jdce7f3bcqapjnstz86xh/cuqx4yaekcjyajyr3gm7zp41o9h) I'll be updating its contents with suggestions from this thread. Feel free to contribute directly to the board!

-------------------------

romeo | 2022-11-12 01:25:03 UTC | #11

[quote="sol, post:10, topic:952"]
Shameless plug – [here’s what I’m proposing as a proof of concept ](https://github.com/Sol-Sanctum/Zenon-PoCs/tree/main/stego_example) for option number 2 and it scales to any file type (as far a I know) with little processing overhead.
[/quote]

In your example - the embedded payload would be easily readable via a simple meta data reader correct? Or would it also be encrypted?

-------------------------

sol | 2022-11-12 01:27:28 UTC | #12

For demonstration purposes, I opted to keep the data in cleartext.
The solution we implement would likely be obfuscated/encrypted, using other bytecode that isn't human-readable.

-------------------------

romeo | 2022-11-12 01:30:28 UTC | #13

[quote="sol, post:12, topic:952"]
The solution we implement would likely be obfuscated/encrypted, using other bytecode that isn’t human-readable.
[/quote]

Ok I see, thanks. Is there any reason why we couldn't pursue both options in time? The method outlined in the article has it's merits I believe and would be worth working on - perhaps starting with a single file type (most common NFT image type I guess)

-------------------------

sol | 2022-11-12 01:50:42 UTC | #14

The constraint is dev time. 

Given ample time and more devs working on this, I'd go for option 1, even though I think it's a bit gimmicky. Sorry if that offends anyone. It's one of those features that would certainly grab people's attention if implemented correctly, though I'm not sure if it's worth the effort required to pull off. 

Like I mentioned, it would require specific solutions for each file type we want to support.
Does anyone disagree with this statement?

I'm afraid the launch would be lackluster and it might lose its flair if we marketed "Launching novel NFT Standard with hidden/unlockable content" and the caveat was "but we only support JPGs for the foreseeable future."

In my mind, both options achieve the same goals; one is obviously a simpler implementation but I think it scales better than the original vision.

-------------------------

0x3639 | 2022-11-12 01:59:08 UTC | #15

[quote="sol, post:10, topic:952"]
The algorithm will inevitably be reverse-engineered to remove that payload, if there is value in doing so.
[/quote]

Just want to make sure I understand.  Even if the payload is removed from the image, it should be protected with a password.  Assuming the contents are secure, there should be no reason to remove the payload.  Is that right?

-------------------------

sol | 2022-11-12 02:13:15 UTC | #16

> Assuming the contents are secure, there should be no reason to remove the payload.

Right, I personally don't see reason why someone would want to strip a data carrier of its embedded content. I'm postulating that it could happen.
The data carrier is publicly accessible anyways; anyone can copy those bits -- directly or indirectly -- and use them as they please ("Save As").
This applies for all tokenized media except for encrypted content (i.e. the public-facing bits are already encrypted.)

-------------------------

sol | 2023-01-08 23:01:27 UTC | #17

I've been thinking about the technical details of the proposed NFT standard and I have some questions about the implementation, mostly with respect to limitations and design decisions. I apologize if my ramblings are incoherent.

Perhaps I'm boiling the ocean with my approach; ultimately, I'm trying to achieve [a use case](https://www.hongkiat.com/blog/nft-use-cases/) for steganography that is more than just single-use consumables.


*Maybe* I should just focus on the simplest implementation of steganography (LSB) and call it a day.

Some things to consider:
1. What if we want to temporarily or permanently reveal some of that embedded information to the world, or to certain people?
   - Context: medical records stored in the NFT. I want my doctor to have limited access to this information.
   - Alt context: [OP's post](https://forum2.zenon.org/t/steganography-nft-what-can-it-be-used-for/952?u=sol_sanctum) and the Multi-Image NFT.
   - Considerations: 
     - multisig for NFT platforms
     - Certificate Authorities to revoke permissions after a time period has expired
2. Do we want to embed an encrypted payload in every token that's minted, even if the payload is empty?
   - Context: anti-steganalysis mechanism where even if a data carrier is correctly identified to be a Zenon NFT, an adversary wouldn't know if the embedded data is useful or not.
   - Counterpoint: If an adversary suspects there is embedded data in a carrier, steganography has failed its purpose.
   - Perhaps we will have two types of NFTs: immutable and mutable (as [suggested by George](https://t.me/zenonnetwork/268211))
   - Note: I am hard-pressed to identify a reason to combine steganography with an immutable NFT beyond one-time consumables.
3. If we do implement steganography in every token issued on NoM, then token transferability is limited to applications that can transcode the asset. Mobile and browser wallets will likely not be able to perform this task, or they may be limited to certain file types due to processing limitations.
4. The amount of data that can be embedded is largely bounded by the size of the container and the encoding method. I found an [example of lossless steganography](http://www.ijfcc.org/papers/243-N3029.pdf) but it has some downsides that I think are unsuitable for our project (listed in section IV.)
   - Steganography tends to be lossy; the original bits are being manipulated and this can introduce visual artifacts that are perceivable to the human eye. 
   - As more of the original data is replaced, embedded capacity increases, but so does "noise" in the carrier data.
   - My pseudo-steganography PoC enables virtually limitless container sizes, introduces no noise in the carrier data, but the presence of embedded data is trivial to detect.


Here's some literature that I found interesting, particularly from page 16 onwards: [Magic LSB Substitution Method (M-LSB-SM)](https://arxiv.org/ftp/arxiv/papers/1506/1506.02100.pdf)

-------------------------

coinselor | 2023-01-09 02:10:43 UTC | #18

ZK and homomorphic encryption might be relevant for the privacy preserving medical records use case. Here's a neat implementation on eth to make data types private:
https://www.youtube.com/watch?v=jgYWv__Wehk

-------------------------

TrevorLeahy3 | 2023-01-09 15:19:23 UTC | #19

Seems to me that multi sig built in could have a big impact on use cases for tokenizing real world assets or just shared digital ones. 

I dont know about the multi image idea though, other than digital collectables or consumables not sure about practical usecases, more so just creative. What can you do with a multi image nft that you cant do with multiple seperate images and a smart contract? 

What i keep coming back to is the special attestation idea and how useful/important it would be to be able to easily assert your ownership of an NFT on chain but also understood this was mainly done thru the metadata. 

If this function needs steganography then every token minted should have the capacity to hold an encrypted payload but it also makes the practise public so doesnt really make as much sense. 

If the assertion can be made outside of any steganography tools then more effort could be made into hiding the embedded data, which the Magic LSB Method sounded pretty good at.

-------------------------

sol | 2023-01-15 03:20:06 UTC | #20

I revisited the NFT Standard article and determined that my initial idea of pseudo-steganography is likely the only viable way to achieve Mr Kaine's vision. I don't see any other way, based on research I've done about modern steganography capabilities. 

I'll explain why in this post.

> TL;DR
I propose that we concatenate an encrypted, variable size data container to carrier data. We may potentially use LSB to embed the Virtual Hologram in the carrier data.

---

Excerpt from the Medium Article:
> When you create an NFT, you should have the option to add additional content that can only be revealed by the NFT holder. Such content ***can be anything***. 
**High definition content**, messages, **video content**, access to secret communities, discount codes, or even smart contracts, treasures, and easter eggs are all potential candidates for unlockable content.

---

Mr Kaine knows people will be minting JPEGs, but stipulates that the solution should permit *any content* to be embedded in the carrier data.

I only know of one way this can be achieved.
Since the embedded data can be of variable size and can potentially be greater than the size of the original carrier data, we must find a steganographic technique that:
- is extremely flexible,
    - in terms of file size, file type
- is cryptographically malleable
     - in terms of asset transferability
- is not constrained by the size of the input data
- can be parsed by anyone to certify authenticity (Spectral Attestation)
- ideally, is accessible to mobile wallets and devices with less compute capabilities

---

**A core limitation of modern steganographic techniques is the size of the carrier.** 

Generally, steganography introduces changes in the original file's data in order to hide other data; replacing *original data* with anything else tends to lead to data loss. 
You can't replace bits and expect all the information to remain intact.

Of course, slight changes to the file may be imperceivable to humans, but there's a relation between how much data that can be stuffed in carrier bits and visual/auditory/spatial degradation of carrier data quality.

> Low impact to original bits
    - more likely to maintain original file quality
    - less capacity for the embedded file

> Higher impact to original bits
    - less likely to maintain original file quality
    - more capacity for the embedded file

This is why steganography is generally *lossy*. Same applies to compression.


[details="About lossless steganography..."]
There are few lossless solutions and they do not fit our needs. They rely on the chance that the carrier data contains the same subset of bits as the embedded data.
I'm not confident this will work for every file and users cannot be limited by their selection of files.
If you find any lossless solutions that could work in our context, please let me know.
[/details]

---

Mr Kaine outlines two options in his article: LSB and BPCS. 

LSB is primitive, popular, easy to implement for many file types, but it has the embedded data size constraint.

BPCS is a newer technique that depends on spatial noise in the carrier data to hide information, and it seems to be only applicable to image files. 
It works well with image data of a realistic setting with lots of different shades, colors, edges, objects, etc, but fares poorly with flat, cartoon-like graphics. 
It takes advantage of visual chaos; cartoons tend to have large areas of the same pixel color.

For example, BPCS would offer much higher capacity for [the image on the left.](https://alexharkness.com/wp-content/uploads/2017/11/Reduce-Noise-800x445.jpg)

---

The final reason why those two methods won't work -- We need to encrypt the embedded contents, because our software is open source and the ledger is public.

A malicious actor will scrape all the carrier data by querying the ledger and extract the embedded payloads of each NFT.

I've tested [AES-256-CBC and AES-256-GCM](https://medium.com/@zenon.network/alphanet-swap-cycles-658981a9d8bd) in Dart; we should expect ~4x file size output or greater. I could try other encryption schemes, as well.

Some results from a few tests:

[details="Show results"]
> Input files
> - input.png = 180 KB
> - secret.png = 120 KB
> - secret.mp4 = 17230 KB

> Unencrypted Output
> - input.png + secret.png => output.png = 299 KB
> - input.png + secret.mp4 => output.png = 17410 KB

> AES-256-CBC Output
> - input.png + encrypted(secret.png) => output.png = 907 KB
> - input.png + encrypted(secret.mp4) => output.png = 105174 KB

> AES-256-GCM Output
> - input.png + encrypted(secret.png) => output.png = 908 KB
> - input.png + encrypted(secret.mp4) => output.png = 78925 KB
[/details]


Here's some binwalk output, they're all the same:

[details="Show binwalk output"]
```
$ binwalk output.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 900 x 900, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, compressed
```
[/details]


Visual representation of my proposal:
![image|484x202, 50%](upload://xdrjeSTSTSS4vTq9AfvI1YvArib.png)



Note: The Virtual Hologram (VH) is likely to be a small value, like the container's header (H) and trailer (T).

Alternatively, since the Virtual Hologram may be short and a fixed length (tbd), we could potentially leverage LSB to embed that in the carrier data for all file types.

---

I've updated my pseudo-steganography PoC but haven't published it yet. 
There are still some cryptography-related logistics I need to work out.

I welcome any feedback regarding my posts on this topic. I'm seeking criticism of the approach, in case there are flaws I haven't considered.

If I don't hear from anyone, I might just "[do it myself](https://github.com/Big-Inches-Club-House/bich/discussions/1)."

-------------------------

romeo | 2023-01-13 10:28:24 UTC | #21

I have thoughts on this, but need time to sit down and respond. Agree with most of your points

-------------------------

0x3639 | 2023-01-13 11:42:04 UTC | #22

Are there any examples of this solution used in production?  I'll google around, but this was the first thing that came to mind.  Seems like a viable option w/out doing any research myself.

-------------------------

0x3639 | 2023-01-13 11:50:09 UTC | #23

Interesting links I found.  I think I understand this.  It's like TrueCrypt.  It's a simple encrypted payload of variable size that is added to anything and does not impact the original thing.  It's like an encrypted wart that you cannot see and can hide stuff in.  Is that about correct?  

https://serverfault.com/questions/335095/variable-size-encrypted-container

Why does it 4x the original size?  Isn't the bloat a function of what you are adding to the encryption package?  For example:  If I add the string "deeZNNutz" to a 100kb image will it 4x the image size?

-------------------------

aliencoder | 2023-01-13 12:18:56 UTC | #24

Same for me. Very interesting ideas.

-------------------------

sol | 2023-01-13 13:59:36 UTC | #25

Yes, it's like a TrueCrypt container. :slight_smile: 

[quote="0x3639, post:23, topic:952"]
For example: If I add the string “deeZNNutz” to a 100kb image will it 4x the image size?
[/quote]

A quick test on my end shows that using a small text file as the secret input will not greatly impact the output file size.
>Example:
input.png = 180 KB
secret.txt = 1 KB
unencrypted and encrypted output were both 180 KB

-------------------------

0x3639 | 2023-01-13 14:16:16 UTC | #26

this is a pretty good idea.  Can the contents of the container be changed?  Not sure why we would need to do that.  But I assume a public key would be added the the container.  And that, along with the private key, will confirm ownership of the digital asset. If the contents of container are tampered with the private key will not authenticate ownership.   

And if someone loses the image it's like losing a private key?  What is to prevent someone from removing the container and attaching it to another image?  I assume the key generation is a function of the hash of the object the container is attached to?

This is cool.

-------------------------

sol | 2023-01-13 14:33:51 UTC | #27

[quote="0x3639, post:22, topic:952"]
Are there any examples of this solution used in production?
[/quote]

I'm not aware of a commercial software that offers this steganographic solution, but maybe someone has already tried this?

[quote="0x3639, post:26, topic:952"]
Can the contents of the container be changed?
[/quote]

Yes, it's dynamic and can be updated by the token holder.
As for why we want this -- let's aim for multi-use NFTs as opposed to single-use.
I'm still thinking of how this will impact the NFT record on-chain.

[quote="0x3639, post:26, topic:952"]
if someone loses the image it’s like losing a private key?
[/quote]

Yes, but hopefully the carrier is uploaded to a reputable storage service.

[quote="0x3639, post:26, topic:952"]
What is to prevent someone from removing the container and attaching it to another image?
[/quote]

Nothing. Some actors may try to extract and bruteforce these containers. This is the tradeoff for having open source code, a public ledger, and a project criteria to embed any amount of data.

[quote="0x3639, post:26, topic:952"]
the key generation is a function of the hash of the object the container is attached to?
[/quote]

I'm still working on this part, but ideas for key management are welcome.

-------------------------

0x3639 | 2023-01-13 14:44:39 UTC | #28

Awesome.  I can dig around for key generation articles too.

But to be clear, the goal is to make sure an encrypted container is attached to a specific "thing A".  And if we remove the encrypted container and attach it to "thing B" it will not be authentic.  

Correct?

-------------------------

sol | 2023-01-13 14:59:51 UTC | #29

[quote="0x3639, post:28, topic:952"]
And if we remove the encrypted container and attach it to “thing B” it will not be authentic.
[/quote]

Spectral Attestation could check a hash that is part of the NFT's record on-chain.
`hash(output with embedded secret)`

If someone manages to append the secret container to another file, good for them. They still need the private keys and the ledger won't validate the imposter file is authentic.

-------------------------

0x3639 | 2023-01-13 15:04:13 UTC | #30

I like this idea a lot. Encrypted Warts. 

EW standard.

-------------------------

0x3639 | 2023-01-22 16:35:00 UTC | #31

Here are some research links to read.

- https://www.coindesk.com/sponsored-content/encrypted-variable-tokens-the-next-generation-of-innovative-media-assets/
- https://www.newtonproject.org/en/evt/
- https://news.bitcoin.com/the-future-of-nft-is-evt-the-new-game-changer-token/
- "NFTs are static, while EVTs are dynamic. EVTs allow certain aspects of the metadata to be re-programmed. Ultimately, EVT functionalities solve the residual royalty problem for creators. With EVTs, a creator can continuously enjoy a percentage of royalties as the content/metadata continues to be traded. NFTs weren’t designed this way because of security issues surrounding the coded language."
- (Not so relevant) https://www.researchgate.net/publication/356339205_Understanding_Security_Issues_in_the_NFT_Ecosystem
- https://merehead.com/blog/make-nfts-secure/ (Not applicable)
- https://apptainer.org/ (Encrypted docker containers.  Just FYI)
- Wonder if we should submit a ZIP (https://eips.ethereum.org/EIPS/eip-721?utm_source=thenewstack&utm_medium=website&utm_content=inline-mention&utm_campaign=platform)

Not much out there on embedded encrypted data in NFTs.

-------------------------

0x3639 | 2023-01-23 15:33:03 UTC | #32

Interesting discussion about Sign in with Ethereum where they discuss data vaults to store information.  

https://www.youtube.com/watch?v=VHwzE6mVm_s

These guys are working on the identity standard
https://blog.spruceid.com/sign-in-with-ethereum-is-a-game-changer-part-1/

https://github.com/spruceid

Wonder if there is anything we can learn about their data vault.

-------------------------

vilkris | 2023-01-31 10:24:57 UTC | #33

I checked your PoC and tried to familiarize myself a little with these concepts.
I understood you're proposing to just add an encrypted payload to the file and the solution does not necessarily need to use LSB or BPCS. Would the benefit of using LSB or BPCS be that it would be harder for an outsider to determine the file has something hidden in it? 

[quote="sol, post:20, topic:952"]
The final reason why those two methods won’t work – We need to encrypt the embedded contents, because our software is open source and the ledger is public.
[/quote]
Why would encrypting the embedded contents make those methods not work?

-------------------------

0x3639 | 2023-02-19 15:17:07 UTC | #34

As we think about NFT and a future marketplace, I found this video pretty interesting.  Posting it here to remember to watch when a marketplace is in the works.  

https://www.youtube.com/watch?v=KBKRrKtGTY8

-------------------------

0x3639 | 2023-04-06 12:00:03 UTC | #35

Interesting research paper shared by @angelo_a_jr 

## Abstract

Adversarial training has proved to be competitive against supervised learning
methods on computer vision tasks. However, studies have mainly been confined
to generative tasks such as image synthesis. In this paper, we apply adversarial
training techniques to the discriminative task of learning a steganographic algorithm. Steganography is a collection of techniques for concealing the existence
of information by embedding it within a non-secret medium, such as cover texts
or images. We show that adversarial training can produce robust steganographic
techniques: our unsupervised training scheme produces a steganographic algorithm
that competes with state-of-the-art steganographic techniques. We also show that
supervised training of our adversarial model produces a robust steganalyzer, which
performs the discriminative task of deciding if an image contains secret information.
We define a game between three parties, Alice, Bob and Eve, in order to simultaneously train both a steganographic algorithm and a steganalyzer. Alice and Bob
attempt to communicate a secret message contained within an image, while Eve
eavesdrops on their conversation and attempts to determine if secret information is
embedded within the image. We represent Alice, Bob and Eve by neural networks,
and validate our scheme on two independent image datasets, showing our novel
method of studying steganographic problems is surprisingly competitive against
established steganographic techniques.

https://proceedings.neurips.cc/paper_files/paper/2017/file/fe2d010308a6b3799a3d9c728ee74244-Paper.pdf

-------------------------

dat_she_pepe | 2023-04-11 15:01:19 UTC | #36

Food for thoughts from another project I discussed with:

"Maybe I'm mixing up things here so open to talk. First I'm not advocating anything tbh. I'm just skeptical when it comes to the crypto ethos (cryptographically verified anything etc.) when projected on others population as most of them don't really care. I think that ultimately we'll come to that but it might takes decades and we're here and now. 

For exemple the vast majority of artists, good or bad, are not wealthy. There are some rich ones of course but that's a very little number. The first ones rely on social proofs to sell as they usually work with 1, 2 or 3 galleries and sometimes with institutional structures so when a sale happens the actors, seller, buyer and artist already know each other. They're part of the same local or national network. The second sale will fall in the same situation. What happen next isn't really the artist's problem in that case, that's what I said talking to institutions might be more interesting. The laters now are in a different situation, they sell and show their work in many social networks they have no control on, however once the first and maybe second sale happened, they don't care (usually). But let's address the elephant in the room because before even starting to talk about what could replace paper certificates (what we use now), we should talk about how NFTs or Ordinal or even Blockchain could replace that or even be used in the scope of real life art production. But maybe this wasn't the point ?

I don't see all darkness in Ordinals and NFTs. From my personal perspective, those are awesome technology that allows digital art to be unique for the first time. However it's highly limited right now. For exemple, I just applied to a video contest call and I had to deal with 7GB files due to the high quality requirements for the diffusion. So copy pasting real life work onto a chain wouldn't really work in many cases, even when it comes to digital art. However and that's what I'm (personally) interested in is how to question the protocol itself and, for example, what it could do to the art economy. I've been working with The Economic Space Agency for a few years but unfortunately nothing but research papers ever came out of that. I would love to see a twist coming from the art scene and not just panini cards."

-------------------------

TrevorLeahy3 | 2023-04-15 15:12:09 UTC | #37

Trying to let some of this soak in but from what i understand it sounds like its got the potential to be the alien tech weve been looking for.

-------------------------

zyler9985 | 2023-06-15 18:00:18 UTC | #38

Bump. High quality thread. Hows this looking w ordinals and brc20 now?

-------------------------

sol | 2023-06-15 18:20:28 UTC | #39

I've re-evaluated the path to achieve the "NFT Standard".

I believe Mr Kaine's suggestion in this post is how we should approach the solution.
https://t.me/zenonnetwork/283835

The ZAS will allow us to support any asset types that gain popularity, but not necessarily *every* type of asset. I think we will need to integrate each one separately and we'll likely prioritize the popular ones.

Examples
- Native NFTs with pointers to off-chain data (similar to ERC-721)
- Native NFTs with data on-chain (similar to inscriptions and stamps)
- Bridged assets, such as Bitcoin inscriptions, ERC-721s, etc.
- Zenon's "NFT Standard" with cryptography/steganography


The initial vision is ambitious and we need some other infrastructure to get us there.

-------------------------

sultanofstaking | 2023-06-15 20:20:18 UTC | #40

Wen unused legacy pillar slot NFTs

-------------------------

sol | 2023-06-15 21:35:20 UTC | #41

[quote="vilkris, post:33, topic:952"]
Would the benefit of using LSB or BPCS be that it would be harder for an outsider to determine the file has something hidden in it?
[/quote]

A determined adversary using statistical analysis and modern digital forensics techniques will be able to detect the hidden data encoded with either of those methods, especially LSB. The chance of detection is even higher if the reference (original) data is publicly available.

[quote="vilkris, post:33, topic:952"]
Why would encrypting the embedded contents make those methods not work?
[/quote]

I made a mistake when I wrote that. The encryption scheme is necessary regardless; the way we encode/embed the data is a separate decision. Theoretically, we could encode encrypted bits into images using LSB, but we won't have much capacity.
I don't think LSB, PBCS, or any other common steganography algorithm is viable for our use case. 
It doesn't even make sense to call it steganography, but I digress.

[quote="sultanofstaking, post:40, topic:952, full:true"]
Wen unused legacy pillar slot NFTs
[/quote]

This is actually a great question and deserves a complete answer.

-------------------------

Stark | 2023-08-03 19:52:02 UTC | #42

I feel like this general idea from stamps, combined with the feeless NoM, could solve the container size problem:

https://twitter.com/trustmachinesco/status/1643353972885913602?s=20
(Mostly posting the tweet for the graphic visual.)

I also have these thoughts about Bitcoin ordinals - do miners hold the complete files on their node? If a node hosts illegal data, how does that play out, with law enforcement?

If all the data on NoM is fragmented, nodes don't have that concern. And it would provide for the data slurry to hide stego data.

IPFS kind of works this way, right?

Seems like anti-ordinal BTC maxis would want to support this.

-------------------------

dat_she_pepe | 2023-08-03 20:19:51 UTC | #43

Stamp is retarded. Nobody cares about it not should care.

-------------------------

sol | 2023-08-03 20:52:05 UTC | #44

You don't like Stamps because of cost or for a different reason? They're unprunable but have some tradeoffs.

Don't tell me you care about UTXO bloat.

-------------------------

dat_she_pepe | 2023-08-05 04:15:24 UTC | #45

No, I just think it's not getting any following, no narrative, nothing. It appeared for some to be able to get low inscriptions numbers after they missed the Ordinal run. I don't see anything good about it VS what Ordinals brings. It looks like a stretch marketing prunning proof non sense in order to take off, and it didn't work.

-------------------------

Stark | 2024-01-02 22:01:32 UTC | #46

https://phys.org/news/2018-12-multichannel-vectorial-holographic-encryption.html

-------------------------

Stark | 2024-01-10 17:53:47 UTC | #47

Might stimulate some ideas:

https://en.wikipedia.org/wiki/Focal_point_(game_theory)

-------------------------

