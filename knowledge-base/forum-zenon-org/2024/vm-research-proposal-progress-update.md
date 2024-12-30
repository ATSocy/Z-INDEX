Thread: vm-research-proposal-progress-update
Jeron | 2023-02-08 22:34:53 UTC | #1

This is the first update for the community from our ongoing research proposal on potential VM implementations.

Our current workload is lower than expected for various reasons:

* @Dumeril: ~50h
* @Jeron: ~25h

Under the project proposal, we proposed two initial phases: an external analysis studying existing virtual machine implementations in other well known blockchains, and an internal analysis, studying the existing znnd (go-zenon) code.

A third phase where we would propose an VM implementation would follow phases one and two.

At present, we are part way through phases one and two and wanted to begin sharing the progress to date with the community for feedback and comment.

We will host the project outputs in the [gitbook](https://docs.zenon.org/zenon-docs/) maintained by @mehowbrainz.
 
The VM Research Project gitbook can be found [here](https://docs.zenon.org/zenon-docs/vm-research-project/vm-smart-contract-concepts).

**External Analysis**

See work to date [here](https://docs.zenon.org/zenon-docs/vm-research-project/external-analysis).

For the external phase, the top 20 blockchain projects by marketcap were reviewed and blockchains with smart contract functionality were analysed with respect to their smart contract VM implementations. A number of additional L1 projects outside of the top 20 were also included for interest. We have begun to summarize the collated information in gitbook. We have not yet performed a highly detailed analysis on any particular project. The first step was just to get a good overview of the landscape. EVM and Wasm-based implementations are the two most commonly used VMs, with a handful of custom approaches also used. The list of projects analysed will likely expand from here and we are also planning to do some deeper analysis on key projects.

**Internal Analysis**

See [here](https://docs.zenon.org/zenon-docs/vm-research-project/internal-analysis), where we begin to present the work to date.

Regarding the analysis and description of the current implementation, we tried to focus on the current embedded VM and how its execution results are included in the chain state.

It turns out it is impossible to understand this in an isolated context, so it was necessary to look at various aspects of the implementation, including:

* Node discovery, synchronization and the p2p protocol
* Local state management and handling using the leveldb interface
* Implementation differences between regular node and pillar node
* General architecture of a node (i.e., how are different software components connected and communicating, where and how is control flow organized etc.)
* Consensus mechanisms

The result is a collection of loose notes, graphics and diagrams on various aspects of NoM and [some supporting code](https://github.com/dumeriz/cl-nom) for leveldb interaction. There’s probably a lot of knowledge hidden in these notes that would be relevant and interesting for the community, so we’re aiming to process as much as possible of these into technical documentation in the next stages. Initially we’ve added a diagram describing the procedure leading to state updates for the embedded smart contracts, as well as a [page](https://docs.zenon.org/zenon-docs/vm-research-project/internal-analysis/database-access-handling) with initial information regarding the usage of databases in NoM.

We hope this approach is in the best interest of other developers and the community. We want to encourage technical discussions about the current implementation, with feedback, questions and contribution from every level of understanding welcome. To make the documentation useful and clear for most people, we rely on input from the community. And of course the hope is still that (1) the team or Kaine joins these discussions, (2) other community members feel inspired to join us. We also hope that this leads to a community carried initiative resulting in an actual implementation in the end.

**Next steps**

With regards to go-zenon, our focus for the next stages will be:

* Supplement the description of the embedded contract execution process with context (when is it triggered; what happens with the generated blocks etc.);
* Describe block propagation, the existing consensus mechanism and which network actors are involved in it;
* Description of account chain handling and the block lattice implementation.

With regards to other implementations, we will proceed as follows:

* Continue to edit and complete the comparison of VMs for other chains;
* Focus on the technical side of certain implementations, to see how certain aspects are handled (e.g. transaction pricing, fault handling, spam prevention etc.). We’ll mostly look at WASM (in eos?) and EVM here.

We’d like to mention that we tried to get the team involved as early as possible. Specifically, we asked (mid-June)

1. If there’s a specific alternative to Wasm that they would like us to look at, apart from the obvious mainstream runtimes like EVM.
2. Whether Wasm was what they had in mind when they initially described the concept of Unikernels, as conceptually, this looks very close.

Unfortunately, neither Kaine nor the team replied to us or Sigli. We hope that they are more inclined to comment on the technical output we generate and correct or enhance it where possible.

We welcome any feedback and questions from the community. We will provide further updates as we continue to make progress.

-------------------------

romeo | 2022-08-10 12:38:31 UTC | #2

I've read through this twice now and found it quite informative - please keep us updated with your progress. I'm hoping it leads to a clear way forward regarding the SC mechanism

-------------------------

