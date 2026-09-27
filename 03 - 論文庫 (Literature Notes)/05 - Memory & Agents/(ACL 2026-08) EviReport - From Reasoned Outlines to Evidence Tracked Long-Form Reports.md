---
paper_id: "Liu2026_EviReport"
title: "EviReport: From Reasoned Outlines to Evidence Tracked Long-Form Reports"
authors:
  - "Zihan Liu"
  - "Jianhui Li"
  - "Zexin Wang"
  - "Fei Sun"
  - "Jingjing Li"
  - "Zheyuan Li"
  - "Ke Xiang"
  - "Hang Cui"
  - "Houhua Gong"
  - "Changhua Pei"
  - "Gaogang Xie"
year: 2025
publication_year: 2026
venue: "Findings of ACL 2026"
doi: "10.18653/v1/2026.findings-acl.1397"
arxiv: null
url: "https://aclanthology.org/2026.findings-acl.1397/"
pdf_file: null
tags:
  - paper
  - report-generation
  - evidence-tracking
  - gap-aware-retrieval
  - benchmark
verification_status: "verified"
last_verified: 2026-09-27
artifact_type: "method_paper"
benchmark_ids:
  - "EviReportBench"
metrics:
  - "Factual Accuracy"
  - "Factual Coverage"
  - "Visual Evidence Integration"
taxonomy_version: "v2"
taxonomy_home: "D09"
primary_domain: "D09"
secondary_domains:
  - "D06"
  - "D07"
paradigm_tags:
  - "long_form_rag"
  - "citation_aware_rag"
adjacent_interfaces: []

---

# EviReport: From Reasoned Outlines to Evidence Tracked Long-Form Reports

## 一話摘要
EviReport 是 evidence-intensive analytical report generation workflow：先把 corpus evidence 組織為 compact、traceable units 並檢索 query-relevant subgraphs，再建立 hierarchical outline，最後用 **facts-first iterative generation + gap-aware append queries** 補足缺失 evidence。

## 核心方法
1. **Evidence organization & retrieval**：把 corpus evidence 組織成可追溯單元，並將 query-relevant subgraphs 包裝成 retrieval-ready evidence。
2. **Reasoned outline**：reasoning-focused LLM 先建立高階 plan，再由 chat model 細化為具 scope / ordering 的 hierarchical outline。
3. **Facts-first iterative generation**：先抽取可驗證 facts，再依 facts 組文；當 evidence 不足時，以 gap-aware append queries 補充檢索。
4. **EviReportBench**：以 factual accuracy、factual coverage、visual evidence integration 評估 report correctness + completeness。

## 主要實驗證據
在 8 個 data-rich indicator report topics 上，相較 strong baselines，官方摘要報告：
- factual coverage：**2.16×**
- factual accuracy：**+8.9 points**
- visual evidence integration：**+34 points**

## 已移除的舊筆記過度敘述
先前 note 曾把 EviReport 描述成具有「唯一 Source Hash」「Evidence Ledger 核銷」以及「append retrieval 挽回 38% factual gaps」等具體機制/數字。這些說法沒有在已核對的官方摘要與可定位文本中得到足夠支持，因此不再作為本 repo 的 factual claim。

## Scope / Boundary
- **Primary D09**：long-form grounded synthesis。
- **D06 secondary**：gap-aware append queries 與 evidence completeness interface。
- **D07 secondary**：evidence packages/context organization interface。
- 不因多階段流程就自動標 D12；是否屬 action-policy orchestration需另有直接方法證據。

## Sources
- ACL Anthology: https://aclanthology.org/2026.findings-acl.1397/
- DOI: https://doi.org/10.18653/v1/2026.findings-acl.1397
