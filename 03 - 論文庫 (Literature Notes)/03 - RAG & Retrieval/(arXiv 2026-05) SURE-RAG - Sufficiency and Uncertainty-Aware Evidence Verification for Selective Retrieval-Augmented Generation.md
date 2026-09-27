---
paper_id: "Qiu2026_SURERAG"
title: "SURE-RAG: Sufficiency and Uncertainty-Aware Evidence Verification for Selective Retrieval-Augmented Generation"
authors:
  - "Jingxi Qiu"
  - "Zeyu Han"
  - "Cheng Huang"
year: 2026
publication_year: null
venue: "arXiv"
doi: null
arxiv: "2605.03534"
url: "https://arxiv.org/abs/2605.03534"
pdf_file: null
tags:
  - paper
  - evidence-sufficiency
  - selective-answering
  - uncertainty
verification_status: "verified"
last_verified: 2026-09-27
artifact_type: "method_paper"
research_questions:
  - "set_level_evidence_sufficiency"
  - "support_refute_insufficient_classification"
  - "selective_answering"
benchmark_ids:
  - "HotpotQA-RAG v3"
metrics:
  - "Macro-F1"
  - "Risk at Coverage"
taxonomy_version: "v2"
taxonomy_home: "D06"
primary_domain: "D06"
secondary_domains:
  - "D09"
paradigm_tags: []
adjacent_interfaces: []
---

# SURE-RAG

## 一話摘要
SURE-RAG 把 evidence sufficiency 明確視為 **set-level property**：單篇 passage 各自看似相關，不代表整組 evidence 已覆蓋必要 hops、沒有 unresolved conflict，或足以支持候選答案。

## 核心方法
- 先做 pair-level claim–evidence relation verification；
- 再把 coverage、relation strength、disagreement、conflict、retrieval uncertainty 聚合成 answer-level signals；
- 輸出 support / refute / insufficient 三分類；
- 只有 support 成立時才回答，否則 selective abstention。

## Taxonomy
- **D06 primary**：直接研究 evidence sufficiency verification 與 selective control。
- **D09 secondary**：sufficiency signal 最終影響 selective answering。
- 此文支持「sufficiency != relevance」，但仍未完整等同本專案的 requirement-slot decomposition → gap localization → targeted retrieval controller。

## Status
2026 arXiv preprint；作為 emerging/supporting literature，不取代 ICLR 2025 Sufficient Context 的 peer-reviewed canonical anchor。

## Sources
- https://arxiv.org/abs/2605.03534
