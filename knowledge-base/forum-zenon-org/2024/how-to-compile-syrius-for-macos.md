Thread: how-to-compile-syrius-for-macos
0x3639 | 2023-02-08 22:42:33 UTC | #1

Here are the steps I took to compile the syrius code for mac.  After hours of failed attempts, I changed the mac to one with an intel processor.  I was NEVER able to build a stable version of syrius on the M1 processor.  So I can confirm these steps ONLY work with a Mac intel processor.

## Install Flutter
Steps were derived from this source: https://docs.flutter.dev/get-started/install/macos

### Create a working folder for Flutter
`mkdir ~/development && cd ~/development`

### Download Flutter
Download the latest Flutter SDK to the `~/development` folder.  Check the link to make sure you are downloading the latest version
https://storage.googleapis.com/flutter_infra_release/releases/stable/macos/flutter_macos_3.3.7-stable.zip

### Extract the file in the desired location
`unzip flutter_macos_3.3.7-stable.zip`

### Add the `flutter` tool to your path

### Add `flutter` to your path

You can update your PATH variable for the current session at the command line, as shown in [Get the Flutter SDK](https://docs.flutter.dev/get-started/install/macos#get-sdk). You’ll probably want to update this variable permanently, so you can run `flutter` commands in any terminal session.

The steps for modifying this variable permanently for all terminal sessions are machine-specific. Typically you add a line to a file that is executed whenever you open a new window. For example:

1. Determine the path of your clone of the Flutter SDK. You need this in Step 3.
2. Open (or create) the `rc` file for your shell. Typing `echo $SHELL` in your Terminal tells you which shell you’re using. If you’re using Bash, edit `$HOME/.bash_profile` or `$HOME/.bashrc`. If you’re using Z shell, edit `$HOME/.zshrc`. If you’re using a different shell, the file path and filename will be different on your machine.
3. Add the following line and change `[PATH_OF_FLUTTER_GIT_DIRECTORY]` to be the path of your clone of the Flutter git repo:

4. Run `source $HOME/.<rc file>` to refresh the current window, or open a new terminal window to automatically source the file.
5. Verify that the `flutter/bin` directory is now in your PATH by running:

```
export PATH="$PATH:[PATH_OF_FLUTTER_GIT_DIRECTORY]/bin"
```
Verify that the `flutter` command is available by running:

```
which flutter
```
### Download and install Xcode

https://developer.apple.com/xcode/

###

Configure the Xcode command-line tools to use the newly-installed version of Xcode by running the following from the command line:

```
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
sudo xcodebuild -runFirstLaunch
```
### 

### Run flutter doctor

Run the following command to see if there are any dependencies you need to install to complete the setup (for verbose output, add the `-v` flag):

```
flutter doctor
```

### Install Brew
`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

Source https://brew.sh/

### Install Cocoapods

`brew install cocoapods`

Source: https://formulae.brew.sh/formula/cocoapods

### Create Working Directory for Project
`mkdir ~/zenon && cd zenon`

### Clone Repo and Build App
```
git clone https://github.com/zenon-network/syrius.git
cd syrius
flutter build macos --release
```

### Download and install the missing dylib files from the Syrius repo 
`cd ~/zenon/syrius/build/macos/Build/Products/Release/s y r i u s.app/Contents/Resources`

Download the following missing files to this directory.

![image|210x138](upload://6U9RKNxTCTcSI9baqMld46TFYzG.png)

These files can be downloaded from the link below.  Or, you can download the official .dmg build of the app and download these files from the official app.  They can be found here: `s y r i u s.app/Contents/Resources` in the .dmg

https://github.com/0x3639/syrius/tree/master/Resources

### Run App

`cd ~/zenon/syrius/build/macos/Build/Products/Release/`

double click the app `s y r i u s.app`

### How to make a `.dmg`

https://www.asmaloney.com/2013/07/howto/packaging-a-mac-os-x-application-using-a-dmg/

https://github.com/create-dmg

-------------------------

sol | 2022-11-06 18:26:16 UTC | #2

Thank you for your help with this part of the build process! I really appreciate your persistence through all the frustration. :pray:

Here's how I envision this working out in the future:
* Devs will need to setup the tools, such as Flutter, Xcode, Cocoapods, etc
* They clone the syrius repo, make adjustments to the Dart/Flutter code
* Execute `flutter build` or `flutter run --release`

The macos build process can be updated to source the four .dylib files dynamically, copy them to the /Resources/ directory, then run a script to package the output into a .dmg file.

-------------------------

coinselor | 2022-11-06 19:01:23 UTC | #3

Thank you both for taking the time to go through all this pain. Flutter is definitely not perfect, and there are lot of idiosyncrasies for each platform, but in the end it should be worth it. There are lot of new state of the art apps being built in flutter like superlist.com, so I can only imagine it will keep getting better. 

I would say a lot of these issues would be trivial to fix for an experienced flutter dev, so I can see founding devs just prioritizing developing the infra further (sentinels, smart contracts, etc) before flushing out these small issues. It's a great help if we can isolate and even correct some of these issues ourselves.

-------------------------

aliencoder | 2022-11-11 16:54:06 UTC | #4

[quote="0x3639, post:1, topic:1116"]
I was NEVER able to build a stable version of syrius on the M1 processor
[/quote]

I think I might have a solution: you'll need to compile the libraries for arm64 architecture. 

Currently they are compiled for x86 and you cannot mix together an x86 binary with arm64 libraries or vice versa.

Latest flutter builds already package MacOS apps as Universal Apps (containing both x86 and arm64 slices). You can inspect it after building with the `file` command:

> $ file s\ y\ r\ i\ u\ s
> s y r i u s: Mach-O universal binary with 2 architectures: [x86_64:Mach-O 64-bit executable x86_64
> - Mach-O 64-bit executable x86_64] [arm64:Mach-O 64-bit executable arm64
> - Mach-O 64-bit executable arm64]
> s y r i u s (for architecture x86_64): Mach-O 64-bit executable x86_64
> s y r i u s (for architecture arm64): Mach-O 64-bit executable arm64

-------------------------

0x3639 | 2022-11-11 18:07:05 UTC | #5

Thank you zir!

-------------------------

aliencoder | 2022-11-27 21:19:14 UTC | #6

Latest flutter tool already compiles Syrius binary as a MacOS universal app. What we need to do is to also have all included libraries built as "fat libs" containing both `x86_64` and `arm64` slices. I've compiled a list of instructions for each necessary library that is included into the Syrius wallet.

1. For `libargon2_ffi`:

```
cd argon2_ffi

cmake -DCMAKE_OSX_ARCHITECTURES="arm64;x86_64" CMakeLists.txt

make
```

Inspect the resulting binary

```
lipo -detailed_info libargon2_ffi.dylib
```
As you can see we have a fat lib with both CPU slices:
```
Fat header in: libargon2_ffi.dylib`
fat_magic 0xcafebabe
nfat_arch 2
architecture x86_64
cputype CPU_TYPE_X86_64
    cpusubtype CPU_SUBTYPE_X86_64_ALL
    capabilities 0x0
    offset 16384
    size 86776
    align 2^14 (16384)
architecture arm64
    cputype CPU_TYPE_ARM64
    cpusubtype CPU_SUBTYPE_ARM64_ALL
    capabilities 0x0
    offset 114688
    size 71056
    align 2^14 (16384)
```

2. For `libpow_links`:

```
cd znn-pow-links-cpp

cmake -DCMAKE_OSX_ARCHITECTURES="arm64;x86_64" CMakeLists.txt

make
```

Inspect the resulting binary

```
lipo -detailed_info libpow_links.dylib
```
As you can see we have a fat lib with both CPU slices:
```
Fat header in: libpow_links.dylib
fat_magic 0xcafebabe
nfat_arch 2
architecture x86_64
    cputype CPU_TYPE_X86_64
    cpusubtype CPU_SUBTYPE_X86_64_ALL
    capabilities 0x0
    offset 16384
    size 35656
    align 2^14 (16384)
architecture arm64
    cputype CPU_TYPE_ARM64
    cpusubtype CPU_SUBTYPE_ARM64_ALL
    capabilities 0x0
    offset 65536
    size 36079
    align 2^14 (16384)
```

3. For `libznn`:

```
cd go-zenon

CGO_ENABLED=1 GOOS=darwin GOARCH=amd64 go build -o ./build/libznn-x86_64.dylib -buildmode=c-shared -tags libznn main_libznn.go

CGO_ENABLED=1 GOOS=darwin GOARCH=arm64 go build -o ./build/libznn-arm64.dylib -buildmode=c-shared -tags libznn main_libznn.go

lipo -create libznn-x86_64.dylib libznn-arm64.dylib -output libznn.dylib
```

Inspect the resulting binary:

```
lipo -detailed_info libznn.dylib
```
Same result for the fat `libznn`:
```
Fat header in: libznn.dylib
fat_magic 0xcafebabe
nfat_arch 2
architecture x86_64
    cputype CPU_TYPE_X86_64
    cpusubtype CPU_SUBTYPE_X86_64_ALL
    capabilities 0x0
    offset 16384
    size 22857720
    align 2^14 (16384)
architecture arm64
    cputype CPU_TYPE_ARM64
    cpusubtype CPU_SUBTYPE_ARM64_ALL
    capabilities 0x0
    offset 22888448
    size 21907554
    align 2^14 (16384)
```

-------------------------

sol | 2022-11-27 17:45:27 UTC | #7

Thank you for sharing this! I didn't even know we could generate universal binaries on MacOS.

-------------------------

aliencoder | 2022-11-27 21:41:33 UTC | #8

Putting everything together would go like this (assuming you have all fat libs in the syrius directory):

```
cd syrius

flutter build macos

cp libargon2_ffi.dylib libpow_links.dylib libznn.dylib ./build/macos/Build/Products/Release/s\ y\ r\ i\ u\ s.app/Contents/Resources/
```

Now you can run Syrius natively on both Intel and Apple Silicon devices.

-------------------------

0x3639 | 2022-11-27 22:42:54 UTC | #9

What about the 4th lib: libExportWallet.dylib?

![Screenshot 2022-11-27 at 1.47.53 PM|689x313](upload://oRqo7LYnZgqm7Gn9J16schY1pMp.png)

-------------------------

sol | 2022-11-27 23:48:50 UTC | #10

I don't have the source code for that and I don't think Mr Kaine will make it available to us.
He's already confirmed to me that it won't be necessary after the swap decay reaches 100%, which is scheduled to happen on December 17th, 2022.

-------------------------

aliencoder | 2022-11-28 23:33:09 UTC | #11

Yes, I think that library was necessary only during the swap cycles. I think it's safe to discard it after the swap decay reaches 100%.

-------------------------

