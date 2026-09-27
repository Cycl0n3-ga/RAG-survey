---
paper_id: "Shao2024_STORM"
title: "Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models"
authors:
  - "Yijia Shao"
  - "Yucheng Jiang"
  - "Theodore A. Kanell"
  - "Peter Xu"
  - "Omar Khattab"
  - "Monica S. Lam"
year: 2024
publication_year: 2024
venue: "NAACL 2024"
doi: "10.18653/v1/2024.naacl-long.347"
arxiv: "2402.14207"
url: "https://aclanthology.org/2024.naacl-long.347/"
pdf_file: "Papers/05 - Memory & Agents/(NAACL 2024-06) Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models.pdf"
tags:
  - "paper"
  - "agentic-long-form-writing"
verification_status: "verified"
last_verified: 2026-09-27
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D09"
primary_domain: "D09"
secondary_domains:
  - "D12"
  - "D05"
paradigm_tags:
  - "long_form_rag"
adjacent_interfaces: []

---

# Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models

## 一話摘要
STORM（Synthesis of Topic Outlines through Retrieval and Multi-perspective Question Asking）把長篇 grounded article generation 的重點前移到 **pre-writing research + outline construction**：先發現多元觀點，再模擬 writer–expert 對話蒐集具來源依據的資訊，最後整理成大綱後撰寫 Wikipedia-like article。

## 核心方法
1. **Perspective discovery**：從相關 Wikipedia articles / references 中尋找不同研究視角。
2. **Simulated conversations**：writer 以不同 perspective 提問，expert 依可信網路來源回答並保留 citations。
3. **Knowledge curation & outline**：把蒐集資訊整理成 outline，再進行 section-level article generation。

## 主要實驗證據
作者建立 **FreshWiki** 評估近期高品質 Wikipedia articles，並邀請 experienced Wikipedia editors 提供回饋。相較 outline-driven retrieval-augmented baseline：
- 被評為 **organized** 的比例提高 **25 個百分點**；
- 被評為 **broad in coverage** 的比例提高 **10 個百分點**。

目前不採用先前筆記中的「72% win rate」說法，因官方摘要與主要公開敘述不支持把它作為本文 headline result。

## Scope / Boundary
- **Primary D09**：研究目標是 grounded, organized long-form article generation。
- **D12 secondary**：pre-writing research 具有角色化、多步搜尋與互動，但不因此把整篇 paper 改成 orchestration-primary。
- **D05 secondary**：搜尋與檢索支援 pre-writing。
- STORM 支持「research-first / outline-aware long-form generation」；它不證明所有長篇 RAG 都必須採相同 pipeline。

## Sources
- ACL Anthology: https://aclanthology.org/2024.naacl-long.347/
- DOI: https://doi.org/10.18653/v1/2024.naacl-long.347
- arXiv: https://arxiv.org/abs/2402.14207
