---
title: "Phase 1 Taxonomy Closure Audit - 2026-09-27"
taxonomy_version: "v2"
status: "phase1_closed"
date: "2026-09-27"
tags:
  - taxonomy
  - audit
  - closure
  - rag
---

# Phase 1 Taxonomy Closure Audit — 2026-09-27

> [!IMPORTANT]
> This note records the **authoritative Phase 1 closure decisions** for D01–D14.
> It is an operational taxonomy for this repository, not a claim that one external survey uses the exact same 14-domain structure.

## 1. Canonical D01–D14

| ID | Canonical Domain | Core distinction |
|---|---|---|
| D01 | **Document Parsing & Structure Recovery** | recover source structure before retrieval-unit design |
| D02 | **Segmentation & Retrieval Granularity** | decide what constitutes a retrievable unit |
| D03 | **Knowledge Extraction & Consolidation** | extract semantic units and resolve/consolidate them |
| D04 | **Representation & Indexing** | encode and organize searchable corpus-side representations |
| D05 | **Query Understanding & Retrieval** | decide what evidence is relevant and retrieve/rank it |
| D06 | **Evidence Sufficiency & Retrieval Control** | decide whether evidence is enough and whether to retrieve/retry/stop |
| D07 | **Context Construction & Utilization** | select/compress/order/pack retrieved evidence and ensure it is usable |
| D08 | **Evidence Reconciliation** | resolve incompatible, temporally misaligned or differently reliable evidence |
| D09 | **Grounded Generation & Long-form Synthesis** | generate supported, attributable answers/reports from evidence |
| D10 | **Knowledge & Index Maintenance** | synchronize derived RAG artifacts when canonical sources change |
| D11 | **Persistent Memory Management** | create/retrieve/consolidate/evolve persistent derived memory |
| D12 | **RAG Orchestration & Action Control** | choose and compose heterogeneous next actions from system state |
| D13 | **Evaluation & Failure Attribution** | measure quality and localize failures using diagnostics/oracles/interventions |
| D14 | **RAG Systems, Security & Privacy** | serving efficiency, integrity/security, privacy and access control |

Existing filenames are intentionally retained until **Phase 7 Repository Normalization** so Obsidian links can be migrated atomically.

## 2. Hard Boundaries

```text
D01 source structure
  != D02 retrieval-unit formation
  != D03 semantic extraction/consolidation
  != D04 representation/index organization
  != D05 query-time retrieval

Relevance (D05)
  != Sufficiency / retrieval control (D06)
  != Context utilization (D07)
  != Evidence reconciliation (D08)
  != Grounded output / citation (D09)

Initial index construction (D04)
  != Source/index maintenance (D10)

Canonical source synchronization (D10)
  != Derived persistent memory (D11)

Iterative retrieval (D05/D06)
  != Heterogeneous state→action orchestration (D12)

Evaluation / diagnosis (D13)
  != Serving / security / privacy engineering (D14)

Domain != Paradigm Tag != Benchmark/Dataset/Metric
```

## 3. Important Scope Corrections

### D01
- Research identity is document parsing / structure recovery.
- Office/Web/DB connectors, URI normalization and hashing are engineering requirements.
- Stable page/span/source anchors are output contracts, not an equally mature research track.

### D02
- Contextualized **representations** belong primarily to D04.
- D02 owns boundary selection, retrieval granularity and hierarchical retrieval units.

### D03
- `Information Preservation` is a quality lens, not an equally mature named field.
- F/R/D/A/P/C/T remains a project hypothesis, not literature consensus.

### D08
- Restored from overly narrow temporal-only scope to **Evidence Reconciliation**.
- Temporal/version conflict, general knowledge conflict, counter-evidence and source reliability belong here when evidence cannot simply coexist.
- Provenance lineage / approval / applicability governance remain thinner gaps.

### D11
- A paper is not D11 simply because it calls an index/database “memory”.
- D11 requires persistent derived state plus memory lifecycle operations.

### D12
- multi-step != agentic
- reflection != agentic
- multiple agents != adaptive orchestration
- fixed workflow != D12 unless state affects action selection

### D14
- Generic robustness is removed as a catch-all.
- Adversarial integrity/security remains D14.
- Ordinary distractor/context robustness is assigned to the lifecycle problem it actually studies.

## 4. Existing Paper Remaps Applied

| Paper | Previous | Phase 1 decision |
|---|---|---|
| HippoRAG (2024) | D04 | **D05 primary / D04 secondary** |
| RAG 2020 | D05 | **CROSS**, D05+D09 secondary |
| RETRO | D05 | **CROSS**, D05+D09 secondary |
| Atlas | D05 | **CROSS**, D05+D09 secondary |
| BEIR | D13 | **D05 primary / D13 secondary** |
| HotpotQA | D13 | **CROSS**, D05+D13 secondary |
| 2WikiMultiHopQA | D13 | **CROSS**, D05+D13 secondary |
| MuSiQue | D13 | **CROSS**, D05+D13 secondary |
| QASPER | D13 | **CROSS**, D05+D13 secondary |
| ASQA | D13 | **D09 primary / D13 secondary** |
| MP-DocVQA / Hi-VT5 | D13 | **CROSS / D13 secondary** |
| A-MEM | A04 | **D11 primary / A04 adjacent** |
| MemoryBank | A04 | **D11 primary / A04 adjacent** |
| MemGPT | A04 | **D11 primary / D12 secondary / A04 adjacent** |
| MemoRAG | D11 | **D05 primary / D11 secondary / A01 adjacent** |

## 5. Existing Metadata / Content Fixes Applied

- LightRAG → canonical **Findings EMNLP 2025**, DOI `10.18653/v1/2025.findings-emnlp.568`.
- DPR DOI → `10.18653/v1/2020.emnlp-main.550`.
- LumberChunker DOI → `10.18653/v1/2024.findings-emnlp.377`.
- IRCoT DOI → `10.18653/v1/2023.acl-long.557`.
- KG²RAG DOI → `10.18653/v1/2025.naacl-long.449`.
- PropRAG DOI → `10.18653/v1/2025.emnlp-main.317`.
- Chain-of-Note DOI → `10.18653/v1/2024.emnlp-main.813`.
- GraphReader DOI → `10.18653/v1/2024.findings-emnlp.746`.
- ARES DOI → `10.18653/v1/2024.naacl-long.20`.
- T²-RAGBench author/title/DOI metadata corrected to ACL Anthology canonical record.
- ReportLogic DOI → `10.18653/v1/2026.acl-long.384`.
- Evidence Sufficiency Benchmark: corrected L4 condition to **No Context**.
- Removed several non-paradigm values such as `benchmark`, `rag_evaluation`, `evaluation`, `factuality`, `hallucination`, and `evidence_sufficiency` from touched notes' `paradigm_tags`.

## 6. Paper-Level Content Corrections Already Present

- STORM: removed unsupported “72% win rate”; retained official +25-point organization / +10-point breadth result.
- OpenScholar: kept D09/D05 and removed unjustified D12/`agentic_rag`.
- EviReport: removed unsupported Source Hash / Evidence Ledger / 38%-gap-recovery claims; retained official 2.16× factual coverage, +8.9 factual accuracy points, +34 visual-evidence-integration points.
- EFSG: replaced unsupported ~94–99% claims with official shared-task results `sentence_support=.612`, `nugget_coverage=.126`, `F1=.182`.

## 7. Missing Anchors Added During This Branch

The following papers identified during closure have now been added as literature notes in this branch after source/metadata verification:

### D01
- PDF-to-Tree — Findings EMNLP 2024
- Intelligent Document Parsing — Findings EMNLP 2025
- READoc — Findings ACL 2025

### D02
- MultiDocFusion — EMNLP 2025
- HiChunk — ACL 2026

### D04 / D05
- Situated Embedding Models for Context-Aware Dense Retrieval — ACL 2026
- VDocRAG — CVPR 2025
- Query Rewriting in Retrieval-Augmented Large Language Models — EMNLP 2023
- RQ-RAG — COLM 2024
- GFM-RAG — NeurIPS 2025

### D06 / D07
- Sufficient Context — ICLR 2025
- SURE-RAG — 2026 arXiv preprint (emerging/supporting)
- SARA — ACL 2026
- The Distracting Effect — ACL 2025
- Attention Basin / AttnRank — ACL 2026

### D08
- Who's Who — Findings EMNLP 2024
- FaithfulRAG — ACL 2025
- MAGIC — Findings EMNLP 2025
- KCR — ACL 2026
- VersionRAG — 2025 arXiv preprint (emerging/supporting; D10 secondary)

### D09
- RARR — ACL 2023
- RioRAG — ACL 2026

### D11
- Mem0 — 2025 arXiv preprint (supporting)
- EviMem — 2026 arXiv preprint (emerging; D06 secondary)

### D12
- DecEx-RAG — EMNLP 2025 Industry
- Reflective RAG — Findings ACL 2026
- Data-Centric Perspectives on Agentic RAG — Findings ACL 2026

### D13
- A Reality Check on Context Utilisation for RAG — ACL 2025
- AgenticRAGTracer — Findings ACL 2026
- SafeRAG — ACL 2025
- How Does Knowledge Selection Help RAG? — Findings EMNLP 2025

### D14
- PipeRAG
- CacheBlend — EuroSys 2025
- RAGCache — canonical ACM TOCS 2026
- TeleRAG — MLSys 2026
- Safeguarding Privacy of Retrieval Data against Membership Inference Attacks
- end-to-end retrieved-content indirect prompt-injection work (USENIX Security 2026)

### Remaining emerging/watchlist items
These remain outside the core representative set even when a supporting note exists:
- SURE-RAG — 2026 preprint
- VersionRAG — 2025 preprint
- Mem0 — 2025 preprint
- EviMem — 2026 preprint
- Search-P1 — ACL Industry 2026 supporting work (not yet added)

Preprints are explicitly labeled as emerging/supporting and do not replace peer-reviewed canonical anchors.

## 8. Known Thin / Emerging Areas

- D03 systematic qualifier-preservation evaluation
- D08 provenance lineage / approval / applicability governance
- D10 deletion propagation, dependency-aware partial recomputation, update-stream benchmarks
- D11 memory governance / forgetting / ownership
- D14 observability/tracing, tenant isolation, derived-data deletion
- requirement-level evidence-gap localization + targeted retrieval remains an active project-research opportunity even though evidence sufficiency itself now has direct literature

## 9. Deferred Deliberately

The following are **not** silently performed during Phase 1:
- mass file/path renames
- deletion of legacy notes
- adding every possible adjacent paper merely to maximize paper count
- changing the project-specific F/R/D/A/P/C/T ontology into a literature claim
- claiming D01–D14 is a standard taxonomy from one survey

Those belong to later phases:
- Phase 2 Legacy Forensic Audit
- Phase 3 Version/Duplicate Cleanup
- Phase 4 Paper-Level Semantic Remapping
- Phase 7 Repository Normalization
- Phase 8 Automated Consistency Validation

## 10. Closure

**Phase 1 status: CLOSED.**

The next step is **Phase 2 — Legacy Forensic Audit**: compare deleted/legacy concepts against the closed D01–D14 taxonomy to identify over-pruning, stale remnants, duplicated concepts, and semantic loss.

## 11. Branch Validation

Final validation performed on `taxonomy-phase1-closure-20260927`:

- **108 / 108 changed literature notes** passed frontmatter/schema lint.
- No changed note contains a `taxonomy_home` / `primary_domain` mismatch for D01–D14.
- No changed note contains a `paradigm_tags` value outside the closed vocabulary.
- Required metadata fields checked on all changed literature notes: `paper_id`, `title`, `authors`, `year`, `publication_year`, `venue`, `verification_status`, `artifact_type`, `taxonomy_version`, `taxonomy_home`, `primary_domain`, `secondary_domains`, `paradigm_tags`, `adjacent_interfaces`.
- Existing domain filenames were deliberately not renamed, so Phase 1 does not introduce path-level breakage solely from the canonical display-name changes.
- README's old primary-domain counts are explicitly marked as a **historical pre-closure snapshot**; authoritative counts will be regenerated during Phase 7/8 normalization/lint after the branch is merged.

## 12. Phase 3 Duplicate Cleanup Queue

The following duplicate/preprint-formal pairs were detected while applying Phase 1. They are **not deleted in Phase 1** because branch code-search does not index non-default branches reliably enough to prove that no stale wikilink points to the older path. They must be handled by **link rewrite + deletion in one atomic Phase 3/7 change**.

| Keep | Delete after link rewrite | Reason |
|---|---|---|
| `(KDD 2025-08) PipeRAG - Fast RAG via Algorithm-System Co-design.md` | `(arXiv 2024-03) PipeRAG - Fast Retrieval-Augmented Generation via Algorithm-System Co-design.md` | same paper; formal KDD version supersedes arXiv-only note |
| `(TOCS 2026) RAGCache - Efficient Knowledge Caching for Retrieval-Augmented Generation.md` | `(TOCS 2025-11) RAGCache - Efficient Knowledge Caching for Retrieval-Augmented Generation.md` | same DOI `10.1145/3768628`; 2026 TOCS canonical record retained |
| `(ACL 2025-07) A Reality Check on Context Utilisation for RAG.md` | `(ACL 2025-07) A Reality Check on Context Utilisation for Retrieval-Augmented Generation.md` | same ACL paper / DOI `10.18653/v1/2025.acl-long.968`; duplicate literature note |

This queue is intentional: **do not count both copies as independent literature anchors**.

## 13. Post-Closure Consistency Note

After the initial Phase 1 validation, additional high-confidence metadata/remapping fixes were applied on the same branch (including D13 ownership cleanup and canonical DOI updates). These edits preserve the same schema rules and closed paradigm vocabulary. A final full-repository lint/count regeneration remains a Phase 8 task after Phase 3 duplicate cleanup, so any interim paper-count snapshot should be treated as provisional rather than a scientific claim.
