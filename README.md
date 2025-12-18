## FuncPipe RAG — end of Module 07

This repository contains the consolidated running project state at the end of **Module 07**:
config-as-data, lazy pipelines, rules DSLs, taps/probes, streaming iteration utilities (Module 03),
plus Module 04's tree-safe recursion (TreeDoc), Result/Option per-record failures, memoization,
breakers/retries/resource safety, and structured error reports.

Module 05 adds type-driven design utilities: ADTs, functors, applicative Validation, monoids,
stable serialization contracts (Envelope + JSON/MessagePack + migrations), Pydantic v2 at the
edges, compositional domain models, and a hybrid NumPy path with equivalence tests.

Module 06 adds monadic helpers (Reader/State/Writer), container-layer transposition helpers,
runtime-configurable pipelines, and explicit exception-to-Result bridging for boundaries.

Module 07 adds a small production architecture layer: ports/capability protocols, a deferred IO
description (`IOPlan`) with a single shell interpreter (`perform`), structured logs as pure data
(Writer + `LogEntry`), idempotent effect design, and explicit Session/Tx bracketing.

Earlier module states are available via git tags and snapshots in `history/`.

### Architecture

```text
RawDoc (CSV) -> CleanDoc -> ChunkWithoutEmbedding -> Chunk -> structural_dedup_chunks
      |             |             |                   |
      |          CleanConfig    gen_chunk_doc       embed_chunk
      |
  DocsReader/FSReader (boundary) -> full_rag_api_docs/full_rag_api_path -> JSONL (shell)
  (see `funcpipe_rag.boundaries.shells`)

# Module 03–04 streaming helpers (optional):
# - stream_chunks / gen_bounded_chunks / safe_rag_pipeline
# - throttle (clock/sleeper injection) + FakeTime
# - TraceLens / RagTraceV3
# - multicast / fork2_lockstep / samplers / peek
# - Result streams: try_map_iter / breakers / retries / error reports

# Module 05 type-driven core APIs:
# - funcpipe_rag.fp (Module-05 type-driven toolkit: ADTs, functors, validation, monoids, domain, perf)
# - funcpipe_rag.boundaries (serde + Pydantic-at-the-edges)

# Module 06 effects (optional):
# - funcpipe_rag.fp.effects (Reader/State/Writer + layering + configurable pipelines)
# - funcpipe_rag.boundaries.adapters (serde + Pydantic edges + exception bridge)

# Module 07 production architecture layer (optional):
# - funcpipe_rag.domain (capabilities + structured logs + idempotency helpers)
# - funcpipe_rag.domain.effects (IOPlan + IOPlan-specific retry/tx helpers)
# - funcpipe_rag.infra.adapters (filesystem/memory storage, clocks, loggers, atomic write-if-absent)
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
