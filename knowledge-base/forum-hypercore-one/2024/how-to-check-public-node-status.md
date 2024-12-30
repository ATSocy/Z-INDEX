Thread: how-to-check-public-node-status
0x3639 | 2024-12-24 11:27:19 UTC | #1

**How to Test if a Zenon Node is Up and Fully Synced**

When running a Zenon Node, it’s important to check its status to ensure it’s operational and in sync with the network. This guide explains how to use the `curl` command to query the sync status of your node. Instructions are provided for both Windows and Linux/macOS users.

**Understanding Sync Status**

The JSON-RPC response includes a state field with three possible values:

1. **State 1**: Not synced. The node is behind in block height and still catching up.
2. **State 2**: Fully synced. The node is synced to the latest block and has sufficient peers.
3. **State 3**: Synced but has low peers. The node is synced to the latest block but has insufficient peers to operate optimally.

**Instructions for Windows Users**

1. **Open Command Prompt**:

• Press Win + R, type cmd, and press Enter.

2. **Run the Command**:

Copy and paste the following command, replacing https://my.hc1node.com:35997 with your node’s API URL:

```bash
curl -X POST https://my.hc1node.com:35997 ^
-H "Content-Type: application/json" ^
-d "{\"jsonrpc\": \"2.0\", \"id\": 40, \"method\": \"stats.syncInfo\", \"params\": []}"
```

3. **Interpret the Response**:

The node will respond with a JSON object similar to this:

```bash
{"jsonrpc":"2.0","id":40,"result":{"state":2,"currentHeight":9177763,"targetHeight":9177763}}
```

• Check the state field:

- `1`: Not synced.
- `2`: Fully synced.
- `3`: Synced but low peers.

**Instructions for Linux and macOS Users**

1. **Open Terminal**:

• On Linux, open your preferred terminal application.
• On macOS, press Command + Space, type Terminal, and hit Enter.

2. **Run the Command**:

Execute the following command, replacing https://my.hc1node.com:35997 with your node’s API URL:

```bash
curl -X POST https://my.hc1node.com:35997 \
-H "Content-Type: application/json" \
-d '{"jsonrpc": "2.0", "id": 40, "method": "stats.syncInfo", "params": []}'
```

3. **Interpret the Response**:

The node will respond with a JSON object, for example:

```bash
{"jsonrpc":"2.0","id":40,"result":{"state":2,"currentHeight":9177763,"targetHeight":9177763}}
```

• Check the state field:

• `1`: Not synced.
• `2`: Fully synced.
• `3`: Synced but low peers.

**Troubleshooting Sync Issues**

• **State 1 (Not Synced)**: The node is still catching up. Verify your node’s network connectivity and block processing.
• **State 2 (Fully Synced)**: The node is fully operational.
• **State 3 (Synced but Low Peers)**: Ensure your node is connected to enough peers. Check your node configuration to add more peers if necessary.
• **No Response**: Verify the API URL and ensure the node’s API port is open and reachable.

-------------------------

