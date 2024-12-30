Thread: draft-how-to-register-a-pillar-for-hyperqube-z
coinselor | 2024-12-21 12:52:56 UTC | #1

We have made it easy for any Zenon Network Pillar to register a spot on hyperqube_z.

To sign up, you just need to sign a message using your **NoM pillar address**. We created a website with a form to help you generate the custom message, copy it, and provide the signature.

## **What You Need**

- **A name for the hyperqube_z pillar**: This will uniquely identify your pillar within the network, just like in NoM.
- **A Zenon address for the hyperqube_z pillar**: This is the address that controls the pillar and is used for voting.
- **A Zenon address for pillar rewards**: You can optionally specify a different address to receive pillar rewards.
- **A Zenon producer address**: This address runs the hqzd node software and creates momentums. For security reasons, it must be different from the pillar address.
- **Syrius Wallet**: You will use Syrius to sign the message and/or create new addresses.

Once you have gathered all this information, you are ready to proceed.

# How-to Video:
https://www.youtube.com/watch?v=jxbKJmvtBrI


## **Steps to Register**

1. **Go to** https://qubepad.vercel.app/register
2. **Search for your pillar name** and click **Register**.
3. **Fill in the required fields** to generate a custom message.
4. **Copy the generated message** to your clipboard.
5. **Open Syrius**: Go to **Settings** > **Security** > **Sign**. Paste the message, then click **Sign**.
6. **Copy the signature in hex format** and paste it into the signature field on the registration page.

That's it! If the signature is correct, it will be validated automatically, and your pillar will be registered successfully.


---
## **FAQs**

### **What is a producer address, and why must it be different?**
A producer address is a Zenon address used to create momentums, which are essential for producing momentums. For security reasons, the pillar private key should never be exposed on a third-party cloud server, such as a VPS server. Instead, pillars should connect to a producer address that can safely create momentums without exposing the pillar's private key.

-------------------------

georgezgeorgez | 2024-12-18 18:47:03 UTC | #2

Okay sorry for all the delay. Have been juggling a few things,

I think the fastest way right now for someone to get setup is to generate a devnet and take the producer address from there. We will then replace genesis and config.json. But this way they have the folder structure already.

So I think comprehensively:
1. Download nomctl on your wallet machine, the one you will use to vote etc. Create a new key, which will be the pillar registration and withdraw key.
2. On a VPS, download nomctl and create a devnet for the file structure etc. Get the producer address.
3. Register using the registration app.

After everyone has done that.

4. Download the shared genesis file.
5. Configure the config json (for peer data/seeders). A few of us will make sure to have stable nodes up first to connect to.
6. Run the deploy script which will build hqzd and install it as a service using the existing directory
7. Wait for genesis launch time.

-------------------------

georgezgeorgez | 2024-12-18 20:09:37 UTC | #3

Some commands

Note you will need golang installed
```
sudo apt install golang
```

```
# For Step 1
# On wallet machine
git clone -b hyperqube_z https://github.com/hypercore-one/nomctl.git
cd nomctl
make nomctl
# for future convenience we will call the keystore hqz
./build/nomctl znn-cli wallet.createNew <YOUR_PASSWORD> hqz

# we need to get the address
# should create a better way to do it, but for now
./build/nomctl znn-cli -u https://my.hc1node.com:35997 -k hqz balance
```

```
# For Step 2
# On VPS
git clone -b hyperqube_z https://github.com/hypercore-one/nomctl.git
cd nomctl
make nomctl
./build/nomctl -hq generate-devnet
ls ~/.hqzd/wallet
```

Edit changed urls to use https instead of ssh

-------------------------

coinselor | 2024-12-19 17:29:07 UTC | #4

Registered.

Just making a note to adapt final instructions to include WSL/Windows instructions for the wallet machine where they might differ.

But we are still waiting for the deploy script to figure out actual final instructions.

-------------------------

georgezgeorgez | 2024-12-19 18:08:57 UTC | #5

I just realized. I don't think this thread has a link to the registration app lol
https://qubepad.vercel.app/

-------------------------

