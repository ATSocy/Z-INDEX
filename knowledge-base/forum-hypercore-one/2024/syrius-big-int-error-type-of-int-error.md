Thread: syrius-big-int-error-type-of-int-error
0x3639 | 2024-03-09 01:13:16 UTC | #1

If you are getting the following error from syrius 

`type '_OneByteString' is not a subtype of type 'int'`

It means you are using an older version of syrius with a new pubic node.  You can fix this one of two ways:

1) Update syrius to the latest version https://znn.link/syrius
2) Change the public node to a legacy node `wss://legacy.hc1node.com:35998`

![Screenshot 2024-03-08 at 7.07.05 PM|690x275](upload://j2deP6IDwm830CxfrChnk3MnyVq.jpeg)

-------------------------

