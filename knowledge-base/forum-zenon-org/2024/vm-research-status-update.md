Thread: vm-research-status-update
Dumeril | 2023-02-08 22:34:53 UTC | #1

This is to inform the community about the status of the research on vm implementations by Jeron and I, under the az umbrella. 

In a nutshell, I’ve personally decided to stop working on zenon, and that includes this project. I’ve had a good time working with jeron on this topic, and I hope he’ll be able to continue what we began with the support of the community. Mostly due to other obligations, we hadn’t been as productive as we wished; nonetheless I think we made some good progress. We were close to publishing another update a few weeks back, but that never happened. From the technical side, this would have mostly consisted of a detailed representation of the current consensus mechanisms. 

More important though, we had decided to divert the focus of the research a bit, as we realized that the task is overwhelming for just two people. So the decision was to take a shortcut on the vm selection and proposal process and focus on wasm going forward. The overwhelming consensus in the industry seems to be that this is the de-facto state of the art currently, and the best we could have done anyway would have been to replicate existing sources. 

There’s one exception though from my point of view which I wanted to look at on greater detail, and to whoever is going to work on this in the future, I want to mention sol vm. Concerning sol, we all know that it’s an unstable chain and it needs to be verified that the vm is not the culprit here. But then, it has one property which lead me to think that it might be worth a deeper look: It is optimized for account based chains like zenon and a multi-threaded implementation. 
In contrast to wasm, which was intended for browser environments and thus is single-threaded. There’s research (probably biased of course) that indicates gigantic performance gains for contracts in sol vm over wasm. 

Anyway, a wasm implementation would be much easier and faster to achieve most likely, since there’s a lot of projects already going that route which would work as templates. Don’t be fooled into thinking that having the runtime would automatically enable smart contracts in all languages that potentially can compile to wasm though- there’s a bridging component/library needed for each single language you want to support. Nevertheless it would be an easier task most likely, than doing the same for another vm like sol‘s. 

This is surely a bit hand-waving as conclusion for my contribution to the project, but it was something I didn’t want to be left unmentioned as an intermediate result of my work. 

Good luck everyone, see you around

-------------------------

zyler9985 | 2022-10-08 13:14:23 UTC | #2

Speaking on the behalf of myself and a few people I've spoken to, thank you for your contributions Dumeril and you will be missed. We hope you could leave the door open to maybe return to this project or another one at some point in the future, who knows what can happen, but know you are always welcome.  All the best with things!

-------------------------

Dumeril | 2022-10-08 15:51:16 UTC | #3

Thank you, I appreciate it

-------------------------

0x3639 | 2022-10-08 17:24:00 UTC | #4

Thank you for the update and everything you've done for the project.  The aliens will miss you and hope you return before price goes up too much!!!  Until the... some AI art to say good luck!  

![2022-10-08 12.22.30|666x500](upload://eIoYw1tNolyf3KYETm0lJbpXvsE.jpeg)

-------------------------

Jeron | 2022-10-08 22:26:26 UTC | #5

As Dumeril mentioned above he is no longer working on the project. 

Tbh I personally lack the technical depth to be able to complete the project solo. If someone is interested in building on what we have done already, please reach out. Hopefully the work to date is of some use to the community as we will no doubt be looking to implement smart contracts in the future. 

The takeaway from reviewing other projects is that wasm is the logical path forward for a generic implementation. Its not to say there aren't better approaches, but it seems to be a solid approach and is probably also one of the more straightforward paths. If we wish to pursue something more novel like the mulitthreading Dumeril mentioned, we would really benefit from input from true domain experts in this space.

Its very encouraging to see all the building going on within the community. I still see a smart contract VM implementaion as critical for early growth annd adoption of the network, even before implementing scaling upgrades. Let's see what Phase 1 brings. 

For any that are interested, the current project outputs are located [here](https://docs.zenon.org/zenon-docs/vm-research-project/vm-smart-contract-concepts).

I won't be pursuing any funding for the work to date, as I don't think we made enough progress against the objective. Hopefully the work is still of some use.

-------------------------

