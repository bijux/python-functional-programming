## FuncPipe RAG — end of Module 04

This repository contains the consolidated running project state at the end of **Module 04**:
config-as-data, lazy pipelines, rules DSLs, taps/probes, streaming iteration utilities (Module 03),
plus Module 04's tree-safe recursion (TreeDoc), Result/Option per-record failures, memoization,
breakers/retries/resource safety, and structured error reports.

Earlier module states are available via git tags and snapshots in `history/`.

### Architecture

```text
RawDoc (CSV) -> CleanDoc -> ChunkWithoutEmbedding -> Chunk -> structural_dedup_chunks
      |             |             |                   |
      |          CleanConfig    gen_chunk_doc       embed_chunk
      |
  Reader/FSReader (boundary) -> full_rag_api_docs/full_rag_api_path -> JSONL (shell)

# Module 03–04 streaming helpers (optional):
# - stream_chunks / gen_bounded_chunks / safe_rag_pipeline
# - throttle (clock/sleeper injection) + FakeTime
# - TraceLens / RagTraceV3
# - multicast / fork2_lockstep / samplers / peek
# - Result streams: try_map_iter / breakers / retries / error reports
```

### Install

```bash
make install
```

### Tests

```bash
make test
```

### Snapshot exports

Snapshots are created from git tags (`module-01`, `module-02`, `module-03`, …):

```bash
make snapshots
```
