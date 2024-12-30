Thread: how-to-set-up-an-ssl-endpoint-for-go-zenon-with-a-caddy-reverse-proxy
0x3639 | 2024-08-31 20:47:29 UTC | #1

### How to Set Up an SSL endpoint for go-zenon with a Caddy Reverse Proxy, Configure UFW Firewall, and Secure Your Server with Fail2ban

In this guide, I'll walk you through setting up a reverse proxy with Caddy for your web applications, configuring UFW (Uncomplicated Firewall) to secure your server, and adding an extra layer of security with Fail2ban to protect against brute-force attacks.

#### **Step 1: Install Caddy**

First, make sure you have Caddy installed on your server. Here are the commands to install it:

```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

#### **Step 2: Locate and Edit the Caddyfile**

Caddy's main configuration file is called the `Caddyfile`. By default, this file is located at `/etc/caddy/Caddyfile`. To edit this file, you can use the `nano` text editor.

1. **Open the Caddyfile in Nano:**

   ```bash
   sudo nano /etc/caddy/Caddyfile
   ```

2. **Add Your Configuration:**

   Here's a sample configuration you can add to the `Caddyfile`:

   ```caddyfile
   example.com { 
       @websocket {
           header Upgrade websocket
       }

       # Handle WebSocket connections and proxy them to the appropriate service
       reverse_proxy @websocket 127.0.0.1:35998 {
           header_up Host {http.reverse_proxy.upstream.hostport}
       }

       # Handle all other HTTP requests and proxy them to the primary web service
       reverse_proxy 127.0.0.1:35997 {
           header_up Host {http.reverse_proxy.upstream.hostport}
       }
   }
   ```
* Make sure to change `example.com` to your domain name.

3. **Save and Exit Nano:**

   After adding your configuration, save the file by pressing `Ctrl + O`, then press `Enter` to confirm. Exit nano by pressing `Ctrl + X`.

#### **Step 3: Set Up UFW Firewall**

To secure your server, it's crucial to configure UFW to allow only necessary traffic. Here's how to do it:

1. **Enable UFW and Allow SSH (Port 22):**

   ```bash
   sudo ufw allow 22/tcp
   ```

   This ensures you can still access your server via SSH.

2. **Allow TCP and UDP Traffic on Port 35995:**

   ```bash
   sudo ufw allow 35995/tcp
   sudo ufw allow 35995/udp
   ```

   This is for allowing traffic to the specific service on this port.

3. **Enable UFW:**

   ```bash
   sudo ufw enable
   ```

4. **Verify UFW Status:**

   ```bash
   sudo ufw status
   ```

   You should see that only ports 22, 35995 (TCP and UDP), and potentially other ports you explicitly opened, are allowed. All other inbound traffic will be blocked.

#### **Step 4: Install and Configure Fail2ban**

Fail2ban is a service that monitors your server logs for suspicious activity, such as repeated failed login attempts, and bans the offending IP addresses. Here's how to set it up:

1. **Install Fail2ban:**

   ```bash
   sudo apt install fail2ban
   ```

2. **Create a Local Configuration:**

   Copy the default configuration file to create a local override:

   ```bash
   sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
   ```

3. **Configure SSH Protection:**

   Open the `jail.local` file in a text editor:

   ```bash
   sudo nano /etc/fail2ban/jail.local
   ```

   Locate the `[sshd]` section and ensure it’s enabled:

   ```ini
   [sshd]
   enabled = true
   port = 22
   filter = sshd
   logpath = /var/log/auth.log
   maxretry = 5
   bantime = 10m
   findtime = 10m
   ```

   This configuration will ban an IP address for 10 minutes if it fails to log in 5 times within 10 minutes.

4. **Start and Enable Fail2ban:**

   ```bash
   sudo systemctl start fail2ban
   sudo systemctl enable fail2ban
   ```

5. **Check Fail2ban Status:**

   You can check the status of Fail2ban and see which IPs have been banned using:

   ```bash
   sudo fail2ban-client status sshd
   ```

   This will show you the status of the SSH jail and any banned IPs.

#### **Step 5: Restart Caddy and Apply Changes**

After configuring the Caddyfile and setting up your firewall and Fail2ban, restart Caddy to apply the changes:

```bash
sudo systemctl restart caddy
```

#### **Final Notes**

With this setup, Caddy handles SSL termination and proxies requests to your backend services, UFW ensures that your server is protected by only allowing essential traffic, and Fail2ban provides an additional layer of security by blocking suspicious activity. This configuration is ideal for running web services securely and efficiently on a single server.

Feel free to ask any questions or share your experiences with this setup!

---

This post now includes instructions on how to locate and edit the Caddyfile using `nano`, making it more accessible for users who might not be familiar with where the Caddyfile is located or how to edit it.

-------------------------

