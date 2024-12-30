Thread: zenon-db-bootstrap
Jdbitmac | 2024-03-27 15:19:54 UTC | #1

I’m wanting to make a bootstrap of db.  Which files do I need?  3 I believe.

-------------------------

0x3639 | 2023-09-25 09:30:59 UTC | #2

Are you trying to backup a bootstrap for syrius or a node? if syrius, windows or mac?

-------------------------

0x3639 | 2023-09-25 09:33:52 UTC | #3

**macOS Users**

1. **Close Syrius.**
2. **Open Finder.**
3. Press `⌘ + shift + H` to go directly to your *Home* folder.
4. Now press `⌘ + shift + period (.)` to make the hidden *Library* folder visible.
5. Navigate to the `Library/znn` folder.
6. Once you’re inside the folder, **copy** these directories: *nom*, *consensus*, and *network*.
7. **Launch Syrius**. 

---

**Windows Users**

1. **Close Syrius**
2. Open the Windows Explorer and navigate to the following path:
`C:\Users\<username>\AppData\Roaming\znn`**Note**: Replace `<username>` with your actual Windows username.
3. Inside this directory, you should see several folders. **Copy** these specific directories: *nom*, *consensus*, and *network*.
4. **Launch Syrius**. The application should start the re-syncing process from scratch.

---

-------------------------

Jdbitmac | 2023-09-25 09:44:33 UTC | #4

This would be for a Linux node

-------------------------

0x3639 | 2023-09-25 09:54:00 UTC | #5

```
sudo -i
systemctl stop go-zenon
cd ~/.znn
cp -r nom/ nom.bak
cp -r consensus/ consensus.bak
cp -r network/ network.bak
systemctl start go-zenon
```

-------------------------

0x3639 | 2023-09-25 09:53:05 UTC | #6

here is a script I wrote if you want to backup to digitalocean

https://gist.github.com/0x3639/4678e255c1f92fbec2cdbd0315e1a127

-------------------------

mehowbrainz | 2023-09-25 13:04:57 UTC | #7

Topic moved to #zenon

-------------------------

