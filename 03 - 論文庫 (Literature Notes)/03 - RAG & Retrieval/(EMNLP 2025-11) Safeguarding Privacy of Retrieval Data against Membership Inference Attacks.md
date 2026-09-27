---
paper_id: "Choi2025_RAGPrivacyMIA"
title: "Safeguarding Privacy of Retrieval Data against Membership Inference Attacks: Is This Query Too Close to Home?"
authors:
  - "Yujin Choi"
  - "Youngjoo Park"
  - "Junyoung Byun"
  - "Jaewook Lee"
  - "Jinseong Park"
year: 2025
publication_year: 2025
venue: "Findings of EMNLP 2025"
doi: "10.18653/v1/2025.findings-emnlp.438"
arxiv: "2505.22061"
url: "https://aclanthology.org/2025.findings-emnlp.438/"
pdf_file: null
tags:
  - paper
  - rag-privacy
  - membership-inference
  - retrieval-data-leakage
verification_status: "verified"
last_verified: "2026-09-27"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D14"
primary_domain: "D14"
secondary_domains: []
paradigm_tags: []
adjacent_interfaces: []
---

# Safeguarding Privacy of Retrieval Data against Membership Inference Attacks

## 一話摘要
針對 private RAG retrieval database 的 membership inference attack，作者觀察攻擊 query 往往只和單一 target document 呈現異常高相似度，據此建立 similarity-based detection，並用 detect-and-hide 策略隱藏高風險 retrieved data。

## Taxonomy
- **D14 primary — Privacy & Access Control**。
- 這不是單純 benchmark：paper 直接提出 detection + defense framework。
- 它證明 retrieval-data privacy 已有 direct RAG-specific literature；但 tenant isolation、deletion governance 等仍是較薄的線。

## Source
- ACL Anthology: https://aclanthology.org/2025.findings-emnlp.438/
