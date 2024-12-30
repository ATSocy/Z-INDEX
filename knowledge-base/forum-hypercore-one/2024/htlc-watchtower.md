Thread: htlc-watchtower
vilkris | 2023-05-30 07:02:21 UTC | #1

The idea of a service that would monitor and automatically proxy unlock HTLCs has been floating around for a while now. I decided to start writing a simple "watchtower" service that does this and I've been testing it out on the HyperCore testnet.

### For the non-technical reader: what's the point of this?
When joining a P2P swap in Syrius, Syrius will automatically scan for the swap's secret (also known as the preimage) and complete the swap automatically. The caveat is that for this to work Syrius has to be running after the preimage has been published but before the swap expires.

There are many reasons that could cause Syrius to not be able to automatically complete the swap, such as:
* Syrius auto locks itself -> the unlock transaction can't be sent because the keystore is locked.
* The user doesn't realize Syrius has to be running.
* A power outage or hardware failure.
* Syrius loses its connection to a node.
* A bug in Syrius.

If the user is not vigilant during the swap, making sure Syrius is running as expected, the user can lose access to the funds that were deposited to them and will be left empty handed.

Fortunately, NoM's embedded HTLC contract supports unlocking HTLCs by proxy and the watchtower service can utilize this feature.

### The watchtower service
The HTLC Watchtower is meant to be a service that anyone can run on a server with relative ease. The watchtower will constantly monitor the embedded HTLC contract and automatically unlock an HTLC when Syrius fails to unlock it for the user. If a watchtower is running it would significantly reduce the risk of users losing funds. Having multiple watchtowers running simultaneously would be even better.

### How it works
The watchtower stores all the HTLCs that are created on the network into a database. When an HTLC is unlocked, it pairs the revealed preimage with all the HTLCs that match the preimage's hashlock in the database.

The watchtower periodically checks the database for HTLCs that have a known preimage and will unlock an HTLC if the recipient address allows it (by default all addresses allow it).

Only active HTLCs are stored in the database and any expired or unlocked HTLCs are removed.

### Setup requirements
The watchtower is designed to be simple to run, with minimal dependencies and requirements.

It will automatically manage the wallet that it uses to send the unlock transactions. The first time the watchtower is run it will request Plasma to be fused to the watchtower address and continue operation once the Plasma requirement is met.

The watchtower can be run on a VPS and it needs a connection to a node (preferably local).

### Benchmarking
Even though the expired and unlocked HTLCs are removed from the database, an adversary could spam the HTLC contract with HTLCs that expire after a long time, filling up the database.

**Some database benchmarks with the current data model:**
DB size with 1M records -> ~900 MB
Writing 1M records to the database -> ~2600 msecs
Adding a preimage to 1M records with the matching hashlock -> ~2600 msecs

### Code
The watchtower's code (WIP) can be found [here](https://github.com/hypercore-one/htlc-watchtower).

-------------------------

sol | 2023-05-09 15:03:32 UTC | #2

Great work, Vilkris!
The combination of proxy unlocking and watchtowers will make atomic swaps even better for our users. Participants no longer need to be online to receive their funds. 👏

-------------------------

0x3639 | 2023-05-09 15:55:01 UTC | #3

Amazing.  I will start running one.

I assume [this file](https://github.com/zenon-tools/htlc-watchtower/blob/main/example.config.yaml) needs to be renamed to `config.yaml` and updated with the correct node.  

Any other instructions before I run it?  Do I need to open any ports and does it need a public static IP?

-------------------------

sol | 2023-05-09 17:28:27 UTC | #4

It's basically a client, like znn-cli or Syrius. Shouldn't need to open any ports.

I reviewed the code and really like the way you designed the application. Well done! :)

I'll test it out later, but the instructions should be:
1. ```git clone https://github.com/zenon-tools/htlc-watchtower.git && cd htlc-watchtower```
2. Default node is `ws://127.0.0.1:35998` and the script will use that node's chain identifier.
   - If you wish to change this, you may create a `config.yaml` in the root directory, following [this template](https://github.com/zenon-tools/htlc-watchtower/blob/main/example.config.yaml).
3. Once the config is set, run this: `dart run src/main.dart`
   - or compile exe with: `dart compile exe -o .\bin\htlc-watchtower .\src\main.dart`

I came across this issue when trying to run the application. Maybe we need to regenerate the .g file?

```
dart run .\src\main.dart
src/models/database/htlc_data.g.dart:16:24: Error: Constant evaluation error:
const HtlcDataSchema = CollectionSchema(
                       ^
../../AppData/Local/Pub/Cache/hosted/pub.dev/isar-3.1.0+1/lib/src/schema/collection_schema.dart:24:24: Context: This assertion failed with message: Outdated generated code. Please re-run code generation using the latest generator.
          Isar.version == version,
                       ^
src/models/database/htlc_data.g.dart:16:7: Context: While analyzing:
const HtlcDataSchema = CollectionSchema(
      ^
```

-------------------------

georgezgeorgez | 2023-05-09 17:03:19 UTC | #5

Very cool!

I don't see why this can't receive some AZ funding.

In the future, we probably want the ability to watch for HTLC unlocks on BTC even if we can't proxy unlock there yet without covenants.

Some configuration to exclude certain HTLCs may allow operators to mitigate/prevent attacks.
E.g only unlocking whitelisted tokens or for whitelisted addresses
(such as delegators, but the tool would only need to expose an API to modify the list)
Perhaps only unlocking after a delay, or within a certain timeframe to expiration, although I imagine that complicates it a bit needing a queue system.

The introduction of dynamic plasma also would make things more interesting if users can choose the amount of plasma to allocate to a tx.

I am all for allowing the community to help each other without explicit incentives.
But I also don't think we can make that assumption.
Non-default configuration to allow people to run the tool for more selfish reasons will lead to greater adoption imho.

-------------------------

vilkris | 2023-05-09 19:42:58 UTC | #6

I'll have to write the instructions how to set this up, but if you want to try it, what Sol said should suffice.

-------------------------

0x3639 | 2023-05-09 19:43:38 UTC | #7

I'm going to set this up as a Dockerfile.  Easier to run them for testnet and mainnet

https://medium.com/google-cloud/build-slim-docker-images-for-dart-apps-ee98ea1d1cf7

I'm not familiar with Dart, but I assume this app does not rely on [dart:mirrors](https://api.dart.dev/stable/2.10.2/dart-mirrors/dart-mirrors-library.html).   @sol is that a reasonable assumption?

> Dart app can be compiled ahead-of-time (AOT) into machine code using [dart2native](https://dart.dev/tools/dart2native). This provides a dramatically improved startup time.
> 
> Unfortunately, there is one catch. Currently dart2native doesn’t support reflection (which relies on [dart:mirrors](https://api.dart.dev/stable/2.10.2/dart-mirrors/dart-mirrors-library.html)). [Metadata annotations](https://dart.dev/guides/language/language-tour#metadata) tend to be popular in various web server, data modeling, serialization, and dependency injection frameworks and libraries, for example.

-------------------------

vilkris | 2023-05-09 19:43:40 UTC | #8

Would you mind running `dart run build_runner build --delete-conflicting-outputs` to see if regenerating the file solves the issue?

If it does I'll have to remove the generated file from git and add that command to the instructions.

-------------------------

vilkris | 2023-05-09 19:58:06 UTC | #9

[quote="georgezgeorgez, post:5, topic:50"]
I don’t see why this can’t receive some AZ funding.
[/quote]
I'm considering requesting AZ funds for this at some point.

[quote="georgezgeorgez, post:5, topic:50"]
In the future, we probably want the ability to watch for HTLC unlocks on BTC even if we can’t proxy unlock there yet without covenants.
[/quote]
Adding monitoring for BTC unlocks would definitely be interesting.

[quote="georgezgeorgez, post:5, topic:50"]
Perhaps only unlocking after a delay, or within a certain timeframe to expiration, although I imagine that complicates it a bit needing a queue system.
[/quote]
Making the unlock happen only within a certain timeframe to expiration should only require a modification to the database query. This could make sense to add.

[quote="georgezgeorgez, post:5, topic:50"]
I am all for allowing the community to help each other without explicit incentives.
But I also don’t think we can make that assumption.
Non-default configuration to allow people to run the tool for more selfish reasons will lead to greater adoption imho.
[/quote]

This is true. At some point the resources required to run services like this start piling up, and with no explicit incentives, it can be hard to justify the effort and cost.

-------------------------

vilkris | 2023-05-09 20:04:20 UTC | #10

It shouldn't rely on that.

-------------------------

0x3639 | 2023-05-09 20:56:44 UTC | #11

Going to try this `Dockerfile`

```
# Specify the Dart SDK base image version using dart:<version> (ex: dart:2.12)
FROM dart:stable AS build

# Resolve app dependencies.
WORKDIR /app
COPY pubspec.* ./
RUN dart pub get

# Copy app source code and AOT compile it.
COPY . .
# Ensure packages are still up-to-date if anything has changed
RUN dart pub get --offline
RUN dart compile exe src/main.dart -o src/main

# Build minimal serving image from AOT-compiled `/main` and required system
# libraries and configuration files stored in `/runtime/` from the build stage.
FROM scratch
COPY --from=build /runtime/ /
COPY --from=build /app/src/main /app/src/

# Start service.
CMD ["/app/src/main"]
```

-------------------------

vilkris | 2023-05-09 20:44:02 UTC | #12

If I'm reading that correctly you're going to have to replace the `bin` directory with `src`, since that's where the `main.dart` file is in this project.

-------------------------

0x3639 | 2023-05-09 20:50:01 UTC | #13

Updated.  I'll give that a try.  Does the `config.yaml` file need to be under the `/app/src/` directory?

-------------------------

vilkris | 2023-05-09 20:53:09 UTC | #14

```
RUN dart compile exe src/main.dart -o bin/main
```
I think you need to change the output to `src/main` here. The config.yaml file has to be in the same directory as the binary, so it would go to `/app/src/`.

-------------------------

0x3639 | 2023-05-09 20:58:47 UTC | #15

Got it.  I corrected that error and got the following build error in Docker.  I will try to fix this myself.

```
 > [build 7/7] RUN dart compile exe src/main.dart -o src/main:                                                                                                  
#0 3.373 Info: Compiling with sound null safety.                                                                                                                
#0 3.373 src/models/database/htlc_data.g.dart:16:24: Error: Constant evaluation error:                                                                          
#0 3.373 const HtlcDataSchema = CollectionSchema(                                                                                                               
#0 3.373                        ^                                                                                                                               
#0 3.373 /root/.pub-cache/hosted/pub.dev/isar-3.1.0+1/lib/src/schema/collection_schema.dart:24:24: Context: This assertion failed with message: Outdated generated code. Please re-run code generation using the latest generator.
#0 3.373           Isar.version == version,
#0 3.373                        ^
#0 3.373 src/models/database/htlc_data.g.dart:16:7: Context: While analyzing:
#0 3.373 const HtlcDataSchema = CollectionSchema(
#0 3.373       ^
#0 3.375 Error: AOT compilation failed
#0 3.375 Generating AOT kernel dill failed!
------
Dockerfile:13
--------------------
  11 |     # Ensure packages are still up-to-date if anything has changed
  12 |     RUN dart pub get --offline
  13 | >>> RUN dart compile exe src/main.dart -o src/main
  14 |     
  15 |     # Build minimal serving image from AOT-compiled `/main` and required system
--------------------
ERROR: failed to solve: process "/bin/sh -c dart compile exe src/main.dart -o src/main" did not complete successfully: exit code: 64
```

-------------------------

0x3639 | 2023-05-09 21:12:55 UTC | #16

get the following when compiling locally

```
x3639@0x3639-NoM:~/Github/htlc-watchtower$ dart run src/main.dart
src/models/database/htlc_data.g.dart:16:24: Error: Constant evaluation error:
const HtlcDataSchema = CollectionSchema(
                       ^
../../.pub-cache/hosted/pub.dev/isar-3.1.0+1/lib/src/schema/collection_schema.dart:24:24: Context: This assertion failed with message: Outdated generated code. Please re-run code generation using the latest generator.
          Isar.version == version,
                       ^
src/models/database/htlc_data.g.dart:16:7: Context: While analyzing:
const HtlcDataSchema = CollectionSchema(
      ^
x3639@0x3639-NoM:~/Github/htlc-watchtower$ 
```

-------------------------

vilkris | 2023-05-09 21:13:10 UTC | #17

That's the same error Sol was having.

You can try to add this command before the compile command:
```
dart run build_runner build --delete-conflicting-outputs
```

-------------------------

0x3639 | 2023-05-09 21:15:52 UTC | #18

[quote="vilkris, post:8, topic:50"]
dart run build_runner build --delete-conflicting-outputs
[/quote]

worked.  What was wrong with my original commands?  And should I run that in the Dockerfile?  I assume yes?

```
x3639@0x3639-NoM:~/Github/htlc-watchtower$ dart run build_runner build --delete-conflicting-outputs
Building package executable... (7.8s)
Built build_runner:build_runner.
[INFO] Generating build script completed, took 426ms
[INFO] Precompiling build script... completed, took 8.1s
[INFO] Building new asset graph completed, took 1.1s
[INFO] Checking for unexpected pre-existing outputs. completed, took 3ms
[INFO] Generating SDK summary completed, took 4.9s
[INFO] Running build completed, took 5.8s
[INFO] Caching finalized dependency graph completed, took 26ms
[INFO] Succeeded after 5.9s with 2 outputs (5 actions)
x3639@0x3639-NoM:~/Github/htlc-watchtower$ dart run src/main.dart
INFO: 2023-05-09 16:13:59.160817: Initializing websocket connection ...
INFO: 2023-05-09 16:13:59.458321: Websocket connection successfully established
INFO: 2023-05-09 16:13:59.469041: Connected to node ws://public.deeznnodez.com:35998
INFO: 2023-05-09 16:13:59.507042: Node is in sync
INFO: 2023-05-09 16:14:00.426838: {"baseAddress":"z1qzyvpp5aylgthynlxv8kgv23n7ny9usauwcr95","crypto":{"argon2Params":{"salt":"0x93bdafabfc4041a71c73b172acf12508"},"cipherData":"0x1b6d0d090255d4e89e2b84707343f58540a1ea93dcb934c9ab9e944214139b76b636cd037c032396854ad9191f9e85de","cipherName":"aes-256-gcm","kdf":"argon2.IDKey","nonce":"0x55014ff9cdcb5fc790fc156c"},"timestamp":1683666840,"version":1}
INFO: 2023-05-09 16:14:00.428235: Created keystore for watchtower.
INFO: 2023-05-09 16:14:00.474322: Loading ./libargon2_ffi_plugin.so from path /home/x3639/.pub-cache/git/znn_sdk_dart-abf887d30311494d7e6cd87b2d74b87f55d37abd/lib/src/argon2/blobs/./libargon2_ffi_plugin.so
INFO: 2023-05-09 16:14:01.096639: The watchtower does not have enough Plasma. Please fuse at least 120 QSR to address: z1qzyvpp5aylgthynlxv8kgv23n7ny9usauwcr95
INFO: 2023-05-09 16:14:01.096873: Waiting for Plasma
```

-------------------------

vilkris | 2023-05-09 21:20:11 UTC | #19

Yes the Docker file needs it. That command auto-generates a file needed for the database. I thought it wouldn't be needed but it is.

-------------------------

0x3639 | 2023-05-09 21:29:23 UTC | #20

[quote="vilkris, post:19, topic:50"]
auto-generates a file
[/quote]
Looks like it makes this file `libisar.so`  Does this filed need to persist?

-------------------------

vilkris | 2023-05-10 06:44:53 UTC | #21

It generates the schema file for the database's data model: `htlc_data.g.dart` This file has to exist.
The `libisar.so` library is automatically downloaded by the database when it initializes itself for the first time. I'm not 100% sure if this works as expected with Docker.

-------------------------

0x3639 | 2023-05-10 10:10:07 UTC | #22

I can get it to build in docker, just can't run it.  probably b/ I'm missing the DB. 

Does `main` only need `htlc_data.g.dart` and `config.json` to run after being built?  And it seems like `htlc_data.g.dart`  needs to persist on a volume?  I can get docker to do this.  I'm going to add this to znndNode if I can get it to work.

-------------------------

vilkris | 2023-05-10 12:46:31 UTC | #23

`htlc_data.g.dart` is a source file used at compile time. Are you getting some error when trying to run it?

I'm not really familiar with Docker, but these commands should be enough to build and run the service (on Ubuntu). In the top level directory:
```
dart pub get
dart run build_runner build --delete-conflicting-outputs
mkdir build
dart compile exe src/main.dart -o build/htlc-watchtower
cp example.config.json build/config.json
```
This will build the `htlc-watchtower` binary into a directory named `build`. The `libisar.so` library has to be in the `build` directory as well. The service will automatically attempt to download it when its run, but maybe this doesn't work with Docker.

To download the library on command line in Ubuntu this should work:
```
wget https://github.com/isar/isar/releases/download/3.1.0/libisar_linux_x64.so -O build/libisar.so
```

-------------------------

0x3639 | 2023-05-10 12:23:40 UTC | #24

perfect.  this is exactly what I need.  I'll get this running and report back.

-------------------------

vilkris | 2023-05-10 13:15:50 UTC | #25

I added this option to the config.json: `unlock_threshold_in_minutes`

It can be used to configure a custom threshold for how much time is left until expiration before the watchtower unlocks an HTLC.

The default is 60 minutes, which means that the watchtower will unlock an HTLC once it is 60 minutes away from expiring. The minimum it can be set to is 30 minutes.

-------------------------

0x3639 | 2023-05-10 18:30:45 UTC | #26

With this last change, I get the following error when running locally on Ubuntu

```
x3639@0x3639-NoM:~/Github/htlc-watchtower/build$ ./htlc-watchtower 
INFO: 2023-05-10 13:25:44.132974: Initializing websocket connection ...
SEVERE: 2023-05-10 13:25:44.134157: Failed to connect to Zenon node. Is the node running?
```

`cat config.json`
```
x3639@0x3639-NoM:~/Github/htlc-watchtower/build$ cat config.json 
node_url_ws: 'ws://public.deeZNNodez.com:35998'
unlock_threshold_in_minutes: 60
```

I've tried 3 different nodes - both ws and wss

-------------------------

0x3639 | 2023-05-10 18:56:34 UTC | #27

When I try to run the Dockerfile Image I get the folllowing error:

`SEVERE: 2023-05-10 18:51:41.965667: Invalid argument(s): Failed to load dynamic library '/app/src/libisar.so': libgcc_s.so.1: cannot open shared object file: No such file or directory
`

But I doubt that is related to the issue above.  I've manually downloaded `https://github.com/isar/isar/releases/download/3.1.0/libisar_linux_x64.so` and moved here  `src/libisar.so`  If we can get the native build to work in Ubuntu, I can trouble shoot the `Dockerfile` 

```
FROM dart:stable AS build

# Resolve app dependencies.
WORKDIR /app
COPY pubspec.* ./
RUN dart pub get

# Copy app source code and AOT compile it.
COPY . .
# Ensure packages are still up-to-date if anything has changed
RUN dart pub get --offline
RUN dart run build_runner build --delete-conflicting-outputs
RUN dart compile exe src/main.dart -o src/main

# Build minimal serving image from AOT-compiled `/main` and required system
# libraries and configuration files stored in `/runtime/` from the build stage.
FROM scratch
COPY --from=build /runtime/ /
COPY --from=build /app/src/. /app/src/

#Start service.
CMD ["/app/src/main"]
```

-------------------------

vilkris | 2023-05-11 07:58:54 UTC | #28

Looks like I typo'd the file extension in the last post, it should be:

```
cp example.config.yaml build/config.yaml
```
And for this:
[quote="0x3639, post:27, topic:50"]
and moved here `src/libisar.so`
[/quote]
[quote="vilkris, post:23, topic:50"]
The `libisar.so` library has to be in the `build` directory
[/quote]

I'll have to write some proper instructions and add them to the repo's readme.

-------------------------

0x3639 | 2023-05-11 14:08:03 UTC | #29

got it.  makes sense now. `build` is required.  I'll get this going today.

-------------------------

0x3639 | 2023-05-11 18:04:21 UTC | #31

I got the Dockerfile to work!!!  I'll make it less shitty and share here.  Maybe I can submit a PR to add that to your repo along with instructions.

-------------------------

0x3639 | 2023-05-11 22:25:55 UTC | #32

```
x3639@0x3639-NoM:~/Github/htlc-watchtower$ docker run -v wallet:/root/.znn/wallet htlc-watchtower
INFO: 2023-05-11 22:18:28.464656: Initializing websocket connection ...
INFO: 2023-05-11 22:18:28.729298: Websocket connection successfully established
INFO: 2023-05-11 22:18:28.729423: Connected to node ws://public.deeznnodez.com:35998
INFO: 2023-05-11 22:18:28.750339: Node is in sync
INFO: 2023-05-11 22:18:28.816243: Loading ./libargon2_ffi_plugin.so from path /root/.pub-cache/git/znn_sdk_dart-abf887d30311494d7e6cd87b2d74b87f55d37abd/lib/src/argon2/blobs/./libargon2_ffi_plugin.so
INFO: 2023-05-11 22:18:29.684808: The watchtower does not have enough Plasma. Please fuse at least 120 QSR to address: z1qpu77xejhe2pcxmkhyh5m9vlssxynxaakmk34c
INFO: 2023-05-11 22:18:29.684876: Waiting for Plasma
INFO: 2023-05-11 22:25:20.597073: The watchtower has enough Plasma now
INFO: 2023-05-11 22:25:20.597150: Watchtower initialized with address z1qpu77xejhe2pcxmkhyh5m9vlssxynxaakmk34c
INFO: 2023-05-11 22:25:20.597238: Running watchtower
```

-------------------------

0x3639 | 2023-05-11 22:27:37 UTC | #33

That was not easy to get this to work with Docker.  I gave up on downloading the `libisar.so` file on build.  I just downloaded manually and put in the `build` folder.  Maybe I'll try again later.

-------------------------

