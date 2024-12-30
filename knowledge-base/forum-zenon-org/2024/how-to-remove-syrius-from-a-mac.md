Thread: how-to-remove-syrius-from-a-mac
0x3639 | 2024-03-27 15:20:00 UTC | #1

Does anyone know how to completely remove SYRIUS from a mac, including the wallet and blockchain sync?  I cannot seem to locate the `~/.znn` folder that is on the PC and Linux version.

Also I cannot `locate .znn` the folder on the mac.

-------------------------

aliencoder | 2023-04-23 20:09:50 UTC | #2

On MacOS aka `darwin`, the `znn` folder is [located here](https://github.com/zenon-network/go-zenon/blob/58eaa81439a39197dd9080230580fb8b47bcd323/node/defaults.go#L52): 
`~/Library/znn`
`/Users/your_username/Library/znn`

-------------------------

