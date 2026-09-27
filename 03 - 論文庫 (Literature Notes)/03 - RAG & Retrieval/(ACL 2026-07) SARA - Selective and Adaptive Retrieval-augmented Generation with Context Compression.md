---
paper_id: "Jin2026_SARA"
title: "SARA: Selective and Adaptive Retrieval-augmented Generation with Context Compression"
authors:
  - "Yiqiao Jin"
  - "Kartik Sharma"
  - "Vineeth Rakesh"
  - "Yingtong Dou"
  - "Menghai Pan"
  - "Mahashweta Das"
  - "Srijan Kumar"
year: 2026
publication_year: 2026
venue: "ACL 2026"
doi: "10.18653/v1/2026.acl-long.661"
arxiv: null
url: "https://aclanthology.org/2026.acl-long.661/"
pdf_file: null
tags:
  - paper
  - context-compression
  - token-budget
  - evidence-selection
verification_status: "verified"
last_verified: "2026-09-27"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D07"
primary_domain: "D07"
secondary_domains:
  - "D04"
paradigm_tags: []
adjacent_interfaces: []
---

# SARA: Selective and Adaptive Retrieval-augmented Generation with Context Compression

## 一話摘要
SARA 直接研究固定 token budget 下如何構造 RAG context：少量重要 passages 保留自然語言細節，其餘 evidence 壓成 semantic vectors，再利用這些 compressed representations 進行 iterative evidence reranking。

## Taxonomy
- **D07 primary**：context construction / compression / budget allocation。
- **D04 secondary**：方法使用 semantic compression vectors 作 representation。
- 與 generic prompt/KV compression 不同；其問題設定明確是 retrieved evidence 的 context construction。

## Source
- ACL Anthology: https://aclanthology.org/2026.acl-long.661/
