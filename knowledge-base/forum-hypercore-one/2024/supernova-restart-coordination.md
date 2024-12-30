Thread: supernova-restart-coordination
0x3639 | 2024-10-20 10:32:45 UTC | #1

Working thread to coordinate the restart of Supernova.

## Datetime: TBD

## Configuration Checks

### Sentry | Validator | Archive Node Seed Addresses
`seeds = "ee5a4e4d21e3248f8efebbcb7889b434c4c48ba4@3.94.70.251:26656,2a3cd2768826aed5792593a2d6c8f6b28435a2a7@172.245.233.171:26656,ced855d1514b84adabe8590acd474487710ca259@167.235.79.123:26656"
`
***Note:*** Seed node operators ***only*** should remove the seed address of their own seed.  This means if you operate a seed node you will only have (2) seed addresses.

## Validator node:
- unconditional_peer_ids = "your_sentry_node_id(s)"
- persistent_peers = "your_sentry"
- pex = "false"

## Sentry node:
- unconditional_peer_ids = "your_validator_node_id"
- persistent_peers = "your_validator"
- private_peer_ids = "your_validator_node_id"
- seeds = "seed_nodes"
- pex = "true"

## Other
- Check supernovad binary version v0.0.4.
- Check the supernova.service.
- Check ufw status and ALLOW every connection to and from port 26656.
- Check the genesis.json hash.
- Check that the selected db backend is rocksdb.
- Check that your sentry, validator or seed full node is fully synced.

## Service
```
[Unit]
Description=supernova service
After=network.target

[Service]
LimitNOFILE=32768
User=root
Group=root
Type=simple
ExecStart=/usr/local/bin/supernovad start
ExecStop=/bin/kill -s SIGTERM $MAINPID
Restart=on-failure
TimeoutStopSec=120s
TimeoutStartSec=30s

[Install]
WantedBy=multi-user.target
```

## Logs

Check the validator logs for:

```
INF This node is a validator ... INF Completed ABCI Handshake - CometBFT and App are synced appHash=D366F08BB5CBB68D82C0C339E8257FC802E567512954C9C3975AA257EA05DA18 appHeight=629763 module=consensus server=node
```

## Comments
All replies will be auto deleted after 3 days.

-------------------------

