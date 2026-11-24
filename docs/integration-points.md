# Integration points

| From | To | What | Where tracked |
|---|---|---|---|
| SliceFS | browser | WASM client on OPFS (IndexedDB fallback); browser support: Chrome/Edge 108+, Firefox 111+, Safari 15.2+ | slicefs#169 |
| SliceFS | o2.services | Sync by object ID over libp2p; DHT announces object IDs; each fetched object is checked against its ID | not filed yet |
| SliceFS | o2.services | Encrypted objects as backbone replicas (availability only) | slicefs encryption design (not filed yet); D1 |
| SliceFS | o2.services | Live control of a mounted store (stats, sync, set options) for jobs and controllers | slicefs#87 |
| SliceFS | all | Store format header with feature flags, migration path, format freeze | slicefs#154, #155, #156 |
| video-compression | SliceFS | Model files (ONNX / WGSL weight packs, SHA-256 today) as content-addressed objects | not filed yet |
| video-compression | SliceFS | GOP-aligned, container-aware chunking, so copies in other containers and trims dedup | not filed yet; D6 |
| video-compression | o2.services | Upscale and interpolation work as jobs on owner devices | — |
| photo-compression | SliceFS | Vault objects (`.spic` stubs, AVIF, originals) in the SliceFS browser store; dedup of originals and near-duplicates | not filed yet; D2 |
| photo-compression | o2.services | Vault keypair = owner identity and key scope; P2P sync; `.spic` extraction as jobs on owner devices | photo-compression (o2 parts deferred) |
