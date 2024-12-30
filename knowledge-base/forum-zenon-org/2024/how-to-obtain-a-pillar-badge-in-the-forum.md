Thread: how-to-obtain-a-pillar-badge-in-the-forum
0x3639 | 2023-01-30 16:43:01 UTC | #1

Attention Pillar Operators

The community is making a big push to better communicate with Pillar operators.  Until decentralized & trustless tools are available, we have a manual method to verify a signed message from a Pillar and then cross reference the address with the list of Pillars.  It’s not automated or trustless, but it’s better than nothing.  We are asking Pillar operators to sign a message and DM it to @romeo or an admin here on the forum.

* Open Syrius
* Go to **Settings**
![image|330x160](upload://oYtzsJdOkHrXN0vXNge6UdDubwy)
* Scroll down to **Security** and select **Sign**
![image|495x341](upload://aT7XePaJRDzQwC9bVGORBVm5f19)
* Input the Pillar name and press **Sign**
* Once you press Sign you will be given a Signature and Public Key string
![image|478x338](upload://c4FFIqGnT2OzqTRQ11Xu8HDTgHT)
* Copy the strings and send to a forum Administrator in this format:

> {
> “message”: “PillarName”,
> “address”: “WALLET ADDRESS”,
> “publickey”: “INSERT PUBLIC KEY FROM SIGNED MESSAGE”,
> “signature”: “INSERT SIGNATURE FROM SIGNED MESSAGE”
> }

We then use this [API & script](https://reqbin.com/7pdoxmxx) written by @vilkris to decrypt the messages and confirm it came from the address provided.  We are then manually checking the address provided against the know list of pillars.  Once "verified" Pillars will be given a badge and eventually will be put into a group for better communication channels. 

Once verified, you will be shown as a Pillar Owner in the forum and the community can be assured it's legitimate.

We hope to automate this entire process with a forum plugin, but until then it's manual.  We hope all Pillars can complete this process so we have a clear communication channel.

-------------------------

romeo | 2022-05-12 23:17:10 UTC | #2



-------------------------

