---
title: "Domain 13 - RAG Evaluation & Failure Attribution"
domain_id: "D13"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Evaluation"
migration_status: "scaffold"
last_updated: "2026-09-25"
---

# Domain 13 - RAG Evaluation & Failure Attribution

> [!IMPORTANT] Canonical Domain v2
> 本頁依「RAG lifecycle 中的研究問題」分類。GraphRAG、Hierarchical RAG、Adaptive RAG、Agentic RAG、Multimodal RAG 等不再與 lifecycle Domain 平行，而以 paradigm tags 管理。
> 目前為 migration scaffold；舊 Domain 尚未刪除。

## Core Question
如何分離評估 retrieval、evidence、generation 與 end-to-end failure，並定位錯誤真正發生在哪一層？

## Includes
- benchmark / dataset / metric / evaluation-framework separation
- retrieval evaluation
- evidence coverage / sufficiency evaluation
- faithfulness / citation evaluation
- long-form evaluation
- oracle experiments
- error attribution / propagation
- meta-evaluation

## Excludes
- runtime observability implementation → D14
- project proposal 冒充 benchmark

## Classification Rules
- 一篇論文可跨多個 Domain，但必須指定一個 Primary Domain。
- 其餘影響層級列為 Secondary Domains。
- 架構型名稱使用 paradigm tags，而非新增 top-level Domain。
- 尚未由既有文獻直接支持的完整方法組合放入 `04 - 研究想法與待驗證提案`。

## Navigation
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Canonical Taxonomy v2]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/Canonical RAG Domain Migration Map|Migration Map]]
