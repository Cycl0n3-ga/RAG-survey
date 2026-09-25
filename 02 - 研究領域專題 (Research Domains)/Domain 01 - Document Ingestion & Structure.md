---
title: "Domain 01 - Document Ingestion & Structure"
domain_id: "D01"
canonical: true
taxonomy_version: "v2"
lifecycle_stage: "Corpus Construction"
last_updated: "2026-09-25"
---

# Domain 01 - Document Ingestion & Structure

> [!IMPORTANT]
> 本頁是目前正式 RAG Taxonomy v2 的 D01。

## Core Question
原始文件如何轉換成保留結構、版面、來源與 metadata 的可檢索 corpus？

## Includes
- document parsing / structure recovery
- layout-aware ingestion
- table / chart / multimodal document structure
- metadata / source-span preservation

## Excludes
- chunk boundary optimization → D02
- knowledge extraction → D03
- retrieval ranking → D05

## Classification Rules
- 一篇論文可跨多個 Domain，但必須指定一個 Primary Domain。
- 其餘影響層級列為 Secondary Domains。
- GraphRAG、Hierarchical RAG、Adaptive RAG、Agentic RAG、Multimodal RAG 等使用 paradigm tags。
- 尚未由既有文獻直接支持的完整方法組合放入 `04 - 研究想法與待驗證提案`。

## Navigation
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Research Taxonomy & Domain Map|RAG Research Taxonomy & Domain Map]]
- [[00 - 導覽與心智圖 (Navigation & MOC)/RAG Paradigm Tags|RAG Paradigm Tags]]
