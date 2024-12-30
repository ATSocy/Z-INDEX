Thread: syrius-build-instructions-with-dylib-files
0x3639 | 2023-04-18 01:05:16 UTC | #1

@aliencoder I just helped a guy build SYRIUS v0.0.6 from scratch using my old instruction here: https://forum2.zenon.org/t/how-to-compile-syrius-for-macos/1116

My instructions included manually downloading the dylib files from my personal repo.  I got them from the .dmg in the then latest release.  I know these files are created with your latest GhA.  But for those that want to build from scratch, do you think we should host those files on the /zenon-network repo somewhere?  Not sure if people should trust them.  But building them manually could be tedious.  

Thoughts?

-------------------------

aliencoder | 2023-04-19 08:53:04 UTC | #2

[quote="0x3639, post:1, topic:1381"]
But for those that want to build from scratch
[/quote]

Building them manually from source is pretty straightforward. You'll need access to a both a **Linux** and a **MacOS** host:

**argon2_ffi** instructions:
- **Linux host** (cross-compile) output -> [Windows](https://github.com/zenon-network/argon2_ffi/blob/38ce76d53969e9155bcc38c2fca679d9ae906f6b/.github/workflows/znn_argon2_ffi_builder.yml#L111), [Linux](https://github.com/zenon-network/argon2_ffi/blob/38ce76d53969e9155bcc38c2fca679d9ae906f6b/.github/workflows/znn_argon2_ffi_builder.yml#L86), [Android](https://github.com/zenon-network/argon2_ffi/blob/38ce76d53969e9155bcc38c2fca679d9ae906f6b/.github/workflows/znn_argon2_ffi_builder.yml#L100)
- **MacOS host** output -> [MacOS](https://github.com/zenon-network/argon2_ffi/blob/38ce76d53969e9155bcc38c2fca679d9ae906f6b/.github/workflows/znn_argon2_ffi_builder.yml#L45), [iOS](https://github.com/zenon-network/argon2_ffi/blob/38ce76d53969e9155bcc38c2fca679d9ae906f6b/.github/workflows/znn_argon2_ffi_builder.yml#L31), [WebAssembly](https://github.com/zenon-network/argon2_ffi/blob/38ce76d53969e9155bcc38c2fca679d9ae906f6b/.github/workflows/znn_argon2_ffi_builder.yml#L53)

**znn-pow-links** instructions:
- **Linux host** (cross-compile) output -> [Windows](https://github.com/zenon-network/znn-pow-links-cpp/blob/fefbaae2178512d4446261cde9444d965b3f246f/.github/workflows/znn_pow_links_builder.yml#L112), [Linux](https://github.com/zenon-network/znn-pow-links-cpp/blob/fefbaae2178512d4446261cde9444d965b3f246f/.github/workflows/znn_pow_links_builder.yml#L87), [Android](https://github.com/zenon-network/znn-pow-links-cpp/blob/fefbaae2178512d4446261cde9444d965b3f246f/.github/workflows/znn_pow_links_builder.yml#L101)
- **MacOS host** output -> [MacOS](https://github.com/zenon-network/znn-pow-links-cpp/blob/fefbaae2178512d4446261cde9444d965b3f246f/.github/workflows/znn_pow_links_builder.yml#L45), [iOS](https://github.com/zenon-network/znn-pow-links-cpp/blob/fefbaae2178512d4446261cde9444d965b3f246f/.github/workflows/znn_pow_links_builder.yml#L31), [WebAssembly](https://github.com/zenon-network/znn-pow-links-cpp/blob/fefbaae2178512d4446261cde9444d965b3f246f/.github/workflows/znn_pow_links_builder.yml#L54)

Workflow [znn-pow-links](https://github.com/zenon-network/znn-pow-links-cpp/blob/master/.github/workflows/znn_pow_links_builder.yml)

Workflow [argon2_ffi](https://github.com/zenon-network/argon2_ffi/blob/master/.github/workflows/znn_argon2_ffi_builder.yml)

-------------------------

