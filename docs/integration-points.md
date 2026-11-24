# Integration points

Back to the [overview](../README.md). Repos: [o2.services](https://github.com/o2alexanderfedin/o2.services), [slicefs](https://github.com/o2alexanderfedin/slicefs), [photo-compression](https://github.com/o2alexanderfedin/photo-compression), [video-compression](https://github.com/o2alexanderfedin/video-compression).

| From | To | What | Where tracked |
|---|---|---|---|
| SliceFS | browser | WASM client on [OPFS](https://developer.mozilla.org/en-US/docs/Web/API/File_System_API/Origin_private_file_system) (IndexedDB fallback); browser support: Chrome/Edge 108+, Firefox 111+, Safari 15.2+ | [slicefs#169](https://github.com/o2alexanderfedin/slicefs/issues/169) |
| SliceFS | o2.services | Sync by object ID over libp2p; DHT announces object IDs; each fetched object is checked against its ID | not filed yet |
| SliceFS | o2.services | Encrypted objects as backbone replicas (availability only) | [encryption notes](encryption.md) (issue not filed yet); [D1](open-decisions.md) |
| SliceFS | o2.services | Live control of a mounted store (stats, sync, set options) for jobs and controllers | [slicefs#87](https://github.com/o2alexanderfedin/slicefs/issues/87) |
| SliceFS | all | Store format header with feature flags, migration path, format freeze | [slicefs#154](https://github.com/o2alexanderfedin/slicefs/issues/154), [slicefs#155](https://github.com/o2alexanderfedin/slicefs/issues/155), [slicefs#156](https://github.com/o2alexanderfedin/slicefs/issues/156) |
| video-compression | SliceFS | Model files (ONNX / WGSL weight packs, SHA-256 today) as content-addressed objects | not filed yet |
| video-compression | SliceFS | GOP-aligned, container-aware chunking, so copies in other containers and trims dedup | not filed yet; [D6](open-decisions.md) |
| video-compression | o2.services | Upscale and interpolation work as jobs on owner devices | — |
| photo-compression | SliceFS | Vault objects (`.spic` stubs, AVIF, originals) in the SliceFS browser store; dedup of originals and near-duplicates | not filed yet; [D2](open-decisions.md) |
| photo-compression | o2.services | Vault keypair = owner identity and key scope; P2P sync; `.spic` extraction as jobs on owner devices | [photo-compression#1](https://github.com/o2alexanderfedin/photo-compression/issues/1) (o2 parts deferred) |
