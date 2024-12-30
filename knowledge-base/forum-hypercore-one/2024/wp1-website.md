Thread: wp1-website
georgezgeorgez | 2024-10-15 13:45:14 UTC | #1

Work thread for website

-------------------------

georgezgeorgez | 2024-10-15 13:56:17 UTC | #2

I think we want to stay with GitHub pages.
Jekyll is the default static site generator for GitHub pages. But using GitHub actions, any static site generator is able to be used.

I'm not really opinionated about this. But it would be good to stay with a common language within our community. Jekyll is Ruby. So maybe Hugo with Go, or any Javascript framework would be fine.

As long as it's easy enough for other community members to understand and build on top of.

-------------------------

coinselor | 2024-10-15 18:54:20 UTC | #3

I've been trying to learn [Threejs](https://threejs.org) lately using React's Three Fiber and Drei libraries. Pending final branding idea, I think it would be really cool and fitting if its some 3d animation. For the asset, we could ask green to create the 3d model, and then it's just putting it on a scene. 

I can't really commit to working on it, still have a few projects I need to finish. But a simple responsive landing page can definitely be done in a weekend, especially with AI's help.

-------------------------

sugoibtc | 2024-10-16 21:52:59 UTC | #4

## Mission of HyperQube-Z

The primary goal of HyperQube-Z (HQZ) is to create a platform that enables faster development and increased participation from contributors, both technical and non-technical. This extension chain serves as an experimental space where developers can test new features without impacting Zenon’s base layer. For instance, one of the first examples is that Vilkris plans to deploy dynamic plasma on HQZ, and we intend to develop incubator contracts specific to this extension chain. Additionally, HyperQube-Z will be used to test the integration of extension chains with mainnet.

HQZ also encourages participation from non-technical contributors through "awareness" tasks such as creating infographics, memes, marketing materials, and website design. These contributions will help expand the visibility and adoption of HQZ.

The tokenomics of HQZ will evolve as we refine how to connect these extension chains to the mainnet. The goal is not to create a token for the sake of having one but to ensure that the native tokens serve a real utility purpose.

## Target Audience

HyperQube-Z is designed for developers who want to experiment with NoM without affecting the base layer. It opens the door for real enthusiasts (degens) to access experimental contracts. Through this platform, other developers will also be able to create extension chains for various use cases. While the broader ecosystem will expand once we have a launchkit, the immediate focus is addressing broader challenges that hinder our development and collaboration, such as:

* Improving the review and approval process for critical development tasks to ensure timely progress.
* Enhancing coordination between contributors to ensure performance-related updates are prioritized and integrated.
* Establishing realistic testing environments for experimental features to better simulate mainnet conditions before deployment.

## Current Problems

The development of innovative features within the Zenon ecosystem is often slowed by a few key issues. One of the most pressing challenges is the lack of efficient review and approval processes for critical updates. Many projects face bottlenecks due to limited reviewer availability, resulting in delays that hinder overall progress.

Additionally, there is a gap between development and actual user adoption. Despite the completion of important updates or features, such as the PTLC embedded contract, we face difficulties in gathering real-world feedback because few users are interacting with or utilizing these technologies. This results in slower iteration cycles and limits the potential for continuous improvement.

This situation highlights the importance of open collaboration and knowledge sharing. While we have been managing collaboration through manual spreadsheets, this system will soon be replaced by incubator voting. The shift to this more structured and transparent process will better facilitate collaboration and task allocation, enhancing the speed and efficiency of development.

Our work packages, such as those outlined in WP1, offer incentives for tasks like documentation, testing, and SDK development, which helps contributors gain hands-on experience. Testing, often overlooked, is essential in software engineering and a key aspect of our governance model.

## Why HyperQube-Z?

Currently, developers are often incentivized to work on large, high-profile projects that generate buzz, but this approach can leave behind unresolved maintenance issues. There is a lack of well-defined review criteria, leading to delays and inefficiencies in the approval process.

To address these issues, HyperQube-Z aims to create a more structured and transparent development environment. By offering clear incentives for each stage of the software development process, including testing, documentation, and maintenance, we ensure that contributors are motivated to see their work through to completion.

Our governance model organizes tasks into specific work packages, categorized into areas such as admin, development, and awareness. This structure ensures that everyone is incentivized to collaborate effectively and complete their tasks.

## Why Launch with Placeholder Tokens?

The NoM architecture requires two tokens to emit, and modifying this setup would necessitate additional engineering work, which isn’t a priority at this stage. By launching with placeholder tokens, HyperQube-Z can begin experimenting and coordinating immediately, as our primary focus is not on improving tokenomics right now. These native tokens can be considered HQZ’s bootstrap tokens, serving as a temporary solution until we determine the best approach for extension chain integration.

While HQZ's native tokens may have limited initial value, they serve a crucial role in enabling experimentation and fostering early-stage development within this experimental environment.

## Utility and Tokenomics

The initial tokenomics of HQZ will reflect its status as an independent network. These tokens are utility tokens designed for extension chain-specific functions and should be considered worthless beyond their protocol use. HyperQube-Z contributors will not engage in market manipulation or attempt to establish a market value for these tokens.

As extension chain integration features mature, HQZ’s tokenomics will evolve. Future tokenomics might incorporate ZNN and QSR—whether as wrapped tokens, collateral, or in competitive features like mainnet staking. However, the immediate focus is on creating a platform that encourages contributor participation and accelerates project velocity, rather than refining tokenomics at this stage.

Over time, as HQZ grows and matures, its tokenomics will continue to evolve. WP1 is already introducing ZNN incentives to drive HQZ’s development, and we plan to implement a bridge for xZNN, allowing it to function within HyperQube-Z.

Additionally, contracts such as an embedded decentralized exchange (DEX) will support any token, including xZNN, with DEX fees payable in xZNN, further enhancing the utility of the network.

## Micro-Workz: Future Vision for HQZ

While our current focus is on enabling faster development and collaboration, we are also planning for future enhancements that will further scale our contributor ecosystem. A key part of this plan is the development of a "jobs/tasks" platform, where community members can post bounties for tasks, and external developers can engage with HQZ.

This platform will be integrated with the incubator, making it easier for developers to pick up smaller tasks and get paid quickly. By reducing the time it takes for contributors to receive their first payment, we aim to attract more outside talent and grow our network of contributors. This initiative directly supports our broader mission to increase participation and project velocity, laying the foundation for a more efficient and collaborative ecosystem.

-------------------------

sugoibtc | 2024-10-16 22:11:38 UTC | #5

I asked GPT to make a visual outline for the website, it gave me this lmao:
![image|690x394](upload://mlXmHpNfCMNiN4gjVpqOVq3gQWO.jpeg)

![image|690x394](upload://GP3tkNFBqahFKIXclDamjcAOsH.jpeg)

![image|690x394](upload://bolvfvAMGemYAYO2AdQYZtzhWhb.jpeg)



### 1. **Homepage**

**Headline:**
*HyperQube-Z (HQZ): Accelerating Innovation and Collaboration*

**Mission Statement:**
HQZ is an experimental platform designed to drive faster development and participation from contributors, both technical and non-technical. It allows developers to test new features without impacting Zenon’s base layer, while non-technical contributors can play a role in raising awareness through tasks such as infographics and marketing materials.

**Call to Action:**

* *"Join the HQZ Ecosystem"*
* *"Get Started with HQZ"*

Buttons should lead to sections for developers and non-technical contributors.

---

### 2. **About Us**

**Section Title:**
*About HyperQube-Z*

**Content:**
HyperQube-Z (HQZ) is a platform built for experimentation and collaboration within the Zenon Network ecosystem. Our mission is to provide a space where contributors can test new features, develop incubator contracts, and integrate extension chains with the Zenon mainnet—all without impacting its core operations.

We aim to include both technical and non-technical contributors in the development of HQZ. While developers focus on testing and building, non-technical contributors play a vital role in raising awareness through tasks like infographics, memes, marketing, and website design.

---

### 3. **How It Works**

**Section Title:**
*How HQZ Works*

**Content:**
HQZ is designed to provide a secure and flexible environment where developers can build and test new features for the Zenon ecosystem. Here’s how HQZ operates:

* **For Developers**: Experiment with NoM without affecting Zenon’s base layer. Developers can also create extension chains for specific use cases. Our focus is on solving development challenges, improving collaboration, and enhancing coordination between contributors.
* **Utility and Tokenomics**: HQZ operates as an independent network with utility tokens that serve specific purposes. These tokens allow contributors to experiment with new features while ensuring integration with the mainnet. As HQZ matures, we will adopt new tokenomics that might include ZNN and QSR for staking and collateral purposes.
* **Why Launch with Placeholder Tokens?**: Placeholder tokens allow us to start experimenting immediately, while the long-term tokenomics will evolve as HQZ grows.

Consider adding infographics or simple diagrams to help explain these processes.

---

### 4. **For Developers**

**Section Title:**
*Develop on HQZ*

**Content:**
HQZ provides a space for developers to experiment with new features in a risk-free environment. Whether you want to test contracts, solve performance issues, or develop on the incubator, HQZ gives you the tools to contribute to the ecosystem.

We are also working on a **"jobs/tasks" platform**, which will allow developers to pick up small tasks, earn bounties, and contribute quickly to the ecosystem. This platform will streamline contributions and help developers get involved faster.

**Links/Resources:**

* Documentation
* GitHub Repository
* Developer Community

---

### 5. **For Non-Technical Contributors**

**Section Title:**
*Get Involved: Non-Technical Contributions*

**Content:**
HQZ isn't just for developers. We invite non-technical contributors to play a vital role in growing the project through "awareness" tasks. This includes designing infographics, creating memes, marketing materials, and even assisting with website design.

By participating, you help spread the word about HQZ, making it more visible and accessible to the community. Whether you’re a designer, marketer, or just someone passionate about blockchain, there’s a place for you in the HQZ ecosystem.

**Examples/Success Stories:**
Share some contributions or showcase examples from community members.

---

### 6. **Future Vision**

**Section Title:**
*The Future of HQZ*

**Content:**
As HQZ grows, our future vision includes creating more opportunities for external developers and contributors. One of the most exciting developments is **Micro-Workz**, a "jobs/tasks" platform integrated with the incubator, where small tasks and bounties will be posted for quick pickup. This will allow contributors to make impactful contributions and get paid quickly.

We are also exploring new integrations with ZNN and QSR, ensuring that as HQZ matures, it continues to drive innovation and collaboration across the ecosystem.

---

### 7. **Tokenomics and Utility**

**Section Title:**
*HQZ Tokenomics*

**Content:**
HQZ’s initial tokenomics are designed to support the development of extension chain-specific functions. These tokens are purely for protocol purposes and do not hold value beyond their utility within the HQZ environment.

As the platform evolves, we expect to integrate ZNN and QSR into HQZ’s tokenomics, allowing these tokens to serve more advanced functions like collateral or staking. We are also working on contracts like an embedded decentralized exchange (DEX), where tokens like xZNN can be traded, and DEX fees paid in xZNN.

---

### 8. **Contact or Community**

**Section Title:**
*Join the HQZ Community*

**Content:**
Be a part of the HQZ ecosystem! Whether you’re a developer, contributor, or simply interested in blockchain innovation, we welcome you to join our community. Connect with us on social media or engage with the team on Discord, where we share updates, resources, and development opportunities.

**Links to:**

* Discord
* Twitter
* GitHub
* Telegram

-------------------------

0x3639 | 2024-10-18 12:18:27 UTC | #6

who are you going to use to program it?

-------------------------

georgezgeorgez | 2024-10-18 19:59:44 UTC | #7

I think one key aspect of the website is showcasing people getting paid through the incubator process.

I think the focus should be collaborative instead of competitive.

E.g. have stats for # of work packages paid out, ZNN amount, # of contributors paid
Probably not a leaderboard which could get toxic.
A section to showcase the awareness assets which have been paid for.

-------------------------

Stark | 2024-10-18 18:42:43 UTC | #8

There is so mych to do, and so few of us. We shouldn't have too much problem stepping on each other's toes, for now.

-------------------------

