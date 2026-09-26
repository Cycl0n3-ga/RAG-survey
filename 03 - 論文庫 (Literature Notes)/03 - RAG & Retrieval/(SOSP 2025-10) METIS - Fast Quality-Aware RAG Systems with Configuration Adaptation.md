---
paper_id: "Ray2025_METIS"
title: "METIS: Fast Quality-Aware RAG Systems with Configuration Adaptation"
authors:
  - "Siddhant Ray"
  - "Rui Pan"
  - "Zhuohan Gu"
  - "Kuntai Du"
  - "Shaoting Feng"
  - "Ganesh Ananthanarayanan"
  - "Ravi Netravali"
  - "Junchen Jiang"
year: 2024
publication_year: 2025
venue: "SOSP 2025"
doi: "10.1145/3731569.3764855"
arxiv: "2412.10543"
url: "https://doi.org/10.1145/3731569.3764855"
pdf_file: null
tags:
  - paper
  - rag-systems
  - serving
  - scheduling
  - configuration-adaptation
verification_status: "verified"
last_verified: 2026-09-26
artifact_type: "method_paper"
research_questions:
  - "rag_serving_scheduling"
  - "quality_latency_tradeoff"
  - "per_query_configuration_adaptation"
benchmark_ids:
  - "four RAG-QA workloads reported by the paper"
metrics:
  - "Response Latency"
  - "Throughput"
  - "Generation Quality"
taxonomy_version: "v2"
taxonomy_home: "D14"
primary_domain: "D14"
secondary_domains:
  - "D05"
  - "D06"
  - "D07"
paradigm_tags:
  - "adaptive_rag"
adjacent_interfaces:
  - "A02"
---

# METIS: Fast Quality-Aware RAG Systems with Configuration Adaptation

## 一話摘要 (TL;DR)
METIS 是直接的 **RAG systems / serving** 工作：它不只調整 retrieval quality，也把每個 query 的 RAG configuration 與 GPU scheduling 聯合最佳化，在品質約束下選擇 retrieval chunk 數、synthesis method 與 intermediate summary length。

## 研究背景與問題定義
更多 retrieved context 往往提高可能的 evidence coverage，卻同時增加 prefill / synthesis latency、GPU memory 與排隊成本。固定 RAG configuration 無法適應 query complexity；只做 scheduler 又看不到 configuration 對 quality 的影響。METIS 因此把 **quality-delay-resource trade-off** 當成 system problem。

## 核心方法
METIS 先以輕量 query profiler 估計 query 需要多少 pieces of information、是否需要 joint reasoning，藉此刪除明顯不合適的 configuration；之後再於縮小後的 configuration space 中，聯合決定：
- retrieval 的 chunk 數；
- chunks 要 joint processing 還是分開處理；
- 是否先摘要以及 intermediate length；
- 哪些 LLM calls 應被共同排程 / batching。

這使「選 configuration」與「GPU scheduler 當下資源狀態」不再彼此獨立。

## 主要實驗證據
- **Page 1 / formal abstract**：在四個 RAG-QA datasets 上，相對既有 RAG optimization schemes，generation latency 降低 **1.64–2.54×**，同時維持 generation quality。
- **Page 2**：per-query configuration 相對固定 configuration，在論文分析中可同時取得更高品質與更低 delay；profiler 約為完整 RAG query execution delay 的十分之一。
- **Page 10**：在相近品質與 response-delay 條件下，METIS 報告 **1.8–4.5×** throughput improvement；主要系統評測使用 NVIDIA A40，另有 Llama 3.1 70B 等補充實驗。

上述數字只適用於論文的 workloads、models、hardware 與 quality constraints，不能直接外推到任意 production RAG。

## Scope / Boundary
METIS 補的是 D14 中原本缺失的 **RAG-specific serving / scheduling / configuration adaptation**。它不是：
- general-purpose KV-cache algorithm；
- retrieval relevance algorithm 本身；
- RAG security / privacy / ACL 系統；
- observability / tracing framework。

因此 KIVI / CacheGen 仍留 A02 交界，而 METIS 可作 D14 Systems 的直接 primary anchor。

## 對本專案研究領域的意義
- **D14 primary**：RAG serving、quality-latency trade-off、resource-aware scheduling。
- **D05/D06/D07 secondary**：系統調整 retrieval count、query-dependent configuration 與 synthesis/context strategy，但主要 contribution 是 systems optimization。
- 正式出版名稱為 **METIS**；早期 arXiv 工作曾使用 RAGServe 名稱，canonical record 應以 SOSP 2025 正式版本為準。

## Sources
- ACM SOSP 2025: https://doi.org/10.1145/3731569.3764855
- arXiv: https://arxiv.org/abs/2412.10543
- 本地 PDF：目前未存，使用 ACM / arXiv 官方全文。
- [[02 - 研究領域專題 (Research Domains)/Domain 14 - RAG Systems, Robustness & Security|D14 RAG Systems, Robustness & Security]]
