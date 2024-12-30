Thread: helios-for-eth-node-on-orchestrator
0x3639 | 2023-12-10 13:37:12 UTC | #1

I'm testing [Helios](https://github.com/a16z/helios) to use as a Trustless ETH client in combination with an Alchemy RPC.  Seems to work as expected.

@sumamu have you tested this and do you think there is any reason we should not do that?  

I really think over time we might consider migrating the Orchestrator to a kubernetes cluster that sets up the binary and nodes for each network.  If we add more networks we need to be running nodes ourselves IMO.    

> Helios is a fully trustless, efficient, and portable Ethereum light client written in Rust.
> 
> Helios converts an untrusted centralized RPC endpoint into a safe unmanipulable local RPC for its users. It syncs in seconds, requires no storage, and is lightweight enough to run on mobile devices.
> 
> The entire size of Helios's binary is 5.3Mb and should be easy to compile into WebAssembly. This makes it a perfect target to embed directly inside wallets and dapps.

-------------------------

