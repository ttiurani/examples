# Android NDK and Rust with Bazel example

## Setup

1) Install latest Android Studio
2) Install correct `build-tools` with `sdkmanager "build-tools;30.0.3"`
3) Install correct NDK with `sdkmanager "ndk;21.4.7075529"`
4) Setup `ANDROID_HOME` to point to installation directory, e.g. `export ANDROID_HOME="$HOME/Library/Android/sdk"`.
5) Setup `ANDROID_NDK_HOME` to point to the right NDK, e.g. `export ANDROID_NDK_HOME="$ANDROID_HOME/ndk/21.4.7075529"`

## Problem

Running:

```
bazel build //jni:ndk_rust_jni --sandbox_debug --verbose_failures --test_output=streamed --fat_apk_cpu=arm64-v8a
```

builds the correct rust JNI:

```
$ objdump -f bazel-bin/jni/libndk_rust_jni.so

bazel-bin/jni/libndk_rust_jni.so:       file format ELF64-aarch64-little

architecture: aarch64
start address: 0x0000000000005160
```

but building the android binary:

```
bazel build //:ndk_rust --sandbox_debug --verbose_failures --test_output=streamed --fat_apk_cpu=arm64-v8a
```

still puts .dylib inside the APK:

```
$ zipinfo bazel-bin/ndk_rust.apk | head -3
Archive:  bazel-bin/ndk_rust.apk
Zip file size: 2061081 bytes, number of entries: 347
-rw----     2.0 fat   867512 b- defN 10-Jan-01 00:00 lib/arm64-v8a/libndk_rust_jni.dylib
```
