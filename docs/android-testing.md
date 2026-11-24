# Android testing

Back to the [overview](../README.md). Related decision: [D4](open-decisions.md).

Plan: a few low-cost Android phones to test the whole stack, maybe with an Android build assembled by the owner.

| Topic | Note |
|---|---|
| Browser path (no build needed) | Chrome for Android 109+ has OPFS with [sync access handles](https://developer.mozilla.org/en-US/docs/Web/API/FileSystemSyncAccessHandle). Chrome on Android 12+ has [WebGPU](https://developer.chrome.com/docs/web-platform/webgpu/overview) with recent Adreno or Mali GPUs. The photo and video PWAs, a browser o2 node and the SliceFS WASM client can all be tested in plain Chrome. |
| Native SliceFS on stock Android | Apps cannot mount FUSE without root: Android gives `/dev/fuse` only to its system storage service. Without root, SliceFS runs as a native library (Rust through the [Android NDK](https://developer.android.com/ndk), target `aarch64-linux-android`, for example with [cargo-ndk](https://github.com/bbqsrc/cargo-ndk)) and shows its files to other apps through a [DocumentsProvider](https://developer.android.com/reference/android/provider/DocumentsProvider) ([Storage Access Framework](https://developer.android.com/guide/topics/providers/document-provider)). |
| Own Android build | With an own build ([AOSP](https://source.android.com/) or [LineageOS](https://lineageos.org/)), a system service can mount SliceFS through FUSE. |
| Phone choice | Pick models with an unlockable bootloader and [LineageOS device support](https://wiki.lineageos.org/devices/) (for example a used Pixel 6a or 7a). The cheapest no-name phones often have locked bootloaders. |
| GPU | Check WebGPU support (Adreno or Mali, Android 12+) for the photo and video models. |
| Storage limits | Browser quotas and eviction: the apps call [`navigator.storage.persist()`](https://developer.mozilla.org/en-US/docs/Web/API/StorageManager/persist). |
