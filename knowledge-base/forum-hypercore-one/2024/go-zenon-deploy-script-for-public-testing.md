Thread: go-zenon-deploy-script-for-public-testing
0x3639 | 2024-09-19 17:16:17 UTC | #1

The [Operations Special Interest Group (SIG)](https://zenon.wiki/index.php/HC1:_Operations_SIG) has been working on a bash script to simplify the process to deploy a `go-zenon` node.  The script is being made available today for public testing.

The script can be used to deploy, build, restore, and monitor `go-zenon`.  Over the coming weeks we plan to enhance the script to add additional functionality.  We will plan to add timeseries monitoring, advanced troubleshooting, and the ability to launch a testnet.

Today we are asking for public testing and feedback on the script.  The goal is to deploy `go-zenon` and then deploy the grafana monitoring stack.  You will be able to monitor the underlying node (vps) and certain `znnd` metrics.  

## Instructions

### Clone the Repo
`git clone https://github.com/hypercore-one/deployment.git`
  
### Move into that Repo
`cd deployment`

### Make the script executable
`sudo chmod +x go-zenon.sh`

### Execute the script
`sudo ./go-zenon.sh`

First the script will install all the necessary packages.  Then it will ask you which repo to clone.  Select `enter` for the default repo.  That is the `/zenon-network/go-zenon` repo.  We plan to change how this works in the future.

After `go-zenon` is built and started then you can install the monitoring package.

### Install Grafana
`sudo ./go-zenon.sh --grafana`

In order to see the metrics navigate to `http://IP_OF_VPS:3000`
Note we use `http` and NOT `https`.  The default username is `admin` and the default password is `admin`.  Change the password and look for the default dashboard setup.  There are two.  

Please provide feedback on the experience and let us know if you have any recommendations for improvement or change.  You can also submit issues or feature requests here: https://github.com/hypercore-one/deployment/issues

-------------------------

edgepillar | 2024-09-19 20:40:04 UTC | #2

Just built one. Super easy and working like a charm so far!

![Screen Shot 2024-09-19 at 23.38.30|690x113](upload://7ysjv7z5nOiVqLDiBwYfP2FFmIa.png)

-------------------------

coinselor | 2024-09-19 21:29:16 UTC | #3

![image|690x261](upload://bEGjyogI4VNOoH8mfQsIcIrv9vw.png)

Ran this over a working/synced zenon node. Worked without issues.

Minor stuff I noted:

- Missing line break at `ption":"","path":"","removed":false}Installation and configuration completed successfully.
`
- I wasn't sure if the grafana dashboard was going to work while the znnd node was still initializing. There's a loading animation but maybe we can add 'Loading...' or 'Connecting...' placeholder.

I also had to add 3000 to ufw so I could connect in this particular VPS, but I know the script is not touching firewalls yet.

Will try with vilkris branch from scratch.

-------------------------

