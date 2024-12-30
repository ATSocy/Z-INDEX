Thread: wp1-governance-contract-pointing-1-3
georgezgeorgez | 2024-10-23 20:33:53 UTC | #1

Round 1 of 3
Please see the following work package and discuss/vote on relative value of the Governance Contract work of [HC1: HyperQube SIG WP1 - Zenon Wiki ](https://zenon.wiki/index.php/HC1:_HyperQube_SIG_WP1)

The Governance Contract work is comprised of individual work items which we want to assign points to:

|Work Item|Points|
| --- | --- |
|Specification|X|
|Implementation|X|
|Testing (Manual or Automated)|X|
|Documentation|X|
|Explorer Updates|X|
|Golang SDK|X|
|Dart SDK|X|
|Javascript SDK|X|
|CLI Tooling|X|
|Future/Bonus|X|


As a baseline, the work package starts with 10k points allocated for pillar momentums and votes and 10k points for the work package coordinator, for a total of 20k points.

Round 1 happens during the planning phase.
Round 2 happens as the work is in progress.
Round 3 happens once the work is done.

-------------------------

georgezgeorgez | 2024-10-23 20:31:02 UTC | #2

I will aim for 30k points for the governance contract work

|Work Item|Points| Rationale|
| --- | --- | ---|
|Specification| 3000 | 
|Implementation| 7000 | 
|Testing (Manual or Automated)| 1000 | 1000 if manual, 5000 if automated using something like k6. Would also likely seek to increase total AZ if automated tests result in reusable framework
|Documentation|2000 |
|Explorer Updates |1500|
|Golang SDK|2000|
|Dart SDK|2000|
|Javascript SDK|2000|
|CLI Tooling|1500|
|Future/Bonus|8000|

-------------------------

vilkris | 2024-10-24 06:11:07 UTC | #3

Also aiming for 30k total.
|Work Item|Points|Rationale|
| --- | --- | --- |
|Specification|4000||
|Implementation|10000|Assuming this includes proper peer review|
|Testing (Manual)|2000||
|Testing (Automated)|0|Maybe some other WP is better suited for this endeavor|
|Documentation|1000||
|Explorer Updates|1500||
|Golang SDK|2000||
|Dart SDK|2000||
|Javascript SDK|500|Nice to have, but not sure how much actual usage|
|CLI Tooling|1500||
|Future/Bonus|5500||

Apparently no syrius development will be included in this WP?

-------------------------

georgezgeorgez | 2024-10-24 18:48:19 UTC | #4

@vilkris the scope of WP1 is getting the governance embedded onto hyperqube_z. it does not include getting it onto mainnet or syrius changes.

We will likely want to try out the governance for a bit on hyperqube_z first before recommending it for mainnet. Mainnet also has some hurdles like spork creation control, which we may have to hardfork away from the current address. My thought is that Syrius development probably isn't appropriate until a contract (which may have been change/iterated on) is scheduled for mainnet.

We will have a future work package of 
* getting gov embedded onto mainnet (hardfork if needed)
* automated end to end testing if we don't include it in this one
* syrius changes

-------------------------

coinselor | 2024-10-24 19:09:53 UTC | #5


|Work Item|Points|Rationale|
| --- | --- | --- |
|Specification|3000||
|Implementation|9500||
|Testing (Manual)|2000||
|Documentation|1000||
|Explorer Updates|2000||
|Golang SDK|1500||
|Dart SDK|1500||
|Javascript SDK|1500||
|CLI Tooling|1500||
|Future/Bonus|6500||

-------------------------

SultanOfStaking | 2024-10-25 00:23:52 UTC | #6

|Work Item | Points | Rationale|
|--- | --- | ---|
|Specification | 3000 | |
|Implementation | 10000 | |
|Testing (Manual) | 2000 | Would pull from bonus if automated|
|Documentation | 1000 | |
|Explorer Updates | 2000 | |
|Golang SDK | 1500 | |
|Dart SDK | 1500 | |
|Javascript SDK | 1500 | |
|CLI Tooling | 1500 | |
|Future/Bonus | 5000 | |

-------------------------

vilkris | 2024-10-25 10:32:17 UTC | #7

Okay makes sense. Thanks for the explanation.

-------------------------

0x3639 | 2024-10-25 13:47:40 UTC | #8

|Work Item|Points|Rationale|
| --- | --- | --- |
|Specification|3000||
|Implementation|9500||
|Testing (Manual)|2000||
|Documentation|1000||
|Explorer Updates|2000||
|Golang SDK|1500||
|Dart SDK|1500||
|Javascript SDK|1500||
|CLI Tooling|1500||
|Future/Bonus|6500|

-------------------------

sugoibtc | 2024-10-25 15:02:24 UTC | #9

|Work Item|Points|Rationale|
|---|---|---|
|Specification|3000||
|Implementation|9500||
|Testing (Manual)|2000||
|Documentation|1000||
|Explorer Updates|2000||
|Golang SDK|1500||
|Dart SDK|1500||
|Javascript SDK|1500||
|CLI Tooling|1500||
|Future/Bonus|6500||

-------------------------

edgepillar | 2024-10-25 16:11:08 UTC | #10

|Work Item |Points |Rationale|
|---|---|---|
|Specification |3000 ||
|Implementation |9500 ||
|Testing (Manual) |2000 ||
|Documentation |1000 ||
|Explorer Updates |2000 ||
|Golang SDK |1500 ||
|Dart SDK |1500 ||
|Javascript SDK |1500 ||
|CLI Tooling |1500 ||
|Future/Bonus |6500 ||

-------------------------

cap | 2024-10-25 20:13:06 UTC | #11

|Work Item|Points|Rationale|
| --- | --- | --- |
|Specification|3000||
|Implementation|9500||
|Testing (Manual)|2000||
|Documentation|2000||
|Explorer Updates|2000||
|Golang SDK|1500||
|Dart SDK|1500||
|Javascript SDK|1500||
|CLI Tooling|1500||
|Future/Bonus|5000||

-------------------------

Stark | 2024-10-25 21:12:50 UTC | #12

|Work Item|Points|Rationale|
| --- | --- | --- |
|Specification|3000||
|Implementation|9500||
|Testing (Manual)|2000||
|Documentation|2000||
|Explorer Updates|2000||
|Golang SDK|1500||
|Dart SDK|1500||
|Javascript SDK|1500||
|CLI Tooling|1500||
|Future/Bonus|5000||

-------------------------

shaimo | 2024-10-26 16:12:37 UTC | #13

|Work Item|Points|Rationale|
| --- | --- | --- |
|Specification|3000||
|Implementation|10000||
|Testing (Manual)|2500||
|Documentation|1500||
|Explorer Updates|2000||
|Golang SDK|1500||
|Dart SDK|1500||
|Javascript SDK|1500||
|CLI Tooling|1500||
|Future/Bonus|5000|

-------------------------

Bzed | 2024-10-26 20:30:38 UTC | #14

|Work Item|Points|Rationale|
|---|---|---|
|Specification|5000||
|Implementation|7500||
|Testing |2500||
|Documentation|3000||
|Explorer Updates|1000||
|Golang SDK|1000||
|Dart SDK|1000||
|Javascript SDK|1000||
|CLI Tooling|1000||
|Future/Bonus|7000||

-------------------------

nexuspillar | 2024-10-27 09:08:51 UTC | #15

|Work Item|Points|Rationale|
| --- | --- | --- |
|Specification|4000||
|Implementation|10000||
|Testing (Manual)|2000||
|Documentation|1500||
|Explorer Updates|2000||
|Golang SDK|1500||
|Dart SDK|1500||
|Javascript SDK|500||
|CLI Tooling|2000||
|Future/Bonus|5000||

-------------------------

digitalSloth | 2024-10-27 19:55:22 UTC | #16

|Work Item|Points|Rationale|
| --- | --- | --- |
|Specification|3500||
|Implementation|10000||
|Testing (Manual)|2000||
|Documentation|1500||
|Explorer Updates|2000||
|Golang SDK|1500||
|Dart SDK|1500||
|Javascript SDK|0||
|CLI Tooling|1500||
|Future/Bonus|6500||

Reason for 0 for the JS SDK is that either the JS or TypeScript SDKs requires a lot of work to bring them up to date which I believe would be better as a separate task outside of this work package.

-------------------------

Asgardians-Pillar | 2024-10-28 16:33:00 UTC | #17

Work Item Points Rationale Specification 3000 Implementation 9500 Testing (Manual) 2000 Documentation 1000 Explorer Updates 2000 Golang SDK 1500 Dart SDK 1500 Javascript SDK 1500 CLI Tooling 1500 Future/Bonus 6500

-------------------------

Zashounet | 2024-10-28 17:48:35 UTC | #18

| Work Item            | Points | |
|----------------------|--------|-----------|
| Specification        | 3000  |           |
| Implementation       | 9000  |           |
| Testing (Manual)     | 2000   |           |
| Documentation        | 1500   |           |
| Explorer Updates     | 1500   |           |
| Golang SDK           | 1500   |           |
| Dart SDK             | 1500   |           |
| Javascript SDK       | 1500     |           |
| CLI Tooling          | 1500   |           |
| Future/Bonus         | 7000   |           |

-------------------------

tapwoot | 2024-10-29 21:28:20 UTC | #19

|Work Item|Points|Rationale|
| --- | --- | --- |
|Specification|3000||
|Implementation|10000||
|Testing (Manual)|2500||
|Documentation|1500||
|Explorer Updates|2000||
|Golang SDK|1500||
|Dart SDK|1500||
|Javascript SDK|1500||
|CLI Tooling|1500||
|Future/Bonus|5000||

-------------------------

georgezgeorgez | 2024-11-04 03:25:57 UTC | #20



-------------------------

