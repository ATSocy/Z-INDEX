Thread: bridge-analytics
sol | 2024-03-27 15:19:48 UTC | #1

I noticed [some code](https://github.com/DexterLabZ/bridge-dapp/pull/1/files#diff-04c4adf9cf321b01469bb7d2cf7a1cadf6cf6bced5bb4a0dd5e706701c869278R1276) was merged into the Bridge webapp repository earlier today and I wanted to get the community's opinion about this direction of development.

It appears that the webapp will emit an event to Google Tag Manager every time someone unwraps ZNN. The event includes the amount that is being unwrapped and bridged back to NoM, and I presume it can be linked to UTMs or attribute.zenon.org campaigns.

I'd like to ask the ZenonORG team:
- Are there any implications to user privacy? Using your funnels, is it possible for your organization to link web2 and web3 identities?
- If not, will the answer change with any future updates to the bridge?
- Will the data be publicly available?

To the community:
- Do you support the changes made to the bridge webapp?
- Would you prefer a neutral alternative that doesn't include analytics?

One point I'd like to make is that https://bridge.zenon.network -- the official bridge link -- redirects to https://bridge.mainnet.zenon.community/, which is controlled by a small group of people without any oversight.

I have no problem with the introduction of analytics on the .community domain, but I'm raising this as a concern because it involves .network.

-------------------------

0x3639 | 2023-12-01 18:50:29 UTC | #2

Here's an idea.  What if [https://bridge.zenon.network](https://bridge.zenon.network/) hosted it's own bridge and that became the "community" bridge with metrics that are available to everyone.  JohnZ (who rugged us) added posthog.  Maybe we update that.  

Then, if someone wants to run their own bridge they can fork it and add analytics they see fit.  The community can support the bridge at https://bridge.zenon.network and anyone who wants to fork and run their own, can support their users directly.  

I can tell you from first hand experience, there is a LOT of effort that goes into supporting users of the bridge.

-------------------------

mehowbrainz | 2023-12-01 19:48:26 UTC | #3

[quote="sol, post:1, topic:1722"]
Are there any implications to user privacy? Using your funnels, is it possible for your organization to link web2 and web3 identities?
[/quote]

The Attribute GTM tags have the anonymizeIp parameter set to true. You can verify and confirm that in your browser's Inspector tools.

Setting the `anonymizeIp` parameter to `true` in Google Analytics provides several benefits, primarily related to user privacy and compliance with data protection regulations:

1. Enhanced User Privacy
- IP Address Anonymization: When `anonymizeIp` is set to `true`, Google Analytics anonymizes the IP addresses of your website's visitors. This is done by removing the last octet of the IP address prior to its storage and processing. 
- Reduced Personally Identifiable Information: An anonymized IP address is less likely to be considered personally identifiable information (PII), which is crucial in protecting the privacy of your website visitors.

2. Compliance with Data Protection Regulations
- General Data Protection Regulation (GDPR): For websites with visitors from the European Union (EU), complying with GDPR is essential. GDPR emphasizes the privacy and protection of personal data. Anonymizing IP addresses is a step towards compliance.
- Other Privacy Laws: Various other data protection laws and regulations around the world, like the California Consumer Privacy Act (CCPA) in the U.S., also necessitate stringent data handling practices. Anonymizing IP addresses helps in adhering to these laws.

3. Building User Trust
- Transparency and Trust: By actively reducing the amount of personal data collected, you signal to your users that you respect their privacy. This can enhance trust in your brand or website.
- **Privacy-Focused Audience**: As users become more privacy-conscious, they tend to favor businesses and websites that take measures to protect their data.

4. Minimal Impact on Data Analysis
- Negligible Effect on Analytics: Anonymizing IP addresses has a minimal impact on the quality and usefulness of the data collected by Google Analytics. You can still gain valuable insights into user behavior, traffic sources, and other key metrics without the exact IP address.
- Geolocation Data: While detailed geolocation accuracy might be slightly reduced, Google Analytics still provides an approximate location of the user, which is often sufficient for most analytical purposes.

5. Potential Reduction in Legal Risks
- Lower Legal Exposure: By reducing the amount of PII collected, you also potentially lower the risk of legal complications related to data breaches or non-compliance with privacy laws.

In summary, setting `anonymizeIp` to `true` in Google Analytics is a proactive step towards enhancing user privacy, ensuring compliance with various data protection laws, building trust with your audience, and minimizing legal risks, all while maintaining the integrity and usefulness of your analytics data.

-------------------------

mehowbrainz | 2023-12-01 19:42:55 UTC | #4

[quote="sol, post:1, topic:1722"]
Will the data be publicly available?
[/quote]

We publish analytics data on Attribute dashboards, however due to limitations with dimensions/APIs, we can only pull a certain amount of data. With the new improvements to with our server-side streaming of GA data, there may be a possibility to showcase even more. We can even use other tools like Looker Studio to create other dashboards, directly streaming data from the GA account.

-------------------------

mehowbrainz | 2023-12-01 19:46:03 UTC | #5

The event was added today as a measure to go full circle on #HyperGrowth initiatives. Attribute links will be able to maintain a connection between zenon.org (or any other funnel domains in the future) to the NoM bridge, and ultimately allow any marketer to prove that his marketing campaign via his Attribute link, was responsible for a specific wZNN > ZNN swap.

Eventually this can develop to track engagement into the syrius wallet by tracking events triggered on landing pages (nothing in syrius wallet).

-------------------------

mehowbrainz | 2023-12-01 19:45:20 UTC | #6

Note that the integration isn't completed yet, we're still debugging on the staging bridge site.

-------------------------

aliencoder | 2023-12-01 19:45:48 UTC | #7

[quote="sol, post:1, topic:1722"]
* Would you prefer a neutral alternative that doesn’t include analytics?
[/quote]

Yes, I prefer no analytics at least for the community/network TLD.

@mehowbrainz is it hard to setup https://bridge.zenon.org with analytics?

-------------------------

cryptocheshire | 2023-12-01 20:02:09 UTC | #8

Whats the reasoning if its fully anonymized?

-------------------------

mehowbrainz | 2023-12-01 19:57:28 UTC | #9

@sumamu and I are discussing the idea of having 2 versions, one with analytics enabled and the other without. We understand the community would want both.

-------------------------

mehowbrainz | 2023-12-02 00:14:44 UTC | #10

[quote="sol, post:1, topic:1722"]
The event includes the amount that is being unwrapped and bridged back to NoM, and I presume it can be linked to UTMs or [attribute.zenon.org](http://attribute.zenon.org) campaigns.
[/quote]

It can be linked to the marketer who referred the wZNN > ZNN swap, but we do not pass any information on which address actually made the swap. Thought I'd clarify this since the word "linked" can be misleading if you don't understand the context the utm parameter is being used in.

-------------------------

mehowbrainz | 2023-12-02 00:17:48 UTC | #11

So to summarize:

1) We don't know which IP address made the swap / quantity because we anonymizeIp
2) We don't pass swapper zenon address information, only the referrer's address so that he can be attributed the conversion for driving that new participation into the network.

-------------------------

0x3639 | 2023-12-22 12:03:03 UTC | #12

Where did we end up with this discussion?  Are we going to run two versions?

-------------------------

mehowbrainz | 2023-12-22 16:19:32 UTC | #13

@sumamu mentioned that he'd deploy an anon variant.

-------------------------

