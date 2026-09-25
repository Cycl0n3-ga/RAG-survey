---
paper_id: "Wallat2026_WhenFactsChange"
title: "When Facts Change: Temporal Knowledge Conflict Resolution in LLMs"
authors:
  - "Jonas Wallat"
  - "Wolfgang Nejdl"
  - "Sandipan Sikdar"
year: 2026
publication_year: 2026
venue: "Findings of ACL 2026"
doi: "10.18653/v1/2026.findings-acl.103"
arxiv: null
url: "https://aclanthology.org/2026.findings-acl.103/"
pdf_file: null
tags:
  - paper
  - temporal-conflict
  - context-memory-conflict
  - temporal-rag
  - benchmark
verification_status: "verified"
last_verified: 2026-09-26
artifact_type: "benchmark_paper"
research_questions:
  - "temporal_knowledge_conflict"
  - "context_memory_conflict"
  - "fact_mutability"
  - "temporal_adaptation"
benchmark_ids:
  - "WikiRecentChanges"
metrics:
  - "Factual Accuracy"
  - "Temporal Reasoning Detection"
taxonomy_version: "v2"
taxonomy_home: "D08"
primary_domain: "D08"
secondary_domains:
  - "D13"
paradigm_tags:
  - "temporal_rag"
adjacent_interfaces: []
---

# When Facts Change: Temporal Knowledge Conflict Resolution in LLMs

## 一話摘要 (TL;DR)
本論文研究 **LLM 的 parametric memory 與 inference-time context 因世界事實更新而衝突時，模型是否會用「fact mutability」判斷該相信哪一邊**。它建立可重算的 WikiRecentChanges benchmark；重點是診斷 temporal conflict，而不是提出一個已解決衝突的新 resolver。

## 研究問題

RAG 會把新 context 放到模型面前，但模型內部仍帶著 pretraining 時期的舊知識，因此：

```text
old parametric fact
        ×
new retrieved/context fact
        ↓
context-memory conflict
```

作者進一步區分：
- **context–memory conflict**：context 與模型內部知識衝突；
- **inter-context conflict**：多個 context / retrieved documents 彼此衝突；
- **intra-memory conflict**：模型內部本身存在矛盾知識。

本篇主要聚焦第一種，且衝突來源是 **temporal misalignment**。

## 方法與 Benchmark

WikiRecentChanges 從 Wikidata 建立：
- stable facts；
- recently updated facts；
- true context；
- counterfactual context。

核心設計是交叉比較「fact 是否 mutable」與「context 是否真實」，觀察模型能否在 context 與 memory 衝突時做出合理選擇。

## 主要結果

- 模型對真正已改變的 facts 比 stable facts 更常產生 temporal reasoning。
- 但這種差異 **很少真正傳到 final answer**。
- 顯式要求模型考慮 mutability，會增加它談論時間變化的比例，卻 **不穩定提升 factual accuracy**。
- failure point 與模型尺度有關：較小模型常無法察覺 conflict；較大模型較能辨認，但仍可能不採取正確決策。

## Scope / Trade-offs

- 本篇是 **diagnostic / benchmark paper**，不是新的 conflict-resolution algorithm。
- 它研究的是 temporal context–memory conflict；不能拿來證明 source authority scoring、multi-document credibility arbitration 已被解決。
- 因此在本 taxonomy 中最適合作為 **D08 primary anchor + D13 secondary**。

## 對本專案的意義

D08 應至少拆成三條 Level-2 research tracks：
1. temporal / version alignment；
2. context–memory / inter-context conflict；
3. provenance / authority arbitration。

本篇直接支撐前兩者中的 temporal context–memory conflict，但不充分支撐一般 source-authority resolver。

## Sources

- ACL Anthology: https://aclanthology.org/2026.findings-acl.103/
- Official PDF: https://aclanthology.org/2026.findings-acl.103.pdf
- [[02 - 研究領域專題 (Research Domains)/Domain 08 - Temporal Conflict & Provenance Resolution|D08 Temporal Conflict & Provenance Resolution]]
