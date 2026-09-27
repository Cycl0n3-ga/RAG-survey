---
paper_id: "Lin2026_TeleRAG"
title: "TeleRAG: Efficient Retrieval-Augmented Generation Inference with Lookahead Retrieval"
authors:
  - "Chien-Yu Lin"
  - "Keisuke Kamahori"
  - "Yiyu Liu"
  - "Xiaoxiang Shi"
  - "Madhav Kashyap"
  - "Yile Gu"
  - "Rulin Shao"
  - "Zihao Ye"
  - "Kan Zhu"
  - "Rohan Kadekodi"
  - "Stephanie Wang"
  - "Arvind Krishnamurthy"
  - "Luis Ceze"
  - "Baris Kasikci"
year: 2026
publication_year: 2026
venue: "MLSys 2026"
doi: null
arxiv: "2502.20969"
url: "https://proceedings.mlsys.org/paper_files/paper/2026/hash/7fd522b89ac21009b7bbe7560a9a5add-Abstract-Conference.html"
pdf_file: null
tags:
  - paper
  - rag-systems
  - lookahead-retrieval
  - prefetching
  - scheduling
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

# TeleRAG: Efficient RAG Inference with Lookahead Retrieval

## 一話摘要
TeleRAG 提出 **lookahead retrieval**：預測接下來需要的 retrieval data，讓 CPU→GPU transfer 與 LLM generation 平行進行，並搭配 prefetching scheduler 與 cache-aware scheduler 支援 multi-GPU inference。

## Taxonomy
- **D14 primary**：端到端 RAG inference/serving system。
- **A02 adjacent**：memory transfer/cache efficiency interface。

## 主要證據
MLSys 2026 proceedings 摘要報告：
- single-query average end-to-end latency 最多降低 **1.98×**
- batched average throughput 最多提升 **1.83×**
並改善有限 GPU memory 下的部署效率。

## Source
- MLSys 2026: https://proceedings.mlsys.org/paper_files/paper/2026/hash/7fd522b89ac21009b7bbe7560a9a5add-Abstract-Conference.html
