---
paper_id: "Zhang2026_QOBench"
title: "QO-Bench: Diagnosing Query-Operator-Preserving Retrieval over Typed Event Tuples"
authors:
  - "Mengao Zhang"
  - "Xiang Yang"
  - "Chang Liu"
  - "Tianhui Tan"
  - "Ke-wei Huang"
year: 2026
publication_year: null
venue: "arXiv; accepted to Findings of EMNLP 2026"
doi: "10.48550/arXiv.2606.04646"
arxiv: "2606.04646"
url: "https://arxiv.org/abs/2606.04646"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2026-06) QO-Bench - Diagnosing Query-Operator-Preserving Retrieval over Typed Event Tuples.pdf"
tags:
  - paper
  - benchmark
  - evaluation
  - graph-rag
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "benchmark_paper"
taxonomy_version: "v2"
taxonomy_home: "D13"
primary_domain: "D13"
secondary_domains:
  - "D03"
  - "D05"
  - "D09"
paradigm_tags: []
adjacent_interfaces: []
research_questions:
  - "query-operator-preserving-retrieval"
  - "typed-event-value-preservation"
  - "retrieval-versus-execution-failure-attribution"
benchmark_ids:
  - "QO-Bench"
dataset_ids:
  - "QO-Bench financial-news corpus"
  - "QO-Bench corporate-event tuple gold"
metrics:
  - "Question-level Recall"
  - "Gold-article coverage"
  - "Macro-Precision"
  - "Macro-F1"
---

# QO-Bench: Diagnosing Query-Operator-Preserving Retrieval over Typed Event Tuples

> **版本與閱讀範圍：** arXiv v1 初次提交於 2026-06-03，v2 為 2026-09-08（19 頁）。arXiv 註明 accepted to Findings of EMNLP 2026；截至核對日尚未找到正式 proceedings record，故 publication_year 留 null，不能把 arXiv 年份當正式出版年份。筆記方法與數值依 v2 全文。

## 一話摘要 (TL;DR)
QO-Bench 用有型別的事件 tuple 和確定性答案，診斷 RAG、ReAct RAG、GraphRAG、IE→SQL 在 filter、join、intersection、ordering、count/group 等操作中，是漏掉證據、丟失欄位還是無法執行運算。

## 研究背景與問題定義 (Problem Statement)
許多金融新聞、法律或科學問題表面上是自然語言，實際要求在文本中找出一組紀錄並執行 database-style operators。只取回語義相關 passage 不保證保留角色、日期、類型及交叉事件關係，也不保證 generator 能正確完成 join、交集、排序或計數。論文分開診斷 index-time preservation 和 query-time execution，以避免把這些失敗都算成普通 retrieval relevance 問題。[§1–3, PDF pp.1–5]

## 核心方法與技術架構 (Methodology & Architecture)
QO-Bench 包含 22,984 篇 news articles、614 個經來源佐證的 corporate events、18 個 query templates 及 785 個問題。事件轉為 typed tuples；gold answers 依 tuple 確定性計算，評分以 tuple exact match（日期採主要設定 ±7 天容差）而非 LLM judge。六個 operator families 為 filter/project、role/type、temporal join、ordering、intersection、count/group。比較 RAG、ReAct RAG、GraphRAG 的 local/global query modes、IE→SQL，並加入 long-context oracle 與 no-context floor 作診斷上/下界。[§3–4, PDF pp.3–6]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 4, PDF p.8：** 785 題 stratified sample、Qwen3.6-27B answer model、±7 天日期容差及 question-weighted micro recall 下，overall recall：LC-oracle `52.2%`、RAG `25.2%`、ReAct RAG `23.9%`、GraphRAG-local `0.9%`、GraphRAG-global `3.8%`、IE→SQL `37.9%`。分項差異顯著：GraphRAG-global 在 filter/project 為 `7.3%`、intersection `2.2%`；IE→SQL 在 intersection 為 `50.9%`，但 temporal join `21.1%`。這是特定金融事件語料與 parity protocol 的診斷，不是跨所有 GraphRAG 的排名。
- **Table 18, PDF p.18：** GraphRAG index 中 event date 在 extraction artifacts 可恢復率 `94.8%`，但 community report 只 `30.9%`；firm entity 則 `56.8%→56.4%`。作者據此定位日期欄位在 entity-centric summarization 中流失，而非僅歸因於 query retrieval。
- **Table 12, PDF p.16；Table 19, PDF p.18：** GraphRAG-global 幾乎涵蓋全部 gold articles（依系統設計近 100%），但最終 recall 仍只有 `3.8%`；LC-oracle 即使取得 gold evidence，intersection recall 也僅 `3.9%`，且該類 91 題中 oracle 在 83 題輸出空集合。它們分別揭示值保留和運算執行瓶頸。
- **條件與實驗邊界：** paper 對模型、輸入及 context budget 做 parity；answer model 主設定為 Qwen3.6-27B。18 個模板產生的 785 題使 operator 可控，但不覆蓋真實 query 的全部語言變異；附錄另以 90 題 paraphrase pilot 檢查表面改寫。[§5、Appendix H, PDF pp.6–9, 17]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** typed-event gold 可確定性計分並逐 operator 分析；把 retrieval coverage、field preservation 與 downstream execution 分開，能指出 GraphRAG 即使全量提供 community reports 仍可能在 summarization 丟掉計數／日期等欄位。它是 failure attribution benchmark，不是新 RAG retriever。
- **限制：** corpus 侷限於 public corporate news/event records，結果可能不轉移到事件標準化較弱的領域；模板問題可控但不足以代表真實問法。Gold tuple 仍受來源歧義、日期慣例、事件階段界線和 entity normalization 影響。論文也提醒各 paradigm 有多種實作，結果依模型和匹配條件而變。[Limitations, PDF p.9]
- **比較邊界：** Table 4 統一了特定資料、answer model、±7 天日期容差及評測預算；結論應限定在這套 protocol。GraphRAG-global 的近全量 coverage 是其 corpus/community-report 傳遞方式所致，不能視為一般高品質 retrieval。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 歸類為 **D13 Evaluation & Failure Attribution**；D03 對應抽出的 typed tuple/value preservation，D05 是 candidate coverage，D09 是證據在 context 中時的答案運算。它可作為 D04/D05/D07/D09 方法比較時的邊界案例：語義相關性、圖連通性與 graph summary 完整度不等於 operator-usable evidence；benchmark 的歸屬不應因此被誤當方法論文。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [arXiv:2606.04646 v2、版本歷史與 accepted status](https://arxiv.org/abs/2606.04646)；[arXiv-issued DOI](https://doi.org/10.48550/arXiv.2606.04646)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2026-06) QO-Bench - Diagnosing Query-Operator-Preserving Retrieval over Typed Event Tuples.pdf|開啟本地 PDF 檔案]]。
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(PVLDB 2025-09) In-depth Analysis of Graph-based RAG in a Unified Framework|Unified Analysis]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2026-04) When to Use Graphs in RAG - A Comprehensive Analysis for Graph Retrieval-Augmented Generation|GraphRAG-Bench]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(Findings ACL 2025-07) GeAR - Graph-enhanced Agent for Retrieval-augmented Generation|GeAR]]。
