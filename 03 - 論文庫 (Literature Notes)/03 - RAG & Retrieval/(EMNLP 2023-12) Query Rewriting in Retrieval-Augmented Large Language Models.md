---
paper_id: "Ma2023_QueryRewritingRAG"
title: "Query Rewriting in Retrieval-Augmented Large Language Models"
authors:
  - "Xinbei Ma"
  - "Yeyun Gong"
  - "Pengcheng He"
  - "Hai Zhao"
  - "Nan Duan"
year: 2023
publication_year: 2023
venue: "EMNLP 2023"
doi: "10.18653/v1/2023.emnlp-main.322"
arxiv: null
url: "https://aclanthology.org/2023.emnlp-main.322/"
pdf_file: null
tags:
  - paper
  - query-rewriting
  - rewrite-retrieve-read
verification_status: "verified"
last_verified: "2026-09-27"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains: []
paradigm_tags: []
adjacent_interfaces: []
---

# Query Rewriting in Retrieval-Augmented Large Language Models

## 一話摘要
把傳統 **Retrieve → Read** 改成 **Rewrite → Retrieve → Read**：先用 LLM 將原始輸入改寫成更適合搜尋的 query，再讓 retriever/search engine 取回 evidence；另以 frozen reader feedback 訓練小型 query rewriter。

## Taxonomy
- **D05 primary**：核心 intervention 是 query transformation / retrieval-query alignment。
- 不因使用 reader feedback 就歸 D12；其 action space 並非一般 RAG orchestration。

## Source
- ACL Anthology: https://aclanthology.org/2023.emnlp-main.322/
