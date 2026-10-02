---
paper_id: "Wang2026_WildGraphBench"
title: "WildGraphBench: Benchmarking GraphRAG with Wild-Source Corpora"
authors: ["Pengyu Wang", "Benfeng Xu", "Licheng Zhang", "Shaohan Wang", "Mingxuan Du", "Chiwei Zhu", "Zhendong Mao"]
year: 2026
publication_year: 2026
venue: "Findings of ACL 2026"
doi: "10.18653/v1/2026.findings-acl.679"
arxiv: "2602.02053"
url: "https://aclanthology.org/2026.findings-acl.679/"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2026-02) WildGraphBench - Benchmarking GraphRAG with Wild-Source Corpora.pdf"
tags: ["paper", "wild-source-corpus", "benchmark"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "benchmark_paper"
taxonomy_version: "v2"
taxonomy_home: "D13"
primary_domain: "D13"
secondary_domains: ["D05", "D07", "D09"]
paradigm_tags: ["graph_rag"]
adjacent_interfaces: []
research_questions: ["in_the_wild_evaluation", "multi_source_evidence_aggregation", "long_context_retrieval", "summary_coverage"]
benchmark_ids: ["WildGraphBench"]
dataset_ids: ["WildGraphBench"]
metrics: ["Accuracy", "Statement Precision", "Statement Recall", "Statement F1"]
source_version: arXiv:2602.02053v2
verified_version: arXiv:2602.02053v2
pdf_pages: 18
pdf_sha256: 7b28df826bd5dd2430deec1fa9e629d1051e1c89af8760f7dc09d72d18f95d71
---

# WildGraphBench: Benchmarking GraphRAG with Wild-Source Corpora

> **版本界線：** ACL Anthology 正式版為 Findings ACL 2026，頁 13875–13890；本地全文是 arXiv v2（2026-02-03）。正式版 PDF 下載端點本次逾時，因此數據依 arXiv v2 頁碼，正式版差異待比對。ACL 摘要將題數概述為 1,100；arXiv v2 的 Table 1 明列 1,197 題。

## 一話摘要 (TL;DR)
WildGraphBench 以 Wikipedia 引文所連結的異質外部來源建構 1,197 題，補測 GraphRAG 在長文件、多來源證據聚合與 section summary 的表現。

## 研究背景與問題定義 (Problem Statement)
常見 GraphRAG benchmark 使用整理過的短段落，較少反映真實來源中長篇、異質、帶雜訊的網頁與 PDF；只要拼接少數已裁切 passage 就能答題，也可能高估多文件推理能力。此工作建 benchmark 測試單一事實檢索、多來源事實聚合及段落層級綜述。[§1–3, pp. 1–5]

## 核心方法與技術架構 (Methodology & Architecture)
作者抽取 12 個 Wikipedia 主題文章及其 reference URL，保留所抓取來源的原始文字與噪訊，並以 citation-linked statements 作為 gold facts。題型分 single-fact、multi-fact、leaf-section summary；multi-fact 僅保留需要至少兩個來源共同支持的 statement。summary 採 statement-level precision/recall/F1，單題 QA 則由 LLM judge 判斷回答是否與 gold statement 等價。[§3.1–3.5, pp. 3–5]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 1, arXiv v2 p. 5：** 資料集共有 1,197 題：667 single-fact、191 multi-fact、339 summary。
- **Table 2, arXiv v2 p. 6：** NaiveRAG 的 single-fact accuracy 為 66.87，HippoRAG2 為 71.51；multi-fact accuracy 為 HippoRAG2 39.27、Microsoft GraphRAG global 47.64、LightRAG hybrid 40.84；summary F1 各方法均不高，NaiveRAG 為 15.84、LightRAG hybrid 為 14.61。作者總結圖方法在多來源聚合有幫助，但 summary 仍可能犧牲細節覆蓋。
- **設定：** 預切 chunk size 1,200 tokens、overlap 100；QA top-k=5，summary top-k=10；GPT-4o-mini 用於建圖與作答、GPT-5-mini 擔任 judge；比較 NaiveRAG、BM25、Fast-GraphRAG、Microsoft GraphRAG local/global、LightRAG、LinearRAG、HippoRAG2。論文未報硬體型號。[§4.1–4.2, pp. 6–7]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 來源雜訊和長度更接近實際外部資料；以引文聲明形成可追溯 gold evidence，且把回答正確性與 summary 覆蓋拆開量測。
- **限制與代價：** 資料以 Wikipedia 引用來源建成，受其引用模式、可抓取來源和抽取模型影響；自動生成問題與 LLM-as-judge 仍可能引入偏差；圖索引在細節 summary 上未必保留全部低階事實。
- **比較邊界：** 表 2 是本文 arXiv v2 的任務、提示與 judge 條件；不能直接與其他 benchmark 的分數比較。ACL 正式版是否修改數據待核。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
歸入 **D13 Evaluation & Failure Attribution**，次領域 D05/D07/D09。它補上 curated multi-hop QA 以外的外部長文件測試，可和 GraphRAG-Bench 的 controlled Novel/Medical corpus 配對閱讀；兩者資料來源與任務定義不同，分數不可併表直接排名。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [ACL Anthology 正式 metadata、摘要、DOI 與頁碼](https://aclanthology.org/2026.findings-acl.679/)；[arXiv:2602.02053 v2（全文）](https://arxiv.org/abs/2602.02053)。預印 v1 日期為 2026-02-02，v2 為 2026-02-03。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2026-02) WildGraphBench - Benchmarking GraphRAG with Wild-Source Corpora.pdf|開啟本地 arXiv v2 PDF]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2026-04) When to Use Graphs in RAG - A Comprehensive Analysis for Graph Retrieval-Augmented Generation|GraphRAG-Bench]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-10) LightRAG - Simple and Fast Retrieval-Augmented Generation|LightRAG]]。
