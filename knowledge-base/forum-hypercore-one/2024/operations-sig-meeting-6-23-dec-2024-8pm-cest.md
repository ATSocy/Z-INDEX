Thread: operations-sig-meeting-6-23-dec-2024-8pm-cest
0x3639 | 2024-12-23 15:04:09 UTC | #1

**What:** Meeting to Discuss Improving Node Operations
**When:** [23 Dec 2024 @ 8PM CEST](https://www.worldtimebuddy.com/?qm=1&lid=6,5,12&h=6&date=2024-12-23&sln=12-13&hf=0)
**Where:** [https://element.zenon.chat/#/room/#sig-operations:hc1.chat ](https://element.zenon.chat/#/room/#sig-operations:hc1.chat)
**Agenda & Notes:** [Operations SIG 23 Dec 2024 - Zenon Wiki ](https://zenon.wiki/index.php/Operations_SIG_23_Dec_2024)

Attention Participants. Please update the meeting notes before the meeting.

-------------------------

0x3639 | 2024-12-24 18:03:51 UTC | #2

## AI Meeting Summary: OP SIG Meeting on December 23, 2024

### AI Podcast Summary of the Meeting

https://www.youtube.com/watch?v=fzJpmIYO7dM

The meeting focused on several key areas including node performance, specifically sync speeds, and backup/restore procedures. The discussion also included potential improvements to testing methodologies and hardware recommendations for different node types.

**Key Discussion Points:**

*   **Sync Speed Issues:**  There are significant concerns about slow sync speeds, especially on cloud VPS platforms like Digital Ocean.  A user, Toker, experienced extremely slow sync times even with 8 vCPUs and 32GB RAM, with an estimated sync time of 3 weeks. It was suggested that shared CPUs may be a contributing factor. The single-threaded nature of leveldb, which is used for data storage, may also limit performance with higher core counts.
*   **Hardware Recommendations:** The group discussed the need for hardware recommendations for different node types (regular znnd node, pillar, hyperqube node). The consensus is that for critical nodes like pillars, dedicated CPUs, or even bare metal servers, are preferable to shared CPUs. It may be better to have one or two high-performance cores instead of many lower-performing cores.
*   **Performance Testing:** Georgezgeorgez wants to start performance testing the hyperqube\_z testnet. The group discussed using scripts to generate load and record the results in a wiki. A testing framework, K6, was mentioned, which could be used for load testing and generating reports. The group also discussed separating the network and verification aspects of syncing when measuring performance.
*   **Backup and Restore:** The group agreed that local backup and restore functionality was immediately important. The plan is to initially focus on local backups before implementing remote backups. The local backup/restore process involves stopping the service, copying files, restarting, and then compressing the copied files.  There was discussion of making the backup process more user-friendly, since `scp` may not be the best solution.
*   **Pillar Node Considerations:**  There was some discussion of allowing pillars to perform maintenance tasks during times when they are not producing a momentum. The group recognized the importance of a good user experience (UX), and that running a pillar from a user's wallet machine may not be suitable.

**Action Items:**

*   **deeznnutz:**
    *   Continue developing the sync speed testing script, focusing on measuring sync duration and server load per momentum.
    *   Implement local backup and restore functionality.
    *   Investigate backup rotation using `rotate-backups` library.
*   **georgezgeorgez:**
    *   Start performance testing the hyperqube\_z testnet.
    *   Define the work for a test suite to verify momentum ranges.
    *   Help define a work package for the new test suite.
*   **coinselor:**
    *   Investigate user-friendly alternatives to `scp` for backup transfers, possibly a web-based UI or an interactive terminal application.
*   **Group:**
    *   Establish minimum hardware specifications for pillars.
    *   Explore the potential of using the K6 testing framework.
    *   Further analyze and work plan for a more comprehensive test suite, hopefully on hyperqube.
    *   Validate the principle of using dedicated CPUs and more performant cores.
*   **All:**
    *   Gather performance metrics from users and their hardware.

**Next Meeting:**

The next meeting is scheduled for January 27, 2025, at 8:00 CET (1:00 EST).

-------------------------

