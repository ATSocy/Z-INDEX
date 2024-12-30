Thread: node-connectivity-communication-test
0x3639 | 2023-08-21 16:25:39 UTC | #1

I setup 17 nodes all over the world.  I'm checking the status every 60 seconds and recording them to a DB.  You can see results here.

http://143.244.145.198:8080/

State 1 = Out of Sync
State 2 = In Sync
State 3 = Low Peer Count
Timout = No Response from AP

Way too many timeouts represented by the API not responding within 10 seconds.  I'm also noticing that the nodes are restarting by themselves at memory usage levels below 80%.

-------------------------

georgezgeorgez | 2023-08-21 17:34:44 UTC | #2

How big are these nodes?

-------------------------

0x3639 | 2023-08-21 17:45:56 UTC | #3

8g ram and 2vcpu.  I'm messing around with this tracker website.  It's going up and down right now.

-------------------------

0x3639 | 2023-08-21 18:00:03 UTC | #4

I just restarted the test.  Removed the DB and started over. All nodes are 100% synced and should return "state"; 2

-------------------------

0x3639 | 2023-08-21 20:47:54 UTC | #5

If you don't want to click on that link, here is the screen shot after about 2-3 hours.  

![image|394x499](upload://lIKIKfviz9DRQZ38xlICqggKvE5.png)

-------------------------

0x3639 | 2023-08-22 08:41:13 UTC | #6

latest results after about 18 hours.  I'm going to tear down this test.  It's expensive to run.

![Screenshot 2023-08-22 at 3.40.26 AM|381x500](upload://m8GxBGQed0rhmRxRhX64nzUB7Xm.png)

-------------------------

