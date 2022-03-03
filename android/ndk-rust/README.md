# Android NDK and Rust with Bazel example

## Setup

1) Install latest Android Studio
2) Install correct `build-tools` with `sdkmanager "build-tools;30.0.3"`
3) Install correct NDK with `sdkmanager "ndk;21.4.7075529"`
4) Setup `ANDROID_HOME` to point to installation directory, e.g. `export ANDROID_HOME="$HOME/Library/Android/sdk"`.
5) Setup `ANDROID_NDK_HOME` to point to the right NDK, e.g. `export ANDROID_NDK_HOME="$ANDROID_HOME/ndk/21.4.7075529"`

## Building the APK

Running:

```
bazel build //:ndk_rust --sandbox_debug --verbose_failures --test_output=streamed --fat_apk_cpu=arm64-v8a,x86,x86_64
```

builds an APK with a rust shared library with the chosen architectures:

```
$ zipinfo bazel-bin/ndk_rust.apk | head -5
Archive:  bazel-bin/ndk_rust.apk
Zip file size: 5104553 bytes, number of entries: 349
-rw----     2.0 fat  4385888 b- defN 10-Jan-01 00:00 lib/arm64-v8a/libndk_rust_jni.so
-rw----     2.0 fat  3884392 b- defN 10-Jan-01 00:00 lib/x86/libndk_rust_jni.so
-rw----     2.0 fat  4379960 b- defN 10-Jan-01 00:00 lib/x86_64/libndk_rust_jni.so
```
