Thread: pillar-or-node-trouble-shooting-steps
0x3639 | 2023-12-03 10:53:52 UTC | #1

Pillars and Nodes have been struggling under the recent load increases.  Here are some ideas to address the potential issues.

## Increase the max number of open files in Linux

To increase the maximum number of open files in Linux, you typically need to adjust the limits in the system configuration. Here's a step-by-step guide:

1. **Check Current Limits**:
   First, check the current limits for your system. Open a terminal and use the following command:
   ```bash
   ulimit -n
   ```
   This will show you the current limit on open files for the current user session.

2. **Temporary Increase**:
   To temporarily increase the limit for the current session, use:
   ```bash
   ulimit -n [new limit]
   ```
   Replace `[new limit]` with the desired number, like `65536`.

3. **Permanent Increase**:
   For a permanent change, you need to edit system configuration files:

   - **Edit Limits Configuration**:
     Open the `/etc/security/limits.conf` file with a text editor (as root or using sudo), and add the following lines:
     ```
     soft nofile 1024
     hard nofile 65536
     ```
     Replace `[soft limit]` and `[hard limit]` with the desired values. The soft limit is the default number of open files, while the hard limit is the maximum number that can be set using `ulimit -n`.

   - **For go-zenon Service**:
     Edit `/etc/systemd/system/go-zenon.service`:
     ```
     [Service]
     LimitNOFILE=65536
     ```

4. **Apply Changes**:
   - After editing the `limits.conf` file, save it and reboot your system for the changes to take effect.
   - If you've modified a systemd service file, reload the systemd configuration with `sudo systemctl daemon-reload`, and then restart the service.

5. **Verify Changes**:
   After rebooting or restarting the service, verify that the changes have been applied by using the `ulimit -n` command again.

Remember, setting these limits too high can affect system stability, so it's important to choose a value that balances your needs with the capabilities of your system.

## Increase the amount of swap memory

To set up a system for dynamically increasing swap space on Linux, you can use a tool like `dphys-swapfile`. This tool is commonly used in Debian-based systems, such as Ubuntu, to manage a dynamic swap file. Here are the general steps to set it up:

### Installing `dphys-swapfile`

1. **Update Your Package Lists**:
   Open a terminal and update your package lists to ensure you get the latest version of the software:
   ```bash
   sudo apt update
   ```

2. **Install `dphys-swapfile`**:
   Install the `dphys-swapfile` package:
   ```bash
   sudo apt install dphys-swapfile
   ```

### Configuring `dphys-swapfile`

1. **Edit the Configuration File**:
   Open the configuration file in a text editor. For example, using `nano`:
   ```bash
   sudo nano /etc/dphys-swapfile
   ```

2. **Configure Swap Settings**:
   In the configuration file, you can set parameters like the size of the swap file. For instance:
   - To set the swap file size to 8GB:
     ```
     CONF_SWAPSIZE=8196
     ```
   - To make the swap file size dynamic based on available RAM, you can comment out the `CONF_SWAPSIZE` line by adding a `#` at the beginning.

3. **Save and Exit**:
   After making your changes, save and exit the editor. In `nano`, this is done by pressing `CTRL+X`, then `Y` to confirm, and `Enter` to save.

### Activating the Swap File

1. **Restart the `dphys-swapfile` Service**:
   Apply the changes by restarting the service:
   ```bash
   sudo systemctl restart dphys-swapfile
   ```

2. **Verify Swap File Creation**:
   Check that the swap is active:
   ```bash
   swapon --show
   ```

   This command will display the active swap files and partitions. Your newly created swap file should be listed.

### Reduce the number of peers in config.json

`sudo nano /root/.znn/config.json`

```
{
    "Producer": {
        "Index": 0,
        "KeyFilePath": "producer",
        "Password": "REDUCE",
        "Address": "REDUCE"
    },
    "Net": {
        "MinPeers": 8,
        "MinConnectedPeers": 8,
        "MaxPeers": 16,
        "MaxPendingPeers": 32
    }
}
```

### Additional Notes

- **Automatic Management**: `dphys-swapfile` will automatically manage the swap file, creating it at boot time and removing it at shutdown.
- **Performance Considerations**: Keep in mind that using swap space can impact system performance, especially if the swap file is used heavily.
- **System Requirements**: Make sure your system has enough disk space for the swap file, especially if you're setting a large fixed size.

This setup provides a basic dynamic swap configuration. For more advanced configurations, refer to the `dphys-swapfile` documentation and your Linux distribution's specific guidelines.

-------------------------

tapwoot | 2023-12-01 18:39:52 UTC | #2

thankyou i needed this

-------------------------

0x3639 | 2023-12-01 18:56:55 UTC | #3

Please try on one node and let us know if it helps.  You can also play around with the swap file size.  If 8g is not enough, increase to some number less than your RAM.  I might try 10G if I had 16G of RAM.

-------------------------

