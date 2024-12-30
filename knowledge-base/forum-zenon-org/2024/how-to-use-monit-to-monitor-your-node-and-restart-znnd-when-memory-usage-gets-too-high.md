Thread: how-to-use-monit-to-monitor-your-node-and-restart-znnd-when-memory-usage-gets-too-high
0x3639 | 2024-03-27 15:20:11 UTC | #1

Several node and pillar operators have reported high memory usage for the znnd service.  I personally run a node with 64g of ram and it rarely runs out of memory.  However, on smaller systems with 16G of ram I regularly have issues with the znnd process consuming 100% of the ram and then crashing.  Users have resorted to setting up a cron job to reboot the service or server all together.  I found a better way to manage this situation with the use on [monit](https://mmonit.com/monit/).  

Monit is an open source tool that can monitor running services, memory usage, cpu usage and many other things.  With monit you can setup a Process ID file to monitor the znnd service.  When memory usage of znnd reaches a user defined threshold, you can setup an action to restart the service or send an email.  That way you can proactively monitor the znnd process and automatically take action when it hits certain thresholds.  The instructions below explain my basic setup for a Linux Machine running Ubuntu 22.04.  Over time I will expand these instructions to include a telegram notification bot.  

## Create a .pid file for Monit to Monitor
This assume you have installed the [znn-controller software](https://github.com/zenon-network/znn_controller_dart).  

```
sudo nano /etc/systemd/system/go-zenon.service
```
add the following line to the `go-zenon.service` file

```
ExecStartPost=/bin/sh -c "echo $MAINPID > /var/run/znnd.pid"
```
The service file should look like this when done.

```
    [Unit]
    Description=znnd service
    After=network.target
    [Service]
    LimitNOFILE=32768
    User=root
    Group=root
    Type=simple
    SuccessExitStatus=SIGKILL 9
    ExecStart=/usr/local/bin/znnd
    ExecStop=/usr/bin/pkill -9 znnd
    ExecStartPost=/bin/sh -c "echo $MAINPID > /var/run/znnd.pid"
    Restart=on-failure
    TimeoutStopSec=10s
    TimeoutStartSec=10s
    [Install]
    WantedBy=multi-user.target
```
In order to reload the changes to the systemd unit file type the following command.
```
sudo systemctl daemon-reload
```
## Install Monit on Ubuntu 22.04

```
sudo apt update && sudo apt upgrade
```

After running the system update command, install Monit Monitoring on Ubuntu 22.04. It is available to install through the default system repository. Hence, no need to look for some third-party repository for future updates.

```
sudo apt install monit
```
![Monit-installation-command-for-Ubuntu-22.04|690x339](upload://iCNOxWfKXI47hioT6q4vXGrs2aO.png)

## Check service Status & Verison of Monit

Once the installation is completed,  check whether its service is running without any error in the background.

```
sudo systemctl status monit --no-pager -l
```

![Check-the-Status-and-Verison-of-Monit|690x360](upload://cDq8zb8gTW7xhrG3rEhDRrolxqN.png)

Service Status

If it is not running, start it using:

```
sudo systemctl start monit
```

**To check the version:**

```
sudo monit --version
```

## Configuration File

The Monit program can be configured using the `/etc/monit/monitrc` file. There are numerous sample settings, some of which are commented out, which are self-explanatory, or whose comments contain help texts. I recommend that you do not make your own settings directly in this file. It is better to create a new one for the desired settings.

```
sudo nano /etc/monit/conf.d/znnd.conf
```
Paste in the following setting and modify them for your specific settings.
```
set mailserver [MAIL SERVER] port [PORT] #change MAIL SERVER and PORT
    username "USERNAME" password "PASSWORD" #change USERNAME and PASSWORS
    using tls #change tls to the correct protocol or leave as is

set alert changeme@gmail.com #change email address

check system $HOST
    if loadavg (1min) per core > 2 for 5 cycles then alert
    if loadavg (5min) per core > 1.5 for 10 cycles then alert
    if cpu usage > 95% for 10 cycles then alert
    if memory usage > 75% then alert
    if swap usage > 25% then alert

check process znnd with pidfile /var/run/znnd.pid
    start program = "/usr/bin/systemctl start go-zenon"
    stop program  = "/usr/bin/systemctl stop go-zenon"
    if cpu > 60% for 2 cycles then alert
    if cpu > 80% for 5 cycles then restart
    #if memory usage > 75% then alert
    #if memory usage > 90% then restart
    if totalmem > 32000.0 MB for 5 cycles then alert #adjust for your situation
    if totalmem > 40000.0 MB for 5 cycles then restart #adjust for your situation

```

## Enable m/Monit httpd port on Ubuntu

By default, port **2812** to communicate Monit will be disabled and has to be enabled by editing its configuration file.

```
sudo nano /etc/monit/monitrc
```

Find the line: **set httpd port 2812**

There remove the **#** tag for the following lines. Also, replace the **allow** and **use address** value from **localhost** to **0.0.0.0** if **you want to access the Monit web interface remotely** as shown in the screenshot.

You can also c**hange the default password** for the admin that is **monit**.

```
set httpd port 2812 and
use address 0.0.0.0 # only accept connection from localhost (drop if you use M/M>
allow 0.0.0.0/0 # allow localhost to connect to the server and
allow admin:monit # require user 'admin' with password 'monit'
```
![Access-Remotely-the-Monit-web-interface|690x460](upload://istmlBOuJvAs3j2S3iMGfmHCDuf.png)

## Check and Load the Changes

To check configuration files are without any errors use the following command:

```
sudo monit -t

# If there are no errors, you will receive the following feedback:
# Control file syntax OK
```
Reload Monit in order to load the changes
```
sudo systemctl restart monti
```

-------------------------

