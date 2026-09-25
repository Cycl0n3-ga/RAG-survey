---
title: "Domain 13 - RAG Evaluation & Failure Attribution"
domain_id: "D13"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Evaluation"
last_updated: "2026-09-25"
---

# Domain 13 - RAG Evaluation & Failure Attribution

## Core Question
如何分層評估 retrieval、evidence、context、generation 與 end-to-end quality，並定位 failure 真正發生在哪一層？

```mermaid
flowchart LR
    R["Retrieval"] -.-> E["Evaluation"]
    EV["Evidence"] -.-> E
    C["Context"] -.-> E
    G["Generation"] -.-> E
    E --> F["Failure Attribution"]
    O["Oracle / Ablation"] -.-> F
```

## Includes
- benchmark / dataset / metric / evaluation framework
- retrieval evaluation
- evidence coverage / sufficiency evaluation
- context utilization evaluation
- faithfulness / citation evaluation
- long-form evaluation
- oracle / ablation protocol
- failure attribution / error propagation
- meta-evaluation

## Excludes
- retrieval algorithm design → D05
- runtime observability / serving telemetry → D14
- project-specific benchmark proposal presented as public benchmark

## Level-2 Topics
- Retrieval Evaluation
- Evidence Evaluation
- Context Utilization Evaluation
- Generation / Faithfulness Evaluation
- Citation Evaluation
- Long-form Evaluation
- Oracle Evaluation
- Failure Attribution

## Boundary
```text
Benchmark != Dataset != Metric != Evaluation Framework
```
End-to-end score 不能直接說明 bottleneck 位於 retrieval、evidence construction、context utilization 或 generation。

## Navigation
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Benchmark Catalog|RAG Benchmark Catalog]]
- [[02 - 研究領域專題 (Research Domains)/Domain 09 - Grounded Generation Attribution & Long-form Synthesis|D09 Grounded Generation & Long-form Synthesis]]
