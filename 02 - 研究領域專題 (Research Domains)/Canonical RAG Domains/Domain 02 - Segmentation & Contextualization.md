---
title: "Domain 02 - Segmentation & Contextualization"
domain_id: "D02"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Corpus Construction"
migration_status: "scaffold"
last_updated: "2026-09-25"
---

# Domain 02 - Segmentation & Contextualization

> [!IMPORTANT] Canonical Domain v2
> 本頁依「RAG lifecycle 中的研究問題」分類。GraphRAG、Hierarchical RAG、Adaptive RAG、Agentic RAG、Multimodal RAG 等不再與 lifecycle Domain 平行，而以 paradigm tags 管理。
> 目前為 migration scaffold；舊 Domain 尚未刪除。

## Core Question
文件應被切成什麼 retrieval units，且切分後如何保留足夠上下文？

## Includes
- fixed / recursive / semantic / structure-aware chunking
- sentence / passage / proposition retrieval units
- parent-child segmentation
- contextual chunk representation
- retrieval granularity

## Excludes
- entity/relation/event extraction → D03
- index structures → D04
- adaptive retrieval control → D06

## Classification Rules
- 一篇論文可跨多個 Domain，但必須指定一個 Primary Domain。
- 其餘影響層級列為 Secondary Domains。
- 架構型名稱使用 paradigm tags，而非新增 top-level Domain。
- 尚未由既有文獻直接支持的完整方法組合放入 `04 - 研究想法與待驗證提案`。

## Navigation
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|Canonical Taxonomy v2]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/Canonical RAG Domain Migration Map|Migration Map]]
