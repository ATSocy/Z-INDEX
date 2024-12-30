Thread: pprof-results-from-go-zenon
0x3639 | 2023-07-02 11:57:43 UTC | #1

@aliencoder @sol not sure where to begin to analyze this.  I'll look for some visual analizers.  

The heap is growing over time.   I will post some exports.  This one is at 45% memory usage.

[heap-45%.txt|attachment](upload://tBZrEiXu0svRylS6g3wao1udzcw.txt) (4.0 MB)

-------------------------

0x3639 | 2023-06-16 19:32:26 UTC | #2

Heap at 60% memory usage

[heap-60%.txt|attachment](upload://me1Zb2ZVjkpUl8HmAL6fT7HMNoe.txt) (4.7 MB)

-------------------------

0x3639 | 2023-07-02 11:57:15 UTC | #3

@sol @aliencoder @sumamu @georgezgeorgez 

Guys, I'm starting to think the growing memory use issue is a real problem we need to fix now.  The orchestrator relies on znnd.  I'm in comms with all (most) of the orchestrators and they all seem to have go-zenon reboot every 24 hours.  That causes the Orchestrator to crash (reboot) every 24 hours.  

Today @vilkris had a 1006 error in the Orchestrator and it froze rather than rebooting.  I'm going to report an issue on the repo.  

As we launch the side chain I'm sure the infra will rely on local znnd.  We simply cannot have a network where go-zenon must be restarted every 24 hours to function.  I was able to get pprof data (posted above) but it's clear to me that I cannot trouble shoot this issue.  @sol had some ideas that I think we should discuss.

-------------------------

Chadass | 2023-07-02 13:08:33 UTC | #4

Disappointed at Mr. Kaine waving away the issue when we all reported it and when I insisted (loudly) saying it WAS a memory issue / memory leak. It would be interesting if ChatGPT could spot such issue in a long multi files code.

Where do you guys think it comes from?

-------------------------

0x3639 | 2023-07-02 16:02:51 UTC | #5

Sol has done some diligence / research and is more qualified to respond.

-------------------------

sol | 2023-07-04 04:24:30 UTC | #6

[quote="Chadass, post:4, topic:127"]
Where do you guys think it comes from?
[/quote]

I don't want to jinx it, but I may have resolved the issue.
Currently soaking the fix on Linux and Windows to see if memory allocation creeps up over time.

Early numbers indicating sub-200 MB memory required for a full node after it has synced, which is very different from the 5GB my *testnet* node was consuming.
While syncing with the fix, it fluctuates between 500-1500MB.

I might have discovered a second "leak"; not sure how to characterize it yet, but I may work on another optimization as well.

I'll confirm my findings with the Golang devs then write a post with troubleshooting steps in case anyone needs to do some performance profiling in the future.

-------------------------

0x3639 | 2023-07-04 09:42:36 UTC | #7

Like I said... Kaine's cousin!  Can't wait to see the results.  Great work.

-------------------------

MoonBaze | 2023-07-04 14:21:44 UTC | #8

@sol can you please share what have you found? I also started looking into the problem, maybe I could help you.

-------------------------

sol | 2023-07-04 21:51:19 UTC | #9

I'm getting some mixed results today so I haven't committed any code to git. 
Like I said, there may be more than one optimization required.

In terms of what I found:

The [handleMsg](https://github.com/zenon-network/go-zenon/blob/master/protocol/handler.go#L208) function spawns hundreds of thousands of orphaned goroutines.

Part of my patch is to add a channel to the goroutine that signals when the handleMsg() is finished parsing a peer's message.

This is what my WIP looks like:
```
c := make(chan int8)
go func() {
	select {
	case <-pm.quitSync:
		p.Disconnect(ErrNoStatusMsg)
	case <-c:
		close(c)
	}
}()
.
.
.
default:
	c <- 0
	return errResp(ErrInvalidMsgCode, "%v", msg.Code)
}
c <- 0
return nil
```

I'm aware `close` may not be necessary, `uint8` could be a `struct{}`. I'm seeing conflicting results when I try to simplify the code above.

Anyways, any insight would be appreciated :)

-------------------------

MoonBaze | 2023-07-05 11:36:20 UTC | #10

I was trying to find this in the original ethereum releases code (1.6, 1.7, 1.8) and this go func was not found. Maybe we could just delete it, I will take a closer look at the code though. This urls could help you.

https://github.com/ethereum/go-ethereum/blob/release/1.6/eth/handler.go#L305

https://github.com/ethereum/go-ethereum/blob/release/1.7/eth/handler.go#L313

-------------------------

MoonBaze | 2023-07-14 14:31:15 UTC | #11

I think I have fixed it, I looked at the Ethereum code base and these methods were not present in the releases so I removed them. Pprof showed me these would be spawned continuously and never returned. I have tested it by resyncing also and looks good. Try it yourselves. @sol @0x3639 

https://github.com/MoonBaZZe/go-zenon/tree/p2p-fix

-------------------------

0x3639 | 2023-07-14 14:33:31 UTC | #12

awesome.  I will try today.  Do I need to sync from genesis?

-------------------------

MoonBaze | 2023-07-14 14:47:50 UTC | #13

You should try it. And also do some RPC and maybe multiple connections.

-------------------------

0x3639 | 2023-07-14 15:06:43 UTC | #14

OK - I'm syncing now.  I'm trying with an 8g server.  I'll let you know when I'm synced up and start testing.

-------------------------

sumamu | 2023-07-14 16:01:49 UTC | #15

Mine's at 2.9M momentums and syncing.

-------------------------

0x3639 | 2023-07-14 16:06:03 UTC | #16

If this works it would be awesome to run this on a Raspberry Pi with no reboots.

-------------------------

sol | 2023-07-14 23:34:31 UTC | #17

Thanks for continuing to work on this.

Do you have any KPIs to quantify the improvement?

Anecdotally, it seemed to work at first, but I was still able to encounter situations when znnd would bloat to multiple GBs of memory.

-------------------------

0x3639 | 2023-07-14 23:54:22 UTC | #18

Here is my sync memory utilization. I'm about 75% done.  Seems to be pretty stable around 25% except the spikes. 

![Screenshot 2023-07-14 at 6.52.07 PM|553x500](upload://uPJprsEfPRFeB3dA5yBNjq3UFK8.png)

-------------------------

0x3639 | 2023-07-15 01:26:09 UTC | #19

has anyone been able to sync 100%.  I'm stuck around 75% and the node seems to be crashing.  syncs a few momentums, then znnd restarts.

-------------------------

sumamu | 2023-07-15 07:06:55 UTC | #20

Fully synced, no issues here. @MoonBaze has cracked it!

-------------------------

0x3639 | 2023-07-15 09:10:54 UTC | #21

Ya, me too.  Not sure what was going on with the sync. But I'm there too and the memory has been constant for several hours.  I've never seen this on any of my nodes. This one has 8g and it's using 40%.  Super exciting!!!

I'm going to buy a PI and try with one of them next.  

![Screenshot 2023-07-15 at 4.08.32 AM|555x500](upload://u0S4ClK2Mz7ufr5kTAkhwbHmgP1.png)

-------------------------

aliencoder | 2023-07-15 15:22:13 UTC | #22

IBD sync memory usage and p2p memory usage are 2 distinct things.

During IBD the memory usage can get higher when large momentums are being processed.

Also the number or connections is an important factor.

-------------------------

0x3639 | 2023-07-16 01:06:16 UTC | #23

Is anyone else seeing memory usage climb in steps?  Before, it would climb all the time slowly.  I'll keep monitoring this.  

![Screenshot 2023-07-15 at 8.04.51 PM|556x500](upload://kL27hlFQFGO8OmvGVejrJsZKwEf.png)

-------------------------

0x3639 | 2023-07-16 15:37:48 UTC | #24

back down to 39%.  Looks like those CPU spikes are doing something.  But the slowly growing memory usage has been fixed for sure. 

![Screenshot 2023-07-16 at 10.35.37 AM|553x499](upload://cAeeD6ZWUtdQnCo8kzbqzDjHwu9.png)

-------------------------

Bzed | 2023-07-16 21:29:24 UTC | #25

Are those spikes in CPU% a big deal for something like a Pi?

-------------------------

0x3639 | 2023-07-17 10:50:04 UTC | #26

probably not.  Pis are pretty powerful these days.  I'll let you know when I fire one up.

-------------------------

0x3639 | 2023-07-17 10:51:26 UTC | #27

Looking good.  

![Screenshot 2023-07-17 at 5.50.39 AM|542x500](upload://v6pONwaw8UE4Q6deb2TKRhKExm0.png)

-------------------------

0x3639 | 2023-07-17 10:52:54 UTC | #28

@MoonBaze does this branch support big int?  I want to update the public node so I can downsize the vps.

https://github.com/MoonBaZZe/go-zenon/tree/p2p-fix

-------------------------

sumamu | 2023-07-17 16:44:30 UTC | #29

[quote="0x3639, post:28, topic:127"]
@MoonBaze does this branch support big int? I want to update the public node so I can downsize the vps.
[/quote]

Yes, I've looked at the commits.

-------------------------

MoonBaze | 2023-07-18 08:15:20 UTC | #30

It does, maybe the pull request will also be accepted soon and you could just clone the master branch

-------------------------

