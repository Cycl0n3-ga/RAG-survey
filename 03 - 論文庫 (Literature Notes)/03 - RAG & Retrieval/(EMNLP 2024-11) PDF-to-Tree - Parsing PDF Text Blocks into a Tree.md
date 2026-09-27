---
paper_id: "Zhang2024_PDFtoTree"
title: "PDF-to-Tree: Parsing PDF Text Blocks into a Tree"
authors:
  - "Yue Zhang"
  - "Zhihao Zhang"
  - "Wenbin Lai"
  - "Chong Zhang"
  - "Tao Gui"
  - "Qi Zhang"
  - "Xuanjing Huang"
year: 2024
publication_year: 2024
venue: "Findings of EMNLP 2024"
doi: "10.18653/v1/2024.findings-emnlp.628"
arxiv: null
url: "https://aclanthology.org/2024.findings-emnlp.628/"
pdf_file: null
tags:
  - "paper"
  - "document-parsing"
  - "hierarchy"
  - "pdf"
verification_status: "verified"
last_verified: 2026-09-27
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D01"
primary_domain: "D01"
secondary_domains:
  - "D02"
paradigm_tags: []
adjacent_interfaces: []
---

# PDF-to-Tree: Parsing PDF Text Blocks into a Tree

## 一話摘要
PDF-to-Tree 將缺少 reading order 的 PDF text blocks 組織成 section/subsection tree；論文明確以 RAG indexing 需要 hierarchical document structure 作為動機。

## 核心方法
提出 transition-based greedy parser，結合 multimodal features 表示 parser state，逐步建立 document tree。

## 主要結果
官方摘要報告 parser accuracy 93.93%，較 baseline 提升 6.72%。

## Taxonomy
- **D01 primary**：document hierarchy / reading-order structure recovery。
- **D02 secondary**：恢復的 hierarchy 可支援 structure-aware segmentation，但 paper 不直接研究 retrieval-unit policy。

## Sources
- https://aclanthology.org/2024.findings-emnlp.628/
- DOI: https://doi.org/10.18653/v1/2024.findings-emnlp.628
