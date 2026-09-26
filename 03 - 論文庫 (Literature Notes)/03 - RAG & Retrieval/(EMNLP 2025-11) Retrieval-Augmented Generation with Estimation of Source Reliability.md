---
paper_id: "Hwang2025_RARAG"
title: "Retrieval-Augmented Generation with Estimation of Source Reliability"
authors:
  - "Jeongyeon Hwang"
  - "Junyoung Park"
  - "Hyejin Park"
  - "Dongwoo Kim"
  - "Sangdon Park"
  - "Jungseul Ok"
year: 2024
publication_year: 2025
venue: "EMNLP 2025"
doi: "10.18653/v1/2025.emnlp-main.1738"
arxiv: "2410.22954"
url: "https://aclanthology.org/2025.emnlp-main.1738/"
pdf_file: null
tags:
  - paper
  - source-reliability
  - multi-source-rag
  - trustworthy-rag
verification_status: "verified"
last_verified: 2026-09-26
artifact_type: "method_paper"
research_questions:
  - "source_reliability_estimation"
  - "multi_source_retrieval"
  - "reliability_aware_aggregation"
benchmark_ids:
  - "Natural Questions"
  - "TriviaQA"
  - "HotpotQA"
metrics:
  - "Accuracy"
taxonomy_version: "v2"
taxonomy_home: "D08"
primary_domain: "D08"
secondary_domains:
  - "D05"
  - "D14"
paradigm_tags: []
adjacent_interfaces: []
---

# Retrieval-Augmented Generation with Estimation of Source Reliability

## 一話摘要 (TL;DR)
RA-RAG 直接處理「**相關 ≠ 可靠**」：它把 documents 依 source 分組，利用跨來源 fact-checking 迭代估計 source reliability，再只從兼具 reliability 與 relevance 的 top-κ sources 取證，最後用 reliability-weighted majority voting 聚合答案。

## 研究背景與問題定義
標準 RAG 通常按 query-document relevance 排名，沒有顯式區分來源可靠度，因此高度相關但錯誤的來源可能主導 retrieval。RA-RAG 將資料庫建模為多來源集合，研究問題是：在不知道來源可靠度的前提下，能否自動估計 reliability，並在 retrieval 與 aggregation 階段真正使用它。

## 核心方法
1. **Source partitioning**：資料依來源 (S_i) 區分，而不是把所有 documents 視為同質 corpus。
2. **Iterative reliability estimation**：由文件生成 fact-checking queries，跨來源產生答案；以加權共識反覆更新每個 source 的 reliability。
3. **κ-RRSS**：只保留兼具高 reliability 與 query relevance 的少量來源，避免逐一詢問所有 sources 的成本。
4. **Weighted Majority Voting (WMV)**：來源的答案依 estimated reliability 加權聚合。

## 主要實驗證據
- **Page 5–6**：以 Natural Questions、TriviaQA、HotpotQA 建立 heterogeneous-source benchmark；同時模擬連續 reliability 分布與 adversary/hammer 極端分布。
- **Page 6**：測試 Llama3-8B-Instruct、Phi3-mini-Instruct、GPT-4o-mini 等模型，並與 Vanilla RAG、Robust RAG、Self-RAG、majority voting、oracle reliability 等比較。
- 論文整體結果顯示 RA-RAG 在 heterogeneous source reliability 的設定下穩定優於不建模來源可靠度的 baselines；此結果應限制在論文的 multi-source reliability 設定，不外推為所有 provenance 問題已解決。

## Scope / Boundary
RA-RAG 提供的是 **source reliability estimation + reliability-aware retrieval/aggregation**。它不直接建模：
- valid time / record time；
- document revision lineage；
- Draft / Approved 等 workflow approval state；
- site / phase / environment 的 applicability scope。

因此它正好補強 D08 的 **Source Reliability / Credibility** track，但不能取代本 repo 的 provenance-time-resolution proposal。

## 對本專案研究領域的意義
- **D08 primary**：提供直接的 source reliability 方法文獻，不再只能以 temporal RAG 旁證 authority/credibility。
- **D05 secondary**：reliability 直接參與 source selection / retrieval。
- **D14 secondary**：可作為 misinformation / untrusted-corpus robustness 的方法交界。

## Sources
- ACL Anthology: https://aclanthology.org/2025.emnlp-main.1738/
- DOI: https://doi.org/10.18653/v1/2025.emnlp-main.1738
- arXiv: https://arxiv.org/abs/2410.22954
- 本地 PDF：目前未存，使用 ACL Anthology / arXiv 官方全文。
- [[02 - 研究領域專題 (Research Domains)/Domain 08 - Temporal Conflict & Provenance Resolution|D08 Temporal Conflict & Provenance Resolution]]
