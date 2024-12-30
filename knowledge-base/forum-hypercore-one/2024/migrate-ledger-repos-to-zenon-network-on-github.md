Thread: migrate-ledger-repos-to-zenon-network-on-github
0x3639 | 2024-02-22 09:13:47 UTC | #1

@CryptoFish is making good progress on the ledger AZ.  Given the importance and potential security concerns, he is recommending that we migrate the ledger repos to the official Zenon Network repo - https://github.com/zenon-network.  

There are 3 repos in question:

- [x] https://github.com/hypercore-one/ledger_ffi_rs 
- [x] https://github.com/hypercore-one/znn_ledger_dart 
- [ ] https://github.com/hypercore-one/ledger-app-zenon // needs to be migrated eventually, but doesn't have priority right now.

Separately, @CryptoFish was asking about what to do with the following repos he maintains at https://github.com/hypercore-one

- [ ] https://github.com/hypercore-one/znn_sdk_csharp 
- [ ] https://github.com/hypercore-one/znn_ledger_csharp
- [ ] https://github.com/hypercore-one/znn_cli_csharp

## Questions

1) Do any developers object to moving the three ledger repos to /zenon-network?
2) I would like to propose the following maintainers to be consistent with zenon_sdk_dart: @aliencoder @CryptoFish @sol @vilkris Does anyone object or want to add maintainers?  
3) My recommendation was to leave the sdk_csharp and cli_csharp repos at HC1 for the time being, but wanted to make sure everyone had an opportunity to discuss that.  Any thoughts on this?

-------------------------

sol | 2023-12-13 02:42:26 UTC | #2

1. No objection -- the code is well written, documented, and integrates with several other repos under that org.
2. I don't have any nominations at this time
3. I'm undecided. Is CryptoFish asking to migrate these to zenon_network?

-------------------------

CryptoFish | 2023-12-13 06:49:31 UTC | #3

[quote="sol, post:2, topic:274"]
I’m undecided. Is CryptoFish asking to migrate these to zenon_network?
[/quote]

Yes, indeed. I've asked 0x because I cannot migrate the repos. I think it is better if all related repos reside under the zenon-network org. Together with the sdk and cli.

The same counts for the ledger-app-zenon repo. We haven't received an official review yet from Ledger, but I can imagine they would like some kind of prove it belongs to zenon-network.
I don't think it matters much for the developer mode, but eventually I think it should be officially recognised by zenon-network.
Moving it now only confuses things, so I propose to wait for a reply from Ledger first, before moving the ledger-app-zenon repo.

-------------------------

aliencoder | 2023-12-13 09:38:39 UTC | #4

I fully support @CryptoFish.

-------------------------

0x3639 | 2023-12-13 14:13:02 UTC | #5

2 posts were split to a new topic: [Is ledger is monitoring our signing activities?](/t/is-ledger-is-monitoring-our-signing-activities/277)

-------------------------

vilkris | 2023-12-14 08:51:11 UTC | #6

I'm fine with moving all six repos to zenon network. They are all well maintained and documented so I think zenon network is a suitable home for them.

-------------------------

CryptoFish | 2023-12-16 11:51:53 UTC | #7

I propose to wait for @sol to finish his Nano S+ tests and migrate the [ledger_ffi_rs](https://github.com/hypercore-one/ledger_ffi_rs) and [znn_ledger_dart](https://github.com/hypercore-one/znn_ledger_dart) repos. This will put all the dart sdk/cli related repos in once place, before release of v0.0.6.

The other repos can wait for the moment.

-------------------------

0x3639 | 2023-12-16 12:16:11 UTC | #8

Cool - Let me know when we are ready and I'll start the migration.

-------------------------

CryptoFish | 2024-02-22 09:15:28 UTC | #9

The [ledger_ffi_rs](https://github.com/zenon-network/ledger_ffi_rs) and [znn_ledger_dart](https://github.com/zenon-network/znn_ledger_dart) repositories have been successfully migrated to the [zenon-network](https://github.com/zenon-network) organization.

-------------------------

CryptoFish | 2024-07-11 07:45:29 UTC | #10

[quote="CryptoFish, post:9, topic:274, full:true"]
The [ledger_ffi_rs](https://github.com/zenon-network/ledger_ffi_rs) and [znn_ledger_dart](https://github.com/zenon-network/znn_ledger_dart) repositories have been successfully migrated to the [zenon-network](https://github.com/zenon-network) organization.
[/quote]

This time it's for real.

This [PR](https://github.com/zenon-network/znn_cli_dart/pull/9) has been opened on the [znn_cli_dart](https://github.com/zenon-network/znn_cli_dart) repository to implement the changes.

This [PR](https://github.com/zenon-network/syrius/pull/121) has already been merged into the `develop` branch on the [znn_cli_dart](https://github.com/zenon-network/syrius) repository and will be implemented in the upcoming release.

-------------------------

