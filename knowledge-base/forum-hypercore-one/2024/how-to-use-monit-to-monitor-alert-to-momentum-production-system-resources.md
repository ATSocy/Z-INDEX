Thread: how-to-use-monit-to-monitor-alert-to-momentum-production-system-resources
0x3639 | 2023-12-02 18:09:04 UTC | #1

Let's setup Monit to monitor `/var/log/syslog` to ensure your Pillar is producing momentums.  We do that by using Monit to check if a certain value ("Height") in the `syslog` is incrementing with each check. We use a custom script that Monit can execute. Monit itself does not have built-in functionality for parsing specific values within log files, but it can easily trigger scripts based on certain conditions.

Here's a step-by-step guide on how you can set this up:

#### Step 1: Write a Script to Check the Log File

Create a script to monitor the `/var/log/syslog` for specific changes.

* **Script Content:**

```
#!/bin/bash

LOG_FILE="/var/log/syslog"
LAST_HEIGHT_FILE="/path/to/last_height.txt"
SEARCH_PATTERN="\[Momentum inserted\] Height:"

# Extract the latest height value from the log file
latest_height=$(grep "$SEARCH_PATTERN" "$LOG_FILE" | tail -1 | awk -F'Height: ' '{print $2}' | awk -F', ' '{print $1}')

# Debug: Print the latest height
echo "Latest height extracted: $latest_height"

# Read the last height value stored
last_height=$(cat "$LAST_HEIGHT_FILE" 2>/dev/null || echo 0)

# Compare and update
if [ -z "$latest_height" ]; then
    echo "Pattern not found"
    exit 1
elif [ "$latest_height" -le "$last_height" ]; then
    echo "Height not incrementing"
    exit 1
else
    echo "$latest_height" > "$LAST_HEIGHT_FILE"
    exit 0
fi

```

* **Make the Script Executable:**

```
chmod +x /path/to/your/script.sh
```

#### Step 2: Configure Monit to Use the Script

Follow these steps to configure Monit:

1. **Locate or Create a Monit Configuration File:**
  * Edit the main configuration file: `/etc/monit/monitrc`
  * Or, create a new file in `/etc/monit/conf.d/`, like `logcheck.conf`.
2. **Add the Service Entry with Interval:** Add the following to your configuration file, including the interval directive:

```
check program check_height with path "/path/to/your/script.sh"
    every 2 cycles
    if status != 0 then alert
```

  * This example sets Monit to run the script every 2 cycles. If your Monit is configured to check every minute, this means the script will be run every 2 minutes.
3. **Save and Exit the Configuration File.**
4. **Check Monit Configuration for Syntax Errors:**

```
sudo monit -t
```

5. **Reload or Restart Monit:**

```
sudo monit reload
```
or

```
sudo service monit restart
```

### Step 3: Configure Email Alerts in Monit

#### 1. Edit the Monit Configuration File

* Open the main Monit configuration file, typically located at `/etc/monit/monitrc`:

```
sudo nano /etc/monit/monitrc
```

#### 2. Configure Mail Server Settings

* Locate or add a section in the configuration file for setting up the mail server. Here's an example using Gmail's SMTP server:

```
set mailserver smtp.gmail.com port 587
    username "your.email@gmail.com" password "yourpassword"
    using tlsv1
    with timeout 30 seconds
```
* Replace `your.email@gmail.com` and `yourpassword` with your actual Gmail email address and password. If you're using two-factor authentication with Gmail, you'll need to generate an app-specific password.
* If you're using a different email provider, you'll need to use their specific SMTP server settings.

#### 3. Set the Alert Recipient

* Define whom Monit should send the email alerts to:

```
set alert your.email@example.com
```
* Replace `your.email@example.com` with the email address where you want to receive the alerts.

#### 4. Customize Email Format (Optional)

* You can customize the email format for alerts. For example:

```
set mail-format {
    from: monit@yourdomain.com
    subject: Monit Alert -- $EVENT $SERVICE
    message: Monit $ACTION $SERVICE at $DATE on $HOST: $DESCRIPTION.
}
```
* Adjust the `from`, `subject`, and `message` fields as needed.

#### 5. Save and Close the Configuration File

* After making these changes, save and close the file.

#### 6. Test the Email Setup

* To ensure that the email setup works, you can force Monit to send a test alert:

```
sudo monit reload
sudo monit status
```
* This reloads Monit with the new configuration and the status command can help in confirming if Monit is running correctly.

#### 7. Reload or Restart Monit

* Apply your changes by reloading or restarting Monit:

```
sudo monit reload
```
or

```
sudo service monit restart
```

## Additional Monitoring

### System Health
Monitor and alert system health.
`sudo nano /etc/monit/conf.d/system_monitor.conf`
```
check device root with path /dev/sda3
    if SPACE usage > 80% for 2 cycles then alert

check system $HOST
    if loadavg (1min) per core > 2 for 5 cycles then alert
    if loadavg (5min) per core > 1.5 for 10 cycles then alert
    if cpu usage > 80% for 10 cycles then alert
    if memory usage > 75% then alert
    if swap usage > 25% then alert
```

### Network Usage
Monitor and alert network usage.
`sudo nano /etc/monit/conf.d/network_usage.conf`
```
## Check a network link status (up/down), link capacity changes, saturation
## and bandwidth usage.
#
  check network public with interface eth0
    if failed link then alert
    if changed link then alert
    if saturation > 90% then alert
    if download > 10 MB/s then alert
    if total uploaded > 1 GB in last hour then alert
```
### Orchestrator Messages
Monitor Orchestrator messages for potential errors
`sudo nano /etc/monit/conf.d/orchestrator_logs.conf`

```
check file syslog with path /var/log/syslog
    if match "KeyGen threshold was not met" then alert
    if match "orchestrator successfully started" then alert
    if match "websocket: close 1006 (abnormal closure): unexpected EOF" then alert
    if match "websocket: close 1001 (going away): upstream went away" then alert
    if match "Stopping orchestrator" then alert
    if match "Started ECDSA Keygen" then alert
    if match "error signing unwrap" then alert
```

#### Notes:

* Ensure the script has read permissions for `/var/log/syslog`.
* Adjust the script as needed for your log file format.
* Configure Monit with your email settings in `monitrc` for alerts.
* Check `/var/log/monit.log` for logs and troubleshooting.
* **Security Considerations:** Storing plain text passwords in configuration files is not recommended for security reasons. Consider using environment variables or other secure methods to store sensitive information.
* **Using a Different Email Provider:** If you're using a different email provider (other than Gmail), you'll need to use their SMTP server settings. Make sure to use the correct server address, port, and encryption method.
* **Spam Filters:** Sometimes, automated alert emails may be flagged as spam. Ensure that your email is configured to allow these messages to reach your inbox.

-------------------------

