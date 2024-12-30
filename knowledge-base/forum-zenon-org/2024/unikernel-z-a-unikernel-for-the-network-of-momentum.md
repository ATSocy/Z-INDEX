Thread: unikernel-z-a-unikernel-for-the-network-of-momentum
EovE7Kj | 2024-04-11 15:25:24 UTC | #1

---

**unikernel-z**

**Description:**A unikernel for the Network of Momentum

**URL:** https://github.com/EovE7Kj/unikernel-z

**Team:** EovE7K, bitcoin advocate/acolyte turned ZNNalien. Building and developing since 2013, langages of merit include C, Go, OCaml.
------
This proposal aims to develop a specialized operating system optimized for running NoM nodes with dual coin support over dual proof-of-work/proof-of-stake (PoW/PoS) consensus mechanism. The primary objective is to achieve feeless transactions by leveraging the unique features in a multi-chain architecture. The proposal focuses on delivering a lightweight, efficient, and secure unikernel solution tailored specifically for the Network of Momentum.

### Phases

#### Phase 1: Testnet

* High-level overview of main tasks:

```
    Develop the core components of the Zenon Unikernel, including support for PoW/PoS consensus mechanism, and networking capabilities.
    Optimize resource usage and performance for efficient operation within a unikernel environment.
    Implement basic security measures to protect against common threats and vulnerabilities.
```

* Completion of Phase 1 will be measured by:

```
    Successful implementation of PoW+PoS consensus mechanism within the unikernel.
    Demonstrable improvement in resource efficiency and performance.
    Deployment of a testnet version of unikernel-z for community testing and feedback.
```

#### Phase 2: zApps

* High level overview of main tasks:

```
    Enhance the security features of the unikernel by implementing advanced cryptographic algorithms and secure communication protocols.
    Integrate support for smart contracts and decentralized applications (zApps) within the unikernel environment.
    Conduct comprehensive testing and optimization to ensure reliability, scalability, and compatibility with Zenon's blockchain network.
```

* Completion of Phase 2 will be measured by:

```
    Implementation of advanced security measures and cryptographic protocols to safeguard the integrity and confidentiality of transactions.
    Successful integration of smart contract support, enabling the execution of decentralized applications within the unikernel environment.
    Validation of performance improvements and scalability enhancements through rigorous testing and benchmarking.
```

#### Phase 3: Adoptions

* High level overview of main tasks:

```
    Finalize documentation and deployment procedures for the unikernel-z, providing comprehensive guidance for node operators and developers.
    Prepare for Alphanet deployment and community adoption, including outreach efforts and educational initiatives.
    Address any remaining issues or optimizations identified during testing and community feedback.
```

* Completion of Phase 3 will be measured by:

```
    Completion of comprehensive documentation covering installation, configuration, and maintenance of the Zenon Unikernel.
    Successful deployment of the Zenon Unikernel on the Alphanet, enabling feeless transactions and supporting the growth of the ecosystem.
    Resolution of any outstanding issues or optimizations based on community feedback and testing results.
```

-------------------------

sultanofstaking | 2024-04-11 13:13:26 UTC | #2

Exciting stuff and love measurable outcomes at each phase. This is beyond me technically so will let others chime in there. Only question is how do phases and funds request correlate?

-------------------------

EovE7Kj | 2024-04-11 15:03:11 UTC | #3

Phases will follow a linear funding progression, as initial phase will require the least amt of resource allocation, subsequent phases will require more.  

---
**Phase 1: 1kZNN,10kQSR**    | majority of budget to be allocated toward testnet development/architecture.  Will likely need to work with other devs who have commits to go-zenon)

**Phase 2: 1.5kZNN,15kQSR** | majority of budget: zApp + smart contracts betas; potential to coincide with other parallel accelerator project(s) 

**Phase 3: 2.5kZNN,25kQSR** | majority of budget: alphanet implementation will be a massive undertaking, especially with regards to long-term support model

-------------------------

NeoShredder | 2024-04-11 16:09:00 UTC | #5

[quote="EovE7Kj, post:1, topic:1871"]
**Team:** EovE7K, bitcoin advocate/acolyte turned ZNNalien. Building and developing since 2013, langages of merit include C, Go,
[/quote]

What's the probable time line for each phase?

-------------------------

0x3639 | 2024-04-11 16:29:54 UTC | #6

Professor E7K,

I'm curious how you came up with the AZ amount.  Don't get me wrong.  I am not complaining.  I'm just wondering the logic behind the number.  

The value of this AZ seems to be greater than what you are asking for.  

Thank you and we are here to help in any way possible.

-------------------------

sultanofstaking | 2024-04-11 16:32:38 UTC | #7

lol send this man to negotiating 101

-------------------------

everlastingOS | 2024-04-11 16:55:49 UTC | #8

With unikernel (an OS) on NoM, will zApps support or running decentralized storage, just like Windows OS handles C:/ drive? So i can be able to access and run my own zApps storage from Raspberry Pi behind my routers NAT, ex a messenger or file sharing (rent out storage for ZNN/QSR) application on NoM.

-------------------------

aliencoder | 2024-04-11 18:21:09 UTC | #9

[quote="EovE7Kj, post:1, topic:1871"]
The proposal focuses on delivering a lightweight, efficient, and secure unikernel solution tailored specifically for the Network of Momentum.
[/quote]

Can you explain how the unikernel will interact with NoM?

-------------------------

EovE7Kj | 2024-04-11 18:48:09 UTC | #10

@0x3639 I could not agree more. It was my understanding that the AZ funding was capped at 5k/50k Z/Q 
I have defined each of these phases with clear goals and metrics; but they are more open-ended in their individual scope... as I imagine aspects of each phase could necessitate their own AZ.
With regards to help -- I will absolutely be tapping this community as things progress. It's why I created an open repo rather than a private webpage for this.

-------------------------

EovE7Kj | 2024-04-11 18:59:43 UTC | #11

The unikernel will encapsulate all aspects of the Network, meaning it should eventually be the de facto runtime environment for **all** nodes. This may be ambitious, but it will not immediately require full overhauls of the existing codebase or network; Phase 1 will focus on "wrapping" our existing znnd in it's own unikernel. POC of this has already been tested by containerizing the go-zenon codebase and translating it to nanoVM kernel.

This will be a long, constantly evolving project... but the immense benefits (performance, scalability, security, immutability) will be well worth the development

-------------------------

EovE7Kj | 2024-04-11 19:21:18 UTC | #12

You as a user would be interfacing with the zApp via smartcontract.  The zApp you are interfacing with can (and should) run on its own unikernel. These in turn would interface with nodes via API, which run on a unikernel-z. 

Here, in phase 2, we can achieve POC of a zApp running on its 'flavor' of unikernel, interfacing with users and nodes as described above.

-------------------------

everlastingOS | 2024-04-11 19:25:50 UTC | #13

will happily look forward to this development.

-------------------------

mehowbrainz | 2024-04-11 19:55:33 UTC | #14

[quote="EovE7Kj, post:10, topic:1871"]
It was my understanding that the AZ funding was capped at 5k/50k Z/Q
[/quote]

Per submission yes, but also I think you missed:

> Proposals can be split into multiple submissions if they require larger budgets.

https://www.zenon.org/en/funding/process#learn-zenon

-------------------------

EovE7Kj | 2024-04-11 21:18:10 UTC | #15

That project will likely fork into multiple AZ proposals, once POC has been delivered and a functional Testnet is online. For now my initial funding proposal can be disregarded, as it may be more realistic to dynamically assess funding requirements and allocations.

-------------------------

0x3639 | 2024-04-11 21:21:07 UTC | #16

[quote="EovE7Kj, post:12, topic:1871"]
unikernel-z
[/quote]

I'm familiar with traditional virtualization stacks like docker and vmware.  Unikernels are new to me so I have a few stupid questions.

When you refer to the "unikernel" does that mean the unikernel stack / environment?  

Does a zApp run in the unikernel stack?  

What is the difference between a unikernel and  unikernel-z?  I think you mentioned that nodes run on a unikernel-z.

-------------------------

EovE7Kj | 2024-04-11 21:55:27 UTC | #17

No stupid questions at all.  This terminology can be confusing.

The nodes running unikernel-z provide the necessary runtime environment for deploying and executing smart contracts. The zApp interacts with this backend infrastructure to perform actions on the blockchain network.

A zApp can be thought of as its own entity, with its *own* unikernel, which interfaces with the NoM on the backend. 


Let's think of *unikernel* here as the ultimate VM; every one should exist for its own specific purpose, with the exact resources allocated for its existence, and nothing more.

This proposal is focusing on a unikernel which will encapsulate the NoM and its nodes (we can call this unikernel-z). This will bring intrinsic value to the security of the network, but the real value is the introduction of smart contract execution. Think of this as a virtual machine running on the nodes of the network (ie. EVM)

-------------------------

crack | 2024-04-11 22:59:05 UTC | #18

[quote="EovE7Kj, post:17, topic:1871"]
The nodes running unikernel-z provide the necessary runtime environment for deploying and executing smart contracts.
[/quote]

NoM only have embedded smart contract for now, is this project will also deploying "new smart contract" ?

As far as I know, the most Unikernel benefit is security. But about performance, can unikernel-z will enhance the NoM performance ? More tps maybe?

And what do you think about Narwhal &Tusk for NoM ? Will we should encapsulate this core upgrade (N&T) to unikernel-z ?

-------------------------

EovE7Kj | 2024-04-11 23:20:49 UTC | #19

Regarding your first point - from what I have surmised, the embedded 'smart contract' of the existing NoM was meant to be a "launchpad" toward a conventional L2 transactional space (one meant to coexist with the BTC blockchain). The OG ZNN Dev team could not have possibly meant for ZNN smart contracts to end here... 

Unikernel-z will absolutely improve  security.. but that is *only* the most salient point. Scalability, redundancy, and performance are guaranteed under a well-deveoped and well-executed unikernal runtime.  

If you've ever worked in a containerized (Podman/Docker/K8s) environment, you can attest: time to first byte on any given container is orders of magnitude greater than that of its baremetal counterpart, or even a traditional VM. Now, realize that a well-designed unikernel OS can dwarf the performance of a traditional container... the tech speaks for itself.

Lastly: [full disclaimer: this is a personal opinion, and does not speak for the Zenon community]  I am of the belief that **N+T** is a brilliant approach to the BFT question. I would welcome it into the NoM, but that is not for me decide.

-------------------------

crack | 2024-04-11 23:34:03 UTC | #20

I'm not a techy person at all, but I remember one of ZNN OG Mr. kainez prefere to build smart contract with WASM
I found this
https://github.com/Mewz-project/Mewz
Can we leverage this project for WASM unikernel smart contract?

-------------------------

EovE7Kj | 2024-04-11 23:37:02 UTC | #21

I re-read this comment and felt compelled to respond again.. 

One major benefit of the uikernel-ization of the NoM is the fact that NoM smart contracts ARE embedded within (and therefore isolated to) the application layer. 

If the end-goal of this Network is for interoperability with BTC (it **must** be), then the smart contracts layer (L2) must be handled *outside* of the application layer.

-------------------------

EovE7Kj | 2024-04-11 23:41:30 UTC | #22

WASM is just a tool like any other (C, Python, Go, Js). I am interested in it and have used it for various applications.

I chose OCaml here beacuse it is one of the few "Meta Languages" (see Lisp, Clojure) that is *ideal* for writing compilers, kernels, etc. It already has a rich library for unikernel development.

-------------------------

crack | 2024-04-11 23:53:39 UTC | #23

[quote="EovE7Kj, post:21, topic:1871"]
the smart contracts layer (L2) must be handled *outside* of the application layer.
[/quote]

I see, some community dev now focuse testing our L2/Sidechain "Supernova" that is compatible with EVM and WASM SC.

-------------------------

romeo | 2024-04-12 03:40:01 UTC | #24

Do you have any ideas or thoughts on what type of zApps would be suitable for early usage of your unikernal solution?

I love the proposal and would vote in favour 🙏

-------------------------

romeo | 2024-04-12 03:41:52 UTC | #25

I think (all imo) Supernova will provide flexibility for external intensive contract executions and EVM compatibility - whereas the unikernal solution mentioned here would be for native zApps and NoM execution specifically (and maybe BTC in the future?)

-------------------------

oginotvavra | 2024-04-12 08:41:39 UTC | #26

Welcome Sir,
could you introduce us to some of your previous work, or give us more insight into your team?

-------------------------

0x3639 | 2024-04-12 10:49:12 UTC | #27

I've been doing some research to make sure I understand this proposal. 

You are proposing to make unikernel-z, a runtime environment for deploying and executing smart contracts on NoM.  Unikernel-z will be a unikernel itself that will "encapsulate the NoM and its nodes". This runtime environment will enable zApps which are unikernel smart contracts with access to NoM consensus.  

1) Is this accurate?  Can you explain what "encapsulate the NoM and its nodes" means?

I understand unikernels are like `.exe` with the minimum OS / libraries required to boot and run.  They access the processor through the OS or Hypervisor.

2) Where will the zApp unikernels run?  Will they run directly on our network hardware?  Or, will zApps be deployed to Amazon, for example, (confirmed by some hash function) and run there and access NoM consensus over a p2p network?  

[quote="EovE7Kj, post:1, topic:1871"]
This proposal aims to develop a specialized operating system optimized for running NoM nodes with dual coin support over dual proof-of-work/proof-of-stake (PoW/PoS) consensus mechanism.
[/quote]

3) Does this mean that Pillars and/or nodes will run within the unikernel-z  runtime environment?

4) In order to run unikernel-z will the operators need access to Bare Metal hardware or the hypervisor?  Can unikernel-z be run on a VM offered by Amazon or Digital Ocean, for example?

5) In order to build and deploy zApps it will likely be written in Ocaml and use MirageOS to build the unikernel. Is that correct?  Ocaml looks to be a very performant language used by FB and Jane Street, but maybe the number of devs who can code in Ocaml is limited?  Do you see that as an obstacle to adoption?  Maybe the benefits of deploying zApps are so great, dev will simply need to learn it. 

6) I assume existing EVM contracts cannot be ported and need to be written from scratch as new zApps.  Is that correct?  Does that worry you?

Thank you

---

## Additional Information for the Community

What is a unikernel?  This video does a good job explaining it.  
https://www.youtube.com/watch?v=aQuEu9bpnVY&t=415s

More on MirageOS and how to set it up.  "MirageOS is a 'library operating system' for constructing secure, high-performance network applications across a variety of cloud computing and mobile platforms."
https://www.youtube.com/watch?v=S4kNwfCRCO4

-------------------------

sultanofstaking | 2024-04-12 13:34:00 UTC | #28

Since the community is negotiating against ourselves and suggesting you ask for more funds, can we put a point on what the initial funding request is (amount) and what needs to be delivered (goals & metrics) for funds release?

-------------------------

EovE7Kj | 2024-04-12 16:00:56 UTC | #29

This is a great post, the MirageOS videos are a perfect introduction to the concept of unikernel. To answer your questions:

> Encapsulating the NoM

* Eventually every single node (syrius, sentry, sentinel, pillar) *can* run within a single, lightweight runtime environment -- this is `unikernel-z`.  
* The fundamental idea here is it that the more standardized, minimal and efficient each node of the Network is, the more powerful and efficient the Network is.
* I dont remember exactly where I read this, but "*the big idea around unikernels, when it comes to the cloud, is: if the datacenter is the computer, then the cloud is its operating system*"
* *Does this mean that Pillars and/or nodes will run within the unikernel-z runtime environment?* -- They would not be **required** to run in unikernel-z, but they would certainly benefit from running in a unikernel as opposed to a traditional OS.

>zApps
* Where will they run? This is for the community (ie. zApp devs) to decide, but they will ultimately need to run as a node in the network (potentially, on Sentinels)
* The idea here is that users interact with zApps via the smart-contract layer, and smart contracts manage the zApp operation
* The development of zApps will be a massive undertaking, and this AZ will probably just brush the surface.

> Baremetal/Hypervisor/Cloud
- This is ultimately up to who is deploying their node
- Ideallty, you would want to run on a hypervisor, but public cloud and even baremetal hw will work.

> OCaml
- This is a good point, the learning curve for this language is steep.  MirageOS makes things *easier*, but other options can be explored (nanoVM, Unikraft, WASM, etc..)
- I propose OCaml because of my comfortability with it; I have used it for unikernel development for another (non-blockchain) project.
- There is potential for zApps to have unikernels written in a different language as long as the API between the node and the app is maintained, but this is a topic for another discussion..
> Existing EVM contracts
- I am still exploring this; ideally we would have some utility to extract the existing contract and translate/deploy. This will require significant dev work

I hope I answered all your quetsions.

-------------------------

0x3639 | 2024-04-12 17:59:05 UTC | #30

[quote="EovE7Kj, post:29, topic:1871"]
I hope I answered all your quetsions.
[/quote]

Yes this is very helpful.  Thank you.

It feels like this proposal could take crypto from analog to digital.  The scale of what is possible with this architecture is difficult to imagine given we are living in a 10 tps world on Ethereum with a shitty EVM.... and 75% failed TXs on SOL.    

It feels like a crypto native bank or games or twitter 2.0 with millions of users could deploy a zApp on NoM and scale up to offer a web 2 experience with a decentralized back end.  I can only assume this proposal relies on the assumption that N&T is possible and in a big way because if not the L1 will never handle the load given what could be possible with unikernels.

-------------------------

EovE7Kj | 2024-04-12 16:35:25 UTC | #31

[quote="0x3639, post:30, topic:1871"]
It feels like this proposal could take crypto from analog to digital. The scale of what is possible with this architecture is difficult to imagine giving we are living in a 10 tps world on Ethereum with a shitty EVM… and 75% failed TXs on SOL.
[/quote]
>  I can only assume this proposal relies on the assumption that N&T is possible and in a big way because if not the L1 will never handle the load given what could be possible with unikernels.


100% to both of these points.

I am a huge proponent of Narwhal and Tusk

-------------------------

EovE7Kj | 2024-04-12 19:51:10 UTC | #32

[quote="sultanofstaking, post:28, topic:1871, full:true"]
Since the community is negotiating against ourselves and suggesting you ask for more funds, can we put a point on what the initial funding request is (amount) and what needs to be delivered (goals & metrics) for funds release?
[/quote]
Given the amount of time and  work the project phases will require, I think the best option is to separate each phase into its own AZ project. Given that I have already submitted the proposal to the accelerator for 5k/50k, the metrics for the first phase can be broken down:

* 2k/20k: znnd running in unikernel (~3-4 weeks)
* 1k/10k: Demonstrable improvement in resource efficiency and performance (~1 week)
* 2k/20k: Successful testnet deployment (~4-8 weeks)

The timelines provided are approximate and intentionally conservative, allowing for a margin of flexibility.

Thoughts?

-------------------------

sultanofstaking | 2024-04-12 20:06:13 UTC | #33

How do you demonstrate 1 & 2 and will 3 be an open testnet? I am always looking for ways to spend more money running ZNN infra :)

-------------------------

0x3639 | 2024-04-12 20:40:12 UTC | #34

[quote="EovE7Kj, post:32, topic:1871"]
Thoughts?
[/quote]

makes sense to me.

-------------------------

EovE7Kj | 2024-04-12 21:13:26 UTC | #35

[quote="sultanofstaking, post:33, topic:1871, full:true"]
How do you demonstrate 1 & 2 and will 3 be an open testnet? I am always looking for ways to spend more money running ZNN infra :slight_smile:
[/quote]
1. `unikernel-znnd` will be released on the Git 
2. Quantitative analysis of znnd metrics (ie. performance testing on unikernel vs. docker vs. vm) I will push the data summary to the Git once completed.
3. Absolutely. The idea is to have an open fork of the NoM.  Anyone can download and spin up the `testnet-unikernel-znnd` to get on the testnet. 

I am thinking now that the 50k QSR can be allocated 100% toward Phase 2 zApp development ; I can fuse all of it to spawn a sentinel and use directly for zApp node interface.

-------------------------

aliencoder | 2024-04-12 22:01:31 UTC | #36

[quote="EovE7Kj, post:29, topic:1871"]
The fundamental idea here is it that the more standardized, minimal and efficient each node of the Network is, the more powerful and efficient the Network is.
[/quote]

I can run `znnd` on my Raspberry Pi or on AWS, in a VM or on bare metal. I don't understand what benefits can bring running `znnd` inside `unikernel-z`. Dockerizing `znnd` gives us similar performance and security gains. I don't think this is the direction outlined in the whitepaper..

I would try to build an unikernel runtime that is able to measure computations in a fully deterministic fashion with on-chain footprint.

We can use zk-proofs to attest a particular computation was carried out inside the unikernel and post the proof on-chain for verification. The embedded contract state can be updated if the verification is successful. Instead of running everything within the EVM, the computation will be offloaded to unikernels. The problem is how to measure computation. This is the tricky part where zk-proofs and other cryptographic schemes are needed.

@EovE7Kj I'm not against your proposal, just thinking out load how I see `unikernel-z`.

-------------------------

EovE7Kj | 2024-04-13 01:51:38 UTC | #37

[quote="aliencoder, post:36, topic:1871"]
I can run `znnd` on my Raspberry Pi or on AWS, in a VM or on bare metal. I don’t understand what benefits can bring running `znnd` inside `unikernel-z`. Dockerizing `znnd` gives us similar performance and security gains.
[/quote]
Developing a unikernel for znnd is just the first step in getting to the `unikernel-z`.  Certainly the goal here is not to simply "wrap" the znnd in a unikernel.. as you've surmised `unikernel-z` will be much broader scope than that. Although, I will note a unikernel-znnd should have much reduced attack surface, faster boot times, and lower resource overhead than a dockerized counterpart. 

[quote="aliencoder, post:36, topic:1871"]
We can use zk-proofs to attest a particular computation was carried out inside the unikernel and post the proof on-chain for verification. The embedded contract state can be updated if the verification is successful.
[/quote]

This is a great idea, especially offloading the computation to the unikernel. We could implement threshold signatures or MPC here as well. There are numerous implementations and mechanisms that can be employed at this level that could improve Network security and efficiency, and I am open to all ideas from the community.  

Your feedback is greatly apprciated @aliencoder, I am a fan of your Supernova chain.

-------------------------

0x3639 | 2024-04-15 13:17:36 UTC | #38

Wanted to share another resource for the community to watch about unikernels.  

This is pretty good if you want to learn more about the benefits of unikernels.  If you watch, start watching where I've linked it.  Running zApps and the Smart Contract layer in unikernels will be such a giant leap forward in crypto.

The speaker claims unikernels are 1400 time more secure than a Docker Container. And they are insanely fast.  Listen to the test they did on DNS.  

![Screenshot 2024-04-13 at 11.00.37 AM|690x383](upload://cd7QyjnBKVr5ZnG3hkZhpZjvDB9.png)

They got a DNS unikernel to come up in 45 ms.  Sounds like there are limitations on "easily" porting code to run in the unikernel.  Speaker mentions this. After watching this video it's becoming more clear what will be possible on NoM.  A lot!! Big applications that require a lot of security and/or scale.  Nothing I know of in crypto today can handle this scale and speed.    

But, it seems like writing code to run in a unikernel is specialized.  I don't think the "average" crypto bro launching a project will be able to easily spin up a zApp.  Maybe I'm wrong. Maybe crypto devs will just have to learn.  OCaml sounds very legit.  Like something Jane Street would use to manage trading.  
  
https://youtu.be/5TZYeAUifEU?si=YGmAEU9n9H9iUUUY&t=458

-------------------------

0x3639 | 2024-04-14 22:28:49 UTC | #39

[quote="EovE7Kj, post:29, topic:1871"]
“*the big idea around unikernels, when it comes to the cloud, is: if the datacenter is the computer, then the cloud is its operating system*”
[/quote]

Here is that quote.  Good article. => https://changelog.com/posts/the-big-idea-around-unikernels

Below is a playlist presented by a software engineer who goes through several academic papers about unikernels.  Do not watch this unless you want to really dig.  It's hours of videos.  

https://www.youtube.com/watch?v=3NWUgBsEXiU&list=PLOuhQnxVenf0dMrMDrq7VT1GwHCib9Sc0

Here is a unikernel dev kit https://unikraft.org/. They have a [Caddy Unikernel](https://github.com/unikraft/catalog/tree/main/examples/caddy) we can test out.  Maybe the community can learn something by messing around with these.

-------------------------

0x3639 | 2024-04-15 13:16:06 UTC | #40

@EovE7Kj how will Smart Contracts get deployed with this framework?  

Will the SC deployer upload the SC to the `unikernel-z` layer?  Or will the deployer need to deploy their own `unikernel-z` instance and deploy there?

-------------------------

EovE7Kj | 2024-04-15 13:17:38 UTC | #41

Love too see the excitement surrounding unikernels.  The implications of this technology are massive for the blockchain space.

[quote="0x3639, post:39, topic:1871"]
Here is a unikernel dev kit [https://unikraft.org/ ](https://unikraft.org/). They have a [Caddy Unikernel ](https://github.com/unikraft/catalog/tree/main/examples/caddy) we can test out. Maybe the community can learn something by messing around with these.
[/quote]

I was going to mention both `uikraft` and [ops](https://ops.city/) (ie. `nanovm`) can be used for early PoC.  In fact, I have already dockerized znnd and converted to a uinikernel `.img` via `ops`. I can share this for testing purpose if anyone is interested.

-------------------------

0x3639 | 2024-04-15 13:46:29 UTC | #42

[quote="EovE7Kj, post:41, topic:1871"]
I can share this for testing purpose if anyone is interested.
[/quote]

I would be interested in testing this.  I'm interested in how I'm going to run these in my infra.  I use vmware and Proxmox.  I see some unikernels can be run in proxmox but require a different configuration and setup. I'd like to test this.

-------------------------

EovE7Kj | 2024-04-15 15:39:02 UTC | #43

[quote="0x3639, post:42, topic:1871"]
I would be interested in testing this. I’m interested in how I’m going to run these in my infra.
[/quote]

working on the qemu and kvm images now.  For reference the docker image is publicly available: `docker.io/eove7kj/znnd:latest`

-------------------------

0x3639 | 2024-04-15 16:20:10 UTC | #44

[quote="EovE7Kj, post:43, topic:1871"]
docker.io/eove7kj/znnd:latest
[/quote]

Looks like it's private still.

-------------------------

EovE7Kj | 2024-04-15 18:38:53 UTC | #45

[quote="0x3639, post:44, topic:1871"]
Looks like it’s private still.
[/quote]
![image|690x209](upload://zvVcsVx77cDmZCYiOgJ7eYzoDds.png)

Hum, it shouldn't be.  I see 6 pulls since I pushed the image.  

Are you able to run the following? 
```bash
docker run -d --name znnd \
    -p 35995:35995 \
    -p 35996:35996 \
    -p 35997:35997 \
    -p 35998:35998 \
    docker.io/eove7kj/znnd:latest
```

-------------------------

0x3639 | 2024-04-15 19:14:01 UTC | #46

Sorry, yes I can access this.  Just spun it up no problem.

-------------------------

0x3639 | 2024-04-15 19:52:09 UTC | #47

@coinselor took a look at the whitepaper again and noticed this image.  Just wanted to share with everyone. Running a zApp on the Sentinel node seems to be consistent with the original vision in the WP.  

![image|561x500](upload://A00DZTlunxrxjHk82vznrRQUzGA.png)

From the WP. 

> Periodically, the users will need to pay for the zApps usage; this system will be designed in a similar way gas [53] is implemented for smart contracts as a fees mechanism that prevents abuse and circumvent the Turing completeness property (e.g. infinite loops). This process will be automatized through a series of smart contracts that will be used to manage the zApps operation and the transfer of gas. The user will have the possibility to cancel at any time the execution of the app, by either explicitly sending an abort command or by not paying the corresponding gas to the node.

-------------------------

0x3639 | 2024-04-15 22:53:58 UTC | #48

If anyone else want to test this, here are the steps:

Install Docker
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

Create a Docker Volume
```
docker volume create znn
```

Start the Docker Image
```
docker run -d --name znnd \
    -p 35995:35995 \
    -p 35996:35996 \
    -p 35997:35997 \
    -p 35998:35998 \
    -v znn:/root/.znn \
    docker.io/eove7kj/znnd:latest
``` 

I just started to sync.  Let's see how it does with the two tough momentums.  I'm running it small 2 vCPUs and 4G Ram to see what happens.

-------------------------

everlastingOS | 2024-04-17 17:26:08 UTC | #49

[quote="EovE7Kj, post:1, topic:1871"]
**Team:** EovE7K, bitcoin advocate/ac
[/quote]

With Unikernel, we can now enable a new era.

Imagine a Zapp within a secure runtime (Lightweight OS mobile app) that blocks unapproved connections and provides a robust framework of decentralized services as plugins ready to go.

A mobile application that runs your packaged Ionic-based Zapps within an ecosystem of Zapps all using the Zenons built-in wallet and Z-unikernel.

Unified interface for users to run multiple Zapps that can share a common identity, wallet, personal storage vault and more.
Every zapps (App capsule) can have its own runtime or unikernel, ex a messenger app inside mobile OS app.

-------------------------

EovE7Kj | 2024-04-17 19:48:46 UTC | #50

[quote="everlastingOS, post:49, topic:1871"]
Imagine a Zapp within a secure runtime (Lightweight OS mobile app) that blocks unapproved connections and provides a robust framework of decentralized services as plugins ready to go.
[/quote]

[quote="everlastingOS, post:49, topic:1871"]
Every zapps (App capsule) can have its own runtime or unikernel, ex a messenger app inside mobile OS app.
[/quote]
E X A C T L Y

-------------------------

everlastingOS | 2024-04-17 19:57:49 UTC | #51

This is what ZenonOS can do, what do the community think?

-------------------------

DrD3 | 2024-04-17 21:42:35 UTC | #52

That this sounds a lil too good to be true.

@EovE7Kj how did you come across the NoM ser?

-------------------------

EovE7Kj | 2024-04-17 21:50:38 UTC | #53

[quote="DrD3, post:52, topic:1871"]
how did you come across the NoM ser?
[/quote]
I have been a fervent supporter after reading the ANN in bitcointalk. Back in the days of the old QT wallet, when the only possible way to buy was via Telegram or Mercatox.

-------------------------

0x3639 | 2024-04-17 23:58:46 UTC | #54

[quote="everlastingOS, post:51, topic:1871"]
what do the community think?
[/quote]

I learn something new every day about this project. And the more I learn the more excited I get.  You highlight some amazing possibilities.  

TBH we (crypto users) live in a world with such limited, slow and expensive options that it's really hard to comprehend such a large advancement NoM can bring. This seems like such a large scale improvement, it's hard to believe it's feasible.

Have you ever tried Nostr?  That's like messaging with pigeons. And we are talking about enabling a decentralized framework on NoM that could allow messaging apps, banking, video streaming, etc.  It's mind boggling.  

I continue to think the L1 needs to be way faster than we think to handle these real world use cases.  

NoM will enable real world use cases we are missing.

-------------------------

EovE7Kj | 2024-04-18 04:09:44 UTC | #55


[quote="0x3639, post:54, topic:1871"]
I continue to think the L1 needs to be way faster than we think to handle these real world use cases.

NoM will enable real world use cases we are missing.
[/quote]

This - 100% 

Traditional L1's have barely scratched the surface in terms of intrinsic *usefulness* and it is why congestion, tx failures and fees are high. The L1 that finds a *useful* method of scaling is the one that will reign supreme in the end. 

[quote="everlastingOS, post:49, topic:1871"]
Imagine a Zapp within a secure runtime (Lightweight OS mobile app) that blocks unapproved connections and provides a robust framework of decentralized services as plugins ready to go.
[/quote]
Imagine 1000's of different applications existing in their own unique runtime environments -- with virtually no overhead -- running on top of nodes in the NoM, where participation is incentivized via the rewards for running as a  Sentinel. **Imagine the TPS with this scale of validators.**

-------------------------

everlastingOS | 2024-04-18 04:58:31 UTC | #56

It is pretty simple, the OS mobile app is just really a wallet with a app grid view, with one unikernel app store, to download the rest of Zapps running on unikernel. Yes have tried Nostr, can be good to look at how Feeds vision was, using DID, P2P carrier to handle all the data traffic, and using users own private data, think it as a private IPFS server running locally on your device, similar how Manyverse do. The nodes Pillars and sentinal cannot store all the data when we have Zapps like video streaming, social media like Nostr/Soapbox so on.

-------------------------

0x3639 | 2024-04-21 13:28:25 UTC | #57

@EovE7Kj how do you debug `unikernel-z`?

Interesting article shared by @rexznn in TG.  He also raised the concern above in the town hall we had.  The author of this article raises this issues as the single biggest problem with using unikernels in production.   https://bcantrill.dtrace.org/2016/01/22/unikernels-are-unfit-for-production/

-------------------------

sultanofstaking | 2024-04-22 00:46:38 UTC | #58

"Gotta have more htop, baby" - Bruce Dickinson

-------------------------

EovE7Kj | 2024-04-22 21:06:22 UTC | #59

[quote="0x3639, post:57, topic:1871"]
@EovE7Kj how do you debug `unikernel-z`?
[/quote]
I am planning to specify a port for `gdb` access, this is the same way that `ops` manages unikernel debugging. 

https://ftp.gnu.org/old-gnu/Manuals/gdb/html_node/gdb_130.html

-------------------------

sultanofstaking | 2024-04-23 12:06:00 UTC | #60

Can we link out to the phase requirements @EovE7Kj ?

* Successful implementation of PoW+PoS consensus mechanism within the unikernel.
* Demonstrable improvement in resource efficiency and performance.
* Deployment of a testnet version of unikernel-z for community testing and feedback.

-------------------------

aliencoder | 2024-04-23 17:39:04 UTC | #61

[quote="sultanofstaking, post:60, topic:1871"]
Successful implementation of PoW+PoS consensus mechanism within the unikernel.
[/quote]

I don't think this is the purpose of the unikernel. The unikernel should act as an off-chain component that interacts with an on-chain embedded contract and provides a trustless execution environment for `zApps`.

Also the tricky part is to develop a trustless operation environment for the unikernel and design a gas metering mechanism that is managed by an on-chain embedded.

-------------------------

everlastingOS | 2024-04-24 08:19:57 UTC | #62

100%

-------------------------

EovE7Kj | 2024-04-24 14:54:20 UTC | #63

[quote="sultanofstaking, post:60, topic:1871"]
Successful implementation of PoW+PoS consensus mechanism within the unikernel.
[/quote]
yes, correct. I conflated POC via znnd with the full scope in my original write-up -- I'll change this on the Git. 

The idea here was unikernelizing the fundamental element of the NoM - a node - and then using that POC as a foundation for zApp unikernel development.

-------------------------

sultanofstaking | 2024-04-27 11:06:06 UTC | #64

So what exactly is included in phase 1?

-------------------------

EovE7Kj | 2024-04-27 22:27:01 UTC | #65

Phase 1 is focusing specifically on znnd.  Delivery will consist of compiled targets (vsphere, aws, hyper-v, vdi) 

I already have the first vbox image up on the Git for people to spin up and test -- this is still in progress and will require improvements to resource allocation. 

These different targets can and should be used in the testnet when we begin to integrate zApps.

-------------------------

sultanofstaking | 2024-04-27 23:14:42 UTC | #66

You submitted a phase 1 for payment in AZ correct? Is that different than the Phase 1 you describe above?

-------------------------

EovE7Kj | 2024-04-28 15:54:00 UTC | #67

I submitted the phase 1 as outlined above, but was not aware this was a submission for payment. I was only trying to align the  first phase described here with the AZ. 

**As there is no timeline for quorum, I recommend remaining pillars await release of  deliverables before voting.**

-------------------------

EovE7Kj | 2024-04-28 22:55:04 UTC | #68

[quote="EovE7Kj, post:65, topic:1871"]
I already have the first vbox image up on the Git for people to spin up and test – this is still in progress and will require improvements to resource allocation.
[/quote]
https://github.com/EovE7Kj/unikernel-z/blob/main/znnd/unikernel/znnd-amd64.vdi

has anyone given the `vdi` a try? For me: depending on the VM resources it either crashes after first Momentum, or it runs through a bunch of Momentums then hangs.  I am still debugging. Could be helpful to have additional eyes on this :)

-------------------------

coinselor | 2024-04-29 01:23:51 UTC | #69

Happy to help, but I could use some extra guidance.

I've tried running this in a linux desktop VirtualBox, but I just see a black screen. 

Do I need to run this on a VPS? I assume the VPS needs to support nested virtualization. A few guiding steps would be appreciated.

-------------------------

EovE7Kj | 2024-04-29 13:41:13 UTC | #70

[quote="coinselor, post:69, topic:1871"]
Do I need to run this on a VPS?
[/quote]
For the time being the vdi is only VirtualBox compatible.  I am still working on building .iso for generic VPS, VM, on-prem.. but for specific cloud providers (AWS, Azure, DO) I am hoping to eventually provide prebuilt images

-------------------------

sultanofstaking | 2024-04-30 00:15:31 UTC | #71

There are likely a number of us that would volunteer to run this as coinselor said. We have a group running supernova w/ a chat on TG to troubleshoot - I am guessing most people there will help test this as well.

-------------------------

sultanofstaking | 2024-04-30 00:16:31 UTC | #72

But yeah for unikernal I will need you to explain some of this like I am a golden retriever lol

-------------------------

EovE7Kj | 2024-04-30 04:11:22 UTC | #73

[quote="sultanofstaking, post:71, topic:1871"]
There are likely a number of us that would volunteer to run this as coinselor said.
[/quote]

As the devs said from the beginning: "Zenon is community" 

I ultimately intend for this project to be a launchpad for community-driven development of unikerneled zApps. With that being said, the overall scope and direction of this project and its phases are subject to community feedback and engagement.  

For example -- since it has already been brought up -- OCaml *does* have a steep learning curve and adoption may be limited... we can absolutely explore implementing WASM or other languages/paradigms for unikernels during zApp phases.

@everlastingOS  and @aliencoder  have already proposed powerful, feasible use-cases for unikernel-z, and we have only just started the discussion.

-------------------------

0x3639 | 2024-04-30 16:41:24 UTC | #74

[quote="EovE7Kj, post:73, topic:1871"]
OCaml *does* have a steep learning curve and adoption may be limited…
[/quote]

I was riding bikes with a buddy who leads up the dev group for a high frequency trading firm.  He codes in C and other supporting languages.  He must have 30y of experience.  I asked him about OCaml and he said he never heard of it.  It was sort of funny...   He said he is siloed in their tech stack and has no time or incentive to learn anything else.

That doesn't mean much in this context.  I was just surprised someone with that much experience had not heard of OCaml.

-------------------------

sultanofstaking | 2024-04-30 17:17:20 UTC | #75

You should ask him if he wants to learn and send him here :slight_smile:

-------------------------

0x3639 | 2024-04-30 17:40:23 UTC | #76

I'm always trying to find angles to suck my friends in....  Start with, have you heard of OCaml??  Then go right to..... so I'm working on this crypto project....

-------------------------

TheDev1776 | 2024-05-01 00:04:53 UTC | #77

Interesting, figured a lot of HFTs use it since it is used heavily at Jane Street.

-------------------------

sultanofstaking | 2024-05-01 00:11:46 UTC | #78

This is your in, "Ah thought u would be familiar since top firms like Jane Street use it. What do you use, cobol?"

-------------------------

EovE7Kj | 2024-05-01 19:12:30 UTC | #79

[quote="0x3639, post:76, topic:1871, full:true"]
I’m always trying to find angles to suck my friends in… Start with, have you heard of OCaml?? Then go right to… so I’m working on this crypto project…
[/quote]

:laughing:
OCaml is a lot more commonly used in France (where it was created). I actually work for a company based in Paris, it's how I was exposed to the language. 

FWIW Arthur Breitman hired a French team to outsource the development of Tezos blockchain (written in OCaml).

-------------------------

romeo | 2024-05-11 03:41:53 UTC | #80

I'm keen to test as soon as you have an ISO compatible with vsphere or proxmox - looking for to it 🙏

-------------------------

0x3639 | 2024-05-06 12:07:45 UTC | #81

@EovE7Kj  I was looking at the WP again.  In the unikernel section the WP states: 

"Periodically, the users will need to pay for the zApps usage; this system will be designed in a similar way gas is implemented for smart contracts as a fees mechanism that prevents abuse and circumvent the Turing completeness property (e.g. infinite loops). This process will be automatized through a series of smart contracts that will be used to manage the zApps operation and the transfer of gas. The user will have the possibility to cancel at any time the execution of the app, by either explicitly sending an abort command or by not paying the corresponding gas to the node."

1) Do you have any thoughts on how this will be implemented?  Will "fees" be needed to pay for zApp usage, or will the fee be in the form of fused QSR or PoW?

2) Will the $PP token being dispensed by the faucet be used with zApps in any way?

3) What are Adaptive Smart Contracts?

Sorry for all the questions.  I'm inquisitive.  

![Screenshot 2024-05-06 at 7.04.22 AM|690x363](upload://1JodSUhKDiTJDR7qkF0B7JYoM5A.jpeg)

-------------------------

EovE7Kj | 2024-05-10 16:31:58 UTC | #82

Sorry for the delayed responses here, I have been traveling the past weeks and have been over my head at my day job.

[quote="0x3639, post:81, topic:1871"]
* Do you have any thoughts on how this will be implemented? Will “fees” be needed to pay for zApp usage, or will the fee be in the form of fused QSR or PoW?
* Will the $PP token being dispensed by the faucet be used with zApps in any way?
[/quote]

These are great points; as the WP addressses - smart contracts will need some mechanism of fees for Turing-completeness.  When I'd initially read this (years ago), I'd assumed the fees would be ZNN or a 'wrapped' version thereof.  I am not sure how fusing QSR could be implemented for smart-contract fees, as I had interpreted the zApp layer being a fundamentally separate abstraction. 

The notion of PP is very interesting; again I had assumed PP would eventually be converted to QSR, but this opens the door to an entirely new potential for the token.  

[quote="0x3639, post:81, topic:1871"]
What are Adaptive Smart Contracts?
[/quote]

Adaptive smart contracts essentially refer to smart contracts that can self-modify their behavior or parameters based on certain conditions or external factors. These can be used in dynamic yield farming, atomic swap apps.  

[quote="0x3639, post:81, topic:1871"]
Sorry for all the questions. I’m inquisitive.
[/quote]

Don't be sorry at all; in fact, your questions have already given me a few new ideas.  I am by no means an OG-dev, professorZ, or Mr Kaine.  I don't have all the answers. I am only a member of this COMMUNITY, and am humbly enthusiastic about this project.

We are all in this together. I proposed the unikernel AZ because of the skills and experience that I can bring to the table.  With regards to smart-contracts, this is going to be a dynamic work-in-progress of the COMMUNITY.

-------------------------

EovE7Kj | 2024-05-10 16:32:39 UTC | #83

[quote="romeo, post:80, topic:1871, full:true"]
I’m keen to test as soon as you have an ISO compatible with vshere or proxmox - looking for to it :pray:
[/quote]

I am close. Hoping to carve out some time this weekend to complete.

-------------------------

0x3639 | 2024-05-11 01:03:59 UTC | #84

## Question
I asked [Perplexity.ai](https://www.perplexity.ai/search/Zenon-Network-has-G.upxRSyRdaDQt4eS.53yg#0) - Do EVM smart contracts allow for adaptive smart contracts?

## Answer
No, traditional Ethereum Virtual Machine (EVM) smart contracts do not natively support adaptive or self-modifying behavior. EVM smart contracts are designed to be immutable once deployed on the Ethereum blockchain.

The immutability of smart contracts is a core principle in Ethereum, ensuring that the code and logic of a contract cannot be altered after deployment. This provides security, transparency, and predictability, as all parties interacting with the contract can be certain that the rules will not change unexpectedly.[1][4]

However, there are ways to introduce some level of adaptability or upgradability to EVM smart contracts through specific design patterns and proxy contracts. Some common approaches include:

1. **Proxy Patterns**: These involve deploying a proxy contract that acts as an intermediary between the user and the actual logic contract. The logic contract can be upgraded by deploying a new version and updating the proxy to point to the new contract address.[2]

2. **Eternal Storage Patterns**: These separate the contract's code and storage into different contracts. The code contract can be upgraded while maintaining the same storage contract, preserving the contract's state.[5]

3. **Governance Mechanisms**: Some contracts implement on-chain governance mechanisms that allow authorized parties (e.g., token holders) to vote on proposed upgrades or parameter changes to the contract's logic.

While these patterns enable upgradability, they do not provide true self-modifying or adaptive behavior as seen in Zenon Network's Adaptive smart contracts. The upgrades or changes in EVM smart contracts still require external triggers or interventions, rather than being driven autonomously by the contract itself based on conditions or external factors.[1][4]

Citations:
[1] https://link.springer.com/article/10.1007/s12083-021-01127-0
[2] https://www.usenix.org/system/files/sec21summer_rodler.pdf
[3] https://www.techtarget.com/searchcio/tip/Top-smart-contract-platforms-to-consider
[4] https://tatum.io/blog/smart-contracts
[5] https://www.immunebytes.com/blog/what-are-upgradable-smart-contracts/

-------------------------

romeo | 2024-05-11 03:41:29 UTC | #85

[quote="EovE7Kj, post:82, topic:1871"]
The notion of PP is very interesting; again I had assumed PP would eventually be converted to QSR, but this opens the door to an entirely new potential for the token
[/quote]

The PP token on the Network now isn't the same as PP from the testnet that was converted to QSR. I thought the PP on the network now was just another ZTS that was created by someone?

-------------------------

0x3639 | 2024-05-11 16:33:38 UTC | #86

Ya, $PP is really perplexing to me.  Appears that [Rigel](https://github.com/znnrigel?tab=repositories) created it and started to dispense it fairly in Aug 2023 with an air drop to all users.  He somehow created a vanity ZTS address that ended in `pp`.  I would like to know how.  I asked this in TG.  

And the $PP token was in the marketing video exactly when the "Adaptive Smart Contract" image appeared.  That leads me to believe $PP could be used to fuel adaptive smart contracts in some way.  BUT, if this was planned from the release of this video (Nov 26, 2021 ) how is it that the token was only created in 2023?  That seems pretty risky to telegraph the $PP token but create it years later.  

UPDATE:  I'm 99% sure my theories are fake news and failed schizo.  But I'm leaving 1% out there due to this image (adaptive smart contracts and PP on the same...).  Maybe Rigel is building something that uses PP to fuel a zApp.  But, that is complete speculation.  

![telegram-cloud-photo-size-1-5044367904820276263-y|690x363](upload://kDufh4Ca5AmPPPK0X7TgGULvDwA.jpeg)

-------------------------

0x3639 | 2024-05-11 10:46:10 UTC | #87

For anyone else looking into $PP, it was not in the [genesis.json](https://bafybeidgz3rykovlqzmlmncm73vylbrllkfd5vigiapan45bkimmjzp2fy.ipfs.dweb.link/?filename=genesis.json).

I did notice this in there:

`  "ExtraData": "000000000000000000004dd040595540d43ce8ff5946eeaa403fb13d0e582d8f#We are all Satoshi#Don't trust. Verify",`

-------------------------

aliencoder | 2024-05-11 16:24:47 UTC | #88

[quote="0x3639, post:81, topic:1871"]
* Will the $PP token being dispensed by the faucet be used with zApps in any way?
[/quote]

I think we should focus on adding more value to ZNN or QSR rather than other ZTS tokens.

-------------------------

romeo | 2024-05-12 23:22:30 UTC | #91

Please be respectful to other members - no need for direct personal comments

-------------------------

0x3639 | 2024-05-17 10:23:10 UTC | #93

I hope to run this today in Proxmox
https://github.com/EovE7Kj/unikernel-z/releases

Setup Instructions
https://forum.hypercore.one/t/how-to-setup-and-run-the-znnd-unikernel-in-proxmox/462

-------------------------

aliencoder | 2024-05-17 17:04:18 UTC | #94

Nice proof-of-concept. The next milestone can be a gas metering implementation for the unikernel.

-------------------------

EovE7Kj | 2024-05-17 19:11:57 UTC | #95

UPDATE! 

The qcow2 build that was pushed last night was not the correct image.  I am re-uploading with the *correct* build now.  @0x3639  I will let you know when this is ready.

-------------------------

EovE7Kj | 2024-05-17 19:25:26 UTC | #97

https://github.com/EovE7Kj/unikernel-z/releases/tag/unikernel-znnd 

New release

-------------------------

aliencoder | 2024-05-17 20:32:01 UTC | #98

@EovE7Kj check [zama](https://www.zama.ai/fhevm). I'm researching how we can integrate a gas metering system inside the unikernel controlled by an embedded contract.

Is it hard to create a custom module that is loaded by the unikernel? Can you tell a bit about the lifecycle of an unikernel? Thanks!

-------------------------

romeo | 2024-05-18 05:16:39 UTC | #99

getting stuck here - doesn't move on past this point

![image|690x275](upload://ut7t1x0rV4xVQqrIV2Sfok6CTQf.png)

will do some troubleshooting soon

-------------------------

0x3639 | 2024-05-18 16:42:55 UTC | #100

which version on Proxmox are you running?

-------------------------

romeo | 2024-05-18 23:19:26 UTC | #101

`pve-manager/8.2.2/9355359cd7afbae4 (running kernel: 6.8.4-3-pve`)

did your test boot past this point?

-------------------------

0x3639 | 2024-05-19 02:17:48 UTC | #102

Looks like I freeze here.

`pve-manager/8.2.2`

![Screenshot 2024-05-18 at 9.16.47 PM|690x259](upload://wbiYzSIWhgjnDfh4GZV2a7aNT93.png)

-------------------------

romeo | 2024-05-19 03:24:32 UTC | #103

I wonder if it's a BIOS issue

@EovE7Kj any advice? I'll try spend some time tonight to look into it in more detail

-------------------------

0x3639 | 2024-05-19 11:11:45 UTC | #104

I double checked my steps and everything looks correct.  I do have an option to select UEFI but that did not help.  It booted into a `shell` command.  

![Screenshot 2024-05-19 at 5.34.10 AM|690x313](upload://xcYjvSg34wtnpbKkjDRvoWt0WXG.png)
![Screenshot 2024-05-19 at 5.34.17 AM|652x500](upload://bx4cPrF2FgLZ9HVidONNSpvBlQo.png)

-------------------------

romeo | 2024-05-19 11:27:32 UTC | #105

could just not be compatible, it says in the github notes that it's only been verified on QEMU and XEN. Pretty sure ProxMox is based on KVM (although they're pretty much forks of each other)

-------------------------

