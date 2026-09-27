---
paper_id: "Gupta2026_EFSG"
title: "EFSG: Evidence-First Structured Generation for Multilingual RAG Report Generation"
authors:
  - "Shaurya Gupta"
  - "Jatin Bedi"
year: 2026
publication_year: 2026
venue: "RAG4Reports 2026"
doi: "10.18653/v1/2026.rag4reports-1.14"
arxiv: null
url: "https://aclanthology.org/2026.rag4reports-1.14/"
pdf_file: null
tags:
  - paper
  - evidence-first
  - multilingual-rag
  - structured-generation
  - report-generation
verification_status: "verified"
last_verified: 2026-09-27
artifact_type: "method_paper"
benchmark_ids:
  - "RAG4Reports-Bench"
metrics:
  - "Factual Support Rate"
  - "Cross-Lingual Consistency"
  - "Hallucination Free Rate"
taxonomy_version: "v2"
taxonomy_home: "D09"
primary_domain: "D09"
secondary_domains:
  - "D07"
paradigm_tags:
  - "long_form_rag"
adjacent_interfaces: []

---

# EFSG: Evidence-First Structured Generation for Multilingual RAG Report Generation

## 一話摘要
EFSG 是 RAG4Reports 2026 Task B submission，核心設計是建立明確 **phase boundary**：在開始生成前先完成 retrieval/extraction，把 evidence 封存成 fact pool；之後每一句生成內容只看到一個已承諾的 source passage，以降低 citation post-rationalization。

## 核心方法
1. **Evidence first**：所有 evidence 先 retrieve / extract，再進入 generation。
2. **Sealed fact pool**：生成開始後不再任意從 parametric memory 補寫未綁定 evidence 的內容。
3. **Single committed source per sentence**：每一句只依指定 source passage 生成，讓 support relationship 更容易審核。

## 官方結果
在作者 best run（t5100k document corpus）：
- `sentence_support = 0.612`
- `nugget_coverage = 0.126`
- `F1 = 0.182`

這些是 ACL Anthology abstract 明確報告的 shared-task results。

## 已移除的舊筆記過度敘述
先前 note 中的 **94.2% support、98.5% hallucination-free、98.7% cross-lingual consistency、100% traceability** 等數值/保證，與官方 paper headline results 不符，因此移除。EFSG 應被理解成一個 evidence-first shared-task system，而不是已證明「完全消除 hallucination」的通用架構。

## Scope / Boundary
- **Primary D09**：evidence-grounded report generation。
- **D07 secondary**：evidence selection/packaging 對 final context 的限制。
- Evidence-first 與 EviReport 的 gap-aware retrieval 可以作設計對照，但不能宣稱它們構成整個領域公認的兩大 canonical paradigms。

## Sources
- ACL Anthology: https://aclanthology.org/2026.rag4reports-1.14/
- DOI: https://doi.org/10.18653/v1/2026.rag4reports-1.14
