Thread: how-to-upgrade-go-zenon-to-v0-0-7
0x3639 | 2023-08-12 10:17:53 UTC | #1

All node and pillar operators should upgrade to `go-zenon v0.0.7`.  The chain recently forked due to a bug caused by an [edge case](https://github.com/zenon-network/go-zenon/pull/26#issuecomment-1674697126) associated with a sort function.  

In order to upgrade follow these instructions:

`sudo ./znn-controller`

Select #1 to deploy.  This will upgrade `go-zenon` to version 0.0.7.  After you upgrade run the controller again.

`sudo ./znn-controller`

This time select #5 to resync.  If you are running a pillar on this node make sure to KEEP the existing producer file.  DO NOT replace the producer file.   if you want to speed up the sync you can run a cron job every 60 minutes to restart go-zenon.

**Note:** If you are 100% confident you are on the main chain, you do NOT need to resync.  You can check this by comparing a recent hash in your log files with the hash in explorer.zenon.info.  If the block and hash match, you do NOT need to resync.  You can see recent blocks and hashes in your node by running this command:

```
journalctl -u go-zenon -n 30 -f
```

Here are the steps to restart `go-zenon` every 60 minutes.  Remove this insertion after syncing.

```
crontab -e
```
then add this line
```
0 * * * * /usr/bin/sudo /usr/sbin/service go-zenon restart
```

A quick breakdown of the cron job:

* `0 * * * *`: This specifies the schedule. The `0` indicates the job runs when the minute is 0 (i.e., the top of the hour). The `*` symbols indicate that the job runs every hour, day, month, and day of the week.
* `/usr/bin/sudo`: This command allows permitted users to execute a command as the superuser or another user. Since restarting a service typically requires root privileges, we use `sudo`.
* `/usr/sbin/service go-zenon restart`: This is the command that restarts the `go-zenon` service.

Note:

* Ensure that the user whose crontab you are editing has permissions in the `/etc/sudoers` file to restart the service without a password. If not, you'd need to configure sudo accordingly, which may present security risks.
* Paths like `/usr/bin/sudo` and `/usr/sbin/service` might differ based on your operating system and configuration. It's good practice to ensure the paths are correct for your system (you can use `which sudo` or `which service` to get the correct paths).

-------------------------

Asgardians-Pillar | 2023-08-15 14:27:43 UTC | #2

My real-estate Pillar didn't fork off but after I updated it it's only catching half it's rewards.
Anything that fixes that?

Also except for putting in the crontab rule is there anything else pillars can do to speed up a full resynch?
I'm running both on a proper spec vps but it's very slow still. No bootstrap available?

Any thoughts on how to have everyone back online quicker the next time we have some kind of a forkoff event?

-------------------------

0x3639 | 2023-08-15 17:46:37 UTC | #3

See DM.  I am finding that nodes need 32G to handle this sync "well" without crashing.

-------------------------

