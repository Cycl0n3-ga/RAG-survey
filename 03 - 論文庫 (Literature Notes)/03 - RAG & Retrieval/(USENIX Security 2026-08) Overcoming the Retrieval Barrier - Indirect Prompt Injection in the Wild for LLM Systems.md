---
paper_id: "Chang2026_RetrievalBarrierIPI"
title: "Overcoming the Retrieval Barrier: Indirect Prompt Injection in the Wild for LLM Systems"
authors:
  - "Hongyan Chang"
  - "Ergute Bao"
  - "Xinjian Luo"
  - "Ting Yu"
year: 2026
publication_year: 2026
venue: "USENIX Security 2026"
doi: null
arxiv: "2601.07072"
url: "https://www.usenix.org/conference/usenixsecurity26/presentation/chang-hongyan"
pdf_file: null
tags:
  - paper
  - rag-security
  - indirect-prompt-injection
  - retrieval-manipulation
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

# Overcoming the Retrieval Barrier: Indirect Prompt Injection in the Wild for LLM Systems

## 一話摘要
這篇把 indirect prompt injection 最難的前置條件——**惡意文件必須先被 retriever 找到**——直接納入 attack design。方法把 malicious content 拆成 retrieval trigger fragment 與 attack fragment，先優化 retrieval，再執行 downstream prompt-injection objective。

## Taxonomy
- **D14 primary — Security & Integrity**。
- 它不是一般 prompt injection：retrieval manipulation 是攻擊成立的必要步驟，因此直接命中 RAG attack surface。
- security benchmark/measurement 仍歸 D13；此篇是 attack method，所以 D14。

## 主要證據
USENIX Security 2026 官方頁面報告，方法在 11 benchmarks、8 embedding models 上達到近 100% retrieval；另展示自然查詢下的 end-to-end RAG/agentic IPI exploits。具體 ASR 僅適用於其 threat model 與實驗條件。

## Source
- USENIX Security 2026: https://www.usenix.org/conference/usenixsecurity26/presentation/chang-hongyan
