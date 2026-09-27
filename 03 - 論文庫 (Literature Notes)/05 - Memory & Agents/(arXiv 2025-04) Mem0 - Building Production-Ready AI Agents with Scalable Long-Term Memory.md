---
paper_id: "Chhikara2025_Mem0"
title: "Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory"
authors:
  - "Prateek Chhikara"
  - "Dev Khant"
  - "Saket Aryan"
  - "Taranjeet Singh"
  - "Deshraj Yadav"
year: 2025
publication_year: 2025
venue: "ECAI 2025"
doi: "10.3233/FAIA251160"
arxiv: "2504.19413"
url: "https://doi.org/10.3233/FAIA251160"
pdf_file: null
tags:
  - paper
  - long-term-memory
  - conversational-memory
  - graph-memory
verification_status: "verified"
last_verified: 2026-09-28
artifact_type: "method_paper"
research_questions:
  - "persistent_conversation_memory"
  - "memory_extraction_consolidation"
  - "graph_memory"
benchmark_ids:
  - "LoCoMo"
metrics:
  - "LLM-as-a-Judge"
  - "Latency"
  - "Token Cost"
taxonomy_version: "v2"
taxonomy_home: "D11"
primary_domain: "D11"
secondary_domains: []
paradigm_tags:
  - "memory_augmented_rag"
adjacent_interfaces:
  - "A04"
---

# Mem0

## 一話摘要
Mem0 研究可跨 multi-session 對話持續存在的 memory lifecycle：從 ongoing conversations 動態抽取 salient information、consolidate 成 persistent memory，再在後續互動中檢索；另提出 graph-memory variant 表示關係結構。

## Taxonomy
- **D11 primary**：核心是 persistent derived-state formation / consolidation / retrieval。
- **A04 adjacent**：主要應用情境是 AI agents，但「agent」不是其 primary research problem。
- 不把 full conversation history 塞入 context 視為 D11；重點在 persistent memory state 的建立與管理。

## Status
已正式發表於 ECAI 2025（Frontiers in Artificial Intelligence and Applications；DOI 10.3233/FAIA251160）。原 arXiv:2504.19413 保留作 preprint identifier。

## Sources
- https://doi.org/10.3233/FAIA251160
- https://arxiv.org/abs/2504.19413
