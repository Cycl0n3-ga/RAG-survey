---
paper_id: "Sun2025_DyGRAG"
title: "DyG-RAG: Dynamic Graph Retrieval-Augmented Generation with Event-Centric Reasoning"
authors: ["Qingyun Sun", "Jiaqi Yuan", "Shan He", "Xiao Guan", "Haonan Yuan", "Xingcheng Fu", "Jianxin Li", "Philip S. Yu"]
year: 2025
publication_year: null
venue: "arXiv"
doi: "10.48550/arXiv.2507.13396"
arxiv: "2507.13396"
url: "https://arxiv.org/abs/2507.13396"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2025-07) DyG-RAG - Dynamic Graph Retrieval-Augmented Generation with Event-Centric Reasoning.pdf"
tags: ["paper", "temporal-qa", "event-graph"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D05"
primary_domain: "D05"
secondary_domains: ["D03", "D04", "D09"]
paradigm_tags: ["graph_rag", "temporal_rag", "multi_hop_rag"]
adjacent_interfaces: []
research_questions: ["event-centric-retrieval", "temporal-evidence-linking", "time-aware-graph-traversal"]
benchmark_ids: ["TimeQA", "TempReason", "ComplexTR"]
dataset_ids: ["TimeQA", "TempReason", "ComplexTR"]
metrics: ["Accuracy", "Recall"]
source_version: arXiv:2507.13396v1
verified_version: arXiv:2507.13396v1
pdf_pages: 18
pdf_sha256: d41a70db49ce29d69ac7cdcde29fe5ea7686ba36aab76cb975f07b17cfb7e164
---

# DyG-RAG: Dynamic Graph Retrieval-Augmented Generation with Event-Centric Reasoning

> **版本與閱讀範圍：** arXiv:2507.13396 v1，2025-07-16 首次提交；已讀官方 HTML 全文並核對官方 PDF。未查得正式出版記錄。原文將時間相近事件連邊作檢索結構；這種邊不應被解讀為已驗證因果關係。

## 一話摘要 (TL;DR)
DyG-RAG 把文件整理成有明確時間錨點的 Dynamic Event Units，透過 event graph 取回有序事件，再以 Time Chain-of-Thought 回答時間 QA。

## 研究背景與問題定義 (Problem Statement)
一般 RAG 以 chunk 為單位，可能把跨句或跨文件的事件次序、時間區間與狀態轉換拆散；靜態知識圖也未必保存事件的時間脈絡。本文研究如何在 temporal QA 中取回及組織可對齊問題時間範圍的事件證據。[§1–2, pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
文件切為 1,200-token chunks、64-token overlap；以 NER 辨識 person／organization／location，抽取 Dynamic Event Units（DEU），每個 DEU 含事件語義與時間錨點。含共同實體且時間相近的 DEUs 形成事件圖。對 query 做時間感知候選檢索及圖遍歷，輸出按時間組織的事件 timeline；Time-CoT prompt 引導模型核對問題時間範圍、時間關係和持續／狀態資訊後生成答案。[§3, pp. 3–5; §4.1, pp. 5–6]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table 2, 本地 PDF p. 10：** TimeQA hard、TempReason L2、ComplexTR golden test 分別含 2,613、5,397、312 題；對應來源文件數 3,159、2,721、112。
- **Table 3, 本地 PDF p. 11：** 統一 Qwen2.5-14B 作圖與生成 backbone、BGE-M3 作檢索 encoder，chunk 1,200 tokens／overlap 64。DyG-RAG 在 TimeQA／TempReason／ComplexTR 的 Accuracy 為 58.78／84.75／55.62，Recall 為 67.02／91.47／69.88。這是本文三個資料集與 token-overlap evaluation protocol 下的結果；不是跨 benchmark 的直接排名。
- **效率與消融：** §4.3–4.5 及 Figures 4–5 比較靜態 KG-RAG、Chunk-RAG，並移除事件 timeline／Time-CoT 的變體；論文稱 DyG-RAG 在三個資料集勝過兩種知識建構基線，完整 timeline 與 Time-CoT 均有幫助。圖表結果未在正文數值表列出，故此處不轉錄圖中近似值。[本地 PDF pp. 12–14]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 事件而非普通 chunk 作為主要時間檢索單位；對時間推論任務提供可檢視的 timeline。比較時統一 backbone、encoder 與 chunk 設定，有助於本文內部的受控對照。
- **限制與代價：** 需先做事件與時間抽取、建立事件圖，再於 query 時遍歷；抽取錯誤或時間錨點缺失可能傳至後續排序與作答。評估限定三個 Wikipedia 衍生 temporal QA benchmark 和特定模型組合，尚不能推廣成任意動態企業資料庫的持續更新能力。
- **比較邊界：** 本文 GraphRAG／LightRAG／HippoRAG 等 baseline 按作者的實作、資料和 Qwen2.5-14B 設定重跑；數值不能與各方法原論文的不同 benchmark 直接比較。此 event graph 的時間鄰近連結是檢索關係，不等於因果標註。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 歸入 **D05 Query Understanding & Retrieval**，secondary D03（event extraction）、D04（event graph representation）、D09（temporal grounded answer）。`temporal_rag` 是 paradigm tag，因方法顯式表達時間條件；D10 仍不適用，本文沒有因此證明 source/index synchronization lifecycle。這篇補足靜態知識圖和時間 QA 之間的 event-level retrieval 機制。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- 原文：[arXiv:2507.13396](https://arxiv.org/abs/2507.13396)（v1 全文及版本紀錄）。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2025-07) DyG-RAG - Dynamic Graph Retrieval-Augmented Generation with Event-Centric Reasoning.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2025-01) Zep - A Temporal Knowledge Graph Architecture for Agent Memory|Zep／Graphiti]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-12) DynaGRAG - Exploring the Topology of Information for Advancing Language Understanding and Generation in Graph Retrieval-Augmented Generation|DynaGRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ACL 2025-07) HybGRAG - Hybrid Retrieval-Augmented Generation on Textual and Relational Knowledge Bases|HybGRAG]]。
