Thread: community-poll-priority-enhacements-for-deployment-script
coinselor | 2024-09-23 22:34:17 UTC | #1

We're looking to improve our [go-zenon deployment](https://github.com/hypercore-one/deployment) script and would love your input on which features we should prioritize.

Based on our current issues and potential enhancements, please vote for the option you think is most important:


[poll name=poll2 type=multiple results=always min=1 max=2 public=true chartType=bar]
* Add support for arm64 architecture
* Real time monitoring of events (UI)
* Save/Restore sync from bootstrap
* Add performance benchmarking for upgrade compatibility testing
* Expand node deployment options (regular, public, testnet, sentry, pillar)
[/poll]

The "Real time monitoring" leverages Grafana to include an user interface for analysis of historical performance data such as sync height over time, etc...

The "Add performance benchmarks" option would introduce automated testing tools to evaluate the impact of proposed optimization PRs, such as those recently submitted by @vilkris. This feature would enable the community to gather quantitative data on node performance improvements, facilitating more informed decisions on code updates and network optimizations.

The "Expand node deployment options" would allow users to easily choose between different node types during deployment, including regular, public, testnet, sentry, and pillar nodes.

Your feedback is crucial in helping us focus our efforts on the most valuable improvements. For more information, visit the [Operations SIG](https://zenon.wiki/index.php/HC1:_Operations_SIG) wiki page.

Feel free to discuss your choices or suggest additional enhancements in the comments below.

-------------------------

