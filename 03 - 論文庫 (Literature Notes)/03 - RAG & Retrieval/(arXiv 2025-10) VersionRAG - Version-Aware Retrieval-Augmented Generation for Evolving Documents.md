---
paper_id: "Huwiler2025_VersionRAG"
title: "VersionRAG: Version-Aware Retrieval-Augmented Generation for Evolving Documents"
authors:
  - "Daniel Huwiler"
  - "Kurt Stockinger"
  - "Jonathan Fürst"
year: 2025
publication_year: null
venue: "arXiv"
doi: null
arxiv: "2510.08109"
url: "https://arxiv.org/abs/2510.08109"
pdf_file: null
tags:
  - paper
  - version-aware-rag
  - evolving-documents
  - temporal-validity
verification_status: "verified"
last_verified: 2026-09-27
artifact_type: "method_paper"
research_questions:
  - "version_aware_retrieval"
  - "document_evolution"
  - "change_tracking"
benchmark_ids:
  - "VersionQA"
metrics:
  - "Accuracy"
  - "Indexing Token Cost"
taxonomy_version: "v2"
taxonomy_home: "D08"
primary_domain: "D08"
secondary_domains:
  - "D10"
paradigm_tags:
  - "temporal_rag"
adjacent_interfaces: []
---

# VersionRAG

## 一話摘要
VersionRAG 顯式建模 evolving documents 的版本序列、content boundaries 與版本間 changes，並依 query intent 執行 version-aware filtering / change tracking。

## Taxonomy
- **D08 primary**：主要 scientific question 是 query-time 哪個版本適用，以及如何處理 version-sensitive questions。
- **D10 secondary**：需要保存 version identity、change history 與可更新的 version-aware index。
- 硬邊界：**D10 maintains versions; D08 reasons over versions.**

## Status
2025 arXiv preprint；可作 temporal/version reconciliation 的 emerging evidence，不視為已建立的 survey consensus。

## Sources
- https://arxiv.org/abs/2510.08109
