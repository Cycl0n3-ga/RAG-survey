---
paper_id: "Wu2026_ReflectiveRAG"
title: "Reflective RAG: Self-Evaluation Driven Strategy Optimization in Agentic Retrieval-Augmented Generation"
authors:
  - "Haiyan Wu"
  - "Chenchen Wang"
  - "Chaoqun Sun"
  - "Chengxiong Lu"
  - "Yan-Hong Chen"
  - "Zhiqiang Zhang"
  - "Xiaoqing Feng"
year: 2026
publication_year: 2026
venue: "Findings of ACL 2026"
doi: "10.18653/v1/2026.findings-acl.648"
arxiv: null
url: "https://aclanthology.org/2026.findings-acl.648/"
pdf_file: null
tags:
  - paper
  - agentic-rag
  - reflection
  - policy-optimization
verification_status: "verified"
last_verified: "2026-09-27"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D12"
primary_domain: "D12"
secondary_domains: []
paradigm_tags:
  - "agentic_rag"
  - "reflective_rag"
adjacent_interfaces: []
---

# Reflective RAG: Self-Evaluation Driven Strategy Optimization

## 一話摘要
以 reflection tags 評估 retrieved information 的 utility，讓 self-evaluation signal 顯式影響後續 retrieval/generation policy；再透過 SFT + RL 優化 agent strategy。

## Taxonomy
- **D12 primary**：reflection 在此不是單純 critic，而是直接導引 strategy/policy。
- 這與 Self-RAG 的 D06 retrieval-control framing不同。

## Source
- ACL Anthology: https://aclanthology.org/2026.findings-acl.648/
