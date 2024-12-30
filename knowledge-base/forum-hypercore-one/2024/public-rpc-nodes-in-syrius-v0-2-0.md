Thread: public-rpc-nodes-in-syrius-v0-2-0
0x3639 | 2024-02-28 11:18:42 UTC | #1

We are moving forwards towards a `syrius v0.2.0` release.  Like other blockchain wallet, we are offering (trusted) public RPC nodes for users to select if they don't want to sync.  Today in TG Main we have three options.  I would like to proposing adding @coinselor's node to the list in `syrius`.

@coinselor is that OK and does anyone object?

![image|609x500](upload://z3VKIIqrosGcAUkaDm7HoAT7eB.jpeg)

In the future we need to come up with a better way to add / remove nodes. Maybe we have a `.json` file in the `syrius` repo that community members can submit PRs on to add / remove nodes.  Does anyone have ideas for this?

Maybe we have a stand alone `nodes.json` file that is easy to find with instructions in the readme.md explaining how to add / remove nodes.  Basically fork the repo, make the change, submit PR.  And we can establish minimum requirements to be considered.

-------------------------

coinselor | 2024-02-28 11:30:44 UTC | #2

It's ok by me, but my node is currently not as robust as the other two and should be the last considered option. I still need to configure a load balancer in front and setup a couple backup locations, devops noob here so I'm learning as I go.

-------------------------

CryptoFish | 2024-02-28 12:28:50 UTC | #3

The public nodes are randomized each time they are loaded, so there is no difference or any meaning attached to one particular node.

The public nodes are currently hard-coded. It is possible to setup a separate repo specifically for the purpose for maintaining a public node database. Something similar as to what ledger does with the [ledger-app-database](https://github.com/LedgerHQ/ledger-app-database).

PR's are made to add or remove app registrations from the list, which is basically one big json file.

In our case the repo would serve as a public node database which can be used by various applications. bc I believe syrius isn't the only application in need of this list.

Once the repo is setup, syrius can use the repo from within the build workflow. This would still require a build to include the latest version, but it does separate the list from the syrius repo. Making it available for other applications to use and in the same time have some standardized way of maintaining it.

-------------------------

aliencoder | 2024-02-28 16:40:15 UTC | #4

[quote="CryptoFish, post:3, topic:385"]
The public nodes are currently hard-coded
[/quote]

And they have a "Community" label for increased transparency.

-------------------------

