Thread: test-btc-atomic-swap-development-progress-with-results
0x3639 | 2022-06-11 16:47:50 UTC | #1

Step by step instruction to test BICH DAO BTC Atomic Swap progress.  Original instructions found here:  https://github.com/Big-Inches-Club-House/bich/discussions/1#discussioncomment-2917850

```
sudo apt-get install git
sudo apt-get install curl
sudo snap install go --classic
```

```
cd ~
git clone -b devnet https://github.com/Big-Inches-Club-House/go-zenon.git
cd go-zenon
make znnd
./build/znnd --data ./devnet generate-devnet --genesis-block=z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7,40000,400000
./build/znnd --data ./devnet
```

leave this running in the existing terminal.  Then open a web browser and go to [https://explorer.zenon.network](https://explorer.zenon.network/)
Connect to [http://127.0.0.1:35997](http://127.0.0.1:35997/)

search for the address
z1qqjnwjjpnue8xmmpanz6csze6tcmtzzdtfsww7

Results below. 

![2022-06-11_11-31-51|690x456](upload://2dSe3KVRTM7pZ9ZXRiRGSJfHBQv.png)

Next, open a new terminal

```
git clone https://github.com/Big-Inches-Club-House/htlc-demo.git
cd htlc-demo
go build fusion-demo.go
./fusion-demo
```
Results below.  These three new entries show 5,000 QSR being fused.  

![2022-06-11_11-38-20|690x334](upload://wkwCHQDHfWY5Hz3EBtYg2Z9xIT1.png)

-------------------------

