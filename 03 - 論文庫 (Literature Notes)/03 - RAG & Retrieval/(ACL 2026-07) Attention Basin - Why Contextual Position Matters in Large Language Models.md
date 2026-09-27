---
paper_id: "Yi2026_AttentionBasin"
title: "Attention Basin: Why Contextual Position Matters in Large Language Models"
authors:
  - "Zihao Yi"
  - "Zhenqing Ling"
  - "Delong Zeng"
  - "Haohao Luo"
  - "Zhe Xu"
  - "Wei Liu"
  - "Jian Luan"
  - "Wanxia Cao"
  - "Ying Shen"
year: 2026
publication_year: 2026
venue: "ACL 2026"
doi: "10.18653/v1/2026.acl-long.1198"
arxiv: null
url: "https://aclanthology.org/2026.acl-long.1198/"
pdf_file: null
tags:
  - paper
  - context-ordering
  - positional-bias
  - attnrank
verification_status: "verified"
last_verified: "2026-09-27"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D07"
primary_domain: "D07"
secondary_domains:
  - "D13"
paradigm_tags: []
adjacent_interfaces: []
---

# Attention Basin: Why Contextual Position Matters in Large Language Models

## 一話摘要
研究 LLM 對 structured context items 的位置偏好，並提出 **AttnRank**：先校準模型的 intrinsic positional attention preference，再把重要 retrieved documents 排到更容易被模型利用的位置。

## Taxonomy
- **D07 primary**：evidence ordering / position-aware context construction。
- **D13 secondary**：包含對 positional utilization failure 的系統性分析。
- 這不是 D05 relevance reranking：候選 evidence 已取得，主要 intervention 是送入 generator 前的排列。

## Source
- ACL Anthology: https://aclanthology.org/2026.acl-long.1198/
