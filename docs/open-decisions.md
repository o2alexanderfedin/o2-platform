# Open decisions

Decisions that are the owner's to make. "One-way" means hard to undo (a published format or contract).

| # | Decision | Options | Kind | Status |
|---|---|---|---|---|
| D1 | Encryption key scope | (a) one key per owner or vault: private, dedup only inside that scope; (b) convergent encryption (key from the content): global dedup, but anyone with a candidate file can check if a store has it | One-way | Open |
| D2 | Photo and video apps on SliceFS | (a) SliceFS (browser client) is their store; (b) they keep their own storage and share only the sync protocol | Costly | Open |
| D3 | o2.services as the mesh for all | Use the o2.services P2P mesh for SliceFS, photo and video sync | Costly | Open (assumed yes in the notes) |
| D4 | Android path | (a) browser only first; (b) SliceFS native library with a DocumentsProvider; (c) own Android build with a FUSE system service | Reversible order | Open |
| D5 | SliceFS store format freeze | Freeze after the v2.2 phases, the format header and the migration path (slicefs#156) | One-way | Planned |
| D6 | Media-aware chunking | A per-file-type chunker (GOP-aligned for video) as a SliceFS store feature | Costly (format) | Idea |
