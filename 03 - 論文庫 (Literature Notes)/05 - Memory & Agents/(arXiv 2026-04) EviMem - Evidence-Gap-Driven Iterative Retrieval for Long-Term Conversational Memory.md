---
paper_id: "Li2026_EviMem"
title: "EviMem: Evidence-Gap-Driven Iterative Retrieval for Long-Term Conversational Memory"
authors:
  - "Yuyang Li"
  - "Yime He"
  - "Zeyu Zhang"
  - "Dong Gong"
year: 2026
publication_year: null
venue: "arXiv"
doi: null
arxiv: "2604.27695"
url: "https://arxiv.org/abs/2604.27695"
pdf_file: null
tags:
  - paper
  - conversational-memory
  - evidence-gap
  - iterative-retrieval
verification_status: "verified"
last_verified: 2026-09-27
artifact_type: "method_paper"
research_questions:
  - "long_term_conversational_memory"
  - "evidence_gap_diagnosis"
  - "targeted_query_refinement"
benchmark_ids:
  - "LoCoMo"
metrics:
  - "Judge Accuracy"
  - "Latency"
taxonomy_version: "v2"
taxonomy_home: "D11"
primary_domain: "D11"
secondary_domains:
  - "D06"
paradigm_tags:
  - "memory_augmented_rag"
adjacent_interfaces: []
---

# EviMem

## 一話摘要
EviMem 結合長期 conversational memory hierarchy 與 evidence-gap-driven iterative retrieval：先檢查累積 memory evidence 是否足夠，再診斷缺少什麼，最後針對 gap 做 targeted query refinement。

## 核心組件
- **LaceMem**：coarse-to-fine conversational evidence memory hierarchy。
- **IRIS**：sufficiency evaluation → evidence-gap diagnosis → targeted iterative retrieval。

## Taxonomy
- **D11 primary**：persistent long-term conversational memory 是 task/state foundation。
- **D06 secondary**：明確使用 insufficiency/evidence-gap signal 控制後續 retrieval。
- 這篇表示 gap-aware retrieval 已有直接鄰近工作，因此本專案不能宣稱「首次提出 evidence-gap-driven iterative retrieval」；更可區分的研究空間是 requirement-level decomposition、explicit coverage state 與更一般化的 controller。

## Status
2026 arXiv preprint；作 emerging adjacent work。

## Sources
- https://arxiv.org/abs/2604.27695
