---
paper_id: "Ouyang2025_OmniDocBench"
title: "OmniDocBench: Benchmarking Diverse PDF Document Parsing with Comprehensive Annotations"
authors:
  - "Linke Ouyang"
  - "Yuan Qu"
  - "Hongbin Zhou"
  - "Jiawei Zhu"
  - "Rui Zhang"
  - "Qunshu Lin"
  - "Bin Wang"
  - "Zhiyuan Zhao"
  - "Man Jiang"
  - "Xiaomeng Zhao"
  - "Jin Shi"
  - "Fan Wu"
  - "Pei Chu"
  - "Minghao Liu"
  - "Zhenxiang Li"
  - "Chao Xu"
  - "Bo Zhang"
  - "Botian Shi"
  - "Zhongying Tu"
  - "Conghui He"
year: 2024
publication_year: 2025
venue: "CVPR 2025"
doi: null
arxiv: "2412.07626"
url: "https://openaccess.thecvf.com/content/CVPR2025/html/Ouyang_OmniDocBench_Benchmarking_Diverse_PDF_Document_Parsing_with_Comprehensive_Annotations_CVPR_2025_paper.html"
pdf_file: null
tags:
  - paper
  - benchmark
  - document-parsing
  - pdf
  - layout
  - ocr
verification_status: "verified"
last_verified: 2026-09-26
artifact_type: "benchmark_paper"
research_questions:
  - "document_parsing_evaluation"
  - "layout_ocr_table_formula_reading_order"
  - "parsing_robustness_across_document_types"
benchmark_ids:
  - "OmniDocBench"
metrics:
  - "End-to-End Parsing Metrics"
  - "Layout Detection Metrics"
  - "OCR / Table / Formula / Reading-Order Metrics"
taxonomy_version: "v2"
taxonomy_home: "D01"
primary_domain: "D01"
secondary_domains:
  - "D13"
paradigm_tags: []
adjacent_interfaces: []
---

# OmniDocBench: Benchmarking Diverse PDF Document Parsing with Comprehensive Annotations

## 一話摘要 (TL;DR)
OmniDocBench 是面向 **PDF document parsing** 的綜合 benchmark，而不是問答 benchmark：它同時評估 layout、OCR、table、formula、reading order 與 end-to-end structured output，直接補上 RAG ingestion 前端「解析品質到底怎麼量」的缺口。

## 研究背景與問題定義
RAG 對 PDF 的下游 retrieval / generation 品質，上限受 ingestion correctness 影響；但舊 benchmark 常只測 layout 或 OCR 單一模組，或只涵蓋單一文件類型。OmniDocBench 因此把不同 document parsers 放在較一致的、多層級 evaluation protocol 下比較。

## Benchmark 設計
- **9 種 PDF document types**，包含 academic papers、textbooks、books、magazines、newspapers、financial reports、slides、exam papers、notes。
- **19 layout categories + 15 attribute labels**。
- 支援三層評測：
  1. end-to-end full-page parsing；
  2. task-specific evaluation（layout / OCR / table / formula / reading order）；
  3. attribute-based evaluation（文件類型與版面/文字/表格屬性）。
- 同時比較 pipeline-based parsers 與 end-to-end VLM-based parsers。

## 對本專案研究領域的意義
- **D01 primary**：這是直接的 parsing/structure benchmark，可用來量化 ingestion error，而不是拿 downstream QA score 反推 parser 好壞。
- **D13 secondary**：提供 parser-level gold/evaluation，適合用在 Gold Parsing → downstream RAG 的 oracle replacement。
- 它不直接回答 chunking、retrieval 或 generation 的最佳方法；parser score 與 end-to-end RAG quality 應分開報告。

## Scope / Limitations
OmniDocBench 是多模態 PDF parsing benchmark。它能測 structured extraction correctness，但不能單獨證明：
- retrieval evidence recall；
- semantic knowledge extraction correctness；
- RAG answer faithfulness；
- production parser latency / cost 在所有硬體上的表現。

## Sources
- CVPR 2025 Open Access: https://openaccess.thecvf.com/content/CVPR2025/html/Ouyang_OmniDocBench_Benchmarking_Diverse_PDF_Document_Parsing_with_Comprehensive_Annotations_CVPR_2025_paper.html
- arXiv: https://arxiv.org/abs/2412.07626
- 本地 PDF：目前未存，使用 CVPR / arXiv 官方全文。
- [[02 - 研究領域專題 (Research Domains)/Domain 01 - Document Ingestion & Structure|D01 Document Ingestion & Structure]]
- [[02 - 研究領域專題 (Research Domains)/Domain 13 - RAG Evaluation & Failure Attribution|D13 RAG Evaluation & Failure Attribution]]
