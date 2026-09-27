---
paper_id: "Jiang2024_PipeRAG"
title: "PipeRAG: Fast Retrieval-Augmented Generation via Algorithm-System Co-design"
authors:
  - "Wenqi Jiang"
  - "Shuai Zhang"
  - "Boran Han"
  - "Jie Wang"
  - "Bernie Wang"
  - "Tim Kraska"
year: 2024
publication_year: null
venue: "arXiv"
doi: "10.48550/arXiv.2403.05676"
arxiv: "2403.05676"
url: "https://arxiv.org/abs/2403.05676"
pdf_file: null
tags:
  - paper
  - rag-systems
  - pipelining
  - retrieval-generation-overlap
verification_status: "verified"
last_verified: "2026-09-27"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D14"
primary_domain: "D14"
secondary_domains: []
paradigm_tags: []
adjacent_interfaces:
  - "A02"
---

# PipeRAG: Fast Retrieval-Augmented Generation via Algorithm-System Co-design

## 一話摘要
PipeRAG 把 periodic retrieval 與 token generation 做 pipeline parallelism，並允許 flexible retrieval intervals，再用 performance model 根據硬體與生成狀態平衡 retrieval quality 與 latency。

## Taxonomy
- **D14 primary**：核心是 RAG-specific systems / serving co-design。
- **A02 adjacent**：涉及 inference efficiency，但不是 generic KV-cache method。
- 目前 canonical record 仍是 arXiv preprint；未在本 repo 假設其已有正式 peer-reviewed venue。

## 主要證據
官方摘要報告，在論文設定下最多可達 **2.6× end-to-end generation latency speedup**，同時改善 generation quality；此數字不可外推到任意硬體/工作負載。

## Source
- arXiv: https://arxiv.org/abs/2403.05676
