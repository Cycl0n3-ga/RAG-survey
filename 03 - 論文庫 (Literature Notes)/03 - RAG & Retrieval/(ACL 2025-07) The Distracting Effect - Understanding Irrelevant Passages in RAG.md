---
paper_id: "Amiraz2025_DistractingEffect"
title: "The Distracting Effect: Understanding Irrelevant Passages in RAG"
authors:
  - "Chen Amiraz"
  - "Florin Cuconasu"
  - "Simone Filice"
  - "Zohar Karnin"
year: 2025
publication_year: 2025
venue: "ACL 2025"
doi: "10.18653/v1/2025.acl-long.892"
arxiv: null
url: "https://aclanthology.org/2025.acl-long.892/"
pdf_file: null
tags:
  - paper
  - distractor-robustness
  - irrelevant-passages
  - context-utilization
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

# The Distracting Effect: Understanding Irrelevant Passages in RAG

## 一話摘要
把「irrelevant passage」進一步區分成對特定 query + LLM 真正會造成錯答的 **hard distracting passages**，定義可量化 distracting effect，並用這些 hard distractors 改善 generator robustness。

## Taxonomy
- **D07 primary**：研究的是 supplied retrieved context 如何干擾 generator 的利用行為。
- **D13 secondary**：包含 distracting-effect measurement。
- 這不是 D14 generic robustness；它不是 malicious attack，而是 context-utilization failure。

## Source
- ACL Anthology: https://aclanthology.org/2025.acl-long.892/
