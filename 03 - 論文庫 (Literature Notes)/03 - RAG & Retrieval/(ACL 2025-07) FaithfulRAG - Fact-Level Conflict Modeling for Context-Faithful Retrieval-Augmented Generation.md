---
paper_id: "Zhang2025_FaithfulRAG"
title: "FaithfulRAG: Fact-Level Conflict Modeling for Context-Faithful Retrieval-Augmented Generation"
authors:
  - "Qinggang Zhang"
  - "Zhishang Xiang"
  - "Yilin Xiao"
  - "Le Wang"
  - "Junhui Li"
  - "Xinrun Wang"
  - "Jinsong Su"
year: 2025
publication_year: 2025
venue: "ACL 2025"
doi: "10.18653/v1/2025.acl-long.1062"
arxiv: null
url: "https://aclanthology.org/2025.acl-long.1062/"
pdf_file: null
tags:
  - paper
  - knowledge-conflict
  - context-parametric-conflict
  - fact-level-resolution
verification_status: "verified"
last_verified: "2026-09-27"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D08"
primary_domain: "D08"
secondary_domains:
  - "D09"
paradigm_tags: []
adjacent_interfaces: []
---

# FaithfulRAG: Fact-Level Conflict Modeling for Context-Faithful Retrieval-Augmented Generation

## 一話摘要
顯式偵測 **parametric knowledge 與 retrieved context** 間的 fact-level conflict，並在生成前對衝突 facts 進行 reasoning / integration，以提高 context-faithful generation。

## Taxonomy
- **D08 primary**：研究問題是 conflict detection + reconciliation。
- **D09 secondary**：resolution 的 downstream 目標是 context-faithful generation。
- 不應放 D07 的 generic “parametric vs retrieved knowledge”；一旦核心問題是兩組 facts 不相容並需決定如何處理，就是 D08。

## Source
- ACL Anthology: https://aclanthology.org/2025.acl-long.1062/
