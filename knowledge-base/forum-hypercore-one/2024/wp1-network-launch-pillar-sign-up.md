Thread: wp1-network-launch-pillar-sign-up
georgezgeorgez | 2024-10-28 15:13:45 UTC | #1

Coordination thread for network launch pillar sign up

-------------------------

georgezgeorgez | 2024-11-07 02:25:41 UTC | #2

The pillar sign up work will require:

* a message format and signature to link hyperqube_z pillars to their mainnet pillar sponsors
* instructions/guide
  * may require new key creation, especially for producer, and to save those keys for network launch
* announcement via AZ
  * the goal is to provide a last call for pillars who want to participate in the hyperqube_z incubator and governance systems
* signature verification script

For example:
The message format could be something like

"[mainnet pillar name]  [hyperqube_z pillar name] [hq_z pillar owner address] [hq_z pillar withdraw address] [hq_z pillar producer address] HYPERQUBE LAUNCH"

and signed by the mainnet pillar owner address

For signature collection, what I want to prove is that any pillar who wanted to participate was given a chance. We can first collect signatures off-chain via discourse and matrix. The AZ announcement can provide instructions on how pillars can submit a sign up via AZ. If no AZ signups occur within a timeframe, then our off-chain list is thorough.

The current round 1 incentives based on median pillar votes:

Pillar Sign Up
1500 / 80250 Points
280 / 15000 ZNN
2804 / 150000 QSR

**Disclaimer** : The payment amounts provided herein are intended as guidelines only and do not constitute a binding offer or guarantee of payment. The HyperQube Incubator framework works with Zenon Network Pillars to signal incentives which are subject to change over multiple rounds. Actual payment amounts will be based on Accelerator-Z grants that depend on the voting rules and requirement of Accelerator-Z.

-------------------------

coinselor | 2024-11-13 11:41:21 UTC | #3

I'd be happy to nominate myself for this task and will work through the requirements, including creating the message format, drafting the guide, and setting up the signature verification script. I’ll also handle the announcement on AZ and ensure clear instructions are provided for all pillars willing to participate. 

Do you have an ETA for when it needs to be finalized?

I also noticed that ZenonHub implements a signature verification API endpoint, so I could quickly set up a website where pillars can submit their information and have it verified automatically. This would streamline the process and help ensure we capture a thorough list of participants.

-------------------------

georgezgeorgez | 2024-11-14 06:57:22 UTC | #4

Thank you @coinselor! Please begin the work at your convenience.

Of course the sooner the better, but there are many moving pieces and we'll get a better sense of urgency as we go if things get blocked. I am working on the code & config and the final genesis file will depend on your work. One expectation I am hoping to set is for contributors is to post a weekly update. It's okay if there's no progress every now and then, but let's showcase incremental work.

Just an arbitrary date, but if we can get a network up by end of year, would be neat. We probably want to leave a bit of time for the AZ announcement to sit. So maybe a tentative due date would be like Dec 7, by beginning of Dec would be even better.

One thing I forgot to mention is that it may be helpful but not critical is having pillars provide a node ID for genesis seeders as well. It's not strictly necessary since we could probably get by with a handful of seeders run by HC1 and whoever else.

-------------------------

georgezgeorgez | 2024-11-14 06:58:40 UTC | #5

Btw, I just want to mention that your work will be important to learn from when it comes to building out the HyperQube LaunchKit for others to spin up extension chains. There will probably be things that we can reuse.

-------------------------

coinselor | 2024-11-17 20:23:11 UTC | #6

**Update**: I've started building a website that fetches all pillars and enables users to edit and submit the required fields for signature validation of the message format.  Aiming to have a working demo ready in the next few days.

-------------------------

