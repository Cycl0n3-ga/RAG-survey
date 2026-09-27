---
paper_id: "Yao2025_CacheBlend"
title: "CacheBlend: Fast Large Language Model Serving for RAG with Cached Knowledge Fusion"
authors:
  - "Jiayi Yao"
  - "Hanchen Li"
  - "Yuhan Liu"
  - "Siddhant Ray"
  - "Yihua Cheng"
  - "Qizheng Zhang"
  - "Kuntai Du"
  - "Shan Lu"
  - "Junchen Jiang"
year: 2025
publication_year: 2025
venue: "EuroSys 2025"
doi: "10.1145/3689031.3696098"
arxiv: "2405.16444"
url: "https://doi.org/10.1145/3689031.3696098"
pdf_file: null
tags:
  - paper
  - rag-systems
  - kv-cache
  - knowledge-cache-fusion
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

# CacheBlend: Fast Large Language Model Serving for RAG with Cached Knowledge Fusion

## 一話摘要
CacheBlend 解決 RAG 輸入含多個、且不一定位於 prefix 的 retrieved chunks 時，預先計算的 KV caches 無法直接正確拼接的問題；它重用 cached KVs，並只選擇性重算少量 token 的 KV values。

## Taxonomy
- **D14 primary**：RAG-specific serving/caching system。
- **A02 adjacent**：技術核心涉及 KV cache，但問題設定是多 retrieved chunks 的 RAG serving。

## 主要證據
EuroSys 2025 正式論文報告，相較 full KV recomputation：
- TTFT 降低 **2.2–3.3×**
- throughput 提升 **2.8–5×**
並維持 generation quality；結果只適用於其測試模型、資料集與硬體。
Microsoft Research 將此工作列為 **EuroSys 2025 Best Paper Award**。

## Source
- DOI: https://doi.org/10.1145/3689031.3696098
