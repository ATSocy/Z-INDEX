Thread: deploy-go-zenon-from-any-repo-and-any-branch
0x3639 | 2023-08-21 11:17:01 UTC | #1

With all the recent testing I've been doing with `go-zenon` I decided to create a script that will quickly deploy `go-zenon` from any repo and any branch.  

Spin up a VPS then follow these Steps:

1. **Download the Script**: First, you need to download the file from the given URL. If you're on a system with `curl` installed (such as Linux or macOS), you can use the following command:

```
curl -O https://gist.githubusercontent.com/0x3639/979e2b0d2b0acea31dfd30849a524d4a/raw/033043a02103602cf7bfa47e9abfb79286c767c2/deploy-go-zenon.sh
```
This command will download the file and save it with the name `deploy-go-zenon.sh` in your current directory.

2. **Give Execution Permissions**: Before you can run the script, you'll need to give it executable permissions. To do this, run:

```
chmod +x deploy-go-zenon.sh
```

3. **Run the Script**: Now, you can run the script using the following command:

```
sudo ./deploy-go-zenon.sh
```

4. **Optional: Examine the Script First**: Before running any script, especially one from the internet, it's good practice to inspect its contents to ensure there's nothing malicious or unintentional that might harm your system.You can view the contents of the file using a text editor or with commands like `cat`:

```
cat deploy-go-zenon.sh
```

Read through the script to ensure you understand its operations and feel comfortable with its actions.

And that's it! These steps should allow you to download and execute the script from your command line.

-------------------------

