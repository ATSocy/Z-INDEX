Thread: docker-znnd-with-monitoring
0x3639 | 2023-02-08 22:34:59 UTC | #1

I'm finally making some progress on my automated node setup.  Do not test this yet.  I'm still working through some things.  I found a good project to start with and added znnd built from source and loki for log monitoring.  This uses Caddy for endpoint SSL which I'm liking a lot.  

This has a nice notification plugin so you can post notices to TG if you want.  

I plan to update the instructions and setup a few more dashboards specific to NoM.   I hope to be done by this weekend.   

https://github.com/0x3639/znndNode

-------------------------

sol | 2022-12-30 02:05:08 UTC | #2

Really nice work so far! What kind of specs do we need to run this docker image?

-------------------------

0x3639 | 2022-12-30 02:10:01 UTC | #3

Good question.  I'm hoping we can run it on a standard node (8g). But I'll need to test that for sure.

-------------------------

romeo | 2022-12-31 10:12:17 UTC | #4

Great stuff, let us know when it's ready for testing

-------------------------

CryptoFish | 2023-02-28 20:16:35 UTC | #5

Great work @0x3639, 

Just for reference, found two issues so far which are:

1. The `DOMAIN=${DOMAIN:-}` and `PUBLIC_IP=${PUBLIC_IP:-}` syntax doesn't work. Instead set directly with `DOMAIN=public.zenon-node.com` and `PUBLIC_IP=69.69.69.69`.

2. The url of the JSON_API data source in Grafana is staticly set to '02.deeZNNutz.com'.

There still might be an issue with the restart functionality. It seems to hang when trying to restart. Will need more testing to be sure.

-------------------------

0x3639 | 2023-02-28 21:27:09 UTC | #6

Thank you for testing.  I will try a fresh install and test again.

-------------------------

CryptoFish | 2023-03-01 11:13:26 UTC | #7

Just wondering, If you make changes to the repo, can I just pull the changes and rebuild by issueing the following command?

```
git pull
sudo docker compose down
sudo docker compose up -d --force-recreate
```

-------------------------

0x3639 | 2023-03-01 17:52:58 UTC | #8

yes, that will make the changes:  it will update the code and recreate the images.  All synced data and changes to grafana will persist.  I'll test the changes and update soon.

-------------------------

