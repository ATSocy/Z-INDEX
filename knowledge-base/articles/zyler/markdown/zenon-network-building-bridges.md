Title: Zenon Network: Building Bridges - Zyler9985 - Medium

URL Source: https://medium.com/@Zyler9985/zenon-network-building-bridges-draft-article-for-feedback-4bb2ef8af7eb

Published Time: 2023-05-13T07:20:06.059Z

Markdown Content:
[![Image 9: Zyler9985](https://miro.medium.com/v2/resize:fill:44:44/1*KaL4NYzSxXL6fDt1krksEA.png)](https://medium.com/@Zyler9985?source=post_page---byline--4bb2ef8af7eb--------------------------------)

The future is multi-chain, and ZNNAliens are here to deliver this. A significant milestone in [Zenon Network’s](https://zenon.network/) ecosystem was reached with the release of an audited bridge to Ethereum, complete with a program to incentivise liquidity providers. This article discusses the bridge, the audit, the liquidity program and the benefits this brings to the ecosystem.

Disclaimer: This article is not financial advice and may contain speculation.

![Image 10](https://miro.medium.com/v2/resize:fit:700/0*XL5vnWkI8BeOx6GX)

## The Bridge & Audit

The decentralised bridge to Ethereum which has been released is actually a subset of the NoM Multichain Technology. This infrastructure facilitates interoperability with other networks such as Ethereum (already supported), BNB Chain and later Bitcoin. You can learn more about the plans for Bitcoin interoperability [**here**](https://medium.com/@Zyler9985/zenon-network-alien-plans-for-bitcoin-draft-for-feedback-3bc7e4ac2f84). Because it involves innovative solutions such as the use of TSS technology, some of these future developments wouldn’t strictly classify as a bridge which is why the nomenclature for ‘Portals’ to other networks has been adopted by the Zenon Community.

Despite wide agreement on the value of interoperability, there exists concerns about the security of cross-chain bridges in the crypto space. This is understandable given the spate of exploits which have occurred; some of them high-profile. This is why the bridge was built with security being the core focus alongside its function.

The bridge was designed with multiple layers of security that utilise innovative mechanisms to achieve a synergistic effect. For example if abnormal activity is detected, this triggers a novel delay mechanism — this creates time for other security measures to take effect. These additional measures are partly automated, partly manual and fully designed to neutralise malicious actors. In the case of a running exploit, the final layer of security is a full halting of the bridge, followed by a disaster-recovery protocol facilitated by guardians elected by the DAO. These guardians are technically savvy, have been in Zenon for a long time and are running validator nodes (the QSR burn required to spawn a validator incentivises a longterm view of network prosperity).

Obviously some things can sound good in theory, but are they practical and sound in execution? To this end the ~3k lines of code which comprise the bridge have been exhaustively tested by a comprehensive battery of assessments probing for vulnerabilities. There have been unit-tests, static analysis, fuzzing/property-based testing, mutation testing, internal audits, community audits, manual testing and an external professional audit.

Chainsafe.io was officially contracted to audit the bridge. Community member Sumamu and his team should be proud of the results, because no vulnerabilities were identified. The executive summary explains there were zero issues found of a critical, major or minor nature. The only points of discussion were 16 informational/optimization issues of a benign nature.

## The Liquidity Program

The Orbital Liquidity Program was created to incentivise liquidity pools to form between Zenon and other blockchains. Because of Zenon Network’s unique dual-ledger architecture, there are two tokens which power the network. They are:

1.  **Zenon | ZNN** | Governance & Running infrastructure

2\. **Quasar | QSR** | Gas & Running infrastructure

The wrapped versions of ZNN and QSR will be available on Ethereum to trade with other erc-20 tokens. Swapping from Ethereum to Zenon will be feeless, because Zenon Network is a feeless layer-1 (QSR is not burnt for gas, but is locked for time to generate ‘plasma’ to manage transaction throughput & complexity).

So going from wZNN to ZNN, or from wQSR to QSR, is feeless. But going from ZNN to wZNN, or from QSR to wQSR, does incur an X% fee. The X% fee supports an affiliate marketing system. The current upper limit for this fee is 3%, but it is expected to decrease over time pending the DAO’s decision which takes into account multiple factors. The benefit is that marketers can be given both an incentive to grow Zenon as well as the means to measure their performance in a way which directly relates to price, liquidity and volume — hard and sound metrics to make sure the value added can justify the spend.

To give an example of how this works: Each time a person leaves Zenon’s ecosystem, the 3% fee becomes embedded into the bridge contract. When someone else enters Zenon’s ecosystem via an affiliate link a marketer has generated, the buyer receives a 1% bonus and the marketer receives the other 2%. The 1% and 2% bonuses are supplied 1:1 by the 3% fee, making this a self-sustaining mechanism which also scales infinitely with price. Click **here** to learn more about the affiliate marketing system.

The Orbital Liquidity Program was designed to mitigate risk and provide ample rewards for liquidity providers. It does that in a number of ways which are explained below, but one of the key takeaways is that this is Protocol Level Liquidity — so LP rewards come directly from network emissions. This means the Liquidity Program is governed by the DAO and has the capacity to be readily replenished if need be. Longterm sustainability is therefore a core feature of this Liquidity Program.

The rewards are in both ZNN and QSR, which come from protocol-level emissions at a baseline of 561.6 ZNN/day and 1250 QSR/day. On top of this, there are Bootstrap Rewards to incentivise early participants. Finally, there is also a liquidity multiplier to reward longterm commitment. This begins at 1 month (for a 1X multiplier) and increases in monthly increments up to a maximum of 12 months (for a 12X multiplier).

## Benefits to the Ecosystem

The NoM Multichain Bridge and the Orbital Liquidity Program provide the foundation for Zenon’s interoperability and growth. A number of exciting milestones are upcoming in Zenon’s roadmap, and if this leads to increased interest in Zenon then a reliable DEX solution is essential to facilitate the smooth inflow of capital — and with it builders, marketers and users.

Because it is still a work-in-progress, you may need to browse the [forum](https://forum.zenon.org/latest) to learn about this in-depth. But the NoM Multichain Bridge is more than just a bridge — it is a foundation for further important tech developments.

For example, there are plans for a Layer-2 implementation to bring EVM/WASM compatibility to Zenon Network. The rational for this is so the base layer can remain feeless, simple and efficient; heavy work and transaction bloating will be kept in a separate execution domain. There is discussion of bridging ZNN to this extension chain where the concept of gas fees will be used.

Furthermore, cornerstones of the NoM Multichain tech are MPC (multi-party computation) and TSS (threshold signature schemes). TSS allows a threshold of T participants from a total of N to jointly compute some data. Basically, a specified majority can provide a signature to approve the spending of assets. Thanks to the taproot upgrade to Bitcoin, there are plans to use TSS technology to control native Bitcoin. Again, click **here** to learn more about the plans for Bitcoin interoperability with Zenon.

## Links To Learn More

**The Tutorial** for buying, using the bridge and providing liquidity

[The Main Site](https://zenon.network/)

[The NoM Multi-chain Infrastructure documentation](https://hypercore-team.github.io/)

[Introductory post on the Zenon Community Forum](https://forum.zenon.org/t/welcome-to-the-multiverse-bridging-the-zenon-ecosystem/932)

[The Community AMA](https://www.zenon.info/zenon-network-trustless-bridge-ama/)

[The Liquidity Program Article](https://www.zenon.info/liquidity-bootstrap-provisioning-campaign/)

[The Chainsafe Audit Article](https://www.zenon.info/chainsafe-zenon-network-bridge-audit/)

Don’t hesitate to reach out to the Zenon Community on Twitter, Discord, Telegram or the Forum if you have any questions or would like to get involved. For example, Accelerator-Z is an on-chain funding mechanism to reward contributors who add value to the ecosystem — this applies whether your skills are in tech, marketing or sales.

## Thanks for reading. And remember …

The future is encrypted, it is up to you to decrypt it!
