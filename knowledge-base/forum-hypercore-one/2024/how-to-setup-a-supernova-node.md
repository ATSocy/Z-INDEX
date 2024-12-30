Thread: how-to-setup-a-supernova-node
coinselor | 2024-11-28 17:56:55 UTC | #1

This guide provides a comprehensive approach to deploying various node types for the Supernova extension-chain, a Zenon EVM-compatible blockchain built on Cosmos SDK technology.

## A Note on Node Types

* **Standard Node**: Maintains a full copy of the blockchain and helps propagate transactions and blocks. Ideal for general participation with moderate hardware requirements.
* **Pillar Node (Validator)**: Validates transactions and participates in consensus to secure the network. Requires higher resources and commitment.
* **Sentry Node**: Acts as a protective layer for validators by filtering network traffic and mitigating attacks. Used by validators to enhance security.
* **Archive Node**: Stores the entire blockchain history without pruning. Essential for full historical data access; demands significant storage and resources.
* **Seed Node**: Provides initial peer information to new nodes joining the network, facilitating their connection. Requires high uptime and reliable network availability.

### System Requirements

|Node Type | vCPUs | RAM | Storage | Swap Space|
|--- | --- | --- | --- | ---|
|Pillar (Validator) Node | 4+ | 8GB+ | 500GB+ | 16GB|
|Sentry (Standard) Node | 4 | 8GB | 300GB+ | 8GB|
|Archive Node | 4+ | 16GB+ | 1TB+ | 32GB|
|Seed Node | 2 | 4GB | 100GB+ | 4GB|

### Recommended Operating Systems
- Ubuntu 22.04 LTS
- Debian (Latest Stable)

### Dependencies:
  - `curl`, `wget`, `jq`, `ufw`, `git`, `make`, `build-essential`

### Initial System Configuration

#### System Update and Dependency Installation
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install build-essential jq ufw git wget -y
```

#### Configure System Limits
Edit `/etc/security/limits.conf` to increase file descriptor limits:
```
*               soft    nofile          60000
*               hard    nofile          60000
```
Apply the new limits:
```bash
ulimit -n 60000
```

#### Firewall Configuration
```bash
sudo ufw enable
sudo ufw allow 22/tcp     # SSH
sudo ufw allow 26656/tcp  # Tendermint P2P
sudo ufw allow 26657/tcp  # Tendermint RPC
sudo ufw allow 1317/tcp   # Cosmos SDK REST API
sudo ufw allow 8545/tcp   # EVM HTTP RPC
sudo ufw allow 8546/tcp   # EVM WS RPC
sudo ufw reload
```

#### Swap Space Configuration
Swap space configuration varies by node type:
- Archive Node: 32GB
- xChain Pillar Node: 16GB
- Sentry Node: 8GB
- Seed Node: 4GB

Example Swap Setup:
```bash
# For an 8GB Sentry Node
sudo fallocate -l 8G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

## Node Types and Configuration

### 1. Sentry (Regular) Node Setup

#### Binary Installation
```bash
# Choose appropriate binary based on system architecture
# For Linux ARM64
wget https://github.com/AliensZone/supernova/releases/download/v0.0.8/supernova_Linux_arm64.tar.gz
tar -xvf supernova_Linux_arm64.tar.gz

# For Linux x86_64
wget https://github.com/AliensZone/supernova/releases/download/v0.0.8/supernova_Linux_x86_64.tar.gz
tar -xvf supernova_Linux_x86_64.tar.gz
```

#### Binary Path Configuration
```bash
sudo mv bin/supernovad /usr/local/bin/
sudo chmod +x /usr/local/bin/supernovad
```
Verify installation:
```bash
supernovad version
```

#### Node Initialization
```bash
# Initialize node with a moniker
supernovad init sentry_node --chain-id supernova_73405-1
```

#### Configuration Modifications
Edit configuration files in `~/.supernova/config/`:

`config.toml`:
```toml
# P2P Configuration
pex = true
persistent_peers = ""  # Will be added when converting to Sentry
seeds = "ced855d1514b84adabe8590acd474487710ca259@167.235.79.123:26656,f5707786778283258b37b5154a520897ab4b75b5@116.203.187.234:26656"
addr_book_strict = false
db_backend = "rocksdb"
```

`app.toml`:
```toml
# Pruning Configuration
pruning = "default"

# Minimum Gas Prices
minimum-gas-prices = "0stake"

# EVM RPC Configuration
[json-rpc]
address = "0.0.0.0:8545"
ws-address = "0.0.0.0:8546"
```

#### Systemd Service Configuration
Create `/etc/systemd/system/supernova.service`:
```ini
[Unit]
Description=Supernova Node Service
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

#### Service Management
```bash
systemctl daemon-reload
systemctl enable supernova.service
systemctl start supernova.service
```

### 2. Converting to Sentry Node

When converting to a Sentry node for a specific pillar/validator:

`config.toml` modifications:
```toml
pex = true
persistent_peers = "VALIDATOR_NODE_ID@VALIDATOR_IP:26656"
private_peer_ids = "VALIDATOR_NODE_ID"
unconditional_peer_ids = "VALIDATOR_NODE_ID@VALIDATOR_IP:26656"
```

### 3. Validator Node Configuration

Additional steps for validator nodes:
- Generate validator key
TO BE CONTINUED....

### 4. Archival Node Configuration

Key differences for archival nodes:
- Increased storage requirements
- Different pruning configuration
- State sync enablement

`app.toml` modifications:
```toml
pruning = "nothing"
snapshot-interval = 15000
snapshot-keep-recent = 2

```
For additional endpoint configuration please read https://forum.hypercore.one/t/how-to-setup-caddy-for-rpc-and-state-sync-on-supernova/556

### 5. Seed Node Configuration

`config.toml` modifications:
```toml
laddr = "tcp://0.0.0.0:26656"
external_address = "YOUR_PUBLIC_IP:26656"
seed_mode = true
```

## Maintenance and Monitoring

1. Regular Updates: 

Build from source
```bash
cd ~/supernova
git pull
make build
sudo cp build/supernovad /usr/local/bin/
systemctl restart supernova.service
```

Download latest binary
```bash
# Choose appropriate binary based on system architecture
# For Linux ARM64
wget https://github.com/AliensZone/supernova/releases/download/v0.0.8/supernova_Linux_arm64.tar.gz
tar -xvf supernova_Linux_arm64.tar.gz

# For Linux x86_64
wget https://github.com/AliensZone/supernova/releases/download/v0.0.8/supernova_Linux_x86_64.tar.gz
tar -xvf supernova_Linux_x86_64.tar.gz
```
Move binary to default location:

```bash
sudo mv bin/supernovad /usr/local/bin/
```

2. Log Monitoring
```bash
journalctl -u supernova.service -f
```

## Network Connectivity

### Seed Nodes
```
ced855d1514b84adabe8590acd474487710ca259@167.235.79.123:26656
f5707786778283258b37b5154a520897ab4b75b5@116.203.187.234:26656
```

-------------------------

tapwoot | 2024-11-29 19:15:10 UTC | #2

thx for this update, much needed

-------------------------

