Thread: bridge-out-of-sync-improvements
0x3639 | 2023-11-24 14:28:59 UTC | #1

In recent weeks Orchestrator Operators have had to "[hard reset](https://forum.hypercore.one/t/orchestrator-update-instructions-to-remove-queues-events-directories/204)" their Orchestrators.  Why is this happening and what are we doing to fix it? 

When Orchestrators get out of sync they sign a different queue of messages.  Each bridge activity requires a minimum number of Orchestrators to sign the TXs (66% + 1).  And when Orchestrators are offline or are signing different TXs where we don't meet the threshold, the TXs fail.  Currently in order to fix this all Orchestrators perform a hard reset.  This deletes the queue of messages to sign and Orchestrators resync a list to sign.  

Why is this happening?

* unconfirmed unwraps persistent disk queue gets corrupted on restart (wip)
* ethereum node ends up on a fork
* ethereum node stops communicating
* ethereum node API gets rate-limited

@sumamu is working on a fix for #1.  Orchestrator operators need to monitor their ETH nodes and make sure they have continuous connectivity.  As the network becomes more popular we as operators need to manage our equipment more actively.  The community expects the bridge to be up and we need to deliver.  

DM me if you are an Orchestrator operator and want instructions on how to more actively manage your equipment.

-------------------------

