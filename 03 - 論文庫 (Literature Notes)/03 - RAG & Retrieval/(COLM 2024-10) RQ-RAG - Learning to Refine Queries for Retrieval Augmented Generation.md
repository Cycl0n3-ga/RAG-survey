---
paper_id: "Chan2024_RQRAG"
title: "RQ-RAG: Learning to Refine Queries for Retrieval Augmented Generation"
authors:
  - "Chi-Min Chan"
  - "Chunpu Xu"
  - "Ruibin Yuan"
  - "Hongyin Luo"
  - "Wei Xue"
  - "Yike Guo"
  - "Jie Fu"
year: 2024
publication_year: 2024
venue: "COLM 2024"
doi: null
arxiv: "2404.00610"
url: "https://arxiv.org/abs/2404.00610"
pdf_file: null
tags:
  - paper
  - query-refinement
  - query-decomposition
  - disambiguation
verification_status: "verified"
last_verified: "2026-09-27"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains: []
paradigm_tags:
  - "multi_hop_rag"
adjacent_interfaces: []
---

# RQ-RAG: Learning to Refine Queries for Retrieval Augmented Generation

## 一話摘要
針對 ambiguous / complex queries，讓模型顯式學會 **rewrite、decompose、disambiguate**，再執行 retrieval；因此它是 D05 Query Understanding 的直接 anchor，而不是單純 retriever paper。

## Taxonomy
- **D05 primary**：query refinement / decomposition / disambiguation。
- multi-hop 使用情境可標 `multi_hop_rag`，但 Domain 仍由 query-side research problem 決定。

## Source
- arXiv: https://arxiv.org/abs/2404.00610
- COLM 2024 peer-reviewed conference paper.
