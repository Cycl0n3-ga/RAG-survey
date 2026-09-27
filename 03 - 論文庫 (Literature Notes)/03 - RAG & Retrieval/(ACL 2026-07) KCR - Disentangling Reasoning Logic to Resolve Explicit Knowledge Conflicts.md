---
paper_id: "Zheng2026_KCR"
title: "Disentangling Reasoning Logic to Resolve Explicit Knowledge Conflicts"
authors:
  - "Xianda Zheng"
  - "Zijian Huang"
  - "Meng-Fen Chiang"
  - "Jiamou Liu"
  - "Yuan Fang"
  - "Michael J. Witbrock"
  - "Kaiqi Zhao"
year: 2026
publication_year: 2026
venue: "ACL 2026"
doi: "10.18653/v1/2026.acl-long.1451"
arxiv: null
url: "https://aclanthology.org/2026.acl-long.1451/"
pdf_file: null
tags:
  - paper
  - knowledge-conflict
  - conflict-resolution
  - reasoning-logic
verification_status: "verified"
last_verified: "2026-09-27"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D08"
primary_domain: "D08"
secondary_domains: []
paradigm_tags: []
adjacent_interfaces: []
---

# KCR: Disentangling Reasoning Logic to Resolve Explicit Knowledge Conflicts

## 一話摘要
KCR 將互相矛盾的 retrieved contexts 拆成不同 reasoning traces，以 textual + graph representations disentangle 邏輯，再用 RL with Verifiable Rewards 強化一致的推理路徑並抑制來自 contradiction 的 spurious reasoning。

## Taxonomy
- **D08 primary**：直接做 explicit knowledge-conflict adjudication。
- 使用 graph representation 是 conflict-resolution machinery，不足以把 D04 設為 primary。

## Source
- ACL Anthology: https://aclanthology.org/2026.acl-long.1451/
