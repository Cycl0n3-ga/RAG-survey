---
title: "Domain 07 - Context Construction & Evidence Utilization"
domain_id: "D07"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Post-Retrieval"
migration_status: "scaffold"
last_updated: "2026-09-25"
---

# Domain 07 - Context Construction & Evidence Utilization

> [!IMPORTANT] Canonical Domain v2
> 本頁依「RAG lifecycle 中的研究問題」分類。GraphRAG、Hierarchical RAG、Adaptive RAG、Agentic RAG、Multimodal RAG 等不再與 lifecycle Domain 平行，而以 paradigm tags 管理。
> 目前為 migration scaffold；舊 Domain 尚未刪除。

## Core Question
候選 evidence 找到後，如何建構有限 context，並確保模型實際使用關鍵證據？

## Includes
- context filtering / dedup / ordering
- context packing / budget allocation
- retrieval-aware context compression
- evidence organization
- lost-in-the-middle / position effects
- parametric-vs-retrieved knowledge interaction

## Excludes
- KV-cache compression 本身 → Adjacent Interface
- retrieval ranking → D05
- claim-level output verification → D09

## Classification Rules
- 一篇論文可跨多個 Domain，但必須指定一個 Primary Domain。
- 其餘影響層級列為 Secondary Domains。
- 架構型名稱使用 paradigm tags，而非新增 top-level Domain。
- 尚未由既有文獻直接支持的完整方法組合放入 `04 - 研究想法與待驗證提案`。

## Navigation
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Canonical Taxonomy v2]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/Canonical RAG Domain Migration Map|Migration Map]]
