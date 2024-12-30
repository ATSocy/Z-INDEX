Thread: automated-script-to-build-and-deploy-the-orchestrator
0x3639 | 2023-08-28 13:46:56 UTC | #1

**How to Download and Run the Orchestrator Deployment Script**

[Note: Written by ChatGPT] In this post, I'll guide you through the process of downloading and running a script that deploys the Orchestrator. Don't worry if you're not a computer programmer; I'll break it down step by step.

### Step 1: Downloading the Script
1. `wget https://gist.githubusercontent.com/0x3639/eda9f69e7bb1043e88a5042206c1fa94/raw/fe90e97bd7e41707b2b03e54be13afff82dc0df0/deploy-orchestrator.sh`

### Step 2: Make The Script Executable 
1. Make the script executable with the command: `chmod +x deploy-orchestrator.sh`

### Step 3: Gathering Required Information

Before running the script, ensure you have the following information at hand:

1. **ZNN Node Address**: This is the address of your ZNN node. 
2. **ETH Node Address**: The address of your Ethereum node.  Follow these instructions to [setup an ETH node](https://forum.hypercore.one/t/how-to-setup-an-eth-node-for-the-orchestrator/84). 
3. **Producer KeyFile Passphrase**: A passphrase for the Producer KeyFile. Ensure you keep this passphrase safe and confidential.

### Step 4: Run the Script
1. Run the script with the command: `./deploy-orchestrator.sh`
2. Follow the on-screen prompts to complete the deployment.

### What Does the Script Do?
The script is designed to deploy the Orchestrator, a service that manages various tasks. Here's a simplified breakdown of its functions:

1. **Check for Required Programs**: The script checks if certain programs (like `gcc`, `go`, and `jq`) are installed on your computer. If not, it installs them for you.
2. **Collect Information**: It will ask you for specific details like your ZNN node address, ETH node address, and a passphrase. These details are essential for the Orchestrator's configuration.
3. **Download and Install Orchestrator**: The script will download the Orchestrator from its GitHub repository, compile it, and install it on your system.
4. **Configuration**: It modifies configuration files to ensure the Orchestrator runs with the correct settings.
5. **Service Creation**: The script sets up the Orchestrator as a system service, ensuring it starts automatically and runs in the background.

-------------------------

