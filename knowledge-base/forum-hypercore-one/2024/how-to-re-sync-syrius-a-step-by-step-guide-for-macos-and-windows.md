Thread: how-to-re-sync-syrius-a-step-by-step-guide-for-macos-and-windows
0x3639 | 2024-02-12 14:44:55 UTC | #1

After the recent and unplanned `fork` users need to upgrade to SYRIUS v0.0.7.  

First, download the latest SYRIUS release: https://github.com/zenon-network/syrius/releases  If your sync gets stuck, follow these instructions:  

---

**macOS Users**

1. **Close Syrius.**
2. **Open Finder.**
3. Press `⌘ + shift + H` to go directly to your *Home* folder.
4. Now press `⌘ + shift + period (.)` to make the hidden *Library* folder visible.
5. Navigate to the `Library/znn` folder.
6. Once you're inside the folder, either **delete** or **rename** these directories: *nom*, *consensus*, and *network*.
7. **Launch Syrius**. It should now begin to re-sync.

---

**Windows Users**

1. **Close Syrius**
2. Open the Windows Explorer and navigate to the following path:
   `C:\Users\<username>\AppData\Roaming\znn`
   
   **Note**: Replace `<username>` with your actual Windows username.
3. Inside this directory, you should see several folders. Either **delete** or **rename** these specific directories: *nom*, *consensus*, and *network*.
4. **Launch Syrius**. The application should start the re-syncing process from scratch.
--- 
Remember, always make sure to backup SYRIUS and/or make sure you seed phrase is ready and works as expected.

-------------------------

Blueginger | 2023-10-15 13:13:08 UTC | #2

Followed this to resync my embedded node in win11. Its not synching from start. How to troubleshoot?

-------------------------

0x3639 | 2023-10-15 14:11:06 UTC | #3

which version of SYRIUS did you install?

-------------------------

Blueginger | 2023-10-15 14:23:02 UTC | #4

Issue happened with 0.0.7, didn't improve with 0.1.0. Running znnd alone too didn't work.

-------------------------

Blueginger | 2023-10-16 05:05:24 UTC | #5

Problem was my anti virus again. Had to re-do all permissions. Now note is syncing.

-------------------------

