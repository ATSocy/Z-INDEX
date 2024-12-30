Thread: syrius-v0-2-0
CryptoFish | 2024-03-30 11:00:56 UTC | #1

The following pull requests have been created for review for the upcoming Syrius 0.2.0 release and are currently being reviewed by our developers. Once reviewed and accepted they will be merged into the [develop](https://github.com/zenon-network/syrius/tree/develop) branch. A release candidate, accompanied by appropriate test cases, is released to the community for testing once all changes have been merged. A final release will be published when no further issues are found.

It is possible that some PRs won't be merged for reasons stated in the PR itself. These will either be rejected or delayed until further notice.

- [x] https://github.com/zenon-network/syrius/pull/43
- [x] https://github.com/zenon-network/syrius/pull/47
- [x] https://github.com/zenon-network/syrius/pull/48
- [x] https://github.com/zenon-network/syrius/pull/49
- [ ] https://github.com/zenon-network/syrius/pull/50 (rejected)
- [x] https://github.com/zenon-network/syrius/pull/51
- [x] https://github.com/zenon-network/syrius/pull/52
- [x] https://github.com/zenon-network/syrius/pull/53
- [x] https://github.com/zenon-network/syrius/pull/55
- [x] https://github.com/zenon-network/syrius/pull/56
- [x] https://github.com/zenon-network/syrius/pull/58
- [x] https://github.com/zenon-network/syrius/pull/59
- [x] https://github.com/zenon-network/syrius/pull/62
- [x] https://github.com/zenon-network/syrius/pull/63
- [x] https://github.com/zenon-network/syrius/pull/65
- [x] https://github.com/zenon-network/syrius/pull/66
- [x] https://github.com/zenon-network/syrius/pull/68
- [x] https://github.com/zenon-network/syrius/pull/69
- [x] https://github.com/zenon-network/syrius/pull/70
- [x] https://github.com/zenon-network/syrius/pull/72
- [x] https://github.com/zenon-network/syrius/pull/76
- [x] https://github.com/zenon-network/syrius/pull/78
- [x] https://github.com/zenon-network/syrius/pull/82
- [x] https://github.com/zenon-network/syrius/pull/83
- [x] https://github.com/zenon-network/syrius/pull/84
- [x] https://github.com/zenon-network/syrius/pull/88
- [x] https://github.com/zenon-network/syrius/pull/93
- [x] https://github.com/zenon-network/syrius/pull/94
- [x] https://github.com/zenon-network/syrius/pull/95
- [x] https://github.com/zenon-network/syrius/pull/97
- [x] https://github.com/zenon-network/syrius/pull/98
- [x] https://github.com/zenon-network/syrius/pull/100
- [x] https://github.com/zenon-network/syrius/pull/101
- [x] https://github.com/zenon-network/syrius/pull/103
- [x] https://github.com/zenon-network/syrius/pull/104
- [x] https://github.com/zenon-network/syrius/pull/107
- [x] https://github.com/zenon-network/syrius/pull/109
- [x] https://github.com/zenon-network/syrius/pull/112

P.S. although all the PRs were opened by me, the work came together through a collective effort of our developers. Special thanks go out to @aliencoder @vilkris @0x3639 @sol @georgezgeorgez

-------------------------

coinselor | 2024-02-04 11:24:53 UTC | #2

Excellent work, good job team :hugs:!

Would also like to bring to everyone's attention how AZ's phase voting is displayed in syrius, as it might need a slight modification so that it's easier for users to find phases that require their attention. Currently, you need to go hunt for the "phase needs voting" tag.

I think a larger CTA where the usual YES/NO/ABSENT buttons for voting proposals appear would be in order, as well as maybe a filter that works with phases. Voting opened filter does not work for phases.

-------------------------

cagri | 2024-02-05 08:59:25 UTC | #3

Thank you all, guys. You are the ones who make this project better.

-------------------------

CryptoFish | 2024-02-05 12:39:25 UTC | #4

Good point, I'll look into it and make an issue for it.

-------------------------

aliencoder | 2024-02-06 10:16:08 UTC | #5

[quote="CryptoFish, post:1, topic:328"]
[Badges for WalletConnect and notifications by KingGorrin · Pull Request #50 · zenon-network/syrius · GitHub ](https://github.com/zenon-network/syrius/pull/50) (rejected)
[/quote]

@0x3639 liked those changes. I agree we can come up with better icons, but I wanted to differentiate between Plasma and the status of the node.

-------------------------

CryptoFish | 2024-02-29 11:07:33 UTC | #6

@coinselor please look at [PR](https://github.com/zenon-network/syrius/pull/68) for a solution.

-------------------------

CryptoFish | 2024-03-07 15:57:41 UTC | #7

We'd like the community to help us test this release. We do this through one or more test rounds. For each test round, a release candidate is issued and testing takes place for a period of time. After each round, any errors found are resolved and a new test round will be announced until no more errors are found.

A number of test cases have been set up to help testers get a grip on what to test. The test cases contain scenarios that try to cover the underlying code changes. The test cases do not cover the code changes 100% and therefore there are situations that are not covered by them.

The following tests have been setup:
- [auto-receive](https://github.com/zenon-network/syrius/tree/release-0.2.0/tests/auto-receive/)
- [community-nodes](https://github.com/zenon-network/syrius/tree/release-0.2.0/tests/community-nodes)
- [ledger](https://github.com/zenon-network/syrius/tree/release-0.2.0/tests/ledger)
- [walletconnect](https://github.com/zenon-network/syrius/tree/release-0.2.0/tests/walletconnect)

When creating a test-run, copy a test and fill in the following information:
- Syrius version you're using to the test
- Environment
- Date of the test
- Name or handle of the tester

The result of a test case is either `PASS` or `FAIL`. Leave it blank if for whatever reason you're not able to test the case. Submit the results of your test-run on the forum. The test-runs give us a good idea of what has been tested.

The reason and details of a `FAIL` test case must be submitted as an issue on the [Syrius](https://github.com/zenon-network/syrius/issues) repo. See below for more information.


## Bug bounties

Testers who find bugs are rewarded through the bug bounty program. Anyone can participate, but in order to qualify for a reward, submitted bugs must meet a number of requirements.

1. Bugs must be submitted on GitHub under the [Syrius](https://github.com/zenon-network/syrius/issues) repository as issues
1. Bugs must have a clear description (a template has been setup to help you fill in the necessary information)
1. Bugs that cannot be reproduced will be ignored
1. The issue must contain a Zenon address to qualify for a reward
1. When duplicates occur, we only award the first report that was received (provided that it can be fully reproduced)

Bugs will be divided into three categories, namely: Low, Medium, High. All bugs for Syrius fall between 0.1 and 3.9 CVSS and the rewards are set accordingly. The following table shows the rewards per category.

| Severity | Amount | Description |
| -- | -- | -- |
| Low | 10 ZNN | Bug won't result in any noticeable breakdown of the system |
| Medium | 25 ZNN | Results in some unexpected or undesired behavior, but not enough to disrupt system function |
| High | 50 ZNN | Bugs capable of collapsing large parts of the system |

A total amount of 500 ZNN has been allocated for the bug bounty program. No further rewards will be paid once it is depleted. The bug bounty fund will remain untouched when no bugs are found, to be used for future releases.


## Testnet

Do not test with live funds, but connect Syrius to a testnet using the following node and chain id. Use the faucet to receive the necessary test funds.

ChainID: 3
Node: wss://syrius-testnet.zenon.community:443
Faucet: https://t.me/znn_faucet_bot


## Test rounds
 
When testing begins, a round of testing will be announced in a separate post. The post contains instructions for downloading the release candidate and all test-runs are collected in that post until the end of the round.

This will be repeated until the release is deemed ready for publication.

-------------------------

aliencoder | 2024-03-07 18:29:31 UTC | #8

[quote="CryptoFish, post:7, topic:328"]
A total amount of 500 ZNN has been allocated for the bug bounty program
[/quote]

Brilliant idea to incentivize testing.

-------------------------

CryptoFish | 2024-03-31 12:07:29 UTC | #9

The testing phase has been completed. I would like to thank everyone who helped for their contribution. Testing is an important part of software development that is often skipped. A total of 19 additional points were completed during this test period. I will prepare a separate post with the results of the bounty program. The rewards will be released together with the AZ payment.

During development, a collaboration emerged between Dr. Greenthumb and me. I initially planned to make a promo video for the release, but I quickly discovered that there are community members who are much better equipped for that task. @Dr.GreenThumb did an amazing job showcasing the new features in his video, it really is the icing on the cake. If the community does not mind I would like to reserve 200 ZNN from the remaining bug bounty program for his work on the video.

A tweet will be made once the release is ready.

-------------------------

CryptoFish | 2024-03-31 12:16:57 UTC | #10

# Bug bountry program rewards

@theta-aquarii 
- 25 ZNN for issue https://github.com/zenon-network/syrius/issues/74

@0x3639 
- 25 ZNN for issue https://github.com/zenon-network/syrius/issues/87
- 10 ZNN for issue https://github.com/zenon-network/syrius/issues/86
- 10 ZNN for issue https://github.com/zenon-network/syrius/issues/99

@coinselor 
- 10 ZNN for issue https://github.com/zenon-network/syrius/issues/85
- 25 ZNN for issue https://github.com/zenon-network/syrius/issues/91
- 10 ZNN for issue https://github.com/zenon-network/syrius/pull/104
- 10 ZNN for issue https://github.com/zenon-network/syrius/pull/106

EverlastingOS
- 10 ZNN for issue https://github.com/zenon-network/syrius/issues/90
- 10 ZNN for issue https://github.com/zenon-network/syrius/issues/108

-------------------------

aliencoder | 2024-03-31 15:27:18 UTC | #11

[quote="CryptoFish, post:1, topic:328"]
[Badges for WalletConnect and notifications by KingGorrin · Pull Request #50 · zenon-network/syrius · GitHub ](https://github.com/zenon-network/syrius/pull/50) (rejected)
[/quote]

I would include this UX improvement for v0.2.0 release.

-------------------------

coinselor | 2024-03-31 15:43:43 UTC | #12

[quote="CryptoFish, post:9, topic:328"]
If the community does not mind I would like to reserve 200 ZNN from the remaining bug bounty program for his work on the video.
[/quote]

No objections here. He did an amazing job.

Thank you for raising the standards for releases moving forward: clear objectives and descriptions, community involvement, constant communication, the whole deal.

Top A. (alien)

-------------------------

0x3639 | 2024-03-31 22:00:57 UTC | #13

[quote="CryptoFish, post:9, topic:328"]
@Dr.GreenThumb did an amazing job showcasing the new features in his video, it really is the icing on the cake. If the community does not mind I would like to reserve 200 ZNN from the remaining bug bounty program for his work on the video.
[/quote]

Awesome!!  Well deserved.

-------------------------

CryptoFish | 2024-04-02 12:42:38 UTC | #14

The [tweet](https://twitter.com/Zenon_Network/status/1775137024770777200) is out, the release is official.

-------------------------

0x3639 | 2024-04-02 20:16:10 UTC | #15

great work to all those involved.

-------------------------

ImperiumZNN | 2024-04-03 16:56:27 UTC | #16

I'd already like to thank you for all the work that's been done! It's really incredible. I'd just like to add one improvement, maybe for the next update (sorry I'm a bit late), and that's to put the revocation window at the top of the Sentinel section, like the "undelegate" in the Pillars section. What do you think?

-------------------------

CryptoFish | 2024-04-12 14:25:19 UTC | #17

Good idea, please submit this as an issue on the repo. This way it can be picked up for the next release.

-------------------------

CryptoFish | 2024-04-12 14:29:07 UTC | #18

[Syrius v0.2.1-alphanet](https://github.com/zenon-network/syrius/releases/tag/v0.2.1-alphanet) has been released. It contains a hotfix  to tackle issue [#115](https://github.com/zenon-network/syrius/issues/115).

-------------------------

Bzed | 2024-04-12 16:15:33 UTC | #19

Thank you for that.

-------------------------

