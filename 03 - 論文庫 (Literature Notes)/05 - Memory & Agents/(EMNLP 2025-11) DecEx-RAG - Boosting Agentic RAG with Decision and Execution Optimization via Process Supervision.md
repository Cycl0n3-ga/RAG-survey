---
paper_id: "Leng2025_DecExRAG"
title: "DecEx-RAG: Boosting Agentic Retrieval-Augmented Generation with Decision and Execution Optimization via Process Supervision"
authors:
  - "Yongqi Leng"
  - "Yikun Lei"
  - "Xikai Liu"
  - "Meizhi Zhong"
  - "Bojian Xiong"
  - "Yurong Zhang"
  - "Yan Gao"
  - "Yiwu"
  - "Yao Hu"
  - "Deyi Xiong"
year: 2025
publication_year: 2025
venue: "EMNLP 2025 Industry Track"
doi: "10.18653/v1/2025.emnlp-industry.99"
arxiv: null
url: "https://aclanthology.org/2025.emnlp-industry.99/"
pdf_file: null
tags:
  - paper
  - agentic-rag
  - process-supervision
  - mdp
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
adjacent_interfaces: []
---

# DecEx-RAG: Decision and Execution Optimization via Process Supervision

## 一話摘要
把 Agentic RAG 形式化成包含 decision-making 與 execution 的 **Markov Decision Process**，用 process-level supervision / policy optimization 學習 task decomposition、dynamic retrieval 與 answer generation。

## Taxonomy
- **D12 primary**：是目前 state → action policy 最直接的 formal anchor。
- 不應因 dynamic retrieval 就改成 D06/D05 primary；其核心是整體 action policy。

## Source
- ACL Anthology: https://aclanthology.org/2025.emnlp-industry.99/
