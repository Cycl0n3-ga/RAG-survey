---
paper_id: "Liu2026_A2RAG"
title: "A2RAG: Adaptive Agentic Graph Retrieval for Cost-Aware and Reliable Reasoning"
authors: ["Jiate Liu", "Zebin Chen", "Shaobo Qiao", "Mingchen Ju", "Danting Zhang", "Bocheng Han", "Shuyue Yu", "Xin Shu", "Jinglin Wu", "Dong Wen", "Xin Cao", "Guanfeng Liu", "Zhengyi Yang"]
year: 2026
publication_year: null
venue: "arXiv"
doi: null
arxiv: "2601.21162"
url: "https://arxiv.org/abs/2601.21162"
pdf_file: "Papers/04 - Knowledge & Graph RAG/(arXiv 2026-01) A2RAG - Adaptive Agentic Graph Retrieval for Cost-Aware and Reliable Reasoning.pdf"
tags: ["paper", "evidence-sufficiency", "provenance-map-back"]
verification_status: "verified"
last_verified: "2026-10-02"
artifact_type: "method_paper"
taxonomy_version: "v2"
taxonomy_home: "D06"
primary_domain: "D06"
secondary_domains: ["D05", "D12"]
paradigm_tags: ["graph_rag", "adaptive_rag", "agentic_rag", "multi_hop_rag"]
adjacent_interfaces: []
research_questions: ["evidence_sufficiency", "progressive_retrieval", "provenance_recovery"]
benchmark_ids: ["HotpotQA", "2WikiMultiHopQA"]
dataset_ids: ["HotpotQA", "2WikiMultiHopQA", "FX operations manual QA"]
metrics: ["Recall@2", "Recall@5", "Exact Match", "F1", "LLM calls", "latency"]
---

# A2RAG: Adaptive Agentic Graph Retrieval for Cost-Aware and Reliable Reasoning

> **版本：** arXiv v1 於 2026-01-29 提交，v2 於 2026-06-04 修訂；本地 PDF 及整理依 v2 全文。正式出版版本尚未核得。

## 一話摘要 (TL;DR)
A2RAG 先查局部圖證據，再按需做 bridge discovery 或 PPR fallback，檢查證據充分性並把圖訊號映射回來源文字，以控制多跳檢索成本。

## 研究背景與問題定義 (Problem Statement)
固定檢索策略會在簡單 query 上浪費成本，也可能無法處理困難多跳題；圖抽取亦可能漏掉只存在於原文的細節。A2RAG 研究如何根據當前證據決定是否擴大檢索，並在 KG 不完整時回到 provenance passages。[§I–II, pp. 1–3]

## 核心方法與技術架構 (Methodology & Architecture)
建立 entity/relation seeds 後，採 local-first 檢索，再以 bounded bridge search 連接分散證據；controller 檢查 evidence sufficiency，不足時才提升檢索強度，最後可作一次 structure-aware PPR，將圖訊號映射回原始文字。Verifier/query rewrite 支援回答或在證據不足時 abstain。[§III, pp. 3–5]

## 主要實驗結果與證據 (Empirical Results & Evidence)
- **Table I, p. 7：** 每個公開資料集抽 200 題。HotpotQA 的 EM/F1/R@2/R@5 為 32.2/43.7/62.4/73.6；2WikiMultiHopQA 為 30.0/42.9/58.9/69.2。LightRAG mix 在 HotpotQA EM/F1 較高（33.9/46.5），所以 A2RAG 的優勢主要是 evidence recall，不是所有 QA 指標都最佳。
- **Tables II–III, pp. 7–8：** 多跳子集分別 n=180、n=150。HotpotQA 上 A2RAG vs. IRCoT：16k vs. 30k tokens、2.0 vs. 3.5 calls、2.7s vs. 4.8s；2WikiMultiHopQA：18k vs. 35k tokens、2.3 vs. 4.2 calls、3.2s vs. 5.6s。表中未列硬體，latency 僅適用於本文實作。
- 作者明確表示公開 benchmark 只跑子集，更大規模與更多元語料尚待評估。seed 抽取品質會影響 bridge discovery。[§IV.A–C、§G, pp. 6–10]

## 優勢、限制及 Trade-offs (Strengths, Limitations & Trade-offs)
- **優勢：** 將 sufficiency check、漸進檢索與停止／回答串成控制流程；圖抽取缺漏時可回到 provenance text；同時報 evidence recall、QA、token、calls 和 latency。
- **限制：** 主要 benchmark 是兩個多跳 QA 資料集的小樣本；seed 和 verifier 品質影響流程，稀疏／碎裂圖會削弱結構導航；長期知識更新仍未處理完整。[§G, pp. 9–10]
- **比較邊界：** 主表與效率表的樣本子集不同；延遲沒有硬體條件，不能直接外推為部署成本。

## 對本專案研究領域的實際意義 (Implications for Research Domains)
本 repo 將其歸入 **D06 Evidence Sufficiency & Retrieval Control**，次領域 D05、D12；使用 `graph_rag`、`adaptive_rag`、`agentic_rag`、`multi_hop_rag`。這是 repo mapping。它把「找到相關內容」和「證據足夠回答」分開建模，適合與 D06 retrieval control 文獻對照。

## 原始來源及相關筆記連結 (Sources & Related Notes)
- [arXiv:2601.21162 v2 metadata/full text](https://arxiv.org/abs/2601.21162)；[PDF](https://arxiv.org/pdf/2601.21162)。
- 本地 PDF：[[Papers/04 - Knowledge & Graph RAG/(arXiv 2026-01) A2RAG - Adaptive Agentic Graph Retrieval for Cost-Aware and Reliable Reasoning.pdf|開啟本地 PDF 檔案]]
- 相關筆記：[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(arXiv 2024-10) LightRAG - Simple and Fast Retrieval-Augmented Generation|LightRAG]]、[[03 - 論文庫 (Literature Notes)/04 - Knowledge & Graph RAG/(ICLR 2024-05) Think-on-Graph - Deep and Responsible Reasoning of Large Language Model on Knowledge Graph|ToG]]。
