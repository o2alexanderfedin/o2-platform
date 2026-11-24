# Android testing

Plan: a few low-cost Android phones to test the whole stack, maybe with an Android build assembled by the owner.

| Topic | Note |
|---|---|
| Browser path (no build needed) | Chrome for Android 109+ has OPFS with sync access handles. Chrome on Android 12+ has WebGPU with recent Adreno or Mali GPUs. The photo and video PWAs, a browser o2 node and the SliceFS WASM client can all be tested in plain Chrome. |
| Native SliceFS on stock Android | Apps cannot mount FUSE without root: Android gives `/dev/fuse` only to its system storage service. Without root, SliceFS runs as a native library (Rust through the NDK, target `aarch64-linux-android`) and shows its files to other apps through a DocumentsProvider (Storage Access Framework). |
| Own Android build | With an own build (AOSP or LineageOS), a system service can mount SliceFS through FUSE. |
| Phone choice | Pick models with an unlockable bootloader and LineageOS or AOSP support (for example a used Pixel 6a or 7a). The cheapest no-name phones often have locked bootloaders. |
| GPU | Check WebGPU support (Adreno or Mali, Android 12+) for the photo and video models. |
| Storage limits | Browser quotas and eviction: the apps call `navigator.storage.persist()`. |
