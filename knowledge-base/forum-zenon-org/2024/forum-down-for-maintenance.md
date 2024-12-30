Thread: forum-down-for-maintenance
DrD3 | 2023-01-30 16:43:01 UTC | #1

Zello!

Forum.zenon.org will be down for an hour at 9am CST (3pm CET) on Friday (29.07.22) for a server update from version 2.9.0.beta4 to 2.9.0.beta7.

-------------------------

0x3639 | 2022-07-29 12:29:21 UTC | #2

This upgrade requires a full upgrade to the front end and back end.  It also requires a reboot before doing anything.  So here are the steps I will take:

1) Backup data locally
2) Shut down server
3) Take Snapshot
4) Reboot the server
5) Stop the web server
6) Rebuild the DB and redis
7) Rebuild the web server

In the event of a failed upgrade I will try to trouble shoot the upgrade.  If I cannot resolve the problem in a reasonable amount of time I will restore from snapshot and then recover the data.

-------------------------

DrD3 | 2022-07-29 13:10:03 UTC | #3

Godspeed ser, hoping that this doesn't take too long!

-------------------------

0x3639 | 2022-07-29 15:07:19 UTC | #4

Upgrade complete without issue

-------------------------

