Thread: how-to-setup-caddy-for-rpc-and-state-sync-on-supernova
0x3639 | 2024-11-14 18:09:31 UTC | #1

### How to Set Up Caddy for RPC and state-sync on Supernova

This guide will help you set up Caddy to proxy requests for RPC services on Supernova, with separate routing for WebSocket and HTTP traffic. This configuration enables easy handling of connections to your RPC and sync services.

#### Step 1: Install Caddy

Start by installing Caddy on your server. Use the following commands to add the Caddy repository and install Caddy:

```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

#### Step 2: Configure the Caddyfile

Once Caddy is installed, create or edit the `Caddyfile` to define reverse proxy rules for `example.com`. Open the `Caddyfile` in a text editor, such as Nano:

```bash
sudo nano /etc/caddy/Caddyfile
```

Add the following configuration block to handle WebSocket connections, standard HTTP requests, and sync connections:

```caddyfile
example.com {
    # Define a matcher for WebSocket connections
    @websocket {
        header Upgrade websocket
    }

    # Handle WebSocket connections and proxy them to IP_ADDRESS:8546
    reverse_proxy @websocket IP_ADDRESS:8546

    # Handle all other HTTP requests and proxy them to IP_ADDRESS:8545
    reverse_proxy IP_ADDRESS:8545
}

sync.example.com {
    reverse_proxy IP_ADDRESS:26657
}
```

> **Note:** Replace `example.com` with your actual domain wherever necessary, and replace `IP_ADDRESS` with the actual IP address of your RPC service.

#### Step 3: Start and Enable Caddy

After saving the changes to your Caddyfile, restart the Caddy service to apply the new configuration:

```bash
sudo systemctl restart caddy
```

You may also want to enable Caddy to start automatically on boot:

```bash
sudo systemctl enable caddy
```

#### Verifying the Setup

Once Caddy is running with the updated configuration, test the endpoints to confirm:
- WebSocket requests to `example.com` route correctly to `IP_ADDRESS:8546`.
- HTTP requests to `example.com` go to `IP_ADDRESS:8545`.
- All requests to `sync.example.com` are routed to `IP_ADDRESS:26657`.

This setup allows Caddy to manage reverse proxying for both WebSocket and HTTP traffic, optimizing communication for Supernova’s RPC and sync services.

---

With this configuration, your Supernova instance should be accessible via Caddy, handling different request types efficiently! Remember to replace `example.com` with your actual domain throughout.

-------------------------

