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

## Representative Notes

**Current primary-note coverage: 20**

- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(arXiv 2024-08) RAGChecker - A Fine-grained Framework for Diagnosing Retrieval-Augmented Generation|RAGChecker]]
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(EACL 2024-03) RAGAS - Automated Evaluation of Retrieval Augmented Generation|RAGAS]]
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(NAACL 2024-06) ARES - An Automated Evaluation Framework for Retrieval-Augmented Generation Systems|ARES]]
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(arXiv 2024-06) RAGBench - Explainable Benchmark for Retrieval-Augmented Generation Systems|RAGBench]]
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(CMC 2026-08) Do LLMs Know When Evidence is Insufficient - An Evidence Sufficiency Benchmark|Evidence Sufficiency Benchmark]]
- [[03 - 論文庫 (Literature Notes)/06 - Benchmarks & Evaluation/(ACL 2026-08) ReportLogic - Evaluating Logical Quality in Deep Research Reports|ReportLogic]]

## Evaluation Artifact Types

本 repo 保留四種評測工件的明確區分：

| Type | Meaning | Example |
|---|---|---|
| Benchmark / Shared Task | 定義 task、protocol、split 或競賽規則 | CRAG / shared task |
| Dataset / Corpus | 實際資料與 gold annotations | BEIR / QASPER / DocRED |
| Metric | scoring formula / measurement | Recall@k / nDCG / Faithfulness |
| Evaluation Framework / Tool | 執行多個 metrics 或診斷流程的軟體 | RAGAS / RAGChecker |

**Benchmark ≠ Dataset ≠ Metric ≠ Evaluation Framework.**

### Text-only Evaluation Boundary

若標記為 text-only，至少要說明：
- 原始 corpus 是否含 image / chart / layout；
- model input 是 extracted text/Markdown，還是 page image / VLM；
- gold answer 是否依賴 visual bounding box 或圖像內容；
- table 是 text serialization 還是 rendered image。

這是 repo 的 evaluation convention，用來避免把 multimodal benchmark 誤標成純文字 benchmark。


## Navigation
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Benchmark Catalog|RAG Benchmark Catalog]]
- [[02 - 研究領域專題 (Research Domains)/Domain 09 - Grounded Generation Attribution & Long-form Synthesis|D09 Grounded Generation & Long-form Synthesis]]
