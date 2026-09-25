---
title: "Domain 09 - Grounded Generation Attribution & Long-form Synthesis"
domain_id: "D09"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Generation"
last_updated: "2026-09-25"
---

# Domain 09 - Grounded Generation, Attribution & Long-form Synthesis

## Core Question
如何由 evidence 產生可驗證、可歸因的答案或長篇報告，並在無法支持時選擇修正或 abstain？

```mermaid
flowchart LR
    CTX["Grounded Context"] --> GEN["Generate"]
    GEN -. "long-form" .-> PLAN["Outline / Section Plan"]
    PLAN --> LONG["Section Synthesis"]
    GEN --> CL["Claims"]
    LONG --> CL
    CL --> VER["Claim-Evidence Verification"]
    VER --> CITE["Citation / Attribution"]
    CITE --> OUT["Answer / Report"]
    VER -. "unsupported" .-> FIX["Repair / Retrieve / Abstain"]
```

## Includes
- grounded generation
- claim decomposition
- claim-evidence verification
- faithfulness / groundedness
- citation / attribution
- abstention
- outline / section planning
- long-form synthesis
- revision / cross-section consistency

## Excludes
- retrieval algorithm → D05/D06
- context packing → D07
- benchmark methodology → D13

## Level-2 Topics
- Grounded Generation
- Claim Verification
- Citation / Attribution
- Abstention
- Long-form Report Generation
- Evidence-to-Section Planning
- Revision / Consistency

## Boundary
```text
Citation present
    != citation relevant
    != citation entails claim
    != answer complete
```

## Representative Notes

**Current primary-note coverage: 6**

- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(NAACL 2024-06) Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models|STORM]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2024-11) OpenScholar - Synthesizing Scientific Literature with Retrieval-Augmented Language Models|OpenScholar]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(ACL 2026-08) EviReport - From Reasoned Outlines to Evidence Tracked Long-Form Reports|EviReport]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(ACL 2026-08) EFSG - Evidence-First Structured Generation for Multilingual RAG Report Generation|EFSG]]
- [[03 - 論文庫 (Literature Notes)/05 - Memory & Agents/(arXiv 2022-03) Teaching language models to support answers with verified quotes|GopherCite]]
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(EMNLP 2023-12) Enabling Large Language Models to Generate Text with Citations|ALCE / Citation-grounded generation]]

## Navigation
- [[02 - 研究領域專題 (Research Domains)/Domain 07 - Context Construction & Evidence Utilization|D07 Context Construction & Evidence Utilization]]
- [[02 - 研究領域專題 (Research Domains)/Domain 13 - RAG Evaluation & Failure Attribution|D13 RAG Evaluation & Failure Attribution]]
