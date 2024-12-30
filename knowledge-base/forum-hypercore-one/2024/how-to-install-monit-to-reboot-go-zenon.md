Thread: how-to-install-monit-to-reboot-go-zenon
0x3639 | 2023-06-14 20:24:04 UTC | #1

# What is Monit?
Monit is a utility for managing and monitoring processes, programs, files, directories and filesystems on a Unix system.

Node and Pillar operators can use Monit to monitor memory usage and use it to restart `go-zenon` when the host memory usage exceeds a certain percent.  This is especially useful if you are running an orchestrator on your Pillar.  The orchestrator requires a valid `go-zenon` node and when the node goes offline the orchestrator will fail. 

If you restart your node or pillar with a cron job, consider implementing monit to reduce the restarts.  This will make the node more stable and will help with the operation of the orchestrator.  

## Step 1 - Install Monit

```
sudo apt install monit
```

## Step 2 - Create a monit file to monitor host memory usage

```
sudo nano /etc/monit/conf-available/host
```

Paste the following content into the `host` file
```
check system $HOST
    # if loadavg (5min) > 3 then alert
    # if loadavg (15min) > 1 then alert
    if memory usage > 70% for 1 cycles then exec "/usr/bin/systemctl restart go-zenon"
```

## Step 3 - Activate the `host` monitoring configuration
```
ln -s /etc/monit/conf-available/host /etc/monit/conf-enabled
```

## Step 4 - Reload Monit to Activate memory monitoring
```
monit reload
```

## Step 5 - Check to make sure Monit is running properly
```
sudo systemctl status monit
```

-------------------------

aliencoder | 2023-06-14 20:26:24 UTC | #2

Did you try `pprof` to debug the memory leaks?

-------------------------

0x3639 | 2023-06-14 20:29:10 UTC | #3

Not yet.  I'm not super familiar with `pprof`.  But I do think solving this issue is critical to orchestrator stability.  I'm talking to lots of pillars and I'm pretty sure stability is impacted b/ everyone is on a cron to reboot go-zenon.  Some reboot 4x a day.  

I can try to mess around with it this week.

-------------------------

tapwoot | 2023-06-14 20:37:33 UTC | #4

Thanks for the instructions for Monit, 4 times a day lol that was me...

-------------------------

aliencoder | 2023-06-14 20:44:55 UTC | #5

https://github.com/uber-go/goleak

https://reintech.io/blog/an-overview-of-gos-debug-package-profiling-and-tracing

-------------------------

0x3639 | 2023-06-16 15:05:09 UTC | #6

`go-zenon` is remarkably unreliable.  I have a healthcheck running on 2 nodes.  it runs a syncInfo check every 30 seconds and gives me the results in telegram. The service is either unresponsive (takes longer than 5 seconds to respond) or is out of sync, about every 30 minutes.  It's more unresponsive than out of sync.  

I'm starting to think this memory issues is critical to solve.  The orchestrators rely on it.  When memory usage approached 70% on a 16g node, the results get worse.  

After I finish up trying to stabilize the public node, I'll try `pprof`.

-------------------------

0x3639 | 2023-06-16 16:00:39 UTC | #7

Instructions to follow

https://forum.zenon.org/t/growing-memory-usage-in-go-zenon/1343/12?u=0x3639

-------------------------

Chadass | 2023-06-17 15:25:51 UTC | #8

Cronjobs work well for me, the orchestrator isn't down since I updated it correctly.

-------------------------

