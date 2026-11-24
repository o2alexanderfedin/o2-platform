# Chunk-level encryption in SliceFS

Encryption is one more filter in the per-object filter chain:

```
plaintext -> FastCDC cut -> zstd -> encrypt -> store
read: load -> decrypt -> zstd decode
```

## Rules

1. Cut on plaintext. Chunk boundaries come from the real data, so an insert changes only the chunks near it.
2. Compress before encryption. Ciphertext does not compress.
3. Use a deterministic AEAD (for example AES-GCM-SIV, or XChaCha20-Poly1305 with a nonce derived from the chunk). A random nonce per write gives a new ciphertext for the same chunk, and dedup is lost.
4. Each object records its filters ("zstd", "encrypted with key K") in its header, so a reader knows which inverse filters to run.
5. Metadata objects (inodes, directories, manifests) go through the same filter, so names and the tree shape are hidden too.

## Object ID options

- **Hash of the ciphertext.** `scrub` and untrusted storage nodes (o2 backbone) can check objects without the key. Fits sync.
- **Keyed hash of the plaintext.** Works, but checks need the key.

## Key scope (decision D1)

| Key | Dedup scope | Leak |
|---|---|---|
| One key per owner or vault | Inside that scope | Outsiders learn nothing; a key holder sees equal chunks |
| Convergent (key from the content) | Global | Anyone with a candidate file can check if a store has it, and guess small changes in a known file |

## Other notes

- Chunk and object sizes stay visible; padding to size classes can hide them at a small space cost.
- Key rotation means rewriting objects; the SliceFS `rehash` tool (slicefs#62) has the same shape.
- If an outside program encrypts data before SliceFS sees it: randomized encryption gives almost no dedup; deterministic chunk-by-chunk encryption with content-defined boundaries keeps part of it. zstd gains nothing in both cases.
