# Research Domains

> [!IMPORTANT]
> 本資料夾就是目前唯一正式的 RAG taxonomy：**14 個 Research Domains（D01–D14）**。

## Structure

```text
Research Domains
├── D01 Document Parsing & Structure Recovery
├── D02 Segmentation & Retrieval Granularity
├── D03 Knowledge Extraction & Consolidation
├── D04 Representation & Indexing
├── D05 Query Understanding & Retrieval
├── D06 Evidence Sufficiency & Retrieval Control
├── D07 Context Construction & Utilization
├── D08 Evidence Reconciliation
├── D09 Grounded Generation & Long-form Synthesis
├── D10 Knowledge & Index Maintenance
├── D11 Persistent Memory Management
├── D12 RAG Orchestration & Action Control
├── D13 Evaluation & Failure Attribution
└── D14 RAG Systems, Security & Privacy
```

## Domain Index

- [[02 - 研究領域專題 (Research Domains)/Domain 01 - Document Parsing & Structure Recovery|D01 Document Parsing & Structure Recovery]]
- [[02 - 研究領域專題 (Research Domains)/Domain 02 - Segmentation & Retrieval Granularity|D02 Segmentation & Retrieval Granularity]]
- [[02 - 研究領域專題 (Research Domains)/Domain 03 - Knowledge Extraction & Consolidation|D03 Knowledge Extraction & Consolidation]]
- [[02 - 研究領域專題 (Research Domains)/Domain 04 - Representation & Indexing|D04 Representation & Indexing]]
- [[02 - 研究領域專題 (Research Domains)/Domain 05 - Query Understanding & Retrieval|D05 Query Understanding & Retrieval]]
- [[02 - 研究領域專題 (Research Domains)/Domain 06 - Evidence Sufficiency & Retrieval Control|D06 Evidence Sufficiency & Retrieval Control]]
- [[02 - 研究領域專題 (Research Domains)/Domain 07 - Context Construction & Utilization|D07 Context Construction & Utilization]]
- [[02 - 研究領域專題 (Research Domains)/Domain 08 - Evidence Reconciliation|D08 Evidence Reconciliation]]
- [[02 - 研究領域專題 (Research Domains)/Domain 09 - Grounded Generation & Long-form Synthesis|D09 Grounded Generation & Long-form Synthesis]]
- [[02 - 研究領域專題 (Research Domains)/Domain 10 - Knowledge & Index Maintenance|D10 Knowledge & Index Maintenance]]
- [[02 - 研究領域專題 (Research Domains)/Domain 11 - Persistent Memory Management|D11 Persistent Memory Management]]
- [[02 - 研究領域專題 (Research Domains)/Domain 12 - RAG Orchestration & Action Control|D12 RAG Orchestration & Action Control]]
- [[02 - 研究領域專題 (Research Domains)/Domain 13 - Evaluation & Failure Attribution|D13 Evaluation & Failure Attribution]]
- [[02 - 研究領域專題 (Research Domains)/Domain 14 - RAG Systems, Security & Privacy|D14 RAG Systems, Security & Privacy]]

## Other Axes

- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Adjacent Interfaces|Adjacent Interfaces]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Taxonomy & Domain Map]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Benchmark Catalog|Benchmark Catalog]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/Survey Papers Index|Survey Papers Index]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/技術全景與 Pareto 權衡分析 (Trade-offs)|技術全景與 Pareto 權衡分析 (Trade-offs)]]

## Literature Coverage Snapshot

> [!WARNING]\n> 下表是 **Phase 1 closure 前的 historical snapshot**。2026-09-27 已完成多筆 primary-domain remap，因此這些數字不再視為 authoritative；最新統計應在 Phase 7/8 normalization + lint 後重新產生。

| Domain | Primary notes |
|---|---:|
| D01 | 2 |
| D02 | 3 |
| D03 | 12 |
| D04 | 6 |
| D05 | 17 |
| D06 | 4 |
| D07 | 3 |
| D08 | 4 |
| D09 | 6 |
| D10 | 1 |
| D11 | 6 |
| D12 | 3 |
| D13 | 21 |
| D14 | 2 |

目前的缺口已不適合用「再加更多 Domain」處理：D08 已有 temporal/conflict + RA-RAG source-reliability anchors，仍缺 provenance lineage / approval-state / applicability-scope arbitration；D10 已有 AURORA，但缺 production CRUD / deletion / invalidation；D12 已有 GraphReader + RAG-Critic 的 direct method anchors，但 coverage 仍比 retrieval/evaluation 薄；D14 已有 METIS systems + PoisonedRAG security anchors，剩下 observability/tracing 與 privacy/access-control 較薄。

## Phase 1 Canonical Names — 2026-09-27

The canonical display names above are authoritative after Phase 1 closure. Existing filenames remain unchanged until Phase 7 path normalization.

Key cleanup outcomes:
- D03 preservation is a quality lens; canonical research problem is extraction + consolidation.
- D08 is restored to general evidence reconciliation instead of temporal-only scope.
- D11 is defined by persistent derived-state lifecycle, not the word “memory”.
- D12 is defined by state→action orchestration, not by whether a system uses agents.
- D14 no longer uses generic robustness as a catch-all; adversarial integrity/security remains in D14 while ordinary distractor/context robustness is assigned to the relevant lifecycle domain.

## Audit Trail
- [[00 - 導覽與心智圖 (Navigation & MOC)/Phase 1 Taxonomy Closure Audit - 2026-09-27|Phase 1 Taxonomy Closure Audit]]
