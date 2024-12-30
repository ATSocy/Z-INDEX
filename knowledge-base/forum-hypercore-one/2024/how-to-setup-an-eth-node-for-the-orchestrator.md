Thread: how-to-setup-an-eth-node-for-the-orchestrator
0x3639 | 2023-05-30 13:01:57 UTC | #1

Before you get started with setting up the [Orchestrator](https://forum.hypercore.one/t/how-to-setup-orchestrator/61?u=0x3639), Pillar Operators need to setup an Ethereum Node.  There are two options to do that.  Operators can either sign up for a 3rd party node as a service or run the node locally.  After setting up the Ethereum node, the Operator needs a websocket (ws) to connect to.  Make note of the websocket endpoint.  It is needed for the Orchestrator `config.json` file setup.   

## NODE AS A SERVICES

Here is a list of some of the most popular Ethereum node providers. Each node service offers different benefits and features in addition to free or paid tiers, you should investigate which ones best suit your needs prior to making a decision.

* [**Alchemy** ↗](https://alchemy.com/)
  * [Docs ↗](https://docs.alchemyapi.io/)
  * Features
    * Largest free tier with 300M compute units per month (~30M getLatestBlock requests)
    * Multichain support for Polygon, Starknet, Optimism, Arbitrum
    * Powering ~70% of the largest Ethereum dapps and DeFi transaction volume
    * Real-time webhook alerts via Alchemy Notify
    * Best-in-class support and reliability / stability
    * Alchemy's NFT API
    * Dashboard with Request Explorer, Mempool Watcher, and Composer
    * Integrated testnet faucet access
    * Active Discord builder community with 18k users

If you select Alchemy sign up for free.  Register your email address and select "Create App".  Give it a name and description.  Select Chain: Ethereum and Network" Ethereum Mainnet.

![Screenshot 2023-05-30 at 7.55.57 AM|679x500](upload://syIkzHRPG9nYuZ94O2N5yJtrcWh.png)

After creating the app you will see it in the app list.  Click on `View Key`. 

![Screenshot 2023-05-30 at 7.56.28 AM|689x161](upload://j7KUF7Ei0CbG8Nml83AEGsT4ycv.jpeg)

Click on `Copy` next to the Websocket address. Paste this into a text file for use in the Orchestrator setup.  This is the URL address with API key that you will use.  Do NOT use the address in this image.  It's not active.

![Screenshot 2023-05-30 at 7.56.41 AM|440x500](upload://6ecP7CU1gxy39mxlB3xy2aQRkMj.png)


* [**All That Node** ↗](https://allthatnode.com/)
  * [Docs ↗](https://docs.allthatnode.com/)
  * Features
    * Largest free tier with 150,000 requests daily
    * Access to 24+ blockchain nodes
    * RPC, HTTPS and WSS endpoints
    * Unlimited access to archive data
    * 24/7 support and uptime over 99.9%
    * Faucet available on multi chains
    * Unlimited endpoint access with limitless number of API keys
    * Trace/Debug namespace available
    * Automated updates
    * Technical support
* [**Ankr** ↗](https://www.ankr.com/)
  * [Docs ↗](https://docs.ankr.com/)
  * Features
    * Ankr Protocol - open access to Public RPC API endpoints for 8+ chains
    * Load balancing and node health monitoring for a fast and reliable gateway to the nearest available node
    * Premium tier enabling WSS endpoint and uncapped rate limit
    * One-click full node and validator node deployment for 40+ chains
    * Scale as you go
    * Analytics tools
    * Dashboard
    * RPC, HTTPS and WSS endpoints
    * Direct support
* [**Blast** ↗](https://blastapi.io/)
  * [Docs ↗](https://docs.blastapi.io/)
  * Features
    * RPC and WSS support
    * Multi-region node hosting
    * Decentralized infrastructure
    * Public API
    * Dedicated Free Plan
    * Multichain support (17+ blockchains)
    * Archive Nodes
    * 24/7 Discord Support
    * 24/7 Monitoring and alerts
    * An overall SLA of 99.9%
    * Pay in crypto
* [**BlockDaemon** ↗](https://blockdaemon.com/)
  * [Docs ↗](https://ubiquity.docs.blockdaemon.com/)
  * Benefits
    * Dashboard
    * Per node basis
    * Analytics
* [**BlockPI** ↗](https://blockpi.io/)
  * [Docs ↗](https://docs.blockpi.io/)
  * Fetures
    * Robust & distributed node structure
    * Up to 40 HTTPS and WSS endpoints
    * Free signup package and monthly package
    * Trace method + Archive data support
    * Packages up to 90 days validity
    * Custom plan and pay as you go payment
    * Pay in crypto
    * Direct support & Technical support
* [**Chainstack** ↗](https://chainstack.com/)
  * [Docs ↗](https://docs.chainstack.com/)
  * Features
    * Free shared nodes
    * Shared archive nodes
    * GraphQL support
    * RPC and WSS endpoints
    * Dedicated full and archive nodes
    * Fast sync time for dedicated deployments
    * Bring your cloud
    * Pay-per-hour pricing
    * Direct 24/7 support
* [**DataHub** ↗](https://datahub.figment.io/)
  * [Docs ↗](https://docs.figment.io/)
  * Features
    * Free tier option with 3,000,000 reqs/month
    * RPC and WSS endpoints
    * Dedicated full and archive nodes
    * Auto-Scaling (Volume Discounts)
    * Free archival data
    * Service Analytics
    * Dashboard
    * Direct 24/7 Support
    * Pay in Crypto (Enterprise)
* [**GetBlock** ↗](https://getblock.io/)
  * [Docs ↗](https://getblock.io/docs/get-started/authentication-with-api-key/)
  * Features
    * Access to 40+ blockchain nodes
    * 40K free daily requests
    * Unlimited number of API keys
    * High connection speed at 1GB/sec
    * Trace+Archive
    * Advanced analytics
    * Automated updates
    * Technical support
* [**InfStones** ↗](https://infstones.com/)
  * Features
    * Free tier option
    * Scale as you go
    * Analytics
    * Dashboard
    * Unique API endpoints
    * Dedicated full nodes
    * Fast sync time for dedicated deployments
    * Direct 24/7 support
    * Access to 50+ blockchain nodes
* [**Infura** ↗](https://infura.io/)
  * [Docs ↗](https://infura.io/docs)
  * Features
    * Free tier option
    * Scale as you go
    * Paid archival data
    * Direct Support
    * Dashboard
* [**Kaleido** ↗](https://kaleido.io/)
  * [Docs ↗](https://docs.kaleido.io/)
  * Features
    * Free startier tier
    * One-click Ethereum node deployment
    * Customizable clients and algorithms (Geth, Quorum & Besu || PoA, IBFT & Raft)
    * 500+ administrative and service APIs
    * RESTful interface for Ethereum transaction submission (Apache Kafka backed)
    * Outbound streams for event delivery (Apache Kafka backed)
    * Deep collection of "off-chain" and ancillary services (e.g. bilateral encrypted messaging transport)
    * Straightforward network onboarding with governance and role-based access control
    * Sophisticated user management for both administrators and end users
    * Highly scalable, resilient, enterprise-grade infrastructure
    * Cloud HSM private key management
    * Ethereum Mainnet Tethering
    * ISO 27k and SOC 2, Type 2 certifications
    * Dynamic runtime configuration (e.g. adding cloud integrations, altering node ingresses, etc.)
    * Support for multi-cloud, multi-region and hybrid deployment orchestrations
    * Simple hourly SaaS-based pricing
    * SLAs and 24x7 support
* [**Moralis** ↗](https://moralis.io/)
  * [Docs ↗](https://docs.moralis.io/)
  * Features
    * Free shared nodes
    * Free shared archive nodes
    * Privacy focused (no logs policy)
    * Cross chain support
    * Scale as you go
    * Dashboard
    * Unique Ethereum SDK
    * Unique API endpoints
    * Direct, technical support
* [**NodeReal MegaNode** ↗](https://nodereal.io/)
  * [Docs ↗](https://docs.nodereal.io/nodereal/meganode/introduction)
  * Features
    * Reliable, fast and scalable RPC API services
    * Enhanced API for web3 developers
    * Multi-chain support
    * Get started for free
* [**NOWNodes** ↗](https://nownodes.io/)
  * [Docs ↗](https://documenter.getpostman.com/view/13630829/TVmFkLwy)
  * Features
    * Access to 50+ blockchain nodes
    * Free API Key
    * Block Explorers
    * API Response Time ⩽ 1 sec
    * 24/7 Support Team
    * Personal Account Manager
    * Shared, archive, backup and dedicated nodes
* [**Pocket Network** ↗](https://www.pokt.network/)
  * [Docs ↗](https://docs.pokt.network/home/)
  * Features
    * Decentralized RPC Protocol and Marketplace
    * 1M Requests Per Day Free Tier (per endpoint, max 2)
    * [Public Endpoints ↗](https://docs.pokt.network/home/resources/public-rpc-endpoints)
    * Pre-Stake+ Program (if you need more than 1M requests per day)
    * 15+ Blockchains Supported
    * 6400+ Nodes earning POKT for serving applications
    * Archival Node, Archival Node w/ Tracing, & Testnet Node Support
    * Ethereum Mainnet Node Client Diversity
    * No Single Point of Failure
    * Zero Downtime
    * Cost-Effective Near-Zero Tokenomics (stake POKT once for network bandwidth)
    * No monthly sunk costs, turn your infrastructure into an asset
    * Load-Balancing built into the Protocol
    * Infinitely scale the number of requests per day and nodes per hour as you go
    * The most private, censorship-resistant option
    * Hands-on developer support
    * [Pocket Portal ↗](https://bit.ly/ETHorg_POKTportal) dashboard and analytics
* [**QuickNode** ↗](https://www.quicknode.com/)
  * [Docs ↗](https://www.quicknode.com/docs/)
  * Features
    * Industry-leading performance and reliability
    * 24/7 technical support & dev Discord community
    * Geo-balanced, multi cloud/metal, low-latency network
    * Multichain support (Optimism, Arbitrum, Polygon + 11 others)
    * Middle-layers for speed & stability (call routing, cache, indexing)
    * Smart-Contract monitoring via Webhooks
    * Intuitive dashboard, analytics suite, RPC composer
    * Advanced security features (JWT, masking, whitelisting)
    * NFT data and analytics API
    * [SOC2 Certified(opens in a new tab)↗](https://www.quicknode.com/security)
    * Suitable for Developers to Enterprises
* [**Rivet** ↗](https://rivet.cloud/)
  * [Docs ↗](https://rivet.readthedocs.io/en/latest/)
  * Features
    * Free tier option
    * Scale as you go
* [**SenseiNode** ↗](https://senseinode.com/)
  * [Docs ↗](https://docs.senseinode.com/)
  * Features
    * Dedicated and Share nodes
    * Dashboard
    * Hosting off AWS on multiple hosting providers across different locations in Latin America
    * Prysm and Lighthouse clients
* [**SettleMint** ↗](https://console.settlemint.com/)
  * [Docs ↗](https://docs.settlemint.com/)
  * Features
    * Free trial
    * Scale as you go
    * GraphQL support
    * RPC and WSS endpoints
    * Dedicated full nodes
    * Bring your cloud
    * Analytics tools
    * Dashboard
    * Pay-per-hour pricing
    * Direct support
* [**Tenderly** ↗](https://tenderly.co/web3-gateway)
  * [Docs ↗](https://docs.tenderly.co/web3-gateway/web3-gateway)
  * Features
    * Free tier including 25 million Tenderly Units per month
    * Free access to historical data
    * Up to 8x faster read-heavy workloads
    * 100% consistent read access
    * JSON RPC endpoints
    * UI-based RPC request builder and request preview
    * Tightly integrated with Tenderly’s development, debugging, and testing tools
    * Transaction simulations
    * Usage analytics and filtering
    * Easy access key management
    * Dedicated engineering support via chat, email, and Discord
* [**Watchdata** ↗](https://watchdata.io/)
  * [Docs ↗](https://docs.watchdata.io/)
  * Features
    * Data reliability
    * Uninterrupted connection with no downtime
    * Process automation
    * Free tariffs
    * High limits that suit any user
    * Support for various nodes
    * Resource scaling
    * High processing speeds
* [**ZMOK** ↗](https://zmok.io/)
  * [Docs ↗](https://docs.zmok.io/)
  * Features
    * Front-running as a service
    * Global transactions mempool with search/filtering methods
    * Unlimited TX fee and infinite Gas for sending transactions
    * Fastest getting of the new block and reading of the blockchain
    * The best price per API call guarantee

[**Zeeve** ↗](https://www.zeeve.io/)

* [Docs ↗](https://www.zeeve.io/docs/)
* Features
  * Enterprise-grade no-code automation platform providing deployment, monitoring and management of Blockchain nodes and networks
  * 30+ Supported Protocols & Integrations, and adding more
  * Value added web3 infrastructure services like decentralized storage, decentralized identity and Blockchain Ledger data APIs for real-world use cases
  * 24/7 support and proactive monitoring ensure the health of nodes all the time.
  * RPC endpoints offer authenticated access to API’s, hassle free management with intuitive dashboard and analytics.
  * Provides both managed cloud and bring your own cloud options to choose from and supports all major cloud providers like AWS, Azure, Google Cloud, Digital Ocean and on-premise.
  * We use intelligent routing to hit the node closest to your user every time


## LOCAL NODE

Multiple user-friendly projects aim to improve the experience of setting up a client. These launchers provide automatic client installation and configuration, with some even offering a graphical interface for guided setup and monitoring of clients.

Below are a few projects which can help you install and control clients just with a few clicks:

* [DappNode ↗](https://docs.dappnode.io/user/quick-start/first-steps/) - DappNode doesn't come only with a machine from a vendor. The software, the actual node launcher and control center with many features can be used on arbitrary hardware.
* [eth-docker ↗](https://eth-docker.net/) - Automated setup using Docker focused on easy and secure staking, requires basic terminal and Docker knowledge, recommended for a bit more advanced users.
* [Stereum ↗](https://stereum.net/ethereum-node-setup/) - Launcher for installing clients on a remote server via SSH connection with a GUI setup guide, control center, and many other features.
* [NiceNode ↗](https://www.nicenode.xyz/) - Launcher with a straightforward user experience to run a node on your computer. Just choose clients and start them with a few clicks. Still in development.
* [Sedge ↗](https://docs.sedge.nethermind.io/docs/intro) - Node setup tool which automatically generates a Docker configuration using CLI wizard. Written in Go by Nethermind.

-------------------------

