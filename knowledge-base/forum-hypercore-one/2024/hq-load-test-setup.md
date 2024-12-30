Thread: hq-load-test-setup
0x3639 | 2024-12-26 22:49:31 UTC | #1

Below is a **step-by-step guide** on how to set up and run a **HQZD load test** using the `nomctl` CLI. This tutorial will show you how to:

1. Create a Python virtual environment  
2. Install dependencies  
3. Configure your `.env` file  
4. Use three Python scripts (`run_loadtest.py`, `receive.py`, `send_spam.py`)  
5. Spin up the load test in the background with `nohup`

---

# 1. Directory Structure

First, decide on your directory layout. One recommended approach is:

```
/someParentDirectory
├── /loadtest
│    ├── .env
│    ├── requirements.txt
│    ├── run_loadtest.py
│    ├── receive.py
│    └── send_spam.py
└── /nomctl
     └── /build
         └── nomctl
```

- **`/nomctl/build/nomctl`** is the compiled Nomctl CLI executable.  
- **`/loadtest`** contains your Python scripts and configuration.

---

# 2. Create and Populate `.env`

In your `/loadtest` folder, create a file named `.env` with the following contents (edit to your needs):

```bash
# .env

# Node URL for the -u flag
URL="http://127.0.0.1:35997"

# Password for the -p flag (not displayed in logs)
PASSWORD="Don'tTrust.Verify"

# Space-separated addresses (these must be valid addresses on your Zenon network)
ADDRESSES="z1qz529j9d2vu0xan22w0ksr6xr6r8cuftrmhmlp z1qpg8v63m534t2vv09yzndv9gu9t6gyrvq3n6qv"
```

Change:
- `URL` to point to your Zenon node IP and port.  
- `PASSWORD` to your actual password (it won’t be printed in logs).  
- `ADDRESSES` to the address(es) you want to send from.

---

# 3. `requirements.txt`

In the same `/loadtest` folder, create `requirements.txt`:

```txt
python-dotenv==1.0.0
```

This ensures we can load environment variables from `.env`. If you need other Python libraries, add them here.

---

# 4. Create the Python Scripts

You need **three** Python scripts in `/loadtest`:

## A. `receive.py`

This script handles the **receive** process with the `-n 26` flag. It runs `nomctl receiveAll` every X seconds (default 60).  

```python
#!/usr/bin/env python3
import os
import time
import argparse
import subprocess
from dotenv import load_dotenv

# Load environment variables from .env
load_dotenv()

def main():
    parser = argparse.ArgumentParser(description="Run receiveAll every X seconds.")
    parser.add_argument(
        "--interval",
        type=int,
        default=60,
        help="Number of seconds between each receiveAll execution (default: 60)."
    )
    args = parser.parse_args()

    url = os.getenv("URL", "http://127.0.0.1:35997")
    password = os.getenv("PASSWORD", "Don'tTrust.Verify")

    # Adjust path to nomctl if needed (up one level to /nomctl/build/)
    nomctl_path = "../nomctl/build/nomctl"

    receive_command = [
        nomctl_path,
        "-hq", "znn-cli",
        "-u", url,
        "-k", "hqz",
        "-p", password,
        "-n", "26",
        "receiveAll"
    ]

    print(f"[receive.py] Starting receive loop. Interval = {args.interval}s")

    while True:
        # Create a safe command string for logging (mask password)
        safe_command_str = ' '.join("****" if arg == password else arg for arg in receive_command)
        print(f"[receive.py] Executing: {safe_command_str}")

        try:
            subprocess.run(receive_command, check=True)
        except subprocess.CalledProcessError as e:
            print(f"[receive.py] Error running receiveAll: {e}")

        # Sleep for the specified interval
        time.sleep(args.interval)

if __name__ == "__main__":
    main()
```

---

## B. `send_spam.py`

This script spawns multiple worker threads to **send** from the addresses you put in `.env`. We use **serialization** so that no two threads send concurrently from the **same** address—this helps avoid the “previous block is missing” error.

```python
#!/usr/bin/env python3
import os
import time
import threading
import argparse
import subprocess
from dotenv import load_dotenv

# Load environment variables from .env
load_dotenv()

def worker_thread(thread_id, interval, nomctl_path, url, password, addresses, address_locks):
    """
    Each worker:
      - Loops forever
      - Sends to each address in turn
      - Acquires a lock per address to avoid concurrent sends from the same address
      - Sleeps 'interval' seconds after each send
    """
    send_command_base = [
        nomctl_path,
        "-hq", "znn-cli",
        "-u", url,
        "-k", "hqz",
        "-p", password,
        "send"
    ]
    
    print(f"[Thread {thread_id}] Starting worker loop...")
    while True:
        for address in addresses:
            # Acquire the lock for this address (serialization)
            with address_locks[address]:
                cmd = send_command_base + [address, "1", "zts1utylzxxxxxxxxxxx6agxt0"]

                # Create a "safe" command string for logging (mask the password)
                safe_cmd_str = ' '.join("****" if arg == password else arg for arg in cmd)
                print(f"[Thread {thread_id}] Executing: {safe_cmd_str}")

                try:
                    subprocess.run(cmd, check=True)
                except subprocess.CalledProcessError as e:
                    print(f"[Thread {thread_id}] Error running send command: {e}")
            
            time.sleep(interval)

def main():
    parser = argparse.ArgumentParser(description="Spin up multiple concurrent send workers (serialized per address).")
    parser.add_argument(
        "--workers",
        type=int,
        default=1,
        help="Number of concurrent workers to spawn (default: 1)."
    )
    parser.add_argument(
        "--interval",
        type=int,
        default=5,
        help="Seconds to wait between sends per worker (default: 5)."
    )
    args = parser.parse_args()
    
    # Read from .env or fallback
    url = os.getenv("URL", "http://127.0.0.1:35997")
    password = os.getenv("PASSWORD", "Don'tTrust.Verify")
    addresses_str = os.getenv("ADDRESSES", "")
    if not addresses_str.strip():
        print("[send_spam.py] No addresses found in .env. Exiting.")
        return
    
    addresses = addresses_str.split()
    
    # Path to nomctl
    nomctl_path = "../nomctl/build/nomctl"

    # Create a lock for each address
    address_locks = {addr: threading.Lock() for addr in addresses}

    # Spawn worker threads
    threads = []
    for i in range(args.workers):
        t = threading.Thread(
            target=worker_thread,
            args=(i, args.interval, nomctl_path, url, password, addresses, address_locks),
            daemon=True
        )
        t.start()
        threads.append(t)

    # Keep main thread alive
    for t in threads:
        t.join()

if __name__ == "__main__":
    main()
```

---

## C. `run_loadtest.py`

Finally, `run_loadtest.py` starts **both** `receive.py` and `send_spam.py` automatically. It waits indefinitely until you hit **Ctrl + C**, at which point it will terminate both child processes.

```python
#!/usr/bin/env python3
import argparse
import subprocess
import time

def main():
    parser = argparse.ArgumentParser(
        description="Run both receive.py and send_spam.py automatically."
    )
    parser.add_argument(
        "--receive-interval",
        type=int,
        default=60,
        help="Interval for receive.py (default: 60)."
    )
    parser.add_argument(
        "--send-workers",
        type=int,
        default=1,
        help="Number of workers for send_spam.py (default: 1)."
    )
    parser.add_argument(
        "--send-interval",
        type=int,
        default=5,
        help="Interval (in seconds) between sends in send_spam.py (default: 5)."
    )
    args = parser.parse_args()

    # Start receive.py
    receive_cmd = [
        "python3",
        "receive.py",
        "--interval",
        str(args.receive_interval)
    ]
    print("[run_loadtest.py] Spawning receive.py process...")
    receive_process = subprocess.Popen(receive_cmd)

    # Start send_spam.py
    send_cmd = [
        "python3",
        "send_spam.py",
        "--workers",
        str(args.send_workers),
        "--interval",
        str(args.send_interval)
    ]
    print("[run_loadtest.py] Spawning send_spam.py process...")
    send_process = subprocess.Popen(send_cmd)

    try:
        # Keep this script running
        while True:
            time.sleep(1)
    except KeyboardInterrupt:
        print("[run_loadtest.py] Caught KeyboardInterrupt, shutting down...")
        # Terminate child processes
        receive_process.terminate()
        send_process.terminate()

if __name__ == "__main__":
    main()
```

---

# 5. Install Dependencies & Run the Scripts

### A. Create a Python Virtual Environment (Recommended)

1. **Change** directory to `/loadtest`:
   ```bash
   cd /someParentDirectory/loadtest
   ```
2. **Create** a venv:
   ```bash
   python3 -m venv venv
   ```
3. **Activate** the venv:
   - **Linux/macOS**:
     ```bash
     source venv/bin/activate
     ```
   - **Windows (Powershell)**:
     ```powershell
     .\venv\Scripts\Activate.ps1
     ```

### B. Install Dependencies

```bash
pip install -r requirements.txt
```

### C. Make Scripts Executable (Optional)

```bash
chmod +x run_loadtest.py receive.py send_spam.py
```

### D. Run the Load Test

1. **Simple** run (foreground):
   ```bash
   ./run_loadtest.py --receive-interval 60 --send-workers 2 --send-interval 3
   ```
   This means:
   - The **receive** script runs every **60 seconds**.  
   - The **send** script uses **2** worker threads, each sending every **3 seconds**.

2. **Stop** with **Ctrl + C**. This stops both `receive.py` and `send_spam.py`.

---

# 6. Run in Background with `nohup`

If you want the process to keep running even after you log out, use `nohup`:

```bash
nohup python3 run_loadtest.py \
    --receive-interval 60 \
    --send-workers 2 \
    --send-interval 3 \
    > loadtest.log 2>&1 &
```

- **`> loadtest.log 2>&1`** writes all output to `loadtest.log`.  
- **`&`** runs it in the background.

Check the log:

```bash
tail -f loadtest.log
```

Stop the background job:

1. Find its PID:
   ```bash
   ps aux | grep run_loadtest.py
   ```
2. Kill it:
   ```bash
   kill <PID>
   ```

---

# 7. Common Errors & Tips

- **“account-block previous block is missing”**  
  - Means you’re sending multiple transactions from the same address **too quickly** or the chain hasn’t processed the previous block yet.  
  - We’ve partially mitigated this by serializing sends per address.  
  - If you still get this, **increase** `receiveAll` frequency, or **add** more addresses so you’re not hammering one address.

- **No `.env` file**  
  - Make sure `.env` is in `/loadtest` and you set your `URL`, `PASSWORD`, and `ADDRESSES`.

- **File not found**  
  - Verify that `../nomctl/build/nomctl` actually exists. Adjust `nomctl_path` if your layout is different.

---

# Conclusion

That’s it! Once set up, you have:

1. **`run_loadtest.py`** as your main entry point.  
2. **`receive.py`** handling inbound transactions with `receiveAll -n 26`.  
3. **`send_spam.py`** sending from your addresses with concurrency, but **serialized** per address.  

With these scripts, you can:

- **Test** your HQZD node.  
- **Collect logs** on performance and errors.  
- **Experiment** with different intervals, workers, and addresses for stress testing.

Feel free to customize and **happy load testing**!

-------------------------

