---
title: "Phase 3 Literature Version & Duplicate Cleanup - 2026-09-28"
taxonomy_version: "v2"
status: "phase3_in_progress"
date: "2026-09-28"
tags:
  - literature
  - canonical-version
  - duplicate-cleanup
  - audit
---

# Phase 3 Literature Version & Duplicate Cleanup — 2026-09-28

> [!IMPORTANT]
> Phase 3 verifies literature identity and publication status independently from taxonomy semantics.
> The target is **one canonical note per paper/work**, preferring the formal peer-reviewed version when it supersedes a preprint and the preprint adds no independent content.

## Rules

1. Prefer official publisher / proceedings / ACL Anthology / OpenReview / proceedings records over secondary listings.
2. Preserve the original arXiv identifier in `arxiv` after formal publication.
3. Use `doi` for the formal/canonical publication DOI.
4. Do **not** put DataCite arXiv identifiers such as `10.48550/arXiv.xxxxx` in `doi`; the `arxiv` field already records that identity.
5. A filename may temporarily retain an old `(arXiv ...)` or wrong venue prefix during Phase 3. Atomic file/link renames are deferred to **Phase 7 Repository Normalization**.
6. Do not invent a DOI merely because `doi: null`; many OpenReview / NeurIPS / ICLR / PMLR / USENIX records legitimately have no DOI in the repo's preferred canonical source.
7. Duplicate removal requires identity evidence: matching DOI, arXiv ID, canonical title/authors, or a verified preprint→formal relationship.

## Corrections Applied

- **Mem0** → ECAI 2025, DOI `10.3233/FAIA251160`.
- **Longformer** → corrected from false `ACL 2020` metadata back to arXiv/CoRR-only status.
- **PyramidKV** → corrected from false `EMNLP 2024` metadata to **COLM 2025 Spotlight**; formal author list synchronized.
- **LLMLingua** → formal title uses **“Compressing Prompts”**; DOI `10.18653/v1/2023.emnlp-main.825`.
- **∞Bench / InfiniteBench** → ACL 2024 DOI `10.18653/v1/2024.acl-long.814`; formal author list synchronized.
- **L-Eval** → ACL 2024 DOI `10.18653/v1/2024.acl-long.776`.
- **LongBench** → ACL 2024 DOI `10.18653/v1/2024.acl-long.172`; formal author list synchronized.
- **Gao et al. RAG survey** → missing author **Qianyu Guo** restored; publication remains arXiv/CoRR.
- **Corrective RAG** → cleared DataCite arXiv DOI from `doi`; remains arXiv/CoRR.

Earlier canonical upgrades already present from Phase 1 remain valid, including LightRAG, MemoRAG, OpenScholar, RAGChecker, T²-RAGBench, ReportLogic and others.

## Current True-Preprint Set Verified So Far

The following have been checked and should remain preprint/arXiv unless a later official publication is found:

- LongNet
- Advancing Transformer Architecture in Long-Context LLMs — survey
- Infini-attention
- Retrieval-Augmented Generation for Large Language Models — Gao et al. survey
- Corrective RAG
- LongRAG
- Late Chunking
- VersionRAG
- SURE-RAG
- InstructUIE
- Microsoft From Local to Global / GraphRAG
- CrossAug
- WebGPT
- GopherCite / Teaching language models to support answers with verified quotes
- MemGPT
- Singh et al. Agentic RAG survey
- EviMem
- RAGBench

## Phase 7 Rename Queue

These notes already have formal-publication metadata but their current path still encodes an older arXiv/preprint or incorrect venue name. Do **not** rename individually during Phase 3; rename atomically with backlinks in Phase 7.

- Mamba → COLM 2024
- SnapKV → NeurIPS 2024
- Byte Latent Transformer → ACL 2025
- Evaluation of Retrieval-Augmented Generation survey → Springer 2025 / CCF BigData
- Graph Retrieval-Augmented Generation: A Survey → ACM TOIS 2026
- LightRAG → Findings EMNLP 2025
- AutoGen → COLM 2024
- MemoRAG → WWW 2025
- OpenScholar → Nature 2026
- Mem0 → ECAI 2025
- RULER → COLM 2024
- RAGChecker → NeurIPS 2024 Datasets & Benchmarks
- Longformer → rename away from the incorrect legacy `ACL 2020` prefix
- PyramidKV → rename away from the incorrect legacy `EMNLP 2024` prefix
- LLMLingua → rename title fragment from `Compressing Context` to `Compressing Prompts`

## Duplicate Cleanup Already Completed

Phase 1 had already verified and removed these duplicate-version pairs:

| Canonical retained | Duplicate removed | Identity evidence |
|---|---|---|
| PipeRAG — KDD 2025 | arXiv-only PipeRAG note | formal publication supersedes preprint |
| RAGCache — ACM TOCS 2026 | duplicate TOCS 2025-named note | same DOI `10.1145/3768628` |
| A Reality Check on Context Utilisation for RAG — ACL 2025 | shortened-title duplicate | same ACL paper / DOI |

## Remaining Work Before Closure

- scan all current literature notes by `paper_id / normalized title / DOI / arXiv`;
- identify duplicate identities independent of filenames;
- verify remaining suspicious venue/year/title/author records;
- record all Phase 7 rename candidates;
- confirm no formal publication is being represented as an arXiv-only canonical note;
- update this file to `phase3_closed` only after final validation.
