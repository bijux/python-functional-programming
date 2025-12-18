## FuncPipe RAG — end of Module 02

This repository contains the consolidated running project state at the end of **Module 02**:
config-as-data, lazy pipelines, rules DSLs, taps/probes, and boundary-friendly Result helpers.

Earlier module states are available via git tags and snapshots in `history/`.

### Architecture

```text
RawDoc (CSV) -> CleanDoc -> ChunkWithoutEmbedding -> Chunk -> structural_dedup_chunks
      |             |             |                   |
      |          CleanConfig    gen_chunk_doc       embed_chunk
      |
  Reader/FSReader (boundary) -> full_rag_api_docs/full_rag_api_path -> JSONL (shell)
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

Snapshots are created from git tags (`module-01`, `module-02`, …):

```bash
make snapshots
```
