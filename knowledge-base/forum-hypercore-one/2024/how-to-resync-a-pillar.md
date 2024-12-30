Thread: how-to-resync-a-pillar
0x3639 | 2023-08-09 16:23:27 UTC | #1

```
sudo -i
systemctl stop go-zenon
cd /root/.znn/
rm -r consensus nom network
systemctl start go-zenon
```

You can check if you are on the right chain by running:
```
grep '5095219' /var/log/syslog

```
The hash should be `0ef9c2dd27e694d754ddf0e2306459417ceef74f23b1f0b6dafdcd19b556e830`

https://explorer.zenon.info/momentum/5095219

-------------------------

shaimo | 2023-08-09 18:46:50 UTC | #2

That grep doesn't find anything on my nodes

-------------------------

sumamu | 2023-08-10 12:03:34 UTC | #3

```
watch systemctl status go-zenon
```

Run this, and compare one of the momentum hashes to https://explorer.zenon.info

-------------------------

