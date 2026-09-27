---
paper_id: "Joren2025_SufficientContext"
title: "Sufficient Context: A New Lens on Retrieval Augmented Generation Systems"
authors:
  - "Hailey Joren"
  - "Jianyi Zhang"
  - "Chun-Sung Ferng"
  - "Da-Cheng Juan"
  - "Ankur Taly"
  - "Cyrus Rashtchian"
year: 2025
publication_year: 2025
venue: "ICLR 2025"
doi: null
arxiv: null
url: "https://proceedings.iclr.cc/paper_files/paper/2025/hash/33dffa2e3d2ab74a783d1a8c292f66d9-Abstract-Conference.html"
pdf_file: null
tags:
  - paper
  - sufficient-context
  - evidence-sufficiency
  - guided-abstention
verification_status: "verified"
last_verified: "2026-09-27"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D06"
primary_domain: "D06"
secondary_domains:
  - "D13"
  - "D09"
paradigm_tags: []
adjacent_interfaces: []
---

# Sufficient Context: A New Lens on Retrieval Augmented Generation Systems

## 一話摘要
正式提出 **sufficient context**：把 RAG error 分成「context 本身不足」與「context 已足夠但模型沒有正確利用」，並建立 sufficiency classifier；再用該 signal 做 selective generation / guided abstention。

## Taxonomy
- **D06 primary**：直接 formalize evidence/context sufficiency。
- **D13 secondary**：sufficiency classification 也用來做 error stratification。
- **D09 secondary**：paper 探索 guided abstention，但主要問題仍是 sufficiency assessment。

## Source
- ICLR 2025: https://proceedings.iclr.cc/paper_files/paper/2025/hash/33dffa2e3d2ab74a783d1a8c292f66d9-Abstract-Conference.html
