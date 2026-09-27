---
paper_id: "Jin2026_RAGCache"
title: "RAGCache: Efficient Knowledge Caching for Retrieval-Augmented Generation"
authors:
  - "Chao Jin"
  - "Zili Zhang"
  - "Xuanlin Jiang"
  - "Fangyue Liu"
  - "Shufan Liu"
  - "Xuanzhe Liu"
  - "Xin Jin"
year: 2024
publication_year: 2026
venue: "ACM Transactions on Computer Systems 44(1)"
doi: "10.1145/3768628"
arxiv: "2404.12457"
url: "https://doi.org/10.1145/3768628"
pdf_file: null
tags:
  - paper
  - rag-systems
  - knowledge-caching
  - retrieval-inference-overlap
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

# RAGCache: Efficient Knowledge Caching for Retrieval-Augmented Generation

## 一話摘要
RAGCache 利用 RAG 的 retrieval pattern，在 GPU/host memory hierarchy 中以 knowledge tree 組織並快取 retrieved knowledge 的 intermediate states，再以 dynamic speculative pipelining 重疊 retrieval 與 LLM generation。

## Taxonomy
- **D14 primary**：RAG-specific systems / serving。
- **A02 adjacent**：涉及 inference-state caching，但不是 generic model KV compression。
- canonical record 採 **ACM TOCS 2026** 正式 journal version，而不是只保留 2024 arXiv。

## 主要證據
正式/作者公開摘要報告，相較 vLLM + Faiss baseline，論文設定下可達：
- TTFT 最多 **4× reduction**
- throughput 最多 **2.1× improvement**

## Source
- DOI: https://doi.org/10.1145/3768628
